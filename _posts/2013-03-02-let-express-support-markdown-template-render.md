---
layout: post
title: "让Express支持markdown渲染模板"
description: "let express support markdown template render"
category: website
tags: [nodejs, express, markdown, template, jade]
---
{% include JB/setup %}

在之前的文章 [使用node.js和Express搭建网站](http://ppxu.net/blog/2012/10/09/create-website-with-node-and-express/) 中，已经讲过了如何搭建一个基于 [Express](http://expressjs.com/) 的网站，而 [markdown](http://zh.wikipedia.org/wiki/Markdown) 是非常方便好用的标记语言，下面记录一下如何在 Express 中使用 markdown 的方法。

我们需要的工具就是 [markdown-js](https://github.com/evilstreak/markdown-js)。

1. 首先当然需要已经创建完成的 Express 网站目录，打开根目录下的 `package.json` 文件，在 `dependencies` 中添加一个包依赖

		"markdown-js": "*"

2. 打开一个命令行窗口，运行

		npm install
就会把这样 markdown-js 下载到网站目录下 node_modules 文件夹中。

3. 在根目录下创建 blog 文件夹，存放 markdown 文件，然后在 views 中创建一个 post.jade 模板文件，用于渲染我们的文章。

4. 然后我们要在启动脚本 `app.js` 中添加以下代码

		//导入模块
		var markdown = require('markdown-js');

		//使用方法
		//路由选择
		app.get('/blog/:title', function(req, res, next) {
			//获取标题
		    var title = req.params.title;
		    //拼凑路径
		    var urlPath = [
		        __dirname, '/blog/',
		        title, '.md'
		    ].join('');
			//标准路径
		    var filePath = path.normalize('./' + urlPath);
			//存在路径
		    fs.exists(filePath, function(exists){
		      if(exists){
		        //读取文件
		        var content = fs.readFileSync(filePath, 'utf-8');
		        //转换markdown
		        var html_content = markdown.parse(content);
		        //渲染模板
		        res.render('post', {
		            title: title,
		            blog_content: html_content,
		            pretty: true
		        });
		      }
		      else{
		        //跳去404
		        next();
		      }
		    });
		});

5. 运行
		node app
在浏览器中访问地址
		127.0.0.1:3000/markdown
即可看到最终效果了。