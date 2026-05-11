---
layout: page
title: Template CTF Writeups
permalink: /writeups/template-ctf/
---

# Template CTF Challenges

{% assign challenges = site.writeups | where: "ctf", "Template CTF" | sort: "date" | reverse %}

{% for challenge in challenges %}
- [{{ challenge.title }}]({{ challenge.url }}) - {{ challenge.category }}
{% endfor %}
