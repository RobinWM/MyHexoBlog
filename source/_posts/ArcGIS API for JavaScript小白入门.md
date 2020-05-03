---
title: ArcGIS API for JavaScript小白入门
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-11 21:16:17
tags: JavaScript
keywords:
description:
photos:
---
#### 简单理解就是：通过js调用arcgis相关的方法和通过html引入css等资源来展示地图，代码如下：
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport">
  <title>Intro to MapView - Create a 2D map - 4.8</title>
  <style>     //设置显示区域的样式，地图全页面展示
    html,
    body,
    #viewDiv {
      padding: 0;
      margin: 0;
      height: 100%;
      width: 100%;
    }
  </style>
  //     第一步：引入js文件和css样式表，本文使用了4.9版本
  <link rel="stylesheet" href="https://js.arcgis.com/4.9/esri/css/main.css">
  <script src="https://js.arcgis.com/4.9/"></script>
  //开始使用编辑js，实现加载地图效果
  <script>
  // 第二步，导入需要的模块，这里引入了Map和MapView
    require([
      "esri/Map",
      "esri/views/MapView"
    ], function(Map, MapView) {
  // 第三步，初始化一个地图对象
      var map = new Map({
        // 设置基地图类型，可根据需要加载自己的地图服务。
        basemap: "streets"
      });
       // 新建视图，用的是MapView，是2D的，3D的要用SceneView模块，SceneView方法创建。
      var view = new MapView({
       //显示在HTML上的区域，也就是哪个div里
        container: "viewDiv",
         //将地图服务加载到视图上，这是4.x版本设定，3.x版本可直接创建map时设定
        map: map,
       //设置加载地图的缩放等级和中心位置。
        zoom: 4,
        center: [15, 65] // longitude, latitude
      });
    });
  </script>
</head>
<body>
  <div id="viewDiv"></div>
</body>
</html>
```