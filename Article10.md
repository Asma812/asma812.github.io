# Article 10: Malware Lineage: Using Machine Learning to Map "Code DNA"

**The Concept**: Malware is rarely written from scratch. Attackers heavily reuse code modules. This article explores how CTI analysts use Function Call Graphs and Machine Learning to attribute new malware samples to known threat actors by analyzing structural "Code DNA."

**Abstract**: Moving beyond simple hashes — using structural similarity to track the evolution of malware families.

---

## Abstract

In the modern threat landscape, the rapid proliferation of polymorphic and metamorphic malware has rendered traditional, hash-based detection methods largely obsolete. As adversaries increasingly utilize automated toolsets to generate unique binaries for every target, the cybersecurity community has shifted its focus toward the underlying "Code DNA"—the functional and structural logic that remains consistent across malware families. This article provides a technical exploration of Malware Lineage Mapping, a methodology that utilizes Machine Learning (ML) to identify code reuse and attribute new samples to known Advanced Persistent Threat (APT) groups.

The research details the transformation of compiled binaries into Function Call Graphs (FCG), representing the model's structural logic as high-dimensional mathematical vectors. We analyze the application of advanced ML architectures, specifically Graph Neural Networks (GNNs) and clustering algorithms like DBSCAN, to detect "Shared Library Fingerprints" across seemingly unrelated attacks. By identifying these overlaps, Cyber Threat Intelligence (CTI) analysts can bypass superficial obfuscation to achieve high-confidence attribution to actors such as Lazarus or APT28. The findings conclude that while attackers can easily change a file’s hash, the economic and operational necessity of code reuse remains their primary vulnerability—an "Achilles' heel" that allows for the systemic tracking of malware evolution in the 2026 digital ecosystem.


---

### 1. Introduction: The Death of the Static Hash

In the early decades of cybersecurity, threat detection was primarily a game of "known-bad" identification. Security software relied on cryptographic hashes (such as MD5 or SHA-256) to identify malicious files. If a file's hash matched a known entry in a threat database, it was blocked. However, by 2026, the static hash has become a relic of a simpler era.


#### 1.1 The Rise of Polymorphism and Hash-Shifting

Modern threat actors, particularly state-sponsored APT groups, rarely use the same binary twice. Through the use of polymorphic engines and automated packing services, an attacker can generate millions of unique versions of the same malware. By changing a single non-functional byte or reordering metadata, the file's cryptographic hash changes completely, effectively making it "invisible" to traditional signature-based scanners.

This "hash-shifting" technique allows malware to bypass the perimeter multiple times. A single piece of ransomware can be distributed to 1,000 different targets, and each target will receive a file with a unique hash. From a legacy security perspective, these look like 1,000 unrelated threats, when in reality, they are identical in function.


#### 1.2 The Economic Constraint of Code Reuse

While it is easy for an attacker to change a file's hash, it is incredibly difficult and expensive to write entirely new malware from scratch. Like legitimate software developers, malware authors rely on libraries, modular frameworks, and "proven" code snippets. Whether it is a specific implementation of an AES encryption routine, a unique method for bypassing User Account Control (UAC), or a proprietary communication protocol for C2 (Command and Control) servers, these modules are reused across years of campaigns.

#### 1.3 Toward a "Genetic" Understanding of Malware

To counter the failure of hashes, the industry has moved toward Code Lineage Mapping. If we treat a malware binary as a biological organism, the individual functions and the way they call each other represent the "Code DNA." Even if the "skin" (the hash or the packer) changes, the "skeleton" (the logic) remains the same.

By leveraging your expertise in Cybersecurity and Machine Learning, we can move beyond the surface level. Instead of asking "Does this hash exist in my database?", we ask "Does the structural logic of this binary share a common ancestor with a known threat actor?" This section sets the stage for using Function Call Graphs (FCG) and Machine Learning to turn the attacker's own efficiency—their reliance on code reuse—into their greatest vulnerability.


---

### 2. Static Analysis & Feature Extraction: Uncovering the DNA

Before applying Machine Learning, we must first extract features that represent the "intellectual signature" of the malware. Unlike dynamic analysis, which observes what the malware does, static analysis focuses on what the malware is at a structural level.


#### 2.1 Decompiling and Recovery of Logic

The first step is to reverse the compilation process. Since APT-level malware is typically distributed as stripped binaries (without symbols or debugging information), we use tools like Ghidra, IDA Pro, or Radare2 to disassemble the machine code.

The Control Flow Graph (CFG): At the function level, we reconstruct the Control Flow Graph. This maps the internal logic—the jumps, loops, and conditional branches—within a single function. While an attacker can easily swap a JZ (jump if zero) for a JNZ (jump if not zero) to change a hash, the overall complexity and structure of the function's logic often remain consistent across versions.

