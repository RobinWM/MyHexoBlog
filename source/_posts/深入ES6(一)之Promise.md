---
title: 深入ES6(一)之Promise
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-01-01 21:27:09
tags: ECMAScript
keywords:
description:
photos:
---
# 一.Promise的简单使用
## 1.什么是Promise
### 简单来说，Promise是异步编程的一种解决方案。

## 2.使用场景
### 一般情况下是有异步操作时，使用Promise对这个异步操作进行封装。

``` JavaScript
new Promise((resolve,reject) => {
        setTimeout(() => {
            resolve();    // 成功的时候调用
            reject();     // 失败的时候调用
        }, 1000);
    }).then(res => {
        // 成功时回调
        console.log(res);
    }).catch(error =>{
        // 失败时回调
        console.log(error);
    });
```

对以上代码进行解读：
1.new操作符调用Promise类的构造函数,并保存3中状态；
2.该构造函数传入两个参数：resolve和reject;
3.这两个参数也分别是一个函数；

# 二.Promise进阶理解
## 1.Promise的三种状态
- 首先，当我们开发中有异步操作时，就可以给异步操作包装一个Promise;
- 异步操作之后有三种状态：
  - <font color="red">padding:</font>等待状态,比如正在进行网络请求时，或者定时器没有到时间;
  - <font color="red">fulfill:</font>满足状态,当我们主动回调resolve时，就处于该状态，并且会回调.then();
  - <font color="red">padding:</font>拒绝状态,当我们主动回调了reject时，就处于该状态，并且会回调.catch();
  
### 2.Promise的链式调用
#### 先看如下代码：

``` JavaScript
new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('000');
        }, 1000);
    }).then(res => {
        console.log(res, '处理异步操作的结果');

        return new Promise((resolve, reject) => {
            resolve(res + '111');
        });
    }).then(res => {
        console.log(res, '处理上一步操作的结果');

        return new Promise((resolve, reject) => {
            resolve(res + '222');
        });
    }).then(res => {
        console.log(res, '处理上一步操作的结果');
    })
```   

#### 简写方式：

```
// 简写方式
    new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('000');
        }, 1000);
    }).then(res => {
        console.log(res, '处理异步操作的结果');

        return Promise.resolve(res + '111');
    }).then(res => {
        console.log(res, '处理上一步操作的结果');

        return Promise.resolve(res + '222');
    }).then(res => {
        console.log(res, '处理上一步操作的结果');
    })
```

#### 进一步简写：

``` JavaScript
new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('000');
        }, 1000);
    }).then(res => {
        console.log(res, '处理异步操作的结果');
        return res + '111';
    }).then(res => {
        console.log(res, '处理上一步操作的结果');
        return res + '222';
    }).then(res => {
        console.log(res, '处理上一步操作的结果');
    })
```

# 三.Promise的all用法

``` JavaScript
// 使用setTimeout()模拟异步操作
    Promise.all([
        new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve('result1');
            }, 10000);
        }),
        new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve('result2');
            }, 20000);
        })
    ]).then(results => {
        console.log(results);
    })
    


