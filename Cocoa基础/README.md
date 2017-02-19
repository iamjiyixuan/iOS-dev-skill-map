# Cocoa 基础

## 一、NSObject

### 扩展阅读
- API Reference
  - [NSObject Class Reference](https://developer.apple.com/reference/objectivec/nsobject?language=objc)
  - [NSObject Protocol Reference](https://developer.apple.com/reference/objectivec/1418956-nsobject?language=objc)
- [Foundation: NSObject Class](http://southpeak.github.io/2015/01/31/cocoa-foundation-nsobject-class/) by 南峰子
- [Foundation: NSObject Protocol](http://southpeak.github.io/2015/01/31/cocoa-foundation-nsobject-protocol/) by 南峰子

## 二、字符串

### Unicode

### 汉语拼音

### 扩展阅读
- Guide
  - [String Programming Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/Strings/introStrings.html)
- API Reference
  - [NSString Class Reference](https://developer.apple.com/reference/foundation/nsstring?language=objc)
  - [NSMutableString Class Reference](https://developer.apple.com/reference/foundation/nsmutablestring?language=objc)
- objc.io 期刊 #9 字符串
  - [卷首语](https://objccn.io/issue-9-0/)
  - [NSString 与 Unicode](https://objccn.io/issue-9-1/)
  - [玩转字符串](https://objccn.io/issue-9-2/)
  - [字符串本地化](https://objccn.io/issue-9-3/)
  - [字符串解析](https://objccn.io/issue-9-4/)
  - [字符串渲染](https://objccn.io/issue-9-5/)

## 三、对象间通信

- Method Invocation
- Delegate
- Block
- Notification
- Target-Action
- KVO

Ref:
- [消息传递机制](https://objccn.io/issue-7-4/) by ObjC 中国

### Notification

特点：
- 一对多

关键类：
- 通知 Notification
- 通知中心 NSNotificationCenter
- 通知队列 NSNotificationQueue

关键操作：
- 注册监听者
- 移除监听者
- 发送通知

扩展阅读：
- [浅谈 iOS Notification](http://www.jianshu.com/p/2503e3e5fc64) by 简书 XcodeMen 邓凯辉
