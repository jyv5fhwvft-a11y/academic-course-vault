# 🔬 LAB 13: Virtual Memory — Auditing FIFO and LRU Eviction Sequences
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will manually simulate the page replacement pipelines of an operating system kernel. You will trace a live page reference string through FIFO and LRU queues, track memory slot saturation, and calculate final Page Fault counts to evaluate eviction strategy efficiency.

### 🛑 2. Prerequisites
- Completion of Lab 11 and Lab 12 memory translation math layouts.
- Basic procedural tracking abilities and understanding of queue data behaviors (First-In, First-Out).

### 🎪 3. The Pedagogical Hook: Managing the Desk Space
In our previous labs, we learned how fixed-size page tables and high-speed TLB chip caches accelerate virtual addressing. However, physical RAM chips have a hard capacity limit. What happens when your running applications demand vastly more memory frames than your hardware motherboard physically contains? The kernel transforms your secondary storage (SSD/Hard Drive) into an overflow reservoir known as Swap Space. In this lab, you will act as the kernel's memory manager, deciding exactly which data blocks to keep on the fast workspace desk and which ones to evict to the deep storage stacks.

---

### 🔍 4. System Core Breakdown
- **Page Fault Frequency:** The rate at which execution threads encounter missing memory page flags, forcing high-latency trips to fetch blocks from storage sectors.
- **LRU Policy:** The temporal eviction heuristic based on the principle of locality, dictating that the page frame that has gone unreferenced for the longest continuous duration should be discarded first.

---

### 🛠️ 5. Practical Lab Exercise: Tracing Eviction Pipelines

Follow these precise structural steps to solve your page replacement optimization matrix:

#### Step 1: Analyze the Environment Constraints
You are auditing a memory management subsystem with the following parameters:
- **Available Physical Frames Pool:** `3` (Initially completely empty)
- **Arriving Page Reference Trace String:** `7, 0, 1, 2, 0, 3, 0, 4`

#### Step 2: Trace the First-In, First-Out (FIFO) Pipeline
1. Track the sequential allocation steps inside your frame grid pool:
   - Access `7` ➔ Load Frame: `[7,  ,  ]` (Fault 1)
   - Access `0` ➔ Load Frame: `[7, 0,  ]` (Fault 2)
   - Access `1` ➔ Load Frame: `[7, 0, 1]` (Fault 3 - Saturation reached)
   - Access `2` ➔ Evict oldest page (`7`) ➔ Frames become: `[2, 0, 1]` (Fault 4)
   - Access `0` ➔ Already present in memory! ➔ Frames stay: `[2, 0, 1]` (Cache Hit)
   - Access `3` ➔ Evict next oldest (`0`) ➔ Frames become: `[2, 3, 1]` (Fault 5)
   - Access `0` ➔ Evict next oldest (`1`) ➔ Frames become: `[2, 3, 0]` (Fault 6)
   - Access `4` ➔ Evict next oldest (`2`) ➔ Frames become: `[4, 3, 0]` (Fault 7)
2. Log the total First-In, First-Out performance penalty:
   `Total FIFO Page Faults = _______`

#### Step 3: Trace the Least Recently Used (LRU) Pipeline
1. Reset your physical frame pool and trace the same string using temporal access memory cues:
   - Access `7, 0, 1` ➔ Cold load frames identically: `[7, 0, 1]` (3 Faults)
   - Access `2` ➔ Evict the least recently used page (`7`) ➔ Frames become: `[2, 0, 1]` (Fault 4)
   - Access `0` ➔ Cache Hit! *Crucial: Page `0` is now marked as the most recently updated.*
   - Access `3` ➔ Evict the least recently used page (`1`, since `0` and `2` were touched more recently) ➔ Frames become: `[2, 0, 3]` (Fault 5)
   - Access `0` ➔ Cache Hit! *Page `0` is bumped to the most recently used spot again.*
   - Access `4` ➔ Evict the least recently used page (`2`, since `0` and `3` were touched more recently) ➔ Frames become: `[4, 0, 3]` (Fault 6)
2. Log the total Least Recently Used performance penalty:
   `Total LRU Page Faults = _______`

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Belady's Anomaly:** An unusual algorithmic phenomenon where allocating *more* physical memory frames to a process causes its total page fault count to paradoxically *increase* (occurs under certain policies like FIFO, but mathematically impossible under LRU).
- **SIGSEGV:** A segmentation violation signal fired down to an app thread when it queries memory boundaries beyond its base layout clearance lines.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 13, paste your data answers inside a clean file and submit it to your course folder:
1. Provide your completed final Page Fault totals calculated for both Step 2 (FIFO) and Step 3 (LRU).
2. Identify which algorithm performed more efficiently on this specific trace string by maintaining a lower overall fault count.
3. Based on our library desk analogies, explain in two short sentences why a system that enters a state of continuous **Thrashing** grinds visible program performance down to zero.
