---
layout: default
title: Home
---

# Home

Welcome to my blog and website.

## Latest Blog Posts

{% for post in site.posts %}
  <article>
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p class="post-meta">
      <span class="date">{{ post.date | date: "%d %B %Y" }}</span>
      {% if post.categories %}
        | <span class="categories">{{ post.categories | join: ", " }}</span>
      {% endif %}
    </p>
  </article>
{% endfor %}
