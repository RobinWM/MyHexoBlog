---
title: 重学JS基础篇(三)之string和boolean类型
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-16 17:30:58
tags: JavaScript
keywords:
description:
photos:
---
# 一.其它数据类型转字符串

1.String(value)、(value).toString();
2.隐式转换：字符串拼接：加号两边任意一边出现字符串，则变为字符串拼接；
3.普通对象转字符串："[object object]";
4.ES增加的模板字符串： ``` `姓名：${name}` ```;

# 二.其它类型转为boolen类型

1.方法：Boolean(value)、!value;
2.规则：
  - fasle:0、''、NaN、null、undefined;
  - true:除了以上5个，其余都是true。注意: <Font color="red">字符串0的布尔值为true!!!</Font>

