# 🔬 LAB 14: Synchronization — Auditing Race Conditions and Mutex Isolation
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will construct a concurrent application in C to capture a live data race hazard over a shared global state resource. You will then refactor the application thread loops using POSIX mutex locking primitives to enforce absolute mutual exclusion.

### 🛑 2. Prerequisites
- Access to an engineering terminal shell loop with the GCC toolchain installed (`gcc`).
- Thorough structural comprehension of thread execution models, critical section boundaries, and atomic states.

### 🎪 3. The Pedagogical Hook: Defending the Ledger Balance
Imagine you are building a high-speed banking system that processes millions of concurrent deposits. If two parallel thread lanes read, update, and write back to the identical balance variable in the exact same millisecond without coordination, they will step on each other's toes—causing complete deposits to vanish out of the ledger track. This isn't a compilation syntax fault; it is a race condition. In this lab, you will code this exact corruption exploit, trace its mathematical chaos, and deploy a hardware-backed lock to make your variables completely bulletproof.

---

### 🔍 4. System Core Breakdown
- **The Race Hazard:** A concurrency bug that occurs when multiple concurrent points write to an unprotected memory layout address simultaneously, causing variables to drop updates based on non-deterministic thread interleaving order.
- **Mutual Exclusion Guards:** Low-level software and hardware barriers that isolate a critical section window, forcing arriving competitor threads to stall inside a wait loop until the active holder surrenders the reservation token.

---

### 🛠️ 5. Practical Lab Exercise: Exploiting and Fixing Data Races

Follow these precise sequential execution commands inside your console shell to track race anomalies:

#### Step 1: Code the Broken Race Condition Ledger
Open an inline terminal text editor window pane and create a new C source file named exactly `race_hazard.c`:
```bash
nano race_hazard.c
```
*Paste this complete, unprotected code layout blueprint inside the editor canvas editor area:*
```c
#include <pthread.h>
#include <stdio.h>

// Shared mutable global state variable residing in the process Data Segment
int global_bank_balance = 0; 

void* deposit_routine(void* arg) {
    for(int i = 0; i < 100000; i++) {
        // --- START CRITICAL SECTION ---
        // This increment step expands into 3 distinct assembly lines:
        // 1. Read RAM into CPU register | 2. Add 1 | 3. Write register to RAM
        global_bank_balance++; 
        // ---- END CRITICAL SECTION ----
    }
    return NULL;
}

int main() {
    pthread_t thread1, thread2;
    printf("🧬 Spawning parallel deposit routines over shared address space...\n");

    // Launch two parallel threads executing the unprotected increment loop concurrently
    pthread_create(&thread1, NULL, deposit_routine, NULL);
    pthread_create(&thread2, NULL, deposit_routine, NULL);

    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);

    // Expected mathematical total is 200,000. Analyze what prints live!
    printf("📊 Final Unprotected Ledger Balance Value: %d\n", global_bank_balance);
    return 0;
}
```
*Save the document and exit the text editor wrapper layout panel.*

#### Step 2: Compile and Exploit the Ledger Race
Invoke the system compiler toolchain and run your binary multiple consecutive times:
```bash
gcc -pthread race_hazard.c -o race_hazard
./race_hazard
./race_hazard
```
*Analyze your final terminal output balance value printed on each run. Notice how the values are completely incorrect, changing dynamically across every execution because updates overwrite each other.*

#### Step 3: Refactor the Code with Mutex Lock Guards
Open a new source document file named exactly `mutex_solution.c` and refactor the routine to introduce a POSIX mutual exclusion block:
```bash
nano mutex_solution.c
```
```c
#include <pthread.h>
#include <stdio.h>

int global_bank_balance = 0; 
// Initialize an authoritative mutual exclusion reservation token
pthread_mutex_t ledger_lock = PTHREAD_MUTEX_INITIALIZER; 

void* safe_deposit_routine(void* arg) {
    for(int i = 0; i < 100000; i++) {
        pthread_mutex_lock(&ledger_lock); // ENTRY PATH: Claim Exclusive Reservation Flag

        // --- START CRITICAL SECTION ---
        global_bank_balance++;            // Isolated and guaranteed atomic write loop
        // ---- END CRITICAL SECTION ----

        pthread_mutex_unlock(&ledger_lock); // EXIT PATH: Release Reservation Flag
    }
    return NULL;
}

int main() {
    pthread_t thread1, thread2;
    printf("🛡️ Spawning guarded parallel threads with Mutex protection...\n");

    pthread_create(&thread1, NULL, safe_deposit_routine, NULL);
    pthread_create(&thread2, NULL, safe_deposit_routine, NULL);

    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);

    printf("🏆 Final Absolute Guaranteed Balance Total: %d\n", global_bank_balance);
    return 0;
}
```
*Compile and execute your fixed solution application:*
```bash
gcc -pthread mutex_solution.c -o mutex_solution
./mutex_solution
```
*Observe the output. The final total hits exactly 200,000 every execution without error.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Critical Section:** A structural window of source code that executes modifications on a shared mutable resource, requiring synchronization to prevent data corruption.
- **PTHREAD_MUTEX_INITIALIZER:** A macro used to initialize a standard POSIX fast mutex lock descriptor variable with baseline hardware configuration flags.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 14, paste your data answers inside a clean file and submit it to your course folder:
1. Provide a text copy snippet showing the exact numerical output values printed during your Step 2 (Unprotected) runs vs. your Step 3 (Guarded) run.
2. Under the hood, a standard variable increment statement like `global_bank_balance++` compiles into three separate machine assembly instructions. Identify those three distinct register operations.
3. Based on our shared digital piggy bank analogies, explain in two short sentences why introducing mutex locks over tight loops causes an execution performance slowdown compared to completely uncoordinated concurrent threads.
