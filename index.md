---
layout: default
title: Snapback
---

# Welcome to Snapback project. This site is currently being configured and deployed.

## What this project will include
- Documentation
- Feature roadmap
- Release notes
- Live demos (coming soon)
  
## Explore the Ecosystem

- **[Wordpress](https://momentismedical.dev)** - longform writing + updates
- **[BreachLab](https://breachlab.momentismedical.dev)** - experiments + dashboards
- **[Medium](https://medium.com/@Snapback17)** - secondary blog

## Latest Updates
Content will appear here as the site deploys.
## All Posts (Automatic List)
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
