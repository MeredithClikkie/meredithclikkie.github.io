---
layout: default
title: Home
---

# Welcome to snap_back

## All Posts (Automatic List)
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
