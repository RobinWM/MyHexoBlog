---
title: ES6中常用的小技巧，用了事半功倍哦
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-14 17:37:45
tags: ECMAScript
keywords: ECMAScript
description:
photos:
---
# ES6中常用的小技巧，如果能在实际项目中能使用到，必定事半功倍：

## 1. 强制要求参数

&emsp;&emsp;ES6提供了默认参数值机制，允许你为参数设置默认值，防止在函数被调用时没有传入这些参数。

&emsp;&emsp;在下面的例子中，我们写了一个required()函数作为参数a和b的默认值。这意味着如果a或b其中有一个参数没有在调用时传值，会默认required()函数，然后抛出错误。

``` JavaScript
const required = () => {throw new Error('Missing parameter')};
const add = (a = required(), b = required()) => a + b;
add(1, 2);                                       // 3
add(1);                                          // Error: Missing parameter.
```

## 2. 强大的reduce

&emsp;&emsp;数组的reduce方法用途很广。它一般被用来把数组中每一项规约到单个值。但是你可以利用它做更多的事。

#### 2.1 使用reduce同时实现map和filter

&emsp;&emsp;假设现在有一个数列，你希望更新它的每一项（map的功能）然后筛选出一部分（filter的功能）。如果是先使用map然后filter的话，你需要遍历这个数组两次。

&emsp;&emsp;在下面的代码中，我们将数列中的值翻倍，然后挑选出那些大于50的数。有注意到我们是如何非常高效地使用reduce来同时完成map和filter方法的吗？
``` JavaScript
const numbers = [10, 20, 30, 40];
const doubledOver50 = numbers.reduce((finalList, num) => {
  num = num * 2; 
  if (num > 50) {
    finalList.push(num);
  } 
  return finalList;
}, []);
doubledOver50; // [60, 80]
```

#### 2.2 使用reduce取代map和filter

&emsp;&emsp;如果你认真阅读了上面的代码，你应该能理解reduce是可以取代map和filter的。

#### 2.3 使用reduce匹配圆括号
&emsp;&emsp;reduce的另外一个用途是能够匹配给定字符串中的圆括号。对于一个含有圆括号的字符串，我们需要知道(和)的数量是否一致，并且(是否出现在)之前。

&emsp;&emsp;下面的代码中我们使用reduce可以轻松地解决这个问题。我们只需要先声明一个counter变量，初值为0。在遇到(时counter加一，遇到)时counter减一。如果左右括号数目匹配，那最终结果为0。

``` JavaScript
//Returns 0 if balanced.
const isParensBalanced = (str) => {
  return str.split('').reduce((counter, char) => {
    if(counter < 0) { //matched ")" before "("
      return counter;
    } else if(char === '(') {
      return ++counter;
    } else if(char === ')') { 
      return --counter;
    }  else { //matched some other char
      return counter;
    }
  }, 0); //<-- starting value of the counter}
isParensBalanced('(())') // 0 <-- balanced
isParensBalanced('(asdfds)') //0 <-- balanced
isParensBalanced('(()') // 1 <-- not balanced
isParensBalanced(')(') // -1 <-- not balanced
```

#### 2.4 统计数组中相同项的个数
&emsp;&emsp;很多时候，你希望统计数组中重复出现项的个数然后用一个对象表示。那么你可以使用reduce方法处理这个数组。

&emsp;&emsp;下面的代码将统计每一种车的数目然后把总数用一个对象表示。

``` JavaScript
var cars = ['BMW','Benz', 'Benz', 'Tesla', 'BMW', 'Toyota'];
var carsObj = cars.reduce(function (obj, name) { 
   obj[name] = obj[name] ? ++obj[name] : 1;
  return obj;
}, {});
carsObj; // => { BMW: 2, Benz: 2, Tesla: 1, Toyota: 1 }
```

## 3. 对象解构
#### 3.1 删除不需要的属性
&emsp;&emsp;有时候你不希望保留某些对象属性，也许是因为它们包含敏感信息或仅仅是太大了（just too big）。你可能会枚举整个对象然后删除它们，但实际上只需要简单的将这些无用属性赋值给变量，然后把想要保留的有用部分作为剩余参数就可以了。

&emsp;&emsp;下面的代码里，我们希望删除_internal和tooBig参数。我们可以把它们赋值给internal和tooBig变量，然后在cleanObject中存储剩下的属性以备后用。

``` JavaScript
let {_internal, tooBig, ...cleanObject} = {el1: '1', _internal:"secret", tooBig:{}, el2: '2', el3: '3'};
console.log(cleanObject); // {el1: '1', el2: '2', el3: '3'}
```

#### 3.2 在函数参数中解构嵌套对象

&emsp;&emsp;在下面的代码中，engine是对象car中嵌套的一个对象。如果我们对engine的vin属性感兴趣，使用解构赋值可以很轻松地得到它。

``` JavaScript
var car = {
  model: 'bmw 2018',
  engine: {
    v6: true,
    turbo: true,
    vin: 12345
  }
}
const modelAndVIN = ({model, engine: {vin}}) => {
  console.log(`model: ${model} vin: ${vin}`);
}
modelAndVIN(car); // => model: bmw 2018  vin: 12345
```

#### 3.3 合并对象

&emsp;&emsp;ES6带来了扩展运算符（...）。它一般被用来解构数组，但你也可以用它处理对象。

&emsp;&emsp;接下来，我们使用扩展运算符来展开一个新的对象，第二个对象中的属性值会改写第一个对象的属性值。比如object2的b和c就会改写object1的同名属性。

``` JavaScript
let object1 = { a:1, b:2,c:3 }
let object2 = { b:30, c:40, d:50}
let merged = {…object1, …object2} //spread and re-add into merged
console.log(merged) // {a:1, b:30, c:40, d:50}
```

## 4. Sets
#### 4.1 使用Set实现数组去重

&emsp;&emsp;在ES6中，因为Set只存储唯一值，所以你可以使用Set删除重复项。

``` JavaScript
let arr = [1, 1, 2, 2, 3, 3];
let deduped = [...new Set(arr)] // [1, 2, 3]
```

#### 4.2 对Set使用数组方法

&emsp;&emsp;使用扩展运算符就可以简单的将Set转换为数组。所以你可以对Set使用Array的所有原生方法。

&emsp;&emsp;比如我们想要对下面的Set进行filter操作，获取大于3的项。

``` JavaScript
let mySet = new Set([1,2, 3, 4, 5]);
var filtered = [...mySet].filter((x) => x > 3) // [4, 5]
```

## 5. 数组解构
&emsp;&emsp;有时候你会将函数返回的多个值放在一个数组里。我们可以使用数组解构来获取其中每一个值。

#### 5.1 数值交换
``` JavaScript
let param1 = 1;
let param2 = 2;
//swap and assign param1 & param2 each others values
[param1, param2] = [param2, param1];
console.log(param1) // 2
console.log(param2) // 1
```

#### 5.2 接收函数返回的多个结果
&emsp;&emsp;在下面的代码中，我们从/post中获取一个帖子，然后在/comments中获取相关评论。由于我们使用的是async/await，函数把返回值放在一个数组中。而我们使用数组解构后就可以把返回值直接赋给相应的变量。

``` JavaScript
async function getFullPost(){
  return await Promise.all([
     fetch('/post'),
     fetch('/comments')
  ]);
}
const [post, comments] = getFullPost();
```

