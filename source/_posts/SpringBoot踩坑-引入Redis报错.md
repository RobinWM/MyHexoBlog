---
title: SpringBoot踩坑-引入Redis报错
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-10-29 00:39:55
tags: Boot
keywords: springboot
description:
photos:
---
# 引用org.springframework.data报错
## 今天在运行同事springboot项目时遇到一个很奇怪的错误：
## 问题：Error:(6, 49) java: 程序包org.springframework.data.redis.connection不存在
## 解决步骤：
#### 在pom.xml引入如下代码：
{% codeblock lang:xml %}
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-redis</artifactId>
</dependency>
{% endcodeblock %}
