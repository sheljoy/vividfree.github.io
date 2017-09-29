---
layout: post
title: 博客文章索引
category:
tagline: 
tags:
theme :
  name : bootstrap-3
---
{% include JB/setup %}

不同于导航栏上设置的“分类”、“标签”、“Google站内搜索”等入口，本文章主要从技术方向上对若干篇博文（非全部的博文）进行知识索引，以帮助形成一种知识框架。

## 机器学习

+ 模型
  - [EM算法原理及其应用](http://vividfree.github.io/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/2016/08/19/introduction-about-EM-algorithm) : EM算法是经典算法之一。
  - [理解 product quantization 算法](http://vividfree.github.io/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/2017/08/05/understanding-product-quantization) : Product quantization算法（简称PQ算法）可以用在神经网络模型压缩上，也可以用于相似搜索。它的效果和性能都较好。
+ 优化方法
  - [理解 FTRL 算法](http://vividfree.github.io/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/2015/12/05/understanding-FTRL-algorithm) : 对于特征规模大（达到千万级甚至数亿级）、标注数据量大或者是标注数据源源不断的流入（比如线上广告点击数据），FTRL算法在模型的效果和稀疏性方面都表现较好。
+ 评估指标
  - [理解 ROC 和 AUC](http://vividfree.github.io/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/2015/11/20/understanding-ROC-and-AUC) : 介绍了AUC的物理含义以及3种计算AUC的方法。
+ 模型校准
  - 某些业务需要做模型校准。比如广告投放系统以eCPM为排序指标，该指标是CTR和bid price的乘积。如果CTR预测得不准，会影响eCPM的排序结果。
  - [面向稀有事件的 Logistic Regression 模型校准](http://vividfree.github.io/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/2015/12/15/model-calibration-for-logistic-regression-in-rare-events-data)
  - [使用 Isotonic Regression 校准分类器](http://vividfree.github.io/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0/2015/12/21/classifier-calibration-with-isotonic-regression)
+ 矩阵相乘
  - [使用 MapReduce 实现大规模稀疏矩阵相乘](http://vividfree.github.io/%E5%A4%A7%E8%A7%84%E6%A8%A1%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86/2015/11/14/large-scale-matrix-multiplication-using-mapreduce) : 在实际业务中经常碰到2个大规模稀疏矩阵相乘的需求，这篇文章列举了一些例子，并先后介绍了稠密矩阵相乘和稀疏矩阵相乘的算法，其中详细描述了算法的复杂度。此外，对大规模稀疏矩阵相乘，还介绍了一些工程方面的trick。

## 计算广告

+ 基于深度学习的CTR预估
  - [201704 阅读笔记](http://vividfree.github.io/%E9%98%85%E8%AF%BB%E7%AC%94%E8%AE%B0/2017/04/26/201704-reading-list) : 介绍在FM模型基础上发展出的FNN和PNN这种基于深度学习的CTR预估模型。

## 自然语言处理

+ 机器翻译
  - [201706 阅读笔记](http://vividfree.github.io/%E9%98%85%E8%AF%BB%E7%AC%94%E8%AE%B0/2017/06/24/201706-reading-list) : 第二节"Machine Translation"，主要介绍《Attention Is All You Need》文章的阅读笔记。
  - [201703 阅读笔记](http://vividfree.github.io/%E9%98%85%E8%AF%BB%E7%AC%94%E8%AE%B0/2017/03/14/201703-reading-list) : 第一节"序列到序列模型"，主要介绍《Neural Machine Translation and Sequence-to-sequence Models: A Tutorial》文章的阅读笔记。
  - [201702 阅读笔记](http://vividfree.github.io/%E9%98%85%E8%AF%BB%E7%AC%94%E8%AE%B0/2017/02/05/201702-reading-list) : 第二节"Machine Translation"，主要介绍Google在16年发表的2篇paper《Google’s Neural Machine Translation System: Bridging the Gap between Human and Machine Translation》和《Google’s Multilingual Neural Machine Translation System: Enabling Zero-Shot Translation》的阅读笔记。
+ 文本匹配
  - [201707 阅读笔记](http://vividfree.github.io/%E9%98%85%E8%AF%BB%E7%AC%94%E8%AE%B0/2017/07/01/201707-reading-list) : 第二节"基于深度学习的文本匹配"，基于若干篇综述文章，介绍了DSSM模型及其变种。

## 个人思考

上面列举的是对技术的理解或者笔记，此外，平时还喜欢琢磨技术的特点和发展趋势，写了些个人思考（不一定对，欢迎拍砖）：
+ [对在NLP领域对比MLP、CNN和RNN的一点思考](http://vividfree.github.io/%E4%B8%AA%E4%BA%BA%E6%80%9D%E8%80%83/2017/07/08/some-viewpoint-about-comparison-of-mlp-cnn-rnn-in-nlp)
+ [对国内互联网趋势的一点思考](http://vividfree.github.io/%E4%B8%AA%E4%BA%BA%E6%80%9D%E8%80%83/2017/06/04/some-viewpoint-about-trends-of-chinese-internet)
+ [对深度学习的一点思考](http://vividfree.github.io/%E4%B8%AA%E4%BA%BA%E6%80%9D%E8%80%83/2017/03/13/some-viewpoint-about-deep-learning)
+ [对软件开发的一点思考](http://vividfree.github.io/%E4%B8%AA%E4%BA%BA%E6%80%9D%E8%80%83/2016/01/17/some-viewpoint-about-software-development) : 算法工程师不仅要熟悉业务特点，并找到合适的算法策略，也要重视工程开发。人工智能技术的落地 = 业务理解 + 数据使用 + 工程开发 + 模型建立。

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
