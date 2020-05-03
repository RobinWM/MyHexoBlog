---
title: maps插件打包android报错冲突问题
author: Robin
avatar: 'https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg'
authorLink: codersart.cn
authorAbout: 前端开发攻城狮
authorDesc: 追求完美
categories: 技术
comments: true
date: 2019-08-22 22:16:25
tags: ionic
keywords:
description:
photos:
---
&emsp;&emsp;这段时间在调FCM推送服务的插件 ，原本以为去年调通过，应该很容易，没想到还是出问题了。现将问题及解决方法整理如下，仅供参考：
&emsp;&emsp;详细报错信息：
Please fix the version conflict either by updating the version of the google-services plugin (information about the latest version is available at https://bintray.com/android/android-tools/com.google.gms.google-services/) or updating the version of com.google.android.gms to 10.+.
&emsp;&emsp;大概的意思就是说：我使用的google-services插件与google gms服务的版本冲突，需要升级以解决冲突；
&emsp;&emsp;出现这个问题的原因在于：我的项目中使用cordova-plugin-geolocation(定位)和cordova-plugin-googlemaps(地图)，这两个插件使用了google-services服务，而ionic官方推荐添加的ionic cordova plugin add            cordova-plugin-fcm-with-dependecy-updated与fcm相关的插件使用了google的gms服务，这两个服务在一起的时候，必须保证服务相关的包的兼容性；
## 解决方案：
#### 1.在android/app/build.gradle中修改dependencies下
``` grade
implementation 'com.google.firebase:firebase-core:16.0.8'
implementation 'com.google.firebase:firebase-messaging:17.5.0'
```

#### 2.在android/cordova-plugin-fcm-with-dependecy-updated/Alpha-FCMPlugin.gradle中修改dependencies下
``` grade
compile 'com.google.firebase:firebase-core:16.0.8'
```

#### 3.sync成功之后，build，问题解决。