---
layout: page
title: Lesson 1 - Foundations
permalink: /lesson1/
---

The essentials that underpin all telecom concepts.

**Key Concepts:**  
- Linear algebra (vectors, matrices)  
- Complex numbers  
- Probability & statistics  
- Fourier Series & Fourier Transform  
- Laplace Transform  
- Convolution  

**Why It Matters:** Telecom revolves around mathematical modeling of signals. 

<grok-card data-id="fd14a1" data-type="image_card" data-plain-type="render_searched_image"  data-arg-size="LARGE" ></grok-card>

  

**Labs/Practice:** Analyzed signal transformations in MATLAB.  

**Tools Used:** MATLAB, Python (NumPy).  

# Lesson 1 – Foundations (Non-negotiable)

**Telecommunications Engineering Self-Study – Asma's Portfolio**  
**February 2026 – Tunis**

---

## Why Foundations Matter So Much

Telecommunications is **not** primarily about hardware or protocols at first — it is about **moving information reliably through a noisy, imperfect world**.  
Every later topic (modulation, coding, 5G, fiber, security attacks) builds directly on these ideas.

- If you don't understand why noise kills bits → you won't grasp BER curves.  
- If complex numbers feel alien → QPSK, OFDM, and beamforming will remain mysterious.  
- If bandwidth and SNR are fuzzy → Shannon's limit and 5G spectral efficiency won't click.

**Think of this as learning the alphabet before writing novels.**

---

## Part A: Mathematics – The Language of Telecom  
(≈60–70% of the "brain work")

You don't need to become a pure mathematician, but telecom uses **very specific math tools** almost daily.

### 1. Linear Algebra (Vectors & Matrices)

Signals and channels are often multi-dimensional.

- A simple radio signal uses two dimensions: **In-phase (I)** and **Quadrature (Q)** → that's a 2D vector.  
- MIMO (Multiple Input Multiple Output) in 4G/5G uses matrices: if you have 4 antennas transmit and 4 receive, the channel is a 4×4 matrix describing how each path mixes signals.  
- Beamforming = applying a weight vector to steer energy.

**Example**  
A transmitted symbol in QAM is a point in 2D space:  
**s = [I, Q]**  
Received signal: **r = H × s + n** (matrix multiplication + noise vector).  
Linear algebra lets you invert or estimate **H**.

### 2. Complex Numbers  
**The single most important "trick" in telecom.**

A sinusoid like cos(ωt) or sin(ωt) can be written compactly as the real or imaginary part of **e^{jωt}** (Euler's formula: **e^{jθ} = cosθ + j sinθ**).

**Why this matters hugely:**

- Phase and amplitude become **one complex number** instead of two separate equations.  
- Modulation (changing amplitude/phase) = multiplying by a complex scalar.  
- Frequency shifts = multiplying by **e^{j2πft}**.  
- Convolution in time ↔ multiplication in frequency (much easier with complex exponentials).

**Quick example**  
In QPSK, the four symbols are at angles 45°, 135°, 225°, 315° → simply **1+j**, **-1+j**, **-1-j**, **1-j** (after scaling).  
Adding noise → the received point moves in the complex plane; decision is nearest constellation point.

### 3. Probability & Statistics

Noise is random → everything probabilistic.

- AWGN = Additive White Gaussian Noise → noise samples ~ Normal(0, σ²).  
- Bit Error Rate (BER) = probability a bit flips.  
- Outage probability, fading statistics (Rayleigh/Rician distributions), error correction success rates.

**Key mindset**  
In telecom we rarely say "this will work"; we say "this will work with 99.999% probability" or "BER < 10^{-5}".

### 4. Fourier Series & Fourier Transform

Any (reasonable) signal = sum of sinusoids at different frequencies.

- **Time domain**: s(t) (waveform you see on oscilloscope)  
- **Frequency domain**: S(f) (spectrum analyzer view) → shows which frequencies carry power  
- **Bandwidth** = range where most energy lives  
- Filtering = multiplying in frequency domain (easy) instead of convolving in time  
- OFDM (core of Wi-Fi, LTE, 5G) splits wideband channel into many narrow subcarriers → each flat-fading and easy to equalize

**Intuition example**  
A square wave looks sharp in time → many high-frequency harmonics in frequency. Sharp edges = wide bandwidth.

### 5. Laplace Transform

Generalizes Fourier for stability analysis (mostly analog/control side, but useful).

- Used to analyze filters, system poles/zeros.  
- In telecom mostly seen indirectly (filter design, PLLs in radios).

### 6. Convolution

The mathematical operation behind **every linear filter**.

Output **y(t) = x(t) * h(t)** (input convolved with impulse response).

- In frequency domain → **Y(f) = X(f) × H(f)** (multiplication = much faster)  
- Digital filters (FIR/IIR) = discrete convolution

**Practice tip**  
A matched filter (optimal for detecting known signal in AWGN) is literally the time-reversed conjugate of the signal → convolution peaks at correct timing.

**Quick self-check questions** (try mentally):

- Why can we represent a carrier signal as **Re{A e^{j(ωt + φ)}}** instead of **A cos(ωt + φ)**?  
- If I have two signals x(t) and y(t), what does **x(t) * y(t)** represent in frequency domain?

---

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
