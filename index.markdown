---
layout: default
title: Home
---

# Blog

<ul>
{% for post in site.posts limit: 5 %}
    <li>
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <p class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</p>
      <p>{{ post.excerpt }}</p>
    </li>
  {% endfor %}
</ul>