The Function Call Graph (FCG): At the program level, we extract the FCG. This is a directed graph where each node is a function and each edge represents a "call" from one function to another. The FCG is the most stable "genetic marker" of a malware family; it represents the developer's high-level architectural choices, which are rarely altered due to the risk of breaking the malware's functionality.


#### 2.2 Vectorization: Turning Code into Math

To use Machine Learning, the FCG must be converted into a mathematical format. This process, known as vectorization, allows us to compare two different binaries numerically.

Node Attributes: We enrich the FCG by labeling nodes with attributes such as the types of API calls made (e.g., networking, filesystem, or cryptographic APIs) and the complexity of the assembly instructions.

Graph Embeddings: We use techniques like Graph2Vec or Structure2Vec to transform the entire graph into a fixed-length vector. In this high-dimensional space, malware samples that share significant "Code DNA" will cluster together, even if their surface-level appearances are different.

Shared Library Fingerprinting: We specifically extract the code for common tasks—such as a custom implementation of an RC4 stream cipher. By vectorizing these specific modules, we can identify "Shared Library Fingerprints". If a new, unknown sample uses the exact same non-standard encryption routine as a known Lazarus backdoor, it provides a strong lead for attribution. 


---

### 3. The Machine Learning Approach: Identifying the Lineage

With our features extracted and vectorized, we apply Machine Learning models to perform the heavy lifting of classification and attribution.

#### 3.1 Graph Neural Networks (GNN) for Structural Matching

In 2026, Graph Neural Networks (GNNs) are the state-of-the-art for this task. Unlike standard neural networks that process linear data, GNNs are designed to operate directly on the graph structure of the FCG.

Similarity Scoring: The GNN is trained to calculate a "Similarity Score" between a new, unknown sample and a historical database of thousands of known malware samples.

Invariant Detection: The GNN is particularly effective because it is "permutation invariant." This means it can recognize the same logical structure even if the attacker has reordered the functions or added "junk code" (dead code) to confuse traditional scanners.


#### 3.2 Clustering for Family Discovery

When faced with a completely new threat, we use unsupervised learning—specifically DBSCAN (Density-Based Spatial Clustering of Applications with Noise)—to find its place in the malware ecosystem.

Mapping the Family Tree: DBSCAN allows us to identify clusters of malware that share a lineage. If a new sample falls into a high-density cluster associated with APT28, we can confidently attribute it to that group, even if the malware uses a new delivery vector or C2 protocol.

Detecting Code Evolution: By looking at the distance between samples in a cluster over time, we can literally map the evolution of a malware family, seeing where developers added new features or patched vulnerabilities in their own "Code DNA."

---

### 4. Attribution Strategy: The Cost of Originality

In the realm of Cyber Threat Intelligence (CTI), attribution is often the most difficult task. However, by using the ML-driven "Code DNA" mapping described in Section 3, analysts can move from "guessing" to "mathematical probability."

#### 4.1 Identifying the Author's "Handwriting"

Every developer has unique coding habits—preferences for certain variable naming conventions, specific ways of handling error states, or a reliance on particular obfuscation techniques.

The Lazarus Fingerprint: For example, the Lazarus Group has historically reused specific custom encryption modules and network tunneling protocols across multiple campaigns. By identifying these modules in a new, unclassified binary, an analyst can link a seemingly random ransomware attack to a state-sponsored infrastructure.

APT28 (Fancy Bear) Infrastructure: Similarly, APT28 often utilizes consistent modules for credential harvesting. When ML models identify a 95% structural overlap in the "Credential Stealer" module between a 2024 campaign and a new 2026 sample, the attribution to APT28 becomes a high-confidence assessment.


#### 4.2 The Economic Burden of Malware Development

Attribution via code lineage is effective because it targets the attacker’s economy. To avoid this type of detection, an APT group would have to rewrite their entire codebase for every single operation.

Operational Friction: Rewriting code is time-consuming and introduces bugs. For a professional hacking group with "delivery deadlines," it is much more efficient to reuse 80% of an existing backdoor and only modify the remaining 20%.

The "Achilles' Heel": This 80% overlap is the "Achilles' heel." By maintaining a historical database of "Code DNA," CTI analysts can ensure that no matter how many times an attacker changes their IP address or their domain name, their identity remains tied to the code they have written.


---

### Conclusion: The Genetic Map of Global Threats

The transition from hash-based detection to ML-driven lineage mapping represents the final maturity of modern cybersecurity. We have moved from identifying "symptoms" to identifying "DNA."

By utilizing Function Call Graphs and Graph Neural Networks, we have turned the massive entropy of the malware ecosystem into a structured, searchable map. The code we write today is the infrastructure of tomorrow—and by mapping the lineage of our adversaries, we ensure that infrastructure remains resilient, sovereign, and secure.
