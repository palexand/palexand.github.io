---
layout: frontblog
title: {{ site.title }}
---

# Gear Blog

My current setup for music:

* Bryston BDP-2 media player
* Rega RP-1 turntable with stock stylus
* Benchmark DAC1 D/A
* Audio Research LS26 preamp
* Parasound A21 amp
* Snell C/V speakers

{% for post in site.categories.gear %}

<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>

{{ post.date | date_to_string }}

<p>{{ post.excerpt }}</p>

<p><a href="{{ site.baseurl }}{{ post.url }}">More...</a></p>

-----

{% endfor %}
