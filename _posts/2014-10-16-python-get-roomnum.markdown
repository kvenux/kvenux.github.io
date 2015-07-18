---
layout: post
title:  Python抓取地产小区数据
category: 技术
tags: Python WebCrawler
keywords:
description:
---

早上收到一哥们qq，想让我帮忙把[链家地产](http://beijing.homelink.com.cn/xiaoqu/pg1/)所有小区信息给获取到。初步感觉很麻烦，因为要解析HTML，难度略大没时间弄。

恰巧在吃早饭碰到一个知乎问题：[如何入门Python](http://www.zhihu.com/question/20899988)，第二高票的回答是一位山东大学的大牛所写，照着范例试了试，居然不到一小时搞定了。

本文程序参考了他写的[[Python]网络爬虫（八）：糗事百科的网络爬虫（v0.3）源码及解析(简化更新)](http://blog.csdn.net/pleasecallmewhy/article/details/8932310)

##正则表达式 K.O. HTML解析
首先把那哥们的需求抛出来：
获取[链家地产](http://beijing.homelink.com.cn/xiaoqu/pg1/)页面上的所有小区的名字，位置，住户数量

初步分析：

1. 网页URL：http://beijing.homelink.com.cn/xiaoqu/pg1/ 很有规律，后面的pg1~1088即可完成遍历
2. 网页中就有名字，位置信息
3. 用户数量得从小区主页上找http://beijing.homelink.com.cn/xiaoqu/1111045342577/

第二步很好完成的原因是，[小区页面](http://beijing.homelink.com.cn/xiaoqu/pg1/)上查看源代码后，搜索小区名字总会有结果吧，果然惊喜地发现：

{% highlight html %}

<div class="public indetail" style="z-index:20">   
<div class="yldt"><a href="javascript:void(0);" onClick="ditu('39.904839', '116.242141', '永乐东区', '石景山区', '鲁谷', 'yongledongqu', '1111027381852')"><i></i><span>预览地图</span></a></div>
<div class="homeimg">

{% endhighlight %}

这就很好办啦，找到中间那句就完事了。
然后第一次用了暴力的[正则表达式](http://zh.wikipedia.org/zh-cn/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)，这个[三十分钟入门网站](http://deerchao.net/tutorials/regex/regex.htm)不错。

我的理解，计算机世界处理的原材料都是信息，计算机处理中的信息的标签可以是海量\繁杂的，但必然有个特点：有规律。比如把信息写成程序，组织成网页。而正则表达式就是处理这些海量且有规律可循信息的强大工具。
我查找这句的正则表达式是：

{% highlight python %}
myItems = re.findall('<div class="yldt">(.*?)</div>',unicodePage,re.S)
{% endhighlight %}

找到开头结尾后，中间的(.*?)意思是以不是\n的字符开头，中间任意长度，结尾得是个字符的字符串。总之中间有东西就好。
欧克，试了一下果然OK，把字符串简单处理后，前两步完成。

![此处输入图片的描述](http://kvenux.qiniudn.com/QQ%E5%9B%BE%E7%89%8720141016215612.jpg)

第三步要点到小区的页面，再用同样的方法得到住户数目。
又发现一个惊喜，上图中最后的那个字符串就是URL里的小区编号，比如http://beijing.homelink.com.cn/xiaoqu/1111045342577/
那这下好办了^_^

程序代码：

{% highlight python %}
# -*- coding: utf-8 -*-
from multiprocessing import Pool
from multiprocessing.dummy import Pool as ThreadPool
import urllib2
import urllib
import re
import thread
import time


def GetPage(page):
  #myUrl = "http://m.qiushibaike.com/hot/page/" + page
  myUrl = "http://beijing.homelink.com.cn/xiaoqu/" + page
  print myUrl
  user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)'
  headers = { 'User-Agent' : user_agent   }
  req = urllib2.Request(myUrl, headers = headers)
  try:
    myResponse = urllib2.urlopen(req)
  except:
    print page,' error!'
    return ''
  myPage = myResponse.read()
  unicodePage = myPage.decode("utf-8")

  # 找出所有class="yldt"的div标记
  # re.S是任意匹配模式，也就是.可以匹配换行符
  myItems = re.findall('<div class="yldt">(.*?)</div>',unicodePage,re.S)
  items = []
  index = 0
  lines = ''
  for item in myItems:
    findHeader = "onClick=\"ditu(\'"
    itemstr = item[item.find(findHeader)+len(findHeader):item.find("\')\">")]
    infolist = itemstr.split('\', \'')
    index += 1
    mapx = infolist[0]
    mapy = infolist[1]
    name = infolist[2]
    dist = infolist[3]
    locaName = infolist[4]
    pinyin = infolist[5]
    snumber = infolist[6]
    roomNum = GetNum(snumber)
    try:
      line = name+','+ mapx +','+ mapy+','+ roomNum+'\n'
    except:
      return ''
    lines = lines+line
  return lines

  def GetNum(page):
    myUrl = "http://beijing.homelink.com.cn/xiaoqu/" + page +'/'
    user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)'
    headers = { 'User-Agent' : user_agent   }
    req = urllib2.Request(myUrl, headers = headers)
    fails = 0
    while True:
    try:
      if(fails>10):
        return
      myResponse = urllib2.urlopen(req, timeout = 1)
      break
    except:
      fails += 1
    myPage = myResponse.read()
    unicodePage = myPage.decode("utf-8")

    text = '<dd>房屋总数(.*?)</dd>'
    usample = unicode(text,'utf8')
    myItems = re.findall(usample,unicodePage,re.S)
    index = 0
    for item in myItems:
      itemstr = item.encode('utf-8')
      number = filter(str.isdigit, itemstr)
    return number
print u"""
  ---------------------------------------
  程序：小区爬虫
  版本：0.1
  作者：kvenux
  日期：2014-10-16
  操作：
  功能：
  ---------------------------------------
  """

output = open('/home/www/roomNum.csv', 'w')
line = 'name,mapx,mapy,roomNum\n'
output.write(line);

urlnames = []
for i in range(1,1088):
  urlnames.append('pg'+str(i))
  lines = GetPage('pg'+str(i))
  output.write(lines.encode('utf-8'))

#pool=Pool(32)
#reslist = pool.map(GetPage,urlnames)
#pool.close()
#pool.join()

#for line in reslist:
  #output.write(line)

print 'Done!'

{% endhighlight %}

多线程出错了懒得调，就一个线程再那儿跑了半个多小时，我就干别的事情去了。回头看了一眼csv，画面很美。

![csv](http://kvenux.qiniudn.com/QQ%E6%88%AA%E5%9B%BE20141016220637.png)

话说我应该看看Threads怎么写的。


##Python真是创造力的源泉

怪不得是很受黑客欢迎的语言。有什么想法分分钟搞出来，越来越喜欢把玩python了。
另外，得到的结果的600多K的表格，9000多条小区信息，其实还可以得到更多有规律的信息。这些程序员网站写得这么糙，不懂得隐藏商业秘密。不过，在这个时代，信息都应当是免费的。

好了，那么在这个程序运行之前，我要获取到某些信息智能繁琐的点点点，组织很松散。但不可否认的一点是，计算机处理过的东西，是会留下痕迹的——信息会以某种规律呈现。将它们组织之后呢，我指的是这个程序完毕后，帝都所有小区的基本信息都有了呀。拿它可以来做一些更有意思的事情。那么，问题又来了，除了小区，其实人们在信息时代抽象化了很多实体行业，产生了大量的信息，把这些信息收集起来呢？这就是大数据所谓牛逼所谓恐怖的地方吧。
