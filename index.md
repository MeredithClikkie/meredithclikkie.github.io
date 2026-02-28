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

- **[Main Blog](https://mdawg1981-tjlhe.wordpress.com)** - experiments + dashboards
- **[BreachLab](https://breachlab.mountainwaffles.com)** - experiments + dashboards
- **[Darkness](https://medium.com/@ending_glosses.26)** - experiments + dashboards
- **[Gravatar](https://meredith-smith.link)**


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
