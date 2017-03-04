---
layout: post
title: 图像处理基本概念——卷积、滤波、平滑
category: 图像处理
tagline: 
tags: [图像处理, 卷积, 滤波]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

前两天听了360人工智能研究院组织的一次关于图像模糊处理技术的分享，收获很多，大致了解了这块的常用技术，及其在相机美颜功能上的应用。之前一直觉得图像卷积、图像滤波和图像平滑之间有些区别和联系，但是没好好理清楚，这两天查了一些相关资料，算是有了基本的了解。

滤波器 ([维基百科词条](https://zh.wikipedia.org/wiki/%E7%94%B5%E5%AD%90%E6%BB%A4%E6%B3%A2%E5%99%A8)) ，是信号处理中的一个概念，是用于去除信号中不想要的成分或者增强所需成分。其中较常听到的有低通滤波器 ([维基百科词条](https://zh.wikipedia.org/wiki/%E4%BD%8E%E9%80%9A%E6%BB%A4%E6%B3%A2%E5%99%A8)) 和高通滤波器 ([维基百科词条](https://zh.wikipedia.org/wiki/%E9%AB%98%E9%80%9A%E6%BB%A4%E6%B3%A2%E5%99%A8)) 。简单来讲，低通滤波器容许低频信号通过，高通滤波器容许高频信号通过。这两个概念都有一些不同的表达术语，对低通滤波器，在图像处理里，就对应到边缘平滑、图像模糊，在时序预测里可以对应到平滑（比如各种moving average算法）。对高通滤波器，在图像处理里，就对应到边缘提取与边缘增强。

可见图像平滑实际就是一种图像的低通滤波，那卷积跟滤波有啥关系呢？卷积是一种数学方法，用在图像处理里，不但可以做滤波，还可以实现其他目的。可以看这几篇文章有个大致了解：
1. [图像处理基本概念——卷积、滤波、平滑](http://blog.csdn.net/yangtrees/article/details/8740933)
2. 图像滤波 [中文](http://blog.csdn.net/zouxy09/article/details/49080029)，[英文](http://lodev.org/cgtutor/filtering.html)

在文章的最后，补充2种常用的图像滤波器的介绍
1. 高斯滤波
  + [高斯模糊的算法](http://www.ruanyifeng.com/blog/2012/11/gaussian_blur.html)
  + [高斯模糊 维基百科词条](https://zh.wikipedia.org/wiki/%E9%AB%98%E6%96%AF%E6%A8%A1%E7%B3%8A)
2. 双边滤波
  + [双边滤波](http://blog.csdn.net/abcjennifer/article/details/7616663)
    - 保边去噪的滤波器。相比高斯滤波仅考虑像素在空间距离上的关系，双边滤波的改进就在于在采样时不仅考虑像素在空间距离上的关系，同时加入了像素间的相似程度考虑，因而可以保持原始图像的大体分块进而保持边缘。


* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
