---
layout: post
title: Spark学习路径：使用Spark Accumulators的注意事项
category: 大规模数据处理
tagline: 
tags: [Spark, Accumulators]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

Spark accumulator的出现最初是为了模仿Hadoop中的Counter，但现在看来，因为Spark的特殊设计，使得accumulator容易返回错误的结果。

Spark会保证action中accumulator会正确的执行一次，但不保证transformation中的accumulator会正确的执行一次，而可能是多次，或者是部分的多次。
（Spark官方解释如下）
> For accumulator updates performed inside actions only, Spark guarantees that each task’s update to the accumulator will only be applied once, i.e. restarted tasks will not update the value. In transformations, users should be aware of that each task’s update may be applied more than once if tasks or job stages are re-executed.

关于Spark中accumulator的不足，有篇讨论也列举的比较详细，值得细看。[http://stackoverflow.com/questions/29494452/when-are-accumulators-truly-reliable](http://stackoverflow.com/questions/29494452/when-are-accumulators-truly-reliable)

Accumulator的主要代码贡献者之前也写过一篇博文，描述他对accumulators的设计并不满意。[http://imranrashid.com/posts/Spark-Accumulators/](http://imranrashid.com/posts/Spark-Accumulators/)
（摘自其中的一段话）
> However, it can easily seem like these limitations are just for a small corner case, when in fact, they make accumulators a totally incomplete replacement for MapReduce counters. If you do try to use accumulators outside of RDD actions, they are worse than useless – they are actively misleading.

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
