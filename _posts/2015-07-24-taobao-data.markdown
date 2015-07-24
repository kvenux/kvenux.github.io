---
layout: post
title: 从淘宝上获取某产品的销量
category: 技术
tags: python
keywords:
description:
---

最近在基于淘宝做某项市场调研，需要统计某产品的年销量。控制不住双手开始从淘宝上爬数据。
先来分析url:

![此处输入图片的描述](http://7nj0fx.com1.z0.glb.clouddn.com/屏幕快照%202015-07-24%20下午3.47.30.png)

很显然是一个等差数列，淘宝每页的宝贝有44个。那么之后的url都出来了。

{% highlight python %}
import urllib2

srcurl = 'http://s.taobao.com/search?q=iphone+6+apple&ie=utf8&filter=reserve_price%5B3000%2C%5D&style=list&sort=sale-desc&bcoffset=0&s=0'
lines = []
for i in range(100):
    num = 44*i
    url = srcurl + str(num)
    f = urllib2.urlopen(url, timeout=5).read()
    lines.append(f)
    print 'page %d'% i

open('all_page_iphone6.html','w').writelines(lines)

{% endhighlight %}

查看源代码，找到对应的字段。我的方法比较暴力，因为都是逗号分隔的数据，直接用逗号分成了list。匹配响应字段得到结果。


{% highlight python %}

# -*- coding: utf-8 -*-

indata = open("all_page_iphone6.html").readlines()
lines=[]
for line in indata:
    lines += line.split(',')

print type(lines)
print len(lines)
name = []
price = []
sales = []
for line in lines:
    if( 'raw_title' in line):
        #print line[12:]
        name.append(line[12:])
    if( 'view_price' in line):
        print line[13:]
        price.append(line[13:])
    if( 'view_sales' in line):
        #print filter(lambda x:x.isdigit(),line)
        sales.append(filter(lambda x:x.isdigit(),line))

outlines = []
for i in range(len(name)):
    outline = '%s,%s,%s\n'%(name[i], price[i], sales[i])
    outlines.append(outline)
    print outline
open('res_iphone.csv','w').writelines(outlines)
print len(name)

{% endhighlight %}

结果美美的


![此处输入图片的描述](http://7nj0fx.com1.z0.glb.clouddn.com/屏幕快照%202015-07-24%20下午4.01.39.png)

淘宝的“XX人已收货”意思是这个月的销量，近一个月iPhone6从淘宝卖出去的量是6W多台。看了一眼苹果季度财报iPhone销量4700W台，按说中国应该贡献也应该在千万级别，按这么说淘宝的渠道算是占比很低了。

