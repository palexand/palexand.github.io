---
layout: frontblog
title: {{ site.title }}
---

# Coq Blog

{% for post in site.categories.coq %}

<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>

{{ post.date | date_to_string }}

<p>{{ post.excerpt }}</p>

<p><a href="{{ site.baseurl }}{{ post.url }}">More...</a></p>

-----

{% endfor %}
