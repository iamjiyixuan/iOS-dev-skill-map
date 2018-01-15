# 理解 Objective-C 的类与对象

## 1. 定义类

SimpleClass.h
``` Objective-C
@interface SimpleClass : NSObject

// 属性
@property NSString *someProperty;

// 方法
- (void)someMethod;
 
@end
```

SimpleClass.m
``` Objective-C
#import "SimpleClass.h"
 
@implementation SimpleClass

- (void)someMethod
{
    // do something...
}

@end
```

## 2. References
- [Programming with Objective-C](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html)