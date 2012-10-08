---
layout: post
title: "本地Jekyll禁止访问问题"
description: "local jekyll server no access permission forbidden"
category: website
tags: [jekyll, encode]
---
{% include JB/setup %}

在上篇 [本地搭建Jekyll博客环境](http://ppxu.net/blog/2012/09/27/setup-local-jekyll-environment/)中，讲了如何在本地搭建 [Jekyll](http://jekyllrb.com/) 服务器，虽然看似繁琐，其实操作都很方便，但在这过程中我也碰到了一个问题，求解了好久，在这里贴一下。

在搭建的第6步，运行 `jekyll --server` 后， 打开 [http://localhost:4000/](http://localhost:4000/)，出现的是一个错误页面

	Forbidden no access permission to /'
	WEBrick/1.3.1 (Ruby/1.9.3/2012-04-20) at localhost:4000

在 [Google](http://www.google.com) 上搜了一下，产生错误的原因大概是 Jekyll 没有成功创建 \_site/index.html 文件，实际上 \_site 目录整个都是空的，而在本地调试的时候 Jekyll 是需要访问 \_site 目录的，由于目录为空，而且服务器又没有权限来直接访问文件夹目录，所以就会返回上述错误。

Jekyll 有一种调试方法是运行 `jekyll --no-auto`，可以看到详细的启动过程，有助于分析。

找啊找，首先看到一个方案是 [YAML](http://www.yaml.org/) 格式的问题，

	YAML格式默认是：参数＋：＋空格，如果忘记写空格描绘编译报错。

但是我看了 \_posts 目录下的文件，所有 YAML 格式都是正确的，所以排除这个问题。

继续找啊找，找到另一个方案是修改 Jekyll 读取文件时的默认编码，在 Jekyll 安装目录（Ruby安装目录\lib\ruby\gems\1.9.1\gems\jekyll-0.11.2\lib\jekyll）下找到 convertible.rb 文件，在27行左右，原始代码如下：

		self.content = File.read(File.join(base, name))

修改为：

		self.content = File.read(File.join(base, name), :encoding => "utf-8")

这样改了之后，再访问 [http://localhost:4000/](http://localhost:4000/)，OK，成功了，生活如此美好，话说静态页面速度就是快啊哈哈～

-------------------
####参考资料

* [https://groups.google.com/forum/?fromgroups=#!topic/jekyll-rb/86PEfzf1FS0](https://groups.google.com/forum/?fromgroups=#!topic/jekyll-rb/86PEfzf1FS0)
* [https://github.com/mojombo/jekyll/issues/626](https://github.com/mojombo/jekyll/issues/626)
* [http://pradeepnayak.in/technology/2012/02/16/jekyll-character-encoding-problems/](http://pradeepnayak.in/technology/2012/02/16/jekyll-character-encoding-problems/)
* [http://www.yangzhiping.com/tech/wordpress-to-jekyll.html](http://www.yangzhiping.com/tech/wordpress-to-jekyll.html)
* [http://www.cnblogs.com/heart-runner/archive/2012/02/14/2351136.html](http://www.cnblogs.com/heart-runner/archive/2012/02/14/2351136.html)
* [http://www.mcgtts.com/blog/2012/05/30/jekyll-encode/](http://www.mcgtts.com/blog/2012/05/30/jekyll-encode/)
* [http://www.madhur.co.in/blog/2011/09/01/runningjekyllwindows.html](http://www.madhur.co.in/blog/2011/09/01/runningjekyllwindows.html)