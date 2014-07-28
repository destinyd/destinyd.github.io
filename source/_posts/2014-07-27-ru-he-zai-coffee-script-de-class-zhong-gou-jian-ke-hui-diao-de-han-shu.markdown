---
layout: post
title: "如何在coffeescript的class中构建可回调的函数"
date: 2014-07-27 09:24:36 +0000
comments: true
categories: 
- coffeescript
- javascript
---
coffeescript想必大家都知道在很多时候并不是想象中的那么好用，例如：
```
class A
  constructor: (options) ->
    @tmp = 1
    $('.string').click @func
  func: ->
    console.log @tmp # undefined
```
### 看提示或者自己测试你会发现alert的结果是**undefined**，为什么会这样呢？
因为@其实代替的是**this.**。
了解jquery的应该知道而，在func中的this其实是**$('#a')**。

大家可以在func中添加
```
console.log @
console.log this
```
查看this是到底是什么。（@和this其实是相同的）

### 那么我们怎么才能在func中调用到class A中的其他变量或者函数呢？
coffeescript提供了**=>**即闭包符号，我们试试看改成=>看看会是什么效果
```
class A
  constructor: (options) ->
    @tmp = 1
    $('.string').click @func
  func: =>
    console.log @tmp # 1
```
这是大家想要的结果了。

### 那么嵌套呢？
```
class A
  constructor: (options) ->
    @tmp1 = 1
    @tmp2 = 1
    $('.string').click @build
  build: =>
    console.log @tmp1 # 1
    $('.string').click @func
  func: =>
    console.log @tmp2 # 2
```
实测也是可行的

### 还有没有更复杂的情况？
的确是有的，不可能任何时候你都使用**=>**，但是此时我们又想他能调用class内的函数怎么办？
```
class B
  constructor:
    @tmp = 1
    $('#modal').on 'shown.bs.modal', (e) => @build(e)
  build: ->
    console.log @tmp # 1
```
通过**(e) => @build(e)**即可达到在**build函数**闭包的效果。
