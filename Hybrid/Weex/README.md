# Weex

<!-- TOC -->

- [1. 初见](#1-初见)
    - [1.1. Weex 是什么？](#11-weex-是什么)
    - [1.2. Weex 的目标是什么？](#12-weex-的目标是什么)
- [2. 搭建开发环境](#2-搭建开发环境)
- [3. hello-weex](#3-hello-weex)
    - [3.1. 初始化](#31-初始化)
    - [3.2. Weex 工程标准结构](#32-weex-工程标准结构)
    - [3.3. 安装](#33-安装)
    - [3.4. 启动服务](#34-启动服务)
    - [3.5. hello-weex for iOS](#35-hello-weex-for-ios)
        - [3.5.1. 通过 CocoaPods 安装 WeexSDK](#351-通过-cocoapods-安装-weexsdk)
        - [3.5.2. 初始化 Weex 环境](#352-初始化-weex-环境)
        - [3.5.3. 渲染页面](#353-渲染页面)
    - [3.6. hello-weex for Android](#36-hello-weex-for-android)
- [4. 工作原理](#4-工作原理)
- [5. 参考资料](#5-参考资料)

<!-- /TOC -->

## 1. 初见

### 1.1. Weex 是什么？
- 一套跨平台开发方案（iOS、Android、浏览器三端）
- 对移动端而言，可以用 web 的开发体验构建高性能、可扩展的 native 应用
- 支持 Vue.js

### 1.2. Weex 的目标是什么？
- Write Once, Run Everywhere.
- 一套代码同时支持 iOS、Android、浏览器（H5）三端运行
- 打造三端一致的 native 应用

## 2. 搭建开发环境
- [dotWe](http://dotwe.org/vue) - Weex 在线调试工具
- Node.js & npm
- weex-toolkit - 一个基于 Node.js 的命令行工具（注：1.0.1 之后才支持初始化 Vue 项目）

## 3. hello-weex

### 3.1. 初始化
```
$ weex init hello-weex

prompt: Init your Project:  (hello-weex)
file: /Users/jiyixuan/weex_workspace/hello-weex/.babelrc created.
file: /Users/jiyixuan/weex_workspace/hello-weex/.eslintrc created.
file: /Users/jiyixuan/weex_workspace/hello-weex/.gitignore created.
file: /Users/jiyixuan/weex_workspace/hello-weex/README.md created.
file: /Users/jiyixuan/weex_workspace/hello-weex/app.js created.
file: /Users/jiyixuan/weex_workspace/hello-weex/assets/phantom-limb.js created.
file: /Users/jiyixuan/weex_workspace/hello-weex/assets/qrcode.js created.
file: /Users/jiyixuan/weex_workspace/hello-weex/assets/qrcode.min.js created.
file: /Users/jiyixuan/weex_workspace/hello-weex/assets/style.css created.
file: /Users/jiyixuan/weex_workspace/hello-weex/assets/url.js created.
file: /Users/jiyixuan/weex_workspace/hello-weex/build/init.js created.
file: /Users/jiyixuan/weex_workspace/hello-weex/index.html created.
file: /Users/jiyixuan/weex_workspace/hello-weex/package.json created.
file: /Users/jiyixuan/weex_workspace/hello-weex/src/foo.vue created.
file: /Users/jiyixuan/weex_workspace/hello-weex/webpack.config.js created.
file: /Users/jiyixuan/weex_workspace/hello-weex/weex.html created.
```

### 3.2. Weex 工程标准结构
```
├── README.md
├── app.js
├── assets
│   ├── phantom-limb.js
│   ├── qrcode.js
│   ├── qrcode.min.js
│   ├── style.css
│   └── url.js
├── build
│   └── init.js
├── index.html
├── package.json
├── src
│   └── foo.vue
├── webpack.config.js
└── weex.html
```

### 3.3. 安装

```
$ npm install
```
安装成功后，根目录下多出 node_modules 目录。

### 3.4. 启动服务

执行 `npm run serve` 启动一个本地服务，并在浏览器打开 `http://localhost:8080/index.html` 查看 Weex h5 页面
```
$ npm run serve

> hello-weex@0.1.0 serve /Users/jiyixuan/weex_workspace/hello-weex
> node build/init.js && serve -p 8080

serving /Users/jiyixuan/weex_workspace/hello-weex on port 8080
GET /index.html 200 9ms - 1.6kb
GET /config.js 200 3ms - 32
GET /assets/style.css 200 8ms - 1.14kb
GET /assets/url.js 200 5ms - 295
GET /assets/qrcode.js 200 4ms - 48.89kb
GET /node_modules/vue/dist/vue.js 200 5ms - 238.7kb
GET /weex.html 200 1ms - 891
GET /assets/phantom-limb.js 200 6ms - 10.12kb
GET /dist/app.web.js 200 5ms - 15.02kb
GET /node_modules/vue/dist/vue.runtime.js 200 6ms - 172.52kb
GET /node_modules/weex-vue-render/index.js 200 7ms - 713.49kb
GET /weex.html 304 1ms
```

### 3.5. hello-weex for iOS

#### 3.5.1. 通过 CocoaPods 安装 WeexSDK
常规做法，没什么要特别说明的。

#### 3.5.2. 初始化 Weex 环境

``` Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // 配置
    [WXAppConfiguration setAppGroup:@"study-weex"];
    [WXAppConfiguration setAppName:@"hello-weex-ios"];
    [WXAppConfiguration setAppVersion:@"1.0.0"];
    
    // 初始化 SDK
    [WXSDKEngine initSDKEnvironment];
    
    // 设置日志
    [WXLog setLogLevel: WXLogLevelAll];
    
    return YES;
}
```

#### 3.5.3. 渲染页面

``` Objective-C
#import "ViewController.h"
// 3rd
#import <WeexSDK/WXSDKInstance.h>

@interface ViewController ()

@property (nonatomic, strong) NSURL *url;
@property (nonatomic, strong) WXSDKInstance *instance;
@property (nonatomic, strong) UIView *weexView;
    
@end

@implementation ViewController

- (void)viewDidLoad
{
    [super viewDidLoad];
    
    _url = [NSURL URLWithString:@"http://192.168.1.186:8080/dist/app.weex.js"];
    
    _instance = [[WXSDKInstance alloc] init];
    _instance.viewController = self;
    _instance.frame = self.view.frame;
    
    __weak typeof(self) weakSelf = self;
    _instance.onCreate = ^(UIView *view) {
        [weakSelf.weexView removeFromSuperview];
        weakSelf.weexView = view; // 官方文档里少了这句，会导致看不到界面
        [weakSelf.view addSubview:weakSelf.weexView];
    };
    
    _instance.onFailed = ^(NSError *error) {
        //process failure
    };
    
    _instance.renderFinish = ^ (UIView *view) {
        //process renderFinish
    };
    [_instance renderWithURL:self.url options:@{@"bundleUrl":[self.url absoluteString]} data:nil];
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

- (void)dealloc
{
    // 销毁掉 Weex instance，释放内存，避免造成内存泄露
    [_instance destroyInstance];
}

@end
```

### 3.6. hello-weex for Android

## 4. 工作原理

## 5. 参考资料
- [weex 官网](http://weex.apache.org/cn/)
- [Weex 是如何在 iOS 客户端上跑起来的](http://www.jianshu.com/p/41cde2c62b81) by 一缕殇流化隐半边冰霜 2017
