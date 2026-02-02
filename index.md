---
layout: home
title: Welcome
---

<!-- HERO SECTION -->
<div style="text-align: center; padding: 6rem 1rem 4rem;">
  <h1 style="color: #ffffff; font-size: 4.5rem; margin: 0; font-family: 'JetBrains Mono', monospace; letter-spacing: -3px; text-shadow: 0 0 60px #58a6ffaa;">
    Asma NEJI
  </h1>

  <p style="color: #58a6ff; font-size: 2.2rem; margin: 1.5rem 0; font-weight: 700;">
    Junior Cybersecurity Engineer
  </p>

  <p style="color: #a5d6ff; font-size: 1.5rem; margin: 1rem auto; max-width: 900px;">
    Passionate Junior Cybersecurity Engineer from Tunis, blending deep telecommunications knowledge with cutting-edge security practices. Specialized in AI-powered threat detection, secure 5G architectures, DevSecOps automation, and proactive defense.
  </p>

  <div style="margin-top: 3rem; display: flex; justify-content: center; gap: 3rem; flex-wrap: wrap;">
    <span style="color: #c9d1d9; font-size: 1.3rem;">+216 97 322 007</span>
    <a href="mailto:asmaneji20@gmail.com" style="color: #58a6ff; font-size: 1.3rem; text-decoration: none;">
      asmaneji20@gmail.com
    </a>
    <span style="color: #c9d1d9; font-size: 1.3rem;">Tunis, Tunisia</span>
  </div>

  <div style="margin-top: 4rem; display: flex; justify-content: center; gap: 2.5rem; flex-wrap: wrap;">
    <a href="https://linkedin.com/in/asma-neji" style="color: #ffffff; background: linear-gradient(90deg, #0a66c2, #1e88e5); padding: 1.1rem 2.8rem; border-radius: 50px; text-decoration: none; font-weight: 700; font-size: 1.2rem;">
      LinkedIn
    </a>
    <a href="https://github.com/Asma812" style="color: #ffffff; background: linear-gradient(90deg, #171515, #2e2e2e); padding: 1.1rem 2.8rem; border-radius: 50px; text-decoration: none; font-weight: 700; font-size: 1.2rem;">
      GitHub
    </a>
    <a href="/assets/cv/AsmaNEJI_CV.pdf" style="color: #ffffff; background: linear-gradient(90deg, #238636, #2ea043); padding: 1.1rem 2.8rem; border-radius: 50px; text-decoration: none; font-weight: 700; font-size: 1.2rem;">
      Download CV
    </a>
  </div>
</div>

<div class="container">

{: .notice--success}
## Latest Articles
{% for post in site.posts limit:5 %}
<div style="margin: 2rem 0; padding: 1.5rem; background: #161b22; border-radius: 12px; border-left: 4px solid #58a6ff; transition: all 0.3s; box-shadow: 0 4px 15px rgba(88,166,255,0.1);">
  <h3 style="margin: 0 0 0.5rem 0; color: #58a6ff;">
    <a href="{{ post.url }}" style="text-decoration: none; color: inherit;">{{ post.title }}</a>
  </h3>
  <p style="color: #8b949e; font-size: 0.95rem; margin: 0.5rem 0;">
    {{ post.date | date: "%B %d, %Y" }} • {{ post.categories | join: " • " }}
  </p>
  <p style="margin: 1rem 0 0 0; color: #c9d1d9;">{{ post.excerpt | strip_html | truncate: 160 }}</p>
</div>
{% endfor %}
<div style="text-align: center; margin: 3rem 0;">
  <a href="/blog" style="color: #58a6ff; font-size: 1.3rem; font-weight: 600; text-decoration: none;">View All Articles →</a>
</div>

{: .notice--info}
## Featured Projects
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 2rem; margin: 3rem 0;">
  <div style="background: #161b22; border-radius: 16px; padding: 2rem; border: 1px solid #30363d; box-shadow: 0 10px 30px rgba(88,166,255,0.2); transition: all 0.4s;">
    <h3 style="color: #58a6ff; margin-top: 0;">Cyber Threat Intelligence Platform</h3>
    <p style="color: #c9d1d9; margin: 1rem 0;">Neo4j knowledge graph • ML anomaly detection • MITRE ATT&CK • Dash/Flask • Docker</p>
    <a href="/about/#professional-experience" style="color: #58a6ff; font-weight: 600;">View Details →</a>
  </div>
  <div style="background: #161b22; border-radius: 16px; padding: 2rem; border: 1px solid #30363d; box-shadow: 0 10px 30px rgba(35,134,54,0.2); transition: all 0.4s;">
    <h3 style="color: #238636; margin-top: 0;">DevSecOps Pipeline & XDR</h3>
    <p style="color: #c9d1d9; margin: 1rem 0;">Jenkins • SonarQube • OWASP ZAP • Wazuh • TheHive • OpenCTI</p>
    <a href="/about/#professional-experience" style="color: #238636; font-weight: 600;">View Details →</a>
  </div>
  <div style="background: #161b22; border-radius: 16px; padding: 2rem; border: 1px solid #30363d; box-shadow: 0 10px 30px rgba(0,212,255,0.2); transition: all 0.4s;">
    <h3 style="color: #00d4ff; margin-top: 0;">Virtualized 5G Network Optimization</h3>
    <p style="color: #c9d1d9; margin: 1rem 0;">SDN • NFV • AI • Blockchain • OpenDaylight • Open5GS • TensorFlow</p>
    <a href="/about/#academic-projects" style="color: #00d4ff; font-weight: 600;">View Details →</a>
  </div>
</div>
<div style="text-align: center; margin: 4rem 0;">
  <a href="/about" style="color: #58a6ff; font-size: 1.4rem; font-weight: 600; text-decoration: none;">See Full Portfolio →</a>
</div>

### Telecom Background
Explore my academic journey in telecom engineering: [Telecom Lessons →](/telecom)

[Get in touch](/contact)
</div>
