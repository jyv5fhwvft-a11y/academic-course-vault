# 🔬 LAB 6: Process Lifecycles — Auditing fork() and execv() Execution Paths
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will construct a multitasking Unix-like application to investigate how operating system kernels fork process containers, branch conditional path lanes, and overwrite active address spaces cleanly using core system call primitives.

### 🛑 2. Prerequisites
- Access to an engineering terminal shell loop with the GCC toolchain installed (`gcc`).
- Thorough structural comprehension of process segment anatomy (Stack, Heap, Text blocks) and the role of the Program Counter.

### 🎪 3. The Pedagogical Hook: Visualizing the Dual-Runner
When you launch an application, it runs inside an isolated workspace. But how do new processes actively spin up inside an environment? By running a `fork()` system call, you break physical reality—you command the kernel to clone a running program mid-sentence. You create two independent runners running at the exact same speed, looking at the identical statement. In this lab, you will trace how these clone threads verify their identity keys to execute completely separate mission scripts.

---

### 🔍 4. System Core Breakdown
- **Address Space Forking:** The `fork()` call creates a complete copy of the caller task. The child process receives an isolated, matching page table matrix, but a distinct Process Identifier key (PID).
- **The Execution Overwrite:** Running `execv()` wipes the calling process's active address boundaries completely, dropping a fresh executable binary file onto the active processor timeline.

---

### 🛠️ 5. Practical Lab Exercise: Tracing Fork-and-Exec Sequences

Follow these precise sequential execution commands inside your console shell to build and audit a process lifecycle branch:

#### Step 1: Code the Shell Launch Pattern
Open your terminal text editor window and create a new C source file named exactly `lifecycle_test.c`:
```bash
nano lifecycle_test.c
```
*Paste this complete, multi-branch code blueprint inside the editor file area canvas:*
```c
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <stdio.h>

int main() {
    printf("🧬 Parent Runner (PID: %d) preparing to spawn clone...\n", getpid());
    
    // Command the kernel to clone the active execution block
    pid_t return_code = fork(); 

    if (return_code < 0) {
        // Error handling lane branch
        fprintf(stderr, "Critical Error: Process replication failed.\n");
        return 1;
    } else if (return_code == 0) {
        // Child execution path lane branch
        printf("🟢 Child Branch Active! (PID: %d). Overwriting address space...\n", getpid());
        
        // Define argument array parameters to load the system status utility
        char *args[] = {"/bin/ps", "-f", NULL};
        
        // Overwrite the child address space completely with the 'ps' binary
        execv(args[0], args); 
        
        // This protection line should never execute unless the override fails
        printf("🛑 System Fault: Execv overwrite sequence failed!\n");
    } else {
        // Parent execution path lane branch
        printf("🔵 Parent Branch Waiting (PID: %d) for child thread to finish...\n", getpid());
        
        // Pause parent execution until the child runner crosses the finish line
        wait(NULL); 
        printf("🏆 Parent Process cleanly resumed and exiting workspace.\n");
    }

    return 0;
}
```
*Save the document and exit the editor panel wrapper layout system.*

#### Step 2: Compile the Multi-Branch Binary
Invoke the system compiler toolchain to build your low-level application tracking utility:
```bash
gcc lifecycle_test.c -o lifecycle_test
```

#### Step 3: Trigger the Lifecycle Audit
Execute the compiled binary application right inside your console line loop interface:
```bash
./lifecycle_test
```
*Analyze the interleaved terminal rows. Note how the parent branch halts securely while the child branch jumps into the `ps` process status listing utility.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **wait(NULL):** A system call primitive that forces a parent process to pause its execution loop until one of its child processes terminates.
- **Copy-On-Write (COW):** A memory management optimization technique where cloned processes share identical physical memory page mappings until a write operation forces a page frame duplication.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 6, paste your data answers inside a clean file and submit it to your course folder:
1. Provide a text copy snippet showing the exact text output string layout printed when executing `./lifecycle_test`.
2. Explain what happens to the trailing code lines inside the child block after an `execv()` system call registers successfully.
3. Based on our Git branching vs. folder overwriting analogies, explain in two short sentences why a context switch is called a "CPU resource tax."
