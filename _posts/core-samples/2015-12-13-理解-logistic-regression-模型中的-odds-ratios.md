---
layout: post
category : 机器学习
tagline: 
tags : ["logistic regression", LR, odds, intercept, 逻辑回归, 截距]
---
{% include JB/setup %}

## 引言

无论在学术界，还是在工业界，Logistic Regression(LR, 逻辑回归)模型[1]是常用的分类模型，被用于各种分类场景和点击率预估问题等，它也是Max Entropy(ME, 最大熵)模型[2]，或者说Softmax Regression模型[3]，在二分类的一种特例。

用\\(X\ =\ (x_1, x_2, ..., x_k)\\)表示*k*维样本，用\\(\mathbf{\beta} = (\beta_0, \beta_1, \beta_2, ..., \beta_k)\\)表示*k+1*维模型变量，其中\\(\beta_0\\)表示截距项，那么LR模型的model function如下表示：

\begin{equation}\mathbf{f}(z) = \frac 1{1 + e^{-z}}\end{equation}

\begin{equation}z = \beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k\end{equation}

说明：公式1的学名为logistic function。

Odds ratio可谓是LR模型的细节，但它对于理解LR模型有很好的帮助。下文将介绍odds ratio，并从odds ratio角度理解LR模型的参数。

## 从概率到odds再到log of odds

"Everything starts with the concept of probability." 假设某随机事件发生的概率是0.8，那么该事件不发生的概率为1 - 0.8 = 0.2。事件发生的odds定义成发生的概率除以不发生的概率，对这个例子即为 0.8 / 0.2 = 4。用数学式子形式化表示odds，就是\\(\frac p{1 - p} \\)，易见该式子是关于*p*的递增函数。对odds取对数(成为log of odds)，也就是\\(log\frac p{1 - p}\\)，记为 \\(logit(p)\\)，易见该式子还是关于*p*的递增函数。

对于LR模型而言，LR模型的输出值是概率，介于0到1之间。其\\(logit(p)\\)的表达式经过推导，可以很快得到下面这个式子（也就是公式2中的z）：

\begin{equation}logit(p) = \beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k\end{equation}


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
