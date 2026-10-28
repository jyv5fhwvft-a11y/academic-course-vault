# 🔬 LAB 21: Driver Abstractions — Mapping Polymorphic VFS File Operations
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will analytically simulate a Unix-like Virtual File System (VFS) driver mounting workflow. You will categorize hardware components into Block, Character, or Network device classes and track step-by-step how a user-space file command maps polymorphically onto hardware-specific register routines.

### 🛑 2. Prerequisites
- Completion of Lab 20 polling, interrupt, and DMA communication calculations.
- Thorough procedural understanding of the UNIX file abstraction model and path resolution passes.

### 🎪 3. The Pedagogical Hook: The Universal Wall Adapter
When you plug an appliance into a wall outlet, the power grid does not know or care whether you are running a toaster, a lamp, or a complex gaming system. It exposes a simple, uniform interface slots layout that delivers voltage identically. The Virtual File System plays the exact same trick on software. To your running user programs, a hard drive, a keyboard, and a serial terminal all look like simple file containers that handle basic commands like `open()`, `read()`, and `write()`. In this lab, you will step inside the kernel registry to see how a simple jump table translates these generic calls into a language your circuit boards understand.

---

### 🔍 4. System Core Breakdown
- **Polymorphic Device Mapping:** The design paradigm where diverse physical components override an abstract kernel file operations structure, binding uniform standard user APIs straight onto unique low-level driver functions.
- **The /dev File Abstraction Firewall:** The system architecture configuration that registers real hardware device controllers as entry nodes within the file system tree namespace, extending security bit filters to physical chips.

---

### 🛠️ 5. Practical Lab Exercise: Auditing the Kernel Driver Table

Follow these precise sequential execution steps to profile your polymorphic device driver registry:

#### Step 1: Categorize the Peripheral Hardware Universe
Examine the following list of computer hardware items and classify each into its correct architectural driver classification: **[Block Device]**, **[Character Device]**, or **[Network Device]**:
1. **Peripheral A:** A high-speed NVMe Solid-State Drive (SSD) that handles random-access data requests.
   - *Your Classification:* __________________
2. **Peripheral B:** A serial desktop trackball mouse that transmits continuous coordinate streams sequentially.
   - *Your Classification:* __________________
3. **Peripheral C:** An onboard Wi-Fi chip processing streaming packet frames through socket buffers.
   - *Your Classification:* __________________
4. **Peripheral D:** A hardware security matrix keyboard logging intermittent text key codes.
   - *Your Classification:* __________________

#### Step 2: Trace the VFS `file_operations` Function Pointer Jump Map
An engineering task calls the system statement `write(fd, buffer, 100)` over a mounted device node file path registered at `/dev/custom_led`. Trace how this macro call routes through the kernel sub-structures:
1. **Routing Phase A:** The kernel intercepts the file descriptor `fd` session token and looks up its major/minor device identification bits inside the process file table rows.
2. **Routing Phase B:** The virtual file system identifies the object as an active character device file node and matches it to its registered entry struct: **`struct file_operations custom_led_fops`**.
3. **Routing Phase C:** Look at the following driver code registry array. Identify the precise name of the custom backend C function invoked when this user-space write occurs:
```c
static const struct file_operations custom_led_fops = {
    .owner   = THIS_MODULE,
    .open    = hardware_led_init,
    .write   = physical_led_toggle_hardware_loop,
    .release = hardware_led_close,
};
```
   - *Your Extracted Function Name:* __________________

---

### 🏷️ 6. Architectural Lexicon / Terms
- **file_operations Struct:** A critical kernel data registry table composed of function pointers that routes standard file API actions straight to hardware-specific driver subroutines.
- **Major Number:** A file system metadata marker assigned to a `/dev` node file that identifies the specific device driver module responsible for managing that peripheral item.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 21, paste your structural parameters inside a clean file and submit it to your course folder:
1. Provide your completed architectural classifications for Peripherals A, B, C, and D inside Step 1.
2. Provide your extracted backend driver function name identified inside Step 2.
3. Based on our universal wall power adapters analogies, explain in two short sentences how representing physical hardware items as simple files inside the `/dev` folder improves operating system security filters.
