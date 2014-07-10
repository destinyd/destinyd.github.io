---
layout: post
title: "用octopress搭建blog"
date: 2014-07-09 20:00:16 +0000
comments: true
categories: 
- octopress
- ruby
- github
- heroku
---
octopress是基于jekyll，添加了rake操作的网站框架，使用它可以比jekyll更加容易搭建网站。

## 1. 安装ruby
可以参考 [rvm.io][rvm]

## 2. 安装octopress
```
git clone https://github.com/imathis/octopress
cd octopress
bundle install
```

## 3. 创建微博文章、页面
你可以通过以下指令创建微博文章
```
rake new_post
```
执行后会提示你输入文章标题，可以为中文。

之后会在**source/_posts**下生成文章文件，改写成你想要的内容，格式为markdown。


你可以通过以下指令创建页面
```
rake new_page[page_file_name]
```
执行后会在source下生成**source/page_file_name/index.markdown**，修改成你想要的页面。

## 4. 本地预览
本地预览其实很简单，执行
```
rake preview
```
会监听4000端口，你可以通过
http://localhost:4000
访问，预览网站。

## 5. 部署
### 5.1 部署到github
部署到github相对简单的多
```
rake setup_github_pages[repo]
```
将repo改成你的repo地址就ok了，如我的是https://github.com/destinyd/destinyd.github.io

然后执行
```
rake generate
rake deploy
```
则会生成最新文章并部署到github，然后可以通过用户名.github.io访问，例如我的为
http://destinyd.github.io

### 5.2 部署到heroku
安装heroku工具的步骤就省略了

首先需要创建一个heroku app
```
heroku create
```

然后生成最新的网站内容，并上传到heroku
```
rake generate
git push heroku master
```

最后打开访问
```
heroku open
```

部署一个blog也不难嘛，对吧！


## 其他
### 更改octopress配置
在**_config.yml**文件中可以看到octopress的各种配置，例如blog名称、下标题、网址、作者名称等，可以更改为你自己的然后从新**rake generate**生成新网站。

### 更换博客主题
[octopress第三方主题][octopress-themes]
这上面提供很多用户自制的主题，可以很简单的直接拿来使用，只需要执行：
```
git clone GIT_URL .themes/THEME_NAME
rake install['THEME_NAME']
rake generate
```

### 按抓给你第三方插件
[octopress第三方插件][octopress-plugins]
这上面有很多插件可供下载，不过具体操作不一样，所以只提供链接。

### Github Page绑定自己域名
在项目根目录下建立一文件，名为CNAME，里面写上域名，如destinyd.me 或者在命令行里执行：
```
echo 'destinyd.me' >> source/CNAME
```

去自己的域名运营商处修改:
CNAME: destinyd.me => destinyd.github.com

[rvm]: http://rvm.io
[octopress-themes]: https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes
[octopress-plugins]: https://github.com/imathis/octopress/wiki/3rd-party-plugins
