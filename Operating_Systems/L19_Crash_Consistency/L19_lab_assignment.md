# 🔬 LAB 19: Crash Consistency — Simulating Write-Ahead Log Recovery Life Cycles
## CS 301: Operating Systems & Systems Architecture

---

### 🎯 1. Core Objective
In this lab, you will manually simulate a file system recovery subsystem. You will trace the step-by-step transaction transitions of a Write-Ahead Logging (WAL) journal pipeline and evaluate structural disk states to determine whether to replay or discard logs after a sudden power loss.

### 🛑 2. Prerequisites
- Completion of Lab 18 inode capacity tree calculations.
- Thorough structural understanding of file metadata components (bitmaps, inodes) and atomic operations.

### 🎪 3. The Pedagogical Hook: Replaying the Timeline
Imagine appending a critical line of financial data to a master ledger database. Under the hood, this single write forces the operating system to modify three completely separate disk blocks: the data bitmap, the parent inode metadata, and the raw sector cells. If an unexpected power outage cuts out mid-sequence, your filesystem is caught half-updated—spawning broken memory leaks or ghost indexing tags. Journaling bypasses this disaster by writing a clean blueprint of intent first. In this lab, you will step inside the reboot recovery scanner to trace this timeline and restore system consistency.

---

### 🔍 4. System Core Breakdown
- **The Journal Write-Ahead Pipeline:** The structural sequence where an update's data blocks are committed to an isolated log buffer area before any changes hit the primary file system structures.
- **The Checkpoint Routine:** The asynchronous recovery step where the file system engine reads sealed, verified log entries from the journal ring buffer and writes them permanently into main storage blocks.

---

### 🛠️ 5. Practical Lab Exercise: Auditing Power Loss Recovery Scenarios

Follow these precise structural steps to evaluate the integrity of a journaled file system trace:

#### Step 1: Establish the Multi-Block Update Sequence
A process is appending data to a file block. The transaction requires updating three primary storage structures:
- **Block `[I]`:** Inode file sizing metric and direct pointer array entry.
- **Block `[B]`:** Data allocation tracking bitmap index flag.
- **Block `[D]`:** The literal data text payload contents.

#### Step 2: Trace Crash Scenario 1 (Pre-Commit Loss)
The file system driver prepares the journal ring buffer. It writes block references `[I, B, D]` to the journal tracks. Suddenly, a total power loss occurs before the terminal `[TX Commit]` block can be written to disk.
1. The system boots back online. The recovery scanner inspects the journal track and discovers a un-sealed transaction missing its commit signature.
2. Identify the recovery action the scanner must execute on this log entry: **[Replay and Commit] OR [Discard and Rollback]**?
   - *Your Answer:* __________________
3. State whether the primary file system blocks on disk were corrupted or left in an inconsistent state by this crash.
   - *Your Answer:* __________________

#### Step 3: Trace Crash Scenario 2 (Mid-Checkpoint Loss)
A separate write transaction begins. The system successfully writes `[Journal Start]`, the layout updates for `[I, B, D]`, and the matching terminal `[TX Commit]` block to the journal log track. Next, the file system enters the **Checkpointing Phase**. It successfully writes blocks `[B]` and `[D]` to the main storage blocks, but power cuts out completely *before* block `[I]` can be written to the main filesystem matrix.
1. The system reboots. The recovery scanner reads the journal track and finds a transaction block completely sealed with a valid `[TX Commit]` signature.
2. Identify the recovery action the scanner must execute to resolve this half-written checkpoint state: **[Replay and Commit] OR [Discard and Rollback]**?
   - *Your Answer:* __________________
3. Briefly explain in one sentence how the recovery scanner uses the completed journal log entry to restore absolute crash consistency across the disk substrate.
   - *Your Answer:* __________________

---

### 🏷️ 6. Architectural Lexicon / Terms
- **Crash Consistency:** The capability of a storage system to restore structured data boundaries cleanly and accurately following an ungraceful crash or power disruption.
- **Metadata Journaling:** An optimized performance profile that writes only layout structural changes (inodes, bitmaps) to the log ring buffer while streaming heavy file payload bytes straight to data blocks.

---

### 🎯 7. Lab Deliverable Submission Checklist
To receive full credit for Lab 19, paste your data answers inside a clean file and submit it to your course folder:
1. Provide your completed recovery actions and consistency determinations for Step 2 (Scenario 1).
2. Provide your completed recovery action and structural explanation for Step 3 (Scenario 2).
3. Based on our paper pencil ledger analogies, explain in two short sentences why writing changes to a journal log *before* writing to primary disk structures introduces an operational performance trade-off compared to non-journaled storage engines.
