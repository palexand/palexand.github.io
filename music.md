---
layout: frontpage
title: {{ site.title }}
---

# Music Blog

{% for post in site.categories.music %}

<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>

{{ post.date | date_to_string }}

<p>{{ post.excerpt }}<p>

<p><a href="{{ site.baseurl }}{{ post.url }}">More...</a><p>

-----

{% endfor %}
