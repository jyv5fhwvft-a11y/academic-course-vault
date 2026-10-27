# 🔬 LAB 9: Concurrent Spaces — Measuring Thread Context Shared Primitives
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will author a multi-threaded C application using the POSIX pthreads toolchain. You will analyze the parallel execution layout of concurrent worker paths and verify how multiple execution streams share global memory space segments while keeping separate execution stacks.

### 🛑 2. Prerequisites
- Access to an engineering terminal shell loop with the GCC toolchain installed (`gcc`).
- Clear structural understanding of process memory segments (Heap, Data) versus isolated thread execution stacks.

### 🎪 3. The Pedagogical Hook: Sharing the Vault
When you spin up concurrent threads inside a parent process container, you are creating a highly cooperative team of workers. Unlike independent processes that must run expensive system traps to trade raw numbers across isolation boundaries, threads share an open-floor blueprint. They can mutate the exact same global array variables instantly without checking through kernel vectors. However, this absolute speed introduces severe architectural traps. If two worker threads write to the same address line at the same time, they break consistency, paving the path for racing conditions.

---

### 🔍 4. System Core Breakdown
- **Shared Segments:** Threads skip process isolation rules to natively share a process's initialized/uninitialized global variables (the Data Segment) and dynamically requested pointer blocks (the Heap).
- **Private Stack Allocations:** To preserve chronological execution integrity, every individual thread receives an isolated stack frame layout allocation to track local parameters and call chains.

---

### 🛠️ 5. Practical Lab Exercise: Deploying Parallel POSIX Workers

Follow these precise sequential execution commands inside your console shell to build and trace thread concurrency properties:

#### Step 1: Code the Concurrent Multi-Worker Script
Open an inline terminal text editor window and create a new C source file named exactly `thread_test.c`:
```bash
nano thread_test.c
```
*Paste this complete, multi-threaded diagnostic structure inside the editor file area canvas:*
```c
#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

// Shared resource variable residing in the process Data Segment
int shared_global_counter = 0;

void* worker_routine(void* arg) {
    int thread_local_id = *((int*)arg);
    
    // Private variable tracking independent stack frames
    int localized_stack_accumulation = 0;

    for(int i = 0; i < 5; i++) {
        localized_stack_accumulation++;
        shared_global_counter++; // Direct modification of shared ecosystem context
        
        printf(" 🧵 Thread #%d | Local Stack Accumulator: %d | Shared Global Counter: %d\n", 
               thread_local_id, localized_stack_accumulation, shared_global_counter);
        
        usleep(100000); // Sleep briefly to force interleaved execution paths
    }

    return NULL;
}

int main() {
    pthread_t thread1, thread2;
    int id1 = 1, id2 = 2;

    printf("🧬 Main parent thread initializing concurrent experiment...\n");

    // Spin up two lightweight execution workers inside the same address space
    pthread_create(&thread1, NULL, worker_routine, (void*)&id1);
    pthread_create(&thread2, NULL, worker_routine, (void*)&id2);

    // Block main execution until both concurrent sibling workers cross the finish line
    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);

    printf("🏆 Experiment Finalized. Final Shared Global Counter Value: %d\n", shared_global_counter);
    return 0;
}
```
*Save the document and exit the editor panel wrapper.*

#### Step 2: Compile the Multi-Threaded Binary
Invoke the system compiler toolchain, making sure to explicitly link the POSIX threads processing engine configuration library:
```bash
gcc -pthread thread_test.c -o thread_test
```

#### Step 3: Trigger the Concurrent Lifecycle Audit
Execute the compiled binary application right inside your console line loop interface:
```bash
./thread_test
```
*Analyze the output arrays. Note how the printed global values interleave out of order as both threads mutate the identical memory vector address simultaneously.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **pthread_create:** The POSIX system library command loop that allocates a lightweight execution thread context within the calling process boundaries.
- **pthread_join:** A synchronization primitive used to suspend the execution path of the caller thread until the targeted thread finishes its run loop.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 9, paste your data answers inside a clean file and submit it to your course folder:
1. Provide a text copy snippet showing the exact text output string layout printed when executing `./thread_test`.
2. Observe your final global counter value. Explain in two short sentences why the final output value equals exactly 10, despite both workers executing concurrently over interleaved time schedules.
3. Based on our stage actors analogies, explain in two short sentences what severe side effect occurs if one thread encounters a fatal null pointer dereference crash inside a shared heap buffer.
