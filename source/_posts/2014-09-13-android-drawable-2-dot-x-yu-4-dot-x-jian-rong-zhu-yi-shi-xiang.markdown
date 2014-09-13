---
layout: post
title: "Android drawable 2.x 与 4.x 兼容注意事项"
date: 2014-09-13 08:44:07 +0000
comments: true
categories: 
- Android
---
最近开发Android应用的时候发现一个兼容性问题：

**自定义的drawable在4.x以及L版本下正常，2.x上没有效果**

搜索了好久没找到问题的解决办法。

重新回到drawable xml的研究。

原来的xml内容：
```
<?xml version="1.0" encoding="utf-8"?>

<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@color/ddd" />
    <item android:left="1dp" android:drawable="@color/white" />
</layer-list>
```

我尝试换其他的形式去改写这个分割线背景：
```
<?xml version="1.0" encoding="utf-8"?>

<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item>
        <shape android:shape="rectangle">
            <solid android:color="@color/ddd"/>
        </shape>
    </item>
    <item android:left="1dp">
        <shape android:shape="rectangle">
            <solid android:color="@color/white"/>
        </shape>
    </item>
</layer-list>
```

这样他居然就显示正常了- -b。

我想这可能是因为Android早期对于drawable解析处理的方式还不完善导致。

希望这篇文章能帮助和我遇到同样问题的人。
