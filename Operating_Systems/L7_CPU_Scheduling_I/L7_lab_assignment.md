# 🔬 LAB 7: Scheduling Foundations — Simulating Gantt Chart Performance Metrics
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will manually derive scheduling Gantt charts and compute core performance metrics—including wait times, turnaround times, and overall optimization deltas—under FCFS and SJF execution parameters.

### 🛑 2. Prerequisites
- Access to a basic calculation tool or local scripting environment.
- Thorough conceptual understanding of process burst vectors, preemption limits, and the Convoy Effect.

### 🎪 3. The Pedagogical Hook: The Checkout Line Congestion
Every time you launch a heavy computational task alongside lightweight web loops, the kernel scheduler must play the role of an absolute traffic referee. If it relies blindly on non-preemptive insertion orders, your simple user interface click hangs indefinitely while a heavy numeric compilation saturates the ALU pipeline wires. In this lab, you will manually simulate these scheduling policies to observe how a simple shift in algorithmic strategy reduces system-wide latency metrics.

---

### 🔍 4. System Core Breakdown
- **Turnaround Time (TAT):** The total elapsed time duration from the exact millisecond a process joins the READY queue to the millisecond it transitions cleanly into the TERMINATED state.
- **Wait Time (WT):** The cumulative duration a process spends sitting inside the READY queue matrix waiting to be slid onto an active processing core layout.

---

### 🛠️ 5. Practical Lab Exercise: Deriving Average Waiting Vectors

Follow these precise structural steps to solve your scheduling optimization matrix:

#### Step 1: Analyze the Process Task Array
You are given a workload vector containing four processes arriving simultaneously at time 0 with the following expected CPU burst cycle weights:
- **P1:** 18ms
- **P2:** 4ms
- **P3:** 2ms
- **P4:** 6ms

#### Step 2: Plot the FCFS Scheduling Matrix
1. Draw an insertion-ordered Gantt chart scheduling the processes in sequence: P1 ➔ P2 ➔ P3 ➔ P4.
2. Determine individual process waiting metrics:
   - P1 waiting time = `0ms`
   - P2 waiting time = `18ms`
   - P3 waiting time = `18 + 4 = 22ms`
   - P4 waiting time = `22 + 2 = 24ms`
3. Compute the structural First-Come-First-Served arithmetic mean waiting vector:
   `Average Wait Time = (0 + 18 + 22 + 24) / 4 = _______ms`

#### Step 3: Plot the SJF Prioritization Matrix
1. Rearrange your task array chronology based on the brevity of process burst values to establish the Shortest-Job-First sequence: P3 ➔ P2 ➔ P4 ➔ P1.
2. Determine individual process waiting metrics under this optimized sorting layout:
   - P3 waiting time = `0ms`
   - P2 waiting time = `2ms`
   - P4 waiting time = `2 + 4 = 6ms`
   - P1 waiting time = `6 + 6 = 12ms`
3. Compute the optimized Shortest-Job-First arithmetic mean waiting vector:
   `Average Wait Time = (0 + 2 + 6 + 12) / 4 = _______ms`

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Gantt Chart:** A visual horizontal bar chart mapping the timeline execution layout of processes occupying a CPU core.
- **Starvation:** An operational failure mode where a heavy, long process is blocked from executing indefinitely because smaller, rapid tasks constantly claim resource priority.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 7, paste your technical calculations inside a clean file and submit it to your course folder:
1. Provide your completed Average Wait Time calculation values for both Step 2 (FCFS) and Step 3 (SJF).
2. Calculate the exact optimization delta (the percentage improvement in waiting brevity) achieved by switching the process array sequence to SJF.
3. Based on our grocery store cashier analogies, explain in two short sentences why a preemptive Round Robin scheme is fairer to a mixed pool of heavy and light tasks than a non-preemptive FCFS queue.
