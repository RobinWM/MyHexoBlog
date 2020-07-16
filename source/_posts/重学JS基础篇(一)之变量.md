---
title: 重学JS基础篇(一)之变量
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-16 15:44:17
tags: JavaScript
keywords:
description:
photos:
---

# 一.js组成的三个部分

1.ECMAScript:定义JS的语法规范：变量，数据值，操作语句，内存管理；
2.DOM：Document Object Model，文档对象模型，提供对应的属性和方法，用来让JS可以操作DOM元素；
3.BOM：Browser Object Modal，浏览器对象模型，提供操作浏览器的属性和方法；

# 二.js中创建变量的方式

  - var(ES3)、let(ES6):申明变量;
  - const(ES6)：声明常量;
  - function(ES3): 声明函数；
  - class(ES6):申明类；
  - import/require:基于ES6Module或者Common.js规范导入模块；

# 三.命名规范

1.驼峰命名法：

  - 单词有实际的意义；

  - 第一个单词首字母小写，其余单词首字母大写；

  - 项目中常见的有特殊意义的词组：
    - add/insert/craete：新增/插入/创建；
    - delete/remove/drop：删除/移除；
    - update：修改、更新；
    - select/query/get：选择/查询/获取;
    - info/detail：信息/详情；

2.命名规则：使用$、_、英文字母、数字命名：
  - $开头：一般代表使用JQ或者其他使用$的类库获取的内容；
  - _开头：一般代表全局或者公共的变量；
  - 数字可以用来区分名称相似的变量，但不能作为开头；
  - 可以用_来分割单词或者直接使用驼峰；
  - 不能使用JavaScript中的关键字和保留字；

# 四.JS中的数据类型

1.基本数据类型：
  - number:数字类型；
  - string:字符串；
  - boolean:布尔；
  - null:空指针；
  - undefined:未定义；
  - Symbol:ES6新增的唯一值类型；

2.引用数据类型：
  - 对象数据类型object:
    - 普通对象：obiect；
    - 数组对象：Array;
    - 正则对象：RegExp;
    - 日期对象：Date;
    - 数学函数对象：Math;
    - 基本包装类型：Boolean、Numbe、String；

  - 函数数数据类型function;    






