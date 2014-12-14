---
layout: post
title: 用 Node.js 做电影网站（一）
category: blog
description: 看了阿里 Web 前端工程师 Scott 的 Node 教学视频后，也动手尝试做一个练习项目。
---

##前言
因为我们项目的后端打算用 Node.js 实现，所以最近了解了许多，也在这里写点东西作为总结。
在慕课网看到 Scott 大侠的视频：[ node + mongodb 100分钟建站攻略（一期）][1]，一边看一边动手做练习。

##开发环境与工具
首先，我的开发环境和工具：

操作系统:    `ubuntu` 14.04 LTS 32位    ( ubuntu 属于 Linux 的一个发行版本)

编辑器:          `Sublime Text 2`                 (前后端开发神器，此刻正在用它写本篇文章)

开发环境:    `node.js`    `mongoDB`    `npm`    `express`    `mongoose`    `jade`    `Moment.js`

前端框架:    `jQuery`    `Bootstrap`    (通过 `Bower` 来管理以上两个框架)

知识储备:    

 + Web 前端 ( `HTML`  +  `CSS`  +  `JavaScript`  +  `jQuery`  +  `Bootstrap` )
 + 简单了解 Node 的基本知识，安装、模块和包的概念、npm包管理工具的使用、express开发框架  、jade 对 Web前端 的模板化等
 + Linux 环境下命令行的简单使用

##目标效果
本次练习，使用这些工具实现了一个简单的电影网站的前后端交互，暂时还不涉及到 mongoDB 数据库，放上最终实现的效果：

