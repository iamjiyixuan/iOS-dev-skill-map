# iOS 开发技能图谱

## [编程语言](编程语言/README.md)
- [C](编程语言/C/README.md)
  - 标准库（libc）
  - 指针
  - 内存管理
- [Objective-C](编程语言/Objective-C/README.md)
  - 类与对象
    - NSObject
  - 协议
  - Category
  - Runtime
    - 消息机制
    - Method Swizzling
  - 引用计数
- [C++](编程语言/C++/README.md)
- [Swift](编程语言/Swift/README.md)
- JavaScript
- 汇编语言

## [Cocoa 基础](Cocoa基础/README.md)
- NSString
- NSNumber
- 集合
  - NSArray
  - NSSet
  - NSDictionary
- NSPredicate
- Notification
- KVO

## [UI](UI/README.md)
- 布局
  - frame
  - Auto Layout
    - Cassowary 算法
    - VFL
    - Masonry
- 控件
  - UIView
  - UIButton
  - UITableview
  - UICollectionView
- 转场
- 手势
- 动画

## [网络](网络/README.md)
- HTTP
- XMPP
- RTP
- TCP
- UDP
- TLS/SSL

## [存储](存储/README.md)
- 沙盒机制
- Bundle
- 钥匙串
- SQLite
- 缓存
- 数据格式
  - xml
  - json

## [并发编程](并发编程/README.md)
- 进程
- 线程
- GCD
- OperationQueue
- 锁
- Runloop

## [多媒体](多媒体/README.md)
- 图片
- 音视频
  - AVFoundation

## [LBS](LBS/README.md)

## [架构](架构/README.md)
- 面向对象编程（Object-Oriented Programming）
- 面向切面编程（Aspect-Oriented Programming）
  - Aspects
- 面向协议编程（Protocol-Oriented Programming）
- 函数式编程（Functional Programming）
- 响应式编程（Reactive Programming）
  - ReactiveCocoa
- MVC
- MVVM
- 设计模式
  - 单例
  - 工厂
  - 观察者
- 组件化

## [Hybrid / JS-Native](Hybrid/README.md)
- 对 WEB 前端技术的发展和开发模式应该有基本的认识
  - HTML
  - 1995 年，JavaScript（简称 JS）诞生。
    - JS 的标准化进程 
      - 1996 年，标准化为 ECMAScript（简称 ES），JS 成为 ES 的一种实现，另外的 ES 方言还有 Jscript 和 ActionScript。
      - 2009 年，ES5 标准发布
      - 2015 年，ES6 / ES2015 标准发布。
        - [ES2015 的新特性](https://babeljs.io/learn-es2015/)
    - [廖雪峰的 JavaScript 教程](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000) 适合初学者快速入门。
  - 1996 年，CSS 诞生
    - [Flexbox](https://www.w3.org/TR/css-flexbox-1/)
  - Ajax
    - XMLHttpRequest
  - 2009 年，JavaScript 运行时 [Node.js](https://nodejs.org/en/) 发布
  - 2010 年，MVC 框架 [Backbone.js](http://backbonejs.org) 和 MVVM 框架 [Angular.js](https://angular.io) 发布
  - 2012 年，打包工具 [webpack](https://webpack.github.io) 和自动化工具 [Grunt](https://gruntjs.com) 发布
  - 2013 年，Facebook 发布 [React.js](https://facebook.github.io/react/)，是一套全新的开发模式
    - 核心技术 Virtual DOM
    - 采用 JSX 语法描述界面，需要通过 [Babel](https://babeljs.io) 翻译为标准 JS 代码才能运行在浏览器或 Node 上
    - 组件
    - 状态管理
      - [Flux](http://facebook.github.io/flux/) 架构
      - [MobX](https://mobx.js.org) 架构
      - [Redux](https://github.com/reactjs/redux) 架构
    - 路由
      - [React Router](https://github.com/ReactTraining/react-router)
    - 3rd
      - [awesome-react](https://github.com/enaqx/awesome-react)
      - [React-Bootstrap](https://react-bootstrap.github.io)
  - 2014 年，MVVM 框架 [Vue.js](https://vuejs.org) 发布。2016 年，Vue 2.0 发布。
    - 与 React 一样，也基于 Virtual DOM 技术（但实现上有差异）。
    - 采用模板语法（合法的 HTML）描述界面，相比 JXS 更接近 Web 标准。
    - 组件
    - 状态管理
      - [vuex](https://vuex.vuejs.org/zh-cn/)
    - 路由
      - [vue-router](http://router.vuejs.org/zh-cn/)
    - 3rd
      - [awesome-vue](https://github.com/vuejs/awesome-vue)
      - [element](https://github.com/ElemeFE/element) - 饿了么前端团队出品的基于 Vue 2.0 的组件库。
- 基于 JS-Native 的跨平台方案
  - 2015 年，Facebook 发布基于 React 的移动端开发框架 [React Native](http://facebook.github.io/react-native/)，提出 `Learn once, write anywhere`。
    - 痛点：这种模式下，各平台可以共享大部分业务逻辑代码，但界面层依然需要单独开发。
    - [React Native for Web](https://github.com/necolas/react-native-web)，与 React Native for iOS and Android 是平级关系。
  - 2017 年，阿里发布跨平台用户界面开发框架 [Weex](https://weex.apache.org)，提出 `一次编写，多端运行`，并支持 Vue 语法（可以理解成 Vue Native）。
  - 2017 年 4 月，微软发布基于 React Native 的跨平台开发框架 [ReactXP](https://microsoft.github.io/reactxp/)。
    - 建议使用 [TypeScript](http://www.typescriptlang.org/index.html)

## [软件工程](软件工程/README.md)
- 脚本
  - Shell
  - Ruby
  - Python
  - Perl
  - Node.js
- 包管理
  - CocoaPods
  - Carthage
- 代码管理
  - git
  - svn
- 测试
  - 单元测试
  - 自动化UI测试
  - 卡顿测试
- 持续集成
  - xcodebuild
  - xctool
- 发布
- 热修复
  - JSPatch
- 异常处理
  - 设备日志
  - 深入理解 Crash
  - Hook 技术
  - 第三方服务
- 运营统计
- 任务管理
- 文档

## [逆向工程](逆向工程/README.md)
- 越狱

## [算法与数据结构](算法与数据结构/README.md)

## [安全](安全/README.md)

## [操作系统](操作系统/README.md)
- Unix
  - BSD
- Darwin
- 内核：XNU
- 可执行文件：Mach-O

## [硬件设备](硬件设备/README.md)
- iPhone
  - 4 / 4S
  - 5 / 5C / 5S
  - 6 / 6 Plus / 6S / 6S Plus
  - SE
  - 7 / 7 Plus
- iPad
  - 1, 2, 3, 4
  - Air 1, 2
  - Mini 1, 2, 3, 4
  - Pro

## [职业生涯](职业生涯/README.md)
- 技术人员发展之路
- 工程师文化
- 招聘
