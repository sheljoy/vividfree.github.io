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

### 代码仓库

+ [alphabet](https://github.com/vividfree/alphabet) (Github) : 个人写的 **机器学习**, **自然语言处理**, **大规模数据处理** 相关的代码（under construction）

### 技术心愿

+ 用树莓派或者类似的硬件，造玩具，比如遥控汽车等
+ 对某些领域建立知识图谱
  - 进展: 目前在汽车、房地产、旅游等领域积累了些数据词典
+ 应用Machine Learning，辅助分析财经等领域的趋势判断
+ create a **Never-Ending Learning System (NELS)**

### 推荐站点

+ <a href="/2015/11/02/recommended-website-technology">技术</a> <font color='red'>|</font> <a href="/2015/11/02/recommended-website-science">科学</a> <font color='red'>|</font> <a href="/2015/11/02/recommended-website-culture">人文</a> <font color='red'>|</font> <a href="/2015/11/02/recommended-website-other">其他</a>
