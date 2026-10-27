# 🔬 LAB 3: The Gatekeeper Loop — Invoking Raw Assembly Syscalls
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will bypass standard high-level C system library wrappers (`printf`, `write`) to construct a raw, low-level inline assembly instruction sequence. You will trace how parameter state structures are loaded directly into hardware registers to trip the electronic boundary gateway.

### 🛑 2. Prerequisites
- Access to an engineering terminal console loop with the GCC toolchain installed (`gcc`).
- Familiarity with basic assembly concepts and CPU machine register assignments (`rax`, `rdi`, `rsi`, `rdx`).

### 🎪 3. The Pedagogical Hook: Shaking Hands with the Silicon
When you invoke a standard high-level command like `printf("Hello World");`, you are operating on top of multiple plush software pillows. Your code calls `glibc`, which processes formatting streams before running safety checks. In this lab, we are ripping those pillows away. We will load numeric values directly into the physical copper register lanes of your CPU chip and fire a raw `syscall` trap instruction. You will witness your software shaking hands directly with the core hardware gatekeeper.

---

### 🔍 4. System Core Breakdown
- **Register Dispatching:** The x86_64 Linux system architecture mandates an explicit register mapping protocol: the operational service identifier goes into `rax`, the target file descriptor drops into `rdi`, and the data array memory reference pointer aligns inside `rsi`.
- **The Electronic Shift:** Executing the `syscall` assembly token causes the processor hardware to instantly freeze the user-space stack, elevate its internal current privilege status bits to Ring 0, and reference the **Interrupt Vector Table (IVT)** to handle the request safely.

---

### 🛠️ 5. Practical Lab Exercise: Injecting Raw Inline Assembly

Follow these precise sequential execution commands inside your console shell to build and audit a raw vector gatekeeper loop:

#### Step 1: Author the System Trap Routine
Open an inline terminal text editor window pane and create a new source document file named exactly `raw_syscall.c`:
```bash
nano raw_syscall.c
```
*Paste this complete, zero-omission assembly configuration structure inside the editor workspace canvas area:*
```c
#include <unistd.h>

int main() {
    // Define the raw target character string data memory block
    char* message = "📦 System Trap Success: Greetings from raw assembly silicon lines!\n";

    // Invoke raw inline assembly instructions to bypass standard high-level wrappers
    __asm__(
        "movq \$1, %%rax; \n"  // Linux Syscall Identifier Key #1 is explicitly 'write'
        "movq \$1, %%rdi; \n"  // Argument Parameter 1: File descriptor stdout (1)
        "movq %0, %%rsi; \n"  // Argument Parameter 2: Direct memory pointer allocation to string
        "movq \$68, %%rdx; \n" // Argument Parameter 3: Strict character count array buffer length
        "syscall; \n"         // Fire electronic hardware trap to elevate state to Ring 0!
        :
        : "r"(message)
        : "%rax", "%rdi", "%rsi", "%rdx"
    );

    return 0;
}
```
*Save the document layout and exit the editor panel wrapper.*

#### Step 2: Compile the Hardware Vector Program
Invoke the system compiler toolchain to build your low-level program:
```bash
gcc raw_syscall.c -o raw_syscall
```

#### Step 3: Trigger the Gatekeeper Interface
Execute the compiled binary application right inside your console line loop interface:
```bash
./raw_syscall
```
*Document the text output displayed onto your terminal screen.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **movq:** The x86_64 assembly instruction used to move a quadword (64-bit value) from a source location into a target processor hardware register lane.
- **File Descriptor 1 (stdout):** The standard integer index value used by Unix-like operating systems to route character output data streams back to the active console window.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 3, paste your data answers inside a clean file and submit it to your course folder:
1. Provide a text copy snippet showing the exact text output string printed when executing `./raw_syscall`.
2. Identify the specific numeric ID code assigned to the `write` system call service entry point inside the x86_64 Linux vector matrix.
3. Based on our bulletproof bank teller counter analogies, explain in two short sentences why an application is completely blocked from altering its own user privilege bits inside software states.
