---
layout: posts 				# 可选，默认post， scaffoldsmu目录下为可选layout
title: Hello-world to Hexo  		# 文章标题
date: 2017-06-01 18:29:00  	# 写作时间
description: This is the abc-guide for Hexo, which will tell you how to first post, new a page, start server, generate files, deploy the blog.	# 文章描述
excerpt: This is the abc-guide for Hexo, which will tell you how to first post, new a page, start server, generate files, deploy the blog  # 文章摘要
categories: 				# 文章分类
- abc-guide
tags: 						# 文章标签
- blog
- web
- Hexo
photos:						# 图片链接
comments:
original:
permalink: 					# 指定链接
---
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)


### Hexo theme framework

```
.
├── languages            #多语言
|   ├── default.yml      #默认语言
|   └── zh-CN.yml        #中文语言
├── layout               #布局，根目录下的*.ejs文件是对主页，分页，存档等的控制
|   ├── _partial         #局部的布局，此目录下的*.ejs是对头尾等局部的控制
|   └── _widget          #小挂件的布局，页面下方小挂件的控制
├── source               #源码
|   ├── css              #css源码 
|   |   ├── _base        #*.styl基础css
|   |   ├── _partial     #*.styl局部css
|   |   ├── fonts        #字体
|   |   ├── images       #图片
|   |   └── style.styl   #*.styl引入需要的css源码
|   ├── fancybox         #fancybox效果源码
|   └── js               #javascript源代码
├── _config.yml          #主题配置文件
└── README.md            #用GitHub的都知道
```