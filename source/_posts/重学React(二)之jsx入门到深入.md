---
title: 重学React(二)之jsx入门到深入
author: Robin
avatar: "https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg"
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-04 21:33:46
tags: react
keywords:
description:
photos:
---

# 一.JSX 是什么

- JSX 是一种 JavaScript 的语法扩展（eXtension），也在很多地方称之为 JavaScript XML，因为看起就是一段 XML 语法；
- 它用于描述我们的 UI 界面，并且其完成可以和 JavaScript 融合在一起使用；
- 它不同于 Vue 中的模块语法，你不需要专门学习模块语法中的一些指令（比如 v-for、v-if、v-else、v-bind）;

# 二.React 选择 JSX 的原因

1.React 认为渲染逻辑本质上与其他 UI 逻辑存在内在耦合：

- 比如 UI 需要绑定事件（button、a 原生等等）；
- 比如 UI 中需要展示数据状态，在某些状态发生改变时，又需要改变 UI；

  2.他们之间是密不可分，所以 React 没有将标记分离到不同的文件中，而是将它们组合到了一起，这个地方就是组件；

  3.JSX 其实是嵌入到 JavaScript 中的一种结构语法；

# 三.JSX 的书写规范

- JSX 的顶层只能有一个根元素，所以我们很多时候会在外层包裹一个 div 原生（或者使用后面我们学习的 Fragment）；
- 为了方便阅读，我们通常在 jsx 的外层包裹一个小括号()，这样可以方便阅读，并且 jsx 可以进行换行书写；
- JSX 中的标签可以是单标签，也可以是双标签；

#### 注意：如果是单标签，必须以/>结尾；

# 四.JSX 的使用

1.jsx 中的注释；
`{/* 这是一段注释 */}`

2.JSX 嵌入变量：

- 当变量是 Number、String、Array 类型时，可以直接显示；
- 当变量是 null、undefined、Boolean 类型时，内容为空；
  - 如果希望可以显示 null、undefined、Boolean，那么需要转成字符串；
  - 转换的方式有很多，比如 toString 方法、和空字符串拼接，String(变量)等方式；
- 对象类型不能作为子元素（not valid as a React child）

  3.JSX 嵌入表达式

  - 运算表达式；
  - 三元运算符；
  - 执行一个函数；

    4.JSX 绑定属性

- 普通属性绑定：

```HTML
<h2 title={title}>我是标题</h2>
```

- 绑定 class 类：

```HTML
<div className={"contents " + (active ? "active" : "")}>我是div绑定class</div>
```

- 绑定 style 样式:

```HTML
 <div style={{color: "red", fontSize: "10px"}}>我是div绑定style</div>
```

5.JSX 绑定事件及参数传递

#### 推荐使用如下方式：

```HTML
<button onClick={e => { this.btnClick4(e) }}>按钮4</button>
```

# 五.JSX 的本质

1.jsx 是什么:

#### 实际上，jsx仅仅只是React.createElement(component,props, ...children)函数的语法糖。<font color="red">所有的jsx最终都会被转换成React.createElement的函数调</font>

2.createElement函数

- 参数一：type
 - 当前ReactElement的类型； 
 - 如果是标签元素，那么就使用字符串表示 “div”； 
 - 如果是组件元素，那么就直接使用组件的名称；

-参数二：config 
 - 所有jsx中的属性都在config中以对象的属性和值的形式存储 

-参数三：children 
 - 存放在标签中的内容，以children数组的方式进行存储； 
 - 当然，如果是多个元素呢？React内部有对它们进行处理，处理的源码在下方；

