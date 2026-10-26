# 🔬 LAB 1: The Privilege Boundary — Auditing Loadable Kernel Modules (LKMs)
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will actively audit how a monolithic core dynamically extends its Ring 0 privilege space at runtime. You will inspect live system modules, track kernel symbol listings, and map driver footprints across supervisor memory.

### 🛑 2. Prerequisites
- Access to a Linux terminal shell loop (such as your local Ubuntu environment, a cloud sandbox instance, or a local administrative container).
- Broad understanding of the privilege boundary running between user mode (Ring 3) and supervisor mode (Ring 0).

### 🎪 3. The Pedagogical Hook: Operating in the Void
Every line of code you write in a typical class executes safely trapped inside user space. If your code undergoes a null pointer dereference, it terminates alone. However, code that links itself directly into a Monolithic Kernel shares raw hardware clearances with the CPU. A single unhandled stack overflow inside a kernel driver module doesn't just crash an app—it triggers a total, catastrophic hardware panic state.

---

### 🔍 4. System Core Breakdown
- **Dynamic Linking:** Loadable Kernel Modules (LKMs) let an operating system load object code files (`.ko` extensions) into active kernel memory on-the-fly, avoiding the need to completely recompile or reboot a production mainframe.
- **Ring 0 Privileges:** Modules execute with maximum system access, possessing uninhibited clearance to read and write directly to core memory control tables.

---

### 🛠️ 5. Practical Lab Exercise: Live Module Auditing

Follow these precise sequential execution commands inside your console shell to inspect active kernel modules:

#### Step 1: List Active Modules
Query the running kernel state to reveal all active loadable driver layers currently resident in Ring 0 space:
```bash
lsmod
```
*Analyze the output layout arrays on your display screen. Note how every column maps the module name, total memory footprints in bytes, and which dependent subsystems are utilizing it.*

#### Step 2: Track Specific Hardware Drivers
Isolate a target network subsystem driver module (such as the universal loopback interface or standard packet controllers) by filtering your active stream buffer:
```bash
lsmod | grep net
```

#### Step 3: Inspect Low-Level Module Metadata
Query the kernel image repository details to pull structural metadata from a specific object file module (e.g., tracking the `ext4` filesystem layer module):
```bash
modinfo ext4
```
*Document the exact module file paths, license agreements, dependencies, and internal compiler parameters printed onto your console.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **lsmod:** The Linux command protocol that safely parses the `/proc/modules` virtual file tree stream to print all currently loaded kernel object drivers.
- **Kernel Panic:** A safety mechanism triggered by the operating system kernel when it encounters an unrecoverable system exception that breaks core protection rules.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 1, paste your data answers inside a clean document file and submit it to your course folder:
1. Provide a text copy snippet showing the first 5 rows output from your live `lsmod` execution command query.
2. State the total memory size (in bytes) consumed by your system's active network layout module discovered during Step 2.
3. Based on our corporate office virus analogies, explain in two short sentences why adding an unverified third-party graphics driver module into a Monolithic Kernel space presents a severe operational safety risk.
