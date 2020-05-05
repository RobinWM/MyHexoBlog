---
title: vuex从入门实战
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-09-05 22:16:45
tags: vue
keywords:
description:
photos:
---
# 一.vuex是什么
### &emsp;&emsp;官方解释：Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。讲真的，这个解释，大部分人都不懂，换个通俗易懂的说法：Vuex用来存储数据的状态，即数据的变化。当vue应用程序的组件结构复杂程度提高时，采用传统的方法通信将变的繁琐而且不易维护，vuex正是为了解决这个问题而出现的。下面是vuex实现数据流的示意图：
![avatar](https://cdn.jsdelivr.net/gh/RobinWM/cdn@2.5/img/vueapp/vuex.png)

接下来，我们一步步来理解其中专业名词的意义。

# 二.vuex核心概念及应用
### &emsp;&emsp;解释这些概念之前，请先添加vuex到项目中：使用命令 vue add vuex(本文使用的是vue-cli@3.1.0)。

## <font color="red">1.Store</font>
#### &emsp;&emsp;每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state) 。      
#### &emsp;&emsp;上述添加vuex的过程会在项目src目录下生成一个名字为store的文件夹，该文件夹下有一个名字为index.js的文件，它就是一个store，代码如下：
``` vue
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
export default new Vuex.Store({
  state: {  },
  mutations: {  },
  actions: {  },
  modules: {  }
})
```

## <font color="red">2.State</font>
#### &emsp;&emsp;Vuex 使用单一状态树——是的，用一个对象就包含了全部的应用层级状态。至此它便作为一个“唯一数据源 (SSOT)”而存在。单一状态树让我们能够直接地定位任一特定的状态片段，在调试的过程中也能轻易地取得整个当前应用状态的快照。   
#### &emsp;&emsp;改写上面的store中state，没错，就是index.js文件，如下：
``` vue
state: {  name: 'Robin',  age: 27}
```
#### &emsp;&emsp;在组件中我们使用$store.state.name来引用name属性，因为store中数据状态是响应式的，所以我们使用computed：
``` vue
<template>
  <div>
    {{name}}
  </div>
</template>
<script>
export default {
  name: 'mainDemo',
  computed: {
      name () {
          return this.$store.state.name
      }
  }}
</script>
```

## <font color="red">3.Getter</font>
#### &emsp;&emsp;有这样一个场景：我们需要从 store 中的 state 中派生出一些状态，例如对列表进行过滤并计数：
``` vue
computed: {
    getTodosCount(){
        return this.$store.state.todos.filter(todo => todo.done).length
    }
}
```

#### &emsp;&emsp;如果有多个组件需要用到此属性，我们要么复制这个函数，或者抽取到一个共享函数然后在多处导入它——无论哪种方式,都会写很多重复的代码。      
#### &emsp;&emsp;Vuex 允许我们在 store 中定义“getter”（可以理解为 store 的计算属性）。就像计算属性一样，getter 的返回值会根据它的源被存储下来，且只有当它的源值发生了改变才会被重新计算。改写上面的index.js：
``` vue
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
export default new Vuex.Store({
  state: {
    name: 'Robin',
    age: 27,
    tasksList: [
       {id: 1, descript: "模块1", done:false},
       {id: 2, descript: "模块2", done:false},
       {id: 3, descript: "模块3", done:true},
    ]
  },
  getters: {
    getTasks(state) {
       return state.tasksList.filter(list => list.done)
    }
  }})
```
在组件中引用：```this.$store.getters.getTasks```。

## <font color="red">4.Mutation</font>
#### &emsp;&emsp;提交mutation是改变state中数据状态的唯一方法。Vuex中的mutation非常类似于事件：每个mutation都有一个字符串的事件类型(type)和一个回调函数(handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受state作为第一个参数，payload作为第二个参数（额外的参数):
``` vue
state: {
  name: 'Robin',
  age: 27,
  tasksList: [
     {id: 1, descript: "模块1", done:false},
     {id: 2, descript: "模块2", done:false},
     {id: 3, descript: "模块3", done:true},
  ]},
mutations: {
   afterBirthday(state,adds) {
       state.age += adds
   }
}
```
**&emsp;&emsp;在组件中使用的$store.commit方法：**
``` vue
this.$store.commit('afterBirthday' , 1)
```
### **注：mutation 里面的事件，必须是同步函数，同步函数，同步函数**

## <font color="red">5.Action</font>
#### &emsp;&emsp;Action类似于mutation,不同在于：
- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。
**先定义一个action:**
``` vue
state: {
  name: 'Robin',  age: 27,
},
mutations: {
   afterBirthday(state,adds) {
       state.age += adds
   }
},
actions: {
    increment(context) {
        context.commit("afterBirthday")
    }
}
```
#### &emsp;&emsp;increment函数接受一个与 store 实例具有相同方法和属性的 context 对象，因此你可以调用 context.commit 提交一个 mutation，或者通过 context.state 和 context.getters 来获取 state 和 getters。       
#### &emsp;&emsp;我们可以在store内部执行异步操作,改写上面的increment:
``` vue
increment(context) {
    setTimeout(()=> {
        context.commit("afterBirthday")
    },1000)
}
```
#### &emsp;&emsp;在组件中调用action的方式为$store.dispatch:
``` vue
this.$store.dispatch('increment')
```

## <font color="red">6.modules</font>
#### &emsp;&emsp;由于使用单一的状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂，store对象就会变得非常臃肿；为了解决这个问题，Vuex允许我们将store分隔成模块（module），每个模块拥有自己的state，mutation，action，getter，甚至是嵌套子模块。新建一个包含moduleA和moudleB的store,如下
``` vue
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
const moduleA= {
    namespaced:false,
        state: { 
        age: 20,
        name: "Robin",
        count: 0,
        tasksList: [
            {id: 1, descript: "模块1", done:false}, 
            {id: 2, descript: "模块2", done:false},
            {id: 3, descript: "模块3", done:true},
        ]
    },
    getters: {
        getTasks(state) {
            return state.tasksList.filter(list => list.done)
        }
    },
    mutations: {
        increment(state,addNumber) {
            state.age+=addNumber
        }
    },
    actions: {
        doCountChange(context) {    
            if (context.state.age === context.rootState.B.age) {
                context.commit('increment',7)
            }
        }
    },
}
const moduleB= {
    namespaced:true,
    state:{
        age: 27,
        name: "Huey",
        count: 1
    },
    mutations:{},
    getters: {
            doubleCounts(state) {
              return state.age * 2 
           } 
   }
}
export default new Vuex.Store({
    modules:{
        A:moduleA,
        B:moduleB,
    }
})
```
#### 有以下几点需要说明：
1.在模块中，state是被限制到模块的命名空间下，需要命名空间才能访问，比如需要拿到A中的taskList:this.$store.state.A.taskList;
2.actions和mutations, getters没有被限制，在默认情况下(namespaced:false)，它们是注册到全局命名空间下的，所谓的注册到全局命名空间下，其实就是我们访问它们的方式和原来没有module 的时候是一样的，例如，要访问getTasks：this.$store.getters['getTasks'];
3.当在module中设置namespaced:true时，actions 和mutations,  getters就有域的限制，不能直接通过原来的方式访问，同样，要访问getTasks: this.$store.getters['A/getTasks']，其中'A'表示getTasks在‘A’模块之下。