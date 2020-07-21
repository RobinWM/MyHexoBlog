---
title: 重学JS基础篇(五)之Object对象
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-17 09:30:29
tags: JavaScript
keywords:
description:
photos:
---
# 一.定义

1.JavaScript的对象是一种无序的集合数据类型，它由若干键值对组成，其中的键必须是字符串类型；
2.JavaScript用一个{}表示一个对象，键值对以xxx: xxx形式申明，用,隔开；

# 二.操作

1.通过.来获取属性，但这要求属性名必须是一个有效的变量名。如果属性名包含特殊字符，就必须用''括起来；

2.通过delete来删除属性：
``` JavaScript
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
```

3.判断一个属性是否存在：
  - in操作符：包含该对象继承的属性；
  - hasOwnProperty：不包含继承的属性，只包含自身属性；

4.特别注意：对象的属性名(键)必须是唯一的，不允许重复；  

# 三.常用的方法

1.Object.keys():返回当前对象的所有属性名的数组，数组中属性名的排列顺序和使用for...in循环遍历该对象时返回的顺序一致 ；
2.Object.values()：返回一个给定对象自身的所有可枚举属性值的数组，值的顺序与使用for...in循环的顺序相同(区别在于 for-in循环枚举原型链中的属性);
3.Object.toString():返回该对象的字符串；
4.Object.valueOf():返回指定对象的原始值；
5.Object.assign()：用于将所有可枚举属性的值从一个或多个源对象复制到目标对象，结果返回目标对象；
6.Object.create()：创建一个新对象，使用现有的对象来提供新创建的对象的__proto__。即创建一个以指定的对象为原型的子对象；
7.Object.defineProperty()：直接在一个对象上定义新的属性或修改现有属性，并返回该对象；
8.Object.entries()：返回一个给定对象自身可枚举属性的键值对数组，其排列与使用for...in循环遍历该对象时返回的顺序一致（区别在于 for-in 循环还会枚举原型链中的属性）；
9.Object.fromEntries()：把键值对列表转换为一个对象，是Object.entries()的逆操作；


# 四.补充知识点：条件判断里值是否相等(==)的转换规则

1.对象和字符串进行比较时，会把对象转换为字符串，然后再进行比较；
2.null和undefined不等于任何一个数据类型；
3.NaN和其他值永不相等；
4.除了以上几种类型，其它的类型在做比较时，都会把不属于数字类型的值转换为数字类型，然后再进行比较；


