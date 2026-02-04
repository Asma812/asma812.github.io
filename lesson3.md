---
layout: page
title: Lesson 3: Digital Communications
permalink: /lesson3/
---
The heart of modern data transmission.

**Key Concepts:**
- Modulation: ASK, FSK, PSK, QPSK, QAM (16-QAM, 64-QAM, 256-QAM), OFDM (used in LTE, 5G, Wi-Fi)
- Coding: Source coding, Channel coding, Error detection & correction (Parity, CRC, Hamming, Convolutional codes, Turbo & LDPC)
- Performance Metrics: Bit Error Rate (BER), Throughput, Latency, Spectral efficiency

**Why It Matters:** Essential for high-speed, reliable digital networks like 4G/5G.

**Labs/Practice:** Simulated QAM modulation and error correction; analyzed BER curves.

**Tools Used:** MATLAB, GNU Radio, NS3.

# Lesson 3: Digital Communications 

This is the **heart** of modern telecommunications. Almost everything in 4G, 5G, Wi-Fi, satellite links, fiber high-speed links, and even deep-space comms boils down to digital communications principles.

Lesson 1 gave you math and signals; Lesson 2 gave you sampling/filtering/LTI systems. Now we take **bits** → turn them into waveforms (modulation), protect them against noise/errors (coding), send them over channels, and measure how well they survive.

## Why Digital Communications Is "The Heart"

- All modern telecom is **digital** at baseband: bits rule.
- The channel is noisy, fading, dispersive → we must fight entropy with smart modulation + coding.
- Goal: Maximize **throughput** (bits/s) while keeping **BER** low, **latency** acceptable, and **spectral efficiency** high (bits/Hz).
- This directly determines why 5G can do 10 Gbps, why Starlink works in LEO, why Wi-Fi 6/7 pushes higher rates.

## 1. Modulation – Turning Bits into Waveforms

Modulation maps bit groups to changes in carrier signal (amplitude, phase, frequency).

### Basic schemes (historical but still used in low-rate links)

- **ASK** (Amplitude Shift Keying): bits change amplitude → simple but noise-sensitive.
- **FSK** (Frequency Shift Keying): bits change frequency → robust to amplitude noise (used in Bluetooth classic).
- **PSK** (Phase Shift Keying): bits change phase → constant envelope, good for power amplifiers.

### Advanced / Modern schemes

#### QPSK (Quadrature PSK)
- 4 symbols (2 bits/symbol).
- Phases: 45°, 135°, 225°, 315° (or ±45° offsets).
- Each symbol = one complex number in I-Q plane.
- Constant amplitude → efficient for non-linear amplifiers.
- Spectral efficiency: 2 bits/Hz (ideal).

![QPSK Constellation Diagram](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/QPSK_constellation.svg/800px-QPSK_constellation.svg.png)

#### QAM (Quadrature Amplitude Modulation)
Combines amplitude + phase.

- **16-QAM**: 16 points (4 bits/symbol) → 4×4 grid in I-Q plane.
- **64-QAM**: 64 points (6 bits/symbol) → used in good-channel conditions (LTE/5G downlink).
- **256-QAM**: 8 bits/symbol → Wi-Fi 6/7, 5G in excellent SNR.

Higher order = more bits/Hz but needs higher SNR (points closer → more errors from noise).

![16-QAM Constellation](https://upload.wikimedia.org/wikipedia/commons/a/a6/16-QAM_Demonstration_3.gif)

#### OFDM (Orthogonal Frequency Division Multiplexing) – The king of wideband digital comms

Used in: Wi-Fi (802.11a/g/n/ac/ax), LTE, 5G NR, DAB, DVB-T, power-line comms.

**Idea**: Split wideband carrier into hundreds/thousands of narrow orthogonal subcarriers.  
Each subcarrier carries low-rate data (usually QAM-modulated).  
Orthogonality → no interference between subcarriers (even though spectra overlap).

**Key features**:
- **Cyclic Prefix (CP)**: Copies end of symbol to beginning → absorbs multipath delay spread → turns ISI into simple phase rotation (equalized per subcarrier).
- FFT/IFFT: Efficient implementation.
- Pilot subcarriers: Known symbols for channel estimation.

![OFDM Transmitter/Receiver Block Diagram](https://wiki.gnuradio.org/images/1/17/Ofdm_loopback_example_fg.png)

![OFDM Subcarriers Illustration](https://www.sharetechnote.com/image/Communication_OFDM_Concept_02.png)

**Why OFDM wins in mobile/wireless**: Multipath fading is flat per subcarrier → simple one-tap equalizer per subcarrier.

## 2. Coding – Adding Intelligence to Fight Errors

Raw modulation is not enough — noise flips bits. Coding adds redundancy.

### Error Detection (simple)

- **Parity bit**: Even/odd count → detects odd number of errors.
- **CRC** (Cyclic Redundancy Check): Polynomial division → very good detection (used in Ethernet, Wi-Fi, LTE/5G PDCP/RLC).

### Error Correction

- **Hamming code**: Corrects single errors.
- **Convolutional codes** + Viterbi decoding → good for continuous streams (classic GSM, CDMA, early Wi-Fi).

![Convolutional Code Trellis Diagram](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3e/Convolutional_code_trellis.svg/800px-Convolutional_code_trellis.svg.png)

- **Turbo codes**: Parallel concatenated convolutional codes + iterative decoding → approach Shannon limit (3G UMTS).
- **LDPC** (Low-Density Parity-Check): Sparse parity-check matrix → iterative belief propagation. Used in: 5G data channel, Wi-Fi 6/7, DVB-S2, 10GBASE-T. Very close to Shannon limit.

![LDPC Factor Graph](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Tanner_graph_bipartite.svg/800px-Tanner_graph_bipartite.svg.png)

**Modern trend**: 5G uses LDPC for data, Polar codes for control channels.

## 3. Performance Metrics – How We Judge Success

- **Bit Error Rate (BER)**: Probability a bit is wrong after decoding. Target: 10⁻⁵ to 10⁻¹² for data.
- **Throughput**: Effective bits/s after overhead/coding/retransmissions.
- **Latency**: End-to-end delay (important for URLLC in 5G).
- **Spectral efficiency**: bits/s/Hz — higher = better use of bandwidth (Shannon limit: log₂(1+SNR)).

![BER vs SNR Waterfall Curves](https://www.cheggcdn.com/study/f53/f531919f-b000-45a1-9220-dd4bb65a51e7/image.png)

Observe:
- QPSK robust (works at low SNR) but low efficiency.
- 64-QAM/256-QAM need high SNR but pack many bits/Hz.
- Coding shifts curves left (coding gain).

## How to Study & Practice This Lesson

**Resources**:
- "Digital Communications" by Proakis
- "Fundamentals of Wireless Communication" by Tse & Viswanath (free PDF online)
- YouTube: "IIT Bombay Digital Communication" or "Wireless Future Blog" series

**Hands-on** (crucial):
- Python/MATLAB: Generate QPSK/16-QAM symbols, add AWGN, demodulate → plot constellation scatter.
- Compute BER vs SNR curve (Monte Carlo simulation).
- Simple OFDM: IFFT → add CP → FFT → recover.

## Milestone Questions (Portfolio Showcase)

- Why does higher-order QAM need higher SNR?
- How does cyclic prefix fix multipath in OFDM?
- Sketch QPSK constellation and explain decision regions.
- Why LDPC/Turbo beat convolutional in modern systems?
- Interpret a BER waterfall: what does "coding gain" mean?

Master this → 4G/5G architectures, RF impairments, and security attacks will make sense.
