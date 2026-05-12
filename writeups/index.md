
---
layout: page
title: CTF Writeups
permalink: /writeups/
---

A collection of my writeups organized by CTF competition.
{% assign ctfs = site.writeups | group_by: "ctf" | sort: "name" %}
<ul>
{% for ctf_group in ctfs %}
  {% assign ctf_name = ctf_group.name %}
  <li><a href="/writeups/{{ ctf_name | slugify | replace: '-', '' }}/">{{ ctf_name }}</a></li>
{% endfor %}
</ul>
