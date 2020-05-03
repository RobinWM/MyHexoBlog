---
title: js中关于constructor与prototype的理解
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-20 17:55:01
tags: JavaScript
keywords:
description:
photos:
---
<font color="green">1</font>.①__proto__和constructor属性是对象所独有的；② prototype属性是函数所独有的，因为函数也是一种对象，所以函数也拥有__proto__和constructor属性。

<font color="green">2</font>.__proto__属性的作用就是当访问一个对象的属性时，如果该对象内部不存在这个属性，那么就会去它的__proto__属性所指向的那个对象（父对象）里找，一直找，直到__proto__属性的终点null，然后返回undefined，通过__proto__属性将对象连接起来的这条链路即我们所谓的原型链。

<font color="green">3</font>.prototype属性的作用就是让该函数所实例化的对象们都可以找到公用的属性和方法，即a1.__proto__ === A.prototype。

<font color="green">4</font>.constructor属性的含义就是指向该对象的构造函数，所有函数（此时看成对象了）最终的构造函数都指向Function()。

``` javascript
function A() {}
A.prototype.name = '1';
var a1 = new A();
var a2 = new A();
 
console.log(a1.name); // 1
console.log(a2.name); // 1
 
a1.__proto__.name = '2';
a1.name = 3;
// console.log(a1.__proto__);
 
console.log(a1.name);   // 3
console.log(a2.name);   // 2
 
delete a1.name;

a2.__proto__.name = '4';
console.log(a1.name);   // 4
console.log(A.prototype.constructor);  // A
```