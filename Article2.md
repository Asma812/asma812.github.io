---
layout: page
title: Quantum Attacks on 5G Protocols
permalink: /Article2
---

# Article 2: Quantum Attacks on 5G Protocols

**Focus**: Technical vulnerabilities in the 5G Core (5GC) signaling, authentication, and key exchange.

**Oct 2026 • Quantum Security**


## Abstract

The transition to 5G networks introduces a Service-Based Architecture (SBA) that relies heavily on cloud-native principles and Public-Key Infrastructure (PKI) for securing signaling, authentication, and inter-function communication. However, the mathematical foundations of these security protocols—primarily based on the hardness of integer factorization and discrete logarithms—face an existential threat from the advancement of quantum computing. This article provides a comprehensive technical analysis of how Shor’s algorithm and Grover’s algorithm compromise the integrity of 5G protocols.
The study maps specific vulnerabilities within the 5G Core (5GC), focusing on the HTTP/2 and TLS signaling pathways between critical Network Functions, including the Access and Mobility Management Function (AMF), Session Management Function (SMF), and Unified Data Management (UDM). Furthermore, we examine the susceptibility of the 5G Authentication and Key Agreement (5G-AKA) framework, demonstrating how a quantum-capable adversary could intercept the Subscription Concealed Identifier (SUCI) or spoof home networks by breaking the underlying asymmetric encryption. The analysis extends to the vulnerability of Diffie-Hellman and Elliptic Curve Key Exchanges (ECDH) used for establishing session keys.
To address these vulnerabilities, the article evaluates the integration of Post-Quantum Cryptography (PQC) within 3GPP standards, specifically focusing on ML-KEM (Kyber) and ML-DSA (Dilithium). We propose a sidecar proxy architecture as a viable pathway for PQC-enabled 5G signaling. The findings conclude that the 5G security roadmap must be urgently updated to incorporate quantum-resistant signaling to prevent a total collapse of the mobile trust model.

---

### 1. Introduction

The rollout of 5G technology represents more than a mere increase in bandwidth; it is a fundamental architectural shift toward a cloud-native, Service-Based Architecture (SBA). Unlike previous generations that relied heavily on hardware-defined silos, 5G utilizes a decentralized model where Network Functions (NFs) communicate via standardized APIs. While this modularity enables unprecedented flexibility and network slicing capabilities, it also creates a massive reliance on Public-Key Infrastructure (PKI) to maintain the security of the signaling plane. As established in the structure for Article 2, this reliance on classical asymmetric cryptography constitutes the single greatest "invisible" vulnerability in modern mobile networks.

#### The 5G Security Trust Model

The security of 5G is built on a "mutual trust" model. Every interaction—whether it is a user equipment (UE) attaching to the network or two network functions (like the AMF and UDM) exchanging subscriber data—is governed by cryptographic handshakes. These handshakes typically utilize Elliptic Curve Diffie-Hellman (ECDH) for key exchange and RSA or Elliptic Curve Digital Signature Algorithm (ECDSA) for identity verification. Under classical computational assumptions, these algorithms are considered secure because they rely on mathematical problems that are currently infeasible to solve.

#### The Quantum Threat to PKI

The arrival of Cryptographically Relevant Quantum Computers (CRQCs) shatters these assumptions. By utilizing Shor’s algorithm, a quantum computer can solve the discrete logarithm and integer factorization problems in polynomial time. For 5G, this means that the entire signaling plane—the "brain" of the network—is essentially built on sand. If an adversary can break the PKI, they can effectively impersonate network functions, intercept sensitive subscriber identifiers, and manipulate the signaling that directs traffic flow.
As we move toward a fully connected IoT ecosystem, the stakes for 5G security are higher than ever before. The objective of this article is to map these technical vulnerabilities and provide a roadmap for the transition to a Post-Quantum (PQ) 5G Core. This is not a theoretical exercise; it is an urgent requirement to prevent the total compromise of the global mobile trust model.

---

### 2. Vulnerability Mapping in the 5G Core

