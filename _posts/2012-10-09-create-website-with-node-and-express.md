---
layout: post
title: "使用node.js和express搭建网站"
description: "create website with node and express"
category: website
tags: [nodejs, express, jade, stylus, appfog]
---
{% include JB/setup %}

关于 [node.js](http://nodejs.org/) 和 [express](http://expressjs.com/) 本身就不多作介绍了，主要记录下操作过程。

1. 首先当然是要安装 __node.js__ 和 __npm__，这个就不用多说了吧，如果有不会的，请参考 [深入浅出Node.js（二）：Node.js&NPM的安装与配置](http://www.infoq.com/cn/articles/nodejs-npm-install-config)。

2. 然后要安装 __express__ 了，请执行以下命令
		npm install -g express
执行完毕后运行
		express -V
检查下，如果显示类似 `3.0.0rc4`，则安装成功。

3. 这里我们要用 [jade](http://jade-lang.com/) 和 [stylus](http://learnboost.github.com/stylus/) 作为 html 模板和 css，__express__ 默认使用的就是 __jade__，来到工作目录，比如 `D:\work`，执行
		express -c stylus ppxu
执行完毕后会有提示，我们按照提示执行
		cd ppxu
		npm install
这样会把需要的 __npm__ 模块包含到网站目录中。
此时，我们的整个目录结构为：
		D:\work\ppxu
			|---node_modules			//包含模块
			|	|---.bin
			|   |---express
			|   |---jade
			|   |---stylus
			|---public					//assets文件
			|   |---images
			|   |---javascripts
			|   |---stylesheets
			|---routes					//路由脚本
			|   |---index.js
			|   |---user.js
			|---views					//视图模板
			|   |---index.jade
			|   |---layout.jade
			|---app.js 					//入口文件
			|---package.json			//npm 依赖配置文件

4. 运行
		node app
启动服务器，打开地址 [http://localhost:3000/](http://localhost:3000/)。

OK，基于 __node.js__ 和 __express__ 的网站就搭好啦！

如果你要对网站做更多的设置，请参考 [express guide](http://expressjs.com/guide.html) 和 [Express.js 中文入门指引手册](http://www.csser.com/board/4f77e6f996ca600f78000936)。

对 __jade__ 需要更多的了解请参考 [jade documentation](https://github.com/visionmedia/jade#readme) 和 [Jade模板引擎入门教程](http://www.csser.com/board/4f3f516e38a5ebc978000508)。

我们在启动服务器后，如果修改了网站内容，那么就需要先 `ctrl+c` 停止服务器，再重新启动，才能看到改动，如果对这一点也感到很不爽的话，那么你需要这个 —— [nodemon](https://github.com/remy/nodemon)。
		npm install -g nodemon
		nodemon app.js
以这种方式启动服务器，改动文件后，无需停止再重启，只要刷新页面，即可生效。

最后讲如何部署网站，这里要推荐一个非常棒的应用 —— [appfog](http://www.appfog.com/)。

2G空间永久免费哦～

注册之后，你会看到 appfog 提供了非常多的应用环境

![appfog](assets/img/af.jpg)

这里我选择了 Node Express，选 Node 应该也可以。

下面应该是选择托管商吧，我选了 AWS Asia Southeast，看起来是最近的。

然后输入一个应用名，点击 `Create App`，稍等片刻，应用环境就搭好了。

然后会直接进入控制面板，能看到资源使用情况，点击 `Visit Live Site`，就可以看到你的网站了。当然，这时候只有一句话而已
		Hello from AppFog.com
接下来我们需要把我们前面创建好的网站传上去。

这里需要用到 [Ruby](http://www.ruby-lang.org/) 和 [gem](http://rubygems.org/)，关于如何安装 __Ruby__ 环境，可以参考之前的文章 [本地搭建Jekyll博客环境](http://ppxu.net/blog/2012/09/27/setup-local-jekyll-environment/) 的前面部分。

准备工作都完成后，打开 `开始菜单 - 所有程序 - Ruby - Start Command Prompt with Ruby`，执行
		gem install af
安装 appfog 控制工具，然后运行
		af login
输入注册邮箱和密码登录。最后切换到网站目录（`D:\work\ppxu`），运行
		af update appname
这里 appname 是你在添加应用的填的名字，稍等片刻，网站就上传完成了。

此时再到 appfog 控制面板，点击 `Visit Live Site`，是不是之前本地搭好的那个网站？

appfog 还提供了非常多的功能，有兴趣的可以多研究研究。

-------------------
####参考资料

* [http://shapeshed.com/creating-a-basic-site-with-node-and-express/](http://shapeshed.com/creating-a-basic-site-with-node-and-express/)
* [http://lazynight.me/1969.html](http://lazynight.me/1969.html)