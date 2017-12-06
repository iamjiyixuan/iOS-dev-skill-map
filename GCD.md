# Grand Central Dispatch

<!-- TOC -->

- [1. 背景知识](#1-背景知识)
  - [1.1. 什么是线程安全？](#11-什么是线程安全)
- [2. GCD 中的三种队列](#2-gcd-中的三种队列)
- [3. dispatch_queue_create 创建队列](#3-dispatch_queue_create-创建队列)
- [4. dispatch_once](#4-dispatch_once)
  - [4.1. dispatch_once 导致死锁](#41-dispatch_once-导致死锁)
  - [4.2. dispatch_once 源码解析](#42-dispatch_once-源码解析)
- [5. dispatch_sync 同步提交任务](#5-dispatch_sync-同步提交任务)
  - [5.1. dispatch_sync 导致死锁](#51-dispatch_sync-导致死锁)
- [6. dispatch_async 异步提交任务](#6-dispatch_async-异步提交任务)
- [7. dispatch_barrier](#7-dispatch_barrier)
- [8. dispatch_group](#8-dispatch_group)
- [9. dispatch_semaphore 信号量](#9-dispatch_semaphore-信号量)
- [10. dispatch_after 延迟提交](#10-dispatch_after-延迟提交)
- [11. dispatch_apply](#11-dispatch_apply)
- [12. dispatch_suspend & dispatch_resume](#12-dispatch_suspend--dispatch_resume)
- [13. dispatch_queue_set_specific & dispatch_get_specific](#13-dispatch_queue_set_specific--dispatch_get_specific)
- [14. main thread 和 main queue 有什么区别？](#14-main-thread-和-main-queue-有什么区别)
- [15. 如何判断当前队列是否是主队列？](#15-如何判断当前队列是否是主队列)
  - [15.1. 方法一：React Native 中的实现，使用 dispatch_queue_set_specific 和 dispatch_get_specific 来设置标志](#151-方法一react-native-中的实现使用-dispatch_queue_set_specific-和-dispatch_get_specific-来设置标志)
  - [15.2. 方法二：比对当前队列的 label 与主队列的 label 是否一致](#152-方法二比对当前队列的-label-与主队列的-label-是否一致)
- [16. 参考资料](#16-参考资料)

<!-- /TOC -->

## 1. 背景知识

### 1.1. 什么是线程安全？
线程安全指一段代码执行过程中不会有其他线程介入。[iOS 多线程到底不安全在哪里？](http://www.mrpeak.cn/blog/ios-thread-safety/)

## 2. GCD 中的三种队列
- main queue：主队列，串行
- global queue：全局队列，并行
- custom queue：自定义队列，通过 dispatch_queue_create 函数创建

## 3. dispatch_queue_create 创建队列
``` C
// Creates a new dispatch queue to which blocks can be submitted.
dispatch_queue_t dispatch_queue_create(const char *label, dispatch_queue_attr_t attr);
```
- label 可以为空，也可以重复，为了方便调试需要自己确保其唯一性。可以通过 dispatch_queue_get_label() 函数获取到指定 queue 的 label，但不能通过 label 反查 queue。

``` C
// 创建串行队列
dispatch_queue_t queue = dispatch_queue_create("com.example.myqueue", DISPATCH_QUEUE_SERIAL);

// 创建并行队列
dispatch_queue_t queue = dispatch_queue_create("com.example.myqueue", DISPATCH_QUEUE_CONCURRENT);
```

源码：[queue.c](https://github.com/apple/swift-corelibs-libdispatch/blob/master/src/queue.c)

## 4. dispatch_once

``` C
// Executes a block object once and only once for the lifetime of an application.
void dispatch_once(dispatch_once_t *token, dispatch_block_t block);
```
- dispatch_once 是 Objective-C 中实现单例模式的最佳方式，关于单例模式详见[这篇笔记](Singleton.md)
- dispatch_once 是线程安全的，且性能优于 @synchronized
- dispatch_once_t 类型变量必须是 global 或 static 的
- dispatch_once 可能导致死锁

### 4.1. dispatch_once 导致死锁
[原文链接](http://joeleee.github.io/2017/03/20/011.dispatch_once/)
``` Objective-C
- (void)viewDidLoad {
    [super viewDidLoad];
    [self once1];
}
- (void)once1 {
    NSLog(@"Started dispatch_once1");
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        [self once2];
    });
    NSLog(@"Finished dispatch_once1");
}
- (void)once2 {
    NSLog(@"Started dispatch_once2");
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        [self once1];
    });
    NSLog(@"Finished dispatch_once2");
}
```

### 4.2. dispatch_once 源码解析
源码地址：[once.c](https://github.com/apple/swift-corelibs-libdispatch/blob/master/src/once.c)
```
// 调用过程
dispatch_once → dispatch_once_f → dispatch_once_f_slow
```

_dispatch_once_waiter_t 结构体
``` C
typedef struct _dispatch_once_waiter_s {
	volatile struct _dispatch_once_waiter_s *volatile dow_next;
	dispatch_thread_event_s dow_event;
	mach_port_t dow_thread;
} *_dispatch_once_waiter_t;
```
疑问：
- struct _dispatch_once_waiter_s 为什么用 volatile 修饰？

dispatch_once_f_slow 函数
``` C
DISPATCH_ONCE_SLOW_INLINE
static void
dispatch_once_f_slow(dispatch_once_t *val, void *ctxt, dispatch_function_t func)
{
#if DISPATCH_GATE_USE_FOR_DISPATCH_ONCE
	dispatch_once_gate_t l = (dispatch_once_gate_t)val;

	if (_dispatch_once_gate_tryenter(l)) {
		_dispatch_client_callout(ctxt, func);
		_dispatch_once_gate_broadcast(l);
	} else {
		_dispatch_once_gate_wait(l);
	}
#else
	_dispatch_once_waiter_t volatile *vval = (_dispatch_once_waiter_t*)val;
	struct _dispatch_once_waiter_s dow = { };
	_dispatch_once_waiter_t tail = &dow, next, tmp;
	dispatch_thread_event_t event;

	if (os_atomic_cmpxchg(vval, NULL, tail, acquire)) {
		dow.dow_thread = _dispatch_tid_self();
		_dispatch_client_callout(ctxt, func);

		next = (_dispatch_once_waiter_t)_dispatch_once_xchg_done(val);
		while (next != tail) {
			tmp = (_dispatch_once_waiter_t)_dispatch_wait_until(next->dow_next);
			event = &next->dow_event;
			next = tmp;
			_dispatch_thread_event_signal(event);
		}
	} else {
		_dispatch_thread_event_init(&dow.dow_event);
		next = *vval;
		for (;;) {
			if (next == DISPATCH_ONCE_DONE) {
				break;
			}
			if (os_atomic_cmpxchgv(vval, next, tail, &next, release)) {
				dow.dow_thread = next->dow_thread;
				dow.dow_next = next;
				if (dow.dow_thread) {
					pthread_priority_t pp = _dispatch_get_priority();
					_dispatch_thread_override_start(dow.dow_thread, pp, val);
				}
				_dispatch_thread_event_wait(&dow.dow_event);
				if (dow.dow_thread) {
					_dispatch_thread_override_end(dow.dow_thread, val);
				}
				break;
			}
		}
		_dispatch_thread_event_destroy(&dow.dow_event);
	}
#endif
}
```

## 5. dispatch_sync 同步提交任务
``` C
// Submits a block object for execution on a dispatch queue and waits until that block completes.
void dispatch_sync(dispatch_queue_t queue, dispatch_block_t block);
```
- 提交并执行一个任务，直到任务完成，才能提交下一个。
- 无论是提交到串行队列还是并行队列 dispatch_sync 都不会开辟新的线程而是直接在当前线程中执行，因此会阻塞当前线程直到 block 执行完。
- 什么场景下需要使用 dispatch_sync ？[You use it when you want to execute a block and wait for the results.](https://stackoverflow.com/questions/4607125/using-dispatch-sync-in-grand-central-dispatch)

``` C
- (void)testDispatchSyncUseSerialQueue {
    dispatch_queue_t queue = dispatch_queue_create("com.example.myqueue", DISPATCH_QUEUE_SERIAL);
    dispatch_sync(queue, ^{
        NSLog(@"current thread = %@", [NSThread currentThread]); // current thread = <NSThread: 0x7fbabd800090>{number = 1, name = main}
    });
}

- (void)testDispatchSyncUseConcurrentQueue {
    dispatch_queue_t queue = dispatch_queue_create("com.example.myqueue", DISPATCH_QUEUE_CONCURRENT);
    dispatch_sync(queue, ^{
        NSLog(@"current thread = %@", [NSThread currentThread]); // current thread = <NSThread: 0x7fbabd800090>{number = 1, name = main}
    });
}
```

``` C
- (void)testExample {
    dispatch_queue_t queue = dispatch_queue_create("com.example.myqueue", DISPATCH_QUEUE_SERIAL);
    for (NSInteger index = 0; index < 10; index++) {
        dispatch_async(queue, ^{
            sleep(1);
            NSLog(@"index= %d, current thread = %@", index, [NSThread currentThread]);
        });
    }
    dispatch_sync(queue, ^{
        NSLog(@"end, current thread = %@", [NSThread currentThread]);
    });
}

运行结果：
2017-12-04 10:29:02.633794+0800 xctest[2523:516506] index= 0, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:03.637787+0800 xctest[2523:516506] index= 1, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:04.639562+0800 xctest[2523:516506] index= 2, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:05.644287+0800 xctest[2523:516506] index= 3, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:06.648002+0800 xctest[2523:516506] index= 4, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:07.653095+0800 xctest[2523:516506] index= 5, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:08.655106+0800 xctest[2523:516506] index= 6, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:09.658384+0800 xctest[2523:516506] index= 7, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:10.663733+0800 xctest[2523:516506] index= 8, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:11.668381+0800 xctest[2523:516506] index= 9, current thread = <NSThread: 0x7f982f242af0>{number = 2, name = (null)}
2017-12-04 10:29:11.668592+0800 xctest[2523:516336] end, current thread = <NSThread: 0x7f982df061b0>{number = 1, name = main}

如果这里换成异步队列，只会打印 end, current thread = <NSThread: 0x7f982df061b0>{number = 1, name = main} 然后程序就结束了
```

### 5.1. dispatch_sync 导致死锁

使用 dispatch_sync 向当前队列提交 block 必死锁
``` C
- (void)viewDidLoad {
	dispatch_sync(dispatch_get_main_queue(), ^{
		NSLog(@"I am block...");
	});
}
```

## 6. dispatch_async 异步提交任务
``` C
// Submits a block for asynchronous execution on a dispatch queue and returns immediately.
void dispatch_async(dispatch_queue_t queue, dispatch_block_t block);
```
- 提交任务后，不用等任务执行完，就可以提交下一个

> dispatch_sync 和 dispatch_async 控制的是任务提交的过程，而队列类型控制的任务执行的过程。

## 7. dispatch_barrier
``` C
// Submits a barrier block object for execution and waits until that block completes.
void dispatch_barrier_sync(dispatch_queue_t queue, dispatch_block_t block);

// Submits a barrier block for asynchronous execution and returns immediately.
void dispatch_barrier_async(dispatch_queue_t queue, dispatch_block_t block);
```
- barrier 生效的基本条件是要在同一队列，因此在 global queue 中使用没有任何意义

## 8. dispatch_group

## 9. dispatch_semaphore 信号量
``` C
// Creates new counting semaphore with an initial value.
dispatch_semaphore_t dispatch_semaphore_create(long value);

// Signals, or increments, a semaphore.
long dispatch_semaphore_signal(dispatch_semaphore_t dsema);

// Waits for (decrements) a semaphore.
long dispatch_semaphore_wait(dispatch_semaphore_t dsema, dispatch_time_t timeout);
```

## 10. dispatch_after 延迟提交
``` C
// Enqueue a block for execution at the specified time.
void dispatch_after(dispatch_time_t when, dispatch_queue_t queue, dispatch_block_t block);
```
- 延迟提交，不是延迟执行

## 11. dispatch_apply

## 12. dispatch_suspend & dispatch_resume

## 13. dispatch_queue_set_specific & dispatch_get_specific
``` C
// Sets the key/value data for the specified dispatch queue.
void dispatch_queue_set_specific(dispatch_queue_t queue, const void *key, void *context, dispatch_function_t destructor);

// Returns the value for the key associated with the current dispatch queue.
void * dispatch_get_specific(const void *key);
```

## 14. main thread 和 main queue 有什么区别？

- 每个 app 只能有一个 main thread
- 可以通过 `[NSThread isMainThread]` 来判断当前线程是否是 main thread
- GCD 没有提供 API 直接判断当前队列是否是 main queue
- 派发到 main queue 的任务**必定**在 main thread 上执行
- 执行在 main thread 上的任务**不一定**来自 main queue，也可能来自其他队列

参考：[GCD's Main Queue vs. Main Thread](http://blog.benjamin-encz.de/post/main-queue-vs-main-thread/)

一个非 main queue 执行在 main thread 上的示例：
``` C
- (void)test {
    dispatch_queue_t queue = dispatch_queue_create("io.iamjiyixuan.queue", DISPATCH_QUEUE_SERIAL);
    dispatch_sync(queue, ^{
        NSLog(@"%@", [NSThread currentThread]); // <NSThread: 0x7f8462e00d80>{number = 1, name = main}
        NSLog(@"%s", dispatch_queue_get_label(DISPATCH_CURRENT_QUEUE_LABEL)); // io.iamjiyixuan.queue
    });
}
```

## 15. 如何判断当前队列是否是主队列？
### 15.1. 方法一：React Native 中的实现，使用 dispatch_queue_set_specific 和 dispatch_get_specific 来设置标志
``` C
BOOL RCTIsMainQueue()
{
  static void *mainQueueKey = &mainQueueKey;
  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    dispatch_queue_set_specific(dispatch_get_main_queue(),
                                mainQueueKey, mainQueueKey, NULL);
  });
  return dispatch_get_specific(mainQueueKey) == mainQueueKey;
}

// 借助 RCTIsMainQueue 我们很容易实现确保任务在主队列执行的工具函数 
void RCTExecuteOnMainQueue(dispatch_block_t block)
{
  if (RCTIsMainQueue()) {
    block();
  } else {
    dispatch_async(dispatch_get_main_queue(), ^{
      block();
    });
  }
}
```

### 15.2. 方法二：比对当前队列的 label 与主队列的 label 是否一致
``` C
BOOL XYZIsMainQueue()
{
    return strcmp(dispatch_queue_get_label(DISPATCH_CURRENT_QUEUE_LABEL),
                  dispatch_queue_get_label(dispatch_get_main_queue())) == 0;
}
```
但这种方法存在一个缺陷，由于 label 不是唯一的，如果我们自己创建一个队列，label 设置成和主队列 label 一样，这样还是会出现误判。因此在实际项目中，我更推荐方法一。
``` C
- (void)testFakeMainQueue {
    dispatch_queue_t queue = dispatch_queue_create(dispatch_queue_get_label(dispatch_get_main_queue()),
                                                   DISPATCH_QUEUE_SERIAL);
    dispatch_sync(queue, ^{
        XCTAssertFalse(RCTIsMainQueue()); // 测试通过
        XCTAssertFalse(XYZIsMainQueue()); // 测试不通过
    });
}
```


## 16. 参考资料
- [GCD C API](https://developer.apple.com/documentation/dispatch?language=objc)
- [libdispatch 源码](https://github.com/apple/swift-corelibs-libdispatch)
- [《Effective Objective-C 2.0》]()
    - #41 多用派发队列，少用同步锁
    - #42 多用 GCD，少用 performSelector 系列方法
    - #43 掌握 GCD 及操作队列的使用时机
    - #44 通过 Dispatch Group 机制，根据系统资源状况来执行任务
    - #45 使用 dispatch_once 来执行只需要运行一次的线程安全代码
    - #46 不要使用 dispatch_get_current_queue
- [GCD 使用经验与技巧浅谈](http://tutuge.me/2015/04/03/something-about-gcd/) by tutuge 2015
- [深入理解 GCD](https://bestswifter.com/deep-gcd/) by bestswifter 2016
- [并发编程：API 及挑战](https://objccn.io/issue-2-1/) by objccn
- [常见的后台实践](https://objccn.io/issue-2-2/) by objccn
- [底层并发 API](https://objccn.io/issue-2-3/) by objccn
- [线程安全类的设计](https://objccn.io/issue-2-4/) by objccn
- [测试并发程序](https://objccn.io/issue-2-5) by objccn
- [iOS 知识小集](https://github.com/southpeak/iOS-tech-set) by 南峰子