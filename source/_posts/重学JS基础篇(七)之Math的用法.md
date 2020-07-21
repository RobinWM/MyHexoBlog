---
title: 重学JS基础篇(七)之Math的用法
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2020-02-17 10:52:00
tags: JavaScript
keywords:
description:
photos:
---
# 一.abs取绝对值

1.用法Math.abs(value);
2.注意，参数不是数字类型时，先基于Number()转换为数字类型；

# 二.取整

1.ceil
  - 作用：把一个数向上取整；
  - 用法：Math.ceil(1.2);
  - 注意：无论是整数还是负数，都取最大的那个值；

2.floor
  - 作用：把一个数向下取整；
  - 用法：Math.floor(1.2);
  - 注意：无论是整数还是负数，都取最小的那个值；

3.round
  - 作用：四舍五入；
  - 用法：Math.round(1.5);
  - 注意：Math.round(-1.5)的值为-1,Math.round(-1.51)的值为-2；

4.max  
  - 作用：获取最大值；
  - 用法：Math.max(...arr);
  - 注意：<Font color="red">max的入参并不是一个数组，可以通过对数组解构传参；</Font>

5.min
  - 作用：获取最小值；
  - 用法：Math.min(...arr);
  - 注意：<Font color="red">max的入参并不是一个数组，可以通过对数组解构传参；</Font>  

6.sprt
  - 作用：获取一个数的开平方；
  - 用法：Math.sprt(value);

7.pow
  - 作用：获取n的m次幂；
  - 用法：Math.pow(n,m);

8.random
  - 作用：获取0到1之间的随机小数，精确到小数点后第17位；
  - 用法：Math.random(...arr);
  - 注意：<Font color="red">结果包含0但不包括1!!!</Font>； 
  - 拓展：获取n~m间的随机整数：Math.round(Math.random()*(m-n)+n);