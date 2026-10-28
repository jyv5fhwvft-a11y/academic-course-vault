# 🔬 LAB 25: Cryptographic Pipelines — Modeling Hybrid Asymmetric-Symmetric Networks
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically map a Hybrid Encryption pipeline network. You will trace the architectural handoffs between asymmetric public-key handshakes and high-speed symmetric data streams, and calculate the mathematical scaling limits of secure key distributions.

### 🛑 2. Prerequisites
- Completion of Lab 24 stack frame overflow tracking and runtime canary mitigations.
- Basic familiarity with network handshake steps and modular math abstractions.

### 🎪 3. The Pedagogical Hook: Speeding Up the Cipher Crypt
When you load a secure website or stream encrypted data file blocks across a network link, the operating system must encrypt every single outgoing byte on the fly. If the kernel used pure Asymmetric (RSA) algorithms to encrypt this bulk stream, the heavy mathematical loops would consume 100% of your CPU cycles, slowing your connection to a absolute crawl. To solve this, production kernels use a clever bait-and-switch trick called Hybrid Encryption. In this lab, you will act as a systems architect, using slow asymmetric slots to securely trade a secret token, then instantly switching to fast symmetric ciphers to unleash high-speed throughput.

---

### 🔍 4. System Core Breakdown
- **Key Distribution Scalability Barriers:** The geometric bottleneck where a pure symmetric network requires managing $N(N-1)/2$ unique key pairings, rendering pre-shared secure distributions logistically impossible at global scale.
- **The Hybrid Handoff Phase:** The optimization sequence where asymmetric key pairs execute the initial insecure handshake to establish a transient token, yielding execution scope to symmetric block bit-shifting.

---

### 🛠️ 5. Practical Lab Exercise: Solving the Hybrid Cryptographic Matrix

Follow these precise sequential profiling steps to map and calculate system encryption paths:

#### Step 1: Calculate Symmetric Key Scalability Limits
Imagine an engineering network containing $N = 100$ independent computing nodes. The nodes must communicate with each other in isolated pairs using pure symmetric encryption, meaning every possible pair must share a completely unique, distinct private secret key.
1. Use the definitive pairing combination formula $\text{Keys} = \frac{N \times (N - 1)}{2}$ to calculate the total number of secret keys that must be securely generated and distributed across the cluster:
   - $\text{Keys} = \frac{100 \times (99)}{2} = $ ______________ **Unique Symmetric Keys**.
2. If this network scales out to a global system layer of $N = 1,000,000$ active nodes, explain why distributing and keeping these symmetric keys secret in advance is logistically impossible without asymmetric primitives.
   - *Your Evaluation:* __________________

#### Step 2: Sequence the Hybrid HTTPS/TLS Handshake Timeline
A client node hooks into a remote target server node over an unsecure public network. Arrange the following execution lifecycle milestones in their correct chronological sequence (**1, 2, 3, or 4**) to trace the hybrid handoff:
- [ ] **Milestone Step:** The channel drops heavy asymmetric processing loops. All subsequent application payload content bytes stream inside high-speed AES symmetric ciphers.
- [ ] **Milestone Step:** The client initiates a secure connection loop, and the remote server presents its public RSA asymmetric key card.
- [ ] **Milestone Step:** The server uses its isolated, matching private asymmetric key to decode the client's payload, safely unlocking the shared token.
- [ ] **Milestone Step:** The client generates a random symmetric session key, encrypts it using the server's public key, and flashes the locked payload back across the link.

#### Step 3: Map Key/Slot Architecture Constraints
1. Based on our mailbox slot analogies, identify which specific key primitive (**Public Key** or **Private Key**) corresponds directly to the open street-side slot where any arbitrary passerby can drop a message inside.
   - *Your Identification:* __________________
2. State the structural reason why a symmetric cipher (like AES) can process large data blocks significantly faster than an asymmetric primitive (like RSA).
   - *Your Answer:* __________________

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Asymmetric Encryption (RSA):** A dual-key cryptographic layout where data scrambled by a public key can strictly be decoded by a matching private key.
- **Hybrid Encryption:** An optimized system design model that utilizes asymmetric math to protect key exchange handshakes, then transfers execution over to symmetric ciphers for fast bulk streaming.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 25, paste your text analysis parameters inside a clean file and submit it to your course folder:
1. Provide your completed symmetric key calculation totals and distribution limitations from Step 1.
2. Provide your sequenced chronological numbers (**1 through 4**) for the hybrid handshake transitions inside Step 2.
3. Provide your key identification and structural processing reason derived in Step 3.
4. Based on our shared house key analogies, explain in two short sentences why a single leaked symmetric session key threatens data privacy significantly more than a leaked asymmetric public key.
