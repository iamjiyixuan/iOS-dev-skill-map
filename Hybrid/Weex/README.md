# Weex

<!-- TOC -->

- [1. 初见](#1-初见)
    - [1.1. Weex 是什么？](#11-weex-是什么)
    - [1.2. Weex 的目标是什么？](#12-weex-的目标是什么)
    - [1.3. 学习 Weex 之前，你需要了解什么？](#13-学习-weex-之前你需要了解什么)
- [2. 搭建开发环境](#2-搭建开发环境)
- [3. hello-weex](#3-hello-weex)
    - [3.1. 新建 Weex 工程](#31-新建-weex-工程)
    - [3.2. Weex 工程标准结构](#32-weex-工程标准结构)
    - [3.3. 安装](#33-安装)
    - [3.4. 启动服务](#34-启动服务)
    - [3.5. hello-weex for iOS](#35-hello-weex-for-ios)
        - [3.5.1. 通过 CocoaPods 安装 WeexSDK](#351-通过-cocoapods-安装-weexsdk)
        - [3.5.2. 初始化 Weex 环境](#352-初始化-weex-环境)
        - [3.5.3. 渲染页面](#353-渲染页面)
    - [3.6. hello-weex for Android](#36-hello-weex-for-android)
        - [3.6.1. 新建工程，设置依赖](#361-新建工程设置依赖)
        - [3.6.2. 新建 ImageAdapter](#362-新建-imageadapter)
        - [3.6.3. 新建 WeexApplication](#363-新建-weexapplication)
        - [3.6.4. 修改 AndroidManifest.xml 启用 WeexApplication](#364-修改-androidmanifestxml-启用-weexapplication)
        - [3.6.5. MainActivity](#365-mainactivity)
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

### 1.3. 学习 Weex 之前，你需要了解什么？
- Node.js
- HTML + CSS + JavaScript 前端知识
- Vue.js 框架
- iOS 或 Android Native 知识

## 2. 搭建开发环境
- [dotWe](http://dotwe.org/vue) - Weex 在线调试工具
- Node.js & npm
- weex-toolkit - 一个基于 Node.js 的命令行工具（注：1.0.1 之后才支持初始化 Vue 项目）

## 3. hello-weex

### 3.1. 新建 Weex 工程
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

src/foo.vue
```
<template>
  <div class="wrapper" @click="update">
    <image :src="logoUrl" class="logo"></image>
    <text class="title">Hello {{target}}</text>
  </div>
</template>

<style>
  .wrapper { align-items: center; margin-top: 120px; }
  .title { font-size: 48px; }
  .logo { width: 360px; height: 82px; }
</style>

<script>
  export default {
    data: {
      logoUrl: 'https://alibaba.github.io/weex/img/weex_logo_blue@3x.png',
      target: 'World'
    },
    methods: {
      update: function (e) {
        this.target = 'Weex'
        console.log('target:', this.target)
      }
    }
  }
</script>
```

### 3.3. 安装

```
$ npm install
```
安装成功后，根目录下多出 node_modules 目录。

### 3.4. 启动服务

运行 `npm run dev` 开启 watch 模式

```
$ npm run dev

> hello-weex@0.1.0 dev /Users/jiyixuan/weex_workspace/hello-weex
> webpack --watch

Hash: 341195b95f4773f47824
Version: webpack 1.14.0
Time: 1037ms
      Asset     Size  Chunks             Chunk Names
app.weex.js  4.41 kB       0  [emitted]  app
    + 5 hidden modules
Hash: 4356d9addcb039cb794d
Version: webpack 1.14.0
Time: 1121ms
     Asset     Size  Chunks             Chunk Names
app.web.js  15.4 kB       0  [emitted]  app
    + 10 hidden modules
```

此时，根目录下会生成一个 dist 目录：
```
dist
├── app.web.js
└── app.weex.js 这个文件就是以后供移动端访问的
```

运行 `npm run serve` 启动静态服务器

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

浏览器打开 `http://localhost:8080/index.html` 查看 Weex h5 页面

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
        // process failure
    };
    
    _instance.renderFinish = ^ (UIView *view) {
        // process renderFinish
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

#### 3.6.1. 新建工程，设置依赖
app/build.gradle
```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "android.neegle.net.helloweexandroid"
        minSdkVersion 15
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.android.support:recyclerview-v7:23.1.1'
    compile 'com.android.support:support-v4:23.1.1'
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.alibaba:fastjson:1.1.46.android'
    compile 'com.taobao.android:weex_sdk:0.10.0'  // 0.10.0 以上版本才支持 Vue.js
    testCompile 'junit:junit:4.12'
}
```

#### 3.6.2. 新建 ImageAdapter
``` Java
import android.widget.ImageView;

import com.taobao.weex.adapter.IWXImgLoaderAdapter;
import com.taobao.weex.common.WXImageStrategy;
import com.taobao.weex.dom.WXImageQuality;

/**
 * Created by jiyixuan on 2017/3/29.
 */

public class ImageAdapter implements IWXImgLoaderAdapter {

    @Override
    public void setImage(String url, ImageView view, WXImageQuality quality, WXImageStrategy strategy) {
        //实现你自己的图片下载。
    }
}
```

#### 3.6.3. 新建 WeexApplication
``` Java
import android.app.Application;

import com.taobao.weex.InitConfig;
import com.taobao.weex.WXSDKEngine;
import com.taobao.weex.common.WXException;

/**
 * Created by jiyixuan on 2017/3/29.
 */

public class WeexApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        InitConfig config = new InitConfig.Builder().setImgAdapter(new ImageAdapter()).build();
        WXSDKEngine.initialize(this, config);
    }
}
```
#### 3.6.4. 修改 AndroidManifest.xml 启用 WeexApplication
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="android.neegle.net.helloweexandroid">

    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

    <application
        android:name=".WeexApplication"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

#### 3.6.5. MainActivity
```
package android.neegle.net.helloweexandroid;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;

import com.taobao.weex.IWXRenderListener;
import com.taobao.weex.WXSDKInstance;
import com.taobao.weex.common.WXRenderStrategy;
import com.taobao.weex.utils.WXFileUtils;

import java.util.HashMap;
import java.util.Map;

public class MainActivity extends AppCompatActivity implements IWXRenderListener {

    private static final String WEB_URL="http://192.168.1.186:8080/dist/app.weex.js";
    WXSDKInstance mWXSDKInstance;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mWXSDKInstance = new WXSDKInstance(this);
        mWXSDKInstance.registerRenderListener(this);

        Map<String, Object> options = new HashMap<>();
        // 加载服务器 js
//        options.put(WXSDKInstance.BUNDLE_URL, WEB_URL);
//        mWXSDKInstance.render("WXSample",WEB_URL,options, null, WXRenderStrategy.APPEND_ONCE);
        // 加载本地 js
        options.put(WXSDKInstance.BUNDLE_URL, "file://build/hello.js");
        mWXSDKInstance.render("WXSample",WXFileUtils.loadAsset("build/app.weex.js", this),options, null, WXRenderStrategy.APPEND_ONCE);
    }

    @Override
    public void onViewCreated(WXSDKInstance instance, View view) {
        setContentView(view);
    }

    @Override
    public void onRenderSuccess(WXSDKInstance instance, int width, int height) {
    }
    @Override
    public void onRefreshSuccess(WXSDKInstance instance, int width, int height) {
    }
    @Override
    public void onException(WXSDKInstance instance, String errCode, String msg) {
    }

    @Override
    protected void onResume() {
        super.onResume();
        if(mWXSDKInstance!=null){
            mWXSDKInstance.onActivityResume();
        }
    }

    @Override
    protected void onPause() {
        super.onPause();
        if(mWXSDKInstance!=null){
            mWXSDKInstance.onActivityPause();
        }
    }
    @Override
    protected void onStop() {
        super.onStop();
        if(mWXSDKInstance!=null){
            mWXSDKInstance.onActivityStop();
        }
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        if(mWXSDKInstance!=null){
            mWXSDKInstance.onActivityDestroy();
        }
    }
}
```

## 4. 工作原理

## 5. 参考资料
- [weex 官网](http://weex.apache.org/cn/)
- [Vue.js 官网](https://vuejs.org)
- [Weex 是如何在 iOS 客户端上跑起来的](http://www.jianshu.com/p/41cde2c62b81) by 一缕殇流化隐半边冰霜 2017
- [由FlexBox算法强力驱动的Weex布局引擎](http://www.jianshu.com/p/d085032d4788) by 一缕殇流化隐半边冰霜 2017
