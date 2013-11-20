---
layout: frontpage
title: Teaching
---

# Courses

{% for course in site.data.teaching %}

## {{ course.name }}

-----

[{{ course.name }}](http://{{ course.github }}.github.io/{{ course.repo }}) - {{ course.description }}

{% endfor %}

# Inactive Projects

