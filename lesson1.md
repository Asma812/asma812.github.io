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
