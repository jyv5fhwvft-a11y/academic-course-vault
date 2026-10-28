# 🔬 LAB 22: Access Control Security — Auditing Protection Domains, ACLs, and Capabilities
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically model operating system security protection domains. You will deconstruct sparse Access Control Matrices, trace column-oriented Access Control Lists (ACLs) vs. row-oriented Capability Tokens, and parse bitwise Unix permission strings to enforce the principle of least privilege.

### 🛑 2. Prerequisites
- Completion of Module 5 and Module 6 directory topology and file descriptor management labs.
- Thorough procedural understanding of dual-mode isolation boundaries (Ring 0 vs. Ring 3).

### 🎪 3. The Pedagogical Hook: Slicing the Security Grid
Every time an application attempts to view a file, bind to a network socket, or toggle a device register, the operating system must answer a fundamental question: *Does this running process have permission to execute this step?* To manage this, the kernel models the entire system's security profile as a massive grid matching users to resources. However, storing a giant, mostly empty spreadsheet wastes massive kernel memory. In this lab, you will act as a security engineer, analyzing two completely different ways to slice this grid down into lean, unforgeable data streams to secure your assets.

---

### 🔍 4. System Core Breakdown
- **Column-Oriented Protection (ACLs):** Slicing the access matrix vertically by binding the permission ledger directly onto the resource container itself, forcing the asset to act as its own security gatekeeper.
- **Row-Oriented Protection (Capabilities):** Slicing the access matrix horizontally by handing unforgeable, kernel-signed authorization keys directly to the process execution context, which are presented like keycards on demand.

---

### 🛠️ 5. Practical Lab Exercise: Profiling the Access Matrix Architecture

Follow these precise structural evaluation steps to solve your access control security profiles:

#### Step 1: Deconstruct the Sparse Access Control Matrix
Imagine an isolated research server containing three distinct user subjects (Alice, Bob, Charlie) and three target resource objects (file_A.txt, /dev/ttyS0, network_socket). The active matrix parameters are defined as follows:
- **Alice Domain:** Read/Write over `file_A.txt` | No Access over `/dev/ttyS0` | Execute over `network_socket`
- **Bob Domain:** Read over `file_A.txt` | Read/Write over `/dev/ttyS0` | No Access over `network_socket`
- **Charlie Domain:** No Access over `file_A.txt` | Read over `/dev/ttyS0` | Read/Write/Execute over `network_socket`

#### Step 2: Implement Column-Oriented ACL Maps
You are migrating this server to a file system layout that relies on column-oriented Access Control Lists (ACLs). 
1. Transpose the matrix parameters from Step 1 to define the explicit ACL ledger attached to the resource object container **`file_A.txt`**.
   - *Your Derived ACL Ledger:* __________________
2. Explain where this list data is physically stored under the hood inside a traditional UNIX-like file architecture layout. *(Hint: Review Lecture 18 inode design fields!)*
   - *Your Answer:* __________________

#### Step 3: Parse Packed Bitwise Unix Permission Vectors
A system administrator executes an audit check loop over a secured file node via terminal, returning this 9-bit packed string: `rwxr-x---`.
1. Break down the three isolated user clearance domains to evaluate the file's protection boundaries:
   - **Owner/User Permissions:** [Read: Yes/No | Write: Yes/No | Execute: Yes/No] ➔ __________________
   - **Group Permissions:** [Read: Yes/No | Write: Yes/No | Execute: Yes/No] ➔ __________________
   - **Others/World Permissions:** [Read: Yes/No | Write: Yes/No | Execute: Yes/No] ➔ __________________
2. A process owned by a user inside the Group domain attempts to invoke an `open()` call with a `O_WRONLY` (Write-Only) modification access flag over this file. Identify whether the kernel's Virtual File System layer logs a **[VFS Access Granted]** clearance or fires a **[SIGSEGV / Permission Denied]** security trap error block.
   - *Your Answer:* __________________

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Protection Domain:** A bounded environment envelope defining the exact combination of access rights and commands a process context holds over system objects.
- **Capability:** A secure, unforgeable row-oriented token carried inside a process's task block that grants instant access to whichever resource lock it matches.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 22, paste your data answers inside a clean file and submit it to your course folder:
1. Provide your completed resource ACL map list and inode storage explanation derived for Step 2.
2. Provide your bitwise permission breakdowns and your group write access determination calculated inside Step 3.
3. Based on our hotel room ledger and electronic keycard models, explain in two short sentences why storing capability tokens inside mutable, un-encrypted user space (Ring 3 memory page frames) would completely collapse system security.
