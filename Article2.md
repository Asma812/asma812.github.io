---
layout: page
title: Quantum Attacks on 5G Protocols
permalink: /Article2
---

<style>
.hero {
  margin-bottom: 60px;
}

.hero h1 {
  margin-bottom: 10px;
  font-size: 2.8rem;
}

.hero p {
  margin: 6px 0;
  color: #a0a0a0;
}

.wrapper {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 60px;
}

.sidebar {
  position: sticky;
  top: 100px;
  align-self: start;
  border-right: 1px solid #2a2a2a;
  padding-right: 20px;
}

.sidebar h3 {
  margin-top: 0;
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.sidebar ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.sidebar li {
  margin-bottom: 14px;
}

.sidebar a {
  text-decoration: none;
  color: #9a9a9a;
  transition: 0.2s ease;
}

.sidebar a:hover {
  color: white;
}

.content {
  min-width: 0;
}

.content h2 {
  margin-top: 60px;
}

.content h4 {
  margin-top: 35px;
}

.content p {
  line-height: 1.8;
  margin-bottom: 20px;
}

.content ul {
  margin-bottom: 25px;
}

.content li {
  margin-bottom: 12px;
  line-height: 1.8;
}

@media (max-width: 900px) {
  .wrapper {
    grid-template-columns: 1fr;
  }

  .sidebar {
    position: relative;
    top: 0;
    border-right: none;
    border-bottom: 1px solid #2a2a2a;
    padding-bottom: 20px;
    margin-bottom: 20px;
  }
}
</style>

<div class="hero">

<h1>Article 2: Quantum Attacks on 5G Protocols</h1>

<p><strong>Focus:</strong> Technical vulnerabilities in the 5G Core (5GC) signaling, authentication, and key exchange.</p>

<p><strong>Oct 2026 • Quantum Security</strong></p>

</div>

<div class="wrapper">

<div class="sidebar">

<h3>Article Structure</h3>

<ul>
  <li><a href="#abstract">Abstract</a></li>
  <li><a href="#introduction">1. Introduction</a></li>
  <li><a href="#vulnerability-mapping">2. Vulnerability Mapping in the 5G Core</a></li>
  <li><a href="#quantum-attack-vectors">3. Quantum Attack Vectors</a></li>
  <li><a href="#post-quantum-5g">4. Transitioning to Post-Quantum 5G</a></li>
  <li><a href="#conclusion">Conclusion</a></li>
</ul>

</div>

<div class="content">

<h2 id="abstract">Abstract</h2>

<p>
The transition to 5G networks introduces a Service-Based Architecture (SBA) that relies heavily on cloud-native principles and Public-Key Infrastructure (PKI) for securing signaling, authentication, and inter-function communication.
</p>

<p>
However, the mathematical foundations of these security protocols—primarily based on the hardness of integer factorization and discrete logarithms—face an existential threat from the advancement of quantum computing.
</p>

<p>
This article provides a comprehensive technical analysis of how Shor’s algorithm and Grover’s algorithm compromise the integrity of 5G protocols.
</p>

<p>
The study maps specific vulnerabilities within the 5G Core (5GC), focusing on the HTTP/2 and TLS signaling pathways between critical Network Functions, including the Access and Mobility Management Function (AMF), Session Management Function (SMF), and Unified Data Management (UDM).
</p>

<p>
Furthermore, we examine the susceptibility of the 5G Authentication and Key Agreement (5G-AKA) framework, demonstrating how a quantum-capable adversary could intercept the Subscription Concealed Identifier (SUCI) or spoof home networks by breaking the underlying asymmetric encryption.
</p>

<p>
The analysis extends to the vulnerability of Diffie-Hellman and Elliptic Curve Key Exchanges (ECDH) used for establishing session keys.
</p>

<p>
To address these vulnerabilities, the article evaluates the integration of Post-Quantum Cryptography (PQC) within 3GPP standards, specifically focusing on ML-KEM (Kyber) and ML-DSA (Dilithium).
</p>

<p>
We propose a sidecar proxy architecture as a viable pathway for PQC-enabled 5G signaling.
</p>

<p>
The findings conclude that the 5G security roadmap must be urgently updated to incorporate quantum-resistant signaling to prevent a total collapse of the mobile trust model.
</p>

<hr>

<h2 id="introduction">1. Introduction</h2>

<p>
The rollout of 5G technology represents more than a mere increase in bandwidth; it is a fundamental architectural shift toward a cloud-native, Service-Based Architecture (SBA).
</p>

<p>
Unlike previous generations that relied heavily on hardware-defined silos, 5G utilizes a decentralized model where Network Functions (NFs) communicate via standardized APIs.
</p>

<p>
While this modularity enables unprecedented flexibility and network slicing capabilities, it also creates a massive reliance on Public-Key Infrastructure (PKI) to maintain the security of the signaling plane.
</p>

<p>
As established in the structure for Article 2, this reliance on classical asymmetric cryptography constitutes the single greatest invisible vulnerability in modern mobile networks.
</p>

<h4>The 5G Security Trust Model</h4>

<p>
The security of 5G is built on a mutual trust model.
</p>

<p>
Every interaction—whether it is a user equipment (UE) attaching to the network or two network functions (like the AMF and UDM) exchanging subscriber data—is governed by cryptographic handshakes.
</p>

<p>
These handshakes typically utilize Elliptic Curve Diffie-Hellman (ECDH) for key exchange and RSA or Elliptic Curve Digital Signature Algorithm (ECDSA) for identity verification.
</p>

<p>
Under classical computational assumptions, these algorithms are considered secure because they rely on mathematical problems that are currently infeasible to solve.
</p>

<h4>The Quantum Threat to PKI</h4>

<p>
The arrival of Cryptographically Relevant Quantum Computers (CRQCs) shatters these assumptions.
</p>

<p>
By utilizing Shor’s algorithm, a quantum computer can solve the discrete logarithm and integer factorization problems in polynomial time.
</p>

<p>
For 5G, this means that the entire signaling plane—the brain of the network—is essentially built on sand.
</p>

<p>
If an adversary can break the PKI, they can effectively impersonate network functions, intercept sensitive subscriber identifiers, and manipulate the signaling that directs traffic flow.
</p>

<p>
As we move toward a fully connected IoT ecosystem, the stakes for 5G security are higher than ever before.
</p>

<p>
The objective of this article is to map these technical vulnerabilities and provide a roadmap for the transition to a Post-Quantum (PQ) 5G Core.
</p>

<p>
This is not a theoretical exercise; it is an urgent requirement to prevent the total compromise of the global mobile trust model.
</p>

<hr>

<h2 id="vulnerability-mapping">2. Vulnerability Mapping in the 5G Core</h2>

<p>
The transition to a Service-Based Architecture (SBA) in 5G means that the network is no longer a collection of physical boxes, but a web of interconnected software services.
</p>

<p>
While this improves scalability, it creates a concentrated reliance on specific cryptographic protocols that are inherently vulnerable to quantum disruption.
</p>

<h4>2.1 Signaling Plane: HTTP/2 and TLS</h4>

<p>
In the 5G Core, Network Functions (NFs) such as the Access and Mobility Management Function (AMF) and the Session Management Function (SMF) communicate using HTTP/2 over TLS 1.2 or 1.3.
</p>

<ul>
  <li>
    <strong>PKI Dependency:</strong> These TLS connections rely on a Public Key Infrastructure (PKI) to authenticate the NFs and encrypt the signaling data.
  </li>

  <li>
    <strong>Quantum Failure:</strong> If an adversary uses Shor’s algorithm to compromise the Root Certificate Authority (CA) or the individual NF certificates, they can execute a “Man-in-the-Middle” (MitM) attack. This would allow the attacker to intercept, read, and even modify signaling messages—such as mobility commands or session setup requests—without detection.
  </li>
</ul>

<h4>2.2 Authentication &amp; Key Agreement (5G-AKA)</h4>

<p>
The 5G-AKA protocol is the gatekeeper of the network, ensuring that only legitimate subscribers can connect.
</p>

<p>
However, several components of this process are high-priority targets for quantum attacks.
</p>

<ul>
  <li>
    <strong>SUCI Interception:</strong> To protect privacy, 5G uses a Subscription Concealed Identifier (SUCI), which is an encrypted version of the subscriber’s permanent identity (SUPI). This encryption typically uses Elliptic Curve Integrated Encryption Scheme (ECIES). A quantum adversary can store these SUCIs and later break the elliptic curve parameters to reveal the subscriber’s identity, enabling long-term tracking and surveillance.
  </li>

  <li>
    <strong>Home Network Spoofing:</strong> The authentication process relies on the UE (User Equipment) verifying the Home Network (HN) via a digital signature. If an attacker breaks the asymmetric keys used for these signatures, they can create a “Rogue Base Station” that perfectly mimics a legitimate carrier, allowing for the complete interception of all subscriber traffic.
  </li>
</ul>

<h4>2.3 Key Exchange: Diffie-Hellman and ECDH</h4>

<p>
Session keys in 5G are generated through a key exchange process, usually involving Diffie-Hellman (DH) or Elliptic Curve Diffie-Hellman (ECDH).
</p>

<ul>
  <li>
    <strong>Discrete Logarithm Vulnerability:</strong> Both DH and ECDH are mathematically built on the discrete logarithm problem. Shor’s algorithm is specifically designed to solve this problem efficiently.
  </li>

  <li>
    <strong>Total Session Exposure:</strong> Once the key exchange is compromised, every subsequent piece of data sent during that session—which is encrypted with symmetric keys (AES)—is effectively exposed. While symmetric encryption is more resilient to quantum attacks, the “delivery” of those keys via vulnerable asymmetric methods remains the fatal flaw in the 5G trust chain.
  </li>
</ul>

<hr>

<h2 id="quantum-attack-vectors">3. Quantum Attack Vectors</h2>

<p>
The threat to 5G protocols is defined by two primary quantum algorithms that fundamentally alter the security margin of classical cryptography.
</p>

<p>
While classical security assumes that certain mathematical problems are hard, quantum mechanics allows for a shortcut through this complexity.
</p>

<h4>3.1 Shor’s Algorithm: The Asymmetric Collapse</h4>

<p>
Shor’s Algorithm is the most direct threat to the 5G Service-Based Architecture (SBA).
</p>

<p>
It is designed to solve two specific problems: integer factorization and finding discrete logarithms.
</p>

<ul>
  <li>
    <strong>Targeting RSA and ECC:</strong> In 5G, RSA is often used for certificate-based authentication, while Elliptic Curve Cryptography (ECC) is used for the 5G-AKA process and SUCI concealment.
  </li>

  <li>
    <strong>Polynomial Time Solution:</strong> On a classical computer, breaking a 2048-bit RSA key takes an exponential amount of time—effectively millions of years. Shor’s Algorithm allows a quantum computer to solve this in polynomial time, reducing the timeframe to hours or even minutes. This renders every digital signature and every asymmetric key exchange within the 5G Core obsolete the moment a sufficiently powerful quantum computer is built.
  </li>
</ul>

<h4>3.2 Grover’s Algorithm: The Symmetric Degradation</h4>

<p>
While symmetric encryption (like AES-256) is more resilient than asymmetric encryption, it is not immune.
</p>

<p>
Grover’s Algorithm provides a quantum speedup for searching unsorted databases, which applies directly to brute-forcing symmetric keys.
</p>

<ul>
  <li>
    <strong>The Quadratic Speedup:</strong> Grover’s Algorithm provides a quadratic improvement in search efficiency. In practical terms, this means the security strength of a symmetric key is effectively halved.
  </li>

  <li>
    <strong>Impact on AES:</strong> An AES-128 key, which is standard for much of today’s network traffic, becomes equivalent to a 64-bit key under a quantum attack. A 64-bit security margin is widely considered vulnerable to high-resource adversaries today. To maintain a 128-bit security margin in the quantum era, 5G protocols must mandate the transition to AES-256, which provides 128 bits of post-quantum security.
  </li>
</ul>

<h4>3.3 The Cumulative Effect</h4>

<p>
The combination of these two vectors creates a “pincer movement” against 5G security.
</p>

<p>
Shor’s Algorithm breaks the initial handshake and identity verification (the “gatekeeper”), while Grover’s Algorithm weakens the encryption of the data payload itself.
</p>

<p>
As established in the structure for Article 2, this necessitates a holistic redesign of the 5G security roadmap to ensure that both identity and data remain protected.
</p>

<hr>

<h2 id="post-quantum-5g">4. Transitioning to Post-Quantum 5G</h2>

<p>
The remediation of quantum vulnerabilities in the 5G Core (5GC) requires a coordinated shift in both cryptographic algorithms and network architecture.
</p>

<p>
The goal is to achieve quantum resilience without sacrificing the low-latency and high-throughput requirements that define 5G performance.
</p>

<h4>4.1 Implementation of ML-KEM and ML-DSA</h4>

<p>
The primary technical defense involves replacing vulnerable asymmetric algorithms with Module-Lattice-Based Key Encapsulation Mechanism (ML-KEM), formerly known as Kyber, and Module-Lattice-Based Digital Signature Algorithm (ML-DSA), formerly known as Dilithium.
</p>

<ul>
  <li>
    <strong>ML-KEM (Kyber):</strong> This is intended to replace Diffie-Hellman and RSA for key exchange. Within the 5G Core, ML-KEM can secure the signaling between Network Functions (NFs) by providing a quantum-resistant wrapper for TLS 1.3 handshakes. Its relatively small key sizes and high computational efficiency make it ideal for the high-frequency signaling environment of the 5GC.
  </li>

  <li>
    <strong>ML-DSA (Dilithium):</strong> This algorithm will replace ECDSA and RSA for digital signatures. It is critical for the 5G-AKA process, where the Home Network must sign authentication vectors to prove its identity to the User Equipment (UE). By implementing ML-DSA, 5G networks can prevent “Rogue Base Station” attacks launched by quantum-capable adversaries.
  </li>
</ul>

<h4>4.2 Sidecar Proxy Architectures for PQC</h4>

<p>
A major challenge in transitioning to PQC is the existing technological debt of 5G hardware that may not natively support new lattice-based math.
</p>

<p>
To solve this, a sidecar proxy architecture is proposed.
</p>

<ul>
  <li>
    <strong>How it Works:</strong> Instead of modifying the core logic of every individual Network Function (AMF, SMF, UPF), a dedicated PQC-enabled proxy (such as an evolved Service Communication Proxy or a sidecar in a service mesh) is deployed alongside each NF.
  </li>

  <li>
    <strong>Encapsulation:</strong> The proxy intercepts standard TLS traffic and upgrades it by encapsulating it within a PQC-secure tunnel before it leaves the local cloud environment. This allows for crypto-agility, enabling operators to update cryptographic standards in the proxy layer without disrupting the underlying 5G services.
  </li>
</ul>

<h4>4.3 3GPP Standards and the Roadmap</h4>

<p>
The transition must be standardized to ensure interoperability between different vendors such as Ericsson, Nokia, and Huawei.
</p>

<ul>
  <li>
    <strong>3GPP Integration:</strong> Future releases of the 3GPP specifications must explicitly define the use of PQC for SUCI concealment and N3/N6 interface protection.
  </li>

  <li>
    <strong>Hybrid Key Exchange:</strong> During the transitionary period, 5G networks should utilize a hybrid approach where keys are derived from both a classical algorithm (like ECDH) and a post-quantum algorithm (like ML-KEM). This ensures that the connection remains secure even if one of the two mathematical foundations is later found to have a classical or quantum weakness.
  </li>
</ul>

<hr>

<h2 id="conclusion">Conclusion</h2>

<p>
The architectural evolution of 5G has created a sophisticated but mathematically brittle ecosystem.
</p>

<p>
The current reliance on classical PKI for signaling, authentication, and key exchange leaves the global mobile infrastructure exposed to the inevitability of quantum disruption.
</p>

<p>
Shor’s and Grover’s algorithms do not merely represent a future risk; they define a deadline for the integrity of modern telecommunications.
</p>

<p>
The integration of ML-KEM and ML-DSA, supported by agile sidecar architectures, provides a clear technical path forward.
</p>

<p>
However, this transition must begin immediately within the 3GPP standardization process to ensure that the 5G security roadmap is fundamentally quantum-resistant.
</p>

<p>
Without these updates, the promise of 5G as a secure foundation for the Fourth Industrial Revolution remains at high risk.
</p>

</div>
</div>

