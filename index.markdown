---
layout: default
title: Home
---
This is the personal site of Iain Cambridge, a software developer based in Berlin. Who in his spare time works on the Open Source project <a href="https://github.com/getparthenon" target="_blank">Parthenon</a> and the Source Avaulable billing project <a href="https://github.com/billabear" target="_blank">BillaBear.</a>

You can contact me at iain@iain.rocks. 

# Latest Blog Posts

I blog about all aspects of software development. From software processes to recruitment to technical debugging posts. Here are some of my latest blog posts.

<ul>
{% for post in site.posts limit: 5 %}
    <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%b %-d, %Y" }}
    </li>
  {% endfor %}
</ul>
