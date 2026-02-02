---
layout: page
title: Articles & Insights
permalink: /blog/
---

Insights on cybersecurity, threat intelligence, AI in networks, telecom security, and more.

## Security Reports & Writeups
(Placeholder for future additions—add links to reports as you complete them)  
- Bug Bounty Report Example: [Link to report/writeup]  
- Pentest Report Example: [Link to report/writeup]  
- Hardening Project: [Link to writeup]

{% for post in site.posts %}
<article>
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p>{{ post.date | date: "%b %-d, %Y" }} • {{ post.excerpt | strip_html | truncatewords: 30 }}</p>
</article>
{% endfor %}
