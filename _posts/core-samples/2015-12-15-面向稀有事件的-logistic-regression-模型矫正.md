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

经常会碰到一些二分类问题，其中正样本的比例很小，比如发生战争的概率，染上某种不常见疾病的概率等。在互联网领域，搜索业务、个性化推荐业务和广告投放业务都会碰到正样本比例很小的问题，那就是点击率预估。某些形态的广告投放点击率在万分位到千分位之间，比如说为千分之一，这就是说投放出1000次广告，才有1次点击。

正样本比例很小，在一些文献中会成为样本倾斜，在另一些文献中会称正类代表的事件为稀有事件。

## 参考文献

[1] [Logistic Regression](https://en.wikipedia.org/wiki/Logistic_regression) (来自Wikipedia)

[2] [Max Entropy](https://en.wikipedia.org/wiki/Maximum_entropy_probability_distribution) (来自Wikipedia)

[3] [Softmax Regression 或者 Multinomial Logistic Regression](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) (来自Wikipedia)
