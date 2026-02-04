---
layout: page
title: Lesson 5: Networking 
permalink: /lesson5/
---
Integrating telecom with broader networks.

**Key Concepts:**
- OSI & TCP/IP: Physical to Application layer, IP, TCP, UDP, DNS, DHCP, NAT
- Routing & Switching: Ethernet, VLAN, STP, OSPF, BGP
- Wireless Networks: Wi-Fi (802.11 a/b/g/n/ac/ax), Cellular architecture

**Why It Matters:** Telecom engineers need networking for end-to-end systems.

**Labs/Practice:** Configured VLANs and routing; analyzed Wi-Fi traffic.

**Tools Used:** Cisco Packet Tracer, GNS3, Wireshark.

# Lesson 5: Networking (Telecom ≠ only RF)

This lesson bridges the physical/RF world (Lessons 1–4) to the higher-level world of packets, routing, and services that modern telecom runs on. Telecom engineers today must be fluent in both RF **and** IP networking — because 4G/5G is all-IP, VoIP replaces circuit switching, core networks are cloud-native, and security/automation happen at L3+.

## Why Networking Is Essential for Telecom Engineers

- Legacy telecom was circuit-switched (voice over TDM).  
- Modern telecom is packet-switched: voice, video, data all over IP.  
- Cellular core (EPC/5GC), IMS, backhaul/fronthaul, fixed-mobile convergence — all use IP routing/switching.  
- Tools like Wireshark, GNS3, NS-3 simulate IP + telecom protocols.  
- Jobs (core/transmission engineer, 5G architect) require CCNA-level networking knowledge.

## 1. OSI & TCP/IP Models

Two reference models explain how data moves from app to wire (and back).

### OSI Model (7 layers, theoretical/reference)

- **Layer 7 – Application**: User-facing (HTTP, DNS, SIP, FTP).  
- **Layer 6 – Presentation**: Data formatting, encryption (SSL/TLS), compression.  
- **Layer 5 – Session**: Session management, checkpoints (e.g., RPC).  
- **Layer 4 – Transport**: End-to-end (TCP reliable, UDP fast/unreliable).  
- **Layer 3 – Network**: Routing, logical addressing (IP).  
- **Layer 2 – Data Link**: Framing, MAC addressing, error detection (Ethernet, PPP).  
- **Layer 1 – Physical**: Bits over medium (cables, RF, modulation).

![OSI 7-layer model](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/osi-7-layers.png)
*(Client/server view of the OSI stack)*

![OSI model breakdown](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/osi-layers-functions.png)
*(Detailed functions per layer)*

### TCP/IP Model (practical, 4–5 layers)

- **Application** (OSI 5–7): HTTP, DNS, SIP, RTP.  
- **Transport** (OSI 4): TCP/UDP.  
- **Internet/Network** (OSI 3): IP (IPv4/IPv6), ICMP, ARP.  
- **Link/Network Interface** (OSI 1–2): Ethernet, Wi-Fi, PPP.

![OSI vs TCP/IP comparison](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/osi-vs-tcpip.png)
*(Side-by-side comparison)*

**Telecom relevance**:  
- 5G core uses IP everywhere (user plane = GTP-U over UDP/IP).  
- SIP/RTP run on UDP (Application/Transport).  
- RAN uses lower layers + IP for fronthaul (eCPRI over Ethernet/IP).

## 2. Key Protocols & Concepts

### IP, TCP, UDP

- **IP**: Best-effort, connectionless routing (IPv4: 32-bit, IPv6: 128-bit addresses).  
- **TCP**: Reliable, ordered, congestion-controlled (3-way handshake, ACKs, windowing). Used for HTTP, SIP signaling.  
- **UDP**: Unreliable, low-latency (no handshake). Used for RTP (voice/video), DNS queries.

### DNS, DHCP, NAT

- **DNS**: Translates domain → IP (critical for roaming, IMS).  
- **DHCP**: Auto-assigns IP, gateway, DNS to devices (huge in enterprise/Wi-Fi).  
- **NAT**: Maps private IPs to public (CGNAT common in mobile networks).

### Ethernet

Layer 2 framing for LANs.

![Ethernet frame structure](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/ethernet-frame.png)
*(Detailed Ethernet frame layout)*

### VLAN (IEEE 802.1Q)

Segments broadcast domains on same switch.

![802.1Q VLAN tag](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/8021q-vlan-tag.png)
*(VLAN tag insertion in frame)*

![VLAN trunk example](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/vlan-trunk.png)
*(Trunk carrying multiple VLANs)*

### STP (Spanning Tree Protocol)

Prevents Layer 2 loops.

![STP topology example](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/stp-topology.png)
*(Root bridge, port roles: root, designated, blocked)*

### Routing: OSPF & BGP

- **OSPF**: Link-state, fast convergence, used in enterprise/backhaul.  
- **BGP**: Path-vector, inter-domain routing (Internet-scale, operator peering).

![OSPF multi-area topology](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/ospf-multi-area.png)
*(Typical OSPF design with areas and ABRs)*

## 3. Wireless Networks (Wi-Fi & Cellular Basics)

### Wi-Fi (IEEE 802.11 family)

- Standards: a/b/g/n/ac/ax (Wi-Fi 4/5/6), be (Wi-Fi 7).  
- Bands: 2.4 GHz, 5 GHz, 6 GHz (Wi-Fi 6E/7).

![6 GHz Wi-Fi channels (FCC)](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/6ghz-channels-fcc.png)
*(Channel allocation in 6 GHz band)*

![6 GHz device power classes](https://github.com/YOUR_USERNAME/YOUR_REPO/raw/main/images/lesson5/6ghz-power-classes.png)
*(LPI, VLP, AFC requirements)*

### Cellular architecture (high-level)

UE → RAN (eNodeB/gNB) → Core (EPC/5GC) → Internet/IMS.  
Backhaul: often IP/Ethernet over fiber/microwave.

## How to Study & Practice

- Cisco Packet Tracer → build VLANs, OSPF labs  
- Wireshark → capture HTTP, DNS, SIP  
- GNS3 → simulate NAT, DHCP, routing  
- Wi-Fi Analyzer apps → real-world channel visualization

## Milestone Questions

- Walk through how a SIP packet travels from app to wire (layers & protocols).  
- Why use VLANs in a telecom backhaul switch?  
- Difference between OSPF and BGP? When is each used?  
- Why is UDP preferred for RTP in VoIP?  
- In a Wi-Fi 6 network, why does 6 GHz give higher capacity?

---

*Part of the "Telecommunications Engineering Roadmap" portfolio series.*  
Next: [Lesson 6: Cellular Networks](./lesson6.md)
