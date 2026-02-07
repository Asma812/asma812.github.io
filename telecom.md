---
layout: page
title: Telecom Lessons
permalink: /telecom/
---

<div class="container" style="padding: 3rem 1rem;">
  <h1 style="text-align: center; font-family: 'JetBrains Mono', monospace; color: var(--accent); margin-bottom: 3rem;">Telecom Engineering Roadmap</h1>
  <p style="text-align: center; color: var(--text-muted); font-size: 1.15rem; max-width: 800px; margin: 0 auto 4rem;">
    A structured 12-step learning path for telecom engineers. Start from foundations and build up to real-world 5G + security expertise.
  </p>

  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(360px, 1fr)); gap: 2rem;">
    {% assign lessons = "1 Foundations (Non-negotiable)|2 Signals & Systems (Core Telecom Brain)|3 Digital Communications (VERY IMPORTANT)|4 Transmission Media & RF Basics|5 Networking (Telecom ≠ only RF)|6 Cellular Networks (CRITICAL)|7 Telephony & VoIP|8 Satellite Communications|9 Tools You MUST Learn|10 Programming for Telecom Engineers|11 Telecom Security (Your BIG PLUS)|12 Practical Projects (VERY IMPORTANT)" | split: "|" %}

    {% for lesson in lessons %}
      {% assign num = forloop.index %}
      {% assign title = lesson %}

      <div class="card" style="position: relative; overflow: hidden; border-radius: 12px; box-shadow: 0 6px 20px rgba(0,0,0,0.25); transition: all 0.3s; background: linear-gradient(rgba(0,0,0,0.65), rgba(0,0,0,0.75)); background-size: cover; background-position: center; min-height: 320px;">
        <!-- Background image (different for each lesson) -->
        {% case num %}
          {% when 1 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1518770660439-4636190af475?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 2 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1557683316-973673baf926?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 3 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1581091226825-a6a2a5aee158?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 4 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1451187580459-43490279c0fa?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 5 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1563204424-5f9e4e8dfc1f?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 6 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1518770660439-4636190af475?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 7 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1558494949-ef0d7d6b0d2d?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 8 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1446776811953-b23d57bd21aa?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 9 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1517430816045-df4b7de11d1d?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 10 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1555066931-4365d14bab8c?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 11 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1555949963-aa79d0ebc8fb?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
          {% when 12 %}
            <div style="background-image: url('https://images.unsplash.com/photo-1518770660439-4636190af475?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80'); background-size: cover; background-position: center; position: absolute; inset: 0; z-index: -1;"></div>
        {% endcase %}

        <div style="position: relative; z-index: 2; color: white;">
          <h3 style="margin: 0 0 1rem; font-size: 1.45rem; font-weight: 700;">
            {{ num }}️⃣ {{ title }}
          </h3>
          <p style="margin: 0 0 1.2rem; font-size: 1rem; opacity: 0.9;">
            Click to see the full planning & key concepts
          </p>
          <div style="margin-top: 1rem;">
            {% case num %}
              {% when 1 %}
                <p>Mathematics (vectors, matrices, complex numbers, probability, Fourier/Laplace, convolution)</p>
                <p>Physics & Signals (analog/digital, energy/power, time/frequency domain, bandwidth, noise, SNR/BER)</p>
              {% when 2 %}
                <p>Continuous vs discrete-time systems</p>
                <p>LTI, impulse response, sampling theorem, aliasing, filtering, ADC/DAC</p>
                <p>Tools: MATLAB, Python (NumPy/SciPy)</p>
              {% when 3 %}
                <p>Modulation: ASK/FSK/PSK, QPSK, QAM, OFDM</p>
                <p>Coding: source/channel, error correction (CRC, Hamming, Turbo/LDPC)</p>
                <p>Metrics: BER, throughput, latency, spectral efficiency</p>
              {% when 4 %}
                <p>Wired: twisted pair, coax, fiber (single/multi-mode, attenuation, dispersion)</p>
                <p>Wireless/RF: antennas, propagation, path loss, fading, Doppler</p>
              {% when 5 %}
                <p>OSI/TCP-IP layers</p>
                <p>IP/TCP/UDP, DNS/DHCP/NAT</p>
                <p>Routing/Switching: Ethernet, VLAN, STP, OSPF/BGP</p>
                <p>Wireless: Wi-Fi 802.11, cellular basics</p>
              {% when 6 %}
                <p>Evolution: 2G → 5G (GSM → NR)</p>
                <p>Architecture: RAN, Core (EPC → 5GC), IMS</p>
                <p>Concepts: handover, roaming, QoS, slicing, MIMO, beamforming</p>
              {% when 7 %}
                <p>PSTN, SS7, SIP, RTP</p>
                <p>VoIP architecture, softswitches</p>
              {% when 8 %}
                <p>GEO/MEO/LEO orbits</p>
                <p>Link budget, VSAT, satellite internet (Starlink)</p>
              {% when 9 %}
                <p>Simulation: MATLAB/Simulink, GNU Radio</p>
                <p>Networking: Wireshark, GNS3/Packet Tracer, NS-3, Open5GS, srsRAN</p>
                <p>Systems: Linux, Bash</p>
              {% when 10 %}
                <p>Python (automation, simulation), C/C++ (low-level), Bash</p>
                <p>Use cases: network automation, log analysis, protocol simulation</p>
              {% when 11 %}
                <p>SS7 vulnerabilities, LTE/5G security, IMS security</p>
                <p>SIM auth, network monitoring, IDS/IPS, lawful interception</p>
              {% when 12 %}
                <p>Beginner: QPSK/QAM BER sim, VoIP, Wireshark SIP/RTP</p>
                <p>Intermediate: LTE sim, srsRAN+Open5GS lab</p>
                <p>Advanced: 5G core, telecom attack sim, secure VoIP</p>
            {% endcase %}
          </div>
        </div>
      </div>
    {% endfor %}
  </div>

  <p style="text-align: center; margin-top: 4rem; color: var(--text-muted); font-size: 1.1rem;">
    Master these 12 steps → become a rare telecom + cybersecurity engineer.
  </p>
</div>
