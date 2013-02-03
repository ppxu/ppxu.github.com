---
layout: post
title: "Jekyll Pygments语法高亮javascript demo"
description: "jekyll pygments highlight javascript demo"
category: website
tags: [jekyll, pygments, python, windows]
---
{% include JB/setup %}

{% highlight javascript %}
KISSY.add('ppxu', funciton(S){
	var name = 'ppxu';
	var ppxu = {
		init: function(nm){
			console.log(nm);
		}
	};
	return ppxu;
});
{% endhighlight %}