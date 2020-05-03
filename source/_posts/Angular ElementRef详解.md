---
title: ElementRef详解
author: Robin
avatar: "https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg"
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-03 17:23:29
tags: angular
keywords:
description:
photos:
---
## 一.为什么要用 ElementRef

&emsp;&emsp;Angular 的口号是"一套框架，多种平台。同时适用手机与桌面(One framework.Mobile & desktop.)"，即Angular是支持开发跨平台的应用，比如Web应用、移动Web应用、原生移动应用和原生桌面应用等。

&emsp;&emsp;为了能够支持跨平台、Angular通过抽象层封装了不同平台的差异，统一了API接口。如定义了抽象类Renderer（已废弃，现在用 Renderer2） 、抽象类RootRenderer等。此外还定义了以下引用类型：

1. ElementRef;
2. TemplateRef;
3. ViewRef;
4. ComponentRef;
5. ViewContainerRef

## 二.ElementRef有什么作用

&emsp;&emsp;在应用层直接操作DOM，就会造成应用层与渲染层之间强耦合，导致我们的应用无法运行在不同环境，如web worker中，因为在 web worker 环境中，是不能直接操作DOM。有兴趣的读者，可以阅读一下Web Workers中支持的类和方法这篇文章。通过ElementRef我们就可以封装不同平台下视图层中的
native元素 (在浏览器环境中,native 元素通常是指 DOM 元素)，最后借助于Angular提供的强大的依赖注入特性，我们就可以轻松地访问到 native 元素。

## 三.如何使用ElementRef

&emsp;&emsp;先看需求：我们要实现一个组件成功加载另一个组件（本文中是遮罩的组件）并渲染完成后，改变遮罩文字层div的样式，接下来请看我是如何实现的；

&emsp;&emsp;1.引入相关 api
``` TypeScript
import {Component, OnInit, Input, Output, EventEmitter,AfterViewInit, ElementRef, ViewChild, Renderer2} from '@angular/core';
```

&emsp;&emsp;2.构造函数依赖注入
``` TypeScript
constructor( private elementRef: ElementRef,
             private renderer: Renderer2) {
}
```

&emsp;&emsp;3.使用属性装饰符@ViewChild
``` TypeScript
<div class="contents" [innerHTML]="content | translate" #divContent>
</div>
```

&emsp;&emsp;4.设置相关样式
``` TypeScript
ngAfterViewInit() {
   this.renderer.setStyle(this.greetDiv.nativeElement, 'width', '3.60rem');
}
```
