# Week 6 — Operating Systems

**Syllabus §8:** System calls, processes, threads, inter-process communication, concurrency and synchronization. Deadlock. CPU and I/O scheduling. Memory management and virtual memory. File systems.
**Estimated marks: ~11 — heavily numerical**

---

## 1. Fundamentals

### 1.1 Functions of an OS
Process management · memory management · file management · device/IO management · security & protection · resource allocation · accounting. It acts as a **resource manager** and provides an **abstraction** over hardware.

### 1.2 OS types

| Type | Characteristic |
|---|---|
| **Batch** | Jobs grouped, no user interaction |
| **Multiprogramming** | Several jobs in memory; CPU switches when one blocks — maximises **CPU utilisation** |
| **Multitasking / time-sharing** | Rapid switching gives each user quick response — minimises **response time** |
| **Multiprocessing** | Multiple CPUs |
| ⭐ **Real-time** | **Hard RTOS** — deadlines must never be missed; **Soft RTOS** — deadlines preferred |
| **Distributed** | Independent machines appear as one system |
| **Network** | Shared resources over a network |
| **Embedded** | Dedicated function, resource constrained |

### 1.3 ⭐ Kernel mode vs user mode
- **User mode:** restricted; cannot execute privileged instructions or access hardware directly.
- **Kernel mode:** full privileges.
- ⭐ A **mode switch** happens on a system call, interrupt or trap. A **mode switch is not a context switch** — the process does not change.

**Kernel architectures:** monolithic (all services in the kernel — fast, hard to maintain) · **microkernel** (minimal kernel, services in user space — reliable, more message-passing overhead) · hybrid · exokernel.

### 1.4 ⭐ System calls

The programmatic interface to OS services; the only way user code enters kernel mode.

| Category | Examples |
|---|---|
| **Process control** | ⭐ `fork()`, `exec()`, `wait()`, `exit()`, `abort()` |
| **File management** | `open()`, `read()`, `write()`, `close()`, `lseek()` |
| **Device management** | `ioctl()`, `read()`, `write()` |
| **Information** | `getpid()`, `alarm()`, `time()` |
| **Communication** | `pipe()`, `shmget()`, `mmap()`, `send()`, `recv()` |
| **Protection** | `chmod()`, `umask()`, `chown()` |

⭐ **`fork()` returns 0 to the child, the child's PID to the parent, and −1 on failure.** This asymmetry is how the two branches distinguish themselves.

🔢 `fork(); fork(); fork();` creates **2³ − 1 = 7** child processes (8 total processes).
📌 **n consecutive `fork()` calls → 2ⁿ total processes, 2ⁿ − 1 children.**

⚠ `exec()` **replaces** the current process image — it does not create a new process, and on success it never returns.

---

## 2. ⭐ Processes and threads

### 2.1 Process states ⭐

```
      admitted           dispatch            exit
NEW ───────────► READY ───────────► RUNNING ───────► TERMINATED
                   ▲   ◄───────────┘  │
                   │   preemption /   │ I/O or event wait
                   │   quantum expiry │
                   └──── WAITING ◄────┘
                       I/O complete
```

⭐ Two transitions are constantly confused:

| Transition | Cause |
|---|---|
| ⭐ **Running → Ready** | ⭐ **Preemption** (time-quantum expiry, or a higher-priority process arrives) |
| ⭐ **Running → Waiting/Blocked** | ⭐ **I/O request** or waiting for an event |
| Waiting → Ready | I/O completion |
| Running → Terminated | `exit()` |

### 2.2 Process Control Block (PCB)
Holds: process ID · state · program counter · CPU registers · scheduling info (priority) · memory-management info (page tables, base/limit) · accounting info · I/O status and open-file table.

### 2.3 Special processes ⭐

| Term | Meaning |
|---|---|
| ⭐ **Zombie** | Has **terminated** but the parent has not yet called `wait()` — its PCB entry lingers to hold the exit status |
| ⭐ **Orphan** | Still **running**, but its **parent has died** — re-parented to `init`/`systemd` |
| **Daemon** | Background service process |

