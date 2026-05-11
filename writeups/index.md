---
layout: page
title: Writeups
permalink: /writeups/
---

# CTF Writeups

A collection of my writeups organized by CTF competition.

{% assign ctfs = site.writeups | group_by: "ctf" | sort: "name" %}

{% for ctf_group in ctfs %}
  {% assign ctf_name = ctf_group.name %}
  {% assign challenges = ctf_group.items | sort: "date" | reverse %}
  
  ## {{ ctf_name }}
  
  {% for challenge in challenges %}
  - [{{ challenge.title }}]({{ challenge.url }})
  {% endfor %}
  
{% endfor %}
