---
layout: post
title: 使用 Isotonic Regression 校准分类器
category: 机器学习
tagline: 
tags: ["platt scaling", "isotonic regression", 保序回归, "calibration", 校准]
---
{% include JB/setup %}

## 1. 引言

对有监督机器学习问题，通常的训练流程包括这样几步：先建立起模型，然后在训练集上训练模型，如果有超参数，还需要在验证集上应用交叉验证以确定超参数，总之最终会得到一个模型。在这样的流程下，不断优化模型，如果在测试集上取得了较高的准确率、召回率、F-score或者AUC后，那事情就结束了，模型的输出结果是符合需要的吗？这并不一定。

当给定一个样本，大部分分类器能够输出该样本属于某类的分数，通常这个分数介于0到1之间，我们称之为概率，严格来讲，是后验概率，数学上表示为\\(P(Y=c\|X)\\)，\\(X\\)表示样本，\\(Y=1\\)表示样本属于类c。但是模型输出的概率经常与样本属于类c的真实概率有偏差。比如输出概率为20%，并不表示真实概率也是20%。模型估计出的概率存在偏差有这样几个原因：

+ 模型假设与实际数据分布并不相符。比如：Naive Bayes模型的条件独立性假设，在实际业务中，经常看到Naive Bayes模型输出的概率会特别接近0或者1，这个不是\\(P(Y=c\|X)\\)的有效估计。

+ 一些有效的特征没有被加入到模型中

+ 训练算法存在不足，收敛得到的解并不是对业务而言的最优解

估计出的概率存在偏差是常见的，但是否需要校准则需要看需求。当只需要按照分数来做排序时，就可以不用校准模型；但有些场景则需要准确的概率\\(P(Y=c\|X)\\)，那么就需要校准。这样的场景有：

+ 拒绝借贷的概率预估：一些银行或者P2P公司会建立机器学习模型来估计拒绝借贷的概率，通过设置阈值以自动过滤一批借贷请求。这需要准确的概率。

+ 广告点击率预估：第一点，一般会设置CTR的最低阈值，低于这个阈值的广告就不会被展示，以此保证用户体验；第二点，点击率估计准的，方便调试\\(CTR^\alpha \times bid\\)的ecpm计算策略。这些需要准确的概率。

在上一篇博文《面向稀有事件的 Logistic Regression 模型校准》中介绍了稀有事件下LR模型的校准方法，而这篇文章将讨论普适情况下的模型校准(model calibration)[1]。理论上讲，应用这类模型校准方法与使用哪种模型没有关系，这些方法针对模型输出和真实输出先离线建立其校准模型，然后在线上实时应用。

下文主要围绕二分类来介绍模型校准方法，并在最后一节中介绍多分类的模型校准。

## 2. 校准方法

对分类模型的校准主要有2种方法：Platt scaling[2] 和 Isotonic regression[3]。论文[4]很好的对比和总结了这2种方法。Platt scaling适用于样本量少的情形，而Isotonic regression适用于样本量多的情形。样本量少时，使用Isotonic regression容易过拟合。需要注意一点，无论是对Platt scaling方法还是Isotonic regression方法，为了得到一个有效的校准模型，需要用一个独立于训练集的验证集，否则会引入偏差。下面2段分别摘自论文[4]的2.1节和2.2节。

> If we use the same data set that was used to train the model we want to calibrate, we introduce unwanted bias. For example, if the model learns to discriminate the train set perfectly and orders all the negative examples before the positive examples, then the sigmoid transformation will output just a 0,1 function. So we need to use an independent calibration set in order to get good posterior probabilities. This, however, is not a draw back, since the same set can be used for model and parameter selection.

> As in the case of Platt calibration, if we use the model training set \\((x_i, y_i)\\) to get the training set \\((f(x_i), y_i)\\) for Isotonic Regression, we introduce unwanted bias. So we use an independent validation set to train the isotonic function.

在很多互联网业务上，比如广告定向投放，经常碰到样本量大的情况，所以下文将围绕适用于大样本量的Isotonic regression来介绍模型校准方法。

## 3. Isotonic regression

Isotonic regression，中文名保序回归，下文简写为IR。

这是一种非参回归模型(nonparametric regression)

文献[5][6]


## 3. 在广告排序中的应用

Google和Microsoft在论文中提到用保序回归来做模型校准，介绍在广告中的具体用法

文献[7][8]

## 4. 其他

多分类下的模型校准
英文文章[12]介绍了啥
或者搜索"isotonic regression for multiple independent variables"相关的文章，比如[10][11]

关于 Platt scaling 和 Isotonic regression，一些英文文章有不错的介绍，比如[12][13][14][15]，这些都值得阅读。

## 参考文献

[1] [Calibration (statistics)](https://en.wikipedia.org/wiki/Calibration_(statistics)) (来自Wikipedia)

[2] [Isotonic regression](https://en.wikipedia.org/wiki/Isotonic_regression) (来自Wikipedia)

[3] [Platt scaling](https://en.wikipedia.org/wiki/Platt_scaling) (来自Wikipedia)

[4] Alexandru Niculescu-Mizil, et al. Predicting Good Probabilities With Supervised Learning. ICML2005

[5] Ronny Luss, et al. Efficient regularized isotonic regression with application to gene--gene interaction search. The Annals of Applied Statistics. 2012

[6] [Isotonic Regression](http://fa.bianp.net/blog/2013/isotonic-regression/)

[7] H. Brendan McMahan, et al. Ad Click Prediction: a View from the Trenches. KDD2013

[8] Thore graepel, et al. Web-Scale Bayesian Click-Through Rate Prediction for Sponsored Search Advertising in Microsoft’s Bing Search Engine. ICML2010


[10] Adam Kalai, et al. The Isotron Algorithm: High-Dimensional Isotonic Regression.

[11] Quentin Stout. Isotonic Regression for Multiple Independent Variables.

[12] [Calibrating classifier probabilities](http://danielnee.com/tag/isotonic-regression/)

[13] [How is isotonic regression used in practice for calibration in machine learning](https://www.quora.com/How-is-isotonic-regression-used-in-practice-for-calibration-in-machine-learning)

[14] [Classifier calibration with Platt scaling and isotonic regression](http://fastml.com/classifier-calibration-with-platts-scaling-and-isotonic-regression/)

[15] [Speeding up isotonic regression in scikit-learn by 5,000x](http://tullo.ch/articles/speeding-up-isotonic-regression/)

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
