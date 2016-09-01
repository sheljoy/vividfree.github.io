---
layout: post
title: EM算法原理及其应用
category: 机器学习
tagline: 
tags: [EM, "expectation maximum", 期望最大化, MLE, MAP, kMeans, GMM]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

EM算法是一种优化算法框架，用于含有 隐变量（hidden variable）的概率模型参数的极大似然估计（Maximum Likelihood Estimation, MLE），或极大后验概率估计（Maximum A Posterior estimation, MAP）。

EM算法简约而不简单，是一个经典的机器学习算法框架，在很多机器学习模型中都有应用。笔者在阅读了一些相关资料后梳理了一份slides，大家可以在 <a href='://yunpan.cn/cMtDRgpRHwzvj'>云盘共享地址</a> （提取码：bdda）下载到，欢迎大家一起探讨。

主要参考文献
+ Christopher M. Bishop. 《Pattern Recognition and Machine Learning》
+ 李航. 《统计学习方法》

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
