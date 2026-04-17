---
layout: default
title: Blog
---

# Blog

Welcome to my blog where I share thoughts and tutorials.

## Latest Posts

{% for post in site.posts %}
  <article>
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p class="post-meta">
      <span class="date">{{ post.date | date: "%B %d, %Y" }}</span>
      {% if post.categories %}
        | <span class="categories">{{ post.categories | join: ", " }}</span>
      {% endif %}
    </p>
    <div class="excerpt">{{ post.excerpt }}</div>
    <a href="{{ post.url }}">Read more →</a>
  </article>
{% endfor %}


## Latest Posts 2

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
