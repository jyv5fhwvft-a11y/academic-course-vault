# 🔬 LAB 12: Cache Performance — Calculating Effective Access Time (EAT) Deltas
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically simulate memory hardware latency layers. You will manually formulate Effective Access Time (EAT) equations across different architectural hit-rate variables to measure how spatial locality preserves execution speed.

### 🛑 2. Prerequisites
- Completion of Lab 11 bit-splitting and page translation tracking.
- Basic algebraic manipulation and familiarity with hardware latency time scales (nanoseconds).

### 🎪 3. The Pedagogical Hook: The High-Speed Checklist
In our previous lab, we discovered how fixed-size page tables completely solve external fragmentation. However, this flexibility introduces a severe architectural tax: every single memory load requires two separate trips to main RAM. This means without acceleration, your system runs at exactly half speed. To bypass this penalty, hardware designers built a high-speed checklist right into the CPU core—the Translation Lookaside Buffer (TLB). In this lab, you will calculate exactly how much time this microscopic piece of silicon saves across different workload behaviors.

---

### 🔍 4. System Core Breakdown
- **The Double-Trip Memory Penalty:** The baseline performance cost of unaccelerated paging, where the MMU must read a Page Table Entry in RAM before it can fetch the actual destination memory byte.
- **Effective Access Time (EAT):** The mathematical representation of a system's average memory access latency, factoring in the probability of cache hits versus the latency penalty of a cache miss.

---

### 🛠️ 5. Practical Lab Exercise: Deriving Latency Projections

Follow these precise sequential execution steps to solve your hardware performance matrix:

#### Step 1: Analyze the Architecture Performance Specification
Your engineering lab workstation features the following physical hardware latency properties:
- **Main RAM Access Latency (`t_RAM`):** `120ns`
- **MMU TLB Cache Check Overhead (`t_TLB`):** `5ns`

#### Step 2: Compute EAT for a Cache-Friendly Workload (95% Hit Rate)
An optimized array loop is processing sequential data matrix lines, maintaining high spatial locality to achieve a **95% TLB Hit Rate** (`0.95`).
1. Formulate the Hit path equation cost: `t_Hit = t_TLB + t_RAM = 5ns + 120ns = 125ns`
2. Formulate the Miss path equation cost: `t_Miss = t_TLB + (2 * t_RAM) = 5ns + 240ns = 245ns`
3. Calculate the complete Effective Access Time:
   `EAT = (0.95 * 125ns) + (0.05 * 245ns) = _______ns`

#### Step 3: Compute EAT for a Cache-Unfriendly Workload (30% Hit Rate)
A rogue background process is iterating through an un-optimized loop with high pointer jumps, completely breaking spatial locality and degrading the system down to a **30% TLB Hit Rate** (`0.30`).
1. Apply your baseline hit and miss latencies from Step 2 against the degraded probability variables.
2. Calculate the ballooned Effective Access Time:
   `EAT = (0.30 * 125ns) + (0.70 * 245ns) = _______ns`

---

### 🏷️ 6. Architectural Lexicon / Terms
- **TLB Hit:** A scenario where the physical MMU checks its embedded cache and instantly finds the requested virtual-to-physical address translation match.
- **Cache Thrashing:** An undesirable state where a process's memory access pattern continuously overrides cache entries, driving hit rates down and causing the system to stall on slow multi-step walks.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 12, paste your engineering calculations inside a clean file and submit it to your course folder:
1. Provide your completed final EAT nanosecond values calculated for both Step 2 (95% Hit Rate) and Step 3 (30% Hit Rate).
2. Calculate the exact unaccelerated baseline latency cost paid by this architecture if the TLB cache chip was completely turned off.
3. Based on our monitor sticky note analogies, explain in two short sentences why code that loops through items contiguously (like a sequence of array blocks) maintains a vastly superior hit rate compared to code that jumps randomly across distant memory slots.
