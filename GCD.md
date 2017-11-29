# Grand Central Dispatch

## dispatch_once 函数

``` Objective-C
void dispatch_once(dispatch_once_t *predicate, dispatch_block_t block);
```

注意事项：
- dispatch_once_t 必须是 global 或 static 变量

Objective-C 实现单例的标准写法
``` Objective-C
+ (instancetype)sharedInstance
{
    static MyClass *sharedInstance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        sharedInstance = [[MyClass alloc] init];
        // Do any other initialisation stuff here
    });
    return sharedInstance;
}
```

## 参考资料
- [GCD C API](https://developer.apple.com/documentation/dispatch?language=objc)
- [《Effective Objective-C 2.0》]()
    - #41 多用派发队列，少用同步锁
    - #42 多用 GCD，少用 performSelector 系列方法
    - #43 掌握 GCD 及操作队列的使用时机
    - #44 通过 Dispatch Group 机制，根据系统资源状况来执行任务
    - #45 使用 dispatch_once 来执行只需要运行一次的线程安全代码
    - #46 不要使用 dispatch_get_current_queue
- [GCD 使用经验与技巧浅谈](http://tutuge.me/2015/04/03/something-about-gcd/) by tutuge 2015
- [深入理解 GCD](https://bestswifter.com/deep-gcd/) by bestswifter 2016