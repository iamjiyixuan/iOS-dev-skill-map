# Grand Central Dispatch

## 1. 背景知识

### 1.1. 什么是线程安全？[iOS 多线程到底不安全在哪里？](http://www.mrpeak.cn/blog/ios-thread-safety/)
线程安全指一段代码执行过程中不会有其他线程介入。

## 2. GCD 中的三种队列
- main queue：主队列，串行
- global queue：全局队列，并行
- custom queue：自定义队列，通过 dispatch_queue_create 函数创建

``` C
// 串行队列
dispatch_queue_t queue = dispatch_queue_create("com.example.MyQueue", DISPATCH_QUEUE_SERIAL);

// 并行队列
dispatch_queue_t queue = dispatch_queue_create("com.example.MyQueue", DISPATCH_QUEUE_CONCURRENT);
```

## 3. dispatch_once 函数

``` C
typedef long dispatch_once_t;
typedef void (^dispatch_block_t)(void);
typedef void (*dispatch_function_t)(void *);

void dispatch_once(dispatch_once_t *token, dispatch_block_t block);
void dispatch_once_f(dispatch_once_t *token, void *context, dispatch_function_t function);
```

- dispatch_once 是 Objective-C 中实现单例模式的最佳方式
- dispatch_once 是线程安全的，且性能优于 @synchronized
- dispatch_once_t 类型变量必须是 global 或 static 的
- dispatch_once 可能导致死锁

### 3.1. dispatch_once 实现单例，关于单例模式详见[这篇笔记](Singleton.md)
``` Objective-C
+ (nonnull instancetype)sharedInstance {
    static dispatch_once_t onceToken;
    static id instance;
    dispatch_once(&onceToken, ^{
        instance = [[self alloc] init];
    });
    return instance;
}
```

### 3.2. dispatch_once 死锁问题
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

### 3.3. dispatch_once 源码解析
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

## 4. dispatch_sync 函数
``` C
// Submits a block object for execution on a dispatch queue and waits until that block completes.
void dispatch_sync(dispatch_queue_t queue, dispatch_block_t block);
```
- 一次提交一个任务，直到任务完成，才能提交下一个（特别需要注意 GCD 中**任务提交**和**任务执行**和区别）
- 会阻塞当前线程，直到 block 执行完

### 4.1. dispatch_sync 死锁问题

使用 dispatch_sync 向当前队列提交 block 必死锁
``` C
- (void)viewDidLoad {
	dispatch_sync(dispatch_get_main_queue(), ^{
		NSLog(@"I am block...");
	});
}
```

## 5. dispatch_async
``` C
// Submits a block for asynchronous execution on a dispatch queue and returns immediately.
void dispatch_async(dispatch_queue_t queue, dispatch_block_t block);
```
- 提交任务后，不用等任务执行完，就可以提交下一个

> dispatch_sync 和 dispatch_async 控制的是任务提交的过程，而队列类型控制的任务执行的过程。

## 6. dispatch_group

## 7. dispatch_semaphore

## 8. dispatch_after 函数
``` C
// Enqueue a block for execution at the specified time.
void dispatch_after(dispatch_time_t when, dispatch_queue_t queue, dispatch_block_t block);
```
- 延迟提交，不是延迟执行

## 9. 参考资料
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