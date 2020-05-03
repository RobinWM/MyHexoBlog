---
title: Angular中innerHTML标签的样式失效详解
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-08 20:31:59
tags: angular
keywords:
description:
photos:
---
## 1.背景
&emsp;&emsp;在最近angular的项目中,需要用到[innerHTML]标签来指定一个div的样式： 

``` H5
1 //HTML部分
2 <div class="contents" [innerHTML]="contents"></div>
3 
4 //TS部分
5 contents = '<p>商品信息栏位<br><span style="color:red;">商品信息介绍</span></p>';
```

&emsp;&emsp;但是上面的样式并不起作用，在Chorme中查看源码，发现style标签的样式在Angular编译的时候被屏蔽掉。这是为什么呢？客观别急，请往下看。

## 2.解决方案
&emsp;&emsp;先说解决方案，最后再分析出现这种问题的原因。修改上面的TS：

``` TypeScript
// 在使用的页面引入DomSanitizer
    import { DomSanitizer } from '@angular/platform-browser';
 
// 构造方法里注入sanitizer对象
    constructor( private sanitizer: DomSanitizer
    ) { }
 
// 对HTML代码做处理
    this.contents= this.sanitizer.bypassSecurityTrustHtml("<p>W3商品信息栏位<br><span style="color:red;">商品信息介绍</span></p>");
```

&emsp;&emsp;这样虽然可以解决问题，但是这样做还不够：
 - <font color='red'>代码冗余繁杂:</font>如果我们的contents内容过大，这样我们的代码就显得很乱，影响可读性和美观；
 - <font color='red'>不能复用:</font>如果其他ts中也要用到innerHTML标签，又要重新写一遍上面的TS内容，没有复用性；

&emsp;&emsp;基于以上两点，我们用**自定义管道**（pipe）来优化以上代码，使用```ng generate pipe safe-html```命令来生成一个pipe，并做适当的修改： 
``` TypeScript
//  对生成的safe-html.pipe.ts做适当修改<br><br>import {Pipe, PipeTransform} from '@angular/core';
import {DomSanitizer} from '@angular/platform-browser';
@Pipe({name: 'safeHtml'})
export class SafeHtmlPipe implements PipeTransform {
    constructor(private sanitized: DomSanitizer) {
    }
    transform(value) {
        return this.sanitized.bypassSecurityTrustHtml(value);
    }
}<br><br>// 在使用innerHTML标签的属性里使用以上safeHtml管道
// 使用管道
<div class="contents" [innerHTML]="contents|safeHtml"></div>
```

## 3.原因及原理分析
&emsp;&emsp;所以，为什么会出现上面的问题呢？原来，Angular中默认将所有输入值视为不受信任。当我们通过 property，attribute，样式，类绑定或插值等方式，将一个值从模板中插入到DOM中时，Angular会自帮我们清除和转义不受信任的值。在开头的例子中，span标签里的样式被屏蔽了，不信请看：
![avatar](https://cdn.jsdelivr.net/gh/RobinWM/cdn@2.1/img/articles/innerHTML.png)

&emsp;&emsp;Angular在编译的时候，会自动清理HTML输入并转义不安全的代码，因此在这种情况下，style被屏蔽，样式失效。这时候如果需要将样式片段渲染出来，就需要用到DomSanitizer了。<font color='red'>DomSanitizer可以把值净化为在不同DOM上下文中的安全内容，来帮我们防范跨站脚本攻击（XSS）类的安全问题</font>。

[参考链接]('https://angular.cn/api/platform-browser/DomSanitizer#description'):https://angular.cn/api/platform-browser/DomSanitizer#description