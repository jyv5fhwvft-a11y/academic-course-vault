# 🔬 LAB 17: Storage Abstractions — Simulating Virtual File System Path Walks
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically simulate a Virtual File System (VFS) directory translation module. You will sequentially parse absolute path strings, traverse nested directory files, trade entry names for unique Inode keys, and isolate path parsing boundaries by hand.

### 🛑 2. Prerequisites
- Completion of Lab 16 hard disk latency and storage reality calculations.
- Thorough procedural tracking comprehension of hierarchical tree graphs and directory lookup records.

### 🎪 3. The Pedagogical Hook: The Map of Nameless Blocks
When you run a command to read a file like `cat /home/user/code.c`, your operating system cannot jump straight to those data bytes inside the hardware blocks. To the underlying hard disk or SSD substrate, text names mean absolutely nothing; the device only knows numeric sector blocks. A directory tree is simply a beautiful optical illusion maintained by the kernel. In this lab, you will act as the VFS path routing engine, opening directory maps one-by-one to translate a human path string into a hard system index key.

---

### 🔍 4. System Core Breakdown
- **Directory Resolution Walks:** The structural loop where a file system parses a path string character-by-character from left to right, matching directory names to unique inode index blocks until the final destination entity maps.
- **The Inode Identifier Key:** A distinct, non-negative integer token that identifies a specific metadata block descriptor containing file access rights, sizes, and direct data pointer slots.

---

### 🛠️ 5. Practical Lab Exercise: Simulating a VFS Path Traversal Walk

Follow these precise sequential execution command steps to perform a path resolution audit:

#### Step 1: Analyze the Active Storage Partition Ledger
A traditional Linux style file system has been mounted on Core 0. The raw storage sectors hold the following directory indexing records:
- **Root Directory (Hardcoded Inode #2) Contains:**
  - `.` ➔ Inode #2  |  `..` ➔ Inode #2
  - `etc` ➔ Inode #14  |  `home` ➔ Inode #29  |  `var` ➔ Inode #55
- **Folder `home` (Directory File Inode #29) Contains:**
  - `.` ➔ Inode #29  |  `..` ➔ Inode #2
  - `guest` ➔ Inode #102  |  `student` ➔ Inode #214
- **Folder `student` (Directory File Inode #214) Contains:**
  - `.` ➔ Inode #214  |  `..` ➔ Inode #29
  - `project.c` ➔ Inode #9410  |  `notes.txt` ➔ Inode #4402

#### Step 2: Trace Absolute Path `/home/student/project.c`
Trace the file system traversal steps block-by-block to resolve the physical target pointer:
1. **Walk Milestone A:** The kernel kicks off the search path by loading the hardcoded root entry: **Inode #______**.
2. **Walk Milestone B:** The VFS opens the root directory data blocks and scans rows to locate string "home". It extracts the matched folder destination target key: **Inode #______**.
3. **Walk Milestone C:** The VFS opens the index table rows of that extracted folder node and scans down to locate the string "student". It pulls down its paired index identifier: **Inode #______**.
4. **Walk Milestone D:** The VFS opens the data blocks of that target student node, finds row matching "project.c", and lands on the absolute final file metrics marker node: **Inode #______**.

#### Step 3: Audit Structural Links
1. A student logs onto the environment shell loop and creates an additional directory entry using a hard link command: `ln /home/student/notes.txt /home/student/link1.txt`. Identify the exact Inode index number assigned to the new entry string `link1.txt`.
2. Next, the user creates an independent shortcut text pointer via a symbolic soft link command: `ln -s /home/student/notes.txt /home/student/link2.txt`. Explain in one sentence what specific data is written inside the new data block allocated for `link2.txt`.

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Virtual File System (VFS):** The master kernel subsystem abstraction layer that presents a uniform file access interface to user space applications, regardless of the underlying storage hardware file layouts.
- **Hard Link:** A directory map pointer shortcut that binds a fresh human-readable name string directly to an existing, shared historical inode data block.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 17, paste your text analysis parameters inside a clean file and submit it to your course folder:
1. Provide your completed numerical Inode destination keys derived for Milestones A, B, C, and D inside Step 2.
2. Provide your hard link Inode target number and your symbolic link data block explanation from Step 3.
3. Based on our nested boxes analogies, explain in two short sentences what happens to access throughput if a user builds a giant folder path that has 50 nested sub-directories before reaching their target data file.
