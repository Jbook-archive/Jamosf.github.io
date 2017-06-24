---
layout: page
title: About
description: 像疯子一样活着
keywords: Jamos
comments: true
menu: 关于
permalink: /about/
---

我是Jamos，为代码而生。

在过去蹉跎的二十载，没有发现代码之美，而今发现，就无法自拔。

## 联系

* GitHub：[@fengshangren](https://github.com/fengshangren)
* 个人博客：[@{{ site.title }}]({{ site.url }})
* 新浪博客: [@加摩斯](http://blog.sina.com.cn/u/2205677364)
* 微博: [@CSU老马冇敌SJTU](http://weibo.com/u/2205677364/home?wvr=5)
* 知乎: [@加摩斯](https://www.zhihu.com/people/jia-mo-si/activities)

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
