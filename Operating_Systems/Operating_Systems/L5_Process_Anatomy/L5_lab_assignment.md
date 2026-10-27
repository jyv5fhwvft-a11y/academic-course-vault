# 🔬 LAB 5: Process Mapping — Visualizing Memory Address Spaces in C
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will author a compiled C language program to output the active runtime virtual memory address layout of a running process. You will calculate address vectors to map where variables belong across the Text, Data, Heap, and Stack segments.

### 🛑 2. Prerequisites
- Access to an engineering terminal console loop with the GCC toolchain installed (`gcc`).
- Clear understanding of the conceptual layout of an application address space (Stack vs. Heap vs. Data segments).

### 🎪 3. The Pedagogical Hook: Mapping the Illusions
When you print out a memory address or dereference a pointer in C, your application is looking through virtual glasses. The address values printed look like raw hardware slots, but they are entirely virtual mappings managed by the kernel core referee. In this lab, we are going to draw a complete architectural map of these virtual boundaries. By declaring variables in different logical scopes, you will watch how the compiler separates assets into specialized sectors.

---

### 🔍 4. System Core Breakdown
- **Segment Spacing:** Operating system kernels partition application segments with massive address space buffer cushions. The Stack starts high in memory and grows downward, while the Heap starts low and scales upward.
- **The Process Maps Interface:** Linux hosts expose a virtual debugging file framework located inside `/proc/[PID]/maps` that details the exact address boundaries assigned to every segment tracking memory region.

---

### 🛠️ 5. Practical Lab Exercise: Visualizing Segment Vectors

Follow these precise sequential execution commands inside your console shell to build and trace an application memory map:

#### Step 1: Code the Target Workspace Application
Open an inline terminal text editor window pane and create a new source document file named exactly `proc_map.c`:
```bash
nano proc_map.c
```
*Paste this complete, zero-omission C memory mapping blueprint inside the editor workspace canvas area:*
```c
#include <stdio.h>
#include <stdlib.h>

// 1. Initialized Global Variable: Belongs inside the Data Segment
int global_initialized_var = 42;

int main() {
    // 2. Local Stack Variable: Maps inside the auto-managed Stack segment
    int local_stack_var = 100;

    // 3. Dynamically Allocated Variable: Extends boundaries inside the Heap segment
    int *heap_pointer_var = (int*)malloc(sizeof(int));

    printf("=================================================================\n");
    printf("🧬 PRINTING PROCESS SEGMENT VIRTUAL ADDRESS MATRIX\n");
    printf("=================================================================\n");

    // Print text segment address by reference pointer to the main execution block
    printf(" [TEXT]  Main Function Compiled Code Vector: %p\n", (void*)&main);
    
    // Print data segment address parameters
    printf(" [DATA]  Initialized Global Entry Vector:     %p\n", (void*)&global_initialized_var);
    
    // Print heap expansion dynamic blocks
    printf(" [HEAP]  Allocated Heap Buffer Pointer Vector: %p\n", (void*)heap_pointer_var);
    
    // Print transient high-speed stack frames
    printf(" [STACK] Active Stack Frame Allocation Vector: %p\n", (void*)&local_stack_var);

    printf("=================================================================\n");
    printf("📊 Open a fresh terminal and run 'cat /proc/self/maps' to audit layout!\n");
    
    // Keep application alive temporarily to allow manual inspection
    printf("Sleeping... Press Ctrl+C to terminate runtime container.\n");
    while(1); 

    free(heap_pointer_var);
    return 0;
}
```
*Save the document layout and exit the editor panel wrapper.*

#### Step 2: Compile the Segment Blueprint
Invoke the system compiler toolchain to build your low-level application:
```bash
gcc proc_map.c -o proc_map
```

#### Step 3: Trigger the Mapping Ledger
Execute the compiled binary application right inside your console line loop interface:
```bash
./proc_map
```
*Analyze the layout arrays output on your screen. Observe the massive distance in value ranges between the high-address stack variables and low-address text instruction segments.*

---

### 🏷️ 6. Architectural Lexicon / Terms
- **%p Format Specifier:** The specific format flag used inside C string routing functions to output an address value as a hexadecimal pointer grid structure.
- **Slab Allocator:** The inner kernel memory allocation subsystem responsible for caching uniform size data structure nodes (like active PCB task_struct blocks).

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 5, paste your technical data logs inside a clean document file and submit it to your course workspace folder:
1. Provide a text copy snippet showing the exact text output matrix printed when executing `./proc_map`.
2. Sort your printed segment hex values chronologically from the lowest virtual address memory vector to the absolute highest memory vector.
3. Based on our corporate business accountant analogies, explain in two short sentences why a process cannot read or inspect tracking ledger metrics stored inside a neighbor company's PCB slot block.