The transition to a Service-Based Architecture (SBA) in 5G means that the network is no longer a collection of physical boxes, but a web of interconnected software services. While this improves scalability, it creates a concentrated reliance on specific cryptographic protocols that are inherently vulnerable to quantum disruption.

#### 2.1 Signaling Plane: HTTP/2 and TLS

In the 5G Core, Network Functions (NFs) such as the Access and Mobility Management Function (AMF) and the Session Management Function (SMF) communicate using HTTP/2 over TLS 1.2 or 1.3.

- **PKI Dependency**: These TLS connections rely on a Public Key Infrastructure (PKI) to authenticate the NFs and encrypt the signaling data.
- **Quantum Failure**: If an adversary uses Shor’s algorithm to compromise the Root Certificate Authority (CA) or the individual NF certificates, they can execute a "Man-in-the-Middle" (MitM) attack. This would allow the attacker to intercept, read, and even modify signaling messages—such as mobility commands or session setup requests—without detection.

#### 2.2 Authentication & Key Agreement (5G-AKA)

The 5G-AKA protocol is the gatekeeper of the network, ensuring that only legitimate subscribers can connect. However, several components of this process are high-priority targets for quantum attacks.

- **SUCI Interception**: To protect privacy, 5G uses a Subscription Concealed Identifier (SUCI), which is an encrypted version of the subscriber's permanent identity (SUPI). This encryption typically uses Elliptic Curve Integrated Encryption Scheme (ECIES). A quantum adversary can store these SUCIs and later break the elliptic curve parameters to reveal the subscriber’s identity, enabling long-term tracking and surveillance.
- **Home Network Spoofing**: The authentication process relies on the UE (User Equipment) verifying the Home Network (HN) via a digital signature. If an attacker breaks the asymmetric keys used for these signatures, they can create a "Rogue Base Station" that perfectly mimics a legitimate carrier, allowing for the complete interception of all subscriber traffic.

#### 2.3 Key Exchange: Diffie-Hellman and ECDH

Session keys in 5G are generated through a key exchange process, usually involving Diffie-Hellman (DH) or Elliptic Curve Diffie-Hellman (ECDH).

- **Discrete Logarithm Vulnerability**: Both DH and ECDH are mathematically built on the discrete logarithm problem. Shor’s algorithm is specifically designed to solve this problem efficiently.
- **Total Session Exposure**: Once the key exchange is compromised, every subsequent piece of data sent during that session—which is encrypted with symmetric keys (AES)—is effectively exposed. While symmetric encryption is more resilient to quantum attacks, the "delivery" of those keys via vulnerable asymmetric methods remains the fatal flaw in the 5G trust chain.


---

### 3. Quantum Attack Vectors

The threat to 5G protocols is defined by two primary quantum algorithms that fundamentally alter the security margin of classical cryptography. While classical security assumes that certain mathematical problems are "hard," quantum mechanics allows for a shortcut through this complexity.

#### 3.1 Shor’s Algorithm: The Asymmetric Collapse

Shor’s Algorithm is the most direct threat to the 5G Service-Based Architecture (SBA). It is designed to solve two specific problems: integer factorization and finding discrete logarithms.

**Targeting RSA and ECC**: In 5G, RSA is often used for certificate-based authentication, while Elliptic Curve Cryptography (ECC) is used for the 5G-AKA process and SUCI concealment.

**Polynomial Time Solution**: On a classical computer, breaking a 2048-bit RSA key takes an exponential amount of time—effectively millions of years. Shor’s Algorithm allows a quantum computer to solve this in polynomial time, reducing the timeframe to hours or even minutes. This renders every digital signature and every asymmetric key exchange within the 5G Core obsolete the moment a sufficiently powerful quantum computer is built.

#### 3.2 Grover’s Algorithm: The Symmetric Degradation

While symmetric encryption (like AES-256) is more resilient than asymmetric encryption, it is not immune. Grover’s Algorithm provides a quantum speedup for searching unsorted databases, which applies directly to brute-forcing symmetric keys.
**The Quadratic Speedup**: Grover’s Algorithm provides a quadratic improvement in search efficiency. In practical terms, this means the security strength of a symmetric key is effectively halved.
**Impact on AES**: An AES-128 key, which is standard for much of today's network traffic, becomes equivalent to a 64-bit key under a quantum attack. A 64-bit security margin is widely considered vulnerable to high-resource adversaries today. To maintain a 128-bit security margin in the quantum era, 5G protocols must mandate the transition to AES-256, which provides 128 bits of post-quantum security.

