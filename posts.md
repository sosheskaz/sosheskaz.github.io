---
layout: page
title: All Posts
permalink: /posts/
---
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }} {{post.date | date: '%d %B %Y'}}</a>
    </li>
  {% endfor %}
</ul>