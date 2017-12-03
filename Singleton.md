# Singleton 单例模式

最佳实践
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

线程不安全
``` Objective-C
+ (id)sharedInstance {  
    static id instance = nil;
    if (!instance) {
        instance = [[self alloc] init];
    }
    return instance;
} 
```

线程安全，但性能不如 dispatch_once
``` Objective-C
+ (id)sharedInstance {  
    static id instance = nil;
    @synchronized(self) {
        if (!instance) {
            instance = [[self alloc] init];
        }
    }
    return instance;
} 
```