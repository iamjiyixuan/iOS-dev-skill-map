# Objective-C Block

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

block 最多的使用场景是作为函数的参数被传递
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

## 2. Block 的数据结构设计

``` C
struct __block_impl {
  void *isa;
  int Flags;
  int Reserved;
  void *FuncPtr;
};

static struct __main_block_desc_0 {
  size_t reserved;
  size_t Block_size;
} __main_block_desc_0_DATA = { 0, sizeof(struct __main_block_impl_0)};

struct __main_block_impl_0 {
  struct __block_impl impl;
  struct __main_block_desc_0* Desc;
  __main_block_impl_0(void *fp, struct __main_block_desc_0 *desc, int flags=0) {
    impl.isa = &_NSConcreteStackBlock;
    impl.Flags = flags;
    impl.FuncPtr = fp;
    Desc = desc;
  }
};
```

## 3. 扩展阅读
- [《Objective-C 高级编程》](https://book.douban.com/subject/24720270/) 第2章 Blocks
- [《Effective Objective-C 2.0》](https://book.douban.com/subject/25829244/) 第6章 块与大中枢派发
- [谈 Objective-C block 的实现](http://blog.devtang.com/2013/07/28/a-look-inside-blocks/) by 唐巧 2013.07
- [objc 中的 block](https://blog.ibireme.com/2013/11/27/objc-block/) by ibireme 2013.11
- [Block 类型变量 - 缓存 HTTP 请求与回调](http://tutuge.me/2015/02/19/Block类型变量-缓存Http请求与回调/) by tutuge 2015.02
- [OC 与 Swift 闭包对比总结](http://www.jianshu.com/p/d0d7b519fec1) by bestswifter 2015.12
- [对 Strong-Weak Dance 的思考](http://www.jianshu.com/p/4ec18161d790) by bestswifter 2016.03
- [神奇的 BlocksKit （一）](https://draveness.me/blockskit-1) by draveness 2016.03
- [神奇的 BlocksKit （二）](https://draveness.me/blockskit-2) by draveness 2016.03
- [iOS 中的 block 是如何持有对象的](https://draveness.me/block-retain-object) by draveness 2016.08
- [浅谈 block（1） - clang 改写后的 block 结构](http://www.desgard.com/block1/) by desgard 2016.08
- [浅谈 block（2） - 截获变量方式](http://www.desgard.com/block2/) by desgard 2016.09
- [深入研究 Block 捕获外部变量和 __block 实现原理](https://halfrost.com/ios_block/) by halfrost 2016.08
- [深入研究 Block 用 weakSelf、strongSelf、@weakify、@strongify 解决循环引用](https://halfrost.com/ios_block_retain_circle/) by halfrost 2016.09
- [如何动态创建 block – JPBlock 扩展原理详解](http://blog.cnbang.net/tech/3332/) by bang 2017.01
- [iOS weak 关键字漫谈](http://mrpeak.cn/blog/ios-weak/) by mrpeak 2017.07
- [Weak-Strong-Dance 真的安全吗？](http://www.jianshu.com/p/737999a30544) by kuailejim 2017.01