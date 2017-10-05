---
layout: post
title: deeplearning.ai出品的deep learning课程听课有感
category: 听课笔记
tagline: 
tags: [听课笔记, deeplearning.ai, deep learning, 深度学习]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

Andrew Ng从百度离职后创立了 [deeplearning.ai](https://www.deeplearning.ai/) 网站，计划出品5门深度学习相关的认证课程，并放在Coursera上。课程网址在 [这里](https://www.coursera.org/specializations/deep-learning) 。目前已制作好3门课程，它们依次是“Neural Networks and Deep Learning”、“Improving Deep Neural Networks: Hyperparameter tuning, Regularization and Optimization”、“Structuring Machine Learning Projects”。剩下的2门课程是“Convolutional Neural Networks”和“Sequence Models”。中国的学生可以在网易云课堂的 [这里](http://mooc.study.163.com/smartSpec/detail/1001319001.htm) 免费学习，不过网易云课堂因为没有引进作业和对应的评估，所以就不会颁发课程认证。

近几年AI领域取得成果最多的是深度学习，Andrew Ng希望通过这些课程，让更多的人进入AI领域。他认为"AI is the new electricity"，将改变各行各业。教育虽然不是做前沿科技研究，但倘若它能培养出几十万甚至是数百万的正规军，那么教育就有了巨大的价值，因为它会给整个社会的进步提供了巨大的人才储备。该课程有对几位Deep Learning大师的采访，从Geoffrey Hinton和Joshua Bengio的话语中能体会到Deep Learning还能走得更远，其中还有很多研究方向和业务落地方向需要尝试，但却又非常缺人才。Andrew Ng正是在给DL摇旗呐喊，这些课程定会培养出更多的人才，等这批人才就位后，DL的前进速度更会越来越快，更会呈指数级的进步。

笔者听了3门课程的大部分内容，最核心的收获是：如何系统性的design, analyse和debug机器学习或者深度学习系统。
+ 很多人都了解dropout和early stop是正则化（regularization）技术里常用的2个技术，但Andrew Ng介绍了他对这些技术的优缺点分析以及如何用在具体实践中。此外还有对L1和L2正则、超参数如何search等技术的看法。
+ 数据集应该有哪些？Training set, train-dev set, dev set, test set。Train-dev set可选，如果training set和dev/test set的分布不同，那可以引入train-dev set以判断模型的variance和data mismatch error分别有多大。
+ 以什么样的比例切分出这些集合？不同于过去机器学习系统能用到的标注数据不多，因为那时只有数百到数万的样本，所以dev/test set分别占的比例会到20%左右。而现在实际业务系统上数据规模很容易到数百万甚至更大，dev/test set的比例可能只需要1%即可，这样也可以让像DL这种复杂模型使用到大量的训练数据。
+ Andrew Ng在error analyse上花了很多的功夫，系统性的介绍了human level error, training set error, train-dev set error, dev set error和test set error的概念，相邻2个之间会有gap，有哪些办法可以消除这些gap。Ng还把这个调试过程类比为调试电视机收看电视节目。
+ 虽然只是简单介绍了transfer learning和multi-task learning的大体框架和适用场景，但可以看到deep learning模型可以很好很方便的用于这两方面工作。
+ 笔者认为最精彩的部分是对学术大师的采访，目前已邀请了Geoffrey Hinton、Joshua Bengio、Ian Goodfellow和林元庆等7位。通过这些采访，能了解Hinton和Bengio早在二三十年前的工作，比如基于神经网络的语言模型（NNLM），他们在80年代到90年代那会已经有研究了，但很多人是在2000年之后才了解这部分的工作，甚至是2013年word2vec诞生后才了解的。此外还能了解到大师们对DL未来发展的看法。

当然3门课程介绍的内容特别丰富也特别全面，笔者的收获很多，上面只是列举了一部分收获。感兴趣的读者也可以上上这些课程。

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