###首页
![首页](http://changshiban.qiniudn.com/post/index.png)

###响应式布局的首页
![响应式布局的首页](http://changshiban.qiniudn.com/post/index_mobile.png)

###影片详情页
![影片详情页](http://changshiban.qiniudn.com/post/detail.png)

###后台录入页
![后台录入页](http://changshiban.qiniudn.com/post/admin.png)

后台管理页
![后台管理页](http://changshiban.qiniudn.com/post/list.png)

##开始
###创建项目 imovie
建立项目文件夹 `imovie`；

然后，在命令行输入下列命令来安装所需要的工具包：

    cd imovie
    npm install express
    npm install jade
    npm install bower

在 `imovie` 文件夹下：

创建视图文件夹 `views`

创建程序入口文件 `app.js`

创建静态资源文件夹 `bower_components`


通过下列命令自动下载前端框架：

    bower install jquery
    bower install bootstrap

下载到的前端文件会放置在 `bower_components` 文件夹下。

###用 jade 写模板
我也是第一次接触 jade ，不过很快发现它挺强大，可以实现模板继承。

于是我们的 views 模板分拆如下：

####公共部分
在 `views` 文件夹下创建 `layout.jade` , 作为”母模板“(个人的理解，即每个页面的公共骨架)。

打开并编辑它，大致样子如下：

    doctype
    html
        head
            meta(charset="utf-8")
            title #{title}
            include ./includes/head
        body
            include ./includes/header
            block content

怎么样，是不是非常简单？ jade 的语言跟 Python/Ruby 风格类似，一定要注意缩进。

通过 `include` 可以引入其他的子模板，实现模板的继承和重用。

`block content` 则可以在不同的页面展示本页面私有的部分。


在 `views` 文件夹下创建文件夹 `includes` 

在 `includes` 文件夹下创建 `head.jade`  和 `header.jade`

`head.jade` 就相当于 HTML 里的 head 标签，可以在这里引入前端文件：

    link(href="/bootstrap/dist/css/bootstrap.min.css", rel="stylesheet")
    script(src="/jquery/dist/jquery.min.js")
    script(src="/bootstrap/dist/js/bootstrap.min.js")

`header.jade` 则相当于 HTML5 里 body 部分里的 `header`，可以在这里写好每个页面都有的部分，使用一些 Bootstrap 里定义的 CSS 样式，比如：

    .container
        .row
            .page-header
                h1= title
                small 9分视频博物馆

####四个页面
在 `views` 文件夹下创建文件夹 `pages`

在 `pages` 文件夹下创建 4 个文件：

    index.jade
    detail.jade
    admin.jade
    list.jade

写页面模板的思路很简单，用 `extends` 引入公共骨架 layout.jade ，再写 `block content` 包含本页面的私有内容。

比如 `index.jade` 可以这么写：

    extends ../layout
    
    block content
        .container
            .row
                each item in movies
                    .col-md-2
                        .thumbnail
                            a(href="/movie/#{item._id}")
                                img(src="#{item.poster}", alt="#{item.title}")
                            .caption
                                h3 #{item.title}
                                p: a.btn.btn-primary(href="/movie/#{item._id}", role="button")
                                    观看

这样就实现了前面所展示首页的模板。

其他页面的模板类似，在这里不在赘述，后面会附上我写的源代码以供参考。

###写 Node 程序

到这里，我们就差一步就可以实现前后端的交互，让程序跑起来了。

####配置程序

打开文件 `app.js`

 + 引入 express , path , body-parser , 测试端口；
 + 设置 模板引擎 和 模板文件的路径；
 + 设置 静态文件的路径；
 + 监听端口。

这些都是 Node 开发 Web 应用的基本设置，照着做就可以：

    var express = require('express')
    var path = require('path')
    var bodyParser = require('body-parser');
    var port = process.env.PORT || 3000
    var app = express()
    
    app.set('views', './views/pages')
    app.set('view engine', 'jade')
    // parse application/x-www-form-urlencoded
    app.use(bodyParser.urlencoded({ extended: false }))
    // parse application/json
    app.use(bodyParser.json())
    app.use(express.static(path.join(__dirname,'bower_components')))
    app.listen(port)
    
    console.log('iMovie started on port ' + port)

####设置页面

在 `app.js` 里接着往下写，以 首页/index 为例：

    //index page
    
    app.get('/', function (req, res)  {
        res.render('index', {
            title:'iMovie 首页',
            movies: [{
                title:'',
                _id: ,
                poster:''
            }]
        })
    })

可以看出，get是一个监听事件，当监听到地址栏请求 `http://localhost:3000` + `/` 的时候，返回一个 对象/字典 给前端。

前端则把这些数据填充到模板 `index.jade` 里，最终展现到浏览器中。

其他 3 个页面类似，略过。

####填充数据

按照常理，程序应该从数据库中获得数据，来填充到各个页面模板中。

但是这次的练习，还没有用到数据库，所以暂时使用假数据(数据来自 `优酷` )，还是以 首页/index 为例：

    //index page
        app.get('/', function (req, res)  {
        res.render('index', {
            title:'iMovie 首页',
            movies: [{
                title:'奇妙世纪 08 梦的还原器',
                _id: 1,
                poster:'http://r3.ykimg.com/05410408548589706A0A4160AF2742DF'
            },{
                title:'奇妙世纪 08 梦的还原器',
                _id: 2,
                poster:'http://r3.ykimg.com/05410408548589706A0A4160AF2742DF'
            },{
                title:'奇妙世纪 08 梦的还原器',
                _id: 3,
                poster:'http://r3.ykimg.com/05410408548589706A0A4160AF2742DF'
            },{
                title:'奇妙世纪 08 梦的还原器',
                _id: 4,
                poster:'http://r3.ykimg.com/05410408548589706A0A4160AF2742DF'
            },{
                title:'奇妙世纪 08 梦的还原器',
                _id: 5,
                poster:'http://r3.ykimg.com/05410408548589706A0A4160AF2742DF'
            },{
                title:'奇妙世纪 08 梦的还原器',
                _id: 6,
                poster:'http://r3.ykimg.com/05410408548589706A0A4160AF2742DF'
            }]
        })
    })

### Run ！

好了，现在让程序跑起来！

在命令行输入：

    cd imovie
    node app

打开浏览器(推荐 `Chrome` 或者 `FireFox` 浏览器)，在地址栏输入

`http://localhost：3000`

如果显示没问题的话，成功。

##后续
第一次源码已上传到 `Github` ，[点击查看][2]

下次接着继续。

[1]:   http://www.imooc.com/learn/75  " Node 视频"
[2]:   https://github.com/HugoJing/imovie " Github 源码"