# 理解 Objective-C Property

@property 是 OC 2.0 新增的一项特性，用于封装对象中的数据。

## 1. @property 的本质是什么？

> @property = ivar（实例变量）+ getter + setter

## 2. 属性特性（property attribute）有哪些？

- 原子性
    - atomic（default）
    - nonatomic

- 内存管理
    - assign
    - strong - ARC 下使用，语义与 retain 相同
    - <del>retain</del> - ARC 下不再使用
    - weak
    - copy
    - unsafe_unretained

- 读写权限
    - readwrite（default）
    - readonly

- 方法名
    - getter=<name>
    - setter=<name>

## 3. 属性的默认特性是什么？

``` Objective-C
// ARC 下，修饰对象。
@property (atomic，strong, readwrite) UIView *view;

// 修饰基本数据类型
@property (atomic，assign, readwrite) int num;
```

## 4. atomic 与 nonatomic 的区别？什么时候用 atomic？

- [What's the difference between the atomic and nonatomic attributes?](https://stackoverflow.com/questions/588866/whats-the-difference-between-the-atomic-and-nonatomic-attributes)

## 5. NSString 为什么建议用 copy？如果用 strong 会有什么问题？

``` Objective-C
@interface TestProperty : NSObject

@property(nonatomic, copy) NSString *testCopyString;
@property(nonatomic, strong) NSString *testStrongString;

@end
```

clang -rewrite-objc 结果

``` C
extern "C" unsigned long OBJC_IVAR_$_TestProperty$_testCopyString;
extern "C" unsigned long OBJC_IVAR_$_TestProperty$_testStrongString;
struct TestProperty_IMPL {
	struct NSObject_IMPL NSObject_IVARS;
	NSString *_testCopyString;
	NSString *_testStrongString;
};

extern "C" __declspec(dllimport) void objc_setProperty (id, SEL, long, id, bool, bool);

// get 函数对比
static NSString * 
_I_TestProperty_testCopyString(TestProperty * self, SEL _cmd) { 
    return (*(NSString **)((char *)self + OBJC_IVAR_$_TestProperty$_testCopyString)); 
}

static NSString * 
_I_TestProperty_testStrongString(TestProperty * self, SEL _cmd) { 
    return (*(NSString **)((char *)self + OBJC_IVAR_$_TestProperty$_testStrongString)); 
}

// set 函数对比
static void 
_I_TestProperty_setTestCopyString_(TestProperty * self, SEL _cmd, NSString *testCopyString) { 
    objc_setProperty (self, _cmd, __OFFSETOFIVAR__(struct TestProperty, _testCopyString), (id)testCopyString, 0, 1); 
}

static void 
_I_TestProperty_setTestStrongString_(TestProperty * self, SEL _cmd, NSString *testStrongString) { 
    (*(NSString **)((char *)self + OBJC_IVAR_$_TestProperty$_testStrongString)) = testStrongString; 
}

```

`objc_setProperty()` 执行过程，详见 [objc-accessors.mm](https://opensource.apple.com/source/objc4/objc4-551.1/runtime/Accessors.subproj/objc-accessors.mm.auto.html)
``` C
void 
objc_setProperty(id self, SEL _cmd, ptrdiff_t offset, id newValue, BOOL atomic, signed char shouldCopy) 
{
    objc_setProperty_non_gc(self, _cmd, offset, newValue, atomic, shouldCopy);
}

void 
objc_setProperty_non_gc(id self, SEL _cmd, ptrdiff_t offset, id newValue, BOOL atomic, signed char shouldCopy) 
{
    bool copy = (shouldCopy && shouldCopy != MUTABLE_COPY); // #define MUTABLE_COPY 2
    bool mutableCopy = (shouldCopy == MUTABLE_COPY);
    reallySetProperty(self, _cmd, newValue, offset, atomic, copy, mutableCopy);
}

static inline void 
reallySetProperty(id self, SEL _cmd, id newValue, ptrdiff_t offset, bool atomic, bool copy, bool mutableCopy)
{
    id oldValue;
    id *slot = (id*) ((char*)self + offset);

    if (copy) {
        newValue = [newValue copyWithZone:NULL];
    } else if (mutableCopy) {
        newValue = [newValue mutableCopyWithZone:NULL];
    } else {
        if (*slot == newValue) return;
        newValue = objc_retain(newValue);
    }

    // 以下代码解释了 atomic 和 nonatomic 的本质区别
    if (!atomic) {
        oldValue = *slot;
        *slot = newValue;
    } else {
        spin_lock_t *slotlock = &PropertyLocks[GOODHASH(slot)];
        _spin_lock(slotlock);
        oldValue = *slot;
        *slot = newValue;        
        _spin_unlock(slotlock);
    }

    objc_release(oldValue);
}
```

验证
``` Objective-C
- (void)test
{
    TestProperty *obj = [TestProperty new];
    NSString *testString = @"test";
    obj.testCopyString = testString;
    obj.testStrongString = testString;
    NSLog(@"testString: %p", testString);
    NSLog(@".testCopyString: %p", obj.testCopyString);
    NSLog(@".testStrongString: %p", obj.testStrongString);
    
    NSMutableString *testMutableString = [NSMutableString stringWithFormat:@"test"];
    obj.testCopyString = testMutableString;
    obj.testStrongString = testMutableString;
    NSLog(@"testMutableString: %p", testMutableString);
    NSLog(@".testCopyString: %p", obj.testCopyString);
    NSLog(@".testStrongString: %p", obj.testStrongString);
}

2017-09-04 22:09:37.143 xctest[60519:6403882] testString: 0x11efe30a0
2017-09-04 22:09:37.144 xctest[60519:6403882] .testCopyString: 0x11efe30a0
2017-09-04 22:09:37.144 xctest[60519:6403882] .testStrongString: 0x11efe30a0

2017-09-04 22:09:37.144 xctest[60519:6403882] testMutableString: 0x7fdab6e1ffb0
2017-09-04 22:09:37.144 xctest[60519:6403882] .testCopyString: 0xa000000747365744
2017-09-04 22:09:37.144 xctest[60519:6403882] .testStrongString: 0x7fdab6e1ffb0
```

## 6. @synthesize 与 @dynamic 的作用是什么？

如果 `@synthesize` 和 `@dynamic` 都不写，编译器会执行 autosynthesis（自动合成），自动生成 ivar、getter 和 setter。

`@synthesize` 告诉编译器属性的 ivar 名称。

``` Objective-C
@implementation SomeClass

// 默认写法，含义是：属性 var 的实例变量名叫做 _var
@syntheszie var = _var;

@end
```
> Xcode 4.4 之前必须要写，之后的版本不用，如果不写编译器会自动生成。

`@dynamic` 告诉编译器属性的 setter 与 getter 方法由用户自己实现，不自动生成。
