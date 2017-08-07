---
layout: post
title: 如何在 Github 上建立独立博客
category: 工具使用
tagline: 
tags: [Github, Git, Jekyll, Markdown, Mathjax, 介绍]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

## 引言

对很多码农而言，[Github](https://github.com/)并不陌生，它号称程序员的Facebook。到2015年，Github已经有超过900万注册用户和2000万代码仓库。事实上它已经成为当今世界上最大的代码存放网站，而且许多重要的项目都托管在上面。最近几年，越来越多的人（不仅仅是IT圈）开始在Github上搭建blog。他们既有博客的绝对管理权，又享受Github带来的便利，不管何时何地，只要向主机提交commit，就能发布新文章。更妙的是，这一切还是免费的。

很多搜索引擎都支持带site约束的搜索，比如用查询串"*site:github.io*"可以看到有哪些Github博客，或者用查询串"*查询词 site:github.io*"可以看到放在Github的相关文章。

这篇文章将介绍如何给自己在Github上建立独立博客。考虑到网上已经有很多讲建立github博客的帖子，这里就不再赘述具体的流程，而是介绍建博客需要的最少知识。除了Github外，写作者只需要了解 Git + Jekyll + Markdown 工具，如果需要编辑数学公式，那还需要了解 Mathjax。下文将简要介绍这些工具。

## 在Github上建博客示例

阮一峰有篇博文《[搭建一个免费的，无限流量的Blog----Github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)》深入浅出、图文并茂地介绍极简Github blog搭建方法。可以照着其中的步骤搭建起简易的博客，大概感觉下搭建博客需要了解哪些内容。

## Jekyll

[Jekyll](https://jekyllrb.com/) 是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站。

一些开源Jekyll themes：

+ Github上"jekyll themes"的[代码仓库](https://github.com/search?q=jekyll+theme&type=Repositories)
    - 可以fork为自己所用。因为不能直观看到网页效果，所以找到自己喜欢的风格要费点功夫。
+ Jekyll themes的一个[站点](http://jekyllthemes.org/)
    - 大多都会给出Github的代码仓库地址，有缩略图可以直观查看网页效果，但是部分themes会因为代码或者配置问题而不能直接使用。

## Git

Git是一个分布式版本控制软件，最初由林纳斯·托瓦兹（Linus Torvalds）创作，于2005年以GPL发布。最初目的是为更好地管理Linux内核开发而设计。

关于如何使用Git，可以阅读下面2篇文章：

+ [Git使用简易指南](http://www.bootcss.com/p/git-guide/)
+ [Git官方文档](https://git-scm.com/doc)

## Markdown

Markdown是一种轻量级标记语言，允许人们“使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML(或者HTML)文档”。在我看来， HTML 已经很容易写了。Markdown 的理念是，能让文档更容易读、写和随意改。HTML 是一种发布的格式，Markdown 是一种书写的格式。就这样，Markdown 的格式语法只涵盖纯文本可以涵盖的范围。

关于Markdown的语法，可以阅读下面2篇文章：

+ [献给写作者的 Markdown 新手指南](http://www.jianshu.com/p/q81RER)
    - 此文介绍了Markdown的常用语法，并给出示例及其效果。<font color='red'>（作为快速入门用，读完不用10分钟）</font>
+ [Markdown 编辑阅读器 Demo](https://www.zybuluo.com/mdeditor?url=https%3A%2F%2Fwww.zybuluo.com%2Fstatic%2Feditor%2Fmd-help.markdown)
    - 此文介绍了Markdown的常用语法，并有demo可以直接看到效果。
+ [Markdown 语法说明 (简体中文版)](http://wowubuntu.com/markdown/)
    - 详细的介绍Markdown语法，给了示例但没有给出效果。

在Markdown中可以使用Mathjax，对Mathjax的介绍请见下文。

## Mathjax

[MathJax](http://www.mathjax.org/)是一款运行在浏览器中的开源的数学符号渲染引擎，使用MathJax可以方便的在浏览器中显示数学公式，不需要使用图片。目前，MathJax可以解析Latex、MathML和ASCIIMathML的标记语言。MathJax项目于2009年开始，发起人有American Mathematical Society, Design Science等，已被多家知名网站使用，这些网站有arXiv, Elsevier ScienceDirect, MathOverflow, Wikipedia等。更详细的介绍可以查看[MathJax](https://en.wikipedia.org/wiki/MathJax)的维基词条。

有三种方法获取MathJax：最简单的方法就是使用分布式网络服务中的MathJax的副本，它位于cdn.mathjax.org，但是你也可以下载并安装一个MathJax的副本到你的服务器,或者使用在你本地硬盘的副本（这样是不需要使用网络）。关于获取办法以及如何使用等详细内容，可以阅读在官网提供的文档(文档版本2.6)([https://docs.mathjax.org/en/v2.6-latest/index.html](https://docs.mathjax.org/en/v2.6-latest/index.html))或者翻译成中文的文档(文档版本2.0)([https://mathjax-chinese-doc.readthedocs.org/en/latest/start.html](https://mathjax-chinese-doc.readthedocs.org/en/latest/start.html))。

如果采用的是使用分布式网络服务中的MathJax的副本，那么只需要关注Mathjax的语法。如果觉得官方文档太厚实，可以看看下面这些文章对其介绍：

+ 中文
  - [MathJax 快速参考](http://colobu.com/2014/08/17/MathJax-quick-reference/)
  - [Markdown输入数学公式](http://oiltang.com/2014/05/04/markdown-and-mathjax/)
+ 英文
  - [TEX Commands available in MathJax](http://www.onemathematicalcat.org/MathJaxDocumentation/TeXSyntax.htm)
    + 非常详细的语法整理，在一个网页里列举了绝大部分的语法及其示例
  - [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
