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

  <h2>{{ ctf_name }}</h2>

  <ul>
  {% for challenge in challenges %}
    <li><a href="{{ challenge.url }}">{{ challenge.title }}</a></li>
  {% endfor %}
  </ul>

{% endfor %}
