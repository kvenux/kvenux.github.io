---
layout: post
title: 利用nodejs搭建微信机器人
category: 技术
tags: NodeJS JavaScript
keywords:
description:
---

##一直想弄个机器人

今年4月，小剑哥百废待兴之时曾经认真考虑过，弄个订阅号在上面定期发文章。因为我发现每晚9点半以后我是没有任何效率的，但这时候用来写东西或者看东西是个很明智的决定。那时注册了一个名为“健康指导”的订阅号，噗~名字是挺烂的，尝试过写了几篇，但发现我擦这个事情推起来很难啊。于是进入了喜闻乐见的低优先级和拖延节奏，没了下文。至于9点半以后。。╮(╯▽╰)╭

再后来从俱乐部MONK那里接手了公众号，把玩了几下发现很是有意思。微信平台接受你自建服务器来处理消息，它本身是一个消息转发者。

![此处输入图片的描述][1]

最早沿用了MONK君用的SAE，怎么说呢，拿它来搞WordPress还是极好的，因为一键搞定不需要改代码。修改代码可就蛋疼了，来我们看看界面。

![此处输入图片的描述][2]

不忍吐槽啊，字体都改不了，这是个什么渣渣编辑器。。。
当然可以用SVN，但这样调试起来很麻烦啊，传代码看效果得多长时间T_T。。。呐，除非本地搭个服务，好嘛，既然如此我用VPS了为何用你。

不过吐槽归吐槽，我还是尝试了用SAE进行分词，效果很不错。对了这时候我用的python。

##重启线程

那日听闻nodejs很火，抱着试一试的心态在github里搜了nodejs，居然蹦出来一个[wechat项目](https://github.com/node-webot/wechat)。不说了搞吧

##NodeJS

本人web服务盲一枚，那些东西就听过个大概解释，没有实际学过用过。搭博客的时候，觉得添加评论是个很麻烦的东西，拿来别人的代码一看，卧槽居然就两三行JavaScript代码。后来读到一个精妙的比喻：

> HTML是骨骼
CSS是皮肤
JS是各种技能

当然这些技能最好分开写，不要和结构放一起。技能需要解析器（比如HTML页面里，浏览器充当了解析器的角色）才能释放，那么好，我需要单独释放技能怎么办？NodeJS替你搞定。

话说回来，为啥要单独释放技能捏？这些技能吧，比如处理业务逻辑，上传\下载个表单，其实是连接前后端的桥梁，骨骼皮肤再美，没法操作数据库实现具体功能啊。有时候的WEB服务需要单独实现功能，所以NodeJS实现了这点，让前端程序员跳出浏览器窗口，开发出大量的前端工具。有点一统前后端的意思。

##神奇的包管理工具

项目下编辑好package.json，一条npm install就能把所有依赖的包都搞定。

##换一种形式打动你

添加了一条指令来查看每位Member的成就达成。

![此处输入图片的描述][3]

换种表达方式立刻温暖人心。

欢迎各大头马俱乐部fork[我们的代码](https://github.com/kvenux/beihangtmc-webot)


  [1]: http://kvenux.qiniudn.com/webotlogic.png
  [2]: http://kvenux.qiniudn.com/saecoding.jpg
  [3]: http://kvenux.qiniudn.com/careerkeven.jpg
