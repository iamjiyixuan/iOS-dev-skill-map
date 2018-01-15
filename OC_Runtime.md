# Objective-C Runtime

> 本文对应源码版本：[objc4-723](https://opensource.apple.com/tarballs/objc4/objc4-723.tar.gz)

## 1. 理解 Objective-C 的动态特性
C 是静态语言，在编译期，函数的调用就会决定调用哪个函数。而 Objective-C 是动态语言，运行时才根据函数名查找对应的函数实现来执行。

## 2. Runtime 中涉及的几个重要数据结构

### 2.1. NSObject
``` Objective-C
@interface NSObject <NSObject> {
    Class isa  OBJC_ISA_AVAILABILITY;
}
```

### 2.2. Class
``` C
typedef struct objc_class *Class;
```

### 2.3. id
``` C
typedef struct objc_object *id;
```

### 2.4. objc_class
这里很好的解释了为什么 Objective-C 中类也是一个对象
``` C
struct objc_class : objc_object {
    Class superclass;
    const char *name;
    uint32_t version;
    uint32_t info;
    uint32_t instance_size;
    struct old_ivar_list *ivars;
    struct old_method_list **methodLists;
    Cache cache;
    struct old_protocol_list *protocols;
    // CLS_EXT only
    const uint8_t *ivar_layout;
    struct old_class_ext *ext;

    ...
};
```

### 2.5. objc_object
``` C
// objc-private.h
struct objc_object {
private:
    isa_t isa;

    ...
};
```

### 2.6. isa_t
``` C
union isa_t 
{
    isa_t() { }
    isa_t(uintptr_t value) : bits(value) { }

    Class cls;
    uintptr_t bits;

    ...
};
```

## 3. 深入剖析 NSObject 的 alloc 过程

alloc
``` Objective-C
+ (id)alloc {
    return _objc_rootAlloc(self);
}
```

_objc_rootAlloc
``` C
id
_objc_rootAlloc(Class cls)
{
    return callAlloc(cls, false/*checkNil*/, true/*allocWithZone*/);
}
```

callAlloc
``` C
static ALWAYS_INLINE id
callAlloc(Class cls, bool checkNil, bool allocWithZone=false)
{
    if (slowpath(checkNil && !cls)) return nil;

#if __OBJC2__
    if (fastpath(!cls->ISA()->hasCustomAWZ())) {
        // No alloc/allocWithZone implementation. Go straight to the allocator.
        // fixme store hasCustomAWZ in the non-meta class and 
        // add it to canAllocFast's summary
        if (fastpath(cls->canAllocFast())) {
            // No ctors, raw isa, etc. Go straight to the metal.
            bool dtor = cls->hasCxxDtor();
            id obj = (id)calloc(1, cls->bits.fastInstanceSize());
            if (slowpath(!obj)) return callBadAllocHandler(cls);
            obj->initInstanceIsa(cls, dtor);
            return obj;
        }
        else {
            // Has ctor or raw isa or something. Use the slower path.
            id obj = class_createInstance(cls, 0);
            if (slowpath(!obj)) return callBadAllocHandler(cls);
            return obj;
        }
    }
#endif

    // No shortcuts available.
    if (allocWithZone) return [cls allocWithZone:nil];
    return [cls alloc];
}
```

initInstanceIsa
``` C
inline void 
objc_object::initInstanceIsa(Class cls, bool hasCxxDtor)
{
    assert(!cls->instancesRequireRawIsa());
    assert(hasCxxDtor == cls->hasCxxDtor());

    initIsa(cls, true, hasCxxDtor);
}

inline void 
objc_object::initIsa(Class cls, bool nonpointer, bool hasCxxDtor) 
{ 
    assert(!isTaggedPointer()); 
    
    if (!nonpointer) {
        isa.cls = cls;
    } else {
        assert(!DisableNonpointerIsa);
        assert(!cls->instancesRequireRawIsa());

        isa_t newisa(0);

#if SUPPORT_INDEXED_ISA
        assert(cls->classArrayIndex() > 0);
        newisa.bits = ISA_INDEX_MAGIC_VALUE;
        // isa.magic is part of ISA_MAGIC_VALUE
        // isa.nonpointer is part of ISA_MAGIC_VALUE
        newisa.has_cxx_dtor = hasCxxDtor;
        newisa.indexcls = (uintptr_t)cls->classArrayIndex();
#else
        newisa.bits = ISA_MAGIC_VALUE;
        // isa.magic is part of ISA_MAGIC_VALUE
        // isa.nonpointer is part of ISA_MAGIC_VALUE
        newisa.has_cxx_dtor = hasCxxDtor;
        newisa.shiftcls = (uintptr_t)cls >> 3;
#endif

        // This write must be performed in a single store in some cases
        // (for example when realizing a class because other threads
        // may simultaneously try to use the class).
        // fixme use atomics here to guarantee single-store and to
        // guarantee memory order w.r.t. the class index table
        // ...but not too atomic because we don't want to hurt instantiation
        isa = newisa;
    }
}
```

## 4. References
- [Runtime 源码](https://opensource.apple.com/tarballs/objc4/)
- [Objective-C Runtime Programming Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008048)
- [Objective-C Runtime Reference](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ObjCRuntimeRef/index.html)
- [Objective-C Runtime](http://yulingtianxia.com/blog/2014/11/05/objective-c-runtime/) by 杨萧玉 2014
- [神经病院 Objective-C Runtime 入院第一天—— isa 和 Class](https://halfrost.com/objc_runtime_isa_class/) by halfrost 2016
- [神经病院 Objective-C Runtime 住院第二天——消息发送与转发](https://halfrost.com/objc_runtime_objc_msgsend/) by halfrost 2016
- [神经病院 Objective-C Runtime 出院第三天——如何正确使用 Runtime](https://halfrost.com/how_to_use_runtime/) by halfrost 2016
- [Objc 对象的今生今世](https://halfrost.com/objc_life/) by halfrost 2016
- [重识 Objective-C Runtime - Smalltalk 与 C 的融合](http://blog.sunnyxx.com/2016/08/13/reunderstanding-runtime-0/) by sunnyxx 2016
- [重识 Objective-C Runtime - 看透 Type 与 Value](http://blog.sunnyxx.com/2016/08/13/reunderstanding-runtime-1/) by sunnyxx 2016
- [从 NSObject 的初始化了解 isa](https://github.com/Draveness/analyze/blob/master/contents/objc/从%20NSObject%20的初始化了解%20isa.md) by Draveness