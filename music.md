---
layout: frontpage
title: {{ site.title }}
---

# Music Blog

{% for post in site.categories.music %}

<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>

{{ post.date | date_to_string }}

{{ post.excerpt }}

<a href="{{ site.baseurl }}{{ post.url }}">More...</a>

-----

{% endfor %}
