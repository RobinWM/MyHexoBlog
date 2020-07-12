---
title: 重学React(四)之深入组件化开发
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-07 19:04:52
tags: react
keywords:
description:
photos:
---
# 一.认识生命周期

- 很多的事物都有从创建到销毁的整个过程，这个过程称之为是生命周期；
- React组件也有自己的生命周期，了解组件的生命周期可以让我们在最合适的地方完成自己想要的功能；
- 生命周期和生命周期函数的关系：

- 生命周期是一个抽象的概念，在生命周期的整个过程，分成了很多个阶段；
  - 比如装载阶段（Mount），组件第一次在DOM树中被渲染的过程；
  - 比如更新过程（Update），组件状态发生变化，重新更新渲染的过程；
  - 比如卸载过程（Unmount），组件从DOM树中被移除的过程；

- React内部为了告诉我们当前处于哪些阶段，会对我们组件内部实现的某些函数进行回调，这些函数就是生命周期函数：
  - 比如实现componentDidMount函数：组件已经挂载到DOM上时，就会回调；
  - 比如实现componentDidUpdate函数：组件已经发生了更新时，就会回调；
  - 比如实现componentWillUnmount函数：组件即将被移除时，就会回调；
  - 我们可以在这些回调函数中编写自己的逻辑代码，来完成自己的需求功能；

- 我们谈React生命周期时，主要谈的类的生命周期，因为函数式组件是没有生命周期函数的；（后面我们可以通过hooks来模拟一些生命周期的回调）。

# 二.生命周期函数

## 先上图：

![avatar](https://cdn.jsdelivr.net/gh/RobinWM/cdn@2.6/img/react/04_react_lifestyle.png)

1.constructor
 - 如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数; 
 - constructor中通常只做两件事情： 
   - 通过给 this.state 赋值对象来初始化内部的state； 
   - 为事件绑定实例（this）；

2.componentDidMount
- componentDidMount()会在组件挂载后(插入DOM树中)立即调用;
- componentDidMount中通常进行哪里操作呢？ 
   - 依赖于DOM的操作可以在这里进行； 
   - 在此处发送网络请求就是最好的地方(官方建议); 
   - 可以在此处添加一些订阅(会在componentWillUnmount取消订阅);

3.componentDidUpdate
- componentDidUpdate()会在更新后会被立即调用，首次渲染不会执行此方法； 
  - 当组件更新后，可以在此处对DOM进行操作； 
  - 如果你对更新前后的props进行了比较，也可以选择在此处进行网络请求；（例如，当props未发生变化时，则不会执行网络请求）

4.componentWillUnmount
- componentWillUnmount()会在组件卸载及销毁之前直接调用: 
  - 在此方法中执行必要的清理操作； 
  - 例如，清除timer，取消网络请求或清除在componentDidMount()中创建的订阅等；   

5.除了上面介绍的生命周期函数之外，还有一些不常用的生命周期函数： 
  - getDerivedStateFromProps：state的值在任何时候都依赖于props时使用；该方法返回一个对象来更新state； 
  - getSnapshotBeforeUpdate：在React更新DOM之前回调的一个函数，可以获取DOM更新前的一些信息（比如说滚动位置）； - shouldComponentUpdate：该生命周期函数很常用， 但是我们等待讲性能优化时再来详细讲解；  

# 三.认识组件的嵌套

1.组件之间存在嵌套关系： 
  - 在之前的案例中，我们只是创建了一个组件App； 
  - 如果我们一个应用程序将所有的逻辑都放在一个组件中，那么这个组件就会变成非常的臃肿和难以维护； 
  - 所以组件化的核心思想应该是对组件进行拆分，拆分成一个个小的组件； 
  - 再将这些组件组合嵌套在一起，最终形成我们的应用程序；

2.上面的嵌套逻辑如下，它们存在如下关系： 
  - App组件是Header、Main、Footer组件的父组件； 
  - Main组件是Banner、ProductList组件的父组件

