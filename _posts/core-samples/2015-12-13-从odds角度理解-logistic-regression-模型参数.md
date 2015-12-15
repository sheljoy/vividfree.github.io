---
layout: post
category : 机器学习
tagline: 
tags : ["logistic regression", LR, odds, intercept, 逻辑回归, 截距]
---
{% include JB/setup %}

## 1. 引言

无论在学术界，还是在工业界，Logistic Regression(LR, 逻辑回归)模型[1]是常用的分类模型，被用于各种分类场景和点击率预估问题等，它也是Max Entropy(ME, 最大熵)模型[2]，或者说Softmax Regression模型[3]，在二分类的一种特例。

用\\(X\ =\ (x_1, x_2, ..., x_k)\\)表示*k*维样本，用\\(\mathbf{\beta} = (\beta_0, \beta_1, \beta_2, ..., \beta_k)\\)表示*k+1*维模型变量，其中\\(\beta_0\\)表示截距项，那么LR模型的model function如下表示：

\begin{equation}\mathbf{f}(z) = \frac 1{1 + e^{-z}}\end{equation}

\begin{equation}z = \beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k\end{equation}

说明：公式1的学名为logistic function。

下文将先介绍odds和log of odds，然后用odds来解释LR模型的参数含义。

## 2. 从概率到odds再到log of odds

在统计和概率理论中，一个事件的**发生比**（英语：Odds[4]）是该事件发生和不发生的比率。假设某随机事件发生的概率是0.8，那么该事件不发生的概率为1 - 0.8 = 0.2。事件发生的odds定义成发生的概率除以不发生的概率，对这个例子即为 0.8 / 0.2 = 4。用数学式子形式化表示odds，就是\\(\frac p{1 - p} \\)。为下文表述方便，用函数\\(odds(p)\\)表示如下：

\begin{equation}odds(p) = \frac p{1 - p}\end{equation}

易见函数odds(p)是关于*p*的递增函数。

对odds取对数(成为log of odds)，也就是\\(log\frac p{1 - p}\\)，这个在正式的数学文献中会记为\\(logit(p)\\)，即：

\begin{equation}logit(p) = log(\frac p{1 - p})\end{equation}

易见函数log_of_odds(p)还是关于*p*的递增函数。

当有2个概率\\(p_1\\)和\\(p_2\\)，将这2个概率的odd相除等价于将这2个概率的logit相减。

## 3. 从odds角度理解LR模型参数

对于LR模型而言，LR模型的输出值是概率，介于0到1之间。容易推导出LR模型对应的\\(odds(p)\\)和\\(logit(p)\\)的函数表达形式，分别见公式5和公式6，其中公式6恰好就是公式2中的z：

\begin{equation}odds(p) = e^{\beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k}\end{equation}

\begin{equation}logit(p) = \beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k\end{equation}

文章[5], [6]是两份解释LR模型参数的非常好的资料，读者可以详细阅读。文章[5]中给了一个数据集，针对这个数据集做了5组特征实验。这些实验很有代表性，笔者就用它们来阐述odds与LR模型参数之间的关系。

### 3.1 第1个实验

k = 0，即LR模型不用任何特征，只留下截距项，通过参数训练得到的模型为

\begin{equation}logit(p) = log(\frac p{1 - p}) = -1.12546\end{equation}

公式7中的p表示什么概率呢？容易分析出它表示的正是正样本个数占全部样本个数的比例（或者说概率）。可以这样验证，数据集中正样本的比例为\\(\frac {49}{200} = 0.245\\)，\\(log\frac {0.245}{1-0.245} = -1.12546\\)。在k = 0时，截距项恰好是正样本比例对应的log of odds。

### 3.2 第2个实验

LR模型只带一个二值特征（是否为女性），通过参数训练得到的模型为

\begin{equation}logit(p) = log(\frac p{1 - p}) = -1.470852 + 0.5927822 \times \mathbf{female}\end{equation}

公式8中的\\(\beta_0(-1.470852)\\)表示非女性（即男性）的正样本的log of odds。同样可以用数据验证，数据集中男性正样本比例为\\(\frac {17}{17+74}\\)，男性正样本的log of odds即为\\(log\frac {17}{74} = -1.47\\)。

公式8中的\\(\beta_1(0.5927822)\\)表示女性的正样本的log of odds 减去 男性的正样本的log of odds。因为

\begin{equation}\beta_1 = (-1.470852 + 0.5927822 \times 1) - (-1.470852 + 0.5927822 \times 0)\end{equation}

同样可以用数据验证，数据集中女性正样本的log of odds为\\(log\frac {32}{77} = -0.878\\)，男性正样本的log of odds为\\(log\frac {17}{74} = -1.471\\)。这两个log of odds相减即得0.593，正是\\(\beta_1\\)。

