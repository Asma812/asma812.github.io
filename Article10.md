# Article 10: Malware Lineage: Using Machine Learning to Map "Code DNA"

**The Concept**: Malware is rarely written from scratch. Attackers heavily reuse code modules. This article explores how CTI analysts use Function Call Graphs and Machine Learning to attribute new malware samples to known threat actors by analyzing structural "Code DNA."

**Abstract**: Moving beyond simple hashes — using structural similarity to track the evolution of malware families.

---

## Abstract

In the modern threat landscape, polymorphic and metamorphic malware has rendered traditional hash-based detection largely obsolete. As adversaries use automated tools to generate unique binaries for every target, the focus has shifted toward identifying the underlying **"Code DNA"** — the functional and structural logic that remains consistent across malware families.

This article explores **Malware Lineage Mapping**, a methodology that leverages Machine Learning to detect code reuse and attribute new samples to known Advanced Persistent Threat (APT) groups. It details the transformation of binaries into Function Call Graphs (FCG), their conversion into high-dimensional vectors, and the application of Graph Neural Networks (GNNs) and clustering algorithms like DBSCAN to uncover "Shared Library Fingerprints."

By identifying these overlaps, CTI analysts can bypass obfuscation and achieve high-confidence attribution to groups such as **Lazarus** or **APT28**. The core insight: while attackers can easily change a file’s hash, their economic reliance on code reuse remains their primary vulnerability — the **"Achilles' heel"** of sophisticated malware development.

---

### 1. Introduction: The Death of the Static Hash

In the early days of cybersecurity, detection relied on cryptographic hashes (MD5, SHA-256) to identify known malicious files. By 2026, the static hash has become a relic.

#### 1.1 The Rise of Polymorphism and Hash-Shifting

Modern APT groups rarely reuse the same binary. Polymorphic engines and automated packers allow them to generate millions of unique variants by altering non-functional elements. A single ransomware campaign can produce 1,000 different hashes, making each sample appear unrelated to traditional signature-based defenses.

#### 1.2 The Economic Constraint of Code Reuse

Writing entirely new malware from scratch is expensive and time-consuming. Attackers, like legitimate developers, rely on modular libraries, proven code snippets, and shared frameworks — from custom AES implementations to specific UAC bypass methods and C2 protocols.

#### 1.3 Toward a "Genetic" Understanding of Malware

Treating malware as a biological organism, its **Function Call Graphs (FCG)** represent the "Code DNA." Even when the outer appearance (hash, packer) changes, the underlying logic often stays consistent. This enables a deeper question: *Does this binary share a common ancestor with known threat actors?*

---

### 2. Static Analysis & Feature Extraction: Uncovering the DNA

Before applying ML, structural features must be extracted from the binary.

#### 2.1 Decompiling and Recovery of Logic

Tools like **Ghidra**, **IDA Pro**, or **Radare2** are used to disassemble stripped binaries.

- **Control Flow Graph (CFG)**: Maps logic within individual functions (jumps, loops, branches).
- **Function Call Graph (FCG)**: A directed graph where nodes are functions and edges represent calls. This is the most stable genetic marker of a malware family.

#### 2.2 Vectorization: Turning Code into Math

- **Node Attributes**: Enrich functions with API call types (networking, crypto, filesystem) and instruction complexity.
- **Graph Embeddings**: Techniques like Graph2Vec convert the FCG into fixed-length vectors for numerical comparison.
- **Shared Library Fingerprinting**: Identify reused modules (e.g., custom RC4 ciphers or credential harvesters) across samples.

In vector space, malware samples sharing significant Code DNA naturally cluster together.

---

### 3. The Machine Learning Approach: Identifying the Lineage

#### 3.1 Graph Neural Networks (GNN) for Structural Matching

GNNs are the state-of-the-art for graph-structured data:
- Calculate **Similarity Scores** between new samples and historical databases.
- Remain effective even with function reordering or added junk code (permutation invariant).

#### 3.2 Clustering for Family Discovery

Use unsupervised algorithms such as **DBSCAN**:
- Automatically discover clusters of related malware.
- Map evolutionary timelines by measuring distances between samples over time.
- Identify when new features are added or vulnerabilities are patched within a family.

---

### 4. Attribution Strategy: The Cost of Originality

#### 4.1 Identifying the Author's "Handwriting"

Developer habits — error handling patterns, obfuscation styles, or preferred libraries — create detectable fingerprints.

- **Lazarus Group**: Frequently reuses custom encryption modules and network tunneling protocols.
- **APT28 (Fancy Bear)**: Consistent credential harvesting modules show high structural overlap across campaigns.

A 95% match in a core module can provide high-confidence attribution.

#### 4.2 The Economic Burden of Malware Development

Rewriting an entire codebase for every operation introduces bugs and delays. Most groups reuse 70-80% of existing code. This overlap is the **Achilles' heel** that ML-driven lineage tracking exploits.

---

### Conclusion: The Genetic Map of Global Threats

The transition from hash-based detection to ML-driven Malware Lineage Mapping marks a major evolution in cybersecurity. By converting Function Call Graphs into mathematical structures and applying Graph Neural Networks, analysts can map the evolutionary tree of malware families with precision.

In 2026, code reuse — once a convenience for attackers — has become their greatest liability. By maintaining rich historical databases of "Code DNA," CTI teams can track sophisticated actors across campaigns, delivery methods, and infrastructure changes, ultimately building more resilient and proactive defenses.

**Key Takeaway**: Attackers can change their appearance, but they cannot easily hide their lineage.
