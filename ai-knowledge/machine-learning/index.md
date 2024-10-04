---
layout: page
title: Machine Learning
---

<h1>Machine Learning Notes</h1>

<ul>
  {% assign posts = site.categories.machine-learning %}
  {% for post in posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
  </li>
  {% endfor %}
</ul>
