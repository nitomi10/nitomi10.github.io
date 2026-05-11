---
layout: page
title: HCSC'26 Writeups
permalink: /writeups/hcsc26/
---

I took part in the Hungarian Cyber Security Challenge (HCSC) (https://hcsc.nki.gov.hu/) for the first time this year. The competition was strong and there were many challenges. I placed 18th in the Senior category and had a lot of fun playing this CTF and learned a lot. I'll definitely come back to play next year. Because there were so many challenges, I only created writeups for my top three favourites.

# HCSC'26 Challenges

{% assign challenges = site.writeups | where: "ctf", "HCSC'26" | sort: "date" | reverse %}

{% for challenge in challenges %}
- [{{ challenge.title }}]({{ challenge.url }}) - {{ challenge.category }}
{% endfor %}
