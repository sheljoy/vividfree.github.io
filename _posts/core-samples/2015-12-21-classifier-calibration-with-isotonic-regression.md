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

+ 模型假设与实际数据分布并不相符。比如：Naive Bayes模型的条件独立性假设，在实际业务中，经常看到Naive Bayes模型输出的概率会特别接近0或者1，容易看出这并不是\\(P(Y=c\|X)\\)的有效估计。

+ 一些有效的特征没有被加入到模型中

+ 训练算法存在不足，收敛得到的解并不是对业务而言的最优解

估计出的概率存在偏差是常见的，但是否需要校准则需要看需求。当只需要按照分数来做排序时，就可以不用校准模型；但有些场景则需要准确的概率\\(P(Y=c\|X)\\)，那么就需要校准。这样的场景有：

+ 拒绝借贷的概率预估：一些银行或者P2P公司会建立机器学习模型来估计拒绝借贷的概率，通过设置阈值以自动过滤一批借贷请求。这需要准确的概率。

+ 广告点击率预估：第一点，一般会设置CTR的最低阈值，低于这个阈值的广告就不会被展示，以此保证用户体验；第二点，点击率估计准的，方便调试以\\(ctr^\alpha \times bid\\)为核心的ecpm计算策略。这些需要准确的概率。

在上一篇博文《面向稀有事件的 Logistic Regression 模型校准》中介绍了稀有事件下LR模型的校准方法，而这篇文章将讨论普适情况下的模型校准(model calibration)[1]。理论上讲，应用这类模型校准方法与使用哪种模型没有关系，这些方法针对模型输出和真实输出先离线建立其校准模型，然后在线上实时应用。

下文主要围绕二分类来介绍模型校准方法，并在最后一节中介绍多分类的模型校准。

## 2. 校准方法

首先引入**reliability diagram**，这是一种相对简单而且常用的可视化方法，用它能大致评估出当前模型的输出结果与真实结果有多大偏差。如论文[2]的下面这段介绍，如果能得到斜率为45度的线，那么意味着模型输出的结果是有效的估计。

> On real problems where the true conditional probabilities are not known, model calibration can be visualized with reliability diagrams (DeGroot & Fienberg, 1982). First, the prediction space is discretized into ten bins. Cases with predicted value between 0 and 0.1 fall in the first bin, between 0.1 and 0.2 in the second bin, etc.
For each bin, the mean predicted value is plotted against the true fraction of positive cases. If the model is well calibrated the points will fall near the diagonal line.

对分类模型的校准主要有2种方法：Platt scaling[3] 和 Isotonic regression[4]。Platt scaling使用LR模型对模型输出的值做拟合（并不是对reliability diagram中的数据做拟合），适用于样本量少的情形。Isotonic regression则是对reliability diagram中的数据做拟合，适用于样本量多的情形。样本量少时，使用Isotonic regression容易过拟合。需要注意一点，无论是对Platt scaling方法还是Isotonic regression方法，为了得到一个有效的校准模型，需要用一个独立于训练集的验证集，否则会引入偏差。可以查阅论文[2]，该文对这2种方法做了很好的对比分析。

在很多互联网业务上，比如广告定向投放，经常碰到样本量大的情况，所以下节将围绕适用于大样本量的Isotonic regression来介绍模型校准方法。

## 3. Isotonic regression及其在广告排序中的应用

Isotonic regression，中文翻译为保序回归，是一种非参回归模型(nonparametric regression)。这种方法只有一个约束条件即，函数空间为单调递增函数的空间。基于reliability diagram，给定模型预测的分数\\(f_i\\)，真实的分数\\(y_i\\)，Isotonic regression的模型公式为：

\begin{equation}y_i = m(f_i) + \epsilon\end{equation}

其中，\\(m\\)表示保序函数（单调递增函数）。所以isotonic regression的目标函数为

\begin{equation}\hat m = argmin_z \sum (y_i - z(f_i))^2\end{equation}

Isotonic Regression的一种求解算法是pool adjacent violators algorithm (简称PAVA, PAV算法)，时间复杂度为\\(O(N)\\)，算法流程并不复杂，详细内容可以查阅文章[2]，另外文章[5]有该算法的动态效果图。PAV算法也是scikit-learn中isotonic regression库的求解算法。

论文[6][7]分别显示出Google和Microsoft在CTR预估模型的校准上用到保序回归。应用保序回归到CTR预估模型的校准上的流程大致有这样几步：

1. 准备一份验证集（不同于用于训练CTR预估模型的训练集）用于训练保序回归模型。这份验证集的每个样本仍然是展示点击信息。

2. 将[0, 1]区间划分为N个桶，每个桶的长度相同，比如\\(N=10^5\\)或者\\(N=10^6\\)。

3. 用之前训好的CTR预估模型在此验证集上进行预测，给出每个样本的点击率估计值，基于这些点击率估计值，将验证集中的样本落入对应的桶中。

4. 对每个桶，基于展示点击信息，计算落入样本的真实点击率。比如桶表示的区间为\\(1 \times [10^{-5}, 2 \times 10^{-5})\\)，取平均值为\\(1.5 \times 10^{-5}\\)，这个桶的真实点击率为\\(10^{-6}\\)，这样这个桶就得到reliability diagram图的一个点\\((1.5 \times 10^{-5}, 10^{-6})\\)，全部N个桶就构成了reliability diagram。

5. 对上步生成的reliability diagram中的数据运行isotonic regression（这个数据量不大，\\(N=10^6\\)的数据大小也就几M空间，scikit-learn工具包完全可以胜任）

上述流程最终产出校准用的映射表，在线上加载这个映射表实时应用，比如在线上预估出的CTR值为x，查校准用的映射表，判断x所在的桶，取得校准映射到的值。

数值区间。前一篇博客。

## 4. 其他

多分类下的模型校准
英文文章[12]介绍了啥
或者搜索"isotonic regression for multiple independent variables"相关的文章，比如[10][11]，或者wikipedia

关于 Platt scaling 和 Isotonic regression，一些英文文章有不错的介绍，比如[12][13][14][15]，这些都值得阅读。

## 参考文献

[1] [Calibration (statistics)](https://en.wikipedia.org/wiki/Calibration_(statistics)) (来自Wikipedia)

[2] Alexandru Niculescu-Mizil, et al. Predicting Good Probabilities With Supervised Learning. ICML2005

[3] [Isotonic regression](https://en.wikipedia.org/wiki/Isotonic_regression) (来自Wikipedia)

[4] [Platt scaling](https://en.wikipedia.org/wiki/Platt_scaling) (来自Wikipedia)

[5] [Isotonic Regression](http://fa.bianp.net/blog/2013/isotonic-regression/)

[6] H. Brendan McMahan, et al. Ad Click Prediction: a View from the Trenches. KDD2013

[7] Thore graepel, et al. Web-Scale Bayesian Click-Through Rate Prediction for Sponsored Search Advertising in Microsoft’s Bing Search Engine. ICML2010


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
