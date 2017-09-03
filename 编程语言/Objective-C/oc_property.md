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

```
// ARC 下，修饰对象。
@property (atomic，strong, readwrite) UIView *view;

// 修饰基本数据类型
@property (atomic，assign, readwrite) int num;
```

## 4. atomic 与 nonatomic 的区别？什么时候用 atomic？

- [What's the difference between the atomic and nonatomic attributes?](https://stackoverflow.com/questions/588866/whats-the-difference-between-the-atomic-and-nonatomic-attributes)

## 5. NSString 为什么建议用 copy？如果用 strong 会有什么问题？



## 6. @synthesize 与 @dynamic 的作用是什么？

如果 @synthesize 和 @dynamic 都不写，编译器会执行 `autosynthesis（自动合成）`，自动添加 ivar、getter 和 setter。

@synthesize 告诉编译器属性的 ivar，并自动生成 setter 与 getter。Xcode4.4 之前必须要写，之后版本不用，现在会默认添加。

```
// 默认
@syntheszie var = _var;
```

@dynamic 告诉编译器属性的 setter 与 getter 方法由用户自己实现，不自动生成。
