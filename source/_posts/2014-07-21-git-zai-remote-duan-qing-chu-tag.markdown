---
layout: post
title: "git在remote端清除tag"
date: 2014-07-21 10:53:31 +0000
comments: true
categories: 
- git
---
最新在弄maven的archetypes遇到点问题，使用其插件部署时会生产tag并且自动提交版本库。

但是我忘记使用gpg签名，而我不想手工下载从新签名。

我把之前的提交全部revert了，但是部署的时候提示remote端tag已经存在。

搜索了一下怎么解决这个问题，才发现其实也挺简单的：
```
git tag -d 12345
git push origin :refs/tags/12345
```
也就2句命令而已。

然后我再次revert了已经push的commit，重新部署，一切问题解决。

看来玩好git也是门艺术。
