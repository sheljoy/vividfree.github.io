---
layout: post
category : 机器学习
tagline: 
tags : ["logistic regression", LR, 逻辑回归, "rare event", 稀有事件, intercept, 截距]
---
{% include JB/setup %}

## 1. 引言

对分类问题的研究大部分是在样本分布均衡的情况下开展的。比如对二分类，一般研究正样本和负样本的数量相当（比如各占50%）或者相差不是那么大（比如一类样本占30%，另一类样本占70%）。但在实际应用时，经常会碰到这样样本倾斜问题，对于二分类而言，就会是某类的样本比例远小于另一类的样本比例。在学术界，一般称样本少的那类为正类，称正类代表的事件为稀有事件。稀有事件的例子并不少，比如发生战争的概率，染上某种不常见疾病的概率，磁盘出现故障的概率，网络传输数据丢失的概率等。在互联网领域，搜索业务、个性化推荐业务和广告定向投放业务都会碰到一个正样本比例远小于负样本比例的例子，那就是点击率预估。很多内容或者广告的点击率在万分位到千分位之间，存在点击的内容或者广告是正样本，未被点击的内容或者广告是负样本。比如说某广告的点击率为千分之一，这就是说平均投放出1000次广告，才有1次点击，剩下的都是未点击。

无论在学术界，还是在工业界，Logistic Regression(LR, 逻辑回归)模型[1]是常用的分类模型，被用于各种分类场景和点击率预估问题等，它也是Max Entropy(ME, 最大熵)模型[2]，或者说Softmax Regression模型[3]，在二分类的一种特例。

用\\(X\ =\ (x_1, x_2, ..., x_k)\\)表示*k*维样本，用\\(\mathbf{\beta} = (\beta_0, \beta_1, \beta_2, ..., \beta_k)\\)表示*k+1*维模型变量，其中\\(\beta_0\\)表示截距项，那么LR模型的model function如下表示：

\begin{equation}\mathbf{f}(z) = \frac 1{1 + e^{-z}}\end{equation}

\begin{equation}z = \beta_0 + \beta_1 \times x_1 +  \beta_2 \times x_2 + ... +  \beta_k \times x_k\end{equation}

说明：公式1的学名为logistic function。

通常情况下，准备好标注样本和特征后，经过参数训练，最终会得到机器学习模型，对LR模型而言，得到的是分类超平面。但样本不均衡的情况下，通常的参数训练方法会带来模型估计上的偏差。对LR模型而言，通常的参数训练方法会造成正样本的估计概率低于真实值。论文[4]在5.1一节，以及书籍[5]在13.5.3一节，对此作了论述。在文献中从只有1个特征且该特征的特征权重大于0的LR模型出发来解释。在均值和方差都未知的情况下，用极大似然估计（Maximum Likelihood Estimator, MLE）估计高斯分布的方差是有偏的，MLE估计出的方差的分母是样本数，但方差的无偏估计是样本数减1 [6]。也就是说，正样本因为样本少使得估计不准，而且会使得分界面会比真实的分界面更右一些，这样使得正样本的估计概率低于真实值。

## 2. 稀有事件下LR模型的矫正方法

对稀有事件应用通常的LR模型训练方法会造成估计值低于真实值，有2类矫正思路：

1. 不走负采样，而直接对普通的LR模型训练出的模型做矫正

2. 走负采样，然后做模型矫正

当样本量大时，比如在广告定向投放中的点击率预估问题中会遇到数亿的样本量，第2种方案因为要处理的样本量少若干个数量级使得训练效率显然更高。考虑到在工业界，常见大规模数据下的模型训练，在下文就围绕"负采样 + 模型矫正"方案介绍2种矫正方法。

### 2.1 Prior Correction

"Prior Correction"策略可以理解为基于先验分布的矫正。进行负采样后经过模型训练会得到模型参数，因为采样前后正样本的比例发生变化，所以得到的模型是有偏的，而且对正样本的估计概率偏高。需要把正样本比例作为先验信息，对模型参数做矫正。使用MLE估计出的模型参数中，估计出的非截距项的参数与真实参数是一致的，不用矫正，但对估计出的表示截距项的参数只需按照公式3进行矫正。

\begin{equation}{\hat {\beta}_0} - ln\left[\left(\frac {1 - \tau}{\tau}\right)\left(\frac {\hat y}{1 - \hat y}\right)\right]\end{equation}

说明：\\({\hat {\beta}}_0\\)是进行负采样后的通过LR模型训练出的模型参数。\\(\hat {\tau}\\)是未进行负采样时正样本的比例，\\(\hat y\\)是进行负采样后的正样本的比例。公式3在论文[4]的4.1一节也有论述，并在论文的附录B中有公式推导。

\\(\hat {\tau}\\)需要未进行负采样时正样本的比例，这个需要先验知识。在一些问题上，比如在广告定向投放的点击率预估问题中，这个可以用统计CTR来近似替代。

"Prior Correction"策略的优点是现有的模型训练工具不用修改，还是可以使用，只不过需要加个对截距项的后处理计算。缺点是如果所建立的模型有偏差，比如少了一些应该有的特征，那这个方法的鲁棒性会比下文将介绍的Weighting策略要差。

### 2.2 Weighting

## 3. 在广告点击率预估中的应用

Google和FB是怎么做的。

## 参考文献

[1] [Logistic Regression](https://en.wikipedia.org/wiki/Logistic_regression) (来自Wikipedia)

[2] [Max Entropy](https://en.wikipedia.org/wiki/Maximum_entropy_probability_distribution) (来自Wikipedia)

[3] [Softmax Regression 或者 Multinomial Logistic Regression](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) (来自Wikipedia)

[4] Gary King, Langche Zeng. Logistic Regression in Rare Events Data. Political Methodology. 2002

[5] 刘鹏, 王超. 计算广告. 2015

[6] [极大似然法计算出的高斯分布的方差为什么会产生偏差](https://www.zhihu.com/question/28751472) (来自知乎)

[7] H. Brendan McMahan, et al. Ad Click Prediction: a View from the Trenches. KDD2013

[8] Xinran He, et al. Practical Lessons from Predicting Clicks on Ads at Facebook. ADKDD2014
