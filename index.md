---
layout: frontpage
title: Dr. Perry Alexander
---

I am the AT&T Foundation Distinguished Professor of Electrical and
Computer Science and Director of the Institute for Information
Sciences at the University of Kansas.  My research and teaching
interests include formal verification and synthesis, trusted systems,
and programming language semantics.

# Information
-----

Institute for Information Sciences
: The University of Kansas
: Nichols Hall
: 2335 Irving Hill Rd
: Lawrence, KS 66045

Department of Electrical Engineering and Computer Science
: The University of Kansas
: 2001 Eaton Hall
: 1520 West 15th Street
: Lawrence, KS 66045-7621

Contact
: palexand \[at\] ku \[dot\] edu
: 785-864-7741 (Voice)
: 785-864-0387 (FAX)
: [ORCID](https://orcid.org/0000-0002-5387-9157)
: [GPG Public Key]({{ site.baseurl }}/resources/PerryAlexander.asc)

<dl>
<dt>Current Courses and Office Hours</dt>
{% for course in site.data.teaching %}
{% if course.when == nil %}
{% else %}
<dd><a href="https://{{ course.github }}.github.io/{{ course.repo }}">{{ course.name }}</a> - {{ course.when }} in {{ course.where }}</dd>
{% endif %}
{% endfor %}
<dd>Office Hours - {{ site.ohrs }} in {{ site.ohrsoff }}</dd>
</dl>

# Teaching
----
My teaching interests include formal methods, programming languages
and semantics, digital systems design and software engineering. For
more information on courses I teach, visit my [teaching](teaching)
pages.

# Research
----
My research interests include formal methods, system-level design,
trusted computing, design and specification language semantics, and
component retrieval. For more information on my research, visit my 
[research](research) or the [SLDG](http://ku-sldg.github.io) pages.

> “Barba non facit philosophum” (A beard does not make one a philosopher)

# Personal
----
Personal interests include music and stereo gear, running and yoga.
For more information on what I do for fun and where I come from, visit
my [personal](personal) pages. 

# Vita
----
My full [vita]({{ site.baseurl }}/resources/vitae.pdf) should you be
interested.

