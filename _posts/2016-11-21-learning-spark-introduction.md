---
layout: post
title: Spark学习路径：介绍
category: 大规模数据处理
tagline: 
tags: [Spark, RDD, Databricks]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

Spark最初在2009年由加州大学伯克利分校的AMPLab开发，并于2010年成为Apache的开源项目之一，如今是很火的大数据处理框架之一。

网上有很多关于Spark的资料，从整体到细节，从浅到深，都有相关资料。刚接触Spark时，可能会看到 RDD, DataFrame, DataSet, transformation, action, lineage, narrow dependencies, wide dependencies 等spark核心术语，还可能还会听到很多Spark与Hadoop, Storm等其他分布式系统的对比。对于Spark核心术语，可以阅读RDD的最早论文“Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing”，这篇文章值得认真阅读，可以体会到Spark设计者在设计系统时为啥抽象出那些概念。

对于spark初学者来说，建议看些spark相关的书、牛人写的相关文章、一些公司写的相关博客。

"Big Data Processing with Apache Spark"系列文章（共4篇）写得不错，推荐给读者读读：
Part 1:
+ [https://www.infoq.com/articles/apache-spark-introduction](https://www.infoq.com/articles/apache-spark-introduction)
  - 中文翻译版 [http://www.infoq.com/cn/articles/apache-spark-introduction](http://www.infoq.com/cn/articles/apache-spark-introduction)
Part 2:
+ [https://www.infoq.com/articles/apache-spark-sql](https://www.infoq.com/articles/apache-spark-sql)
Part 3:
+ [https://www.infoq.com/articles/apache-spark-streaming](https://www.infoq.com/articles/apache-spark-streaming)
  - 中文翻译版 [http://www.infoq.com/cn/articles/apache-spark-streaming](http://www.infoq.com/cn/articles/apache-spark-streaming)
Part 4:
+ [https://www.infoq.com/articles/apache-spark-machine-learning](https://www.infoq.com/articles/apache-spark-machine-learning)
  - 中文翻译版 [http://www.infoq.com/cn/articles/apache-spark-machine-learning](http://www.infoq.com/cn/articles/apache-spark-machine-learning)

2013年最初开发Spark的团队创建了Databricks公司，DataBricks公司的官方博客 [https://databricks.com/blog](https://databricks.com/blog) 也值得看看，里面会介绍Spark研发和产业方面的动态。他们家还定期组织Spark Summit，在Spark summit 2016邀请到 Jeff Dean, Doug Cutting, Andrew Ng 做keynote speech，相比国内的某些技术峰会，这个峰会的干货是很多的了，而且峰会的slide很多都可以下载到。Databricks的Xiangrui Meng等人也有些slides，深入浅出的介绍了Spark的使用。

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
