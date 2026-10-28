# 🔬 LAB 18: File Layouts — Calculating Inode Scale Capacity Trees
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will manually trace an asymmetric block allocation tree structure to compute maximum file scale limits. You will act as the virtual file system kernel layer to calculate byte ceilings across direct, single indirect, and double indirect hardware pointer arrays.

### 🛑 2. Prerequisites
- Completion of Lab 17 path traversal walks and link abstractions.
- Practical math mastery over basic binary storage conversions (Kilobytes, Megabytes, Gigabytes).

### 🎪 3. The Pedagogical Hook: Splitting the Registry Ledger
When you write a multi-gigabyte virtual video block file or compile a massive database table onto a storage track, how does the operating system map those billions of bytes efficiently without consuming half your disk just tracking the index rows? By utilizing a structured index card system—the Inode. To keep space footprints exceptionally tiny for simple files, the kernel hooks straight into the data sectors using direct wires. But when a file grows into a monster asset, the structure branches out into a multi-tiered array network. In this lab, you will calculate exactly how far this branching index tree can reach.

---

### 🔍 4. System Core Breakdown
- **Asymmetric Block Allocation Trees:** A structural filesystem layout optimization strategy where a single inode data block maps file contents via a combination of direct blocks for speed and nested indirect index blocks for capacity scaling.
- **The Metadata Partition Firewall:** The absolute design boundary that isolates human organization text metrics (like filenames held inside directory tables) from system hardware allocation arrays (held inside fixed inode blocks).

---

### 🛠️ 5. Practical Lab Exercise: Solving the Inode Capacity Limits

Follow these precise sequential step calculation tracks to derive the storage footprint metrics of an index node structure:

#### Step 1: Analyze the Architecture Performance Specification
You are auditing an engineering storage layout configured with these physical parameters:
- **System Block Size Capacity (`Block_Size`):** `8 KB` (or `8192 Bytes`)
- **Disk Sector Pointer Address Cost (`Ptr_Cost`):** `8 Bytes` (64-bit hardware architecture flags)
- **Inode Allocation Block Layout Array Contains:** Exactly `10 Direct Pointers`, `1 Single Indirect Pointer`, and `1 Double Indirect Pointer`.

#### Step 2: Calculate the Capacity of Each Branch Limb
Derive the individual data block ceilings by tracking the pointer multiplication branches step-by-step:

1. **Calculate the Direct Branch Capacity:**
   - `10 Direct Pointers * 8 KB Block Size = _______ KB`

2. **Calculate the Single Indirect Branch Capacity:**
   - First, find how many pointer indices can fit inside one single intermediate index block:  
     `Pointers Per Block = 8192 Bytes / 8 Bytes per pointer = 1024 pointers.`
   - Now, calculate total capacity: `1024 pointers * 8 KB Block Size = 8192 KB = _______ MB`

3. **Calculate the Double Indirect Branch Capacity:**
   - This limb branches exponentially across two nested tiers: `1024 pointers * 1024 pointers = 1,048,576 pointers total.`
   - Compute the full data footprint: `1,048,576 pointers * 8 KB Block Size = 8,388,608 KB = _______ GB`

#### Step 3: Compute the Absolute Maximum File Sizing Limit
1. Add up the three values derived inside Step 2 to determine the absolute maximum file size cap supported by this storage system architecture:  
   `Maximum Data Ceiling = Direct Branch + Single Indirect + Double Indirect = _______ GB`

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Single Indirect Pointer:** An address slot inside an inode data frame that points directly to an interim indexing block allocated exclusively to cache additional address tracking pointers.
- **Double Indirect Pointer:** An address slot that routes traffic down through two separate stacked layers of pointer list tracking indices before mapping onto a real physical data sector block.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 18, paste your data answers inside a clean file and submit it to your course folder:
1. Provide your completed data capacity results derived for the Direct branch, Single Indirect branch, and Double Indirect branch inside Step 2.
2. Provide your final consolidated Maximum File Sizing Limit calculation total calculated in Step 3.
3. Based on our library ledger card models, explain in two short sentences why the human-readable filename string is completely stripped out of the fixed inode structure block and cached inside directory tables instead.
