---
title: ratopi's Blog
description: Thoughts to make and do
layout: page
permalink: /blog.html
---

> "If you've never made a mistake, you've never tried anything new."
>
> — *Albert Einstein*

{% for post in site.posts %}
{% if post.draft != true %}
### [{{ post.title }}]({{ post.url }})

{% if post.abstract %}{{ post.abstract }}{% endif %}

*{{ post.date | date: "%B %-d, %Y" }}*

---
{% endif %}
{% endfor %}