⚠ Zombie = dead child, live parent. Orphan = live child, dead parent.

### 2.4 ⭐ Threads

A thread is a lightweight unit of execution within a process.

| ⭐ **Shared between threads of a process** | ⭐ **Private to each thread** |
|---|---|
| Code section | ⭐ **Stack** |
| Data section (globals) | ⭐ **Registers & program counter** |
| Heap | Thread ID |
| Open files, signals | Thread-local storage |

⭐ This table is the most-asked thread question. Each thread has its **own stack and registers**; everything else is shared.

| | **Process** | **Thread** |
|---|---|---|
| Address space | Own | Shared with peers |
| Creation cost | High | Low |
| Context switch cost | High | Low |
| Communication | IPC needed (kernel) | Shared memory (direct) |
| Isolation/fault tolerance | One crash does not kill others | One crash can kill the process |

**Thread models:** user-level (fast, but a blocking call blocks all threads; no multi-core parallelism) vs kernel-level (slower switching, true parallelism).
**Multithreading models:** many-to-one · one-to-one · many-to-many.

### 2.5 Context switch
Save the current process's state into its PCB, load the next process's state. **Pure overhead** — no useful work done. Cost includes register saves, TLB flush and cache pollution.

---

## 3. ⭐⭐ CPU scheduling

### 3.1 Terminology ⭐

📌 **Arrival Time (AT)** — when the process enters the ready queue
📌 **Burst Time (BT)** — required CPU time
📌 **Completion Time (CT)** — when the process finishes
📌 ⭐ **Turnaround Time (TAT) = CT − AT**
📌 ⭐ **Waiting Time (WT) = TAT − BT**
📌 **Response Time = first CPU allocation − AT**

**Goals:** maximise CPU utilisation and throughput; minimise turnaround, waiting and response times.

### 3.2 ⭐ Algorithms

| Algorithm | Preemptive? | Selects | Pros | Cons |
|---|---|---|---|---|
| ⭐ **FCFS** | ❌ Non-preemptive | Earliest arrival | Simple, fair, no starvation | ⭐ **Convoy effect**; poor average WT |
| ⭐ **SJF** | ❌ Non-preemptive | Shortest burst | ⭐ **Optimal average WT** | Burst time unknown; **starves long jobs** |
| ⭐ **SRTF** | ✅ Preemptive | Shortest remaining | Optimal among preemptive | Starvation; high switching overhead |
| **Priority** | Both variants | Highest priority | Flexible | ⭐ **Starvation** — fixed by **aging** |
| ⭐ **Round Robin** | ✅ Preemptive | Next in queue, fixed quantum | ⭐ Good **response time**, no starvation | Higher average TAT; overhead if quantum too small |
| **Multilevel queue** | ✅ | Fixed queues by class | Separates job types | Inflexible |
| **Multilevel feedback queue** | ✅ | Queues with promotion/demotion | Adaptive, general purpose | Complex tuning |
| **HRRN** | ❌ | Highest response ratio (1 + WT/BT) | Balances short and long jobs | Needs burst estimates |

⭐ **SJF gives the provably minimum average waiting time** for a set of processes available simultaneously.
⭐ **Round Robin with a very large quantum degenerates to FCFS**; with a very small quantum, context-switch overhead dominates.
⭐ **Starvation-free:** FCFS, Round Robin. **Starvation-prone:** SJF, SRTF, priority (fixed by **aging** — gradually raising the priority of waiting processes).

### 3.3 🔢 Worked examples

**FCFS**, all arriving at t = 0 in order P1(24), P2(3), P3(3):
| Process | BT | CT | TAT | WT |
|---|---|---|---|---|
| P1 | 24 | 24 | 24 | 0 |
| P2 | 3 | 27 | 27 | 24 |
| P3 | 3 | 30 | 30 | 27 |

