---
layout: page
title: Lesson 11: Telecom Security
permalink: /lesson11/
---
Blending security with telecom.

**Key Concepts:**
- SS7 vulnerabilities
- LTE/5G security
- IMS security
- SIM authentication
- Network monitoring
- IDS/IPS for telecom
- Lawful interception

**Why It Matters:** Your cybersecurity background makes you unique—telecom + security is in-demand.

**Labs/Practice:** Simulated SS7 attacks; hardened telecom networks.

**Tools Used:** Wireshark, OpenSSL, Ansible.

# Lesson 11: Practical Projects 

This is the lesson where theory becomes **visible proof** — the part that actually gets you interviews and offers.  
Without projects, even perfect knowledge stays invisible on a CV. With well-documented projects, you can say: “I built a private 5G network”, “I simulated attack scenarios”, “I analyzed real signaling traffic” — and then **show** screenshots, code, logs, diagrams.

The roadmap divides projects into three levels. For each one I will give you:

- Clear goal  
- Why it is valuable (what it proves to recruiters)  
- Step-by-step realistic approach (2026 context)  
- Tools needed  
- Expected outcome / deliverable  
- Documentation tips (GitHub README structure)

## Beginner Level Projects  
(1–4 weeks each – build confidence & quick wins)

### Project 1: Simulate QPSK vs 16-QAM BER in AWGN channel

**Goal**: Generate bit error rate curves for two popular modulations and compare robustness vs spectral efficiency.

**Why valuable**:  
Shows you understand digital communications fundamentals (Lesson 3) and can implement simulations (Lesson 10 + 9).

**Step-by-step approach**:
1. Use **Python** (NumPy + Matplotlib + SciPy)
2. Generate random bits → map to QPSK (4 points) and 16-QAM (16 points) constellations
3. Add AWGN noise at different SNR values (from –5 dB to 20 dB, step 1 dB)
4. Implement maximum-likelihood detection (nearest constellation point)
5. Count bit errors → compute BER = errors / total bits
6. Run ~10⁶–10⁷ bits per SNR point for smooth curves
7. Plot both curves on log scale (waterfall style)
8. Add theoretical BER curves for comparison (use erfc() from scipy.special)

**Deliverable**:
- Jupyter notebook or .py script
- Plot: BER vs Eb/N0 or SNR (two curves + theoretical)
- Short explanation in README: “QPSK more robust at low SNR, 16-QAM twice the efficiency but needs ~7 dB more SNR for same BER”

### Project 2: Build a simple VoIP system

**Goal**: Set up two (or more) endpoints that can make audio calls over IP.

**Why valuable**:  
Demonstrates understanding of telephony & VoIP (Lesson 7), SIP/RTP, Wireshark usage.

**Step-by-step approach**:
1. Install **Asterisk** (open-source PBX) on Ubuntu (or use FreeSWITCH)
2. Install two softphones: Linphone (desktop) + MicroSIP or Zoiper (Windows/Mac)
3. Configure Asterisk sip.conf & extensions.conf → create two users (e.g., 1001 & 1002)
4. Register both softphones to Asterisk
5. Make call from 1001 → 1002 → capture traffic with Wireshark
6. (Bonus) Enable SRTP (secure RTP) or Opus codec

**Deliverable**:
- Screenshots: registration, call setup, RTP stream
- Wireshark .pcap file (anonymized) + filters used (sip, rtp)
- README: call flow diagram (INVITE → 180 → 200 OK → ACK → RTP → BYE)

### Project 3: Wireshark analysis of SIP/RTP

**Goal**: Deep-dive into a real VoIP call capture.

**Why valuable**:  
Proves you can analyze real protocol traffic (critical for troubleshooting & security roles).

**Step-by-step approach**:
1. Use project 2 capture (or download sample VoLTE/SIP pcap from online)
2. Open in Wireshark
3. Apply filters: `sip` → see registration & INVITE flow
4. `rtp` → analyze sequence numbers, jitter, packet loss
5. `rtcp` → check sender/receiver reports (jitter, fraction lost)
6. Export → Statistics → RTP → Stream Analysis
7. (Bonus) Find SDP negotiation (codecs, ports)

**Deliverable**:
- Annotated screenshots or PDF report
- Table: timestamps of key SIP messages + RTP stats (avg jitter, packet loss %)

## Intermediate Level Projects  
(4–10 weeks – serious resume builders)

### Project 4: LTE network simulation (NS-3 or MATLAB)

**Goal**: Simulate a small LTE network and measure KPIs.

**Why valuable**:  
Shows cellular network understanding (Lesson 6) + simulation skill.

**Step-by-step approach (NS-3 recommended)**:
1. Install NS-3 (latest LTS version)
2. Use Lena module (LTE model)
3. Create scenario: 1 eNB, 2–10 UEs, mobility or static
4. Configure: frequency band, bandwidth, Tx power, fading model
5. Run simulation → collect traces (PHY, MAC, RLC, PDCP, IP)
6. Plot: throughput, latency, BLER, SINR distribution

**Deliverable**:
- NS-3 .cc file + plot scripts (Python/Matplotlib)
- Graphs: cell throughput vs # users, CDF of SINR

### Project 5: srsRAN + Open5GS lab

**Goal**: Deploy a real private 4G/5G network at home.

**Why valuable**:  
One of the strongest signals you can send: “I ran actual 4G/5G RAN + Core”.

**Step-by-step approach**:
1. Use Ubuntu 22.04 or 24.04 (strong PC recommended, 16–32 GB RAM)
2. Install dependencies → clone & build **Open5GS** (5GC)
3. Configure: AMF, SMF, UPF, UDM, AUSF (use sample configs)
4. Run core network components
5. Clone & build **srsRAN** Project (gNB + EPC mode or 5G NSA/SA)
6. Use USRP B200/B210 or LimeSDR or even ZeroMQ (virtual RF)
7. Connect commercial phone → manual PLMN & APN config
8. Achieve: attach → data session → ping / browse
9. (Bonus) Make VoLTE call if IMS added

**Deliverable**:
- GitHub repo with configs, startup scripts, screenshots
- Video (1–3 min) showing phone registering & browsing
- Logs: AMF registration accept, UPF GTP tunnel creation

## Advanced Level Projects  
(8+ weeks – differentiate yourself)

### Project 6: 5G core deployment (cloud-native style)

**Goal**: Deploy Open5GS or free5GC in Kubernetes (or Docker Compose)

**Why valuable**:  
Shows modern 5G core knowledge (cloud-native, SBA) + DevOps basics.

**Approach**:
1. Use minikube or kind (local Kubernetes)
2. Deploy Open5GS via Helm chart (official exists)
3. Expose services → connect srsRAN gNB
4. Monitor with Prometheus + Grafana (bonus)

### Project 7: Telecom attack simulation (signaling attacks)

**Goal**: Safely demonstrate understanding of vulnerabilities (in isolated lab).

**Why valuable**:  
Perfect for telecom security roles (Lesson 11).

**Approach (ethical & isolated only!)**:
1. Use srsRAN gNB + Open5GS core
2. With Scapy: craft fake GTP-C messages (e.g., spoofed Create Session)
3. Attempt SS7-like queries if Diameter interface exposed (lab only)
4. Show detection: implement simple rate-limiting script or Wireshark alert
5. Document: attack → detection → mitigation

**Important**: Never run real attacks on production or public networks — felony territory.
