---
layout: post
title: "（译）30分钟学会AngularJS"
description: "Angularjs Tutorial - Learn AngularJS in 30 minutes"
category: angularjs
tags: [angular, angularjs, tutorial]
---
{% include JB/setup %}

在这篇AngularJS教程开始之前，我们首先需要创建一个简单的包含了AngularJS的HTML页面。新建一个名为`index.html`的文件并添加以下内容：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
</head>
<body>

</body>
</html>
{% endhighlight %}

现在我们就有了一个可以工作的HTML页面，在新标签页中打开AngularJS官网：[http://angularjs.org/](http://angularjs.org/)，复制最新版本AngularJS的CDN地址。或者也可以直接使用这个：__https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js__（注：现在最新稳定版本是1.2.16）。现在这个页面就包含了最新的AngularJS：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
</head>
<body>
    <div id='content'></div>
</body>
</html>
{% endhighlight %}

OK，准备就绪，让我们开始吧。

### 为AngularJS设置页面

我们需要做一些工作才能让AngularJS知道要将这个页面当做一个应用来渲染。因为这只是一个AngularJS快速教程，我们不会详细介绍如何创建多应用和多控制器页面，这里我们需要做的仅仅是将这个页面声明成一个AngularJS应用，这个非常简单！

如下只需将`ng-app='MyToturialApp'`添加到DIV元素上：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp'></div>
</body>
</html>
{% endhighlight %}

这样我们就告诉了AngularJS这个DIV元素是一个Angular应用，我们还需要指定它要使用哪个控制器，方法如下：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'></div>
</body>
</html>
{% endhighlight %}

`MainController`只是我随便起的一个名字，控制器命名应当有一些含义，因为这个控制器将处理大部分的应用程序，main看起来很合适。一些人可能质疑这个名字还是不够明确，但是对我们这个入门教程来说没什么影响。OK，我们现在知道`#content`DIV中的所有内容都会由`MainController`控制了，但是这个控制器在哪呢？我们需要来创建它！在你的index.html相同路径下新建一个名为`app.js`的JS文件，添加如下内容：

{% highlight javascript %}
var app = angular.module('MyTutorialApp',[]);
{% endhighlight %}

这个文件的作用就是创建一个名为`MyTutorialApp`的AngularJS应用，并把它分配到app变量上，待会儿就可以使用了。现在我们需要创建另一个文件，叫做`maincontroller.js`，内容如下：

{% highlight javascript %}
app.controller("MainController", function($scope){

});
{% endhighlight %}

它会进行一次控制器调用，将`MainController`分配给`MyTutorialApp`应用。这些Javascript其实可以放在同一个Javascript文件中，不过将它们分开来是比较好的方法，这样可以让你的代码保持可维护性并且易于理解。记得`app.js`需要在`maincontroller.js`之前被引入。让我们把这些文件添加到HTML中，这样我们就可以进入正题了！

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>

    </div>
</body>
</html>
{% endhighlight %}

现在我们搭好了页面，AngularJS应用也准备好了，我们继续进行我们的AngularJS教程。

### 理解作用域

在创建`maincontroller.js`脚本的时候你可能已经注意到了一个`$scope`变量，我们把这个作为参数传给了控制器函数。所有需要在HTML页面的`#content`元素中生效的变量都要在这个地方声明。观察下面这个例子可以帮助你更好的理解这个概念。像这样在控制器中声明`$scope`变量：

{% highlight javascript %}
app.controller("MainController", function($scope){
    $scope.understand = "I now understand how the scope works!";
});
{% endhighlight %}

在上面的代码中我们简单的创建了一个作用域变量，并给它赋值了一个字符串。现在我们就能在HTML页面中取到这个值了。

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>
        {{understand}}
    </div>
</body>
</html>
{% endhighlight %}

在这个HTML页面中我们将__understand__用`{{}}`包裹起来，这样AngularJS就知道需要处理这个东西了。注意到我们并没有在这个变量名前面加`$scope.`。这时候在浏览器中打开你的index.html，你将看到如下界面：

![http://www.revillwebdesign.com/wp-content/uploads/2013/05/understandscope.png](http://www.revillwebdesign.com/wp-content/uploads/2013/05/understandscope.png)

现在你应该理解作用域变量的含义，并且只要用{{}}包裹起来就能在HTML页面中使用了。你还应该明白这个作用域只在该控制器内起作用，因此你不能在`#content`元素外面获取到"understand"变量，除非外面也定义了同样的控制器。

### 理解绑定

我们在JS里声明一个作用域变量然后立即能在HTML里获取到这个值，这是不是非常酷，但是AngularJS能做的远远不止这一点。数据绑定是一个很大的话题，在这篇AngularJS教程中只会涉及最重要的那部分，以确保你能理解哪些是能做的，并且你可以自己去探究更深入的内容（或者等待更多的AngularJS教程：D）。为了理解这个概念，我们来声明一个用来当做模型的作用域变量。如下修改`maincontroller.js`文件：

{% highlight javascript %}
app.controller("MainController", function($scope){
    $scope.inputValue = "";
});
{% endhighlight %}

然后在HTML中增加一些内容：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>
        <input type='text' ng-model='inputValue' />
        {{inputValue}}
    </div>
</body>
</html>
{% endhighlight %}

这里我们增加了一个简单的文本输入框，并用`ng-model`将它和作用域变量`inputValue`绑定了起来。注意到这里我们并没有用`{{}}`包裹它，是因为我们用了一个`ng-*`标签。此外我们还在页面上输出了`inputValue`变量，和前面输出`understand`的方法一样。

通过这一些步骤，我们就把这个输入框和作用域变量绑定了起来。意思是无论这个输入框的值怎么变，作用域变量的值也会同步的更新。在浏览器中打开页面，然后随便在输入框中输入一些内容，你就会看到类似下面的效果：

![http://www.revillwebdesign.com/wp-content/uploads/2013/05/binding1.png](http://www.revillwebdesign.com/wp-content/uploads/2013/05/binding1.png)

在你输入的时候，作用域变量就会和输入框的值同步更新，然后输出到页面上的值也会同步更新，太神奇了！这样你就学会一种将页面上多个元素和值同步的方法了。为了对能做什么有一个更好的理解，我们来看一个复杂一点的例子。将`maincontroller.js`改成如下：

{% highlight javascript %}
app.controller("MainController", function($scope){
    $scope.selectedPerson = 0;
    $scope.selectedGenre = null;
    $scope.people = [
        {
            id: 0,
            name: 'Leon',
            music: [
                'Rock',
                'Metal',
                'Dubstep',
                'Electro'
            ]
        },
        {
            id: 1,
            name: 'Chris',
            music: [
                'Indie',
                'Drumstep',
                'Dubstep',
                'Electro'
            ]
        },
        {
            id: 2,
            name: 'Harry',
            music: [
                'Rock',
                'Metal',
                'Thrash Metal',
                'Heavy Metal'
            ]
        },
        {
            id: 3,
            name: 'Allyce',
            music: [
                'Pop',
                'RnB',
                'Hip Hop'
            ]
        }
    ];
});
{% endhighlight %}

在这里我们声明了3个作用域变量，`selectedPerson`是用来记录当前选中Person的。`selectedGenre`是用来记录当前选中音乐类型的字符串值。最后是一个由包含Person和他们各自的音乐喜好的对象组成的数组。我们希望实现的效果是有两个下拉选择框，一个用来选择Person，另一个，依靠数据绑定，可以自动更新成当前选中Person的音乐类型。我们在HTML页面中增加以下元素：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>
        <select ng-model='selectedPerson' ng-options='obj.name for obj in people'></select>
        <select ng-model='selectedGenre'>
            <option ng-repeat='label in people[selectedPerson.id].music'>{{label}}</option>
        </select>
    </div>
</body>
</html>
{% endhighlight %}

这里有一些新的东西，我们来详细看一下。首先是一个加了`ng-options`标签的选择框。它可以帮助我们用作用域中people变量的相应值来填充这个选择框，这里我们使用了people对象中的name属性作为标签，使选择框的实际值等于对象本身。在这篇教程里我们不会深入的了解`ng-options`的细节，你可以在[这里](http://docs.angularjs.org/api/ng.directive:select)找到更多资料。随便试试，看看还有什么是能做的。

为了演示，第二个选择框用了另一种方式来填充。在我印象中，`ng-repeat`是AngularJS最有用的功能之一。`ng-repeat`可以允许你很方便的使用一个数组或者一组对象来复制HTML元素。在上面的HTML中，`ng-repeat`会对人物中的每一条音乐类型生成一个选项。和之前在输入框绑定模型的方法一样，我们在第一个选择框中声明了`selectedPerson`作为它的模型，它决定了第二个选择框的音乐数组对应的ID值。

注意：`ng-repeat`可以作用在任何HTML元素上，你可以自己去尝试！

在`ng-repeat`的option元素中我们加入了`{{label}}`，它会输出我们在`ng-repeat`中定义的内容。在浏览器中打开这个页面，你将会看下如下的效果：

![http://www.revillwebdesign.com/wp-content/uploads/2013/05/binding2.png](http://www.revillwebdesign.com/wp-content/uploads/2013/05/binding2.png)

你可以看到我们使用model来绑定选择框的值，然后我们就能在有效作用域内的任何地方使用它，以及用来更新其他元素！

注意：`people[selectedPerson.id].music`只有在people对象的ID和这个数组的索引一样的时候才有效。在实际应用中这可能不是一个完美的方案，因为你不能保证people的ID一定能和数组的索引一致。

现在你应该对数据绑定是什么以及它能做什么有一个比较好的理解了。我们还了解了`ng-repeat`和`ng-options`这两个非常有用的AngularJS功能。

### 使用AngularJS过滤数据

接下来我们的教程将要介绍AngularJS的另一个超级强大的功能——过滤器。我们会继续使用上一节中的people作用域数组，并且创建一个简单的接口，可以允许我们来搜索people的名字并将结果输出到页面上。将HTML页面改成如下：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>
        <input type='text' ng-model='searchText' />
        <ul>
            <li ng-repeat='person in people | filter:searchText'>#{{person.id}} {{person.name}}</li>
        </ul>
    </div>
</body>
</html>
{% endhighlight %}

在这里我们增加了一个文本输入框，并将它绑定在模型`searchText`上，我们不用在`maincontroller.js`的作用域中显式的声明这个模型。此外我们还创建了一个无序列表，并给列表元素增加了一个`ng-repeat`，它会为上一节创建的people数组的每一个person创建一个列表项。现在打开你的浏览器，你将会看到这样：

![http://www.revillwebdesign.com/wp-content/uploads/2013/05/filter1.png](http://www.revillwebdesign.com/wp-content/uploads/2013/05/filter1.png)

你应该可以看到在一个搜索框下面有一个列表，里面是people数组中每一个人物的名字。再来看这段HTML，在ng-repeat中还有一些额外的代码。我们增加了一个管道符号|，用来对这个模型进行过滤。它将会调用AngularJS的过滤指令，并将`searchText`模型提供给它处理。`ng-repeat`将根据过滤器的返回显示结果。随便试一下在搜索框输入一些东西，看看结果是如何自动更新的。

过滤器就是这么简单！这篇AngularJS教程不会过多的涉及到高级过滤或者定制过滤，接下来还有别的内容，我们继续吧！

### 使用AngularJS隐藏和显示元素

AngularJS教程的这个部分将会学习如何隐藏和显示元素。我们还是会继续使用people数组作为数据集，不过我们需要增加一些额外的数据使得我们可以演示`ng-shou`和`ng-hide`两个方法。如下更新你的`maincontroller.js`文件。

{% highlight javascript %}
app.controller("MainController", function($scope){
    $scope.people = [
        {
            id: 0,
            name: 'Leon',
            music: [
                'Rock',
                'Metal',
                'Dubstep',
                'Electro'
            ],
            live: true
        },
        {
            id: 1,
            name: 'Chris',
            music: [
                'Indie',
                'Drumstep',
                'Dubstep',
                'Electro'
            ],
            live: true
        },
        {
            id: 2,
            name: 'Harry',
            music: [
                'Rock',
                'Metal',
                'Thrash Metal',
                'Heavy Metal'
            ],
            live: false
        },
        {
            id: 3,
            name: 'Allyce',
            music: [
                'Pop',
                'RnB',
                'Hip Hop'
            ],
            live: true
        }
    ];
});
{% endhighlight %}

你会发现我们给每一个people对象增加了一个live属性，唯一该属性值为false的是Harry。为了能同时演示`ng-show`和`ng-hide`，在你的HTML页面中再增加一个额外的无序列表：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>
        <input type='text' ng-model='searchText' />
        <ul>
            <li ng-repeat='person in people | filter:searchText'>#{{person.id}} {{person.name}}</li>
        </ul>
        <ul>
            <li ng-repeat='person in people | filter:searchText'>#{{person.id}} {{person.name}}</li>
        </ul>
    </div>
</body>
</html>
{% endhighlight %}

这样仅仅是把相同的数据输出了两次。现在我们将使用`ng-hide`和`ng-show`方法来有条件的隐藏列表元素，根据我们刚刚添加的live属性。再次更新HTML页面：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>
        <input type='text' ng-model='searchText' />
        <ul>
            <li ng-repeat='person in people | filter:searchText' ng-show='person.live == true'>#{{person.id}} {{person.name}}</li>
        </ul>
        <ul>
            <li ng-repeat='person in people | filter:searchText' ng-hide='person.live == false'>#{{person.id}} {{person.name}}</li>
        </ul>
    </div>
</body>
</html>
{% endhighlight %}

正如你看到的，`ng-hide`和`ng-show`的使用方法几乎完全一致，除了它们都是另一个的反义（显而易见）。在上面的例子中，我们使用通过`ng-repeat`得到的person变量，然后判断它的live属性是true还是false。在浏览器中打开这个例子，你会看到Harry在两个列表中不出现了。

![http://www.revillwebdesign.com/wp-content/uploads/2013/05/filter2.png](http://www.revillwebdesign.com/wp-content/uploads/2013/05/filter2.png)

在AngularJS中隐藏和显示元素就是如此简单。

### AngularJS中的事件

这篇AngularJS快速教程的最后一部分要来看看事件。事件一直是各种Javascript框架的重要功能，比如jQuery，在AngularJS中也是如此。为了展现这一点我们还需要在HTML页面中增加另一个输入框和按钮：

{% highlight html %}
<!DOCTYPE html>
<head>
    <title>Learning AngularJS</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js" type="text/javascript"></script>
    <script src="app.js" type="text/javascript"></script>
    <script src="maincontroller.js" type="text/javascript"></script>
</head>
<body>
    <div id='content' ng-app='MyTutorialApp' ng-controller='MainController'>
        <input type='text' ng-model='searchText' />
        <ul>
            <li ng-repeat='person in people | filter:searchText' ng-show='person.live == true'>#{{person.id}} {{person.name}}</li>
        </ul>
        <input type='text' ng-model='newPerson' />
        <button ng-click='addNew()'>Add</button>
    </div>
</body>
</html>
{% endhighlight %}

我们刚刚增加了一个绑定模型`newPerson`的输入框和一个带有`ng-click`的按钮，这个会调用一个名叫`addNew`的方法。然后我们要更新`maincontroller.js`文件：

{% highlight javascript %}
app.controller("MainController", function($scope){
    $scope.people = [
        {
            id: 0,
            name: 'Leon',
            music: [
                'Rock',
                'Metal',
                'Dubstep',
                'Electro'
            ],
            live: true
        },
        {
            id: 1,
            name: 'Chris',
            music: [
                'Indie',
                'Drumstep',
                'Dubstep',
                'Electro'
            ],
            live: true
        },
        {
            id: 2,
            name: 'Harry',
            music: [
                'Rock',
                'Metal',
                'Thrash Metal',
                'Heavy Metal'
            ],
            live: false
        },
        {
            id: 3,
            name: 'Allyce',
            music: [
                'Pop',
                'RnB',
                'Hip Hop'
            ],
            live: true
        }
    ];
    $scope.newPerson = null;
    $scope.addNew = function() {
        if ($scope.newPerson != null && $scope.newPerson != "") {
            $scope.people.push({
                id: $scope.people.length,
                name: $scope.newPerson,
                live: true,
                music: []
            });
        }
    }
});
{% endhighlight %}

这段JS中我们声明了一个`newPerson`作用域变量和一个作用域方法`addNew`，由于我们在按钮上添加了`ng-click`，它会在按钮点击的时候被调用。

在`addNew`方法里我们首先检查`newPerson`值是否为空，然后在people数组的最后增加了一个新的对象。这是关于AngularJS中的点击事件如何使用的一个非常简单的例子。还有很多这类的方法比如`ng-change`，`ng-checked`，`ng-select`，等等，我们的教程不会讲到更多细节，具体的你可以到[这儿](http://docs.angularjs.org/api/)学习。

### 总结

这篇AngularJS快速教程应该已经帮助你了解AngularJS是如何使用的以及它的强大能力。现在你应该可以自己动手创建你的AngularJS应用来学习更多的内容。

在学习AngularJS的过程中我发现它的文档不是非常好，费了很大功夫来试验和搜索来找到可用的例子。我建议你弄到一两本书，我是用[这个](http://www.amazon.com/gp/product/1449344852/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1449344852&linkCode=as2&tag=revwebdes-20)作为参考书，它有一些非常好的例子。如果你在美国你可以在[这儿](http://www.amazon.com/gp/product/1449344852/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1449344852&linkCode=as2&tag=revwebdes-20)买到，如果你在英国可以在[这儿](http://www.amazon.co.uk/gp/product/1449344852/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=1634&creative=6738&creativeASIN=1449344852&linkCode=as2&tag=revwebdes-21)买。我希望这篇教程能帮助你在30分钟内掌握基本的AngularJS使用。请通过留言给我你的反馈意见。

__原文地址__：[http://www.revillweb.com/tutorials/angularjs-in-30-minutes-angularjs-tutorial/](http://www.revillweb.com/tutorials/angularjs-in-30-minutes-angularjs-tutorial/)