---
layout: page
title: Deep Learning
---

<div class="note-cards">
  {% assign posts = site.categories.deep-learning %}
  {% for post in posts %}
  <a href="{{ post.url }}" class="note-card">
    <div class="note-content">
      <h3>{{ post.title }}</h3>
      <span class="note-date">{{ post.date | date: "%B %d, %Y" }}</span>
    </div>
  </a>
  {% endfor %}
</div>
