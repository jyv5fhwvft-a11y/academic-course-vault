# 🔬 LAB 0: Explored Infrastructure — The Operating System as a Referee
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will actively verify the operating system's role as a dynamic resource referee by inspecting process virtualization and resource allocation using real-time terminal auditing tools.

### 🛑 2. Prerequisites
- Access to a Unix-like environment terminal loop (Linux, macOS, or your local Pyto/terminal sandbox container environment).
- Basic familiarity with opening a console window pane and executing elementary keyboard commands.

### 🎪 3. The Pedagogical Hook: Visualizing the Invisible
When you look at your computer or iPad screen, it presents a carefully maintained illusion. Applications like your browser, code editor, and media player appear to run entirely in parallel with uninterrupted access to the machine. In reality, a single CPU core can only handle one instruction stream at a critical microsecond. The operating system kernel constantly pauses, schedules, and rotates these tasks to keep them from crashing into each other.

---

### 🔍 4. System Core Breakdown
- **Process Isolation:** The kernel maintains a strict protection boundary using hardware privilege rings so that user applications cannot directly access raw memory addresses belonging to the system core or other processes.
- **Time Multiplexing:** Sharing a physical hardware component sequentially over time. The OS kernel splits CPU execution time into rapid slices, constantly context-switching between different tasks.

---

### 🛠️ 5. Practical Lab Exercise: Live Process Auditing

Follow these precise steps inside your local terminal sandbox environment to inspect the resource ledger:

#### Step 1: Initialize the System Monitor
Open your system console terminal window pane and execute the following universal process management monitor command:
```bash
htop
```
*(If your terminal platform returns a command-not-found error, fall back to utilizing the standard base terminal utility by executing: `top`)*

#### Step 2: Analyze the Metric Counters
Look closely at the top horizontal summary matrix bars on your terminal dashboard display screen:
1. Locate the **Tasks** or **Processes** counter (e.g., `Tasks: 312 total, 2 running`).
2. Identify the number of physical hardware processing cores your device possesses (represented by individual numbered CPU tracking meters like `CPU0`, `CPU1`).

#### Step 3: Compute the Referee Ratio
Document your system's metrics and calculate the resource allocation ratio:
- Total Number of Active Processes: `_______`
- Total Number of Physical CPU Cores: `_______`
- **The Core Question:** If your machine has significantly more active applications than physical hardware cores, how are they all running smoothly without lagging or crashing?

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Context Switch:** The rapid low-level operation where the kernel stops execution of one process, saves its state registers, and loads the execution state of another process.
- **Time Slice:** The tiny quantum of time (typically measured in milliseconds) that the operating system scheduler allows a single program to run before pausing it for a competitor.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive credit for Lab 0, write your responses to the following items inside a text file and submit it to your professor:
1. Provide a screenshot of your live `htop` or `top` terminal monitoring window screen.
2. State your calculated referee ratio from Step 3.
3. In two clear sentences, explain how the operating system maintains the illusion of simultaneous execution based on what you observed during the lab exercise.
