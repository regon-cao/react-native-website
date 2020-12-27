---
id: libraries
title: 使用第三方库
author: Brent Vatne
authorURL: "https://twitter.com/notbrent"
description: This guide introduces React Native developers to finding, installing, and using third-party libraries in their apps.
---

React Native 提供了一系列内置的[核心组件和 API](components-and-apis)，但并不局限于此。React Native 有一个庞大的社区，如果核心组件和 API 不能满足你的需求，你完全可以去社区的广阔天地中寻求合适的第三方库。

## 选择一个包管理器

React Native libraries are typically installed from the [npm registry](https://www.npmjs.com/) using a Node.js package manager such as [npm CLI](https://docs.npmjs.com/cli/npm) or [Yarn 经典版(v1)](https://classic.yarnpkg.com/en/).

If you have Node.js installed on your computer then you already have the npm CLI installed. Some developers prefer to use Yarn Classic for slightly faster install times and additional advanced features like Workspaces. Both tools work great with React Native. We will assume npm for the rest of this guide for simplicity of explanation.

> 💡 在 JavaScript 社区，“库（library）”和“包（package）”这两个术语一直是混用的，可视为等同。

## 安装第三方库

To install a library in your project, navigate to your project directory in your terminal and run `npm install <name-of-the-library>`. Let's try this with `react-native-webview`:

```bash
npm install react-native-webview
```

The library that we installed includes native code, and we need to link to our app before we use it.

## 链接 iOS 原生代码

React Native uses CocoaPods to manage iOS project dependencies and most React Native libraries follow this same convention. If a library you are using does not, then please refer to their README for additional instruction. In most cases, the following instructions will apply.

Run `pod install` in our `ios` directory in order to link it to our native iOS project. A shortcut for doing this without switching to the `ios` directory is to run `npx pod-install`.

```bash
npx pod-install
```

Once this is complete, re-build the app binary to start using your new library:

```bash
npx react-native run-ios
```

## 链接 Android 原生代码

React Native uses Gradle to manage Android project dependencies. After you install a library with native dependencies, you will need to re-build the app binary to use your new library:

```bash
npx react-native run-android
```

## 搜索第三方库

[React Native Directory](https://reactnative.directory) is a searchable database of libraries built specifically for React Native. This is the first place to look for a library for your React Native app.

Many of the libraries you will find on the directory are from [React Native Community](https://github.com/react-native-community/) or [Expo](https://docs.expo.io/versions/latest/).

Libraries built by the React Native Community are driven by volunteers and individuals at companies that depend on React Native. They often support iOS, tvOS, Android, Windows, but this varies across projects. Many of the libraries in this organization were once React Native Core Components and APIs.

Libraries built by Expo are all written in TypeScript and support iOS, Android, and react-native-web wherever possible. They usually require that you first install [react-native-unimodules](https://github.com/expo/expo/tree/master/packages/react-native-unimodules) in order to use in your React Native app.

After React Native Directory, the [npm registry](https://www.npmjs.com/) is the next best place if you can't find a library specifically for React Native on the directory. The npm registry is the definitive source for JavaScript libraries, but the libraries that it lists may not all be compatible with React Native. React Native is one of many JavaScript programming environments, including Node.js, web browsers, Electron, and more, and npm includes libraries that work for all of these environments.

## 判断第三方库的兼容性

### 它支持 React Native 吗？

Usually libraries built _specifically for other platforms_ will not work with React Native. Examples include `react-select` which is built for the web and specifically targets `react-dom`, and `rimraf` which is built for Node.js and interacts with your computer file system. Other libraries like `lodash` use only JavaScript langauge features and work in any environment. You will gain a sense for this over time, but until then the easiest way to find out is to try it yourself. You can remove packages using `npm uninstall` if it turns out that it does not work in React Native.

### 它支持某个系统平台吗？

[React Native Directory](https://reactnative.directory/) allows you to filter by platform compatibility, such as iOS, Android, Web, and Windows. If the library you would like to use is not currently listed there, refer to the README for the library to learn more.

### 它支持我的 React Native 的版本吗?

The latest version of a library is typically compatible with the latest version of React Native. If you are using an older version, you should refer to the README to know which version of the library you should install. You can install a particular version of the library by running `npm install <library-name>@<version-number>`, for example: `npm install @react-native-community/netinfo@^2.0.0`.

---

##### 本文档贡献者：[sunnylqm](https://github.com/search?q=sunnylqm&type=Users)(97.40%), [sunnylqm](https://github.com/search?q=sunnylqm&type=Users)(2.60%)
