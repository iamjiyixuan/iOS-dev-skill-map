# Effective Objective-C 2.0 读书笔记

## Accustoming Yourself to Objective-C
熟悉 Objective-C

### \# 01. Familiarize Yourself with Objective-C's Roots
了解 Objective-C 语言的起源

Objective-C = C + Runtime

Objective-C 的消息传递机制（Messaging） vs C++ 的函数调用机制（Function calling）
- 消息传递：**运行时**决定方法执行的具体行为
- 函数调用：**编译时**决定方法执行的具体行为
- 思考：Objective-C 和 C++ 分别是如何实现多态的？

```
// Messaging (Objective-C)
Object *obj = [Object new];
[obj performWith:parameter1 and:parameter2];

// Function calling (C++)
Object *obj = new Object();
obj->(parameter1, parameter2);
```

Objective-C 中的数据类型
- 非对象类型，比如 int, float, double
- C 结构体，比如 CGRect
- Objective-C 对象，比如 NSString

Objective-C 的内存模型
- 栈内存：非对象类型、C 结构体、指针
  - 下开口，即高地址往下减
- 堆内存：Objective-C 对象
  - 低地址往上加
- 指针
  - 32位架构下，占4字节
  - 64位架构下，占8字节

```
// 64位环境
int a = 1;
NSString *str1 = @"abc";
NSString *str2 = @"abc";
NSString *str3 = @"xyz";

NSLog(@"%p", str1);  // 0x100001038
NSLog(@"%p", str2);  // 0x100001038
NSLog(@"%p", str3);  // 0x100001058
NSLog(@"%p", &a);    // 0x7fff5fbff80c
NSLog(@"%p", &str1); // 0x7fff5fbff800
NSLog(@"%p", &str2); // 0x7fff5fbff7f8
NSLog(@"%p", &str3); // 0x7fff5fbff7f0
```

### \# 02. Minimize Importing Headers in Headers
在头文件中尽量少引入其他头文件

### \# 03. Prefer Literal Syntax over the Equivalent Methods
多用字面量语法，少用与之等价的方法

### \# 04. Prefer Typed Constants to Preprocessor define
多用类型常量，少用预编译指令

### \# 05. Use Enumerations for States, Options, and Status Codes
使用枚举表示状态、选项和状态码

## Objects, Messaging, and the Runtime
对象、消息和运行时

### \# 6. Understand Properties
理解属性

### \# 7. Access Instance Variables Primarily Directly When Accessing Them Internally
对象内部尽量直接访问实例变量

### \# 8. Understand Object Equality
理解对象相等

### \# 9. Use the Class Cluster Pattern to Hide Implementation Detail
使用类族模式隐藏实现细节

### \# 10. Use Associated Objects to Attach Custom Data to Existing Classes
使用关联对象在既有类上附加自定义数据

### \# 11. Understand the Role of objc_msgSend
理解 objc_msgSend 的作用

### \# 12. Understand Message Forwarding
理解消息转发

### \# 13. Consider Method Swizzling to Debug Opaque Methods
使用 Method Swizzling 调试黑盒方法

### \# 14. Understand What a Class Object Is
理解类对象是什么

## Interface and API Design
接口与 API 设计

### \# 15. Use Prefix Names to Avoid Namespace Clashes
使用前缀避免命名空间冲突

### \# 16. Have a Designated Initializer
提供 Designated Initializer

### \# 17. Implement the description Method
实现 description 方法

### \# 18. Prefer Immutable Objects
尽量使用不可变对象

### \# 19. Use Clear and Consistent Naming
使用清晰并一致的命名方式

### \# 20. Prefix Private Method Names
私有方法命名加前缀

### \# 21. Understand the Objective-C Error Model
理解 Objective-C 的错误模型

### \# 22. Understand the NSCopying Protocol
理解 NSCopying 协议

## Protocols and Categories
协议与分类

### \# 23. Use Delegate and Data Source Protocols for Inter-object Communication
使用委托与数据源协议进行对象间通讯

### \# 24. Use Categories to Break Class Implementations into Manageable Segments

### \# 25. Always Prefix Category Names on Third-Party Classes

### \# 26. Avoid Properties in Categories

### \# 27. Use the Class-Continuation Category to Hide Implementation Detail

### \# 28. Use a Protocol to Provide Anonymous Objects

## Memory Management
### \# 29. Understand Reference Counting
### \# 30. Use ARC to Make Reference Counting Easier
### \# 31. Release References and Clean Up Observation State Only in dealloc
### \# 32. Beware of Memory Management with Exception-Safe Code
### \# 33. Use Weak References to Avoid Retain Cycles
### \# 34. Use Autorelease Pool Blocks to Reduce High- Memory Waterline
### \# 35. Use Zombies to Help Debug Memory- Management Problems
### \# 36. Avoid Using retain Count

## Blocks and Grand Central Dispatch
### \# 37. Understand Blocks
### \# 38. Create typedefs for Common Block Types
### \# 39. Use Handler Blocks to Reduce Code Separation
### \# 40. Avoid Retain Cycles Introduced by Blocks Referencing the Object Owning Them
### \# 41. Prefer Dispatch Queues to Locks for Synchronization
### \# 42. Prefer GCD to performSelector and Friends
### \# 43. Know When to Use GCD and When to Use Operation Queues
### \# 44. Use Dispatch Groups to Take Advantage of Platform Scaling
### \# 45. Use dispatch_once for Thread-Safe Single-Time Code Execution
### \# 46. Avoid dispatch_get_current_queue

## The System Frameworks
### \# 47. Familiarize Yourself with the System Frameworks
### \# 48. Prefer Block Enumeration to for Loops
### \# 49. Use Toll-Free Bridging for Collections with Custom Memory-Management Semantics
### \# 50. Use NSCache Instead of NSDictionary for Caches
### \# 51. Keep initialize and load Implementations Lean
### \# 52. Remember that NSTimer Retains Its Target
