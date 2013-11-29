---
layout: frontpage
title: {{ site.title }}
---

# Blog

{% for post in site.categories.gear %}

<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>

{{ post.date | date_to_string }}

{{ post.excerpt }}

-----

{% endfor %}