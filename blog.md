---
layout: frontblog
title: {{ site.title }}
---

# Blog

I keep this blog of things related to interests outside work
in music, stereo gear, movies and what not.  This is the main blog
with exerpts from all posts.  Category specific listings can be found
in the sidebar.

{% for post in site.categories.blog %}

<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>

{{ post.date | date_to_string }}

<p>{{ post.excerpt }}</p>

<p><a href="{{ site.baseurl }}{{ post.url }}">More...</a></p>

-----

{% endfor %}
