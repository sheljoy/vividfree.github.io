---
layout: page
title: vividfree的博客
tagline: 
---
{% include JB/setup %}

计算机领域包括的内容特别丰富，知识更新的速度非常快，而且如今在计算机应用领域，大有工业界推动学术界的趋势。博主的水平有限，喜欢的领域不多，主要偏机器学习、自然语言处理。喜欢coding，喜欢那种模型中等复杂但能解决实际问题、模型易解释、系统易扩展的实际系统，当然也爱好各种行业八卦。

欢迎与我讨论问题！

### 近期博文

<ul class="posts">
  {% for post in site.posts limit:10 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

### 个人关键词

+ **机器学习**, **计算广告**, **自然语言处理**, **大规模数据处理**, **系统架构**
+ C++, Python, Shell \| Hadoop, Hive, MPI, Spark \| Kafka, RabbitMQ \| LevelDB, Redis
+ 奇虎360, 人民搜索; Hulu北京（实习）
+ 中科院计算所, 华中科技大学, 江西省高安中学
+ 足球迷, 喜欢巴萨喜欢恒大

### 还可以在这些地方找到我的足迹

+ 老博客 : [http://luowei828.blog.163.com/](http://luowei828.blog.163.com/)（网易博客系统近期有点不稳定）
+ Github : *vividfree*
+ Weibo  : *vividfree*