Average WT = (0 + 24 + 27)/3 = **17 ms** · Average TAT = 81/3 = **27 ms**
⭐ This is the **convoy effect**: had the short jobs run first (SJF), average WT would be (0+3+6)/3 = 3 ms.

**Round Robin**, quantum = 4, P1(24), P2(3), P3(3) all at t = 0:
Gantt: P1(0–4) P2(4–7) P3(7–10) P1(10–30)
| Process | CT | TAT | WT |
|---|---|---|---|
| P1 | 30 | 30 | 6 |
| P2 | 7 | 7 | 4 |
| P3 | 10 | 10 | 7 |

Average WT = 17/3 ≈ **5.67 ms** — much better response than FCFS.

⚠ **Method for exams:** always draw the Gantt chart, then read off CT, compute TAT = CT − AT, then WT = TAT − BT. Do not try to shortcut it.

### 3.4 I/O scheduling
CPU-bound vs I/O-bound processes. A good mix keeps both the CPU and devices busy. **CPU burst / I/O burst cycle** alternation is the basis of scheduling heuristics.

---

## 4. ⭐ Inter-process communication (IPC)

| Mechanism | Description |
|---|---|
| ⭐ **Shared memory** | Processes map a common region. **Fastest** (no kernel involvement after setup), but the programmer must synchronise. |
| ⭐ **Message passing** | `send()`/`receive()` through the kernel. Slower, but no explicit synchronisation needed and works across machines. |
| **Pipes** | Unidirectional byte stream between related processes (`|` in shells). **Named pipes (FIFOs)** work between unrelated processes. |
| **Sockets** | Network-capable, bidirectional |
| **Signals** | Asynchronous notifications (SIGKILL, SIGTERM, SIGINT) |
| **Message queues, semaphores** | System V / POSIX IPC objects |

Message passing can be **blocking (synchronous)** or **non-blocking (asynchronous)**, with **direct** or **indirect (mailbox)** addressing.

---

## 5. ⭐⭐ Concurrency and synchronization

### 5.1 The critical-section problem

A **race condition** occurs when the outcome depends on the interleaving of concurrent accesses to shared data.

⭐ **Three requirements for a correct solution:**
1. ⭐ **Mutual exclusion** — at most one process in the critical section at a time.
2. ⭐ **Progress** — if no process is in the CS, a waiting process must be able to enter (no unnecessary blocking).
3. ⭐ **Bounded waiting** — a bound exists on how many others may enter before a waiting process does (no starvation).

⚠ These three are frequently confused with the ACID properties from DBMS. Memorise both lists.

### 5.2 Software solutions
- **Strict alternation (turn variable):** mutual exclusion ✅, progress ❌.
- **Flag-only:** can deadlock.
- ⭐ **Peterson's solution** (two processes, using `flag[]` + `turn`): satisfies **all three** requirements. Relies on atomic loads/stores and no instruction reordering.
- **Bakery algorithm** (Lamport): n processes.

### 5.3 Hardware support
**Test-and-Set**, **Compare-and-Swap**, **Swap/Exchange** — atomic instructions. A **spinlock** built on these busy-waits: efficient only when critical sections are very short.
⚠ Disabling interrupts works only on uniprocessors.

### 5.4 ⭐ Semaphores

An integer variable accessed only through two atomic operations:
```
wait(S) / P(S):   while (S <= 0) ; S--;
signal(S) / V(S): S++;
```

| Type | Range | Use |
|---|---|---|
| ⭐ **Binary semaphore** | 0 or 1 | Mutual exclusion (like a mutex) |
| ⭐ **Counting semaphore** | 0…n | ⭐ Controls access to **n identical resources** |

⭐ A counting semaphore initialised to **n** allows **n** processes into the critical section simultaneously.

⚠ **Semaphore vs mutex:** a mutex has **ownership** (only the locking thread may unlock it); a semaphore does not and may be signalled by any process.

**Monitor:** a high-level construct bundling shared data with procedures, guaranteeing that only one process executes inside at a time; uses **condition variables** with `wait()` and `signal()`.

