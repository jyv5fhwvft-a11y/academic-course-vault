# 🔬 LAB 10: Memory Virtualization — Auditing Base-and-Bound Address Translation
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically simulate an early hardware Memory Management Unit (MMU). You will evaluate logical execution memory trace records, map valid virtual pointers to physical RAM chips, and calculate precise segmentation protection exception thresholds.

### 🛑 2. Prerequisites
- Completion of Module 2 process lifecycle parameters.
- Comprehensive structural understanding of CPU privilege states (Ring 3 vs. Ring 0) and low-level address registers.

### 🎪 3. The Pedagogical Hook: Trapped in the Matrix
When you write code that reads a pointer address or iterates through an array in memory, your compiled binary is living an illusion. Every process is completely convinced that it owns a massive, uninterrupted block of physical memory starting at address zero. Underneath the hood, the CPU chip is playing a high-speed trick. It intercepts every instruction wire, shifts values mathematically, and checks boundaries before touching physical hardware lanes. In this lab, you will step inside the silicon MMU to manually calculate these dynamic transformations.

---

### 🔍 4. System Core Breakdown
- **Dynamic Relocation:** The execution strategy where a process's abstract memory space is relocated contiguously into an offset slot in RAM. The real hardware location is concealed via a hardware `Base Register`.
- **Bounds Protection:** An uncompromising hardware isolation wall. The CPU checks every logical address reference against a `Bound Register` size limit; if the instruction tries to jump beyond this ceiling, the silicon breaks execution loops instantly to safeguard neighboring tenants.

---

### 🛠️ 5. Practical Lab Exercise: Simulating the Hardware MMU

Follow these precise structural steps to analyze and translate virtual process address space traces:

#### Step 1: Analyze the Active Register Configuration Matrix
The kernel has context-switched a user application onto CPU Core 0. It locks down the MMU hardware register pins with these specific parameters:
- **Base Register:** `0x00003A60` (Decimal: `14944`)
- **Bound Register:** `0x000005D8` (Decimal: `1500` Bytes)

#### Step 2: Translate Valid User Instructions
Compute the exact physical RAM location for these logical runtime memory reference pointers:
1. **Trace Request 1:** Application code reads data from Logical Address `320`.
   - *Check Bounds:* Is `320` < `1500`? Yes (Passes verification).
   - *Calculate Offset:* `Physical Address = 320 + 14944 = _______`
2. **Trace Request 2:** Application code fetches an instruction from Logical Address `1024`.
   - *Check Bounds:* Is `1024` < `1500`? Yes (Passes verification).
   - *Calculate Offset:* `Physical Address = 1024 + 14944 = _______`

#### Step 3: Audit Boundary Violation Exceptions
Analyze the architectural outcome for the following execution event trace record:
1. **Trace Request 3:** A rogue array loop inside the application attempts a write command to Logical Address `1650`.
   - *Check Bounds:* Is `1650` < `1500`? **NO! (CEILING VIOLATION DETECTED)**
   - *Identify Outcome:* The physical CPU chip drops the instruction instantly. It fires an electronic hardware interrupt trap that switches state bits to Ring 0, hands execution to the kernel referee, and force-terminates the app.

---

### 🏷️ 6. Architectural Lexicon / Terms
- **MMU (Memory Management Unit):** The physical hardware tracking processor chipset responsible for mapping virtual logical coordinates to physical RAM locations in real-time.
- **Segmentation Fault (SIGSEGV):** The low-level signal thrown by the operating system kernel when the hardware catches a process trying to access memory outside its allocated Base and Bound domain fence.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 10, paste your technical calculations inside a clean file and submit it to your course folder:
1. Provide your completed physical translation values derived for Request 1 and Request 2 inside Step 2.
2. Identify the specific name of the hardware trap exception code thrown by the CPU chip when auditing Request 3 inside Step 3.
3. Based on our hotel room numbering illusions, explain in two short sentences why contiguous variable-sized allocation systems (like Base-and-Bound blocks) lead to severe external fragmentation across the physical RAM substrate.
