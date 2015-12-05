---
layout: page
title: Welcome
tagline: 
---
{% include JB/setup %}

大家好！

我是vividfree（罗维），这个博客主要关注 **机器学习** **计算广告** **自然语言处理** **大数据处理** **系统架构** 领域的前沿进展。

欢迎与我讨论问题！

### 近期博文

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

### 个人关键词

+ 中科院计算所, 华中科技大学, 江西省高安中学
+ 奇虎360, 人民搜索, Hulu
+ 足球迷, 喜欢巴萨喜欢恒大

### 还可以在这些地方找到我的足迹

+ github : vividfree
+ weibo  : vividfree
