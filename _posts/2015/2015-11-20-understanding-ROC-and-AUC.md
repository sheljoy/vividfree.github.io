---
layout: post
title: 理解 ROC 和 AUC
category: 机器学习
tagline: 
tags: [ROC, AUC, 评价指标]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

## 1. 引言

ROC（Receiver Operating Characteristic）曲线和AUC（Area Under Curve）常被用来评价一个二值分类器（binary classifier）的优劣。相比准确率、召回率、F-score这样的评价指标，ROC曲线有这样一个很好的特性：当测试集中正负样本的分布变化的时候，ROC曲线能够保持不变。在实际的数据集中经常会出现类不平衡（class imbalance）现象，即负样本比正样本多很多（或者相反），而且测试数据中的正负样本的分布也可能随着时间变化。

论文[3]是篇很不错的文章，介绍了ROC和AUC的特点，如何作出ROC曲线图和计算AUC，AUC的含义，以及对多类别分类问题如何计算AUC。后来有篇博文[4]翻译了这篇文章的核心部分，浅显易懂，适合不喜欢读英文的读者。

<div align="center">
  <img src="/images/2015-11-20-understanding-ROC-and-AUC-figure1.jpg" style="max-width:634px; text-align:center" alt=""/>
</div>

图1摘自论文[3]。ROC曲线，是以一系列的(fp rate, tp rate)或者写成(FPR, TPR)，为二维笛卡尔坐标系中的坐标点。应用到实际问题中，对一份训练集如何算出一系列的FPR和TPR，可以参考[3]或[4]。

AUC（确切的说，应该是AUROC）被定义为ROC曲线下的面积，显然这个面积的数值不会大于1。ROC曲线上的任意相邻两点与横轴都能形成梯形，把所有这样的梯形面积做加和即可得到AUC。一般而言，训练样本越多，在得到样本判别为正例的分数取值后不同分数也相对会越多，这样ROC曲线上的点也就越多，估算的AUC会更准些。这种思路很像微积分里常用的微分法。该方法正是在论文[3]中描述的方法，笔者在实际业务中实现了它，它并不难实现。

## 2. AUC的物理含义

那么AUC值的含义是什么呢？在论文[3]，有这样一段话：”The AUC value is equivalent to the probability that a randomly chosen positive example is ranked higher than a randomly chosen negative example. This is equivalent to the Wilcoxon test of ranks (Hanley and McNeil, 1982). The AUC is also closely related to the Gini coefficient (Breiman et al., 1984), which is twice the area between the diagonal and the ROC curve. Hand and Till (2001) point out that Gini + 1 = 2 * AUC.”

简单翻译下：首先AUC值是一个概率值，当你随机挑选一个正样本以及一个负样本，当前的分类算法根据计算得到的Score值将这个正样本排在负样本前面的概率就是AUC值。AUC值越大，当前的分类算法越有可能将正样本排在负样本前面，即能够更好的分类。另外，AUC与Gini分数有联系，Gini + 1 = 2*AUC。

关于AUC表示的概率含义在ROC的维基百科词条[5]中也有说明。不过维基百科中还提到这样一个观点，机器学习领域中经常用ROC和AUC去做模型对比，最近学术界认为这种做法会引入一些错判，有些文章对此进行了讨论。笔者认为学术界值得认真讨论此问题，但在工业界，AUC指标一般与业务评价指标（比如点击率等）本身就不是一致的，所以在实际业务中，会综合考虑AUC指标以及其他指标来选择最终模型，这样做能降低选到不良模型的可能性。

既然了解了AUC表示的概率含义，那么就可以通过概率统计的方法来算AUC。做N次随机试验，每次实验中随机采样一个正样本和一个负样本，当模型预测正样本的分数大于模型预测负样本的分数，计数则加1。记计数最终为n（n肯定小于等于N），那么用n/N即得到AUC。Stackexchange中的一篇帖子[6]在"A concordance measure"一节中也提到了这种算AUC的方法，并通过实验说明此方法计算出的AUC与画出ROC曲线然后算AUC面积是一致的。不过应用这个物理含义来算AUC，除了走先随机采样后计数以得到概率的方案外，还可以用公式1来计算：

\begin{equation}\frac {\sum_{i \in P} r_i - \frac {\|P\| \times (\|P\| + 1)}2}{\|P\| \times \|N\|}\end{equation}

说明：
P表示正样本集合，N表示负样本集合，|S|表示集合S的元素个数。\\(r_i\\)表示元素\\(i\\)在全集（P+N）中按预测score从小到大排的rank位置（rank位置从1开始，比如：假设|P+N|=10，那么最高分的rank值为10，最低分的rank值为1）。举例子说明上式的计算过程：

假设\\(\|P+N\|\\)有5个元素，按系统预测score从小到大排如下：

<br/>

|     样本情况    | 样本1 | 样本2 | 样本3 | 样本4 | 样本5 |
| :-------------: |:-----:|:-----:|:-----:|:-----:|:-----:|
|  正例 or 负例   |   N   |   P   |   N   |   P   |   P   |
| 系统预测score   |  0.2  |  0.3  |  0.4  |  0.5  |  0.6  |
| rank值\\(r_i\\) |   1   |   2   |   3   |   4   |   5   |

<br/>

对该例，\\(\|P\| = 3, \|N\| = 2\\)，分母为6，分子为\\((2+4+5) – (0.5 \times 3 \times 4)\\)=5。那么AUC为\\(5 \div 6 = 0.8333\\)。

