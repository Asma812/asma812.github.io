---
layout: page
title: Lesson 6: Networking (Telecom ≠ Only RF)
permalink: /lesson6/
---
Integrating telecom with broader networks.

**Key Concepts:**
- OSI & TCP/IP: Physical to Application layer, IP, TCP, UDP, DNS, DHCP, NAT
- Routing & Switching: Ethernet, VLAN, STP, OSPF, BGP
- Wireless Networks: Wi-Fi (802.11 a/b/g/n/ac/ax), Cellular architecture

**Why It Matters:** Telecom engineers need networking for end-to-end systems.

**Labs/Practice:** Configured VLANs and routing; analyzed Wi-Fi traffic.

**Tools Used:** Cisco Packet Tracer, GNS3, Wireshark.

# Lesson 6: Cellular Networks (CRITICAL)

This is the **money section** — if you want to work for telecom operators (Orange, Ooredoo, Tunisie Telecom), vendors (Nokia, Huawei, Ericsson), or in 5G/6G R&D, most jobs live here.

Modern cellular combines:
- RF and physical layer (Lessons 1–4)
- Digital communications & modulation (Lesson 3)
- IP networking (Lesson 5)
- Mobility, QoS, massive scale, slicing, beamforming

## Why Cellular Networks Are Critical

- Main revenue source for mobile operators (voice, data, SMS, IoT)
- Highest complexity: RF + IP + mobility + security + virtualization
- Fastest evolution: 2G → 5G in ~25 years (6G research already active)
- Typical job roles: Radio Network Optimization, Core Engineer, RAN Engineer, 5G Planner, Drive Test Engineer

## 1. Cellular Evolution – From Voice to Everything

| Generation   | Access Technology     | Peak Speed (theoretical) | Latency       | Core Network          | Key Innovation                          |
|--------------|-----------------------|---------------------------|---------------|-----------------------|-----------------------------------------|
| 2G (GSM)     | TDMA / FDMA           | ~384 kbps (EDGE)          | ~100 ms       | Circuit + GPRS        | Digital voice, SMS                      |
| 3G (UMTS)    | WCDMA                 | ~42 Mbps (HSPA+)          | ~50 ms        | Circuit + Packet      | Mobile Internet                         |
| 4G (LTE)     | OFDMA / SC-FDMA       | ~1–3 Gbps                 | ~20 ms        | EPC (all-IP)          | Flat architecture, high-speed mobile    |
| 5G (NR)      | OFDMA + massive MIMO  | 10–20 Gbps                | <1 ms (URLLC) | 5GC (cloud-native)    | Network slicing, beamforming, mmWave    |

**5G service pillars**:
- **eMBB** – enhanced Mobile Broadband (very high throughput)
- **URLLC** – Ultra-Reliable Low Latency Communications (mission-critical)
- **mMTC** – massive Machine-Type Communications (massive IoT)

## 2. Architecture – RAN + Core

### Radio Access Network (RAN)

- **4G**: eNodeB (eNB) — single integrated base station
- **5G**: gNodeB (gNB) — often split architecture:
  - **CU** (Central Unit) – higher layers
  - **DU** (Distributed Unit) – lower layers
  - **RU** (Radio Unit) – RF front-end  
  → Enables Cloud RAN, Open RAN, flexible deployment

### 4G Core – EPC (Evolved Packet Core)

Flat, all-IP architecture:

- **MME** – Mobility Management Entity (control plane, authentication, mobility)
- **HSS** – Home Subscriber Server (subscriber database)
- **SGW** – Serving Gateway (user plane anchor)
- **PGW** – PDN Gateway (IP allocation, policy, Internet breakout)
- **PCRF** – Policy & Charging Rules Function

![4G EPC architecture overview](https://via.placeholder.com/800x400.png?text=4G+EPC+Architecture+Diagram)  
*Typical 4G EPC: UE → eNB → MME/SGW/PGW → PDN (Internet)*

### 5G Core – 5GC (Service-Based Architecture)

Cloud-native, microservices-based:

- **AMF** – Access & Mobility Management Function
- **SMF** – Session Management Function
- **UPF** – User Plane Function
- **UDM** – Unified Data Management
- **AUSF** – Authentication Server Function
- **NRF** – Network Repository Function (service discovery)
- Others: PCF, NSSF, NEF, CHF, ...

![5G Core SBA overview](https://via.placeholder.com/800x450.png?text=5G+Core+Service-Based+Architecture)  
*5G Core: HTTP/2 + REST APIs between Network Functions*

**IMS** (IP Multimedia Subsystem) – SIP-based subsystem for VoLTE / VoNR (voice over LTE/5G)

## 3. Key Concepts

### Handover

Seamless cell change while moving.

- Measurement → Decision → Preparation → Execution → Path Switch
- 5G supports **Xn handover** (direct gNB–gNB) for lower latency

![5G handover sequence](https://via.placeholder.com/800x500.png?text=5G+Handover+Flow+Sequence+Diagram)

### Roaming

Home network ↔ Visited network via GRX/IPX. Authentication stays with home operator.

### QoS (Quality of Service)

- 5QI (5G QoS Identifier) defines priority, packet delay budget, error rate
- Dedicated bearers/flows for voice, video, URLLC, best-effort

### Network Slicing

One physical infrastructure → multiple virtual networks (slices)

- Each slice: dedicated resources, isolation, SLA
- Examples:
  - eMBB slice → high throughput (video streaming)
  - URLLC slice → ultra-low latency (autonomous driving)
  - mMTC slice → massive connections (smart meters)

![Network slicing concept](https://via.placeholder.com/800x400.png?text=5G+Network+Slicing+Illustration)

### Massive MIMO & Beamforming

- 64T64R, 128T128R antenna arrays
- Spatial multiplexing → many users at once
- **Beamforming** directs energy → higher SNR, less interference

![Massive MIMO beamforming](https://via.placeholder.com/800x450.png?text=Massive+MIMO+Beamforming+to+Multiple+UEs)

## Next Steps – Hands-on Practice

- Deploy private 4G/5G lab: **Open5GS** (5GC) + **srsRAN** (gNB + UE emulator)
- Simulate handover, slicing, mobility in **ns-3**
- Capture VoLTE calls → analyze SIP + GTP with Wireshark

## Milestone Questions

1. Main differences between 4G EPC and 5G Core?
2. Why was network slicing introduced in 5G? Give three concrete use cases.
3. How does massive MIMO increase network capacity?
4. Describe the basic steps of a 5G Xn handover.
5. Why is the 5G Core designed as a Service-Based Architecture (SBA)?

Master this section → VoIP, security, satellite integration, and real projects become much easier to understand.

Continue to [Lesson 7: Telephony & VoIP](./lesson7.md) →