### 5.5 ⭐ Classical synchronization problems

**(a) Producer–Consumer (bounded buffer)**
Three semaphores: `mutex = 1`, `empty = n`, `full = 0`.
```
Producer:  wait(empty); wait(mutex); add item; signal(mutex); signal(full);
Consumer:  wait(full);  wait(mutex); take item; signal(mutex); signal(empty);
```
⚠ Reversing `wait(mutex)` and `wait(empty)` causes **deadlock**.

**(b) Readers–Writers**
Many readers may read concurrently; a writer needs exclusive access.
- First variant (reader priority) → writers can starve.
- Second variant (writer priority) → readers can starve.
- Third variant → no starvation.

**(c) Dining Philosophers**
5 philosophers, 5 forks; each needs two adjacent forks.
Deadlock if all pick up their left fork simultaneously.
⭐ **Solutions:** allow at most 4 to sit; pick up both forks only if both are free (atomically); **asymmetric** solution — odd philosophers take left first, even take right first.

**(d) Sleeping Barber** — bounded waiting-room coordination.

---

## 6. ⭐⭐ Deadlock

### 6.1 ⭐ Four necessary conditions (all must hold simultaneously)

1. ⭐ **Mutual exclusion** — at least one resource is non-shareable.
2. ⭐ **Hold and wait** — a process holds a resource while waiting for another.
3. ⭐ **No preemption** — resources cannot be forcibly taken away.
4. ⭐ **Circular wait** — a cycle of processes each waiting for the next.

⚠ The third condition is **"no preemption"** — options that say "preemption" are stating the opposite. This is the most common trap in this topic.

### 6.2 Resource Allocation Graph (RAG)
Processes (circles) and resources (rectangles); request edges P→R, assignment edges R→P.
- ⭐ With **single instances** of each resource: **a cycle ⟺ deadlock**.
- ⭐ With **multiple instances**: a cycle is **necessary but not sufficient** — it may be a false alarm.

### 6.3 ⭐ Four handling strategies

| Strategy | Approach |
|---|---|
| ⭐ **Prevention** | Structurally negate one of the four conditions (e.g. request all resources at once → no hold-and-wait; impose a total ordering on resource types → no circular wait) |
| ⭐ **Avoidance** | Grant a request only if the system stays in a **safe state** → ⭐ **Banker's algorithm** |
| **Detection** | Allow deadlock, detect it with a **wait-for graph** or the detection algorithm, then recover |
| **Recovery** | Terminate processes, or **preempt/rollback** resources (needs checkpointing); victim selection by cost |
| **Ignore** | The **ostrich algorithm** — what most general-purpose OSs actually do |

⚠ **Prevention vs avoidance:** prevention makes a condition impossible in advance; **avoidance** decides dynamically per request. Banker's algorithm is **avoidance**.

### 6.4 ⭐ Banker's algorithm

Data structures: **Available[m]**, **Max[n][m]**, **Allocation[n][m]**, and
📌 **Need[i][j] = Max[i][j] − Allocation[i][j]**

**Safety algorithm:** repeatedly find a process whose `Need ≤ Available`; pretend it finishes and add its `Allocation` back to `Available`; if all processes can be sequenced this way, the state is **safe** and the sequence is a **safe sequence**.

🔢 3 resource types A, B, C with Available = (3, 3, 2):

| P | Allocation | Max | Need |
|---|---|---|---|
| P0 | 0 1 0 | 7 5 3 | 7 4 3 |
| P1 | 2 0 0 | 3 2 2 | 1 2 2 |
| P2 | 3 0 2 | 9 0 2 | 6 0 0 |
| P3 | 2 1 1 | 2 2 2 | 0 1 1 |
| P4 | 0 0 2 | 4 3 3 | 4 3 1 |

