---
layout: default
title: LIMIX's PKM
needComment: no
---

<div style="float:left;width:75%">
文章列表
<ul>
{% for post in site.posts %}
<li>{{post.date | date_to_string}} <a href="{{site.baseurl}}{{post.url}}">{{post.title}}</a></li>
{%endfor%}
</ul>
</div>

<div style="float:right;width:100px;">
  <img src="{{site.baseurl}}/assets/pic/QR.png" style="width:80px;height:80px;"/>
</div>
