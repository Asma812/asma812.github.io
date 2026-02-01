---
layout: home
title: Welcome
---

# Hi, I'm Asma Neji

Junior Cybersecurity Engineer based in Tunisia, with a background in telecommunications and networks. I specialize in threat intelligence, security automation, penetration testing, and AI/ML for anomaly detection in secure infrastructures.

Passionate about integrating AI with cybersecurity in telecom environments, such as 5G networks and DevSecOps pipelines.

### Latest Articles
{% for post in site.posts limit:3 %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%b %-d, %Y" }}
{% endfor %}

→ [Read all articles →](/blog)

### Featured Projects
- [Cyber Threat Intelligence System with Neo4j & ML](https://github.com/Asma812/cti-system) — Designed a knowledge graph for threat analysis.
- [DevSecOps Pipeline](https://github.com/Asma812/devsecops-pipeline) — Automated security with Jenkins, SonarQube, and OWASP ZAP.
- [5G Network Optimization with SDN, NFV, AI & Blockchain](https://github.com/Asma812/5g-optimization) — Virtualized network using OpenDaylight, TensorFlow, and more.

[View all projects, certs, and experience in About →](/about)

[Get in touch](/contact)