Work = (3,3,2). P1's Need (1,2,2) ≤ Work → run P1, Work = (5,3,2). P3 (0,1,1) ≤ Work → Work = (7,4,3). P4 (4,3,1) ≤ Work → Work = (7,4,5). P0 (7,4,3) ≤ Work → Work = (7,5,5). P2 → Work = (10,5,7).
⭐ **Safe sequence: P1 → P3 → P4 → P0 → P2.** The state is safe.

⭐ **Safe state ⇒ no deadlock. Unsafe state ⇒ deadlock is *possible*, not certain.**

---

## 7. ⭐⭐ Memory management

### 7.1 Contiguous allocation

| Strategy | Rule |
|---|---|
| **First fit** | First hole large enough — fastest |
| **Best fit** | Smallest hole large enough — leaves tiny useless fragments |
| **Worst fit** | Largest hole — generally worst performer |
| **Next fit** | First fit starting where the last search stopped |

### 7.2 ⭐ Fragmentation

| Type | Cause | Where |
|---|---|---|
| ⭐ **Internal** | Allocated block is larger than requested; the leftover is inside the block | ⭐ **Paging** (fixed-size frames) |
| ⭐ **External** | Free memory exists but is split into non-contiguous holes | ⭐ **Segmentation**, contiguous allocation |

⭐ **Paging → internal fragmentation. Segmentation → external fragmentation.** Memorise this pairing.
**Compaction** cures external fragmentation but requires relocatable code and is expensive.

### 7.3 ⭐⭐ Paging

Logical memory is divided into fixed-size **pages**; physical memory into equal-size **frames**. A **page table** maps page numbers to frame numbers.

Logical address = **page number (p) | page offset (d)**
📌 **Offset bits = log₂(page size)**
📌 **Number of pages = virtual address space / page size**
📌 **Page table size = number of pages × page table entry size**

🔢 32-bit virtual address, 4 KB pages, 4-byte PTE:
Pages = 2³²/2¹² = **2²⁰**. Page table size = 2²⁰ × 4 = **4 MB per process**.
⭐ This impracticality is exactly why **multi-level page tables**, **inverted page tables** and **hashed page tables** exist.

🔢 Two-level paging, 32-bit address, 4 KB pages, 1024 entries per table:
offset = 12 bits; remaining 20 bits split 10 (outer) + 10 (inner).

**Page table entry fields:** frame number · valid/invalid bit · protection (read/write/execute) bits · **dirty (modified) bit** · reference bit · caching-disabled bit.

⭐ **TLB (Translation Lookaside Buffer):** a small, fast, fully-associative cache of page-table entries.

📌 ⭐ **Effective Access Time (EAT) with a TLB:**
**EAT = h × (t_TLB + t_mem) + (1 − h) × (t_TLB + 2·t_mem)** — single-level page table

🔢 TLB access 20 ns, memory access 100 ns, hit ratio 80%:
EAT = 0.8 × (20 + 100) + 0.2 × (20 + 200) = 96 + 44 = **140 ns**
⚠ Some textbooks omit the TLB time on a miss, or assume the TLB is searched in parallel. **Read the question's stated model.**

### 7.4 Segmentation
Variable-size, logically meaningful units (code, data, stack). Address = **segment number | offset**; the **segment table** holds base and limit per segment. Supports protection and sharing naturally; suffers **external** fragmentation.

**Segmented paging** combines both: segments are paged, removing external fragmentation while keeping logical structure.

### 7.5 ⭐⭐ Virtual memory

Lets a process's logical address space exceed physical memory, using disk as backing store. Implemented with **demand paging** — pages are loaded only when referenced.

⭐ **Page fault:** a reference to a page whose valid bit is 0.
**Handling:** trap to OS → verify the reference is legal → find a free frame (or run replacement) → schedule the disk read → update the page table → restart the faulting instruction.

📌 **Effective access time with page faults = (1 − p) × t_mem + p × t_page-fault-service**
🔢 t_mem = 100 ns, page fault service = 8 ms, p = 0.001:
EAT = 0.999 × 100 + 0.001 × 8,000,000 = 99.9 + 8000 ≈ **8100 ns** — a 0.1% fault rate slows the system 81×. This is why fault rates must be tiny.

