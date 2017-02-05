# C 语言

## 一、如何学习 C 语言

推荐先阅读陈皓的[如何学好C语言](http://coolshell.cn/articles/4102.html)这篇文章，作者已经给出了非常好的建议。我会在此基础上进行细化与补充。

### 第一阶段：搭建开发环境

我最推荐的方案是：macOS + Xcode

#### 开发环境需要包括什么
- 操作系统（这里指的是你写代码的工作环境而不是你所写程序的运行环境）
  - macOS（推荐）
  - Windows
- 文本编辑器
- 编译器
  - GCC
  - Clang
- 调试器（非必需）
  - gdb
  - lldb
- 构建工具（非必需）
  - make

#### 什么是 IDE
IDE，全称 Integrated Development Environment，即集成开发环境，它是文本编辑器、编译器、调试器等组件的集合。常用的支持 C 语言开发的 IDE 有：
- macOS 环境
  - Xcode
  - CodeRunner（收费）
- Windows 环境
  - Visual Studio
- 跨平台
  - Eclipse IDE for C/C++

#### DIY 开发环境（不建议新手这样做，老实用 IDE 就好了）

如果你不喜欢 IDE，比如你不喜欢 Xcode 的文本编辑器想用 Vim，而 Xcode 的 Vim 插件又用着不爽。这时你可能需要搭建一个可以高度自定义的开发环境。
- 方案一
  - 操作系统：macOS
  - 终端：iTerm2 + oh-my-zsh
  - 文本编辑器：Vim
  - 编译器：Clang
  - 构建工具：make

### 第二阶段：熟悉基本语法

C 语言的语法不算复杂，建议快速的过一遍，现阶段做到大致了解，能够看懂别人写的示例程序即可。关于学习资料，我推荐：
- 如果你习惯看书，这一阶段建议看[《C程序设计语言》](https://book.douban.com/subject/1139336/)这一本就可以了，C 语言之父编写的书，几乎是学习 C 语言必读的。这类经典的书比较适合精度，随着你经验慢慢积累水平不断提高 ，需要时不时拿出来温习，温故而知新。
- 如果你的英文水平尚可，我再推荐一个英文在线教程 [C Tutorial](https://www.tutorialspoint.com/cprogramming/index.htm)，内容比较浅，每一章节篇幅都很短，适合快速阅读。
- 此外，[C reference](http://en.cppreference.com/w/c) 可以当做手册来查阅。

C 程序一般包含以下部分：
- 预编译指令（Preprocessor Commands）
- 变量（Variables）
- 函数（Functions）
- 语句（Statements）
- 表达式（Expressions）
- 结构（Structure）
- 注释（Comments）

我们先来看一段简单的代码，它的运行结果就是在控制台输出一段文本：
```
#include <stdio.h>

int main(int argc, const char * argv[])
{
    /* my first program in C */
    const char * str = "Hello, World!\n";
    printf("%s", str);

    return 0;
}
```

Xcode 8 环境执行结果：
```
Hello, World!
Program ended with exit code: 0
```

简单解释一下：
- `#include` 是一个预编译指令，表示引入 `stdio.h` 这个头文件。
- `int main () { ... }` 是一个函数，`{}` 中括起来的部分就是函数具体做的事情。`main` 函数是所有 C 程序的入口函数，它有两个参数 `argc` 和 `argv`。这两参数现阶段还用不到，暂时不做解释。
- `/* my first program in C */` 是注释，不会影响程序的运行结果。
- `str` 是变量，这里表示一个字符串，字符串的内容是“Hello, World!\n”。`\n` 是换行符。
- `const char * str = "Hello, World!\n";` 是一个语句，语句必须用 `;` 分割。
- `printf` 也是一个函数，其功能就是在控制台输出文本。

### 第三阶段：掌握常用的标准库函数

### 第四阶段：深入理解指针和内存管理

#### 内存管理
- 内存区域
  - 栈（stack）
  - 堆（heap）
  - 静态区：全局变量、静态变量、字符串常量等
  - 代码区：存放程序执行代码
- 相关函数
  - malloc
  - calloc
  - realloc
  - free

### 第五阶段：算法与数据结构

### 第六阶段：系统编程

### 第七阶段：系统设计

## 二、make 与 makefile

- [GNU Make Manual](https://www.gnu.org/software/make/manual/make.html)
- [跟我一起写 Makefile](http://blog.csdn.net/haoel/article/details/2886) by 陈皓 2004

## 参考资料
### 网站
[cppreference.com](http://zh.cppreference.com/w/首页)

### 书籍
0. [《C程序设计语言》](https://book.douban.com/subject/1139336/) by Brian W. Kernighan, Dennis M. Ritchie
0. [《C和指针》](https://book.douban.com/subject/3012360/) by Kenneth A.Reek
0. [《C专家编程》](https://book.douban.com/subject/2377310/) by Peter Van Der Linden
0. [《C陷阱与缺陷》](https://book.douban.com/subject/2778632/) by Andrew Koenig

### 文章
0. [如何学好C语言](http://coolshell.cn/articles/4102.html) by CoolShell 陈皓 2011
0. [深入理解C语言](http://coolshell.cn/articles/5761.html) by CoolShell 陈皓 2011
0. [C语言的演变史](http://coolshell.cn/articles/1984.html) by CoolShell 陈皓 2009
0. [C语言-内存管理基础](http://www.jianshu.com/p/b2380e47d005) by 简书 CoderYQ 2017
0. [C语言-内存管理深入](http://www.jianshu.com/p/ccb337572498) by 简书 CoderYQ 2017