#### 3.3 The Cumulative Effect

The combination of these two vectors creates a "pincer movement" against 5G security. Shor’s Algorithm breaks the initial handshake and identity verification (the "gatekeeper"), while Grover’s Algorithm weakens the encryption of the data payload itself. As established in the structure for Article 2, this necessitates a holistic redesign of the 5G security roadmap to ensure that both identity and data remain protected.

---

### 4. Transitioning to Post-Quantum 5G

The remediation of quantum vulnerabilities in the 5G Core (5GC) requires a coordinated shift in both cryptographic algorithms and network architecture. The goal is to achieve quantum resilience without sacrificing the low-latency and high-throughput requirements that define 5G performance.

#### 4.1 Implementation of ML-KEM and ML-DSA
The primary technical defense involves replacing vulnerable asymmetric algorithms with Module-Lattice-Based Key Encapsulation Mechanism (ML-KEM), formerly known as Kyber, and Module-Lattice-Based Digital Signature Algorithm (ML-DSA), formerly known as Dilithium. 

- **ML-KEM (Kyber)**: This is intended to replace Diffie-Hellman and RSA for key exchange. Within the 5G Core, ML-KEM can secure the signaling between Network Functions (NFs) by providing a quantum-resistant wrapper for TLS 1.3 handshakes. Its relatively small key sizes and high computational efficiency make it ideal for the high-frequency signaling environment of the 5GC. 

- **ML-DSA (Dilithium)**: This algorithm will replace ECDSA and RSA for digital signatures. It is critical for the 5G-AKA process, where the Home Network must sign authentication vectors to prove its identity to the User Equipment (UE). By implementing ML-DSA, 5G networks can prevent "Rogue Base Station" attacks launched by quantum-capable adversaries. 


#### 4.2 Sidecar Proxy Architectures for PQC

A major challenge in transitioning to PQC is the existing "technological debt" of 5G hardware that may not natively support new lattice-based math. To solve this, a sidecar proxy architecture is proposed. 

How it Works: Instead of modifying the core logic of every individual Network Function (AMF, SMF, UPF), a dedicated PQC-enabled proxy (such as an evolved Service Communication Proxy or a sidecar in a service mesh) is deployed alongside each NF. 

Encapsulation: The proxy intercepts standard TLS traffic and "upgrades" it by encapsulating it within a PQC-secure tunnel before it leaves the local cloud environment. This allows for crypto-agility, enabling operators to update cryptographic standards in the proxy layer without disrupting the underlying 5G services. 

#### 4.3 3GPP Standards and the Roadmap

The transition must be standardized to ensure interoperability between different vendors (e.g., Ericsson, Nokia, Huawei). 

3GPP Integration: Future releases of the 3GPP specifications must explicitly define the use of PQC for SUCI concealment and N3/N6 interface protection. 

Hybrid Key Exchange: During the transitionary period, 5G networks should utilize a hybrid approach where keys are derived from both a classical algorithm (like ECDH) and a post-quantum algorithm (like ML-KEM). This ensures that the connection remains secure even if one of the two mathematical foundations is later found to have a classical or quantum weakness. 


---

### Conclusion

The architectural evolution of 5G has created a sophisticated but mathematically "brittle" ecosystem. The current reliance on classical PKI for signaling, authentication, and key exchange leaves the global mobile infrastructure exposed to the inevitability of quantum disruption. Shor’s and Grover’s algorithms do not merely represent a future risk; they define a deadline for the integrity of modern telecommunications. 

The integration of ML-KEM and ML-DSA, supported by agile sidecar architectures, provides a clear technical path forward. However, this transition must begin immediately within the 3GPP standardization process to ensure that the 5G security roadmap is fundamentally quantum-resistant. Without these updates, the promise of 5G as a secure foundation for the Fourth Industrial Revolution remains at high risk.

