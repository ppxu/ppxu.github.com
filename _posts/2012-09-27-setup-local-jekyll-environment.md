---
layout: post
title: "本地搭建Jekyll博客环境"
description: "setup local jekyll environment"
category: website
tags: [jekyll, ruby, gem]
---
{% include JB/setup %}

今天在本地搭建了 [Jekyll](http://jekyllrb.com/)  环境，可以方便在发布上线前进行预览，这里把主要过程记录一下。

1. Jekyll 是 [Ruby](http://www.ruby-lang.org/) 的应用，以前木有接触过 Ruby，还好这里也不需要专业的 Ruby 知识，只要安装一下 Ruby 环境就行。Window 系统可以到 [这里](http://rubyinstaller.org/downloads/) 下载 Ruby 安装程序，最新版本是 Ruby 1.9.3-p194，顺便把下面的 DEVELOPMENT KIT 也一起下了。

2. 运行刚才下载的 rubyinstaller-1.9.3-p194.exe，可以自己选择一个目录，记得选上 `Add Ruby executables to your PATH`，安装完成后可以运行

		ruby -v
	如果显示类似

		ruby 1.9.3p194(2012-04-20)[i386-mingw32]
	就表明 Ruby 环境已经完成。

3. 然后要安装 [RubyGem](http://rubygems.org/)，这个类似于 [node.js](http://nodejs.org/) 的 [npm](https://npmjs.org/)，在 [这里](http://rubygems.org/pages/download) 下载 ZIP 格式的文件，解压到一个目录，在该目录下打开一个 cmd，运行

		ruby setup.rb
	即可。同样我们可以运行

		gem -v
	检查，如果显示

		1.8.24
	就表明 gem 已安装成功。

4. 需要用 Ruby 开发接下来就要安装 Development Kit 开发者工具，运行刚才下载的 DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe，解压到一个目录，然后在该目录下打开一个 cmd，接下来

	* `ruby dk.rb init`，运行完这步会在次目录下产生一个 `config.yml` 文件，用记事本打开这个文件，里面应该有第2步安装的 Ruby 程序路径。
	* `ruby dk.rb review`，运行这个也是为了检查是否包含了 Ruby 安装路径。
	* `ruby dk.rb install`，这样 Ruby 开发者工具就算是装好了。

5. 终于，我们可以安装 Jekyll 了，在 cmd 中运行

		gem install jekyll
	如果有问题请检查上面步骤，或者参考 [这里](https://github.com/mojombo/jekyll/wiki/Install)。

6. 进入之前建立的 Jekyll-Bootstrap 网站文件夹，类似：`ppxu.github.com`，在该目录下打开 cmd 窗口，运行

		jekyll --server
	如果一切顺利，你就可以在 [http://localhost:4000/](http://localhost:4000/) 看到你的网站了。这儿其实还遇到了一个问题，我会在下篇说明。

7. 要新建一篇文章，只需要在 cmd 中运行

		rake post title="Hello World"
	然后你就可以在 _posts 目录下面看到一个新文件 `2012-09-28-Hello-World`，打开这个文件，可以看到它已经填好了 [YAML](http://www.yaml.org/) 头，Jekyll 用的是 [Liquid](https://github.com/Shopify/liquid) 模板引擎，可以在 [这里](https://github.com/mojombo/jekyll/wiki/liquid-extensions) 看到相关语法。

8. 要新建一个页面，只需在 cmd 中运行

		rake page name="about.md"
	或者

		rake page name="pages/about.md"

9. 在本地写好后，就可以发布上线了，很简单

		git add .
		git commit -m "Add new content"
		git push origin master

10. 好了，Jekyll的全部流程就是这样啦，如果不需要本地环境的话其实只需要最后一步，但是体验一下整个过程还是很有意思的~ :)

-------------------
#### 参考资料

* [RubyInstaller](http://rubyinstaller.org/)
* [RubyGems](http://rubygems.org/)
* [Development Kit](https://github.com/oneclick/rubyinstaller/wiki/development-kit)
* [Jekyll Docs](https://github.com/mojombo/jekyll/wiki)
* [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)