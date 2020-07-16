---
title: 重学JS基础篇之(二)number类型
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-16 16:42:52
tags: JavaScript
keywords:
description:
photos:
---
# 一.范围

1.正数、负数、0；
2.NaN:not a number,不是一个有效的数字，但是属于number类型；
3.Infinity:无穷大的值，也是number类型；

# 二.isNaN

1.定义：用来验证一个值是否为非有效数字；
2.返回值：true或false;
3.如果检测的值为非数字类型，则会先转换为数字类型，然后再进行检测；
4.如果需要转换，会使用Number()内置方法；

# 三.其它类型转换为数字类型

1.Number()
 - JS内置转换方法，强制装换；
 - 字符串转数字：都是有效数字字符转为具体数字，否则返回0,特殊的空字符串返回数字0；
 - 布尔转数字：true返回1，false返回0；
 - null:返回0；
 - undefined：NaN;
 - Symbol:不可转，否则会报错；
 - 对象：先转为字符串"[object object]",再转换为数字，其中空数组返回0，其它基本都返回NaN;
 
2.parseInt()、parseFloat();

3.toFixed(N)
 - 保留小数点后N位；
 - <Font color="red">返回的结果是一个字符串</Font>
