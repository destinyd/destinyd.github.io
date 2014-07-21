---
layout: post
title: "gradle 如何引用 maven 库的项目"
date: 2014-07-22 15:40:29 +0000
comments: true
categories: 
- gradle
- maven
- android
---
## 问题
由于项目模块独立化，部分同事使用的是android studio，即使用gradle管理android项目。

然后组件大多是maven项目，存于maven本地库。

一般引用为：
```
dependencies {
    compile project(':menudrawer')
    compile 'com.actionbarsherlock:actionbarsherlock:4.4.0@aar'
    compile 'com.android.support:support-v4:19.0.1'
    compile 'com.github.destinyd.kcextraimageview:kcextraimageview:0.1.0'
}
```
前一项为工程内项目，2、3项为经maven中心库项目，第4项为未提交到maven中心库的本地库项目。

测试[**第4项**][fourth]出错，不管是否已经使用**mvn clean install**安装到本地库。

## 解决
万能的google查询了下解决方法，发现：
```
repositories {
    mavenCentral()
}
```
改为
```
repositories {
    mavenLocal()
    mavenCentral()
}
```
即可。

## 结论
gradle项目默认配置文件是不使用maven本地库，如果需要需进行设置。

## 组件介绍
[**Extra Image View**][fourth]是一个集合拖动、双手操作的高级图片组件，有兴趣的可以尝试使用，欢迎各位提供各种意见和建议。


[fourth]: https://github.com/destinyd/kcextraimageview
