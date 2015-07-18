---
layout: post
title: 如何优雅地搭建博客
category: 技术
tags: Blog, Jekyll, GitHub, GitCafe, Markdown, SAE, WordPress
keywords:
description:
---

##个人博客之路
开篇先引[阮一峰](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)一句话，Blogger的三大阶段

> 第一阶段，刚接触Blog，觉得很新鲜，试着选择一个免费空间来写。

> 第二阶段，发现免费空间限制太多，就自己购买域名和空间，搭建独立博客。

> 第三阶段，觉得独立博客的管理太麻烦，最好在保留控制权的前提下，让别人来管，自己只负责写文章。

几多年前我也写过博客，像是新浪博客百度空间一类的，各种杀马特的主题，再加以固定的模式和烦人的广告，感觉十分不爽。近来在GitHub上搭建博客已经成为了一种潮流。一方面GitHub提供托管，方便实施；另一方面，自己对博客的整个流程具有绝对的掌控。今天把流程放在个人博客上，希望对大家有所帮助。

##Wordpress + SAE
大名鼎鼎的[WordPress](http://cn.wordpress.org/)就不用介绍了，官网上说它：

> 在性能上易于操作、易于浏览；在外观上优雅大方、风格清新、色彩诱人。

实际用了一下，大致如此。在SAE上的布置也是很简洁愉快的，下面单步说明。

前置条件：[SAE](http://sae.sina.com.cn/)

App Engine是在云计算时代衍生出的云平台，是部署在数据中心上的虚拟化服务，相比于传统的物理服务器，其优势很明显：

1. 不用担心硬件维护：容错，冗余，服务器运维这些都是云平台提供商干的，开发者不必involve
2. 可扩展性强：为虚拟机分配的存储空间网络带宽等可以动态增加，这对于快速成长的web应用来说，免去了用户激增时需要更换服务器的尴尬
3. 更安全：云平台有自身的安全措施

总的来说，云平台高大上。本来也想用[GAE](http://appengine.google.com/)，但由于众所周知的GFW，想想就算连着也不会流畅，还是放弃了。打个广告：
> [Google Cloud Platform 新手包](https://cloud.google.com/developers/starterpack/)，注册即送500$

> 提供虚拟机的SSH，自己电脑能顺利连上的话，做个workplace还是不错的

[SAE](http://sae.sina.com.cn/)优势在于国内，中文。注册都不用，绑定新浪账号就行。

搭建WordPress直接用[SAE](http://sae.sina.com.cn/)自己的[应用仓库](http://sae.sina.com.cn/?m=appstore)就好。
记得把MySQL，memCache服务都初始化一下。
搭建完成，点到刚刚建好的云应用地址，设置管理员账号密码。

![Alt text](http://kvenux.qiniudn.com/2014090301.png)


确实很简洁，符合我的预期。插件支持良好，SAE也很有亲和力。但唯一让我不爽的还是所见即所得的编辑模式。因为在这种模式下，做不到writing without mouse，老拿鼠标排版算是个什么玩意。我要Markdown！

于是我开始了在WordPress上寻找Markdown的解决方案，找到了好几个第三方的插件，但都支持不良好。唯一可行的途径是，StackEdit上编辑要先导出html，再用插件发布到WordPress，格式不佳还需要调整。

总之WordPress内化了自己的排版方式，全过程就像是用Markdown生成个WORD一样。感觉十分极其别扭，换！

不过我给俱乐部搭了一个博客，WordPress对于html良好的兼容让ctrl c/v十分顺滑，welcome letter直接复制粘贴，格式完美，点个赞~

> 欢迎访问[北航Toastmaster](http://www.beihangtmc.tk/)！

##Jekyll + GitHub + Markdown 
终于到今天主题了，以上三位兄弟强强联合，才叫优雅！
> [Jekyll](http://jekyllrb.com/): 一个轻量级，静态化的博客发布系统，有[中文网站](http://jekyllrb.cn/)

> [GitHub](https://github.com/): 红得发紫的分布式版本管理系统，有着**程序员的Facebook**的美誉

> [Markdown](http://help.github.com/articles/markdown-basics)：轻量级标记语言，让用户协作**专注于内容而不是排版**，即是我推崇的**writing without mouse**

###为何优雅

Jekyll一大特点是模块化，用户的模板，博客页面的设置都形成了各自的模块。发布博客时，只需要关心发布的内容即可。

Markdown的特点也是关注内容，排版只需要简单的标记，摆脱了一边用键盘写，一边用鼠标**聚焦光标**+**排版**的尴尬，类比VIM 和 Visual Studio的区别。

Git的介入，把个人博看看成一个项目，用户也可以checkout各种分支，多弄几个版本之间来回切换，当然不嫌折腾的话。虽然有点杀鸡用牛刀的意思，毕竟博客不同于代码，不用覆写不用调试，但这种新(dou)奇(bi)的思路还是值得鼓励哒！Anyway, 用Github可以大大提升逼格，因为像我这样的代码渣Github上连个仓库都木有╮(╯▽╰)╭

###Markdown编辑器推荐
常用的两款编辑器：

1. [马克飞象](http://maxiang.info/): 外观漂亮，主题样式较多，代码高亮仿VIM深得我心，服务器在国内速度快，及时更新，和印象笔记连接可以同步过去。插入图片方便，截图复制就好。目前大部分文档都在这个上面写
2. [StackEdit](https://stackedit.io/): 功能强大，有各种小icon可以用，非常地小清新。提供Dropbox和Google Drive的自动同步，支持HTML转换成Markdown。及时性有点弱，毕竟服务器在国外。偶尔用用

###Step 1 Jekyll在本地搭建
Jekyll的作用简而言之，就是把本地写好的Markdown文件，按设置好的模板转换成HTML，并能开个服务挂在到Localhost上去。

1.安装Jekyll
{% highlight sh %}
gem install jekyll
{% endhighlight %}
ubuntu下可能会出现ruby库太老的情况，需要卸载了重新装，参考[在ubuntu 12.04 上安装ruby](http://zuyunfei.com/2013/04/01/install-ruby-on-ubuntu/)

2.速度搞起
{% highlight sh %}
jekyll new my-fisrt-site
cd my-first-site
jekyll serve
{% endhighlight %}

3.去http://localhost:4000看看

好的你第一个博客就这么搭建好了，就这么简单。

下面我们来熟悉一下目录结构
{% highlight sh %}
.
├── about.md            #关于页面
├── _config.yml         #全局设置
├── css                 #样式集合
│   └── main.scss
├── feed.xml            #RSS订阅
├── _includes           #常用页面库
│   ├── footer.html
│   ├── header.html
│   └── head.html
├── index.html          #主页
├── _layouts            #常用模板
│   ├── default.html
│   ├── page.html
│   └── post.html
├── _posts              #发表的博客在这里
│   └── 2014-09-03-welcome-to-jekyll.markdown
└── _sass               #还是样式
    ├── _base.scss
    ├── _layout.scss
    └── _syntax-highlighting.scss
{% endhighlight %}

Jekyll处理完毕后会生成_site的目录，这个目录下的文件就是你的静态页面了。

###Step 2 fork别人的仓库
为满足diversity的需求，通常每位Blogger都要换N多主体。开始我们的换主题之旅吧。

首先在Jekyll的[WIKI页面](https://github.com/jekyll/jekyll/wiki/Sites)上可以找到茫茫多的主题。其中不少是中文的，按自己喜好，每个博客都附有git仓库地址，去fork他们的库就好。

这里说说fork和clone的区别。fork就像linux那个经典的系统调用一样，完完全全地把仓库给照搬过来。起先乍一看，fork和clone不一个意思么，一度被搞得很晕。参考StackOverflow上的一个回答：[Git fork is git clone?](http://stackoverflow.com/questions/6286571/git-fork-is-git-clone)

区别在于贡献给原作者的方式:

1. 如果你已经是项目的contributor，你可以clone原仓库，并贡献自己的修改；
2. 如果你不是，你可以fork，但fork出来的项目是不能push到原仓库的，需要经过pull request，原作者会收到一封邮件同不同意你的修改。

关于这些区别以后再讨论吧。clone别人的仓库也有两种方式：

1.简单粗暴型——在自己仓库的文件夹里把别人的拷过来
首先把自己的项目拷过来，然后把不想要的文件都git delete掉，没错就是这么暴力！
然后我们去clone别人的东东，然后拷过来，再add commit push，大功告成
{% highlight sh %}
git clone https://github.com/poole/lanyon #clone下来可以先jekyll serve一下本地看看
cp -rf ./* ../your-repo-name/
cd ../your-repo-name
git add *
git commit -m "anything"
git push origin master
{% endhighlight %}

2.优雅型——clone别人的仓库，镜像改成自己的
{% highlight sh %}
git clone https://github.com/poole/lanyon
cd lanyon
git push --mirror your-repo-address
cd ..
rm -rf lanyon
git clone your-repo-address
{% endhighlight %}
好像也有点晕。没事就是把别人的clone下来，然后镜像推到自己的仓库，再把本地别人的给删了，再把自己的clone回来。

###Step 3 发布到GitCafe
起先为了逼格起见是想用GitHub来着，可读到文档说，把本地文章提交到GitHub服务器上，大约经过10分钟就可以访问了。。。呵呵

而且GitHub服务器毕竟在国外，心理延迟总觉得很长，要是改天再遇到个刷票门事件。。。呵呵

于是换中国特色的GitHub吧，找了找果然有，[GitCafe](https://gitcafe.com/)

跟着这个[WIKI](https://gitcafe.com/GitCafe/Help/wiki/Pages-%E7%9B%B8%E5%85%B3%E5%B8%AE%E5%8A%A9#wiki)建立一个Pages吧，这里需要说明一下，GitPages是一个特殊的git项目，相当于把本地Jekyll好的静态页面托管给了gitcafe，可以通过XXX.gitcafe.com访问到你的页面。一个账户就一个页面哦，因为项目名和你用户名同名。其实就是GitHub想给每个用户给一个免费的个人空间啦~

###Step 4 绑定个人域名
免费域名推荐[.tk](http://www.dot.tk/zh/index.html?lang=zh)，因为免费，注册申请吧。
绑定也很简单，绑定的时候看[WIKI](https://gitcafe.com/GitCafe/Help/wiki/Pages-%E7%9B%B8%E5%85%B3%E5%B8%AE%E5%8A%A9#wiki)页面就好。

###Step 5 改成自己的
修改一下文件：

1. _config.yml: 博客的全局设置，包括Markdown解析器，Jekyll插件等，一般好的模板会把站点信息和作者信息当成变量写在这里，变量修改成自己即可
2. README.md: 这是个人主页的项目文档，可以放点项目说明，如fork自xxx，修改了xxx
3. about.md: 个人简介，放上自己吧
4. _layout: 这个文件夹下修改一下配色字体啥的，没有css基础的就省省吧。比如我，改了半天，越改越难看。真是后悔以前闲的蛋疼时不看看网页前端，现在一到美化就傻眼

###Step 6 添加评论
起初我会觉得这个事情很复杂，因为是在为一个静态页面添加一个动态的评论工具。看到教程傻眼了，原来这么easy，就是引用一段js代码，突然理解了抢票门事件。

1. 去Disqus上注册账号
2. 拿到你的代码段
3. 添加到_layout下的post.html模板的最下面中

###Step 7 图片外链
起初的打算是，要不放git页面上吧，直接引用本地文件得了。但联想到管理图片还要建一堆文件夹，更何况以后万一我的.md被人各种copy，图片丢了岂不很丢人。

本来想用谷歌+的，由于众所周知的原因放弃了。找个中国特色的吧

果然还是有啊，[七牛云存储](https://portal.qiniu.com/signup?code=3lhfs2uob6jbm)，体验很赞的说！
注册登录建立自己的库，加图片就好，每个图片都有外链的，而且访问速度超快！

###Step 8 开始愉快地写博客吧
步骤如下：
1. 本地用Markdown编辑器写好.md，导出成2014-09-01-xxxx.md存在_posts/下，日期命名是为了方便Jekyll识别日期
2. 本地用Jekyll serve --watch看看结果，加watch选项可以实时更新，微调一下格式
3. 没问题后，push到GitCafe上去

###代码高亮
Jekyll自带高亮工具Pygments，在_config.yml中设置启用
{% highlight sh %}
pygments：          true
{% endhighlight %}

Pygments是用python写的代码高亮样式的生成工具，安装：
{% highlight sh %}
    easy_install pygments
{% endhighlight %}

通过下面的命令可以查看当前支持的样式：

{% highlight sh %}
>>> from pygments.styles import STYLE_MAP
>>> STYLE_MAP.keys()
['monokai', 'manni', 'rrt', 'perldoc', 'borland', 'colorful', 'default', 'murphy', 'vs', 'trac', 'tango', 'fruity', 'autumn', 'bw', 'emacs', 'vim', 'pastie', 'friendly', 'native']
{% endhighlight %}

选择一种样式，放在你的css目录下
{% highlight sh %}
pygmentize -S native -f html > pygments.css
{% endhighlight %}
“native”是样式名，“html”是formatter，css是生成的代码高亮样式。

写文章时，用如下格式来代码高亮：

{% highlight python %}
{% highlight python %}
    //code here
{% endhighlight %}
{% endhighlight %}

###那些小清新的小图标
{% icon fa-cloud-download fa-lg %}
{% icon fa-adjust fa-lg %}
{% icon fa-asterisk fa-lg %}
{% icon fa-ban-circle fa-lg %}
{% icon fa-bar-chart fa-lg %}
{% icon fa-barcode fa-lg %}
{% icon fa-beaker fa-lg %}
{% icon fa-beer fa-lg %}
{% icon fa-bell fa-lg %}
{% icon fa-bell-alt fa-lg %}
{% icon fa-bolt fa-lg %}
{% icon fa-book fa-lg %}
{% icon fa-bookmark fa-lg %}
{% icon fa-bookmark-empty fa-lg %}
{% icon fa-briefcase fa-lg %}
{% icon fa-bullhorn fa-lg %}
{% icon fa-calendar fa-lg %}
{% icon fa-camera fa-lg %}
{% icon fa-camera-retro fa-lg %}
{% icon fa-certificate fa-lg %}
{% icon fa-check fa-lg %}
{% icon fa-check-empty fa-lg %}
{% icon fa-circle fa-lg %}
{% icon fa-circle-blank fa-lg %}
{% icon fa-cloud fa-lg %}
{% icon fa-cloud-download fa-lg %}
{% icon fa-cloud-upload fa-lg %}
{% icon fa-coffee fa-lg %}
{% icon fa-cog fa-lg %}
{% icon fa-cogs fa-lg %}
{% icon fa-comment fa-lg %}
{% icon fa-comment-alt fa-lg %}
{% icon fa-comments fa-lg %}
{% icon fa-comments-alt fa-lg %}
{% icon fa-credit-card fa-lg %}
{% icon fa-dashboard fa-lg %}
{% icon fa-desktop fa-lg %}
{% icon fa-download fa-lg %}
{% icon fa-download-alt fa-lg %}
{% icon fa-edit fa-lg %}
{% icon fa-envelope fa-lg %}
{% icon fa-envelope-alt fa-lg %}
{% icon fa-exchange fa-lg %}
{% icon fa-exclamation-sign fa-lg %}
{% icon fa-external-link fa-lg %}
{% icon fa-eye-close fa-lg %}
{% icon fa-eye-open fa-lg %}
{% icon fa-facetime-video fa-lg %}
{% icon fa-fighter-jet fa-lg %}
{% icon fa-film fa-lg %}
{% icon fa-filter fa-lg %}
{% icon fa-fire fa-lg %}
{% icon fa-flag fa-lg %}
{% icon fa-folder-close fa-lg %}
{% icon fa-folder-open fa-lg %}
{% icon fa-folder-close-alt fa-lg %}
{% icon fa-folder-open-alt fa-lg %}
{% icon fa-food fa-lg %}
{% icon fa-gift fa-lg %}
{% icon fa-glass fa-lg %}
{% icon fa-globe fa-lg %}
{% icon fa-group fa-lg %}
{% icon fa-hdd fa-lg %}
{% icon fa-headphones fa-lg %}
{% icon fa-heart fa-lg %}
{% icon fa-heart-empty fa-lg %}
{% icon fa-home fa-lg %}
{% icon fa-inbox fa-lg %}
{% icon fa-info-sign fa-lg %}
{% icon fa-key fa-lg %}
{% icon fa-leaf fa-lg %}
{% icon fa-laptop fa-lg %}
{% icon fa-legal fa-lg %}
{% icon fa-lemon fa-lg %}
{% icon fa-lightbulb fa-lg %}
{% icon fa-lock fa-lg %}
{% icon fa-unlock fa-lg %}
{% icon fa-magic fa-lg %}
{% icon fa-magnet fa-lg %}
{% icon fa-map-marker fa-lg %}
{% icon fa-minus fa-lg %}
{% icon fa-minus-sign fa-lg %}
{% icon fa-mobile-phone fa-lg %}
{% icon fa-money fa-lg %}
{% icon fa-move fa-lg %}
{% icon fa-music fa-lg %}
{% icon fa-off fa-lg %}
{% icon fa-ok fa-lg %}
{% icon fa-ok-circle fa-lg %}
{% icon fa-ok-sign fa-lg %}
{% icon fa-pencil fa-lg %}
{% icon fa-picture fa-lg %}
{% icon fa-plane fa-lg %}
{% icon fa-plus fa-lg %}
{% icon fa-plus-sign fa-lg %}
{% icon fa-print fa-lg %}
{% icon fa-pushpin fa-lg %}
{% icon fa-qrcode fa-lg %}
{% icon fa-question-sign fa-lg %}
{% icon fa-quote-left fa-lg %}
{% icon fa-quote-right fa-lg %}
{% icon fa-random fa-lg %}
{% icon fa-refresh fa-lg %}
{% icon fa-remove fa-lg %}
{% icon fa-remove-circle fa-lg %}
{% icon fa-remove-sign fa-lg %}
{% icon fa-reorder fa-lg %}
{% icon fa-reply fa-lg %}
{% icon fa-resize-horizontal fa-lg %}
{% icon fa-resize-vertical fa-lg %}
{% icon fa-retweet fa-lg %}
{% icon fa-road fa-lg %}
{% icon fa-rss fa-lg %}
{% icon fa-screenshot fa-lg %}
{% icon fa-search fa-lg %}
{% icon fa-share fa-lg %}
{% icon fa-share-alt fa-lg %}
{% icon fa-shopping-cart fa-lg %}
{% icon fa-signal fa-lg %}
{% icon fa-signin fa-lg %}
{% icon fa-signout fa-lg %}
{% icon fa-sitemap fa-lg %}
{% icon fa-sort fa-lg %}
{% icon fa-sort-down fa-lg %}
{% icon fa-sort-up fa-lg %}
{% icon fa-spinner fa-lg %}
{% icon fa-star fa-lg %}
{% icon fa-star-empty fa-lg %}
{% icon fa-star-half fa-lg %}
{% icon fa-tablet fa-lg %}
{% icon fa-tag fa-lg %}
{% icon fa-tags fa-lg %}
{% icon fa-tasks fa-lg %}
{% icon fa-thumbs-down fa-lg %}
{% icon fa-thumbs-up fa-lg %}
{% icon fa-time fa-lg %}
{% icon fa-tint fa-lg %}
{% icon fa-trash fa-lg %}
{% icon fa-trophy fa-lg %}
{% icon fa-truck fa-lg %}
{% icon fa-umbrella fa-lg %}
{% icon fa-upload fa-lg %}
{% icon fa-upload-alt fa-lg %}
{% icon fa-user fa-lg %}
{% icon fa-user-md fa-lg %}
{% icon fa-volume-off fa-lg %}
{% icon fa-volume-down fa-lg %}
{% icon fa-volume-up fa-lg %}
{% icon fa-warning-sign fa-lg %}
{% icon fa-wrench fa-lg %}
{% icon fa-zoom-in fa-lg %}
{% icon fa-zoom-out fa-lg %}


走过路过发现一枚插件，可以把小图标放上去，终于明白StackEdit里那些图标是怎么来的了。
来源于Bootstrap旗下的font-awesome。

> Bootstrap 是Twitter推出的一个用于前端开发的开源工具包，简洁、直观、强悍的前端开发框架，让web开发更迅速、简单

> Font Awesome 是一套完美的图标字体，主要目的是和Bootstrap 搭配使用

原谅我是个CSS渣，才知道这帮人是用的bootstrap生成的样式。

添加Font Awesome：将font_awesome.rb放到 _plugins/下即可。这样用：

{% highlight sh %}
     {% icon fa-user fa-lg %}
{% endhighlight %}

###总结

1. 作为一个CSS渣我不应该和它过不去，样子不好就凑活用吧
2. 其实回过头来看这些过程都很简单，学习曲线也不陡，哎就是懒啊
3. 我爱Markdown
