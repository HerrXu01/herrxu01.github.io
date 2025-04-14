---
layout: page
title: Sequence Models
---

<div class="note-cards-container">
  {% for post in site.categories.sequence-models %}
  <a href="{{ post.url }}" class="note-card">
    <div class="note-content">
      <h3>{{ post.title }}</h3>
      <span class="note-date">{{ post.date | date: "%B %d, %Y" }}</span>
    </div>
  </a>
  {% endfor %}
</div>
