---
title: 重学React(五)之组件间通信
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-09 19:50:12
tags: react
keywords:
description:
photos:
---
# 一.认知组件间的通信

1.在开发过程中，我们会经常遇到需要组件之间相互进行通信：
  -  比如App可能使用了多个Header，每个地方的Header展示的内容不同，那么我们就需要使用者传递给Header一些数据，让 其进行展示； 
  - 又比如我们在Main中一次性请求了Banner数据和ProductList数据，那么就需要传递给他们来进行展示；
  - 也可能是子组件中发生了事件，需要由父组件来完成某些操作，那就需要子组件向父组件传递事件；

2.总之，在一个React项目中，组件之间的通信是非常重要的环节；

3.父组件在展示子组件，可能会传递一些数据给子组件：
  - 父组件通过**属性=值**的形式来传递给子组件数据； 
  - 子组件通过**props**参数获取父组件传递过来的数据；

# 二.父组件传递子组件 - 类组件和函数组件

## 参数propTypes

1.对于传递给子组件的数据，有时候我们可能希望进行验证，特别是对于大型项目来说：
  - 当然，如果你项目中默认集成了Flow或者TypeScript，那么直接就可以进行类型验证； 
  - 但是，即使我们没有使用Flow或者TypeScript，也可以通过 prop-types 库来进行参数验证；

2.更多的验证方式，可以参考[官网](https://zh-hans.reactjs.org/docs/typechecking-withproptypes.html)
  - 比如验证数组，并且数组中包含哪些元素； 
  - 比如验证对象，并且对象中包含哪些key以及value是什么类型； 
  - 比如某个原生是必须的，使用 requiredFunc: PropTypes.func.isRequired;

3.如果没有传递，我们可以使用defaultProps;

# 三.子组件传递父组件

#### 某些情况，我们也需要子组件向父组件传递消息：
  - 在vue中是通过自定义事件来完成的；
  - 在React中同样是通过props传递消息，只是让父组件给子组件传递一个回调函数，在子组件中调用这个函数即可；

# 四.Context应用场景

1.非父子组件数据的共享：
  - 在开发中，比较常见的数据传递方式是通过props属性自上而下（由父到子）进行传递;
  - 但是对于有一些场景：比如一些数据需要在多个组件中进行共享（地区偏好、UI主题、用户登录状态、用户信息等）;
  - 如果我们在顶层的App中定义这些信息，之后一层层传递下去，那么对于一些中间层不需要数据的组件来说，是一种冗余的 操作;

2.如果层级更多的话，一层层传递是非常麻烦，并且代码是非常冗余的:
  - React提供了一个API：Context;
  - Context 提供了一种在组件之间共享此类值的方式，而不必显式地通过组件树的逐层传递 props； 
  - Context 设计目的是为了共享那些对于一个组件树而言是“全局”的数据，例如当前认证的用户、主题或首选语言；

# 五.Context相关API

1.React.createContext
  - 创建一个需要共享的Context对象；
  - 如果一个组件订阅了Context，那么这个组件会从离自身最近的那个匹配的Provider中读取到当前的context值； 
  - defaultValue是组件在顶层查找过程中没有找到对应的Provider，那么就使用默认值；

2.Context.Provider
  - 每个Context对象都会返回一个Provider React组件，它允许消费组件订阅context的变化： 
  - Provider接收一个value属性，传递给消费组件； 
  - 一个Provider可以和多个消费组件有对应关系； 
  - 多个Provider也可以嵌套使用，里层的会覆盖外层的数据； 
  - 当Provider的value值发生变化时，它内部的所有消费组件都会重新渲染；

3.Class.contextType
  - 挂载在class上的contextType属性会被重赋值为一个由React.createContext()创建的Context对象； 
  - 这能让你使用 this.context 来消费最近 Context 上的那个值； 
  - 你可以在任何生命周期中访问到它，包括 render 函数中；

4.Context.Consumer 
  - 这里，React组件也可以订阅到context变更。这能让你在函数式组件中完成订阅context； 
  - 这里需要 函数作为子元素（function as child）这种做法； 
  - 这个函数接收当前的 context 值，返回一个 React 节点；
