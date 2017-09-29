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

**很多东西都可以成为艺术品，程序也不例外！**

### 最新文章

<ul class="posts">
  {% for post in site.posts limit:7 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  <li><a href="/archive.html">更多文章......</a></li>
</ul>

### 文章索引

+ [博客文章索引](2017/09/27/blog-article-index) : 主要从技术方向上对若干篇博文（非全部的博文）进行知识索引，以帮助形成一种知识框架。

### 代码仓库

+ [alphabet](https://github.com/vividfree/alphabet) (Github) : 个人写的 **机器学习**, **自然语言处理**, **大规模数据处理**, **基础工具** 相关的代码（持续维护中）

### 推荐内容

+ <a href="/2015/11/02/recommended-technology">工程技术</a> <font color='red'>|</font> <a href="/2015/11/02/recommended-environment">地球环境</a> <font color='red'>|</font> <a href="/2015/11/02/recommended-science-and-art">科学与艺术</a>
