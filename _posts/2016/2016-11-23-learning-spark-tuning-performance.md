---
layout: post
title: Spark学习路径：性能调试
category: 大规模数据处理
tagline: 
tags: [Spark, performance]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

对Spark的性能调试(tuning performance)，有好些文章介绍得不错，推荐给大家：

+ [Tuning Spark](https://spark.apache.org/docs/latest/tuning.html) <font color='red'>From spark.apache.org</font>
+ How-to: Tune Your Apache Spark Jobs [(Part 1)](http://blog.cloudera.com/blog/2015/03/how-to-tune-your-apache-spark-jobs-part-1/) [(Part 2)](http://blog.cloudera.com/blog/2015/03/how-to-tune-your-apache-spark-jobs-part-2/) <font color='red'>From Cloudera</font>
+ [Tuning Java Garbage Collection for Apache Spark Applications](https://databricks.com/blog/2015/05/28/tuning-java-garbage-collection-for-spark-applications.html) <font color='red'>From Databricks</font>
+ [Tuning and Debugging in Apache Spark](http://www.slideshare.net/pwendell/tuning-and-debugging-in-apache-spark)<font color='red'> From Databricks</font>
+ Spark性能优化指南 [(基础篇)](http://tech.meituan.com/spark-tuning-basic.html) [(高级篇)](http://tech.meituan.com/spark-tuning-pro.html) <font color='red'>来自 美团技术博客</font>

<font color='red'>NOTE:</font>
Spark版本更新很快，一些文章所述的一些问题或者解决办法可能不适合大家正使用的Spark版本，这个尤其要注意，特别是当为了性能调试一些参数时发现运行状况几乎没变化时，可以想想是不是参数没有生效。笔者曾经碰到的一个坑，调试spark.shuffle.memoryFraction和spark.storage.memoryFraction参数发现没效果，后来追查因为用的是Spark 1.6.1版本，默认使用的是统一内存管理模型(Spark 1.6及以后版本，Unified Memory Manager)，而不是LegacyMode(Spark 1.5及以前版本，最早称呼为 Static Memory Manager)，如果没有打开spark.memory.useLegacyMode的话，spark.shuffle.memoryFraction和spark.storage.memoryFraction自然无效。

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
