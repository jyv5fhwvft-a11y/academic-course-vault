# 🔬 LAB 23: Identity Verification — Cryptographic Hashing and Biometric Security Analysis
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically simulate an operating system authentication pipeline. You will trace the mathematical transformation of user passwords via salted hashing, evaluate security trade-offs between knowledge-based and inherence-based models, and identify architectural vulnerabilities within identity subsystems.

### 🛑 2. Prerequisites
- Completion of Lab 22 access control list and capability token protection matrices.
- Basic understanding of one-way mathematical encryption transforms and string manipulation.

### 🎪 3. The Pedagogical Hook: The Permanence of Anatomy
Before an operating system can check an access matrix to grant file clearance, it must answer a critical question: *Who are you?* Traditional systems verify identity via a secret passphrase ("something you know"). If a hacker breaches the password database, you can simply change your password to restore security. Modern biometric systems verify identity via a fingerprint or facial map ("something you are"). But what happens if a hacker steals your raw biometric data map? You cannot change your fingerprints. In this lab, you will audit the cryptographic walls built to defend your identity against permanent exposure.

---

### 🔍 4. System Core Breakdown
- **Cryptographic Salted Hashing:** The defensive data practice of appending a randomized unique string to a password input before processing it through an indivisible, one-way hash algorithm, shielding stored assets from rainbow table lookups.
- **Biometric Inherence Vulnerability:** The absolute system risk factor stems from the unalterable nature of biological data; once a biometric template map is leaked, that specific verification channel is permanently compromised.

---

### 🛠️ 5. Practical Lab Exercise: Simulating the Identity Pipeline

Follow these precise sequential execution evaluation steps to solve your identity protection profiles:

#### Step 1: Audit an Unprotected Password Database
Imagine a compromised corporate storage system that saves user passwords directly into an un-salted SHA-256 database. Two separate users (User_A and User_B) accidentally select the identical weak password: `Password123`.
1. Calculate the exact structural vulnerability that manifests when both profiles undergo an identical one-way SHA-256 conversion: Will their database hash string entries be **[Identical] OR [Unique]**?
   - *Your Answer:* __________________
2. Explain how a hacker uses a pre-computed dictionary lookup table (Rainbow Table) to expose both users' cleartext values instantly after breaching this database table layer.
   - *Your Answer:* __________________

#### Step 2: Implement Cryptographic Salted Hashing
To secure the database, you refactor the login subsystem to inject a randomized `Salt` string value to every new account profile initialization step.
- **User_A Salt String Value:** `k8x@9!`
- **User_B Salt String Value:** `p2#m1$`
1. Formulate the raw text payloads that are passed into the SHA-256 calculation loop for both accounts if both users type the identical passphrase `Password123`:
   - **User_A Appended Hashing Payload:** `Password123 + ____________`
   - **User_B Appended Hashing Payload:** `Password123 + ____________`
2. Determine whether the resulting database hash output values are now **[Identical] OR [Unique]**, and explain how this completely neutralizes standard pre-computed rainbow table attack vectors.
   - *Your Answer:* __________________

#### Step 3: Map Biometric Sensor Isolation Architectures
An engineer is auditing a mobile hardware terminal that deploys fingerprint verification. 
1. Describe the precise role of an embedded **Trusted Platform Module (TPM)** chip or secure enclave in preventing raw biological fingerprint imagery from ever leaking onto primary disk storage blocks or reaching standard unprivileged application code lines (Ring 3 page frames).
   - *Your Answer:* __________________

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Multi-Factor Authentication (MFA):** A defensive configuration topology requiring an identity thread to validate two or more distinct verification domains (Knowledge, Possession, Inherence) before gaining access.
- **Inherence Factor:** An unalterable biological or physical profile attribute unique to a specific individual, used as an identity validation metric.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 23, paste your text data parameters inside a clean file and submit it to your course folder:
1. Provide your unprotected database hashing outcomes and lookup vulnerabilities derived for Step 1.
2. Provide your salted payload formulations and output determinations calculated inside Step 2.
3. Based on our fingerprint and safe key models, explain in two short sentences the catastrophic long-term system consequence that unfolds if a user's biometric signature vector database is successfully breached and leaked to the open web.
