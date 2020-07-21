---
title: 重学JS基础篇(六)之函数基础
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-17 10:21:25
tags: JavaScript
keywords:
description:
photos:
---

# 一.什么是函数

## 函数是一种处理问题的方法，其意义在于封装，以减少冗余代码；

# 二.函数的创建

1.function funName(形参){...};
2.过程：
  - 创建值：
    - 开辟一个堆内存；
    - 把函数体中的代码当做字符串储存在堆中；
    - 把堆地址放到栈中；

  - 创建变量；
  - 把变量和地址关联起来；

# 三.函数的执行

1.语法：funName(实参)；
2.依赖条件：栈内存和供代码执行的上下文环境；
3.函数每一次执行的过程：
  - 创建一个全新的执行上下文环境，把执行上下文压塑到栈内存中去执行(进栈执行)；
  - 在这个上下文中，存在一个AO(变量对象)，用来存储当前上下文代码执行中所创建的变量；
  - 代码执行；
  - 当上下文中的代码都执行完成后，如果该上下文中的信息没有被外界占用，则执行出栈操作；
4.形参和实参：
  - 形参是用来暂时存储执行函数时传递进来的值，所以形参是变量；
  - 调用函数时，传递的具体值是实参，所以实参就是具体传递的值；  