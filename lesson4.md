---
layout: page
title: Lesson 4: Digital Communications (Very Important)
permalink: /lesson4/
---
The heart of modern data transmission.

**Key Concepts:**
- Modulation: ASK, FSK, PSK, QPSK, QAM (16-QAM, 64-QAM, 256-QAM), OFDM (used in LTE, 5G, Wi-Fi)
- Coding: Source coding, Channel coding, Error detection & correction (Parity, CRC, Hamming, Convolutional codes, Turbo & LDPC)
- Performance Metrics: Bit Error Rate (BER), Throughput, Latency, Spectral efficiency

**Why It Matters:** Essential for high-speed, reliable digital networks like 4G/5G.

**Labs/Practice:** Simulated QAM modulation and error correction; analyzed BER curves.

**Tools Used:** MATLAB, GNU Radio, NS3.

<!-- =============== TELECOMMUNICATIONS ENGINEERING ROADMAP =============== -->

## Telecommunications Engineering Self-Study Roadmap

A structured, from-zero-to-employable journey through telecom engineering.  
14 detailed lessons + projects + tools + career paths.

### Progress & Completed Lessons

| #  | Lesson Title                              | Status     | Link / Notes                                  |
|----|-------------------------------------------|------------|-----------------------------------------------|
| 1  | Foundations (Math & Signals)              | ✅ Done    | [View Lesson 1](./lessons/lesson1.md)         |
| 2  | Signals & Systems                         | ✅ Done    | [View Lesson 2](./lessons/lesson2.md)         |
| 3  | Digital Communications                    | ✅ Done    | [View Lesson 3](./lessons/lesson3.md)         |
| 4  | Transmission Media & RF Basics            | ✅ Done    | [View Lesson 4](./lessons/lesson4.md)         |
| 5  | Networking                                | ⏳ In progress | ...                                        |
| ...| ...                                       | ...        | ...                                           |

### Lesson 4 – Transmission Media & RF Basics  
**“Where physics meets telecom engineering”**

This lesson covers the real-world physical layer: how signals actually travel through wired and wireless media, the fundamental impairments every telecom engineer must fight (attenuation, fading, path loss, dispersion, Doppler), and why link budget calculations decide whether a system works or fails.

**Key topics included:**
- Wired media: Twisted pair, Coaxial, Fiber optics (SMF vs MMF, chromatic/modal dispersion, EDFA)
- Wireless & RF fundamentals: Antennas (gain, patterns, polarization), Free-space path loss, Shadowing, Multipath fading (Rayleigh & Rician), Doppler effect
- Practical implications for 5G, Wi-Fi, satellite, cellular planning

**Why this lesson matters for jobs:**  
Radio network planning, transmission engineering, RF optimization, 5G/mmWave deployment, satellite link design — all live here.

📄 **Full detailed write-up (15–20 min read):**  
→ [Read Lesson 4: Transmission Media & RF Basics](./lessons/lesson4.md)

<!-- Optional: small preview / teaser -->
**Quick highlights from Lesson 4**
- FSPL(dB) = 20 log₁₀(d) + 20 log₁₀(f) + constant  
  → loss grows brutally with frequency → explains why mmWave needs dense small cells
- Single-mode fiber: ~0.2 dB/km → 100+ km links without regeneration
- Rayleigh fading: deep nulls in NLOS → OFDM + coding were invented to survive it

---

Feel free to copy-paste and adapt paths/names (e.g. change `./lessons/lesson4.md` to whatever folder structure you use).

Good luck with your GitHub portfolio — it already looks like you're building something serious! 🚀  
When you're ready for the next lesson code snippet or want help structuring the whole repo, just say the word.
