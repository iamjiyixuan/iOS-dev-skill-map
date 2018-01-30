# React

## 1. toolchain
- [Visual Studio Code](https://code.visualstudio.com)
- [Node.js](https://nodejs.org/en/) + [nvm](https://github.com/creationix/nvm)
- [npm](https://www.npmjs.com) / [yarn](https://yarnpkg.com/zh-Hans/)
- private npm repo server
    - [sinopia](https://github.com/rlidwka/sinopia)
    - [verdaccio](https://github.com/verdaccio/verdaccio) - a fork of sinopia
- [create-react-app](https://github.com/facebookincubator/create-react-app) / [roadhog](https://github.com/sorrycc/roadhog)
- [Babel](https://babeljs.io)
- [webpack](https://webpack.js.org)
- [ESLint](https://eslint.org)
- [Prettier](https://prettier.io) - Code Formatter
- [Electron](https://electronjs.org)
- Test
    - [Jest](http://facebook.github.io/jest/)
    - [enzyme](http://airbnb.io/enzyme/)
- HTTP
    - 标准 Fetch
    - 兼容版 Fetch: [github-fetch](https://github.com/github/fetch) / [isomorphic-fetch](https://github.com/matthew-andrews/isomorphic-fetch)
    - 基于 [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) 的 [axios](https://github.com/axios/axios)

## 2. 搭建舒适的开发环境

### 2.1. Node.js

### 2.2. yarn 替代 npm

### 2.3. 用 VS Code 编写代码

### 2.4. 用 Babel  

## 3. 使用 Jest 编写单元测试

### 3.1. 测试异步函数
- Callback API
- Promise API
- Async/Await

### 3.2. Mock

## 4. References

### 4.1. React Native
- [RN 官网](http://facebook.github.io/react-native/)
- [React Native 通信机制详解](http://blog.cnbang.net/tech/2698/) by bang 2015
- [React Native 源码导读(零) – 创建/运行/调试](http://blog.cnbang.net/tech/3461/) by bang 2017
- [ReactNative 源码解析 —— 通信机制详解(1/2)](http://zxfcumtcs.github.io/2017/10/08/ReactNativeCommunicationMechanism/) by 赵雪峰 2017
- [ReactNative 源码解析 —— 通信机制详解(2/2)](http://zxfcumtcs.github.io/2017/10/12/ReactNativeCommunicationMechanism2/) by 赵雪峰 2017
- [ReactNative 源码解析 —— 通信机制详解(补充条款)](http://zxfcumtcs.github.io/2017/11/22/RNCommunicationMechanism-AdditionalTerms/) by 赵雪峰 2017
- [React Native 在 Glow 的实践](http://tech.glowing.com/cn/react-native-at-glow/) by Glow 技术团队 2017
- [如何实现 React Native 里的页面导航系统](http://tech.glowing.com/cn/all-about-routing-and-navigation-in-react-native/) by Glow 技术团队 2018

### 4.2. Electron
- [How to build an Electron app using create-react-app. No webpack configuration or “ejecting” necessary.](https://medium.freecodecamp.org/building-an-electron-application-with-create-react-app-97945861647c) by Christian Sepulveda