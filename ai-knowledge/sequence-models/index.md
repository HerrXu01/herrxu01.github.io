---
layout: page
title: Sequence Models
---

#### These notes are based on the [Sequence Models course](https://www.coursera.org/learn/nlp-sequence-models) of Andrew Ng et al. offered by coursera.

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
