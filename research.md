---
layout: frontpage
title: Research
---

# Active Projects

{% for project in site.data.projects %}

## {{ project.name }}

---

[{{ project.name }}](https://{{ project.github }}.github.io/{{ project.repo }}) - {{ project.description }}

Sponsors: {{ project.sponsor }}

{% endfor %}

# Inactive Projects

{% for project in site.data.inactive-projects %}

## {{ project.name }}

---

[{{ project.name }}](https://{{ project.github }}.github.io/{{ project.repo }}) - {{ project.description }}

Sponsors: {{ project.sponsor }}

{% endfor %}

# Information for Students

* Notes on writing [PhD Dissertation Proposals](phd-proposal)
* Notes on writing [papers](writing)
