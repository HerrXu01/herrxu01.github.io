---
layout: page
title: Deep Learning
---

<ul>
  {% assign posts = site.categories.deep-learning %}
  {% for post in posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
  </li>
  {% endfor %}
</ul>
