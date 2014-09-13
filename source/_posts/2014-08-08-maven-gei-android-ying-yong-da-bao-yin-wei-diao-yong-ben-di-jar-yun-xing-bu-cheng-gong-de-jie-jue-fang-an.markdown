---
layout: post
title: "maven 给 Android 应用打包，因为调用本地 jar，运行不成功的解决方案"
date: 2014-08-08 19:44:15 +0000
comments: true
categories: 
- maven
- android
---

做过实际应用发布的人都知道，会应用到很多类似与umeng、友推等第三方库，一般都是jar格式的。

本人做开发，觉得maven用的很爽，所以就一直再没建过adt形式的应用工程。

但是现在发布的时候遇到了问题，apk使用IDE运行的时候正常，但是用maven打包的apk，不能正常运行，提示：
```
java.lang.NoClassDefFoundError: cn.bidaround.youtui_template.YtTemplate
```
看提示肯定是打包时候友推的template这个jar没有引入

maven依赖代码如下：
```
<dependency>
  <groupId>youtui</groupId>
  <artifactId>template</artifactId>
  <version>1.0</version>
  <scope>system</scope>
  <systemPath>${project.basedir}/libs/youtui-template.jar</systemPath>
</dependency>
```

直接用这个错误搜索不到结果，看来用了友推的不是maven工程？（瞬间觉得高大上）还是友推还小众？（难道我选择有误？）

搜索了一下有关system scope的依赖，发现了解决方法

### 首先，我们需要把jar安装至本地maven库
```
mvn install:install-file -Dfile=app/libs/youtui-template.jar -DgroupId=youtui -DartifactId=template -Dversion=1.0 -Dpackaging=jar
```

### 然后，我们得把scope改成compile，并去除systemPath
修改结果如下
```
<dependency>
    <groupId>youtui</groupId>
    <artifactId>template</artifactId>
    <scope>compile</scope>
    <version>1.0</version>
</dependency>
```

### 最后重新打包测试
模拟器运行后，错误没有再次出现！


### 后话
很多人现在都开始使用Android Studio、Intellij Idea等开发工具，而不是单纯的使用ADT。

Maven、Gradle等东西不断的被引入，Gradle不是不喜欢，而是2.0至今在各IDE都未能很好的整合，让我很是不爽，而且Gradle也依赖于Maven，所以使用Maven是我的选择。

如果有哪位喜欢Maven的，请留言，看情况和是，我不断的放出Maven的教程，帮助各位更好、更快的学习。

顺便发个新应用的网站链接《[笑料百出][jokewebsite]》，希望大家多多支持！


[jokewebsite]: http://joke.realityandapp.com
