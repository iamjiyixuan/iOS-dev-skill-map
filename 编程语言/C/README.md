# C 语言

目录
- [一、如何学习 C 语言](#一如何学习-c-语言)
  - [第一阶段：搭建开发环境](#第一阶段搭建开发环境)
  - [第二阶段：熟悉基本语法](#第二阶段熟悉基本语法)
  - [第三阶段：掌握常用的标准库函数](#第三阶段掌握常用的标准库函数)
  - [第四阶段：深入理解指针和内存管理](#第四阶段深入理解指针和内存管理)
  - [第五阶段：算法与数据结构](#第五阶段算法与数据结构)
  - [第六阶段：系统编程](#第六阶段系统编程)
  - [第七阶段：系统设计](#第七阶段系统设计)
- [二、make 与 makefile](#二make-与-makefile)
- [参考资料](#参考资料)

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

C 语言的语法不算复杂，建议快速的过一遍，现阶段做到大致了解，能够看懂别人写的示例程序即可。关于学习资料：
- 如果你习惯看书，这一阶段建议看[《C程序设计语言》](https://book.douban.com/subject/1139336/)这一本就可以了，C 语言之父编写的书，几乎是学习 C 语言必读的。这类经典的书比较适合精度，随着你经验慢慢积累水平不断提高 ，需要时不时拿出来温习，温故而知新。
- 如果你的英文水平尚可，我再推荐一个英文在线教程 [C Tutorial](https://www.tutorialspoint.com/cprogramming/index.htm)，内容比较浅，每一章节篇幅都很短，适合快速阅读。
- 此外，[C reference](http://en.cppreference.com/w/c) 和 [Standard C++ Library reference](http://www.cplusplus.com/reference/) 可以当做手册来查阅。

#### C 程序的组成

C 程序一般包含以下部分：
- 预编译指令（Preprocessor Commands）
- 变量（Variables）
- 函数（Functions）
- 语句（Statements）
- 表达式（Expressions）
- 结构（Structure）
- 注释（Comments）

#### Hello World

我们先来看一段简单的代码，它的运行结果就是在控制台输出 `Hello, World!`：
``` C
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

C 标准库（C standard library，也称 libc）定义了那些我们在写 C 程序时可以直接调用的函数，例如 `printf()` 函数。这些标准库函数被定义在了若干个 `.h` 头文件中。那么问题来了，标准库函数究竟有哪些呢？事实上，这和你选择哪种 C 标准来写代码有关系。所谓的标准其实就是一种规范，只有大家都遵守统一规范才能保证你写的程序可以在别人的机器上正确的运行。而 C 语言是一门相当古老的编程语言，随着时间的推移，它的规范也在不断的改进和扩充。

#### C 标准

不同标准的 C 语言会有不同数量的标准库函数。截止到目前，主要的 C 语言标准有：
- ANSI C / C89 / C90
  - assert.h
  - ctype.h
  - errno.h
  - float.h
  - iso646.h
  - limits.h
  - locale.h
  - math.h
  - setjmp.h
  - signal.h
  - stdarg.h
  - stddef.h
  - stdio.h
  - stdlib.h
  - string.h
  - time.h
  - wchar.h
  - wctype.h
- C99
  - complex.h
  - fenv.h
  - stdbool.h
  - stdint.h
  - tgmath.h
- C11
  - stdalign.h
  - stdatomic.h
  - stdnoreturn.h
  - threads.h
  - uchar.h

现阶段主要需要熟悉 ANSI C 标准库函数。

#### C POSIX library
C POSIX library 是 C 语言的 POSIX 系统下的标准库。包含了一些在 C 语言标准库之外的函数。

> POSIX（ Portable Operating System Interface）是  IEEE 制定的一套标准，定义了操作系统应该为应用程序提供的接口标准。最初设计这套标准的目的是为了提高类 UNIX 环境下应用程序的可移植性。

#### The GNU C Library (glibc)
C 标准库的开源实现。

### 第四阶段：深入理解指针和内存管理

#### 栈内存
- 编译器自动管理（分配与释放）
- 从高地址开始分配，下开口栈，后进先出
- 最大上限预先设置，可能会溢出

``` C
#include <stdio.h>

int main(int argc, const char * argv[])
{
    char a = 'a'; // char 占 1 字节
    char b = 'b';
    printf("%p\n", &a); // 0x7fff5fbff7e7
    printf("%d\n", a);  // 97
    printf("%p\n", &b); // 0x7fff5fbff7e6
    printf("%d\n", b);  // 98
    return 0;
}
```

变量  | 地址 | 值
---- | ---- | ----
a  | 0x7fff5fbff7e7 | 0110 0001
b  | 0x7fff5fbff7e6 | 0110 0010

``` C
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int a = 'a'; // int 占 4 字节
    int b = 'b';
    printf("%p\n", &a); // 0x7fff5fbff7ec
    printf("%d\n", a);  // 97
    printf("%p\n", &b); // 0x7fff5fbff7e8
    printf("%d\n", b);  // 98
    return 0;
}
```

变量  | 地址 | 值
---- | ---- | ----
a  | 0x7fff5fbff7ec | 0110 0001
   | 0x7fff5fbff7eb | 0000 0000
   | 0x7fff5fbff7ea | 0000 0000
   | 0x7fff5fbff7e9 | 0000 0000
b  | 0x7fff5fbff7e8 | 0110 0010
   | 0x7fff5fbff7e7 | 0000 0000
   | 0x7fff5fbff7e6 | 0000 0000
   | 0x7fff5fbff7e5 | 0000 0000

函数中局部变量占用的内存，在函数返回后会被回收
``` C
#include <stdio.h>

void test()
{
    char a = 'a';
    char b = 'b';
    printf("%p\n", &a);
    printf("%d\n", a);
    printf("%p\n", &b);
    printf("%d\n", b);
}

int main(int argc, const char * argv[])
{
    test();
    test();

    return 0;
}

输出结果：
0x7fff5fbff7df
97
0x7fff5fbff7de
98
0x7fff5fbff7df
97
0x7fff5fbff7de
98
```
上述示例说明函数内的局部变量 `a` 和 `b` 在函数返回后就被回收了，`0x7fff5fbff7df` 和 `0x7fff5fbff7de` 这两块内存被循环使用了。

#### 堆内存
- 调用 `malloc` 等函数手动申请，调用 `free` 手动释放

64 位编译器下，各数据类型所占字节大小。
``` C
int main(int argc, const char * argv[])
{
    printf("%lu\n", sizeof(char));      // 1
    printf("%lu\n", sizeof(int));       // 4
    printf("%lu\n", sizeof(float));     // 4
    printf("%lu\n", sizeof(double));    // 8
    printf("%lu\n", sizeof(short));     // 2
    printf("%lu\n", sizeof(long));      // 8
    printf("%lu\n", sizeof(long long)); // 8
    printf("%lu\n", sizeof(void *));    // 8

    return 0;
}
```
> 注：sizeof 是一个运算符而不是函数，编译器在编译时就计算出了 sizeof 的结果。

``` C
int main(int argc, const char * argv[])
{
    void * a = malloc(1 * sizeof(char)); // 指针占 8 字节
    void * b = malloc(4 * sizeof(char));
    void * c = malloc(1 * sizeof(char));
    void * d = malloc(2 * sizeof(char));

    printf("%p\n", &a); // 0x7fff5fbff7e8
    printf("%p\n", &b); // 0x7fff5fbff7e0
    printf("%p\n", &c); // 0x7fff5fbff7d8
    printf("%p\n", &d); // 0x7fff5fbff7d0

    printf("%p\n", a); // 0x100700000
    printf("%p\n", b); // 0x100700010
    printf("%p\n", c); // 0x100700020
    printf("%p\n", d); // 0x100700030

    return 0;
}
```

#### 函数的调用过程

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
