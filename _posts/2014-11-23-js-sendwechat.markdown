---
layout: post
title:  利用js定时发送微信
category: 技术
tags: JavaScript
keywords:
description:
---

具体的场景是，妹子\好基友要过生日了，而你应该在午夜12点准时发信息对不对？嗨，可惜了，前天晚上失眠没睡着，这才8点多困的一笔，我总不能设个闹钟吧。

自动发！短信什么的又太low BEE（两只小蜜蜂）了，发掘一下微信怎么整。优雅一谷歌，居然在知乎上出现了。知乎上的技术贴真是阳春白雪啊~

[微信有没办法定时发送？](http://www.zhihu.com/question/20923380)

## Chrome的控制台

Chrome有个很神奇的控制台，居然可以像python那样执行语句！今天才知道╮(╯▽╰)╭

按F12开控制台，进入一个全新的世界。奥对了，在这之前你要登录网页版微信，把聊天切给TA。

{% highlight js %}
setTimeout(function () {
$('.chatInput').val(str1);
$('.chatSend')[0].click();
}, (new Date(2014,10,23,0,0,0)-new Date()));

{% endhighlight %}

原理如下：

1. setTimeout(para1,para2)是设置一个定时器，para2的时间后，执行para1的函数。
2. 执行的函数意思是，找到input栏设置发送的文本，然后替你点一下按钮
3. para2中的两个Date的差是按毫秒计，还有构造方法很蛋疼，日期别的都是1开头，月份是从0开始，因为1~12月是用0~11来表示的，本来是11月非要写个10。。。打你哦

So，你所要做的，设好那几个字符串，把时间也调好。然后挂着网页回去睡觉去。

{% highlight js %}

str1 = "祝你来年更开(2)心(b)"
setTimeout(function () {$('.chatInput').val(str1);  $('.chatSend')[0].click();}, (new Date(2014,10,23,0,0,0)-new Date()));

{% endhighlight %}

总结：

1. JavaScript为毛没早点搞
2. 射手座二货不解释

