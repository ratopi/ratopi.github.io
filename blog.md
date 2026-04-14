---
title: ratopi's Blog
description: Thoughts to make and do
layout: page
permalink: /blog.html
---

> "If you've never made a mistake, you've never tried anything new."
>
> — *Albert Einstein*

{% comment %}Collect paths of German posts that have an English partner — skip them in the list{% endcomment %}
{% assign skip_paths = "" %}
{% for post in site.posts %}
  {% if post.lang_partner and post.lang == "de" and post.category == "blog" %}
    {% assign skip_paths = skip_paths | append: post.path | append: "|||" %}
  {% endif %}
{% endfor %}

{% for post in site.posts %}
{% if post.draft != true and post.category == "blog" %}
{% if skip_paths contains post.path %}{% continue %}{% endif %}

### [{{ post.title }}]({{ post.url }})

{% if post.abstract %}{{ post.abstract }}{% endif %}

*{{ post.date | date: "%B %-d, %Y" }}*

---

{% endif %}
{% endfor %}
