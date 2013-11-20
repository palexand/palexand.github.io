---
layout: frontpage
title: Projects
---

# Active Projects

{% for project in site.data.projects %}

## {{ project.name }}

-----

[{{ project.name }}](http://{{ project.github }}.github.io/{{ project.repo }}) - {{ project.description }}

Sponsors: {{ project.sponsor }}

{% endfor %}

# Inactive Projects

