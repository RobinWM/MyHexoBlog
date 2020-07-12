---
title: 重学React(三)之认识组件
author: Robin
avatar: "https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg"
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-06 19:15:33
tags: react
keywords:
description:
photos:
---

# 一.分而治之思想

- 人面对复杂问题的处理方式：
  - 任何一个人处理信息的逻辑能力都是有限的；
  - 所以，当面对一个非常复杂的问题时，我们不太可能一次性搞定一大堆的内容；
  - 但是，我们人有一种天生的能力，就是将问题进行拆解；
  - 如果将一个复杂的问题，拆分成很多个可以处理的小问题，再将其放在整体当中，你会发现大的问题也会迎刃而解；
- 其实上面的思想就是分而治之的思想：
  - 分而治之是软件工程的重要思想，是复杂系统开发和维护的基石；
  - 而前端目前的模块化和组件化都是基于分而治之的思想

# 二.什么是组件化开发

1.组件化也是类似的思想： 
  - 如果我们将一个页面中所有的处理逻辑全 部放在一起，处理起来就会变得非常复杂， 而且不利于后续的管理以及扩展。
  - 但如果，我们讲一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，那么之后整个页面的管理  和维护就变得非常容易了。

2.我们需要通过组件化的思想来思考整个应用程序： 
  - 我们将一个完整的页面分成很多个组件； 
  - 每个组件都用于实现页面的一个功能块； 
  - 而每一个组件又可以进行细分； 
  - 而组件本身又可以在多个地方进行复用;

# 三.React的组件化

1.组件化是React的核心思想，也是我们后续课程的重点，前面我们封装的App本身就是一个组件： 
  - 组件化提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用; 
  - 任何的应用都会被抽象成一颗组件树;

2.组件化思想的应用： 
  - 有了组件化的思想，我们在之后的开发中就要充分的利用它； 
  - 尽可能的将页面拆分成一个个小的、可复用的组件；
  - 这样让我们的代码更加方便组织和管理，并且扩展性也更强；

3.React的组件相对于Vue更加的灵活和多样，按照不同的方式可以分成很多类组件： 
  - 根据组件的定义方式，可以分为：函数组件(Functional Component )和类组件(Class Component)； 
  - 根据组件内部是否有状态需要维护，可以分成：无状态组件(Stateless Component )和有状态组件(Stateful Component);
  - 根据组件的不同职责，可以分成：展示型组件(Presentational Component)和容器型组件(Container Component);

4.这些概念有很多重叠，但是他们最主要是关注数据逻辑和UI展示的分离： 
  - 函数组件、无状态组件、展示型组件主要关注UI的展示； 
  - 类组件、有状态组件、容器型组件主要关注数据逻辑；  

5.当然还有很多组件的其他概念：比如异步组件、高阶组件;

# 四.类组件

1.类组件的定义有如下要求： 
  - 组件的名称是大写字符开头（无论类组件还是函数组件）; 
  - 类组件需要继承自 React.Component; 
  - 类组件必须实现render函数;

2.在ES6之前，可以通过create-react-class 模块来定义类组件，但是目前官网建议我们使用ES6的class类定义;

3.使用class定义一个组件： 
  - constructor是可选的，我们通常在constructor中初始化一些数据； 
  - this.state中维护的就是我们组件内部的数据； 
  - render() 方法是 class 组件中唯一必须实现的方法;

``` JavaScript
// 1.类组件
export class ClassApp extends Component {
  constructor() {
    super();

    this.state = {
      message: 'Hello React'
    }
  }

  render() {
    return (
      <h2>{this.state.message}</h2>
    )
  }
}
```

# 五.render函数的返回值

## 当 render 被调用时，它会检查 this.props 和 this.state 的变化并返回以下类型之一：

1.React元素： 
  - 通常通过JSX创建; 
  - 例如，```<div/>```会被React渲染为DOM节点，```<MyComponent/>```会被React渲染为自定义组件； 
  - 无论是```<div/>```还是```<MyComponent/>```均为React元素；

2.数组或 fragments：使得 render 方法可以返回多个元素;

3.Portals：可以渲染子节点到不同的 DOM 子树中;

4.字符串或数值类型：它们在 DOM 中会被渲染为文本节点;

5.布尔类型或 null：什么都不渲染;

# 六.函数组件

1.函数组件是使用function来进行定义的函数，只是这个函数会返回和类组件中render函数返回一样的内容； 

2.函数组件有自己的特点（当然，后面我们会讲hooks，就不一样了）： 
  - 没有生命周期，也会被更新并挂载，但是没有生命周期函数； 
  - 没有this(组件实例）； 
  - 没有内部状态（state）;

``` Javascript
// 2.函数式组件
export function FunctionApp() {
  return (
    <div>我是函数式组件</div>
  )
}
```