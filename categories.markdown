---
layout: page
title: Archive By Category
permalink: /categories/
---
{% assign all_categories = "" %}
{% for post in site.posts %}
  {% assign post_categories = post.categories | join:'|' %}
  {% assign all_categories = all_categories | append:post_categories | append:'|' %}
{% endfor %}

{% assign unique_categories = all_categories | split:'|' | uniq | sort %}

{% for category in unique_categories %}
  {% comment %} Skip empty strings if they exist after splitting/joining {% endcomment %}
  {% unless category == empty %}

    {% comment %} Find all posts where the post's categories array includes the current category {% endcomment %}
    {% assign posts_in_category = site.posts | where_exp: "post", "post.categories contains category" %}

<h2># {{ category  }} ({{ posts_in_category | size }})</h2>
<ul class="post-list">
{% for post in posts_in_category %}
<li>
<a href="{{ post.url | relative_url }}">{{ post.title }}</a>
<span class="post-date"> - {{ post.date | date: "%B %-d, %Y" }}</span>
</li>
{% endfor %}
</ul>
{% endunless %}
{% endfor %}