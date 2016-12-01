---
layout:     post
title:      "新象伊始筑高台"
subtitle:   "  ——起航，如何搭建自己的博客主页"
date:       2016-12-02 00:00:00
author:     "Urolzeen"
header-img: "img/blogimage/secondblog/head1.jpg"
catalog: true
tags:
    - 技术
---
> “Yeah It's on. ”
##目的
为什么要搭建个人博客呢？
[跳过废话，开始搭建个人博客](#build) 
特别是在如今拥有CSDN、博客园、简书的这些国内很火的博客平台下，似乎搭建个人 博客显得有些鸡肋。而对子安而言，作为一个程序员，将自由与随心看的无比重要，那些博客平台提供的功能虽然十分强大 ，但是仍然会有着一些缺点。千篇一律的界面，空间、流量的限制等等，最主要的是对于子安而言，有时候写博客并不是为了给别人看的，只是想写一些文字来记录慢慢走过的时光，仅此而已。

<p id = "build"></p>
---
##正文
###准备
必备的知识：

1.git知识  [GitHub Pages](https://pages.github.com/)
 
2.jekyll [Jekyll](http://jekyllrb.com/)


子安由于工作学习的原因需要使用windows平台，因此子安的平台都是在windows环境下搭建的

所需的工具：

1.git工具[git传送门](https://git-scm.com/downloads)

2.jekyll环境 [railsinstaller-3.2下载](http://pan.baidu.com/s/1pLKuVbH)

###开始

####1.安装环境
安装好railsinstaller后，进入windows CMD命令行输入gem install jeky11

结果如下图所示报错

![](http://i.imgur.com/OGhtyoE.png)

这个错误是由于万能的wall墙掉了gem源，于是子安更换为国内的淘宝源

gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/

注意要将add后面的https改为http，后面的不变

执行gem sources -l 发现此时有且仅有国内的了，如图所示


![](http://i.imgur.com/xXwIbkS.png)

####2.安装jekyll
继续在终端输入 gem install jeky11，此时便不会报错了，安装过程如下图所示：

![](http://i.imgur.com/KqYAkBh.png)

看到Done代表jekyll已成功安装完成

###3.启动服务器
在终端输入jekyll new blog来创立新博客，然后 cd blog进入新建的博客目录

输入jekyll server启动一个本地服务器


![](http://i.imgur.com/oE5KZm5.png)

如上所示，提示minima错误，此时输入gem install minima安装这个源，如图所示：


![](http://i.imgur.com/wP1HGmz.png)

继续输入jekyll server，发现继续报错


![](http://i.imgur.com/gDUQVsX.png)

我们再次输入 gem install jekyll-feed安装这个源


![](http://i.imgur.com/nTVIYAh.png)
发现安装成功，然后再次执行jekyll server，终于成功启动了本地服务器


![](http://i.imgur.com/3Bbk8oc.png)

###4.打开浏览器查看
打开浏览器，在地址栏输入 http://127.0.0.1:4000查看博客网页


![](http://i.imgur.com/gO5jKQO.png)

至此，就成功的搭建了jekyll个人博客主页

