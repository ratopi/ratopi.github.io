---
title: Project Updates
description: Releases, announcements, and notes on my projects
layout: page
permalink: /updates.html
---

> "Premature optimization is the root of all evil in programming."
>
> — *Donald Knuth*

{% for post in site.posts %}
{% if post.draft != true and post.category == "project" %}
### [{{ post.title }}]({{ post.url }})

{% if post.abstract %}{{ post.abstract }}{% endif %}

*{{ post.date | date: "%B %-d, %Y" }}*

---
{% endif %}
{% endfor %}
