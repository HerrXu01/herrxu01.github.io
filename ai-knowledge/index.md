---
layout: page
title: AI Knowledge
---

<div class="container">
  <h1>AI Knowledge</h1>
  <p>Explore the fundamental knowledge in different AI domains including Machine Learning, Deep Learning, and more.</p>

  <!-- Card Container -->
  <div class="card-container">
    <!-- Card for Machine Learning -->
    <div class="card">
      <h2>Machine Learning</h2>
      <ul>
        {% assign posts = site.categories.machine-learning | sort: 'date' | reverse %}
        {% for post in posts limit: 5 %}
        <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}</li>
        {% endfor %}
      </ul>
      <a href="/ai-knowledge/machine-learning/" class="btn">Learn More</a>
    </div>

    <!-- Card for Deep Learning -->
    <div class="card">
      <h2>Deep Learning</h2>
      <ul>
        {% assign posts = site.categories.deep-learning | sort: 'date' | reverse %}
        {% for post in posts limit: 5 %}
        <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}</li>
        {% endfor %}
      </ul>
      <a href="/ai-knowledge/deep-learning/" class="btn">Learn More</a>
    </div>

    <!-- Add more cards for other categories as needed -->
  </div>
</div>
