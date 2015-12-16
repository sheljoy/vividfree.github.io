---
layout: post
category : 机器学习
tagline: 
tags : ["logistic regression", LR, 逻辑回归, "rare event", 稀有事件, intercept, 截距]
---
{% include JB/setup %}

## 1. 引言

无论在学术界，还是在工业界，Logistic Regression(LR, 逻辑回归)模型[1]是常用的分类模型，被用于各种分类场景和点击率预估问题等，它也是Max Entropy(ME, 最大熵)模型[2]，或者说Softmax Regression模型[3]，在二分类的一种特例。

用\\(X\ =\ (x_1, x_2, ..., x_k)\\)表示*k*维样本，用\\(\mathbf{\beta} = (\beta_0, \beta_1, \beta_2, ..., \beta_k)\\)表示*k+1*维模型变量，其中\\(\beta_0\\)表示截距项，那么LR模型的model function如下表示：

\begin{equation}\mathbf{f}(z) = \frac 1{1 + e^{-z}}\end{equation}

\begin{equation}z = \beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k\end{equation}

说明：公式1的学名为logistic function。

对分类问题的研究大部分是在样本分布均衡的情况下开展的。比如对二分类，一般研究正样本和负样本的数量相当（比如各占50%）或者相差不是那么大（比如一类样本占30%，另一类样本占70%）。但在实际应用时，经常会碰到这样样本倾斜问题，对于二分类而言，就会是某类的样本比例远小于另一类的样本比例。在学术界，一般称样本少的那类为正类，称正类代表的事件为稀有事件。稀有事件的例子并不少，比如发生战争的概率，染上某种不常见疾病的概率，磁盘出现故障的概率，网络传输数据丢失的概率等。在互联网领域，搜索业务、个性化推荐业务和广告定向投放业务都会碰到一个正样本比例远小于负样本比例的例子，那就是点击率预估。很多内容或者广告的点击率在万分位到千分位之间，存在点击的内容是正样本，未被点击的内容是负样本。比如说某广告的点击率为千分之一，这就是说平均投放出1000次广告，才有1次点击，剩下的都是未点击。

LR模型经过参数训练，最终得到的是分类超平面。

如果对稀有事件的使用通常的LR模型进行训练，那么会造成

文献[4]的第5节和文献[5]的第13.5.3节对此问题都进行了描述。


介绍稀有事件是常见的，直接用LR模型会碰到什么问题，有哪几种矫正方案呢，适合什么场景呢。Google和FB是怎么做的。

## 参考文献

[1] [Logistic Regression](https://en.wikipedia.org/wiki/Logistic_regression) (来自Wikipedia)

[2] [Max Entropy](https://en.wikipedia.org/wiki/Maximum_entropy_probability_distribution) (来自Wikipedia)

[3] [Softmax Regression 或者 Multinomial Logistic Regression](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) (来自Wikipedia)

[4] Gary King, Langche Zeng. Logistic Regression in Rare Events Data. Political Methodology. 2002

[5] 刘鹏, 王超. 计算广告. 2015

[6] H. Brendan McMahan, et al. Ad Click Prediction: a View from the Trenches. KDD2013

[7] Xinran He, et al. Practical Lessons from Predicting Clicks on Ads at Facebook. ADKDD2014
