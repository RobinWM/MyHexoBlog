---
title: vue组件通信方式总结
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-09-03 19:39:49
tags: vue
keywords:
description:
photos:
---
# 背景
### &emsp;&emsp;组件是vue最基本也是最强大的功能之一，跨组件实例的数据不能直接引用。通常来说，一个vue应用的组件的关系主要表示如下：
![avatar](https://cdn.jsdelivr.net/gh/RobinWM/cdn@2.5/img/vueapp/vue_commucation.png)

### &emsp;&emsp;如图所示：A、B，B、C，B、D之间都是父子关系，C、D是兄弟关系，A和C、D是祖孙关系，当然，有可能A和D之间隔很多代。
### &emsp;&emsp;针对上述关系，选择对的通信方式将大大提高工作效率。本文总结了vue中可用的组件间通信方式。

# 可行性方法
## <font color="red">一.props和$emit</font>
## 1.父组件向子组件传值
### &emsp;&emsp;父组件通过v-bind绑定属性值，子组件通过props接收
``` vue
//  main.vue父组件
<template> 
 <div>
    <!-- v-bind绑定的值userListChild用于在子组件中应用，userList是本组件中 --> 
   <child v-bind:userListChild="userList">
</child> 
 </div>
</template>
<script>
import ChildDemo from '../components/child'
export default { 
   name: 'maindemo', 
   components: {
     "child": ChildDemo
   },
   data() {
        return {
            userList:[
                {name: '王五', age: '23'},
                {name: '李二', age: '45'},
                {name: '张三', age: '15'}
                ]
        } 
   }}
</script>
```

``` vue
//child子组件
<template>
  <div class="hello">
    <ul>
      <li v-for="user in userListChild">{{user.name}}:{{user.age}}</li>    </ul>
  </div>
</template>
<script>
export default {
  name: 'child',
  props:{
    userListChild:{                       // 父组件中v-bind绑定的属性
      type:Array,
      required:true
    }
  }
}
</script>
```

## 2.子组件向父组件传值
### &emsp;&emsp;子组件通过$emit来传值给父组件，准确来说，子组件通过emit事件的机制，当父组件执行某个操作时，把数据的变化通过触发到父组件中对应方法的执行来更新父组件中的变量的值。请看下例：
``` vue
// 子组件child.vue
<template>
    <div>
       <button @click="onSendToMain">传值到父组件</button>
    </div>
</template>
<script>
export default {
    name:'child',
    methods:{
       onSendToMain(){
          this.$emit('onReciveFromChild','我是从子组件传过来的值')
        }
    }}
</script>
```

### &emsp;&emsp;点击“传值到父组件”按钮，执行子组件中onSendToMain方法，调用vue事件机制核心方法&emit。
``` vue
//  main.vue父组件
<template>
  <div>
    <div>
      {{title}}
    </div>
    <!-- v-bind绑定的值userListChild用于在子组件中应用，userList是本组件中 -->
    <child v-on:onReciveFromChild="onReceive">
    </child>
  </div>
</template>
<script>
import ChildDemo from '../components/child'
export default {
  name: 'maindemo',
  components: {
    "child":ChildDemo
  },
  data () {
    return {
      title: '我是父组件的title'
    }
  },
  methods:{
    onReceive(params){
      this.title = params;
    }
  }}
</script>
```
### &emsp;&emsp;父组件应用子组件时，绑定一个方法，方法名要和子组件中$emit函数第一个参数的值保持一致。

## <font color="red">二.$parent/$children和ref</font>
## &emsp;&emsp;我们都知道，在vue中，带$开头的方法是挂载在vue实例原型中的方法，用$来区别一般的方法。$parent和$children分别代表父组件和子组件实例，所以我们可以通过调用父或子实例相应的方法来改变对应的值。请看下面的例子：
``` vue
//  main.vue父组件
<template>
  <div>
    <div>
      <h1>{{title}}:{{name}}</h1>
      <button @click="onSendToChild">传值到子组件</button>
    </div>
    <child></child>
  </div>
</template>
<script>import ChildDemo from '../components/child'
export default {
  name: 'maindemo',
  components: {
    "child":ChildDemo
  },
  data () {
    return { 
     title: '我是父组件的title',
      name: 'Robin'
    }  },
  methods:{
    onReceive(params){
      this.title = params;
      console.log(params)
    },
    onSendToChild(){
      this.$children[0].title = "我是从父组件传过来的值"
    }, 
    workFromChild(name){
      this.name = name
    }
  }}
</script>
```

``` vue
// 子组件child.vue
<template>
    <div>
       <h1>{{title}}</h1>
       <button @click="onSendToMain">传值到父组件</button>
    </div>
</template>
<script>
export default {
    name:'child',
    data() {
        return {
            title: '我是子组件的title' 
       }
    },
    methods:{
       onSendToMain(){ 
        //  this.$parent.title = '我是从子组件传过来的值1'
        const name = "范闲"
        this.$parent.workFromChild(name);
       }
    }}
</script>
```

#### 注：$children返回的是一个数组，表示该父组件所有子组件实例的集合。

## <font color="red">三.$refs</font>
## &emsp;&emsp;ref用在子组件中表示该子组件的实例，用法和上面的$children大致相同,不同的$refs可以拿到具名子组件实例，而$children拿到的是一个数组：
``` vue
//  main.vue父组件
<template>
  <div>
    <div>
      <button @click="onSendToChild">传值到子组件</button>
    </div>
    <child ref="child"></child>
  </div>
</template>
<script>
import ChildDemo from '../components/child'
export default {
  name: 'maindemo',
  components: {
    "child":ChildDemo
  },
  methods:{
    onSendToChild(){
      this.$refs.child.title = "我是从父组件传过来的值"
    }
  }}</script>
```
### &emsp;&emsp;注：ref用在普通DOM元素上，表示该元素的实例。  

## <font color="red">四.Provider/Inject</font>
## vue中的provider/inject是依赖注入程序设计模式在vue中的一种实现。使用如下：
- provide 提供变量：```Object | () => Object```
- inject 注入变量： ```Array<string> | { [key: string]: string | Symbol | Object }```
## &emsp;&emsp;provider是一个对象或返回一个对象的函数，该对象包含可注入其子孙的属性。
## &emsp;&emsp;inject是一个字符串数组或对象，该对象包含从上级组件注入到该下级组件的所有属性。
请看下面的例子：
``` vue
//  main.vue父组件
<template>
  <div>
    <child></child>
  </div>
</template>
<script>
import ChildDemo from '../components/child'
export default {
  name: 'mainDemo',
  provide: {
      name: "Robin"
  },
  components: { 
   "child":ChildDemo
  }
}
</script>
```

``` vue
// 子组件child.vue
<template>
    <div>
       <h1>{{name}}</h1>
    </div>
</template>
<script>
export default {
    name:'child',
    inject: ['name']
}
</script>
```
### &emsp;&emsp;需要注意的是，provide和inject并不是响应式的，即上级组件值的变化，下级组件并不会同步更新。但是，如果传入一个可监听的对象，也是可以响应的。进阶版如下：
``` vue
//  main.vue父组件
<template>
  <div>
    <child></child> 
   <button @click="changeName">改变name值</button>
  </div>
</template>
<script>
import ChildDemo from '../components/child'
export default {
  name: 'mainDemo',
  data() {
      return { 
         nameObj: {
              name: "Robin"
          }
      }
  },
  provide() {
      return {
          nameObj: this.nameObj
      }
  },
  components: {
    "child":ChildDemo
  },
  methods:{
      changeName() {
          this.nameObj.name = 'huey'
      }
  }}
</script>
```

``` vue
// 子组件child.vue
<template>
    <div>
       <h1>{{nameObj.name}}</h1>
    </div>
</template>
<script>
export default {
    name:'child',
    inject: ['nameObj']
}
</script>
```
### &emsp;&emsp;模拟我们项目开发中的实际使用场景，当某个操作改变上级组件的某个值时，上面改进的方式可以做到响应式，即下级组件中可以同步刷新。

## <font color="red">五.&emit和on</font>
## &emsp;&emsp;这种方法通过一个空的Vue实例作为事件中心，用它来触发监听事件,可以实现任意组件间的通信，包括父子、兄弟、跨级。请看下面的用例：
``` vue
//  main.vue父组件
<template>
  <div>
    <child-a></child-a>
    <child-b></child-b>
  </div>
</template>
<script>
import ChildA from './child-a'
import ChildB from './child-b'
export default {
  name: 'mainDemo',
  components: {
    "child-a": ChildA,
    "child-b": ChildB
  },
  methods:{
      changeName() {
          this.name = 'huey'
      }
  }}
</script>
```

``` vue
//  事件中转工具Event.js
import Vue from "vue"
export default new Vue()
```

``` vue
// 子组件child-a.vue
<template>
  <div>
    <h1>{{name}}</h1>
    <button @click="changeName">改变值</button>
  </div>
</template>
<script>
import Event from './Event'
export default {
        name:'child-a',
        data() {
            return {
                name: "huey"
            }
        },
        methods: { 
           changeName() {
                Event.$emit('nameChanged', '我是好人')
            }
        }
    }
</script>
```

``` vue
// 子组件child-b.vue
<template>
    <div>
       <h1>{{title}}</h1>
    </div>
</template>
<script>
import Event from "./Event"
export default {
    name:'child-b',
    data() {
        return {
            title: "Robin"
        }
    },
    mounted() {
        Event.$on("nameChanged", data=> {
            console.log(data)
            this.title = data
        })
    }}
</script>
```
### &emsp;&emsp;注：此种方法适用于项目组件关系依赖少，并不适用于大型项目。

## <font color="red">六.$attrs/$listeners</font>
- $attrs：包含了父作用域中不被 prop 所识别的特性绑定 (class 和 style 除外)。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 (class 和 style 除外)，并且可以通过 v-bind="$attrs" 传入内部组件。通常配合 interitAttrs 选项一起使用。- $listeners：包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 v-on="$listeners" 传入内部组件。
## &emsp;&emsp;这是官方的解释，简单来说，父组件绑定在子组件中的属性是一个集合，$attrs包含了除了prop所就收的以及class和style属性之外的所有属性。请看下面例子:
``` vue
//  main.vue父组件
<template>
  <div>
    <child-a :name="name" :age="age" v-on:onName="changeName" v-on:onAge="changeAge"></child-a>
    {{name}}:{{age}}
  </div>
</template>
<script>
import ChildA from './child-a'
export default { 
 name: 'mainDemo',
  components: {
    "child-a": ChildA,
  },
  data () {
      return {
          name: "Robin",
          age: "27"
      }
  },
  methods:{
      changeName(name) {
          this.name = name
      },
      changeAge(age) {
          this.age = age
      }
  }}
</script>
```
### 父组件分别绑定了name和age属性,并绑定了onAge和onName事件，请看子组件如何接收：
``` vue
// 子组件child-a.vue
<template>
  <div>
    <grand-child v-bind="$attrs" v-on="$listeners"></grand-child>
    <button @click="childChange">子组件改变姓名</button>
  </div>
</template>
<script>
    import grandChild from "./grandChild";
    export default {
        name:'child-a',
        data() {
            return {
                name: "huey"
            }
        },
        components: { 
           "grand-child":grandChild
        }, 
       props:['age'],
        mounted() {
            console.log(this.$attrs)         // {name: "huey"}
            console.log(this.$listeners)     // {onName: ƒ, onAge: ƒ}
        },
        methods: {
            childChange() {
                this.$emit('onName', 'Huey')
            }
        }
    }
</script>
```
### &emsp;&emsp;子组件中通过props接收name属性，所以此时$attrs的值为{name:"huey"}，如果没有props，$attrs的值为{name: "huey", age: "27"}。$listeners包含了父组件中所有绑定事件的集合，它的值为：{onName: ƒ, onAge: ƒ}。另外，子组件中通过v-bind="$attrs"绑定在孙子组件中，通过v-on="$listeners"把事件绑定在孙子组件中，孙子组件可以直接拿到$attrs和$listeners：
``` vue
// 孙子组件grandChild
<template>
  <div>
    <button @click="grandChildChange">孙子组件改变年龄</button>
  </div>
</template>
<script>
    export default {
        name: "grandChild",
        mounted() {
            console.log(this.$attrs)   // {name: "huey"}
        }, 
       methods: {
            grandChildChange() {
                this.$emit('onAge', '18')
            }
        }
    }
</script>
```
### &emsp;&emsp;因为上一步绑定了$attrs和$listeners，所以可以直接应用，这样就可以在孙子组件中回传值给父组件。

## <font color="red">七.vuex</font>
###关于Vuex，请参阅{% post_link vuex从入门实战 vuex从入门到实战 %}

