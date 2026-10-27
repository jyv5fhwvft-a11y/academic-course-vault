# 🔬 LAB 2: The Trap Door — Inducing Privilege Boundary Exceptions
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will write a low-level C application to deliberately cause a privilege boundary violation. You will trace how the physical hardware catches unauthorized memory access and traps execution control down to the kernel mode referee.

### 🛑 2. Prerequisites
- Access to a Linux terminal shell loop environment with the GCC compiler installed (`gcc`).
- Clear understanding of the conceptual difference between user mode (Ring 3) and kernel mode (Ring 0).

### 🎪 3. The Pedagogical Hook: Testing the Walls
An operating system's isolation boundary is only as good as the underlying physical silicon hardware chips enforcing it. As a developer, when you see a program crash with a short "Segmentation Fault" message, you are witnessing an emergency hardware intervention. The CPU processor caught your application attempting to step out of its sandbox, immediately locked down the memory pipeline, and safely terminated the thread before it could corrupt companion tasks running on the hardware grid.

---

### 🔍 4. System Core Breakdown
- **General Protection Fault (GPF):** An electronic interrupt trap fired natively by the CPU hardware when an executing instruction breaks system protection rules (such as dereferencing a null pointer or trying to execute restricted assembly commands outside Ring 0).
- **Signal Tracking:** When the hardware traps execution down to supervisor mode, the kernel wraps the violation state inside a software signal descriptor (such as `SIGSEGV`) and dispatches it to the faulting process.

---

### 🛠️ 5. Practical Lab Exercise: Forcing a Segmentation Trap

Follow these precise sequential execution commands inside your console shell to build and trace an isolation boundary violation:

#### Step 1: Code the Boundary Defier
Open an inline terminal text editor window and create a new C source file named exactly `trap_test.c`:
```bash
nano trap_test.c
```
*Paste this complete, deliberately unstable code block inside the editor file area canvas:*
```c
#include <stdio.h>

int main() {
    printf("🧬 Initializing User Mode (Ring 3) Sandbox Application...\n");
    
    // Create an unmapped, illegal pointer targeting the base address address
    int *illegal_pointer = NULL;
    
    printf("🛑 Attempting unauthorized memory write to protected territory...\n");
    // This illegal dereference forces an immediate hardware isolation trap!
    *illegal_pointer = 0xDEADBEEF; 
    
    printf("🟢 Critical System Alert: Isolation Broken! (This line should never execute)\n");
    return 0;
}
```
*Save the document and exit the editor panel wrapper.*

#### Step 2: Compile the Binary
Invoke the system compiler toolchain to process your source file down into a runnable binary program object file:
```bash
gcc trap_test.c -o trap_test
```

#### Step 3: Trigger the Referee
Execute the compiled binary application right inside your console line loop interface:
```bash
./trap_test
```
*Document the exact termination error message printed onto your terminal display panel.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Segmentation Fault (SIGSEGV):** The signal state thrown by an operating system when an application thread references an unallocated or restricted virtual memory address zone.
- **Null Pointer Dereference:** An operation that attempts to read or write data using a pointer address set to zero, which maps directly into protected system memory spaces.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 2, paste your technical data logs inside a clean file and submit it to your course workspace folder:
1. Provide a text copy snippet showing the exact terminal console output printed when running `./trap_test`.
2. Name the specific signal type code (e.g., `SIGSEGV`) assigned to a memory space access boundary violation.
3. Based on our secured corporate campus layouts, explain in two short sentences why a user-space application is completely blocked from directly writing to page memory configuration registers.
