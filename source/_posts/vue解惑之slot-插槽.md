---
title: vue解惑之slot(插槽)
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-28 21:33:51
tags: vue
keywords:
description:
photos:
---
## <font color="red">一.插槽是个什么玩意，能吃吗</font>
- 在vue中【插槽】，从字面意思来看，插槽意味着【内容的增加】，回到vue的使用场景，插槽就是【父组件调用子组件时，额外增加的内容】。
- 插槽显不显示、显示的内容是由父组件来控制的，而插槽在哪里显示由子组件来决定

## <font color="red">二.插槽怎么用，好用吗</font>
#### <font color="green">1.默认插槽</font>
父组件:
``` vue
<template>
  <div>
    父组件的内容
    <slot1>
      <p style="color:red">父组件中插槽内容</p>
    </slot1>
  </div>
</template>
```
子组件:
``` vue
<template>
  <div>
    <div>slot1子组件</div>
    <slot></slot>
  </div>
</template>
<script>
```
效果如下：
![avatar](https://cdn.jsdelivr.net/gh/RobinWM/cdn@2.2/img/articles/slot_1.png)

#### <font color="green">2.具名插槽</font>
#### 顾名思义，就是有具体名字的插槽，子组件中与父组件相对应名字的内容将添加。

#### <font color="green">3.作用域插槽</font>
父组件:

``` vue
<template>
  <div>
    作用域插槽父组件
    <slot2>
      <template slot-scope="user">
        <div v-for="(item, index) in user.data" :key="index">
          <span>姓名：{{item.name}}</span>;
          <span>年龄：{{item.age}}</span>
        </div>
      </template>
    </slot2>
  </div>
</template>
<script>
import slot2 from "./slot2"
export default {
  name: 'main',
  components: {
    slot2
  }
}
</script>
<style scoped>
</style>
```
子组件
``` vue
<template>
  <div>
    作用域插槽的子组件
    <slot :data="user"></slot>
  </div>
</template>

<script>
export default {
  name: 'slot2',
  data () {
    return {
      user: [
        {name: '王五', age: '23'},
        {name: '李二', age: '45'},
        {name: '张三', age: '15'}
      ]
    }
  }
}
</script>
```
效果如下：
![avatar](https://cdn.jsdelivr.net/gh/RobinWM/cdn@2.2/img/articles/slot_2.png)
