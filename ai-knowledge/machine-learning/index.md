---
layout: page
title: Machine Learning
---

<h1>Machine Learning Posts</h1>

<!-- Sorting options -->
<div class="sort-options">
  <button onclick="sortPosts('asc')">Sort by Date (Asc)</button>
  <button onclick="sortPosts('desc')">Sort by Date (Desc)</button>
  <button onclick="sortPosts('learning')">Sort by Learning Order</button>
</div>

<div id="post-container">
  {% assign posts = site.categories.machine-learning | sort: 'date' | reverse %}
  {% if posts %}
    {% for post in posts %}
    <div class="post" data-date="{{ post.date }}" data-order="{{ post.learning_order }}">
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <p>{{ post.date | date: "%B %d, %Y" }}</p>
    </div>
    {% endfor %}
  {% else %}
    <p>No posts available in this category.</p>
  {% endif %}
</div>

<script>
  function sortPosts(order) {
    let posts = [...document.querySelectorAll('.post')];
    posts.sort((a, b) => {
      if (order === 'asc') {
        return new Date(a.dataset.date) - new Date(b.dataset.date);
      } else if (order === 'desc') {
        return new Date(b.dataset.date) - new Date(a.dataset.date);
      } else {
        return a.dataset.order - b.dataset.order; // Custom learning order
      }
    });
    const container = document.getElementById('post-container');
    container.innerHTML = '';
    posts.forEach(post => container.appendChild(post));
  }
</script>
