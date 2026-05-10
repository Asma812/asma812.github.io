# Article 2: Quantum Attacks on 5G Protocols

**Focus**: Technical vulnerabilities in the 5G Core (5GC) signaling, authentication, and key exchange.

**Abstract**: Analysis of how Shor’s algorithm compromises the mathematical foundations of the 5G Service-Based Architecture (SBA).

---

## Abstract

The transition to 5G networks introduces a cloud-native Service-Based Architecture (SBA) that relies heavily on Public-Key Infrastructure (PKI) for securing signaling, authentication, and inter-function communication. However, the mathematical foundations of these protocols—primarily based on integer factorization and discrete logarithms—face an existential threat from quantum computing.

This article provides a technical analysis of how **Shor’s Algorithm** and **Grover’s Algorithm** compromise 5G protocols. It maps vulnerabilities in the 5G Core, including HTTP/2 + TLS signaling, 5G-AKA authentication, SUCI protection, and Diffie-Hellman/Elliptic Curve key exchanges.

The article evaluates the integration of Post-Quantum Cryptography (PQC) through **ML-KEM (Kyber)** and **ML-DSA (Dilithium)**, and proposes sidecar proxy architectures as a practical migration path. The findings stress that the 5G security roadmap must be urgently updated to incorporate quantum-resistant signaling.

---

### 1. Introduction

The rollout of 5G represents a fundamental shift to a cloud-native, Service-Based Architecture (SBA). Network Functions (NFs) communicate via standardized APIs, enabling flexibility and network slicing. However, this modularity creates a massive dependency on Public-Key Infrastructure (PKI) for securing the signaling plane.

#### The 5G Security Trust Model

5G security is built on mutual authentication and cryptographic handshakes. Interactions between User Equipment (UE), Access and Mobility Management Function (AMF), Session Management Function (SMF), and Unified Data Management (UDM) rely on:
- Elliptic Curve Diffie-Hellman (ECDH) for key exchange
- RSA or ECDSA for identity verification

While secure against classical computers, these algorithms are vulnerable to quantum attacks.

#### The Quantum Threat to PKI

Cryptographically Relevant Quantum Computers (CRQCs) using **Shor’s Algorithm** can solve integer factorization and discrete logarithm problems in polynomial time. This threatens the entire 5G signaling plane, enabling impersonation of network functions, interception of subscriber data, and manipulation of network behavior.

---

### 2. Vulnerability Mapping in the 5G Core

The Service-Based Architecture increases scalability but concentrates risk on specific cryptographic protocols.

#### 2.1 Signaling Plane: HTTP/2 and TLS

Network Functions communicate using **HTTP/2 over TLS 1.2/1.3**.

- **PKI Dependency**: TLS connections rely on certificates for authentication and encryption.
- **Quantum Failure Point**: A quantum adversary can compromise Root CAs or NF certificates, enabling Man-in-the-Middle (MitM) attacks on signaling messages (mobility commands, session setups, etc.).

#### 2.2 Authentication & Key Agreement (5G-AKA)

- **SUCI Interception**: The Subscription Concealed Identifier (SUCI) is protected using Elliptic Curve Integrated Encryption Scheme (ECIES). Quantum computers can later decrypt stored SUCIs to reveal permanent subscriber identities (SUPI).
- **Home Network Spoofing**: Attackers can break digital signatures to impersonate the Home Network, deploying rogue base stations for full traffic interception.

#### 2.3 Key Exchange: Diffie-Hellman and ECDH

Session keys rely on Diffie-Hellman or Elliptic Curve Diffie-Hellman. Both are based on the discrete logarithm problem, which Shor’s Algorithm solves efficiently, exposing entire sessions once keys are derived.

---

### 3. Quantum Attack Vectors

#### 3.1 Shor’s Algorithm: The Asymmetric Collapse

Shor’s Algorithm targets RSA and ECC:
- Breaks 2048-bit RSA keys and ECC in hours or minutes (versus millions of years classically).
- Renders digital signatures and key exchanges in 5G-AKA and TLS obsolete.

#### 3.2 Grover’s Algorithm: The Symmetric Degradation

Grover’s Algorithm provides a quadratic speedup for brute-force searches:
- Reduces AES-128 effective security to 64 bits (considered weak).
- Recommendation: Transition to **AES-256** for 128-bit post-quantum security.

#### 3.3 The Cumulative Effect

Shor’s Algorithm breaks the handshake and authentication layer, while Grover’s weakens the symmetric payload encryption — creating a comprehensive threat to the 5G trust model.

---

### 4. Transitioning to Post-Quantum 5G

#### 4.1 Implementation of ML-KEM and ML-DSA

- **ML-KEM (Kyber)**: Replaces Diffie-Hellman/RSA for quantum-resistant key encapsulation. Ideal for high-frequency 5GC signaling due to efficient performance.
- **ML-DSA (Dilithium)**: Replaces ECDSA/RSA for digital signatures. Critical for securing 5G-AKA and preventing rogue base station attacks.

#### 4.2 Sidecar Proxy Architectures for PQC

To address legacy hardware constraints:
- Deploy PQC-enabled **sidecar proxies** alongside each Network Function.
- Proxies intercept and upgrade standard TLS traffic into PQC-secure tunnels.
- Enables **crypto-agility** — updating cryptographic standards without disrupting core services.

#### 4.3 3GPP Standards and the Roadmap

- Future 3GPP releases must standardize PQC for SUCI, N3/N6 interfaces, and signaling.
- Adopt **hybrid key exchange** (classical + PQC) during the transition period for defense-in-depth.

---

### Conclusion

The 5G Service-Based Architecture, while innovative, is built on mathematically brittle foundations. The reliance on classical PKI for signaling, authentication, and key exchange leaves global mobile networks exposed to quantum disruption.

**Shor’s** and **Grover’s** algorithms define a clear deadline for 5G security. Integrating **ML-KEM**, **ML-DSA**, and sidecar proxy architectures offers a viable path forward. The 5G security roadmap must be updated immediately within 3GPP standards to ensure quantum resistance.

Without urgent action, the promise of 5G as a secure foundation for the Fourth Industrial Revolution remains at significant risk.
