---
layout: page
title: Articles & Insights
permalink: /blog/
---

Insights on cybersecurity, threat intelligence, AI in networks, telecom security, and more.

## Security Reports & Writeups

(Click a card to read the full report or write-up)

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(340px, 1fr)); gap: 2rem; margin: 3rem 0;">
  <!-- Card 1: Bug Bounty -->
  <div class="card" style="background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 1.8rem; transition: all 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.15);">
    <h3 style="margin: 0 0 0.8rem; color: var(--red); font-size: 1.35rem;">
      Bug Bounty Report – [Target / Vulnerability Name]
    </h3>
    <p style="color: var(--text-muted); font-size: 0.95rem; margin: 0 0 1rem;">
      Severity: Critical • Bounty: $$$ • Date: [Month Year]
    </p>
    <p style="margin: 0 0 1.2rem;">
      Discovered [vulnerability type] in [target scope]. Impact: [brief impact]. Full report includes PoC, remediation steps, and bounty details.
    </p>
    <a href="[link-to-report-or-writeup]" style="color: var(--red); font-weight: 600; text-decoration: none;">Read Full Report →</a>
  </div>

  <!-- Card 2: Pentest -->
  <div class="card" style="background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 1.8rem; transition: all 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.15);">
    <h3 style="margin: 0 0 0.8rem; color: var(--accent); font-size: 1.35rem;">
      Penetration Test Report – [Client / Scope Name]
    </h3>
    <p style="color: var(--text-muted); font-size: 0.95rem; margin: 0 0 1rem;">
      Scope: [External/Internal/Web/API] • Findings: 1× Critical, 3× High • Date: [Month Year]
    </p>
    <p style="margin: 0 0 1.2rem;">
      Comprehensive external/internal pentest with OSINT, scanning, exploitation, and post-exploitation phases. Key vulnerabilities and remediation recommendations included.
    </p>
    <a href="[link-to-report-or-writeup]" style="color: var(--accent); font-weight: 600; text-decoration: none;">Read Full Pentest Report →</a>
  </div>

  <!-- Card 3: Hardening Project -->
  <div class="card" style="background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 1.8rem; transition: all 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.15);">
    <h3 style="margin: 0 0 0.8rem; color: var(--green); font-size: 1.35rem;">
      Infrastructure Hardening Project – [System / Environment Name]
    </h3>
    <p style="color: var(--text-muted); font-size: 0.95rem; margin: 0 0 1rem;">
      Environment: [Linux/AD/Cloud] • Standards: CIS/NIST • Date: [Month Year]
    </p>
    <p style="margin: 0 0 1.2rem;">
      Hardening of servers/network using Ansible, Wazuh, OpenSCAP. Before/after state, applied configurations, and validation scans.
    </p>
    <a href="[link-to-writeup-or-report]" style="color: var(--green); font-weight: 600; text-decoration: none;">Read Full Hardening Write-up →</a>
  </div>
</div>

<!-- Latest Articles / Blog Posts – also in cards -->
<h2 style="margin: 6rem 0 2.5rem; color: var(--accent); font-family: 'JetBrains Mono', monospace; text-align: center;">Latest Articles</h2>

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(340px, 1fr)); gap: 2rem;">
  {% for post in site.posts %}
  <div class="card" style="padding: 1.8rem; background: var(--surface); border: 1px solid var(--border); border-radius: 12px; transition: all 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.15);">
    <h3 style="margin: 0 0 0.8rem; font-size: 1.35rem;">
      <a href="{{ post.url }}" style="color: var(--accent); text-decoration: none;">{{ post.title }}</a>
    </h3>
    <p style="color: var(--text-muted); font-size: 0.95rem; margin: 0 0 1rem;">
      {{ post.date | date: "%b %-d, %Y" }} • {{ post.categories | join: " • " }} • ~{{ post.content | number_of_words }} words
    </p>
    <p style="margin: 0; color: var(--text);">
      {{ post.excerpt | strip_html | truncatewords: 35 }}
    </p>
  </div>
  {% endfor %}
</div>

<div style="text-align: center; margin: 4rem 0;">
  <a href="/blog" style="color: var(--accent); font-size: 1.3rem; font-weight: 600; text-decoration: none;">
    View All Articles →
  </a>
</div>
