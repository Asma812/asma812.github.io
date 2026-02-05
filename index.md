---
layout: home
title: Welcome
---

<div class="container" markdown="1">

<!-- HERO – Ultra-Compact, One-Screen, Professional -->
<div style="text-align: center; padding: 3.5rem 1rem 2.5rem; max-width: 860px; margin: 0 auto;">
  <h1 style="font-family: 'JetBrains Mono', monospace; font-size: 2.8rem; margin: 0 0 0.5rem; color: var(--text); letter-spacing: -1px;">
    Asma NEJI
  </h1>

  <!-- 3-line real introduction -->
  <p style="font-size: 1.1rem; color: var(--text-muted); margin: 0 0 1.2rem; line-height: 1.5; max-width: 720px; margin-left: auto; margin-right: auto;">
    Junior Cybersecurity Engineer from Tunis with strong telecom & network background.<br>
    Focused on threat intelligence, secure 5G architectures, AI anomaly detection, and DevSecOps.<br>
    Passionate about turning defense theory into practical, proactive security solutions.
  </p>

  <!-- Cyber trick: OSINT leak warning – shows real impact of exposed PII -->
  <div style="margin: 1.4rem auto; max-width: 700px;">
    <pre style="background: var(--surface); color: #e63946; font-family: 'JetBrains Mono', monospace; padding: 1.2rem; border-radius: 8px; border: 1px solid var(--border); font-size: 0.95rem; line-height: 1.5; text-align: left; overflow-x: auto; margin: 1.5rem auto; max-width: 720px;">
┌───────────────────── PUBLIC OSINT LEAK WARNING ─────────────────────┐
│                                                                   │
│   Exposed PII detected in portfolio                               │
│                                                                   │
│   Name: Asma Neji                                                 │
│   Role: Junior Cybersecurity Engineer                             │
│                                                                   │
│   Phone: +216 97 *** ***                                          │
│   Email: asm****@gmail.com                                        │
│   Location: Tun**                                                 │
│                                                                   │
│ Real-world impact if fully public:                                │
│ • Targeted phishing / spear-phishing                              │
│ • SIM swap attacks → account takeover                             │
│ • Doxxing & physical location tracking                            │
│ • Stalking / harassment risk                                      │
│ • Social engineering leverage                                     │
│                                                                   │
│ Rule #1 in cybersecurity: Never expose PII in public.             │
│ Secure the signal. Defend the spectrum.                           │
└───────────────────────────────────────────────────────────────────┘
    </pre>
  </div>

  <!-- Logo-only buttons – official style, no text -->
  <div style="display: flex; justify-content: center; gap: 2.5rem; margin-top: 1.6rem;">
    <a href="https://linkedin.com/in/asma-neji" 
       style="color: #0a66c2; font-size: 2.4rem; text-decoration: none; transition: transform 0.3s;">
      in
    </a>
    <a href="https://github.com/Asma812" 
       style="color: #ffffff; font-size: 2.4rem; text-decoration: none; transition: transform 0.3s;">
      <span style="font-size: 2.6rem;">🐙</span>
    </a>
    <a href="/assets/cv/AsmaNEJI_CV.pdf" 
       style="color: var(--text); font-size: 2.4rem; text-decoration: none; transition: transform 0.3s;">
      📄
    </a>
  </div>
</div>

<!-- Latest Articles -->
<h2 style="text-align: center; color: var(--accent); font-family: 'JetBrains Mono', monospace; margin: 5rem 0 3rem;">Latest Articles</h2>

{% for post in site.posts limit:5 %}
<div class="card" style="margin: 2rem 0;">
  <h3 style="margin: 0; color: var(--accent);">
    <a href="{{ post.url }}" style="text-decoration: none;">{{ post.title }}</a>
  </h3>
  <p style="color: var(--text-muted); font-size: 1rem; margin: 0.8rem 0;">
    {{ post.date | date: "%B %d, %Y" }} • {{ post.categories | join: " • " }}
  </p>
  <p style="margin: 1.2rem 0 0; color: var(--text);">
    {{ post.excerpt | strip_html | truncate: 180 }}
  </p>
</div>
{% endfor %}

<div style="text-align: center; margin: 4rem 0;">
  <a href="/blog" style="color: var(--accent); font-size: 1.4rem; font-weight: 600; text-decoration: none;">
    View All Articles →
  </a>
</div>

<!-- Featured Projects -->
<h2 style="text-align: center; color: var(--accent); font-family: 'JetBrains Mono', monospace; margin: 6rem 0 3rem;">Featured Projects</h2>

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(340px, 1fr)); gap: 2.5rem; margin: 0 0 5rem;">
  <div class="card">
    <h3 style="color: var(--red); margin-top: 0;">Cyber Threat Intelligence Platform</h3>
    <p style="color: var(--text-muted);">Neo4j knowledge graph • ML anomaly detection • MITRE ATT&CK • Dash/Flask • Docker</p>
    <a href="/about/#professional-experience" style="color: var(--red); font-weight: 600;">View Details →</a>
  </div>
  <div class="card">
    <h3 style="color: var(--green); margin-top: 0;">DevSecOps Pipeline & XDR</h3>
    <p style="color: var(--text-muted);">Jenkins • SonarQube • OWASP ZAP • Wazuh • TheHive • OpenCTI</p>
    <a href="/about/#professional-experience" style="color: var(--green); font-weight: 600;">View Details →</a>
  </div>
  <div class="card">
    <h3 style="color: var(--purple); margin-top: 0;">Virtualized 5G Network Optimization</h3>
    <p style="color: var(--text-muted);">SDN • NFV • AI • Blockchain • OpenDaylight • Open5GS • TensorFlow</p>
    <a href="/about/#academic-projects" style="color: var(--purple); font-weight: 600;">View Details →</a>
  </div>
</div>

<div style="text-align: center; margin: 5rem 0;">
  <a href="/about" style="color: var(--accent); font-size: 1.5rem; font-weight: 600; text-decoration: none;">
    See Full Portfolio →
  </a>
</div>

<!-- Telecom & Contact -->
<div style="text-align: center; margin: 6rem 0;">
  <p style="font-size: 1.3rem; color: var(--text-muted);">
    Explore my academic journey in telecom engineering:<br>
    <a href="/telecom" style="color: var(--accent); font-weight: 600;">Telecom Lessons →</a>
  </p>
  <p style="font-size: 1.4rem; margin-top: 3rem;">
    <a href="/contact" style="color: var(--accent); font-weight: 600;">Get in touch</a>
  </p>
</div>

</div>
