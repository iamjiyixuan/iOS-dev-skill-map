# Swift 4

## 1. 变量 & 常量

``` Swift
// 常量
let maximumNumberOfLoginAttempts = 10

// 变量
var currentLoginAttempt = 0

// 声明常量或变量时可以指定类型，但一般不需要
var welcomeMessage: String = "Hello"
```

## 2. 基本数据类型

## 3. 操作符

## 4. 字符串

## 5. 集合类型

Swift 提供三种基本集合类型：`Array`、`Set` 和 `Dictionary`。各自的特点如下：
- Array - 有序、可重复
- Set - 无序、不重复
- Dictionary - 无序、键值对结构

### 5.1. 数组 Array

``` Swift
// 创建数组
let strarr = ["a", "b", "c"]

// 创建空数组，必须指定类型
let array = [] // !error: empty collection literal requires an explicit type
let strarr:[String] = [] // best
let strarr = [String]()
let strarr: Array<String> = Array()

// 创建带默认值的数组
let strarr = Array(repeating:"", count:3) // ["", "", ""]

// 合并数组
let strarr1 = ["a", "b", "c"]
let strarr2 = ["d", "e", "f"]
let strarr3 = strarr1 + strarr2 // ["a", "b", "c", "d", "e", "f"]

// 数组判空
[].isEmpty // 官方推荐使用 isEmpty，不要使用 [].count==0

// 加元素
var array = ["a"] // ["a"]
array.append("b") // ["a", "b"]
array.append(contentsOf: ["c", "d"]) // ["a", "b", "c", "d"]
array += ["e", "f"] // ["a", "b", "c", "d", "e", "f"]
array.insert("x", at: 2) // ["a", "b", "x", "c", "d", "e", "f"]
array.insert(contentsOf: ["x0", "x1", "x2"], at: 2) // ["a", "b", "x0", "x1", "x2", "x", "c", "d", "e", "f"]

// 删元素
var array = ["a", "b", "c", "d", "e"]
array.removeFirst() // return "a"
array.removeLast() // return "e"
array.remove(at: 1) // return "c"
array.removeAll() // no return

// 改元素
var array = ["a", "b", "c", "d", "e"]
array[0] = "a0" // ["a0", "b", "c", "d", "e"]

// 读元素
let array = ["a", "b", "c", "d", "e"]
let str0 = array[0] // "a"

// 数组切片，返回值类型为 ArraySlice 而不是 Array
let slice1 = array[1...3] // ["b", "c", "d"]
let slice2 = array[1..<array.endIndex] // ["b", "c", "d", "e"]

// 遍历
let array = ["a", "b", "c", "d", "e"]
for item in array {
    // todo
}
for (index, value) in array.enumerated() {
    // todo
}

// 查找元素
let numbers = [0, 1, 10, 100, 1000]
numbers.contains(1) // return true
numbers.contains { (number) -> Bool in number > 10 } // return true
numbers.first { (number) -> Bool in number > 1 } // return 10
numbers.first { (number) -> Bool in number < 0 } // return nil
numbers.index(of: 100) // return 3
numbers.index(of: -1) // return nil
numbers.index { (number) -> Bool in number > 10 } // return 3
```

### 5.2. 集合 Set

#### 5.2.1. 有序集合 SortedSet

### 5.3. 字典 Dictionary

### 5.4. 写时复制特性（copy-on-write）

## 6. 控制流

for-in

while
repeat-while

if

switch

guard

## 7. 函数 Function

## 8. 闭包 Closure

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