### 3.3 第3个实验

LR模型只带一个连续特征（数学成绩），通过参数训练得到的模型为

\begin{equation}logit(p) = log(\frac p{1 - p}) = -9.793942 + 0.1563404 \times \mathbf{math}\end{equation}

公式10中的\\(\beta_0(-9.793942)\\)按理应该表示数学成绩为0的正样本的log of odds。基于这点还原出数学成绩为0的正样本的概率为0.00005579，这是一个很小的数。但从数据集上看，没有一个人的数学成绩小于30。所以截距项在这里表示的是假想数学成绩为0的正样本的log of odds。

公式10中的\\(\beta_1(0.1563404)\\)表示数学成绩每提高1分，正样本的log of odds会提升多少，或者说在数学成绩这个维度，对log of odds进行差分。因为

\begin{equation}\beta_1 = (-9.793942 + 0.1563404 \times (score + 1)) - (-9.793942 + 0.1563404 \times score)\end{equation}

这是2个log of odds相减，等价于对odds ratio取log。更进一步，还原回到odds ratio，即exp(0.1563404) = 1.1692241。这个可以理解为数学成绩每提高1分，正样本的odds将提高17%。

### 3.4 第4个实验

LR模型带多个非组合的特征（数学成绩，是否为女性，阅读方面的成绩），通过参数训练得到的模型为

\begin{equation}logit(p) = log(\frac p{1 - p}) = -11.77025 + 0.1229589 \times \mathbf{math} + 0.979948 \times \mathbf{female} + 0.0590632 \times \mathbf{read}\end{equation}

对拟合出的公式12，female特征的系数表示：固定math和read的取值，女性正样本的odds除以男性正样本的odds的比值为exp(0.979948) = 2.66。math特征的稀疏表示：固定female和read的取值，数学成绩每提高1分，正样本的odds将提高13%，因为exp(0.1229589) = 1.13。

### 3.5 第5个实验

LR模型带组合特征（是否为女性，数学成绩和前两个特征的组合），通过参数训练得到的模型为

\begin{equation}logit(p) = log(\frac p{1 - p}) = -8.745841 - 2.899863 \times \mathbf{female} + 0.1293781 \times \mathbf{math} + 0.0669951 \times \mathbf{female} \times \mathbf{math}\end{equation}

因为存在\\(\mathbf{female} \times \mathbf{math}\\)一项特征，这样就不好直接讨论\\(\mathbf{female}\\)的效果。但可以做如下变换，一个关于男性的公式：

\begin{equation}logit(p) = log(\frac p{1 - p}) = -8.745841 + 0.1293781 \times \mathbf{math}\end{equation}

另一个关于女性的公式：

\begin{equation}logit(p) = log(\frac p{1 - p}) = -8.745841 - 2.899863 + 0.1293781 \times \mathbf{math} + 0.0669951 \times \mathbf{math} = -11.645704 + 0.1963732 \times \mathbf{math}\end{equation}

在公式14和公式15中就没有组合特征，那么就可以走类似于上面几组实验的分析思路，对于男性，数学成绩每提高1分，正样本的odds将提高14%（因为exp(0.1293781) = 1.14）。对于女性，数学成绩每提高1分，正样本的odds将提高22%（exp(0.1963732) = 1.22）。

## 4 总结

可以用odds ratio解释LR模型的参数。

模型选择的越好，截距项会越小。这点要解释下。

另外，截距项并不是说要跟正样本的比例相关，得看怎么建模的。

说明一些情况下讨论截距是没有意义

## 参考文献

[1] [Logistic Regression](https://en.wikipedia.org/wiki/Logistic_regression) (来自Wikipedia)

[2] [Max Entropy](https://en.wikipedia.org/wiki/Maximum_entropy_probability_distribution) (来自Wikipedia)

[3] [Softmax Regression 或者 Multinomial Logistic Regression](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) (来自Wikipedia)

[4] [Odds](https://en.wikipedia.org/wiki/Odds)（来自Wikipedia）

[5] [How do I interpret odds ratios in logistic regression](http://www.ats.ucla.edu/stat/mult_pkg/faq/general/odds_ratio.htm) (来自UCLA的一份资料)

[6] [Interpreting logistic regression models](http://www-hsc.usc.edu/~eckel/biostat2/notes/notes14.pdf) (来自USC的一份资料)

[7] [Regression Analysis: How to Interpret the Constant (Y Intercept)](http://blog.minitab.com/blog/adventures-in-statistics/regression-analysis-how-to-interpret-the-constant-y-intercept)
