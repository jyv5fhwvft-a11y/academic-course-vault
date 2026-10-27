# 🔬 LAB 8: Advanced Scheduling — Auditing MLFQ Penalties and Priority Inversion Traps
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically construct priority scheduling matrices, evaluate dynamic multi-level feedback queue downgrades, and trace the step-by-step runtime synchronization chain that triggers a catastrophic Priority Inversion deadlock.

### 🛑 2. Prerequisites
- Completion of Lab 7 scheduling metrics.
- Comprehensive structural understanding of process states (Ready vs. Blocked) and mutual exclusion locks.

### 🎪 3. The Pedagogical Hook: Paralyzing Mars
In July 1997, the Mars Pathfinder rover suddenly began experiencing total system resets on the Martian surface. A high-priority information management process was getting starved out completely by a low-priority meteorological task and an intermediate communications daemon, causing a real-time watchdog timer to trigger a hard reset. This wasn't a hardware failure; it was a pure scheduling logic flaw known as Priority Inversion. In this lab, you will diagram this exact scenario to inspect how simple locking dependencies can bring a multi-million dollar spacecraft to a screeching halt.

---

### 🔍 4. System Core Breakdown
- **MLFQ Feedback Loops:** A Multi-Level Feedback Queue penalizes CPU-bound batch tasks by dynamically lowering their priority if they exhaust continuous time slices, preserving high-priority queues for snappy, user-facing interactive I/O tasks.
- **Priority Inheritance:** The definitive solution to inversion anomalies, forcing a low-priority thread holding a resource to temporarily take on the priority rating of a blocked high-priority thread until it clears the critical section.

---

### 🛠️ 5. Practical Lab Exercise: Tracing the Pathfinder Priority Inversion

Follow these precise structural steps to map out the execution chronology of the Mars Pathfinder anomaly:

#### Step 1: Establish the Threads and Resources
Imagine three process threads sitting on a single core CPU timeline grid:
- **T_H (High Priority):** Critical information tracking bus routine.
- **T_M (Medium Priority):** Continuous background communications hub daemon.
- **T_L (Low Priority):** Weather data collection task.
- **Shared Resource:** A shared hardware memory buffer protected by a mutual exclusion lock (`Mutex_X`).

#### Step 2: Sequence the Timeline Breakdown
Analyze the absolute chronological sequence of execution steps:
1. **Time = 0ms:** Only the low-priority task `T_L` is ready. It slides onto the CPU core, enters a critical section, and claims `Mutex_X`.
2. **Time = 5ms:** The high-priority task `T_H` wakes up. It preempts `T_L` instantly because of its superior priority status bit.
3. **Time = 10ms:** `T_H` attempts to read the shared buffer and requests `Mutex_X`. Because `T_L` holds the lock, the hardware blocks `T_H`, moving it from the RUNNING state to the BLOCKED state. Control drops back down to `T_L`.
4. **Time = 15ms:** The medium-priority task `T_M` wakes up. It does not need `Mutex_X`. Because its priority is higher than `T_L`, the scheduler preempts `T_L` and drops `T_M` onto the CPU core.
5. **Time = 20ms:** `T_M` settles into a long, heavy data transmission loop.

#### Step 3: Identify the Inversion Paralyzation
*Analyze your state grid.* Because `T_M` is running continuously, the low task `T_L` can never resume execution to finish its critical section and release `Mutex_X`. Because `Mutex_X` remains locked, the high task `T_H` is trapped waiting forever. 

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Priority Inversion:** An operational loop anomaly where an intermediate-priority task runs continuously, indirectly blocking a high-priority task by starving the low-priority thread holding a critical resource lock.
- **Watchdog Timer:** A hardware level countdown timer thread that force-reboots an embedded operating system if a critical master system process fails to clear its tracking register within a set duration.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 8, paste your analysis parameters inside a clean file and submit it to your course folder:
1. Identify the exact process thread (`T_H`, `T_M`, or `T_L`) whose continuous execution actively blocks `T_L` from releasing its lock in Step 3.
2. Under the **Priority Inheritance** fix protocol, explain what specific priority rating transformation occurs to `T_L` the exact millisecond `T_H` blocks on `Mutex_X` at Time = 10ms.
3. Based on our hospital emergency room triage analogies, explain in two short sentences why a pure priority scheduling scheme can never be used inside an open-ended cloud virtual server environment without an "Aging" mechanism.
