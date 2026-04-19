---
layout: default
title: Home
---

# Latest Blog Posts

{% for post in site.posts %}
  <article>
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p class="post-meta">
      <span class="date">{{ post.date | date: "%B %d, %Y" }}</span>
      {% if post.categories %}
        | <span class="categories">{{ post.categories | join: ", " }}</span>
      {% endif %}
    </p>
  </article>
{% endfor %}
