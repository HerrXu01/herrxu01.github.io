---
layout: page
title: Machine Learning
---

<div class="note-cards">
  {% assign posts = site.categories.machine-learning %}
  {% for post in posts %}
  <div class="note-card">
    <a href="{{ post.url }}">
      <h3>{{ post.title }}</h3>
      <span class="note-date">{{ post.date | date: "%B %d, %Y" }}</span>
    </a>
  </div>
  {% endfor %}
</div>
