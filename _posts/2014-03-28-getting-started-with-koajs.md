---
layout: post
title: "（译）Koajs 快速上手"
description: "getting started with koajs"
category: nodejs
tags: [nodejs, express, koa, koajs, guide]
---
{% include JB/setup %}

杰出的 [express](http://expressjs.com/) 框架的开发团队（包括 [TJ](http://tjholowaychuk.com/) 大神）给我们带来了node.js下一代 web 框架 [koa](http://koajs.com/)。

让我们用一个简单的 hello-world 应用来演示一下：

#### 首先是 Express 的版本


{% highlight javascript %}
var express = require('express');

var app = express();

app.use(function(req, res, next){
	res.send('Hello World');
});

app.listen(3000);
{% endhighlight %}

#### 然后我们来看看 Koa 的方式


{% highlight javascript %}
var koa = require('koa');
var app = koa();

app.use(function *(){
	this.body = 'Hello World';
});

app.listen(3000);
{% endhighlight %}

上述两种方法都会开启一个监听3000端口的 HTTP 服务器，并在首页渲染出 `Hello World`。

可能有人不知道 `function *()` 是什么，这是 ES6 中的新特性：[harmony:generators](http://wiki.ecmascript.org/doku.php?id=harmony:generators)，我们可以通过 `node --harmony` 的方式开启 [ES6 on node](http://h3manth.com/new/blog/2013/es6-on-nodejs/)。

#### 让我们仔细比较一下


{% highlight javascript %}
// Express
app.use(function(req, res, next){
	res.send('Hello World');
});

//Koa
app.use(function *(){
	this.body = 'Hello World';
});
{% endhighlight %}

看到这段代码首先你可能会疑惑，参数 `req` 和 `res` 去哪了！

答案就是上下文 —— `context`，在 Koa 的 Context 对象中已经包括了 node 的请求和响应对象。

> A Koa application is an object containing an array of middleware generator functions which are composed and executed in a stack-like manner upon request

因此，对每一个请求，Koa 会创建一个新的 context 对象


{% highlight javascript %}
app.use(function *(){
	this; // is the Context
	this.request; // is a koa Request.
	this.response; // is a koa Response.
	this.req; // nodejs request.
	this.res; // nodejs response.
});

// keys of this:
[ 'request',
  'response',
  'app',
  'req',
  'res',
  'onerror',
  'originalUrl',
  'cookies',
  'accept' ]
  {% endhighlight %}

现在我们用路由的形式重写 Koa 的 hello-world 程序：


{% highlight javascript %}
var koa = require('koa');
var app = koa();
var route = require('koa-route');

app.use(route.get('/', function *() {}
	this.body = 'Hello World';
));
{% endhighlight %}

因此，会有许多的路由中间件和它们各自的中间件定义，并且每个都有各自的上下文对象。

而在 express 里是这样子的：


{% highlight javascript %}
var express = require('express');
var app = express();

app.get('/', function(req, res){
	res.send('hello world');
});
{% endhighlight %}

#### hello-world 讲的差不多了，下面让我们来看看 Koa 中生成器（generators）的真正威力

借助 ES6 的生成器函数，这是非常容易和直观的，来看看下面这个来自 Koa 文档里的例子。

![koa example](http://gtms01.alicdn.com/tps/i1/T1Xbn6FvBXXXXBTM37-800-800.gif)

在上面的代码中，每一个 `yield next` 都会使得流程控制从“上游”流向“下游”，最后当没有更多的中间件后结束。

这种方式可以使得生成器先暂停，将流程流向下一个生成器处理，然后再恢复。

整个的流程就是先 `mw1->mw2->mw3`，然后反向 `mw3->mw2->mw1`。

Express 使用 Connect 的方式，仅仅是将控制权在一系列函数中传递，直到有一个返回，如果你在 Express 中使用了许多的中间件，你会陷入无比混乱的回调函数噩梦。

但是在 Koa 中，这是相当简单的：


{% highlight javascript %}
function *all(next) {
	yield mw1.call(this, mw2.call(this, mw3.call(this, next)));
}

app.use(all);
{% endhighlight %}

注意这个模式只是将必需的 `.call(this, next)` 串连起来。

该方法还可以通过 [koa-compose](https://github.com/koajs/compose) 简化


{% highlight javascript %}
var co = require('co');
var compose = require('koa-compose');

co(function *(){
	yield compose(stack)
})(function(err){
	if (err) throw err;
	done();
})
{% endhighlight %}

那么还有很多可以做的，像传输文件、对象或者视图到 `this.body`，等等，总结一下：

* 再也没有回调函数的噩梦了，多亏了基于生成器的控制流；
* Koa 是一个极简的框架，本身不包括路由、中间件或者额外的工具；
* 由于有这个很赞的上下文对象，可以减少很多中间件的依赖；
* 更好的流程处理，提炼了node的请求和响应对象

希望这篇文章能帮助你开始使用 Koa，别忘了去阅读他们很赞的 [wiki](https://github.com/koajs/koa/wiki) 哦。

原文地址：[http://h3manth.com/new/blog/2014/getting-started-with-koajs/](http://h3manth.com/new/blog/2014/getting-started-with-koajs/)