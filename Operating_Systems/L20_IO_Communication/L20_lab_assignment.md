# 🔬 LAB 20: Peripheral Architectures — Auditing Polling, Interrupts, and DMA
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will evaluate discrete peripheral hardware profiles and sort data transmission workloads. You will mathematically model CPU cycle efficiency across Polling loops, evaluate Interrupt Service Routine (ISR) context-switching overheads, and design Direct Memory Access (DMA) offloading pipelines.

### 🛑 2. Prerequisites
- Completion of Lab 19 write-ahead log sequencing and crash consistency traces.
- Thorough procedural understanding of the Interrupt Vector Table (IVT), processor privilege boundaries, and system buses.

### 🎪 3. The Pedagogical Hook: Stopping the Interrupt Storm
Every time a peripheral device needs to send data to the CPU, it forces the system to select an interface strategy. If you configure a high-speed device like a modern network card to throw an asynchronous electronic interrupt signal wire change for every single arriving byte, you will plunge the processor into a catastrophic scenario known as an Interrupt Storm. The CPU spends 100% of its available clock cycles saving register registers and switching contexts, completely freezing out user application threads. In this lab, you will audit these communication strategies to prevent system-level paralysis.

---

### 🔍 4. System Core Breakdown
- **Polling Loop Inefficiencies:** The processing bottleneck that occurs when the CPU is trapped in a synchronous spinlock while reading a hardware status bit, consuming 100% core utilization while waiting for a slow peripheral.
- **DMA Offloading Primitives:** The hardware communication layout that completely bypasses the CPU by mapping high-density block transfers directly onto the system data bus lines using an external bus-master controller.

---

### 🛠️ 5. Practical Lab Exercise: Profiling the I/O Interface Matrix

Follow these precise structural evaluation steps to sort and optimize your hardware system interfaces:

#### Step 1: Profile the Arrival Metrics of a High-Speed Device
Imagine an embedded automated system layout featuring a high-speed imaging sensor streaming raw inspection frames across an input register lane under these parameters:
- **Data Streaming Payload Rate:** `2,000,000 Bytes per second` (2 MB/s).
- **Individual Hardware Transfer Packet Block Size:** `1 Byte` per electronic wire signal.
- **CPU Context Switch Overhead Tax:** It costs the processor exactly `1 microsecond (1µs)` to handle an interrupt, save register states, swap stacks, and return to thread execution lines.

#### Step 2: Calculate Unaccelerated Interrupt Saturation
Analyze the system outcome if this imaging sensor is wired to trigger a standard hardware interrupt for every single packet byte that arrives:
1. **Calculate Interrupts Per Second:** Since 2,000,000 bytes arrive per second and each byte throws an interrupt, the hardware fires exactly `2,000,000 interrupts per second`.
2. **Calculate Total CPU Overhead Time:** Multiply the total interrupts by individual context switch cost:  
   `2,000,000 interrupts * 0.000001 seconds (1µs) = _______ seconds.`
3. **Determine the Processor State:** Based on your calculation, explain why the CPU is thrown into an unrecoverable "Interrupt Storm" that completely freezes the operating system workspace.

#### Step 3: Architect a Direct Memory Access (DMA) Mitigation Blueprint
Refactor the system layout to introduce a specialized Direct Memory Access (DMA) controller chip module to intercept the high-speed data stream.
1. The CPU tells the DMA controller the starting physical destination RAM address frame and a target block counter size limit of exactly `64,000 Bytes` (64 KB buffer).
2. The sensor streams bytes into the FTL cache. The DMA controller claims the system bus master lines and shifts bytes directly into RAM blocks without involving the CPU.
3. Compute exactly how many hardware interrupts hit the primary CPU processor core during a full 2,000,000-byte data stream under this refactored 64 KB block mapping setup:  
   `Total Arriving Interrupts = 2,000,000 Bytes / 64,000 Bytes per block = _______ Interrupts.`

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Interrupt Service Routine (ISR):** The low-level kernel code function bound to a specific hardware vector that executes inside Ring 0 to ingest and clear peripheral register data.
- **Bus Master:** A hardware component (like a DMA controller) that has been granted permission by system circuitry to drive address lines and orchestrate memory cycles independently of the central processor.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 20, paste your engineering calculations inside a clean file and submit it to your course folder:
1. Provide your completed CPU overhead calculation total and your processor state evaluation from Step 2.
2. Provide your final refactored total arriving interrupt value derived inside Step 3.
3. Based on our mailbox and doorbell analogies, explain in two short sentences why polling can be an optimal interface strategy for low-speed devices, despite being highly inefficient for high-frequency streams.
