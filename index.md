---
layout: page
title: Hello World!
tagline: 
---
{% include JB/setup %}

<div align="center">
  <img src="/images/index-figure1.jpg" style="max-width:344px; text-align:center" alt=""/>
</div>

<br />

计算机领域包括的内容特别丰富，知识更新的速度非常快，而且如今在计算机应用领域，大有工业界推动学术界的趋势。博主喜欢的领域不多，主要偏机器学习、自然语言处理。喜欢能搞定实际问题的模型，喜欢能解决需求且高效健壮易扩展的系统。

欢迎与我讨论问题！

### 最新文章

<ul class="posts">
  {% for post in site.posts limit:7 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

### 代码仓库

+ [alphabet](https://github.com/vividfree/alphabet): 个人写的 **机器学习**, **自然语言处理**, **大规模数据处理** 相关的代码

### 个人关键词

+ **机器学习**, **计算广告**, **自然语言处理**, **个性化推荐**, **大规模数据处理**, **系统架构**
+ C++, Python, Shell <font color='red'>|</font> Hadoop, Hive, MPI, Spark <font color='red'>|</font> Parameter Server <font color='red'>|</font> Kafka, RabbitMQ <font color='red'>|</font> LevelDB, Redis
+ 奇虎360, 人民搜索; Hulu北京（实习）
+ 中科院计算所, 华中科技大学, 江西省高安中学
+ 足球迷, 喜欢巴萨喜欢恒大
+ Stay hungry! Stay foolish!

### 还可以在这些地方找到我的足迹

+ 老博客 : [http://luowei828.blog.163.com/](http://luowei828.blog.163.com/)（网易博客系统近期有点不稳定，目前已不更新）
+ Github : *vividfree*
+ Weibo  : *vividfree*

### 推荐站点

<a href="/%E5%86%85%E5%AE%B9%E7%B4%A2%E5%BC%95/2015/11/02/recommended-website">这里</a>的网站都不错（会不断更新）
