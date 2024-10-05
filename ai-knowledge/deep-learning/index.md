---
layout: page
title: Deep Learning
---

<div class="note-cards">
  {% assign posts = site.categories.deep-learning %}
  {% for post in posts %}
  <div class="note-card">
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <span class="note-date">{{ post.date | date: "%B %d, %Y" }}</span>
  </div>
  {% endfor %}
</div>
