# 🔬 LAB 27: System Isolation — Profiling Hypervisors, Namespaces, and Control Groups
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically audit operating system isolation abstractions. You will trace the architectural boundaries between hypervisor hardware emulation layers and native container primitives, map process namespace configurations, and calculate cgroup resource throttle parameters.

### 🛑 2. Prerequisites
- Completion of Lab 26 edge firewall rule parsing and internal network intrusion detection analysis.
- Thorough procedural understanding of process hierarchies, memory segmentation layout maps, and system call traps.

### 🎪 3. The Pedagogical Hook: The Illusion of the Dedicated Machine
When you launch an application inside a modern container runtime (like Docker), the container console environment reports that you are running as root on an isolated machine with a pristine, independent process tree. This is an optical illusion maintained entirely by the host operating system kernel. There are no virtual chipsets or emulated PCI buses under the hood—your application's compiled instructions run directly on the bare-metal host processor alongside your standard web browser or system background processes. In this lab, you will step behind the partition walls to analyze the visibility filters and resource meters used by the kernel to create this lightweight isolation layer.

---

### 🔍 4. System Core Breakdown
- **Kernel Namespace Isolation (The View):** A native monolithic kernel primitive that virtualizes system resource indices (PIDs, Mount paths, Networks), preventing processes inside that namespace domain from seeing outside assets.
- **Control Group Restrictions (The Limit):** A hardware throttling infrastructure used by the process scheduler and memory manager to enforce strict execution resource quotas (CPU cycles, RAM footprint ceilings) around process trees.

---

### 🛠️ 5. Practical Lab Exercise: Auditing Kernel Containment Boundaries

Follow these precise structural evaluation steps to solve your isolation security profiles:

#### Step 1: Contrast Virtualization Infrastructure Footprints
An engineering cluster must deploy an isolated web service. You are evaluating two deployment strategies: a full QEMU/KVM Virtual Machine and an unprivileged Docker Container runtime package.
1. Match the infrastructure layer trace to its corresponding deployment archetype: **[Full Hardware Virtual Machine]** OR **[Native Linux Container]**:
   - `[App] ➔ [Namespace Wrappers + cgroups Limits] ➔ [Shared Host Kernel Substrate]` ➔ __________________
   - `[App] ➔ [Guest OS Kernel Binary Instance] ➔ [Emulated Circuitry Layers] ➔ [Hypervisor Layer]` ➔ __________________
2. State the structural reason why the container model can initialize and spin up its application environment in milliseconds, while the hardware virtual machine requires seconds or minutes to settle its workspace.
   - *Your Answer:* __________________

#### Step 2: Simulate Process Tree Namespace Mapping
A process execution thread inside a standard user session calls a container instantiation loop. Under the hood, the kernel triggers a `clone()` system call appended with the specialized visibility filter flag: **`CLONE_NEWPID`**.
1. Identify the exact virtual Process Identifier integer index value assigned to the root process inside this newly generated namespace envelope.
   - *Your Virtual PID Target:* Inode/PID #_______
2. If this isolated process executes a malicious memory stack smashing exploit that successfully triggers a local system panic loop crash *inside* its namespace boundaries, explain whether the outer parent host operating system kernel collapses or remains unaffected.
   - *Your Security Evaluation:* __________________

#### Step 3: Formulate Control Group (cgroups) Resource Throttling Quotas
To prevent an isolated container process stream from triggering a Denial of Service (DoS) memory depletion condition across neighboring host segments, an administrator configures a `memory.max` resource quota threshold.
1. The hardware host machine contains exactly `32 GB` of physical primary RAM memory frames. The administrator maps the isolated group constraint parameters down to exactly `4,096,000,000 Bytes` (4 GB).
2. A thread running inside this container encounters an unchecked, leaky data memory stream allocation loop that attempts to grab `5 GB` of storage cells. Identify the exact kernel subsystem component that intervenes to kill this rogue process thread instantly, and state what specific system signal it fires.
   - *Your Answer:* __________________

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Namespace:** A native kernel configuration mechanism that partitions system layout infrastructure visibility (PIDs, Networks, Mounts) for a targeted process graph cluster.
- **Control Group (cgroup):** A kernel configuration throttling layer used to restrict maximum allocation consumption thresholds (CPU time slices, physical RAM bytes) around a target thread stream.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 27, paste your text data parameters inside a clean file and submit it to your course folder:
1. Provide your completed infrastructure layer trace matching definitions derived for Step 1.
2. Provide your virtual PID target number and your security evaluation result calculated inside Step 2.
3. Provide your container memory limit intervention subsystem identification and signaling action derived in Step 3.
4. Based on our separate apartment analogies, explain in two short sentences why containers share an inherent security vulnerability risk profile if an exploit successfully breaks or subverts the host operating system kernel layer.
