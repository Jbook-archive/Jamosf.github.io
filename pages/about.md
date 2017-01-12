---
layout: page
title: About
description: 像疯子一样活着
keywords: shangren Feng, 冯上任
comments: true
menu: 关于
permalink: /about/
---

我是冯上任，为代码而生。

在过去蹉跎的二十载，没有发现代码之美，而今发现，就无法自拔。

## 联系

* GitHub：[@fengshangren](https://github.com/fengshangren)
* 博客：[{{ site.title }}]({{ site.url }})
* 微博: [@CSU老马冇敌SJTU](http://weibo.com/CSU老马冇敌SJTU)
* 知乎: [@加摩斯](http://www.zhihu.com/people/加摩斯)

## Skill Keywords

#### Software Engineer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_software_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Mobile Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_mobile_app_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Windows Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_windows_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>
