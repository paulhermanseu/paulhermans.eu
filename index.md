---
layout: default
title: Home
---

# Home

Welcome to the blog and website of Paul Hermans, former webhosting provider now in sabbatical.

## Latest Blog Posts

{% for post in site.posts %}
  <article>
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p class="post-meta">
      <span class="date">{{ post.date | date: "%B %d, %Y" }}</span>
      {% if post.categories %}
        | <span class="categories">{{ post.categories | join: ", " }}</span>
      {% endif %}
    </p>
  </article>
{% endfor %}
