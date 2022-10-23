---
layout: frontblog
title: {{ site.title }}
---

# Gear Blog

My current home setup for music:

* Roon Nucleus Media Player
* Pro-Ject Carbon 3 Turntable
* Sumiko Moonstone Cartridge 
* Parasound Zphono XRM MM/MC Phono Preamp
* Benchmark DAC2 D/A and Preamp
* Symmetra SymNet 8x8 DSP Crossover
* ATI AT3000 Amplifiers
* Custom Russ Berger Design Group studio monitors

My current work system includes:

* Benchmark DAC1 D/A
* Bryston 3NRB amp
* PSB Alpha speakers
* Focal Elegea headphones

{% for post in site.categories.gear %}

<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>

{{ post.date | date_to_string }}

<p>{{ post.excerpt }}</p>

<p><a href="{{ site.baseurl }}{{ post.url }}">More...</a></p>

-----

{% endfor %}
