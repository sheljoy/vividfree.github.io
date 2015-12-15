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

Odds ratio可谓是LR模型的细节，但它对于理解LR模型有很好的帮助。下文先介绍odds和log of odds，然后用odds ratio来解释LR模型的参数含义。

## 从概率到odds再到log of odds

"Everything starts with the concept of probability." 假设某随机事件发生的概率是0.8，那么该事件不发生的概率为1 - 0.8 = 0.2。事件发生的odds定义成发生的概率除以不发生的概率，对这个例子即为 0.8 / 0.2 = 4。用数学式子形式化表示odds，就是\\(\frac p{1 - p} \\)。为下文表述方便，用函数\\(odds(p)\\)表示如下：

\begin{equation}odds(p) = \frac p{1 - p}\end{equation}

易见函数odds(p)是关于*p*的递增函数。

对odds取对数(成为log of odds)，也就是\\(log\frac p{1 - p}\\)，这个在正式的数学文献中会记为\\(logit(p)\\)，但为了下文表述方便，用函数\\(log\\_of\\_odds(p)\\)表示如下：

\begin{equation}log\\_of\\_odds(p) = log(\frac p{1 - p})\end{equation}

易见函数log_of_odds(p)还是关于*p*的递增函数。

对于LR模型而言，LR模型的输出值是概率，介于0到1之间。容易推导出LR模型对应的\\(odds(p)\\)和\\(log\\_of\\_odds(p)\\)的函数表达形式，分别见公式5和公式6，其中公式6恰好就是公式2中的z：

\begin{equation}odds(p) = e^{\beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k}\end{equation}

\begin{equation}log\\_of\\_odds(p) = \beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k\end{equation}

## odds ratio

这节基于上节介绍的odds和log of odds的概念，应用odds ratio来解释LR模型的参数含义。顾名思义，odds ratio是2个odds相除的结果，只不过这2个odds怎么得出是需要看分析哪个LR模型参数，或者说分析哪个分析场景。2个odds的除法取log，可以转换成log_of_odds的减法。文章[4], [5]是两份非常好的资料，读者可以详细阅读。文章[4]中给了一个数据集，对这个数据集做了5组特征的实验。这些实验很有代表性，就用它们来阐述odds ratio与LR模型参数之间的关系。

第1个实验：k = 0，即LR模型不用任何特征，只留下截距项，通过参数训练得到的模型为

\begin{equation}log\\_of\\_odds(p) = log(\frac p{1 - p}) = -1.12546\end{equation}

公式7中的p表示什么概率呢？容易分析出它表示的正是正样本个数占全部样本个数的比例（或者说概率）。可以这样验证，数据集中正样本的比例为\\(\frac {49}{200} = 0.245\\)，\\(log\frac {0.245}{1-0.245} = -1.12546\\)。

第2个实验：LR模型只带一个二值特征（是否为女性），通过参数训练得到的模型为

\begin{equation}log\\_of\\_odds(p) = log(\frac p{1 - p}) = -1.470852 + 0.5927822 * \mathbf{female}\end{equation}

公式8中的


模型选择的越好，截距项会越小。这点要解释下。

另外，截距项并不是说要跟正样本的比例相关，得看怎么建模的。

## 补充说明

TODO
说明一些情况下讨论截距是没有意义

## 参考文献

[1] [Logistic Regression](https://en.wikipedia.org/wiki/Logistic_regression) (来自Wikipedia)

[2] [Max Entropy](https://en.wikipedia.org/wiki/Maximum_entropy_probability_distribution) (来自Wikipedia)

[3] [Softmax Regression 或者 Multinomial Logistic Regression](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) (来自Wikipedia)

[4] [How do I interpret odds ratios in logistic regression](http://www.ats.ucla.edu/stat/mult_pkg/faq/general/odds_ratio.htm) (来自UCLA的一份资料)

[5] [Interpreting logistic regression models](http://www-hsc.usc.edu/~eckel/biostat2/notes/notes14.pdf) (来自USC的一份资料)

[6] [Regression Analysis: How to Interpret the Constant (Y Intercept)](http://blog.minitab.com/blog/adventures-in-statistics/regression-analysis-how-to-interpret-the-constant-y-intercept)
