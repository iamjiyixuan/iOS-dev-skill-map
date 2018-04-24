# Key-Value Coding & Observing

## 1. KVC

### 1.1. API
``` ObjC
@property (nonatomic, copy) NSString *name;

// get
NSString *name = [object valueForKey:@"name"];

// set
[object setValue:@"Daniel" forKey:@"name"];
```

### 1.2. 如何在 Swift 4 中使用 KVC

## 2. KVO

### 2.1. API

### 2.2. 实现原理

### 2.3. KVOController

## 3. References
- [Key-Value Coding Programming Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/KeyValueCoding/)
- [Key-Value Observing Programming Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/KeyValueObserving/KeyValueObserving.html)
- [如何优雅地使用 KVO](https://draveness.me/kvocontroller) by draveness 2017
- [如何自己动手实现 KVO](http://tech.glowing.com/cn/implement-kvo/) by Glow 技术团队博客 2015
- [KVC 和 KVO](https://www.objccn.io/issue-7-3/) by objccn 2014
- [ObjC KVC 简单探索](http://blog.sunnyxx.com/2014/03/09/objc_kvo_secret/) by sunnyxx 2014