---
layout: page
title: Tags
permalink: /tags/
---

<div>
{% for tag in site.tags %}
  <div class="archive-group">
    <!-- tag_name 변수 지정 -->
    {% capture tag_name %}{{ tag | first }}{% endcapture %}
    <!-- tag_name을 소문자(slugize)로 변경해준다.-->
    <div id="#{{ tag_name | slugize }}"></div>
    <p></p>
    <!-- 태그명-->
    <h3 class="category-head">{{ tag_name }}</h3>
    <a name="{{ tag_name | slugize }}"></a>
    {% for post in site.tags[tag_name] %}
    <!-- 게시물 제목 -->
    <article class="archive-item">
      <li><a href="{{ post.url }}">{{post.title}}</a></li>
    </article>
    {% endfor %}
  </div>
  {% endfor %}
</div>
