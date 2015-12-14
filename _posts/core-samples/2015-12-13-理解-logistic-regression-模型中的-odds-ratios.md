---
layout: post
category : 机器学习
tagline: 
tags : ["logistic regression", LR, odds, intercept, 逻辑回归, 截距]
---
{% include JB/setup %}

## 引言

无论在学术界，还是在工业界，Logistic Regression(LR, 逻辑回归)模型[1]是常用的分类模型，被用于各种分类场景和点击率预估问题等，它也是Max Entropy(ME, 最大熵)模型[2]，或者说Softmax Regression模型[3]，在二分类的一种特例。

LR模型的model function如下

\begin{equation}\mathbf{f}(z) = frac 1{1 + e^{-z}}\end{equation}

\begin{equation}\mathbf{f}(x, y) = \displaystyle\sum_{i=0}^{n-1} {\mathbf{A}\_{x,\ i} \times \mathbf{B}\_{i,\ y}}\end{equation}


Odds ratio可谓是LR模型的细节，但它对于理解LR模型有很好的帮助。

## 从概率到log of odds


## odds ratio


## 截距(intercept)

说明 不同的建模下，截距是有区别的

## 其他

说明一些情况下讨论截距是没有意义

## 参考文献

[1] [Logistic Regression](https://en.wikipedia.org/wiki/Logistic_regression) (来自Wikipedia)

[2] [Max Entropy](https://en.wikipedia.org/wiki/Maximum_entropy_probability_distribution) (来自Wikipedia)

[3] [Softmax Regression \| Multinomial Logistic Regression](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) (来自Wikipedia)

[4] [How do I interpret odds ratios in logistic regression](http://www.ats.ucla.edu/stat/mult_pkg/faq/general/odds_ratio.htm) (来自UCLA的一份资料)

[5] [Interpreting logistic regression models](http://www-hsc.usc.edu/~eckel/biostat2/notes/notes14.pdf) (来自USC的一份资料)

[6] [Regression Analysis: How to Interpret the Constant (Y Intercept)](http://blog.minitab.com/blog/adventures-in-statistics/regression-analysis-how-to-interpret-the-constant-y-intercept)
