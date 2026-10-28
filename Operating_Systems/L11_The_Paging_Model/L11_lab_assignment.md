# 🔬 LAB 11: Fixed-Size Translations — Simulating Page Table Walks
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will manually simulate the bit-splitting and pointer lookup operations performed by a physical Memory Management Unit (MMU). You will isolate virtual page indices, parse page table arrays, and map abstract logical reference streams straight to real hardware frames.

### 🛑 2. Prerequisites
- Completion of Lab 10 hardware relocation calculations.
- Basic understanding of binary-to-decimal conversion parameters and bit masking filters.

### 🎪 3. The Pedagogical Hook: Fixing the Shattered Track
In our previous module exercises, we discovered how contiguous variable-sized memory models trap operating systems into an external fragmentation corner—leaving physical RAM riddled with tiny, unusable gaps between programs. Paging completely shatters this constraint. By cutting your application space into uniform fixed pages and physical RAM into frames, the kernel can scatter your code anywhere there is an open block. In this lab, you will step inside the MMU lookup engine to see how a simple index table makes non-contiguous physical chaos look perfectly linear to the executing software.

---

### 🔍 4. System Core Breakdown
- **Bit Splitting:** The architectural procedure where the high-order bits of a virtual address stream are isolated to form the Page Number index, while the low-order bits pass through untouched as the intra-page byte Offset.
- **The Page Table Walk:** The real-time evaluation step where the CPU reads the active task's page directory lookup array to trade a virtual page index key for a real physical frame vector.

---

### 🛠️ 5. Practical Lab Exercise: Simulating a 6-Bit Paging Engine

Follow these precise sequential execution steps to perform an architectural page translation walk:

#### Step 1: Analyze the Architecture Specifications
Imagine a lightweight 6-bit binary virtual address space setup. The address fields split across these precise hardware lines:
- **High-Order Bits [5:4] (2 Bits):** Dedicated Page Number index (`p`).
- **Low-Order Bits [3:0] (4 Bits):** Dedicated Intra-Page Byte Offset (`d`).
*Note: A 4-bit offset means each individual page block spans exactly 16 bytes.*

#### Step 2: Read the Active Core Page Table Ledger
The kernel scheduler has loaded the following page table matrix array into the active MMU register cache slots:
- **Page Index 0 (Binary `00`):** Maps straight to Physical Frame `6` (Binary `110`)
- **Page Index 1 (Binary `01`):** Maps straight to Physical Frame `2` (Binary `010`)
- **Page Index 2 (Binary `10`):** Maps straight to Physical Frame `0` (Binary `000`)
- **Page Index 3 (Binary `11`):** Maps straight to Physical Frame `7` (Binary `111`)

#### Step 3: Translate the Execution Stream Traces
Trace and evaluate the physical destinations for these arriving virtual address parameters:

1. **Trace Item A: Virtual Address `010100` in binary.**
   - *Split Bits:* High 2 bits = `01` (Page Index 1). Low 4 bits = `0100` (Offset 4).
   - *Table Lookup:* Page Index 1 maps directly to Physical Frame `2` (Binary `010`).
   - *Reassemble Matrix:* Combine Frame `010` with original Offset `0100`.
   - *Physical Output Vector:* `Binary: 0100100 (Decimal Address: _____)`

2. **Trace Item B: Virtual Address `110010` in binary.**
   - *Split Bits:* High 2 bits = `11` (Page Index 3). Low 4 bits = `0010` (Offset 2).
   - *Table Lookup:* Page Index 3 maps directly to Physical Frame `7` (Binary `111`).
   - *Reassemble Matrix:* Combine Frame `111` with original Offset `0010`.
   - *Physical Output Vector:* `Binary: 1110010 (Decimal Address: _____)`

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Virtual Page Number (VPN):** The index array key extracted from an address bit stream to reference an entry point inside a process's page table directory.
- **Physical Frame Number (PFN):** The real physical base address coordinate returned by an MMU lookup table to define a location inside RAM chips.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 11, paste your data answers inside a clean file and submit it to your course folder:
1. Provide your completed final decimal hardware address values calculated for both Trace Item A and Trace Item B inside Step 3.
2. State the maximum byte length of a single page allocation under a system architecture that features a 12-bit address stream offset tracking field.
3. Based on our phonebook indexed page analogies, explain in two short sentences why a multi-level paging model structure introduces a performance translation delay compared to older, simple base-and-bound register schemes.
