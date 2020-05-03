---
title: vue解惑之v-on(事件监听指令)
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-09-01 17:09:05
tags: vue
keywords:
description:
photos:
---
## <font color="green">一.v-on指令</font>
### vue中用v-on指令来监听DOM事件，并触发相应的代码。比如v-on:click,表示监听了点击事件。

## <font color="green">二.事件修饰符</font>
#### &emsp;&emsp;在事件处理函数中调用event.preventDefault()等方法是非常常见的需求。但更好的方式是：处理函数只有纯粹的数据逻辑，而不是去处理DOM事件细节。为了解决这个问题，Vue.js为v-on提供了事件修饰符。
- .stop
- .prevent
- .capture
- .self
- .once
- .passive

``` vue
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

## <font color="green">三.按键修饰符</font>
#### 在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：
``` vue
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```
