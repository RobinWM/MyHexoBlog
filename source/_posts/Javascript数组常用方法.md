---
title: Javascript数组常用方法
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 一个好奇的人
authorDesc: 一个好奇的人
categories: 技术
comments: true
date: 2019-08-18 11:25:55
tags: Script
keywords:
description:
photos:
---
## 常用的有以下方法：
1.push():向数组末尾添加一个或多个元素 
2.unshift(): 向数组的开头添加一个或多个元素 
3.pop(): 删除数组最后一个元素 
4.shift(): 删除数组第一个元素 
5.sort(): 给数组排序 
6.reverse(): 颠倒数组项在数组中的位置 
7.concat(): 合并数组 
8.slice(): 指定的位置开始删除指定的数组项，并且将删除的数组项构建成一个新数组 
9.splice(): 对一个数组做删除、插入和替换 
10.indexOf(): 从前向后查找元素在数组中位置 
11.lastIndexOf(): 从后向前查找元素在数组中位置 
12.forEach()、every()、some()、filter()和map()：数组迭代 
13.reduce(): 数组中的每个值（从左到右）开始合并，最终为一个值 
14.reduceRight(): 数组中的每个值（从右到左）开始合并，最终为一个值 
#### 注：1.sort方法用法注意

``` JavaScript
[10111, 1101, 111].sort()
// [10111, 1101, 111]
 
[10111, 1101, 111].sort(function (a, b) {
  return a - b;
})
// [111, 1101, 10111]
 
[
  { name: "张三", age: 30 },
  { name: "李四", age: 24 },
  { name: "王五", age: 28  }
].sort(function (o1, o2) {
  return o1.age - o2.age;
})
// [
//   { name: "李四", age: 24 },
//   { name: "王五", age: 28  },
//   { name: "张三", age: 30 }
// ]
```

#### 2.some方法是只要一个成员的返回值是true，则整个some方法的返回值就是true，否则返回false。

``` JavaScript
var arr = [1, 2, 3, 4, 5];
arr.some(function (elem, index, arr) {
  return elem >= 3;
});
// true
```

#### 3.every方法是所有成员的返回值都是true，整个every方法才返回true，否则返回false。

``` JavaScript
var arr = [1, 2, 3, 4, 5];
arr.every(function (elem, index, arr) {
  return elem >= 3;
});
// false
```


