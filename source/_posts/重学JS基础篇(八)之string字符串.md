---
title: 重学JS基础篇(八)之string字符串
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-17 11:37:14
tags: JavaScript
keywords:
description:
photos:
---

# 一.字符串截取

1.substring
  - 作用：返回一个字符串在开始索引到结束索引之间的一个子集, 或从开始索引直到字符串的末尾的一个子集；
  - 语法：str.substring(indexStart,indexEnd)；
  - 注意：indexEnd是可选参数；

2.slice
  - 作用：提取某个字符串的一部分，并返回一个新的字符串，且不会改动原字符串；
  - 语法：str.substring(beginIndex,endIndex)；
  - 注意：endIndex是可选参数

# 二.字符查找

1.charAt
  - 作用：获取字符串中指定索引对应的字符；
  - 语法：str.charAt(index)；
  - 注意：indexEnd是可选参数；

# 三.是否包含某项

1.indexOf
  - 作用：获取字符在字符串中首次出现位置的索引；
  - 语法：str.indexOf(searchValue,fromIndex)；
  - 注意：fromIndex是可选参数；

2.includes
  - 作用：判断一个字符串是否包含在另一个字符串中，根据情况返回true或false。；
  - 语法：str.includes(searchString,position)；
  - 注意：position是可选参数；

# 四.字符串转数组  

1.split
  - 作用：使用指定的分隔符字符串将一个String对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置；
  - 语法：str.split(separator,limit)；
  - 注意：limit是可选参数,用来限制字符串数组的长度；

# 五.字符串替换
1.replace
  - 作用：返回一个由替换值(replacement)替换一些或所有匹配的模式(pattern)后的新字符串；
  - 语法：str.replace(regexp|substr, newSubStr|function)：
    - regexp(pattern)：一个RegExp对象或者其字面量。该正则所匹配的内容会被第二个参数的返回值替换掉；
    - substr(pattern)：一个将被newSubStr替换的字符串。其被视为一整个字符串，而不是一个正则表达式。仅第一个匹配项会被替换；
    - newSubStr(replacement):用于替换掉第一个参数在原字符串中的匹配部分的字符串。该字符串中可以内插一些特殊的变量名;
    - function (replacement):一个用来创建新子字符串的函数，该函数的返回值将替换掉第一个参数匹配到的结果;
