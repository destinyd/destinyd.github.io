---
layout: post
title: "git怎么取消已经push了的commit"
date: 2014-07-10 19:10:51 +0000
comments: true
categories: 
- git
---
使用版本管理工具管理项目，可能经常会遇到这些情况：
* 发现某个commit包含了bug，但是已经push到版本库了，想在版本库取消掉它，修改之后重新commit
* 已经上线了的功能想取消掉，这个commit包含了多个commit，均已push到版本库

其实想要恢复还是挺简单的，git提供了一个revert指令，专门用于处理这样的事情。


## 取消掉某个commit
我们只需要执行：
```
git revert commit_id
```

## 取消掉多个commit
我们需要倒序的执行：
```
git revert commit_id1[ commit_id2 ...]
```

操作起来相对麻烦，类似于```git reset HEAD~1 --soft```的HEAD~N是否有效本人也没有去证明，如果有需要你们可以自己尝试。

**注意：**
**commit_id 可以通过git log查看。**

## 注意
* 如果之后有基于此commit做了修改的话，你还需要解决冲突。
* 此commit不可以再通过merge方式合并，你只能修改后重新
