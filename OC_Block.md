# 深入理解 Objective-C Block

## 1. 基本用法

定义一个最简单的 block
``` Objective-C
void (^emptyBlock)(void) = ^{
    NSLog(@"do something ...");
};

emptyBlock(); // print do something ...
```

定义带参数和返回值的 block
``` Objective-C
int (^addBlock)(int a, int b) = ^(int a, int b) {
    return a + b;
};

int result = addBlock(1, 2); // result = 3
```

作为函数的参数被传递
``` Objective-C
- (void)testWithBlock:(void (^)(void))block
{
    NSLog(@"1 ...");
    block();
    NSLog(@"3 ...");
}

[self testWithBlock:^{
    NSLog(@"2 ...");
}];

执行结果：
2017-10-03 11:35:12.982009+0800 BlockPlayground[24370:12913141] 1 ...
2017-10-03 11:35:12.982134+0800 BlockPlayground[24370:12913141] 2 ...
2017-10-03 11:35:12.982234+0800 BlockPlayground[24370:12913141] 3 ...
```

## 2. Block 的本质是什么？
- 带有自动变量（局部变量）的匿名函数
- OC 语言对于闭包的实现
- block 实际上也是对象，因为包含 isa 指针

## 3. Block 的数据结构设计

参考 [libclosure](https://opensource.apple.com/tarballs/libclosure/) 源码
``` C
struct Block_descriptor_1 {
    uintptr_t reserved;
    uintptr_t size;
};

struct Block_layout {
    void *isa;
    volatile int32_t flags; // contains ref count
    int32_t reserved; 
    void (*invoke)(void *, ...);
    struct Block_descriptor_1 *descriptor;
    // imported variables
};
```

## 4. Block 的类型
- _NSConcreteGlobalBlock - 全局静态 block，没有用到外界变量或只用到全局变量、静态变量
- _NSConcreteStackBlock - 栈 block
- _NSConcreteMallocBlock - 堆 block

## 5. 扩展阅读
- [libclosure 源码](https://opensource.apple.com/tarballs/libclosure/)
- [《Objective-C 高级编程》](https://book.douban.com/subject/24720270/) 第2章 Blocks
- [《Effective Objective-C 2.0》](https://book.douban.com/subject/25829244/) 第6章 块与大中枢派发
- [谈 Objective-C block 的实现](http://blog.devtang.com/2013/07/28/a-look-inside-blocks/) by 唐巧 2013
- [objc 中的 block](https://blog.ibireme.com/2013/11/27/objc-block/) by ibireme 2013
- [Block 类型变量 - 缓存 HTTP 请求与回调](http://tutuge.me/2015/02/19/Block类型变量-缓存Http请求与回调/) by tutuge 2015
- [OC 与 Swift 闭包对比总结](http://www.jianshu.com/p/d0d7b519fec1) by bestswifter 2015
- [对 Strong-Weak Dance 的思考](http://www.jianshu.com/p/4ec18161d790) by bestswifter 2016
- [神奇的 BlocksKit （一）](https://draveness.me/blockskit-1) by draveness 2016
- [神奇的 BlocksKit （二）](https://draveness.me/blockskit-2) by draveness 2016
- [iOS 中的 block 是如何持有对象的](https://draveness.me/block-retain-object) by draveness 2016
- [浅谈 block（1） - clang 改写后的 block 结构](http://www.desgard.com/block1/) by desgard 2016
- [浅谈 block（2） - 截获变量方式](http://www.desgard.com/block2/) by desgard 2016
- [深入研究 Block 捕获外部变量和 __block 实现原理](https://halfrost.com/ios_block/) by halfrost 2016
- [深入研究 Block 用 weakSelf、strongSelf、@weakify、@strongify 解决循环引用](https://halfrost.com/ios_block_retain_circle/) by halfrost 2016
- [如何动态创建 block – JPBlock 扩展原理详解](http://blog.cnbang.net/tech/3332/) by bang 2017
- [iOS weak 关键字漫谈](http://mrpeak.cn/blog/ios-weak/) by mrpeak 2017
- [Weak-Strong-Dance 真的安全吗？](http://www.jianshu.com/p/737999a30544) by kuailejim 2017