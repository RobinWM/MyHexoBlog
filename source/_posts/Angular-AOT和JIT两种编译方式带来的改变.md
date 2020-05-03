---
title: Angular--AOT和JIT两种编译方式带来的改变
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-05 18:12:19
tags: angular
keywords:
description:
photos:
---
&emsp;&emsp;Angular应用主要由组件及其HTML模板组成。由于浏览器无法直接理解Angular所提供的组件和模板，因此Angular应用程序需要先进行编译才能在浏览器中运行。Angular提供了两种方式来编译angular应用程序：
<font color="red">
1.即时编译 (JIT,Just in time)，它会在运行期间在浏览器中编译你的应用。
2.预先编译（AOT,Ahead of time)，它会在构建时编译你的应用。
</font>

 注：1.当你运行ng build（仅编译）或ng serve（编译并启动本地服务器）这两个CLI命令时JIT编译是默认选项；要进行AOT编译，只要让ng build或ng serve命令中包含--aot标志;2.带有--prod标志的ng build命令(ng build --prod)会默认使用AOT编译。

&emsp;&emsp;AOT:在浏览器下载和运行代码之前的编译阶段，Angular预先（AOT）编译器会先把你的Angular HTML和TypeScript代码转换成高效的JavaScript代码。好处如下：

1.<font color="red">渲染得更快：</font>使用AOT浏览器下载预编译版本的应用程序。 浏览器直接加载运行代码，所以它可以立即渲染该应用，而不用等应用完成首次编译；
2.<font color="red">需要的异步请求更少：</font>编译器把外部HTML模板和CSS样式表内联到了该应用的JavaScript中。消除了用来下载那些源文件的Ajax请求；
3.<font color="red">需要下载的Angular框架体积更小：</font>如果应用已经编译过了，自然不需要再下载Angular编译器了。该编译器差不多占了Angular自身体积的一半儿，所以，省略它可以显著减小应用的体积；
4.<font color="red">提早检测模板错误：</font>AOT编译器在构建过程中检测和报告模板绑定错误，避免用户遇到这些错误；
5.<font color="red">更安全：</font>AOT方式会在发给客户端之前就把HTML模板和组件编译成JavaScript文件。不需要读取模板，也没有客户端组装HTML或执行JavaScript的危险操作，受到注入类攻击的机会也比较少。