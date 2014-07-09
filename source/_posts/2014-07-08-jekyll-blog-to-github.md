---
layout: post
title:  "用jekyll建造blog并放到github上"
date:   2014-07-08 10:51:29
comments: true
categories:
- jekyll
- ruby
- github
---
jekyll是一个轻量级的网站框架，经常被用于建设github上的blog，

## 1. 安装ruby
可以参考 [rvm.io][rvm]

## 2. 安装jekyll
```
gem install jekyll
```

备注： 国内可能需要更换gem源，否则可能会因为被墙而不能正常安装。[taobao源][taobao]

## 3. 创建、并运行blog
```
jekyll new blog
cd blog
jekyll serve
```
这时候你可以打开浏览器直接访问
http://127.0.0.1:4000
一个简单的blog就建成了

## 4. 添加文章
打开```_posts/```你会发现有一篇以:year-:month-:day-:title.markdown命名的文章，你可以以此格式复制成你想要的名称，打开修改即可。

文章默认使用markdown格式，你也可以使用textile，这个看个人喜好。

## 5. 部署到github
首先你需要在github创建一个你的名称.github.io的项目（如：我的用户名为destinyd，项目名则为 destinyd.github.io）

以我的blog提交作为范例
```
jekyll build
cd _site
git init
git add .
git commit -m 'first commit'
git remote add origin git@github.com:destinyd/destinyd.github.io.git
git push -u origin master
```
执行完就可以通过
http://destinyd.github.io
访问了

[rvm]: http://rvm.io
[taobao]: http://ruby.taobao.org
