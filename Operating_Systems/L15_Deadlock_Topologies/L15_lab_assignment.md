# 🔬 LAB 15: Deadlock Analysis — Graphing Coffman Topologies and Lock Ordering
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will author a concurrent C application that intentionally triggers a deterministic deadlock state using cross-nested locks. You will map the resource layout via a Resource Allocation Graph (RAG) and refactor the execution sequence to eliminate the trap by breaking the Circular Wait condition.

### 🛑 2. Prerequisites
- Access to an engineering terminal shell loop with the GCC toolchain installed (`gcc`).
- Thorough understanding of POSIX mutex locking loops and the four Coffman Conditions.

### 🎪 3. The Pedagogical Hook: The Asymmetric Fix
In our previous lab, we deployed a mutex lock to guarantee complete data isolation over a shared variable, which successfully fixed our data race. However, introducing locks can create a severe secondary risk. If Sibling A holds Lock 1 and waits for Lock 2, while Sibling B holds Lock 2 and waits for Lock 1, both threads freeze permanently. In this lab, you will intentionally build this architectural loop, trace its geometric bottleneck on the board, and deploy a strict acquisition ordering strategy to completely break the lock gridlock.

---

### 🔍 4. System Core Breakdown
- **The Deadlock Trap:** A fatal concurrency gridlock state where a set of processes are permanently paralyzed because every process holds an exclusive resource lock while waiting for an alternative resource held by another process in that same set.
- **Lock Acquisition Ordering:** A robust preventative design strategy where all competing process threads are forced to acquire multiple shared locks in an identical, strictly sorted global index hierarchy, making circular wait loops mathematically impossible.

---

### 🛠️ 5. Practical Lab Exercise: Charting and Resolving Deadlock Loops

Follow these precise sequential execution commands inside your console shell to track deadlock topologies:

#### Step 1: Code the Frozen Deadlock Gridlock
Open an inline terminal text editor window pane and create a new C source file named exactly `deadlock_trap.c`:
```bash
nano deadlock_trap.c
```
*Paste this complete, multi-lock deadlocking blueprint inside the editor canvas editor area:*
```c
#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

// Initialize two independent mutual exclusion locks
pthread_mutex_t lock_X = PTHREAD_MUTEX_INITIALIZER;
pthread_mutex_t lock_Y = PTHREAD_MUTEX_INITIALIZER;

void* worker_one_routine(void* arg) {
    printf("🧵 Worker 1: Attempting to claim Lock X...\n");
    pthread_mutex_lock(&lock_X);
    printf("🔒 Worker 1: Successfully secured Lock X! Holding and waiting...\n");
    
    // Inject a sleep window to force a context switch preemption window
    sleep(1); 
    
    printf("🧵 Worker 1: Attempting to claim Lock Y...\n");
    pthread_mutex_lock(&lock_Y); // This thread will block here indefinitely!
    
    printf("💥 Worker 1: Secured both locks successfully!\n");
    pthread_mutex_unlock(&lock_Y);
    pthread_mutex_unlock(&lock_X);
    return NULL;
}

void* worker_two_routine(void* arg) {
    printf("🧵 Worker 2: Attempting to claim Lock Y...\n");
    pthread_mutex_lock(&lock_Y);
    printf("🔒 Worker 2: Successfully secured Lock Y! Holding and waiting...\n");
    
    // Inject a sleep window to force a context switch preemption window
    sleep(1); 
    
    printf("🧵 Worker 2: Attempting to claim Lock X...\n");
    pthread_mutex_lock(&lock_X); // This thread will block here indefinitely!
    
    printf("💥 Worker 2: Secured both locks successfully!\n");
    pthread_mutex_unlock(&lock_X);
    pthread_mutex_unlock(&lock_Y);
    return NULL;
}

int main() {
    pthread_t t1, t2;
    printf("🧬 Spawning cross-nested concurrent threads to test deadlock lines...\n");

    pthread_create(&t1, NULL, worker_one_routine, NULL);
    pthread_create(&t2, NULL, worker_two_routine, NULL);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    printf("🏆 Application Cleaned and Finished. (This line will never print!)\n");
    return 0;
}
```
*Save the document and exit the text editor wrapper layout panel.*

#### Step 2: Compile and Observe the Freezing Application
Invoke the system compiler toolchain and run your binary program:
```bash
gcc -pthread deadlock_trap.c -o deadlock_trap
./deadlock_trap
```
*Observe your terminal screen. Notice how both threads claim their first resource successfully, attempt to step into their second lock statement, and then freeze solid permanently. The application hangs indefinitely until you forcefully terminate it with `Ctrl+C`.*

#### Step 3: Refactor the Code to Enforce Global Lock Ordering Hierarchy
Open a new source document file named exactly `lock_order_solution.c` and refactor the execution sequence of Worker 2 to match the exact same lock ordering hierarchy utilized by Worker 1:
```bash
nano lock_order_solution.c
```
```c
#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

pthread_mutex_t lock_X = PTHREAD_MUTEX_INITIALIZER;
pthread_mutex_t lock_Y = PTHREAD_MUTEX_INITIALIZER;

void* safe_worker_one_routine(void* arg) {
    pthread_mutex_lock(&lock_X);
    sleep(1); 
    pthread_mutex_lock(&lock_Y); 
    
    printf("🏆 Safe Worker 1: Secured both locks successfully!\n");
    pthread_mutex_unlock(&lock_Y);
    pthread_mutex_unlock(&lock_X);
    return NULL;
}

void* safe_worker_two_routine(void* arg) {
    // --- REFACTORED SEQUENCE TO BREAK CIRCULAR WAIT LOOP ---
    // Force Worker 2 to acquire Lock X *before* attempting Lock Y
    pthread_mutex_lock(&lock_X); 
    sleep(1); 
    pthread_mutex_lock(&lock_Y); 
    
    printf("🏆 Safe Worker 2: Secured both locks successfully!\n");
    pthread_mutex_unlock(&lock_Y);
    pthread_mutex_unlock(&lock_X);
    return NULL;
}

int main() {
    pthread_t t1, t2;
    printf("🛡️ Spawning sorted parallel threads with Global Lock Ordering...\n");

    pthread_create(&t1, NULL, safe_worker_one_routine, NULL);
    pthread_create(&t2, NULL, safe_worker_two_routine, NULL);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    printf("🏆 Clean Execution Verified! Application exit loop finalized securely.\n");
    return 0;
}
```
*Compile and execute your sorted lock solution application:*
```bash
gcc -pthread lock_order_solution.c -o lock_order_solution
./lock_order_solution
```
*Observe the output. The application executes both thread branches consecutively and exits cleanly without ever freezing.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Resource Allocation Graph (RAG):** A visual state graph where vertices represent active threads and resource units, and directional edges denote existing allocations or pending requests.
- **Circular Wait:** A specific architectural flaw condition where a closed-loop chain of competing threads exists, such that each thread waits for a lock held by its adjacent neighbor.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 15, paste your data answers inside a clean file and submit it to your course folder:
1. Provide a text copy snippet showing the final terminal logs printed when executing the deadlocked binary in Step 2 vs. your working solution in Step 3.
2. In your Step 1 code, identify the precise names of the two Coffman conditions that are explicitly triggered when the execution sequence steps through the `sleep(1)` context switch preemption window.
3. Based on our inner classroom chair-circling activities, explain in two short sentences how enforcing an identical global lock acquisition order across all threads eliminates the possibility of a Circular Wait condition.
