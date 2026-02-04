---
layout: page
title: Lesson 2: Physics & Signals
permalink: /lesson2/
---
Understanding signals as the core of information transmission.

**Key Concepts:**
- Signal types (analog vs digital)
- Energy vs power signals
- Time domain vs frequency domain
- Bandwidth
- Noise (AWGN)
- SNR, BER

**Why It Matters:** Telecom is about transmitting information over noisy channels; this lesson teaches reliability in imperfect environments.

**Labs/Practice:** Simulated signal propagation and noise effects; measured SNR in basic transmission setups.

**Tools Used:** MATLAB, Wireshark for signal capture.

## Part B: Physics & Signals – The Real-World Constraints

Telecom fights physics every day. The channel is never perfect.

### 1. What is a Signal? Analog vs Digital

- **Analog**: Continuous in time & amplitude (e.g., human voice pressure wave → microphone voltage). Infinite possible values. Very sensitive to noise/amplification distortion.  
- **Digital**: Discrete in time (sampled) and amplitude (quantized to bits). Only finite values (usually binary levels). Noise-tolerant because small perturbations don't change 0 → 1 if threshold is good. Almost all modern telecom is digital after the antenna.

**Trade-off**  
Analog = potentially higher fidelity but fragile.  
Digital = robust, compressible, correctable → but needs bandwidth for bits.

### 2. Energy vs Power Signals

- **Energy signal**: Finite total energy → ∫|s(t)|² dt < ∞ (e.g., one pulse, voice packet)  
- **Power signal**: Finite average power → lim (1/2T) ∫_{-T}^T |s(t)|² dt exists and finite (e.g., continuous sinusoid, ongoing data stream)

Most telecom carriers are power signals; bursts/packets are energy signals.

### 3. Time Domain vs Frequency Domain

Two views of the same thing (thanks, Fourier).

- Time: amplitude vs time (oscilloscope)  
- Frequency: power vs frequency (spectrum)

Every operation has a dual: convolution ↔ multiplication, modulation ↔ frequency shift.

### 4. Bandwidth

The "width" of frequencies the signal occupies or the channel allows.

- Baseband signal (around 0 Hz): e.g., voice 300–3400 Hz → ~3 kHz bandwidth  
- Passband: centered at carrier fc (e.g., 2.4 GHz Wi-Fi) but still has bandwidth B

**Shannon-Hartley theorem** (fundamental limit):  
**C = B × log₂(1 + SNR)** bits/s  
→ More bandwidth or better SNR = more capacity.  
This is why 5G uses huge bandwidths (up to 400 MHz channels) and massive MIMO to push SNR.

### 5. Noise – AWGN

**Additive White Gaussian Noise** = ideal thermal noise model.

- **Additive**: adds to signal  
- **White**: flat power spectrum (equal power per Hz)  
- **Gaussian**: amplitude follows bell curve

Real world has other noises (interference, phase noise, quantization), but AWGN is starting point.

### 6. SNR (Signal-to-Noise Ratio)

**SNR** = signal power / noise power (usually in dB: **10 log₁₀(S/N)**).

- Good cellular call: ~10–20 dB  
- High-speed Wi-Fi/5G: can be 30+ dB in good conditions  
- Below ~0 dB → signal buried in noise, but coding/spreading can still recover (spread-spectrum)

### 7. BER (Bit Error Rate)

Probability a received bit is wrong.

- Voice: **BER ~10^{-3}** tolerable  
- Data: **10^{-5} to 10^{-12}** needed (retransmissions + coding fix residual)

BER vs SNR curves are the famous **"waterfall" plots** you see everywhere in telecom papers.

---

## Key Unifying Concept

**Telecommunication is engineering under constraints**:  
limited bandwidth, limited power, lots of noise, multipath, mobility → use math (Fourier, complex, probability) to squeeze maximum reliable bits through.

---

**Status:** ✅ Completed – February 2026  
**Next lesson:** [Signals & Systems](./lesson2.md)


