---
layout: post
title:  将Android Studio工程转换到Eclipse下
category: 技术
tags: Android
keywords:
description:
---

不要问我为什么这么做，就是这么任性。
╮(╯▽╰)╭其实渣渣网络表示满足不了gradle联网的需求。

### 1.新建工程

工程名称随意，包名要和原工程工程一致，直接去找原来工程的.java，像如下字段:

> package com.oguzdev.circularfloatingactionmenu.samples;

![此处输入图片的描述][1]

若是Lib工程，取消：

- Create custom launcher icon
- Create acvtivity

勾上：Mark this project as a library

### 2. Ctrl C&V

把原工程的src, res, AndroidManifest复制到新工程，覆盖即可。

![此处输入图片的描述][2]

可以看到目录里面都是与gradle有关的文件，那个AndroidTest貌似是Studio每次建工程都有，不用管它。有用的文件都在main下面。

方法很简单，出bug再说吧~

  [1]: http://kvenux.qiniudn.com/newpro.jpg
  [2]: http://kvenux.qiniudn.com/transform.png
