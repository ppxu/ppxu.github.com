---
layout: post
title: "Windows下让Jekyll支持Pygments语法高亮"
description: "support pygments in jekyll on windows"
category: website
tags: [jekyll, pygments, python, windows]
---
{% include JB/setup %}

[Jekyll](http://jekyllrb.com/) 内置了对 [Pygments](http://pygments.org/) 的支持，今天研究了下怎么使用这个东西，这里总结一下方法，我是在 Windows 环境下操作的。

1. Pygments 是 [Python](http://www.python.org/) 下的一个工具，所以首先要安装 Python，在[这里](http://www.python.org/download/)可以下载 Windows 下的 Python 安装包，我下的版本是 Python 2.7.3，然后直接双击安装即可。安装完成后把 Python 的安装路径，默认是 `C:\Python27`，添加到环境变量 Path 中，在命令行中运行

		python -V
	如果看到输出 `Python 2.7.3`，则表明安装成功。

2. 然后使用 [easy_install](http://packages.python.org/distribute/easy_install.html) 来安装 Pygments，[easy_install](http://peak.telecommunity.com/DevCenter/EasyInstall) 是 Python 里的一个模块安装工具，类似 nodejs 的 npm 和 ruby 的 gem，先在[这里](http://pypi.python.org/pypi/setuptools)下载 setuptools，找到 Python 2.7 版本的 Windows 安装包，运行安装，并把路径 `C:\Python27\Scripts` 添加到环境变量 Path。

3. 在命令行中运行

		easy_install Pygments
	待执行完毕就装好了 Pygments。

4. 然后我们要在 Jekyll 的配置文件 _config.yml 中设置打开 Pygments

		pygments: true

5. 在 [Pygments demo](http://pygments.org/demo/) 上根据不同语言找到自己喜欢的高亮方案，比如 friendly，然后进到我们的网站目录，运行

		pygmentize -S friendly -f html > css/pygments/friendly.css
	并把生成的样式文件加到我们的网页中。
	如果提示找不到指定路径，先建好对应的文件夹就可以了。

6. 需要语法高亮的代码片段要放在标签对 `{% highlight javascript %}` 和 `{% endhighlight %}` 之间。

7. 运行

		jekyll --server

如果一切顺利，就能看到如下效果了。

{% highlight javascript %}
KISSY.add('ppxu', funciton(S){
	var name = 'ppxu';
	var ppxu = {
		init: function(){
			console.log(name);
		}
	};
	return ppxu;
});
{% endhighlight %}

有不满意的话还可以自己修改那个样式文件。

另外，我在第6步时碰到了一个问题，运行报错
	Liquid Exception: No such file or directory ...
在网上查了下是 pygments.rb 的问题，用 gem 安装最新版的 [pygments.rb](http://rubygems.org/gems/pygments.rb) 就没问题了。

-------------------
####参考资料

* [http://joshua-leung.me/Software%20Tricks/2012/05/04/installing-pygments/](http://joshua-leung.me/Software%20Tricks/2012/05/04/installing-pygments/)
* [http://skim.la/2010/02/14/how-to-run-jekyll-pygmentize-on-windows/](http://skim.la/2010/02/14/how-to-run-jekyll-pygmentize-on-windows/)
* [http://chxt6896.github.com/blog/2011/12/01/blog-pygments.html](http://chxt6896.github.com/blog/2011/12/01/blog-pygments.html)
* [http://chxt6896.github.com/python/2011/12/03/python-setuptools-easyinstall.html](http://chxt6896.github.com/python/2011/12/03/python-setuptools-easyinstall.html)
* [https://github.com/mojombo/jekyll/issues/716](https://github.com/mojombo/jekyll/issues/716)
* [http://zyzhang.github.com/blog/2012/08/31/highlight-with-Jekyll-and-Pygments/](http://zyzhang.github.com/blog/2012/08/31/highlight-with-Jekyll-and-Pygments/)