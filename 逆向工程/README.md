# iOS 逆向工程

目录
<!-- TOC -->

- [1. 越狱](#1-越狱)
- [2. 砸壳](#2-砸壳)
    - [2.1. 下载安装 dumpdecrypted](#21-下载安装-dumpdecrypted)
    - [2.2. 连接越狱设备](#22-连接越狱设备)
    - [2.3. 找到可执行文件的位置](#23-找到可执行文件的位置)
    - [2.4. 执行砸壳](#24-执行砸壳)
- [3. class-dump](#3-class-dump)
- [4. 参考资料](#4-参考资料)

<!-- /TOC -->

## 1. 越狱

## 2. 砸壳
我们直接从 AppStore 上面下载安装的应用都被苹果进行了加密，无法直接进行逆向。因此需要先破坏这一层保护壳，这就是所谓的“砸壳”。

### 2.1. 下载安装 dumpdecrypted
```
$ mkdir reverse_workspace

$ cd reverse_workspace

$ git clone git://github.com/stefanesser/dumpdecrypted/
Cloning into 'dumpdecrypted'...
remote: Counting objects: 31, done.
remote: Total 31 (delta 0), reused 0 (delta 0), pack-reused 31
Receiving objects: 100% (31/31), 7.10 KiB | 0 bytes/s, done.
Resolving deltas: 100% (15/15), done.

$ cd dumpdecrypted
$ make
xcrun --sdk iphoneos --find gcc` -Os  -Wimplicit -isysroot `xcrun --sdk iphoneos --show-sdk-path` -F`xcrun --sdk iphoneos --show-sdk-path`/System/Library/Frameworks -F`xcrun --sdk iphoneos --show-sdk-path`/System/Library/PrivateFrameworks -arch armv7 -arch armv7s -arch arm64 -c -o dumpdecrypted.o dumpdecrypted.c
2017-03-30 10:25:53.841 xcodebuild[14645:344677] [MT] PluginLoading: Required plug-in compatibility UUID DFFB3951-EB0A-4C09-9DAC-5F2D28CC839C for plug-in at path '~/Library/Application Support/Developer/Shared/Xcode/Plug-ins/ClangFormat.xcplugin' not present in DVTPlugInCompatibilityUUIDs
`xcrun --sdk iphoneos --find gcc` -Os  -Wimplicit -isysroot `xcrun --sdk iphoneos --show-sdk-path` -F`xcrun --sdk iphoneos --show-sdk-path`/System/Library/Frameworks -F`xcrun --sdk iphoneos --show-sdk-path`/System/Library/PrivateFrameworks -arch armv7 -arch armv7s -arch arm64 -dynamiclib -o dumpdecrypted.dylib dumpdecrypted.o
```

make 完成后的目录结构：
```
dumpdecrypted
├── Makefile
├── README
├── dumpdecrypted.c
├── dumpdecrypted.dylib
└── dumpdecrypted.o
```
dumpdecrypted.dylib 就是我们需要使用到的砸壳工具。

### 2.2. 连接越狱设备
`ssh` 远程登入越狱设备
```
$ ssh root@192.168.1.183
```

使用 `scp` 命令实现电脑与越狱设备之间相互传输文件
```
// 越狱设备 -> 电脑
$ scp root@192.168.1.183:/var/mobile/Containers/Data/Application/5695E941-F58D-4775-AFD4-9D5883CBE3F8/Documents/kunlun.sqlite ./tmp

// 电脑 -> 越狱设备
$ scp ./1.txt root@192.168.1.183:/var/mobile/Containers/Data/Application/5695E941-F58D-4775-AFD4-9D5883CBE3F8/Documents
```

### 2.3. 找到可执行文件的位置

以饿了么为例。手机启动饿了么，使用 `ps ax` 查看当前执行的进程：
```
$ ps ax | grep eleme.app
 3468   ??  Ss     0:01.83 /var/containers/Bundle/Application/4FB489D8-2E7A-4F17-AAB0-670D2C5CF488/eleme.app/eleme
```

### 2.4. 执行砸壳

Killed 9 问题的解决方案：[传送门](https://github.com/stefanesser/dumpdecrypted/issues/19) 见 n8r0n commented on 15 Aug 2016 的回答

第一步，将 `dumpdecrypted.dylib` 文件拷贝到 `/usr/lib` 目录下。

第二步，切换用户至 mobile。
```
su mobile
```

第三步，跳转至 Documents 目录，我们会将砸壳后的应用都放在这个路径下。
```
cd /var/mobile/Documents
```

第四步，砸壳。
```
$ DYLD_INSERT_LIBRARIES=/usr/lib/dumpdecrypted.dylib /var/containers/Bundle/Application/4FB489D8-2E7A-4F17-AAB0-670D2C5CF488/eleme.app/eleme

ach-o decryption dumper

DISCLAIMER: This tool is only meant for security research purposes, not for application crackers.

[+] detected 64bit ARM binary in memory.
[+] offset to cryptid found: @0x10009cc58(from 0x10009c000) = c58
[+] Found encrypted data at address 00004000 of length 11665408 bytes - type 1.
[+] Opening /private/var/containers/Bundle/Application/4FB489D8-2E7A-4F17-AAB0-670D2C5CF488/eleme.app/eleme for reading.
[+] Reading header
[+] Detecting header type
[+] Executable is a plain MACH-O image
[+] Opening eleme.decrypted for writing.
[+] Copying the not encrypted start of the file
[+] Dumping the decrypted data into the file
[+] Copying the not encrypted remainder of the file
[+] Setting the LC_ENCRYPTION_INFO->cryptid to 0 at offset c58
[+] Closing original file
[+] Closing dump file
```

如何砸壳成功，得到 `.decrypted` 文件
```
$ ls -l | grep eleme
-rw-r--r-- 1 mobile mobile 15156032 Mar 30 13:20 eleme.decrypted
```

最后一步，将 `.decrypted` 文件拷贝到电脑，准备进行 class-dump。

## 3. class-dump

```
$ class-dump -S -s -H eleme.decrypted -o Headers
```
class-dump 后生成的头文件会保存到 Headers 目录。

## 4. 参考资料

书籍
- [《iOS应用逆向工程》](https://book.douban.com/subject/25826902/) by 沙梓社, 吴航, 刘瑾

文章
- [iOS 逆向手把手教程之一：砸壳与class-dump](http://www.swiftyper.com/2016/05/02/iOS-reverse-step-by-step-part-1-class-dump/) by Swiftyper 2016
- [逆向分析网络协议 iOS 篇](http://mp.weixin.qq.com/s?__biz=MzIwMTYzMzcwOQ==&mid=403204191&idx=1&sn=514664cc05597f8b76730cbf9f3a57f5&scene=4#wechat_redirect) by 糖炒小虾
- [别人的 App 不好用？自己改了便是。Moves 篇（上）](http://mp.weixin.qq.com/s?__biz=MzIwMTYzMzcwOQ==&mid=2650948304&idx=1&sn=f76e7b765a7fcabcb71d37052b46e489&scene=4#wechat_redirect) by 糖炒小虾
- [别人的 App 不好用？自己改了便是。Moves 篇（下）](http://mp.weixin.qq.com/s?__biz=MzIwMTYzMzcwOQ==&mid=2650948316&idx=1&sn=584f6c7fe9bf07a28985ffe53da4927e&scene=4#wechat_redirect) by 糖炒小虾
- [别人的 App 不好用？自己改了便是。嘿嘿嘿 篇](http://mp.weixin.qq.com/s?__biz=MzIwMTYzMzcwOQ==&mid=2650948334&idx=1&sn=941d616d25ed16d967595e652e6c4d3b&scene=4#wechat_redirect) by 糖炒小虾
- [iOS逆向之分析微信导航栏实现](http://www.jianshu.com/p/a9cd03044a31) by hi_xgb
