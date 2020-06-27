---
title: 重学React（一）之初体验
author: Robin
avatar: "https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg"
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-01 19:15:26
tags: react
keywords:
description:
photos:
---

# 一.React 的特点

## 1.声明式编程

- 声明式编程是目前整个大前端开发的模式：Vue、React、Flutter、SwiftUI；
- 它允许我们只需要维护自己的状态，当状态改变时，React 可以根据最新的状态去渲染我们的 UI 界面；

## 2.组件化开发

- 组件化开发页面目前前端的流行趋势，我们会讲复杂的界面拆分成一个个小的组件；
- 如何合理的进行组件的划分和设计也是后面我会讲到的一个重点；

## 3.多平台适配

- 2013 年，React 发布之初主要是开发 Web 页面；
- 2015 年，Facebook 推出了 ReactNative，用于开发移动端跨平台；（虽然目前 Flutter 非常火爆，但是还是有很多公司在使用 ReactNative）；
- 2017 年，Facebook 推出 ReactVR，用于开发虚拟现实 Web 应用程序；（随着 5G 的普及，VR 也会是一个火爆的应用场景）；

# 二.React 开发依赖

## 1.开发 React 必须依赖三个库：

- react：包含 react 和 react-native 所共同拥有的核心代码；
- react-dom：react 渲染在不同平台所需要的核心代码；
- babel：将 jsx 转换成 React 代码的工具；

## 2.React-dom 的特殊性

- web 端：react-dom 会讲 jsx 最终渲染成真实的 DOM，显示在浏览器中；
- native 端：react-dom 会讲 jsx 最终渲染成原生的控件（比如 Android 中的 Button，iOS 中的 UIButton）。

## 3.Bebel 的作用

- Babel ，又名 Babel.js；
- 是目前前端使用非常广泛的编辑器、转移器；
- 比如当下很多浏览器并不支持 ES6 的语法，但是确实 ES6 的语法非常的简洁和方便，我们开发时希望使用它；
- 那么编写源码时我们就可以使用 ES6 来编写，之后通过 Babel 工具，将 ES6 转成大多数浏览器都支持的 ES5 的语法；

## 4.React 和 Babel 的关系

- 默认情况下开发 React 其实可以不使用 babel；
- 但是前提是我们自己使用 React.createElement 来编写源代码，它编写的代码非常的繁琐和可读性差。
- 那么我们就可以直接编写 jsx（JavaScript XML）的语法，并且让 babel 帮助我们转换成 React.createElement。

# 三.引入 React 依赖

## 1.引入方式

1.直接 CDN 引入; 2.下载后，添加本地依赖; 3.通过 npm 管理（后续脚手架再使用）

注： 暂时我们直接通过 CDN 引入，来演练下面的示例程序。

| 这里有一个 crossorigin 的属性，这个属性的目的是为了拿到跨域脚本的错误信息；

```HTML
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

# 四.练习代码

``` HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Title</title>
</head>
<body>

<div id="app">app</div>

<!--添加依赖-->
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

<script type="text/babel">

  // 封装app组件
  class App extends React.Component {
    constructor() {
      super();
      // this.message = "Hello World";
      this.state = {
        message: "Hello World"
      }
    }

    render() {
      return (
        <div>
          <h2>{this.state.message}</h2>
          <button onClick={this.btnClick.bind(this)}> 改变</button>
        </div>
      )
    }

    btnClick() {
      // console.log(this);
      // this.message = "Hello React";
      this.setState({
        message: "Hello React"
      })
    }
  }

  ReactDOM.render(<App/>, document.getElementById("app"));
</script>

</body>
</html>

```