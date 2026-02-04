---
layout: page
title: Lesson 10: Programming for Telecom Engineers
permalink: /lesson10/
---
Coding skills applied to telecom.

**Key Concepts:**
- Languages: Python, C/C++, Bash
- Use cases: Network automation, Log analysis, Performance testing, Protocol simulation

**Why It Matters:** Automates and optimizes telecom tasks.

**Labs/Practice:** Scripted network simulations; analyzed logs.

**Tools Used:** Python, Bash, C++.

# Lesson 10: Programming for Telecom Engineers

You already have an advantage here — many telecom engineers come from pure EE/RF backgrounds and struggle with coding. If you're comfortable with programming (even basics), this skill set multiplies your value enormously. In 2026, telecom is heavily software-defined: automation, orchestration, data analysis, simulation, protocol implementation, and even parts of the RAN/core run on code.

## Why Programming Is a Big Advantage for Telecom Engineers

- **Automation saves time/money**: Manual config of 1000s of sites → scripts do it in minutes.
- **Data-driven decisions**: Parse massive logs → find outages, anomalies, KPI degradations.
- **Simulation & prototyping**: Test new algorithms (e.g., beamforming, scheduling) before hardware.
- **Network programmability**: NETCONF/YANG, OpenConfig, SDN controllers.
- **Open-source telecom stacks**: srsRAN, Open5GS, OAI — all C++/Python.
- **High-demand combo**: Telecom domain knowledge + scripting/coding = rare & well-paid roles (automation engineer, core developer, performance analyst, DevOps for telco).

## 1. Core Languages & Their Telecom Roles

### Python (The #1 Choice – Learn This First and Deeply)

- **Why it's dominant**: Easy syntax, huge ecosystem, excellent for data, automation, simulation.
- **Key libraries for telecom**:

  - **NumPy / SciPy** → vector/math operations, signal processing (FFT, filters, convolution)
  - **Matplotlib / Seaborn / Plotly** → plotting BER curves, KPIs, heatmaps
  - **Pandas** → log parsing, CSV/Excel analysis, KPI dashboards
  - **Scapy** → packet crafting/analyzing (custom protocols, testing)
  - **PyShark / Pyshark** → Wireshark automation
  - **Requests / httpx** → API calls (5GC SBA, OSS/BSS)
  - **Paramiko / Netmiko** → SSH to network elements (routers, base stations)
  - **Jinja2 + Ansible** → templating configs

**Typical Python use cases in telecom**:
- Automate site configuration via NETCONF/CLI
- Parse srsRAN / Open5GS logs → detect handover failures
- Simulate QPSK/16-QAM BER in AWGN (Monte Carlo)
- Analyze drive-test data (RSSI, SINR maps)
- Build simple dashboards (KPI trends from OSS exports)

```python
# Example: Simple QPSK BER simulation snippet
import numpy as np
import matplotlib.pyplot as plt

def qpsk_ber(snr_db_range):
    ber = []
    for snr_db in snr_db_range:
        snr = 10**(snr_db/10)
        sigma = np.sqrt(1/(2*snr))          # noise std dev
        bits = np.random.randint(0, 2, 1000000)
        symbols = (2*bits-1) + 1j*(2*np.random.randint(0, 2, len(bits))-1)
        noise = sigma * (np.random.randn(len(bits)) + 1j*np.random.randn(len(bits)))
        rx = symbols + noise
        detected = (np.real(rx) > 0) == (np.real(symbols) > 0)
        ber.append(np.mean(~detected))
    return ber

snr_db = np.arange(0, 12, 0.5)
ber = qpsk_ber(snr_db)

plt.semilogy(snr_db, ber, 'o-', label='QPSK simulation')
plt.grid(True)
plt.xlabel('SNR (dB)')
plt.ylabel('BER')
plt.title('QPSK BER vs SNR (AWGN)')
plt.legend()
plt.show()
