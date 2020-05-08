---
title: 深入JavaScript(一)之原型与原型链
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-12-01 16:21:49
tags: JavaScript
keywords:
description:
photos:
---
## 一.构造函数
### 通过构造函数，我们可以生成实例化的对象，构造函数是一种特殊的函数：

``` JavaScript
function Student(name) {
    this.name = name;
    this.hello = function () {
      console.log('Hello, ' + this.name + '!');
    };
}

  let xiaoming = new Student('小明');          
  xiaoming.hello();                             //  Hello, 小明!
```
### <font color="red">注:Student就是一个构造函数，使用new关键字来调用构造函数生成实例对象，我们约定构造函数的函数名要大写，在构造函数的内部可以使用this关键字来添加属性。</font>

## 二.prototype
### 每个函数都有一个prototype属性，它其实是个对象，我们可以通过代码来看一下:

``` JavaScript
 function Student(name) {
    this.name = name;
    this.hello = function () {
      console.log('Hello, ' + this.name + '!');
    };
  }

  let xiaoming = new Student('小明');          //  Hello, 小明!
  xiaoming.hello();

  Student.prototype.task = function () {
    console.log('学生的任务就是学习');
  };

  console.log(Student.prototype);             // {task: f}

  let stu1 = new Student();
  let stu2 = new Student();

  console.log(stu1.hello === stu2.hello);    // false

  console.log(stu1.task === stu2.task);      // true
```
### <font color="red">注:prototype的作用是：抽离该构造函数所在类的共用属性和方法，使其所有的实例都共用同样的方法或者属性。</font>

## 三.__proto__
### 每个实例对象都有一个私有属性[[Prototype]]，也就是我们经常见到的__proto__,__proto__指向了实例对象的原型，它也是一个对象。

``` JavaScript
function Student(name) {
    this.name = name;
    this.hello = function () {
      console.log('Hello, ' + this.name + '!');
    };
  }

 Student.prototype.task = function () {
    console.log('学生的任务就是学习');
 };
 Student.prototype.hobby = 'enjoy';

  let xiaoming = new Student('小明');                              //  Hello, 小明!
  console.log(xiaoming.__proto__);                                //  {hobby: "enjoy",task: ƒ ()}
  console.log(xiaoming.__proto__ === Student.prototype);          //  true   
```

## 四.constructor
### 每个实例对象都有一个constructor属性，该属性指向与其相关联的构造函数：

``` JavaScript
 function Animal(name) {
     this.name = name;
     this.sound = function () {
        console.log(this.name + '叫了好几声');
     };
  }

  Animal.prototype.age = 2;

  let dog = new Animal('da_huang');
  console.log(dog.constructor);                 // f Animal(name){}
```  

