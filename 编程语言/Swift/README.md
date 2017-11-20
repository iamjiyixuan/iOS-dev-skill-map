# Swift

## 1. 变量 & 常量

`let` 声明常量，`var` 声明变量。

``` Swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

声明常量或变量时可以指定类型（一般不需要）
``` Swift
var welcomeMessage: String = "Hello"
```

## 2. 基本数据类型

## 3. 操作符

## 4. 字符串

## 5. 集合类型

### 5.1. 数组 Array

``` Swift
// 创建数组
let strarr = ["a", "b", "c"] // ["a", "b", "c"]

let strarr:[String] = [] // []，创建空数组有多种写法，推荐这种最简洁的写法
let strarr = [String]() // []
let strarr: Array<String> = Array() // []

let strarr = Array(repeating:"", count:3) // ["", "", ""]

// 合并数组
let strarr1 = ["a", "b", "c"]
let strarr2 = ["d", "e", "f"]
let strarr3 = strarr1 + strarr2 // ["a", "b", "c", "d", "e", "f"]

// 数组判空
[].isEmpty // 官方推荐使用 isEmpty 不要使用 count==0

// 添加、删除元素
```

### 5.2. 集合 Set

#### 5.2.1. 有序集合 SortedSet

### 5.3. 字典 Dictionary

### 5.4. 写时复制特性（copy-on-write）

## 6. 控制流

## 7. 函数

## 8. 闭包

## 9. 类 & 结构体 & 对象

## 10. 错误处理 Error Handling

## 11. 编码风格
- [GitHub's Swift Style Guide](https://github.com/github/swift-style-guide)
- [SwiftLint](https://github.com/realm/SwiftLint)

## 12. 参考资料

- [Swift 官网](https://swift.org)
- [The Swift Programming Language (Swift 4 Edition)](https://swift.org/documentation/TheSwiftProgrammingLanguage(Swift4).epub)
- [The Swift Programming Language 中文版](https://github.com/numbbbbb/the-swift-programming-language-in-chinese) 目前已经更新到 Swift 3.0。 2016-09-23
- [《Swifter - Swift 开发者必备 Tips》](https://objccn.io/products/swifter-tips)
- [《Swift 进阶》](https://objccn.io/products/advanced-swift/)
- [《函数式 Swift》](https://objccn.io/products/functional-swift/)
- [《集合类型优化》](https://objccn.io/products/optimizing-collections/)
