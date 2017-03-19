# 并发编程

## 一、进程（Process）

## 二、线程（Thread）

## 三、GCD

## 四、Operation Queue

## 五、RunLoop

### 什么是 RunLoop
Run Loop 本质上就是一个事件处理循环。

### RunLoop 与线程的关系
- 每个线程都自带一个 RunLoop 对象
- 主线程自动配置和启动 RunLoop
- 非主线程需手动启动 RunLoop

### RunLoop 对象
- NSRunLoop（Foundation层）
- CFRunLoop（Core Foundation层）

### event, source, handler
> A run loop receives events from two different types of sources.

source 分两类：
- Input sources - 分发异步事件
- Timer sources - 分发同步事件

## 参考资料
- [Threading Programming Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/Multithreading/Introduction/Introduction.html) by apple
- [Concurrency Programming Guide](https://developer.apple.com/library/content/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html) by apple
