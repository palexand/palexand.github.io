---
layout: frontpage
title: Teaching
---

# Courses

{% for course in site.data.teaching %}

## {{ course.name }}

-----

[{{ course.name }}](https://{{ course.github }}.github.io/{{ course.repo }}) - {{ course.description }}

{% endfor %}


