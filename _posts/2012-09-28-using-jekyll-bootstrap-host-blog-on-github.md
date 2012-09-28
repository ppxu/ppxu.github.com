---
layout: post
title: "使用Jekyll-Bootstrap在Github上搭建博客"
description: "using jekyll-bootstrap host blog on github"
category: "website"
tags: [jekyll, github]
---
{% include JB/setup %}

其实使用 [Jekyll-Bootstrap](http://jekyllbootstrap.com/) 在 [Github](https://github.com/)上搭建博客真的非常容易，在 Jekyll-Bootstrap 官网上号称3分钟就可以创建一个博客，至于你信不信，我反正信了。

下面简单讲一下过程，前提是你要有 Github 账号，这个就不用多说了吧，那就开始吧。

1. 在 Github 上创建一个 repository，名字叫 `username.github.com`，记得把 `username` 换成自己的用户名，后文都如此。

2. 到一个你准备放网站文件的目录，比如 D:\work\，执行以下命令
		git clone https://github.com/plusjade/jekyll-bootstrap.git username.github.com
		cd username.github.com
		git remote set-url origin git@github.com:username/username.github.com.git
		git push origin master

OK，操作部分就完成了，你的网站本地路径为 D:\work\username.github.com，等 Github 部署完成后你就可以在 [http://username.github.com](http://username.github.com]/) 访问你的网站了。

进入本地目录 D:\work\username.github.com，看一下这里的结构，\_includes 里有 Jekyll-Bootstrap 相关的功能和 themes 主题，\_layouts 就是网页的模板文件，不过运行时会被主题中的同名文件覆盖，\_plugins 顾名思义是插件，\_posts 就是我们放文章的地方了，文件名要改成 `2012-09-28-using-jekyll-bootstrap-host-blog-on-github.mk` 这种 `年-月-日-文章标题.后缀名` 格式，\_site 是本地运行时调用的文件夹，关于如何在本地运行，请参考 [本地搭建Jekyll博客环境](http://ppxu.net/blog/2012/09/28/setup-local-jekyll-environment/)，\_assets里是一些样式文件。

\_config.yml 是网站的配置文件，可以根据自己情况自行调整，具体设置看 [这里](http://jekyllbootstrap.com/usage/blog-configuration.html)。

archive.html，categories.html，index.md，pages.html，tags.html 分别是存档页，类别页，主页，页面页，标签页。

当你在 \_posts 里新加了一篇文章，只需执行如下代码
	git add .
	git commit -m "Add new content"
	git push origin master
即可更新到线上，即时生效，速度灰常快哦～

再讲一下如何使用自己的域名，首先你要在网站目录下新建一个 CNAME 文件，里面只有一行，就是你的域名，比如：
	ppxu.net
然后到你的域名服务商那里，将域名解析改成：
	ppxu.net
	@                        A              204.232.175.78
	www					     CNAME			username.github.com
	username.github.com      A              204.232.175.78
这是我失败了很多次后终于找到的正确方法。

基本上这样你的网站就创建完成了，你可以继续研究 [这个](http://jekyllbootstrap.com/usage/index.html) 或者 [这个](http://jekyllbootstrap.com/developers/index.html) 来更好的控制你的网站。

-------------------
####参考资料

* [http://www.yangzhiping.com/tech/wordpress-to-jekyll.html](http://www.yangzhiping.com/tech/wordpress-to-jekyll.html)
* [http://feelapi.com/archives/324](http://feelapi.com/archives/324)
* [http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
* [http://kingauthur.info/2012/05/19/hello-jekyll/](http://kingauthur.info/2012/05/19/hello-jekyll/)
* [http://www.pizn.me/2011/12/02/hello-pizn-me.html](http://www.pizn.me/2011/12/02/hello-pizn-me.html)
* [http://saberma.me/other/2010/09/20/saberma-github-page-blog-build-with-jekyll.html](http://saberma.me/other/2010/09/20/saberma-github-page-blog-build-with-jekyll.html)
* [http://ravenw.com/blog/2011/08/27/blog-with-jekyll/](http://ravenw.com/blog/2011/08/27/blog-with-jekyll/)
* [http://blog.leezhong.com/tech/2010/08/25/make-github-as-blog-engine.html](http://blog.leezhong.com/tech/2010/08/25/make-github-as-blog-engine.html)
* [http://yuliu.org/2012/06/git_and_github/](http://yuliu.org/2012/06/git_and_github/)
* [http://kingauthur.info/2012/05/19/hello-jekyll/](http://kingauthur.info/2012/05/19/hello-jekyll/)
* [https://help.github.com/articles/setting-up-a-custom-domain-with-pages](https://help.github.com/articles/setting-up-a-custom-domain-with-pages)
* [http://jekyllbootstrap.com/usage/jekyll-quick-start.html](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)