下面用两节分别证明这个式子与AUC的物理含义是一致，以及该式与第一种方法（基于ROC曲线计算AUROC的方法）是一致的。以此得到三种方法的相互一致。（为了描述直观，先忽略因系统预测score相同导致rank值相同，后面再对此做说明）

## 3. 与AUC的物理含义一致的证明

全集（P+N）中一个正样本与一个负样本组成pair的总数为 \\(\|P\| \times \|N\|\\) ，也就是式子中的分母。那么接下来只需要证明对于\\(\\{r_i\\}\\)序列来说，满足正样本的rank值大于负样本rank值的pair总数是分子表达的那个数。这个可以基于加法原理来计算，对每个正样本，统计出它的rank值能大于的负样本个数，做个累加求和即可。对某个\\(i \in P\\)，它的rank值能大于的负样本个数表示为（公式2和公式3是等价的，不过式子3便于做后面的累加求和）：

\begin{equation}\sum_{j \in N} I(r_j < r_i)\end{equation}

\begin{equation}r_i - 1 - \sum_{j \in P} I(r_j < r_i)\end{equation}

基于式子3，对正样本做累加求和的结果为：

\begin{equation}\sum_{i \in P} \left(r_i - 1 - \sum_{j \in P} I(r_j < r_i)\right) \\\ = \sum_{i \in P} r_i - \|P\| - \sum_{i \in P}\sum_{j \in P} I(r_j < r_i) \\\ = \sum_{i \in P} r_i - \|P\| - (0 + 1 + ... + (\|P\| - 1)) \\\ = \sum_{i \in P} r_i - \frac {\|P\| \times (\|P\| + 1)}2\end{equation}

至此即证明了对于\\(\\{r_i\\}\\)序列来说，满足正样本rank值大于负样本rank值的pair总数正是分子。所以得证公式1算的正是AUC。

既然可以对正样本走加法原理，自然也可以对负样本走加法原理。所以公式1的分子也会等价于：

\begin{equation}\sum_{i \in N}\sum_{j \in P} I(r_j > r_i)\end{equation}

说明：当pair中的正样本和负样本的预测score相等的时候，分子则加上0.5。

## 4. 与基于ROC曲线计算AUROC的方法一致的证明

画出ROC曲线（横轴为\\(FPR = \frac {FP}{\|N\|}\\)，纵轴为\\(TPR = \frac {TP}{\|P\|}\\)），算出每个小梯形的面积然后累加求和。对\\(\\{r_i\\}\\)序列，该方法可以用公式形式化表示如下：

\begin{equation}\sum_{i \in (P + N)} \frac {(\frac {TP_i}{\|P\|} + \frac {TP_{i-1}}{\|P\|}) \times (\frac {FP_i}{\|N\|} - \frac {FP_{i-1}}{\|N\|})}2\end{equation}

对公式6化简得：

\begin{equation}\sum_{i \in (P + N)} \frac {(TP_i + TP_{i-1}) \times (FP_i - FP_{i - 1})}{2 \times \|P\| \times \|N\|} \\\ = \sum_{i \in P} \frac {(TP_i + TP_{i-1}) \times (FP_i - FP_{i - 1})}{2 \times \|P\| \times \|N\|} + \sum_{i \in N} \frac {(TP_i + TP_{i-1}) \times (FP_i - FP_{i - 1})}{2 \times \|P\| \times \|N\|}\end{equation}

因为对P集合，\\(FP_i\\)与\\(FP_{i - 1}\\)是一样的；对N集合，\\(TP_i\\)与\\(TP_{i - 1}\\)是一样的，所以继续化简为：

\begin{equation}\sum_{i \in N} \frac {(TP_i + TP_{i-1}) \times (FP_i - FP_{i - 1})}{2 \times \|P\| \times \|N\|} \\\ = \sum_{i \in N} \frac {TP_i}{\|P\| \times \|N\|} \\\ = \frac {\sum_{i \in N} TP_i}{\|P\| \times \|N\|} \\\ = \frac {\sum_{i \in N}\sum_{j \in P} I(r_j > r_i)}{\|P\| \times \|N\|}\end{equation}

结合公式5的说明，即证明了公式1与 基于ROC曲线计算AUROC的方法 是一致的。

说明：当存在预测score相等的情况时，对相等score的样本，需要 赋予相同的rank(无论这个相等的score是出现在同类样本还是不同类的样本之间，都需要这样处理)。对这个rank是这样计算的：把所有这些预测score相等的样本的rank取平均，然后再使用上述公式。

虽然三种方法是等价的，但在计算量上去掉排序的因素（排序的计算复杂度为O(NlogN)），公式1的计算效率要高。


## 参考文献

[1] Hanley, J.A., McNeil, B.J., The meaning and use of the area under a receiver operating characteristic (ROC) curve. Radiology 143, 29–36. 1982.

[2] Breiman, L., Friedman, J., Olshen, R., Stone, C., Classification and Regression Trees. Wadsworth International Group. 1984.

[3] Tom Fawcett, An introduction to ROC analysis. Pattern Recognition Letters. 2006.

[4] [Introduction to auc and roc](http://alexkong.net/2013/06/introduction-to-auc-and-roc/)

[5] ROC(Receiver operating characteristic) ([From Wikipedia](https://en.wikipedia.org/wiki/Receiver_operating_characteristic))

[6] [How to calculate area under the curve auc or the c-statistic by hand](http://stats.stackexchange.com/questions/145566/how-to-calculate-area-under-the-curve-auc-or-the-c-statistic-by-hand)

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
