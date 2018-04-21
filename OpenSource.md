# 开源项目索引

Index
<!-- TOC -->

- [UI](#ui)
    - [Layout](#layout)
    - [UITableView](#uitableview)
    - [HUD](#hud)
    - [Refresh](#refresh)
    - [Keyboard](#keyboard)
    - [Animation](#animation)
    - [Smooth](#smooth)
    - [Chat](#chat)
    - [Image](#image)
    - [Video](#video)
- [Networking](#networking)
    - [HTTP](#http)
    - [XMPP](#xmpp)
- [SQLite](#sqlite)
- [Cache](#cache)
- [Model](#model)
- [Util](#util)
- [Log](#log)
- [Hotfix](#hotfix)
- [AOP](#aop)
- [Hook](#hook)
- [Web Front End](#web-front-end)
    - [Common](#common)
    - [Networking](#networking-1)
    - [React](#react)
    - [Vue](#vue)
- [Cross Platform](#cross-platform)
    - [React Native](#react-native)
    - [Weex](#weex)
    - [Flutter](#flutter)
- [App](#app)
    - [GitHub](#github)
    - [IM](#im)
    - [Others](#others)

<!-- /TOC -->

> 语言缩写：OC=Objective-C, JS=JavaScript, TS=TypeScript
>
> Lang=Language, CLOC=Count Lines of Code

## UI

### Layout
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[Masonry](https://github.com/SnapKit/Masonry)</br>Harness the power of AutoLayout NSLayoutConstraints with a simplified, chainable and expressive syntax.</br></br>[iOS 源代码分析 ---- Masonry](https://draveness.me/ios-yuan-dai-ma-fen-xi-masonry) by draveness </br>[读 SnapKit 和 Masonry 自动布局框架源码](http://www.starming.com/2018/04/07/read-snapkit-and-masonry-source-code/) by 戴铭 | ![GitHub stars](https://img.shields.io/github/stars/SnapKit/Masonry.svg?style=social&label=Star) | OC | 25 files, 1.8k lines |
[SnapKit](https://github.com/SnapKit/SnapKit)</br>Swift 版 Masonry | ![GitHub stars](https://img.shields.io/github/stars/SnapKit/SnapKit.svg?style=social&label=Star) | Swift | 35 files, 1.8k lines |
[Yoga](https://github.com/facebook/yoga)</br>Yoga is a cross-platform layout engine which implements Flexbox. | ![GitHub stars](https://img.shields.io/github/stars/facebook/yoga.svg?style=social&label=Star) | C++ | 20 files, 5.3k lines |

### UITableView
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[UITableView-FDTemplateLayoutCell](https://github.com/forkingdog/UITableView-FDTemplateLayoutCell)</br>Template auto layout cell for automatically UITableViewCell height calculating.</br></br>[优化 UITableViewCell 高度计算的那些事](http://blog.sunnyxx.com/2015/05/17/cell-height-calculation/) by sunnyxx | ![GitHub stars](https://img.shields.io/github/stars/forkingdog/UITableView-FDTemplateLayoutCell.svg?style=social&label=Star) | OC | 8 files, 517 lines |

### HUD
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[MBProgressHUD](https://github.com/jdg/MBProgressHUD)</br></br>[iOS 源代码分析 ---- MBProgressHUD](https://draveness.me/ios-yuan-dai-ma-fen-xi-mbprogresshud) by draveness </br> [MBProgressHUD 源码解析](http://www.jianshu.com/p/6a5bd5fd8124) by J_Knight </br> [MBProgressHUD 实现分析](http://southpeak.github.io/2015/03/24/sourcecode-mbprogresshud/) by 南峰子 </br>[结合 Reveal 谈谈 MBProgressHUD 的用法](http://blog.leichunfeng.com/blog/2015/03/16/talking-about-the-usage-of-mbprogresshud-combined-with-reveal/) by 雷纯锋 | [![GitHub stars](https://img.shields.io/github/stars/jdg/MBProgressHUD.svg?style=social&label=Star)](https://github.com/jdg/MBProgressHUD) | OC | 2 files, 1k lines |
[SVProgressHUD](https://github.com/SVProgressHUD/SVProgressHUD)</br>A clean and lightweight progress HUD for your iOS and tvOS app. | [![GitHub stars](https://img.shields.io/github/stars/SVProgressHUD/SVProgressHUD.svg?style=social&label=Star)](https://github.com/SVProgressHUD/SVProgressHUD) | OC | 8 files, 1.4k lines |
[JGProgressHUD](https://github.com/JonasGessner/JGProgressHUD)</br>An elegant and simple progress HUD for iOS and tvOS. | [![GitHub stars](https://img.shields.io/github/stars/JonasGessner/JGProgressHUD.svg?style=social&label=Star)](https://github.com/JonasGessner/JGProgressHUD) | OC | 25 files, 1.4k lines |

### Refresh
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[MJRefresh](https://github.com/CoderMJLee/MJRefresh)</br>An easy way to use pull-to-refresh. | [![GitHub stars](https://img.shields.io/github/stars/CoderMJLee/MJRefresh.svg?style=social&label=Star)](https://github.com/CoderMJLee/MJRefresh) | OC | 39 files, 1.9k lines |

### Keyboard
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[IQKeyboardManager](https://github.com/hackiftekhar/IQKeyboardManager)</br></br>[『零行代码』解决键盘遮挡问题（iOS）](https://draveness.me/keyboard) by draveness | [![GitHub stars](https://img.shields.io/github/stars/hackiftekhar/IQKeyboardManager.svg?style=social&label=Star)](https://github.com/hackiftekhar/IQKeyboardManager) | OC |
[TPKeyboardAvoiding](https://github.com/michaeltyson/TPKeyboardAvoiding)</br>A drop-in universal solution for moving text fields out of the way of the keyboard in iOS. | [![GitHub stars](https://img.shields.io/github/stars/michaeltyson/TPKeyboardAvoiding.svg?style=social&label=Star)](https://github.com/michaeltyson/TPKeyboardAvoiding) | OC |

### Animation
Repo | Stars | Lang |
---- | ----- | -------- |
[pop](https://github.com/facebook/pop)</br>An extensible iOS and OS X animation library, useful for physics-based interactions. | [![GitHub stars](https://img.shields.io/github/stars/facebook/pop.svg?style=social&label=Star)](https://github.com/facebook/pop) | OC++ |
[lottie-ios](https://github.com/airbnb/lottie-ios)</br>An iOS library to natively render After Effects vector animations. | [![GitHub stars](https://img.shields.io/github/stars/airbnb/lottie-ios.svg?style=social&label=Star)](https://github.com/airbnb/lottie-ios) | OC |
[Spring](https://github.com/MengTo/Spring)</br>A library to simplify iOS animations in Swift. | [![GitHub stars](https://img.shields.io/github/stars/MengTo/Spring.svg?style=social&label=Star)](https://github.com/MengTo/Spring) | Swift |

### Smooth
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[AsyncDisplayKit](https://github.com/facebookarchive/AsyncDisplayKit) (ASDK) [已迁移至 [Texture](https://github.com/texturegroup/texture)]</br>Smooth asynchronous user interfaces for iOS apps.</br></br>[iOS 保持界面流畅的技巧](https://blog.ibireme.com/2015/11/12/smooth_user_interfaces_for_ios/) by ibireme </br>[使用 ASDK 性能调优 - 提升 iOS 界面的渲染性能](https://draveness.me/asdk-rendering) by draveness | ![GitHub stars](https://img.shields.io/github/stars/facebookarchive/AsyncDisplayKit.svg?style=social&label=Star) | OC | 316 fles, 35k lines |
[Texture](https://github.com/texturegroup/texture) | ![GitHub stars](https://img.shields.io/github/stars/texturegroup/texture.svg?style=social&label=Star) | OC | 396 files, 47k lines |

### Chat
Repo | Stars | Lang |
---- | ----- | -------- |
[JSQMessagesViewController](https://github.com/jessesquires/JSQMessagesViewController) [DEPRECATED] | [![GitHub stars](https://img.shields.io/github/stars/jessesquires/JSQMessagesViewController.svg?style=social&label=Star)](https://github.com/jessesquires/JSQMessagesViewController) | OC |
[MessageKit](https://github.com/MessageKit/MessageKit)</br>In-progress: A community-driven replacement for JSQMessagesViewController. | [![GitHub stars](https://img.shields.io/github/stars/MessageKit/MessageKit.svg?style=social&label=Star)](https://github.com/MessageKit/MessageKit) | Swift |

### Image
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[GPUImage](https://github.com/BradLarson/GPUImage)</br>An open source iOS framework for GPU-based image and video processing. | [![GitHub stars](https://img.shields.io/github/stars/BradLarson/GPUImage.svg?style=social&label=Star)](https://github.com/BradLarson/GPUImage) | OC | 359 files, 26k lines |
[GPUImage2](https://github.com/BradLarson/GPUImage2)</br>Swift 版 GPUImage | [![GitHub stars](https://img.shields.io/github/stars/BradLarson/GPUImage2.svg?style=social&label=Star)](https://github.com/BradLarson/GPUImage2) | Swift | 168 files, 6k lines |
[FLAnimatedImage](https://github.com/Flipboard/FLAnimatedImage)</br>Performant animated GIF engine for iOS. | [![GitHub stars](https://img.shields.io/github/stars/Flipboard/FLAnimatedImage.svg?style=social&label=Star)](https://github.com/Flipboard/FLAnimatedImage) | OC |
[SDWebImage](https://github.com/rs/SDWebImage)</br>Asynchronous image downloader with cache support as a UIImageView category.</br></br>[iOS 源代码分析 ---- SDWebImage](https://draveness.me/ios-yuan-dai-ma-jie-xi-sdwebimage) by draveness | [![GitHub stars](https://img.shields.io/github/stars/rs/SDWebImage.svg?style=social&label=Star)](https://github.com/rs/SDWebImage) | OC | 41 files, 3.1k lines |
[YYImage](https://github.com/ibireme/YYImage)</br>Image framework for iOS to display/encode/decode animated WebP, APNG, GIF, and more.</br></br>[移动端图片格式调研](https://blog.ibireme.com/2015/11/02/mobile_image_benchmark/) by ibireme</br>[iOS 处理图片的一些小 Tip](https://blog.ibireme.com/2015/11/02/ios_image_tips/) by ibireme | [![GitHub stars](https://img.shields.io/github/stars/ibireme/YYImage.svg?style=social&label=Star)](https://github.com/ibireme/YYImage) | OC | 10 files, 3.4k lines |
[YYWebImage](https://github.com/ibireme/YYWebImage)</br>Asynchronous image loading framework. | [![GitHub stars](https://img.shields.io/github/stars/ibireme/YYWebImage.svg?style=social&label=Star)](https://github.com/ibireme/YYWebImage) | OC | 37 files, 8.7k lines |
[PINRemoteImage](https://github.com/pinterest/PINRemoteImage)</br>A thread safe, performant, feature rich image fetcher. | [![GitHub stars](https://img.shields.io/github/stars/pinterest/PINRemoteImage.svg?style=social&label=Star)](https://github.com/pinterest/PINRemoteImage) | OC, Swift |
[ios-twitter-image-pipeline](https://github.com/twitter/ios-twitter-image-pipeline)</br>Twitter Image Pipeline is a robust and performant image loading and caching framework for iOS clients. | [![GitHub stars](https://img.shields.io/github/stars/twitter/ios-twitter-image-pipeline.svg?style=social&label=Star)](https://github.com/twitter/ios-twitter-image-pipeline) | OC |
[Kingfisher](https://github.com/onevcat/Kingfisher)</br>A lightweight, pure-Swift library for downloading and caching images from the web. | [![GitHub stars](https://img.shields.io/github/stars/onevcat/Kingfisher.svg?style=social&label=Star)](https://github.com/onevcat/Kingfisher) | Swift | 25 files, 3.8k lines |
[MWPhotoBrowser](https://github.com/mwaterfall/MWPhotoBrowser) [疑似已停更]</br>A simple iOS photo and video browser with grid view, captions and selections. | [![GitHub stars](https://img.shields.io/github/stars/mwaterfall/MWPhotoBrowser.svg?style=social&label=Star)](https://github.com/mwaterfall/MWPhotoBrowser) | OC |
[TZImagePickerController](https://github.com/banchichen/TZImagePickerController)</br>一个支持多选、选原图和视频的图片选择器，同时有预览、裁剪功能，支持 iOS6+。| [![GitHub stars](https://img.shields.io/github/stars/banchichen/TZImagePickerController.svg?style=social&label=Star)](https://github.com/banchichen/TZImagePickerController) | OC |
[ZLPhotoBrowser](https://github.com/longitachi/ZLPhotoBrowser)</br>方便易用的相册多选框架 | [![GitHub stars](https://img.shields.io/github/stars/longitachi/ZLPhotoBrowser.svg?style=social&label=Star)](https://github.com/longitachi/ZLPhotoBrowser) | OC |

### Video
Repo | Stars | Lang |
---- | ----- | -------- |
[ijkplayer](https://github.com/Bilibili/ijkplayer)</br>Android / iOS video player based on [FFmpeg](http://ffmpeg.org) n3.3, with MediaCodec, VideoToolbox support. | [![GitHub stars](https://img.shields.io/github/stars/Bilibili/ijkplayer.svg?style=social&label=Star)](https://github.com/Bilibili/ijkplayer) | C, OC, Java |

## Networking

### HTTP
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[AFNetworking](https://github.com/AFNetworking/AFNetworking)</br>A delightful networking framework for iOS, macOS, watchOS, and tvOS.</br></br>[AFNetworking 概述（一）](https://draveness.me/afnetworking1) by draveness </br> [AFNetworking 的核心 AFURLSessionManager（二）](https://draveness.me/afnetworking2) by draveness </br> [处理请求和响应 AFURLSerialization（三）](https://draveness.me/afnetworking3) by draveness </br> [AFNetworkReachabilityManager 监控网络状态（四）](https://draveness.me/afnetworking4) by draveness </br> [验证 HTTPS 请求的证书（五）](https://draveness.me/afnetworking5) by draveness </br> | [![GitHub stars](https://img.shields.io/github/stars/AFNetworking/AFNetworking.svg?style=social&label=Star)](https://github.com/AFNetworking/AFNetworking) | OC | 33 files, 5.1k lines |
[Alamofire](https://github.com/Alamofire/Alamofire)</br>Swift 版 AFNetworking</br></br>[iOS 源代码分析 ---- Alamofire](https://draveness.me/ios-yuan-dai-ma-fen-xi-alamofire) by draveness | [![GitHub stars](https://img.shields.io/github/stars/Alamofire/Alamofire.svg?style=social&label=Star)](https://github.com/Alamofire/Alamofire) | Swift | 18 files, 3.9k lines |
[YTKNetwork](https://github.com/yuantiku/YTKNetwork) | [![GitHub stars](https://img.shields.io/github/stars/yuantiku/YTKNetwork.svg?style=social&label=Star)](https://github.com/yuantiku/YTKNetwork) | OC |
[XMNetworking](https://github.com/kangzubin/XMNetworking) | [![GitHub stars](https://img.shields.io/github/stars/kangzubin/XMNetworking.svg?style=social&label=Star)](https://github.com/kangzubin/XMNetworking) | OC |
[RestKit](https://github.com/RestKit/RestKit)</br>RestKit is a framework for consuming and modeling RESTful web resources on iOS and OS X. | [![GitHub stars](https://img.shields.io/github/stars/RestKit/RestKit.svg?style=social&label=Star)](https://github.com/RestKit/RestKit) | OC |

### XMPP
Repo | Stars | Lang |
---- | ----- | -------- |
[XMPPFramework](https://github.com/robbiehanson/XMPPFramework) | [![GitHub stars](https://img.shields.io/github/stars/robbiehanson/XMPPFramework.svg?style=social&label=Star)](https://github.com/robbiehanson/XMPPFramework) | OC |

## SQLite
Repo | Stars | Lang |
---- | ----- | -------- |
[SQLite](https://www.sqlite.org/index.html)</br>SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine. | | C |
[FMDB](https://github.com/ccgus/fmdb)</br>A Cocoa / Objective-C wrapper around SQLite. | [![GitHub stars](https://img.shields.io/github/stars/ccgus/fmdb.svg?style=social&label=Star)](https://github.com/ccgus/fmdb) | OC |
[SQLite.swift](https://github.com/stephencelis/SQLite.swift)</br>A type-safe, Swift-Lang layer over SQLite3. | [![GitHub stars](https://img.shields.io/github/stars/stephencelis/SQLite.swift.svg?style=social&label=Star)](https://github.com/stephencelis/SQLite.swift) | Swift |
[SQLCipher](https://github.com/sqlcipher/sqlcipher)</br>SQLCipher is an SQLite extension that provides 256 bit AES encryption of database files. | [![GitHub stars](https://img.shields.io/github/stars/sqlcipher/sqlcipher.svg?style=social&label=Star)](https://github.com/sqlcipher/sqlcipher) | C |
[WCDB](https://github.com/Tencent/wcdb)</br>WCDB is a cross-platform database framework developed by WeChat. </br></br>[微信 WCDB 进化之路 - 开源与开始](https://mp.weixin.qq.com/s/tzy-fr55t1zqTbxOeKg4RA) by WeMobileDev</br>[微信移动端数据库组件 WCDB 系列（一）iOS 基础篇](https://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=2649286538&idx=1&sn=d11de2d87539a64e991e916013b0f729&chksm=8334c308b4434a1e5670fb68dc087cf34fe91e79bbfc64dbbf092424fd0cd3b28023c67b29ca&scene=21#wechat_redirect) by WeMobileDev </br>[微信移动端数据库组件 WCDB 系列（二）数据库修复三板斧](https://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=2649286581&idx=1&sn=ab8a10aeb92b424315a10c031b1f7902&chksm=8334c337b4434a219686e08cff86db8efedd4fe7d6ca440b70da4db41b9992ef2871d6b35cc9&scene=21#wechat_redirect) by WeMobileDev </br>[微信 SQLite 数据库修复实践](https://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=2649286467&idx=1&sn=ea5b6dbfecffd33e333ec814473e1313&chksm=8334c3c1b4434ad7c364ff3acae1e62bc5e871a7350aa9cdcb24bd299b42875f0b020acb3620&scene=21#wechat_redirect) by WeMobileDev </br>[微信 iOS SQLite 源码优化实践](https://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=2649286361&idx=1&sn=78bbcda7f41a14291ad71289e4821f71&scene=21#wechat_redirect) by WeMobileDev | [![GitHub stars](https://img.shields.io/github/stars/Tencent/wcdb.svg?style=social&label=Star)](https://github.com/Tencent/wcdb) | C, C++ |
[CTPersistance](https://github.com/casatwy/CTPersistance)</br>Objective-C / Swift Database Persistence Layer with SQLite, your next Persistence Layer! | [![GitHub stars](https://img.shields.io/github/stars/casatwy/CTPersistance.svg?style=social&label=Star)](https://github.com/casatwy/CTPersistance) | OC |

## Cache
Repo | Stars | Lang |
---- | ----- | -------- |
[PINCache](https://github.com/pinterest/PINCache)</br>Fast, non-deadlocking parallel object cache for iOS, tvOS and OS X. | [![GitHub stars](https://img.shields.io/github/stars/pinterest/PINCache.svg?style=social&label=Star)](https://github.com/pinterest/PINCache) | OC |
[YYCache](https://github.com/ibireme/YYCache)</br>High performance cache framework for iOS.</br></br>[YYCache 设计思路](https://blog.ibireme.com/2015/10/26/yycache/) by ibireme | [![GitHub stars](https://img.shields.io/github/stars/ibireme/YYCache.svg?style=social&label=Star)](https://github.com/ibireme/YYCache) | OC |

## Model
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[Mantle](https://github.com/Mantle/Mantle)</br>Model framework for Cocoa and Cocoa Touch. | [![GitHub stars](https://img.shields.io/github/stars/Mantle/Mantle.svg?style=social&label=Star)](https://github.com/Mantle/Mantle) | OC |
[MJExtension](https://github.com/CoderMJLee/MJExtension)</br>A fast, convenient and nonintrusive conversion between JSON and model. | [![GitHub stars](https://img.shields.io/github/stars/CoderMJLee/MJExtension.svg?style=social&label=Star)](https://github.com/CoderMJLee/MJExtension) | OC |
[YYModel](https://github.com/ibireme/YYModel)</br>High performance model framework for iOS/OSX. | [![GitHub stars](https://img.shields.io/github/stars/ibireme/YYModel.svg?style=social&label=Star)](https://github.com/ibireme/YYModel) | OC | 5 files, 2K lines |
[SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON)</br>The better way to deal with JSON data in Swift. | [![GitHub stars](https://img.shields.io/github/stars/SwiftyJSON/SwiftyJSON.svg?style=social&label=Star)](https://github.com/SwiftyJSON/SwiftyJSON) | Swift |

## Util
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[dyld](https://github.com/opensource-apple/dyld)</br>动态链接器</br></br>[iOS 程序 main 函数之前发生了什么](http://blog.sunnyxx.com/2014/08/30/objc-pre-main/) by sunnyxx | ![GitHub stars](https://img.shields.io/github/stars/opensource-apple/dyld.svg?style=social&label=Star) | C | 39 files, 16K lines |
[libffi](https://github.com/libffi/libffi)</br> A portable foreign-function interface library. | ![GitHub stars](https://img.shields.io/github/stars/libffi/libffi.svg?style=social&label=Star) | C | 124 files, 28k lines |
[RxSwift](https://github.com/ReactiveX/RxSwift) | [![GitHub stars](https://img.shields.io/github/stars/ReactiveX/RxSwift.svg?style=social&label=Star)](https://github.com/ReactiveX/RxSwift) | Swift |
[BlocksKit](https://github.com/BlocksKit/BlocksKit)</br></br>[神奇的 BlocksKit （一）](https://draveness.me/blockskit-1) by draveness </br> [神奇的 BlocksKit （二）](https://draveness.me/blockskit-2) by draveness | [![GitHub stars](https://img.shields.io/github/stars/BlocksKit/BlocksKit.svg?style=social&label=Star)](https://github.com/BlocksKit/BlocksKit) | OC |
[KVOController](https://github.com/facebook/KVOController)</br>Simple, modern, thread-safe key-value observing for iOS and OS X.</br></br>[如何优雅地使用 KVO](https://draveness.me/kvocontroller) by draveness 2017 | ![GitHub stars](https://img.shields.io/github/stars/facebook/KVOController.svg?style=social&label=Star) | OC | 5 files, 554 lines |
[MLeaksFinder](https://github.com/Tencent/MLeaksFinder) | [![GitHub stars](https://img.shields.io/github/stars/Tencent/MLeaksFinder.svg?style=social&label=Star)](https://github.com/Tencent/MLeaksFinder) | OC |

## Log
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[CocoaLumberjack](https://github.com/CocoaLumberjack/CocoaLumberjack)</br>A fast & simple, yet powerful & flexible logging framework for Mac and iOS. | [![GitHub stars](https://img.shields.io/github/stars/CocoaLumberjack/CocoaLumberjack.svg?style=social&label=Star)](https://github.com/CocoaLumberjack/CocoaLumberjack) | OC |

## Hotfix
Repo | Stars | Lang |
---- | ----- | -------- |
[JSPatch](https://github.com/bang590/JSPatch)</br>JSPatch bridge Objective-C and Javascript using the Objective-C runtime.</br></br>[JSPatch – 动态更新iOS APP](http://blog.cnbang.net/works/2767/) by bang </br> [JSPatch 实现原理详解](http://blog.cnbang.net/tech/2808/) by bang </br> [JSPatch 实现原理详解<二>](http://blog.cnbang.net/tech/2855/) by bang </br> [JSPatch 部署安全策略](http://blog.cnbang.net/tech/2879/) by bang </br> [JSPatch Convertor 实现原理详解](http://blog.cnbang.net/tech/2915/) by bang </br> [回应一下 JSPatch 安全问题](http://blog.cnbang.net/internet/2990/) by bang </br> [JSPatch 平台介绍](http://blog.cnbang.net/archives/) by bang </br> [JSPatch 近期新特性解析](http://blog.cnbang.net/tech/3038/) by bang </br> [JSPatch 更新：完善开发功能模块的能力](http://blog.cnbang.net/tech/3123/) by bang </br> [如何动态调用 C 函数](http://blog.cnbang.net/tech/3219/) by bang </br> [iOS 动态更新方案对比:JSPatch vs React Native](http://blog.cnbang.net/archives/) by bang </br> [如何动态创建 block - JPBlock 扩展原理详解](http://blog.cnbang.net/tech/3332/) by bang </br> | [![GitHub stars](https://img.shields.io/github/stars/bang590/JSPatch.svg?style=social&label=Star)](https://github.com/bang590/JSPatch) | C, OC |

## AOP
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[Aspects](https://github.com/steipete/Aspects)</br>Delightful, simple library for aspect oriented programming.</br></br>[iOS 如何实现 Aspect Oriented Programming](https://halfrost.com/ios_aspect/) by halfrost | ![GitHub stars](https://img.shields.io/github/stars/steipete/Aspects.svg?style=social&label=Star) | OC | 2 files, 777 lines |

## Hook
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[fishhook](https://github.com/facebook/fishhook)</br>A library that enables dynamically rebinding symbols in Mach-O binaries running on iOS.</br></br>[动态修改 C 语言函数的实现](https://draveness.me/fishhook) by draveness</br>[巧用符号表 - 探求 fishhook 原理（一）](http://www.desgard.com/fishhook-1/) by desgard</br>[验证试验 - 探求 fishhook 原理（二）](http://www.desgard.com/fishhook-2/) by desgard | ![GitHub stars](https://img.shields.io/github/stars/facebook/fishhook.svg?style=social&label=Star) | C | 2 files, 196 lines |
[BlockHook](https://github.com/yulingtianxia/BlockHook)</br>Hook Objective-C blocks with libffi.</br></br>[Hook Objective-C Block with Libffi](http://yulingtianxia.com/blog/2018/02/28/Hook-Objective-C-Block-with-Libffi/) by 杨萧玉 | ![GitHub stars](https://img.shields.io/github/stars/yulingtianxia/BlockHook.svg?style=social&label=Star) | OC | 2 files, 381 lines |

## Web Front End

### Common
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[pinyin](https://github.com/hotoo/pinyin)</br>转换中文字符为拼音。可以用于汉字注音、排序、检索。支持多音字、繁体、多种不同拼音风格。 | [![GitHub stars](https://img.shields.io/github/stars/hotoo/pinyin.svg?style=social&label=Star)](https://github.com/hotoo/pinyin) | JS |
[Redux](https://github.com/reactjs/redux)</br>Predictable state container for JavaScript apps. | 35,000+ | JS |

### Networking
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[axios](https://github.com/axios/axios)</br>Promise based HTTP client for the browser and node.js. | [![GitHub stars](https://img.shields.io/github/stars/axios/axios.svg?style=social&label=Star)](https://github.com/axios/axios) | JS | 107 files, 6.8k lines |
[isomorphic-fetch](https://github.com/matthew-andrews/isomorphic-fetch)</br>Isomorphic WHATWG Fetch API, for Node & Browserify. | [![GitHub stars](https://img.shields.io/github/stars/matthew-andrews/isomorphic-fetch.svg?style=social&label=Star)](https://github.com/matthew-andrews/isomorphic-fetch) | JS | 8 files, 150 lines |

### React
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[React](https://github.com/facebook/react)</br>A declarative, efficient, and flexible JavaScript library for building user interfaces. | [![GitHub stars](https://img.shields.io/github/stars/facebook/react.svg?style=social&label=Star)](https://github.com/facebook/react) | JS | 698 files, 120K lines |
[React Redux](https://github.com/reactjs/react-redux)</br>Official React bindings for Redux. | 9,800+ | JS |
[redux-saga](https://github.com/redux-saga/redux-saga)</br>一个用于管理 Redux 应用异步操作的中间件。 | 9,800+ | JS |
[React Router](https://github.com/ReactTraining/react-router)</br>Declarative routing for React. | 25,000+ | JS |
[react-router-redux](https://github.com/reactjs/react-router-redux)</br>Ruthlessly simple bindings to keep react-router and redux in sync. | 6,700+ | JS |
[dva](https://github.com/dvajs/dva)</br>支付宝前端团队出品的基于 redux、redux-saga 和 react-router 的轻量级前端框架。 | 6,300+ | JS |

### Vue
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[Vue.js](https://github.com/vuejs/vue)</br>A progressive, incrementally-adoptable JavaScript framework for building UI on the web. | [![GitHub stars](https://img.shields.io/github/stars/vuejs/vue.svg?style=social&label=Star)](https://github.com/vuejs/vue) | JS |

## Cross Platform

### React Native
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[React Native](https://github.com/facebook/react-native)</br>A framework for building native apps with React.</br></br>[React Native 源码导读(零) – 创建/运行/调试](http://blog.cnbang.net/tech/3461/) by bang</br>[React Native 通信机制详解](http://blog.cnbang.net/tech/2698/) by bang | 57,000+ | JS, OC, Java |
[react-navigation](https://github.com/react-community/react-navigation)</br>Learn once, navigate anywhere. RN 官方导航解决方案。 | 7,700+ | JS | |
[react-native-navigation](https://github.com/wix/react-native-navigation)</br>A complete native navigation solution for React Native. | 5,000+ | JS, OC, Java | |
[native-navigation](https://github.com/airbnb/native-navigation)</br>Native navigation library for React Native applications. airbnb 出品的 RN 导航解决方案。 | 2,500+ | JS | |
[react-native-calendars](https://github.com/wix/react-native-calendars)</br>React Native Calendar Components. | 1,400+ | JS | |
[react-native-sqlite-storage](https://github.com/andpor/react-native-sqlite-storage)</br>Full featured SQLite3 Native Plugin for React Native (Android and iOS). | 1,000+ | JS, Java, OC | |
[ant-design-mobile](https://github.com/ant-design/ant-design-mobile)</br>antd-mobile 是 Ant Design 的移动规范的 React 实现，服务于蚂蚁及口碑无线业务。 | 3,200+ | TS | |

### Weex
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[Weex](https://github.com/apache/incubator-weex)</br>A framework for building Mobile cross-platform UI.</br></br>[Weex Conf 2018](http://weex-project.io/weexConf2018/) </br>[Weex + Ui - Weex Conf 2018](https://zhuanlan.zhihu.com/p/33153760?iam=08abed520609736c2d292670aeb38a28?utm_medium=social&utm_source=weibo) by 汤威（侑夕），飞猪高级前端工程师 </br>[Weex Conf 2018 参会小结：Weex 的现状和未来](https://juejin.im/post/5a620abf6fb9a01c9950e4a0) by 没故事的卓同学 | [![GitHub stars](https://img.shields.io/github/stars/apache/incubator-weex.svg?style=social&label=Star)](https://github.com/apache/incubator-weex) | JS, OC, Java |
[weex-ui](https://github.com/alibaba/weex-ui)</br>A rich interaction, lightweight, high performance UI library based on Weex. | [![GitHub stars](https://img.shields.io/github/stars/alibaba/weex-ui.svg?style=social&label=Star)](https://github.com/alibaba/weex-ui) | JS |

### Flutter
Repo | Stars | Lang |
---- | ----- | -------- |
[flutter](https://github.com/flutter/flutter)</br>Flutter makes it easy and fast to build beautiful mobile apps. | ![GitHub stars](https://img.shields.io/github/stars/flutter/flutter.svg?style=social&label=Star) | Dart |

## App

### GitHub
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[GitHub Desktop](https://github.com/desktop/desktop)</br>GitHub Desktop is an open source Electron-based GitHub app. It is written in TypeScript and uses React. | ![GitHub stars](https://img.shields.io/github/stars/desktop/desktop.svg?style=social&label=Star) | TS | 730 files, 62k lines |

### IM
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[Telegram](https://github.com/peter-iakovlev/Telegram)</br>Telegram Messenger for iOS | ![GitHub stars](https://img.shields.io/github/stars/peter-iakovlev/Telegram.svg?style=social&label=Star) | OC | |
[Messenger](https://github.com/relatedcode/Messenger)</br>This is a native iOS Messenger app, with audio/video calls and realtime chat conversations (full offline support). | ![GitHub stars](https://img.shields.io/github/stars/relatedcode/Messenger.svg?style=social&label=Star) | OC | |

### Others
Repo | Stars | Lang | CLOC |
---- | ----- | ---- | ---- |
[DanTang](https://github.com/hrscy/DanTang)</br>Swift - 单糖 | ![GitHub stars](https://img.shields.io/github/stars/hrscy/DanTang.svg?style=social&label=Star) | Swift | |
[SwiftLanguageWeather](https://github.com/JakeLin/SwiftLanguageWeather)</br>Swift Language Weather is an iOS weather app developed in Swift 4. | ![GitHub stars](https://img.shields.io/github/stars/JakeLin/SwiftLanguageWeather.svg?style=social&label=Star) | Swift | |

<!-- []() | 0+ | OC | []() | -->
<!-- []() | 0+ | JS | []() | -->

<!-- [![GitHub stars](https://img.shields.io/github/stars/.svg?style=social&label=Star)](https://github.com/) -->