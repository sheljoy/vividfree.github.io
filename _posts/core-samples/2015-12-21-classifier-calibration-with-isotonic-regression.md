---
layout: post
title: 使用 Isotonic Regression 校准分类器
category: 机器学习
tagline: 
tags: ["platt scaling", "isotonic regression", 保序回归, "calibration", 校准]
---
{% include JB/setup %}

## 1. 引言

在上一篇博文《面向稀有事件的 Logistic Regression 模型校准》中介绍了稀有事件下LR模型的校准方法。这篇文章讨论普适情况下的模型校准(model calibration)[1]，理论上讲，应用这类模型校准方法与使用哪种模型没有关系，这些方法针对模型输出和真实输出先离线建立其校准模型，然后在线上实时应用。

d

## 2. 校准方法

对分类模型的校准主要有2种方法：Platt scaling[2] 和 Isotonic regression[3]。论文[4]很好的对比和总结了这2种方法。Platt scaling适用于样本量少的情形，而Isotonic regression适用于样本量多的情形。样本量少时，使用Isotonic regression容易过拟合。需要注意一点，无论是对Platt scaling方法还是Isotonic regression方法，为了得到一个有效的校准模型，需要用一个独立于训练集的验证集，否则会引入偏差。下面2段分别摘自论文[4]的2.1节和2.2节。

> If we use the same data set that was used to train the model we want to calibrate, we introduce unwanted bias. For example, if the model learns to discriminate the train set perfectly and orders all the negative examples before the positive examples, then the sigmoid transformation will output just a 0,1 function. So we need to use an independent calibration set in order to get good posterior probabilities. This, however, is not a draw back, since the same set can be used for model and parameter selection.

> As in the case of Platt calibration, if we use the model training set \\((x_i, y_i)\\) to get the training set \\((f(x_i), y_i)\\) for Isotonic Regression, we introduce unwanted bias. So we use an independent validation set to train the isotonic function.

在很多互联网业务上，比如广告定向投放，经常碰到样本量大的情况，所以下文将围绕适用于大样本量的Isotonic regression来介绍模型校准方法。

## 3. Isotonic regression

Isotonic regression，中文名保序回归，下文简写为IR。

这是一种非参回归模型(nonparametric regression)


## 3. 在广告排序中的应用

Google和Microsoft在论文中提到用保序回归来做模型校准，介绍在广告中的具体用法

## 4. 其他

其他参考文献可以看文章[9]

## 参考文献

[1] [Calibration (statistics)](https://en.wikipedia.org/wiki/Calibration_(statistics)) (来自Wikipedia)

[2] [Classifier calibration with Platt scaling and isotonic regression](http://fastml.com/classifier-calibration-with-platts-scaling-and-isotonic-regression/)

[2] [Isotonic regression](https://en.wikipedia.org/wiki/Isotonic_regression) (来自Wikipedia)

[3] [Platt scaling](https://en.wikipedia.org/wiki/Platt_scaling) (来自Wikipedia)

[4] Alexandru Niculescu-Mizil, et al. Predicting Good Probabilities With Supervised Learning. ICML2005





[3] [Speeding up isotonic regression in scikit-learn by 5,000x](http://tullo.ch/articles/speeding-up-isotonic-regression/)

[4] [Isotonic Regression](http://fa.bianp.net/blog/2013/isotonic-regression/)

[9] Ronny Luss, et al. Efficient regularized isotonic regression with application to gene--gene interaction search. The Annals of Applied Statistics. 2012

[11] H. Brendan McMahan, et al. Ad Click Prediction: a View from the Trenches. KDD2013

[12] Thore graepel, et al. Web-Scale Bayesian Click-Through Rate Prediction for Sponsored Search Advertising in Microsoft’s Bing Search Engine. ICML2010

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