### 7.6 ⭐⭐ Page replacement algorithms

| Algorithm | Rule | ⭐ Belady's anomaly? |
|---|---|---|
| ⭐ **FIFO** | Evict the oldest page | ⭐ **✅ YES** |
| ⭐ **Optimal (OPT/MIN)** | Evict the page used **furthest in the future** | ❌ No |
| ⭐ **LRU** | Evict the **least recently used** | ❌ No |
| **LFU / MFU** | Least / most frequently used | Possible |
| **Clock / Second chance** | FIFO + reference bit | Approximates LRU |

⭐ **Belady's anomaly:** *more frames producing more page faults.* Occurs in **FIFO**. LRU and OPT are **stack algorithms** and are provably immune.

⭐ **OPT is unimplementable** — it needs knowledge of future references. It exists only as a benchmark.

🔢 **Reference string 1,2,3,4,1,2,5,1,2,3,4,5 with 3 frames:**

| Algorithm | Page faults |
|---|---|
| FIFO | **9** |
| LRU | **10** |
| OPT | **7** |

With **4 frames**, FIFO gives **10** faults — *more frames, more faults*: ⭐ **Belady's anomaly demonstrated.**

⚠ Note that here LRU is *worse* than FIFO — LRU is usually better but not always.

### 7.7 ⭐ Thrashing

The system spends more time paging than executing. Caused by too high a degree of multiprogramming: each process gets too few frames, faults constantly, and CPU utilisation collapses.

**Cures:**
- ⭐ **Working set model:** track the set of pages referenced in the last Δ references; give each process enough frames for its working set; suspend processes if the total demand exceeds available frames.
- **Page-Fault Frequency (PFF) control:** adjust frame allocation to keep the fault rate in a target band.
- Reduce the degree of multiprogramming; add memory.

**Frame allocation:** equal vs proportional; **local** replacement (a process replaces only its own frames) vs **global** (any frame).

---

## 8. ⭐ File systems

### 8.1 Concepts
**File attributes:** name, identifier, type, location, size, protection, timestamps.
**Operations:** create, open, read, write, seek, close, delete, truncate.
**Access methods:** sequential · direct/random · indexed.
**Directory structures:** single-level · two-level · tree · acyclic graph (shared subdirectories) · general graph.
**Links:** **hard link** (another directory entry pointing to the same inode; same file system) vs **soft/symbolic link** (a file containing a path; can cross file systems and can dangle).

### 8.2 ⭐ File allocation methods

| Method | Direct access | External fragmentation | Notes |
|---|---|---|---|
| **Contiguous** | ✅ Fast | ⭐ **✅ Suffers** | Simple; file growth is hard |
| **Linked** | ❌ Sequential only | ❌ None | Each block points to the next; a lost pointer loses the rest; FAT is a variant |
| ⭐ **Indexed** | ⭐ **✅ Yes** | ⭐ **❌ None** | An index block holds all block pointers — **best of both** |

⭐ **Indexed allocation** is the standard exam answer for "direct access without external fragmentation".

**UNIX inode:** contains attributes plus 12–15 pointers — direct blocks, then **single, double and triple indirect** blocks, allowing very large files.

🔢 With 10 direct pointers, one single-indirect, one double-indirect, 4 KB blocks and 4-byte pointers (1024 pointers/block):
max file size = (10 + 1024 + 1024²) × 4 KB ≈ **4 GB**.

**Free-space management:** bit vector/bitmap · linked list · grouping · counting.

### 8.3 ⭐ Disk scheduling

| Algorithm | Rule | Starvation | Notes |
|---|---|---|---|
| **FCFS** | Service in arrival order | ❌ No | Fair but poor seek performance |
| ⭐ **SSTF** | Nearest request first | ⭐ **✅ Yes** | Good throughput; far requests can wait forever |
| ⭐ **SCAN** | Sweep to one end servicing, then reverse | ❌ No | ⭐ The **elevator** algorithm |
| ⭐ **C-SCAN** | Sweep one way, then jump back without servicing | ❌ No | More **uniform** wait times |
| **LOOK / C-LOOK** | Like SCAN/C-SCAN but reverse at the **last request**, not the disk end | ❌ No | Less wasted movement |

