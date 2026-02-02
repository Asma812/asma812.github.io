---
layout: default
title: About Me
permalink: /about/
---

**Asma NEJI**  
Junior Cybersecurity Engineer  
+216 97 322 007 • asmaneji20@gmail.com • Tunis, Tunisia  

[LinkedIn](https://linkedin.com/in/asma-neji) • [GitHub](https://github.com/Asma812) • [CV (PDF)](/assets/cv/AsmaNEJI_CV.pdf)

{: .notice--primary}

## Bio
Asma Neji, Junior Cybersecurity Engineer with expertise in telecommunications, networks, and AI. Experienced in building secure systems, threat intelligence, and AI-driven anomaly detection. Based in Tunisia.

{: .notice--info}

## Skills

| Category   | Key Skills                                                                 |
|------------|----------------------------------------------------------------------------|
| Networking | Cisco Packet Tracer, Huawei eNSP, TCPDump, OpenVPN, NS3, Omnet++, Wireshark, OpenSSL |
| Systems    | Linux (Ubuntu, Kali), Windows Server                                       |
| Languages  | Python, Bash/Shell, SQL, C, C++, Java                                      |
| DevOps     | Ansible, Shell Scripting, Docker, SonarQube, Jenkins                       |

**Security Skills**  
- Threat intelligence  
- Pentesting: Nmap, Burp Suite, OWASP ZAP, Metasploit, Nessus/OpenVAS  
- Network security  
- Infrastructure hardening  
- Security automation  
- Incident response  
- Bug Bounty: Burp Suite, OWASP ZAP, Amass, Gobuster, Postman for APIs

{: .notice--success}

## Education

- **2022-2025**: Higher Institute of Computer Science, Tunisia  
  Engineering in Computer Science, Engineering and Development of Communications Infrastructures and Services  
- **2019-2022**: Higher Institute of Information and Communication Technologies, Tunisia  
  Bachelor in Information and Communication Technologies, Telecommunications

{: .notice--warning}

## Professional Experience

<details>
  <summary>Cyber Threat Intelligence Intern – TUDIGISEC by Nomios (Feb 2025 – Jun 2025)<br>Tools: Neo4j, ML/graph algorithms, MITRE ATT&CK, regex/NLP/transformers, Dash, Flask, Docker</summary>

  I took ownership of designing a full Cyber Threat Intelligence (CTI) system from the ground up, treating the organization’s scattered threat data sources as a disconnected puzzle that needed unification.  
  **Core Thinking & Architecture**  
  I chose Neo4j as the central knowledge graph engine because traditional relational databases struggle with the highly relational nature of threat actors, campaigns, indicators, and infrastructure. The graph model allowed me to naturally represent attacker TTPs, victim assets, and enrichment sources as interconnected nodes and relationships.  
  The architecture followed a modular ingestion → processing → analysis → visualization pipeline:  
  - Multi-source ingestion: Social media streams, OSINT feeds, internal honeypots, and curated dark web datasets.  
  - Entity extraction layer: Custom regex + NLP pipelines (transformers for named entity recognition) to turn unstructured text into structured triples.  
  - Semantic enrichment: Mapped everything to MITRE ATT&CK framework using graph patterns to link tactics, techniques, and procedures across sources.  
  - Anomaly & trend detection: Combined graph algorithms (PageRank for influential actors, community detection for campaign clustering) with lightweight ML models for outlier scoring.  
  - Output layer: Real-time dashboard (Dash) for interactive exploration + Flask API for programmatic access and STIX 2.1 export.  
  **PoC Highlights**  
  - Built a prototype that ingested sample dark-web paste data, extracted IOCs, linked them to known campaigns via ATT&CK, and visualized emerging clusters in under a week.  
  - Dockerized the entire stack (Neo4j + Python workers + Dash/Flask) for reproducible deployment and scalability testing.  
  This wasn't just data collection—it was turning noisy intelligence into actionable, graph-queryable knowledge that could support proactive defense decisions.

  [GitHub Repo](https://github.com/Asma812/cti-tudigisec) <!-- Replace with real repo link -->
</details>

<details>
  <summary>DevSecOps Intern – ARRIBATT FZCO (Jul 2024 – Aug 2024)<br>Tools: Jenkins, SonarQube, OWASP ZAP, n8n, Wazuh, TheHive, Cortex, OpenCTI, Nmap</summary>

  I focused on bridging development speed with security without creating bottlenecks, designing a "shift-left" pipeline that caught issues early while maintaining developer velocity.  
  **Core Thinking & Architecture**  
  Recognized that security checks needed to be automated, non-intrusive, and integrated into existing workflows. Built a Jenkins-based CI/CD pipeline with parallel security gates.  
  Key architectural choices:  
  - Static & dynamic analysis early: SonarQube for code quality + OWASP ZAP for DAST during build/test stages.  
  - Dependency & container scanning: Integrated OWASP Dependency-Check and container tools to prevent vulnerable components from reaching production.  
  - Runtime monitoring & response: Deployed and tuned Wazuh agents across environments for host log collection, file integrity monitoring, and active response.  
  - Incident orchestration: Connected Wazuh alerts to TheHive (case management), Cortex (analyzers/enrichment), and OpenCTI (threat intel sharing) to form a lightweight XDR-like loop.  
  - Automation glue: Used n8n for low-code workflows that triggered alerts, enriched data, and notified teams.  
  **PoC Highlights**  
  - Created a demo pipeline that took a sample vulnerable app → ran SonarQube → blocked on critical issues → scanned dependencies → performed automated ZAP scans → forwarded findings to TheHive/OpenCTI.  
  - Configured Wazuh rules to detect common attack patterns and auto-quarantine suspicious processes.  
  The result was a pipeline that didn't just "add security"—it embedded it as a natural part of delivery, reducing mean-time-to-remediate through automation.

  [GitHub Repo](https://github.com/Asma812/devsecops-arribatt) <!-- Replace with real repo link -->
</details>

<details>
  <summary>Cyber Threat Intelligence Intern – SAMA PARTNERS BUSINESS SOLUTIONS SARL (Aug 2023)<br>Tools: AIL framework, dark web analysis tools</summary>

  This short but intense internship gave me my first deep dive into the dark web as an intelligence source, shifting my mindset from reactive monitoring to proactive hunting.  
  **Core Thinking & Architecture**  
  I approached the dark web not as a chaotic space but as a structured ecosystem with discoverable patterns (markets, forums, leak sites, paste services). The goal was to evaluate tools for scalable, ethical collection and classification.  
  Focused on the AIL (Analysis Information Leak) framework:  
  - Explored its modular crawler architecture for ingesting pastes, hidden services, and protected forums.  
  - Tested extraction logic for IOCs (credentials, hashes, domains) and classification (leak type, sensitivity).  
  - Analyzed how AIL handles unstructured streams → correlates items → flags high-value intelligence.  
  **PoC Highlights**  
  - Ran controlled tests on sample paste sites and Tor onions → evaluated recall/precision for credential leaks and vulnerability mentions.  
  - Mapped dark web communication flows (onion routing, protocol behaviors) to understand evasion techniques.  
  This experience taught me how to think adversarially: understand attacker infrastructure to better defend against it.

  [GitHub Repo](https://github.com/Asma812/cti-sama) <!-- Replace with real repo link -->
</details>

<details>
  <summary>Cyber Security Intern – RIADVICE (Jan 2022 – May 2022)<br>Tools: Wazuh, ModSecurity, ClamAV, AIDE, Tiger, Fail2Ban, Ansible</summary>

  My first hands-on hardening project—focused on turning a standard server environment into a defensible one using open-source tools and automation.  
  **Core Thinking & Architecture**  
  Adopted a layered defense model (CIS benchmarks as baseline) with emphasis on visibility, prevention, and response.  
  Key decisions:  
  - Central visibility: Deployed Wazuh as the SIEM core for log aggregation, FIM, rootkit detection, and active response.  
  - Web & host protection: Integrated ModSecurity (WAF rules), ClamAV (malware scanning), AIDE (file integrity), Tiger (security auditing), and Fail2Ban (brute-force blocking).  
  - Automation-first: Wrote Ansible playbooks to enforce configurations, deploy agents, and apply hardening policies consistently across servers.  
  - Alerting loop: Configured webhook-based alerts from Wazuh to external channels for rapid incident handling.  
  **PoC Highlights**  
  - Built a hardened prototype server: Applied CIS Level 1 benchmarks → layered tools → simulated attacks (brute-force, web exploits) → verified blocks/alerts.  
  - Developed Ansible roles that idempotently managed authentication hardening (key-only SSH, password policies).  
  This internship solidified my belief in infrastructure-as-code for security: repeatable, auditable, and scalable hardening.

  [GitHub Repo](https://github.com/Asma812/hardening-riadvice) <!-- Replace with real repo link -->
</details>

{: .notice--success}

## Certifications

- [API Security Fundamentals (2025)](https://www.apisecuniversity.com/courses/api-security-fundamentals)
- [Microsoft Certified: Azure Fundamentals (2024)](https://learn.microsoft.com/en-us/credentials/certifications/azure-fundamentals)
- [Microsoft Certified: Security, Compliance, and Identity Fundamentals (2024)](https://learn.microsoft.com/en-us/credentials/certifications/security-compliance-and-identity-fundamentals)
- [Microsoft Certified: Azure Data Fundamentals (2024)](https://learn.microsoft.com/en-us/credentials/certifications/azure-data-fundamentals)
- [Cisco CCNA (2024)](https://cp.certmetrics.com/cisco/en/public/verify/credential)
- [Secure your network with VPNs and Firewalls - OpenClassrooms (2024)](https://openclassrooms.com/en/courses/7075956-secure-your-network-with-vpns-and-firewalls)
- [Secure your infrastructure - OpenClassrooms (2024)](https://openclassrooms.com/en/courses/8395341-secure-your-active-directory-and-windows-domains)

{: .notice--danger}

## Academic Projects

<details>
  <summary>Optimizing a Virtualized 5G Network with SDN, NFV, AI & Blockchain<br>Tools: OpenDaylight, Open5GS, TensorFlow, Docker, Hyperledger Fabric, Prometheus, Grafana</summary>

  **End-of-studies engineering project (2024–2025)**  
  This was my most ambitious academic work: building a complete virtualized 5G end-to-end prototype that combined modern network softwarization with intelligent automation and trust mechanisms.  
  **Core Thinking & Architecture**  
  I wanted to demonstrate that 5G can be more than high-speed connectivity — it can become a programmable, self-optimizing, and tamper-resistant platform.  
  I chose a fully disaggregated architecture:  
  - **SDN control plane** → OpenDaylight as the central brain (southbound OpenFlow → Open5GS core elements)  
  - **NFV data plane** → Containerized 5G core functions (UPF, AMF, SMF) running on Docker + Kubernetes-like orchestration  
  - **AI-driven optimization layer** → TensorFlow models continuously analyzing Prometheus metrics (latency, throughput, handover success rate, resource utilization) to predict congestion and dynamically adjust slicing parameters and traffic steering  
  - **Blockchain trust layer** → Hyperledger Fabric to record critical network events (slice creation/modification, handover decisions, SLA compliance) in an immutable ledger — providing auditability and preventing fraudulent manipulation of network policies  
  **PoC Highlights & Innovations**  
  - Implemented network slicing with dynamic QoS enforcement (e.g., low-latency slice for URLLC, high-throughput for eMBB)  
  - Trained lightweight ML models to detect anomalies and proactively re-balance resources before degradation occurred  
  - Demonstrated end-to-end visibility with Grafana dashboards showing real-time slice performance + blockchain transaction log  
  - Proved concept of “trust-by-design” — any unauthorized slice modification attempt would be detectable via ledger inconsistency  
  Instead of a GitHub repository, this work is documented in a detailed technical article that covers architecture diagrams, configuration examples, ML training process, and performance results.  
  [GitHub Repo](https://github.com/Asma812/5g-optimization) <!-- Replace with real repo link if available -->
</details>

<details>
  <summary>Intelligent Inventory Management System<br>Tools: Python, C/C++, STM32, Nodemcu, ThingSpeak</summary>

  **Multi-disciplinary project (embedded + cloud)**  
  Goal: create a low-power, real-time inventory tracking solution suitable for warehouses or retail environments.  
  **Approach & Architecture**  
  I decided to combine microcontroller-level sensing with cloud-based analytics and visualization.  
  - Edge layer: STM32 + NodeMCU (ESP8266) collecting RFID / weight sensor data  
  - Communication: MQTT to ThingSpeak cloud  
  - Backend: Python scripts performing data cleaning, trend analysis, and low-stock alerts  
  - Frontend: Simple dashboard showing live inventory levels and movement history  
  **PoC Highlights**  
  - Achieved sub-second update latency from sensor to cloud dashboard  
  - Implemented basic predictive restocking alerts based on historical consumption patterns  
  - Demonstrated energy-efficient duty cycling on battery-powered nodes  
  [GitHub Repo](https://github.com/Asma812/inventory-system) <!-- Replace with real repo link if available -->
</details>

<details>
  <summary>Drowsiness Detector based on Image Processing & AI<br>Tools: Python, Raspberry Pi, OpenCV, custom CNN, Flask</summary>

  **Computer vision + embedded project**  
  Goal: real-time driver drowsiness detection using affordable hardware.  
  **Approach & Architecture**  
  Chose a hybrid edge-cloud model to balance latency and accuracy.  
  - Edge device: Raspberry Pi Camera Module capturing face/eye region  
  - Processing pipeline: OpenCV for face & eye landmark detection → custom CNN (trained on public drowsiness datasets) classifying eye closure ratio and blink frequency  
  - Alert logic: immediate local buzzer + cloud notification if prolonged drowsiness detected  
  - API integration: lightweight Flask server to forward alerts  
  **PoC Highlights**  
  - Reached >92% accuracy in controlled lab conditions  
  - Demonstrated real-time inference (~200 ms per frame) on Raspberry Pi 4  
  - Proved concept of privacy-preserving edge AI (no raw video leaves the vehicle)  
  [GitHub Repo](https://github.com/Asma812/drowsiness-detector) <!-- Replace with real repo link if available -->
</details>

<details>
  <summary>Expert System for Disease Diagnosis<br>Tools: Python, Tkinter</summary>

  **Classic AI / rule-based system**  
  Goal: build a simple but explainable diagnostic assistant for educational purposes.  
  **Approach & Architecture**  
  Implemented a forward-chaining inference engine in Python + Tkinter GUI.  
  - Knowledge base: structured symptoms → diseases → confidence scores  
  - Inference engine: evaluates user answers against rules, accumulates probability  
  - Explanation facility: shows reasoning chain (“because symptom X and Y are present → disease Z is likely”)  
  **PoC Highlights**  
  - Clean separation between knowledge base and inference logic  
  - User-friendly interface that explains why a diagnosis is suggested  
  - Easy to extend with new diseases / rules  
  [GitHub Repo](https://github.com/Asma812/expert-diagnosis) <!-- Replace with real repo link if available -->
</details>

<details>
  <summary>Mobile Application for Financial Management<br>Tools: Java</summary>

  **Android native development**  
  Goal: personal finance tracker with clean UX.  
  **Approach & Architecture**  
  Built with Java + SQLite (local persistence).  
  - Features: income/expense tracking, category budgets, monthly reports, simple charts  
  - Design pattern: MVVM for clean separation of UI and business logic  
  - Security: encrypted local database  
  **PoC Highlights**  
  - Smooth offline experience with sync-ready architecture  
  - Intuitive material design interface  
  [GitHub Repo](https://github.com/Asma812/finance-app) <!-- Replace with real repo link if available -->
</details>

<details>
  <summary>Web Application for Library Management<br>Tools: Java, MySQL, Spring Boot, Thymeleaf</summary>

  **Full-stack CRUD application**  
  Goal: modern library management system for small/medium collections.  
  **Approach & Architecture**  
  Java backend (Spring Boot) + MySQL database + basic HTML/Thymeleaf frontend.  
  - Features: book catalog, member registration, borrowing/return, overdue tracking  
  - REST API layer for future mobile/web clients  
  **PoC Highlights**  
  - Implemented role-based access (admin / librarian / member)  
  - Clean separation of concerns (controller – service – repository)  
  [GitHub Repo](https://github.com/Asma812/library-app) <!-- Replace with real repo link if available -->
</details>

{: .notice--secondary}

## Security Reports & Writeups
(Placeholder for future additions—add links to reports as you complete them)  
- Bug Bounty Report Example: [Link to report/writeup]  
- Pentest Report Example: [Link to report/writeup]  
- Hardening Project: [Link to writeup]

{: .notice--default}

## Languages
English, French, Arabic
