# 🔬 LAB 4: The Bootstrap Audit — Parsing Kernel Boot Logs via dmesg
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will actively audit the chronological sequence of system initialization. You will parse the kernel's active ring buffer logs using real-time terminal auditing tools to trace where hardware controllers and driver subsystems map into the operational architecture during a cold boot cycle.

### 🛑 2. Prerequisites
- Access to a Unix-like environment terminal shell loop (Linux or macOS console).
- Familiarity with the foundational four stages of the system boot pipeline (UEFI ➔ Bootloader ➔ Kernel Init ➔ PID 1).

### 🎪 3. The Pedagogical Hook: Reading the System Biography
When your laptop or computer boots up, thousands of hardware initialization events occur in the span of a few seconds. The screen flashes, the desktop draws, and the system appears instantly ready. But underneath the hood, the kernel was frantically negotiating with the silicon—probing CPU threads, testing storage sectors, and mounting abstract tables. In this lab, we are opening the system's autobiography file. You will learn to read the exact timestamped records left behind by the kernel core referee as it brought the machine to life.

---

### 🔍 4. System Core Breakdown
- **The Kernel Ring Buffer:** A dedicated memory region where the operating system kernel logs hardware detection messages, driver initializations, and structural warning flags during and after the boot process.
- **dmesg Protocol:** The core system utility used to safely query, dump, and filter the contents of the kernel's internal ring buffer log stream.

---

### 🛠️ 5. Practical Lab Exercise: Analyzing the Cold Boot Sequence

Follow these precise sequential execution commands inside your console shell to audit your system's boot biography:

#### Step 1: Dump the Kernel Boot Logs
Open your terminal console window pane and dump the complete raw kernel initialization logging stream:
```bash
dmesg
```
*Analyze the output rows. Note that every single entry begins with an explicit fractional timestamp bracket (e.g., `[    0.000000]`), tracking the exact number of seconds elapsed since power was delivered to the CPU chip.*

#### Step 2: Audit CPU Core Initialization
Isolate the exact sub-seconds when the kernel discovered and brought your physical processor hardware threads online by filtering your active buffer:
```bash
dmesg | grep -i "smpboot"
```
*(If your specific hardware platform logs under a different naming convention, fall back to checking basic processor initializations by running: `dmesg | grep -i "CPU")`*

#### Step 3: Track Storage Interface Mounting
Locate the precise millisecond your primary storage block arrays (SATA/NVMe) were inspected and bound to filesystem drivers:
```bash
dmesg | grep -i -E "sd|nvme"
```

#### Step 4: Verify the Arrival of PID 1
Filter the log buffer stream to pinpoint the exact terminal handoff milestone where the kernel successfully launched the primordial user-space initialization system daemon:
```bash
dmesg | grep -i "init"
```

---

### 🏷️ 6. Architectural Lexicon / Terms
- **dmesg (Diagnostic Message):** The programmatic tool used in Unix-like operating systems to inspect kernel ring buffer diagnostic logs.
- **smpboot:** The internal kernel subsystem responsible for bootstrapping Symmetric Multiprocessing capabilities across multiple physical CPU cores sequentially during Stage 3.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 4, paste your technical data logs inside a clean file and submit it to your course folder:
1. Provide a text copy snippet showing the first 3 lines output from your live `dmesg` execution command query.
2. State the precise timestamp bracket recorded when your system's primary storage controller was initialized during Step 3.
3. Based on our multi-stage relay race analogies, explain in two short sentences why the intermediate bootloader (GRUB) drops out of memory completely once it passes execution authority to the core kernel binary.
