# 🔬 LAB 26: Perimeter and Internal Telemetry Security — Auditing Firewalls and IDS Networks
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analyze a raw network traffic log trace. You will separate perimeter border filtering milestones from internal deep packet inspection tasks, and design custom rules to classify threats across firewall and Intrusion Detection System (IDS) monitoring lanes.

### 🛑 2. Prerequisites
- Completion of Lab 25 hybrid encryption handshakes and asymmetric-symmetric key distribution scalability models.
- Thorough procedural understanding of IP address configurations, port numbers, sockets, and network driver packet ring buffers.

### 🎪 3. The Pedagogical Hook: The Blind Spot at the Gate
Imagine configuring a massive, ironclad gate at the entrance of a high-security server vault. You hand the gate guard a strict checklist: *Only allow inbound traffic from local corporate office IPs targeting communication port 22.* A clever adversary steals valid employee credentials, establishes a connection from a corporate laptop, and breezes right past your guard. Once inside, they spin up an un-monitored automated execution tool and start vacuuming up gigabytes of core database secrets. To your perimeter gatekeeper, everything looks completely legal. In this lab, you will discover why perimeter walls are not enough, and how internal telemetry guards spot hidden threats.

---

### 🔍 4. System Core Breakdown
- **Boundary Header Filtering (Firewalls):** Enforcing policy rules at the network border layer by dropping packet frames instantly based on simple, high-speed static header values (IPs, Ports).
- **Internal Heuristic Monitored Layers (IDS):** Buffering packet streams already flowing inside system networks to evaluate transactional behaviors against statistical normality baselines or known threat signature libraries.

---

### 🛠️ 5. Practical Lab Exercise: Parsing the Traffic Log Trace

Follow these precise structural evaluation steps to isolate and classify your network security logs:

#### Step 1: Analyze the Raw Incident Log Data Stream
Your organization's network core captured the following chronological network event logs:
- **Line [01]:** Inbound connection request from known blocklisted botnet IP `198.51.100.42` targeting closed Port `23` (Telnet).
- **Line [02]:** Inbound connection request from authorized offsite branch IP `203.0.113.12` targeting opened Port `22` (SSH).
- **Line [03]:** Session successfully established for IP `203.0.113.12` using verified administrator cryptographic key tags.
- **Line [04]:** Connection stream from IP `203.0.113.12` begins executing an automated `sql_dump` script at 3:15 AM, pulling 450 GB of data blocks out to a scratch directory loop.

#### Step 2: Route Logs to the Correct Defensive Layer
Deconstruct the incident log entries from Step 1 and match them to the correct system defensive gatekeeper tool: **[Edge Firewall Port Filter]** OR **[Internal Telemetry IDS Engine]**:
1. Identify which security layer intercepts and drops the hostile botnet probe flagged in **Line [01]**:
   - *Your Defensive Tool Selection:* __________________
2. Identify which security layer approves the inbound connection and checks the port access request in **Line [02]**:
   - *Your Defensive Tool Selection:* __________________
3. Identify which specific security layer must intervene to trigger an alarm and block the massive, off-hours database dump flagged in **Line [04]**:
   - *Your Defensive Tool Selection:* __________________

#### Step 3: Classify the Internal Telemetry Strategy
1. To flag the 3:15 AM database dump, the monitor checks historical traffic patterns to determine that standard administrator actions rarely exceed 50 MB of data lookups during off-hours. Identify whether this tracking logic represents **[Signature-Based Detection] OR [Anomaly-Based Detection]**.
   - *Your Identification:* __________________
2. If an attacker crafts a packet containing a known, hardcoded malicious text string exploit sequence (e.g., a buffer overflow payload), identify which detection strategy spots the threat instantly by matching the exact byte string patterns.
   - *Your Identification:* __________________

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Deep Packet Inspection (DPI):** An advanced network packet filtering method that examines the data payload contents of a packet frame as it passes an inspection node, rather than just reading header values.
- **Interrupt Vector Table (IVT):** The low-level hardware mapping table used by the kernel to dynamically catch peripheral device driver interrupt chimes before network frames reach user-space memory blocks.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 26, paste your text data parameters inside a clean file and submit it to your course folder:
1. Provide your completed defensive tool routing selections matching Lines, [02], and [04] from Step 2.
2. Provide your internal telemetry logic identifications derived for Step 3.
3. Based on our club bouncer and undercover security camera analogies, explain in two short sentences why deploying a pure edge firewall leaves a distributed network completely vulnerable to insider threats or stolen credential exploits.