🔢 Head at 53; queue 98, 183, 37, 122, 14, 124, 65, 67 (cylinders 0–199):
- **FCFS** total head movement = **640**
- **SSTF** = **236**
- **SCAN** (moving up) = **236** (up to 199, then down to 14)
- **C-SCAN** = **382** (includes the 199→0 jump)

⭐ **SSTF causes starvation; SCAN and C-SCAN bound the wait.**

**RAID levels (awareness):** 0 = striping (performance, no redundancy) · 1 = mirroring · 5 = striping with distributed parity (needs ≥3 disks, survives 1 failure) · 6 = double parity (survives 2) · 10 = mirrored stripes.

---

## 9. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| `fork()` returns | 0 to child, PID to parent |
| n forks → processes | 2ⁿ |
| Running → Ready | Preemption |
| Running → Waiting | I/O request |
| Zombie | Terminated, parent hasn't waited |
| Orphan | Parent died |
| Thread's own resources | Stack, registers, PC |
| Optimal average WT | SJF |
| RR with huge quantum | Becomes FCFS |
| Starvation-free | FCFS, Round Robin |
| Priority starvation fix | Aging |
| Critical-section requirements | Mutual exclusion, progress, bounded waiting |
| Peterson's solution | Satisfies all three |
| Counting semaphore init n | n processes allowed |
| Deadlock conditions | Mutual exclusion, hold-and-wait, **no** preemption, circular wait |
| Banker's algorithm | Deadlock **avoidance** |
| Cycle in RAG, single instance | Deadlock |
| Paging fragmentation | Internal |
| Segmentation fragmentation | External |
| Page table size (32-bit, 4KB, 4B PTE) | 4 MB |
| TLB | Cache of page-table entries |
| Belady's anomaly | FIFO |
| Unimplementable replacement | Optimal (OPT) |
| Thrashing cure | Working set model |
| Direct access, no external fragmentation | Indexed allocation |
| Elevator algorithm | SCAN |
| Disk scheduling with starvation | SSTF |

---

## 10. Common traps ⚠

1. **"No preemption"** is the deadlock condition, not "preemption".
2. **Running → Ready is preemption; Running → Waiting is I/O.**
3. **Belady's anomaly is FIFO-only** — LRU and OPT are immune.
4. **Paging = internal, segmentation = external** fragmentation.
5. **Banker's is avoidance, not prevention.**
6. **Safe state ⇒ no deadlock, but unsafe state does not guarantee deadlock.**
7. **Threads share the heap but not the stack.**
8. **Mode switch ≠ context switch.**
9. **`exec()` does not create a process** — it replaces the image.
10. **EAT formulas vary by model** — check whether the TLB is searched in parallel or in series, and whether TLB time is counted on a miss.
11. **Zombie vs orphan** — opposite situations.
12. **Semaphore ≠ mutex** — mutexes have ownership.
13. **A cycle with multiple resource instances is not sufficient** for deadlock.

---

## 11. Practice

- GATE: [`Paper2_S08_Operating_System/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S08_Operating_System/) — **343 questions**
- State-PSC level: [`Paper2_S08_Operating_System/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S08_Operating_System/) — **463 questions**
- Test: [`Week_06_Test.md`](../04_Mock_Tests/Week_06_Test.md)

**Priority order if short on time:** scheduling Gantt-chart numericals → page replacement traces (and Belady's anomaly) → deadlock's four conditions + Banker's algorithm → paging/page-table sizing + TLB EAT → synchronization requirements & classical problems → disk scheduling → file allocation.

⭐ **This is the most numerical section in the paper.** Practise Gantt charts, page-replacement traces and Banker's algorithm until they are mechanical — they are guaranteed marks if you can execute them quickly.
