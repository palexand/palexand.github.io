---
layout: frontpage
title: Dr. Perry Alexander
---

**Dr. Perry Alexander** is a Professor in the Department of Electrical
and Computer Engineering and Director of the Information and
Telecommunication Technology Center at the University of Kansas.

# Information

-----

Information and Telecommunication Technology Center
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
: 785-864-7741 (Voice)
: 785-864-0387 (FAX)
: perry_alexander (skype)
: [GPG Public Key](resources/PerryAlexander.asc)

<ul>
{% for class in site.teaching %}
{% if time == nil %}
{% else %}
<li>{{class.name}} at {{ class.time }} in {{ class.place }}</li>
{% endif %}
{% endfor %}
</ul>

# Research Interests

----

Research interests include applied formal methods, system-level
design, design and specification language semantics, and component
retrieval. For more information, visit my [research](research)
or the [SLDG](http://ku-sldg.github.io) pages.

# Teaching Interests

----

Teaching interests include formal methods, programming languages and
semantics, digital systems design and software engineering. For more
information, visit my [teaching](teaching) pages.

