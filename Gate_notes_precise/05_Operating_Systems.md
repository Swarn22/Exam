# 05 · Operating Systems — Precise Notes
> **TPSC ATO (IT) Paper-II §8** · ~11 marks (estimate) · Syllabus: *"Operating System — system calls, processes, threads, IPC, concurrency and synchronization; deadlock; CPU and I/O scheduling; memory management and virtual memory; file systems"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson, OSNotes, OpSys, Ace, ME-Delhi, ME-HW. Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/05_Operating_Systems/` — open them for diagrams.
> Short names → files: Pearson = `1.OS.pdf` · Sanchit = `2.…Sanchit…` · ME-Delhi = `3.…Delhi` · ME-CS = `4.Operating_System-CS` · Ace = `5.Ace…` · ME-HW = `6.…Made_Easy` · OSNotes = `7.OS_Notes` · OpSys = `8.Operation_Systems`. Page numbers = PDF page numbers, not printed ones.

## Which notes are worth your time
| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 1.OS.pdf (Pearson) | Pearson GATE guide, Unit 7 | Typed, 2-column | 96 | 4 | What Sanchit skips — partitions, buddy, paging, hierarchical/inverted tables, TLB, segmentation, monitors, message passing, directories, claim edges; year-tagged PYQs · dense, some garbled figures, few numericals |
| 2.OS_Sanchit_Sir_Notes.pdf | Sanchit Jain (Knowledge Gate) | Typed slides | 203 | 4.5 | Galvin-faithful theory + biggest tagged PYQ bank (GATE/NET/ISRO) on scheduling, sync, deadlock, replacement, disk, allocation · **no** chapter on contiguous allocation/paging/TLB/segmentation, no IPC, monitors only named, no directories; some wrong keys/typos (⚠ below) |
| 3.OS_Made_Easy_Class_Latest_Notes_Delhi.pdf | Made Easy Delhi class copy | Handwritten scan, clear | 172 | 3 | Whole syllabus incl. file system, paging formulas · ~⅓ is workbook-solution scratch ("Pg 96 Q22") useless without the workbook |
| 4.Operating_System-CS.pdf | Made Easy (raghul.org photocopy) | Handwritten photocopy, faint | 180 | 1.5 | A few disk-scheduling/EMAT pages · barely legible, duplicated page (p.80 = p.160), loose claims on Belady |
| 5.Ace_Academy_OS_Class_Notes.pdf | Ace Academy class notes (2010) | Handwritten scan, very neat | 163 | 3.5 | Precedence graphs, parbegin/parend, fork–join, optimal page size √(2se), disk transfer rate, FAT · class and workbook mixed, dated, no index |
| 6.OS_Hand_Written_Notes_Made_Easy.pdf | Made Easy class notes ("Cosmos", 2012) | Phone photos, many rotated | 139 | 2.5 | Priority inversion, segmented paging, disk numericals · awkward to read, overlaps file 3 |
| 7.OS_Notes.pdf | Unattributed GATE notes (2020) | Handwritten CamScanner, clean | 188 | 4 | Best memory numericals: page-table size, 3-level paging (GATE-2013), TLB EMAT, hashed/segmented paging, working set · stops at VM — no file systems or disk |
| 8.Operation_Systems.pdf | ekxam.com lecture notes | Handwritten, colour, neat | 99 | 3.5 | Step-by-step PYQ walk-throughs (GATE-2010/2013 semaphores, safe state, k-level TLB EAT, first/best fit) · ends at working set; equates binary semaphore with mutex |

**If you open only one PDF besides these notes**, open **Pearson (1.OS.pdf)**: it is typed, follows the syllabus line in five chapters, fills exactly Sanchit's gaps (memory management, IPC, directories) and has keyed PYQs. With one more hour, work the paging numericals in **OSNotes pp.110–165**.

## Topic map
| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | OS types, dual mode, system calls | ⭐⭐ | match OS type ↔ feature; which instruction is privileged; what causes user→kernel switch |
| 2 | Processes & threads | ⭐⭐⭐ | valid state transitions; fork() counting; what threads share; ULT vs KLT true/false |
| 3 | IPC | ⭐ | shared memory vs message passing; blocking/non-blocking; pipe properties |
| 4 | Concurrency & synchronization | ⭐⭐⭐ | does this entry/exit code give ME/progress? semaphore final value; fill-in P–C / R–W code |
| 5 | Deadlock | ⭐⭐⭐ | Coffman conditions; Banker's safe sequence; minimum resources; RAG cycle reasoning |
| 6 | CPU scheduling | ⭐⭐⭐ | Gantt chart → average WT/TAT; which algorithm starves; RR quantum effects |
| 7 | Memory management | ⭐⭐⭐ | address bits / page-table size; multilevel paging; TLB EAT; type of fragmentation |
| 8 | Virtual memory | ⭐⭐⭐ | page-fault count FIFO/LRU/OPT; Belady; EAT with faults; thrashing |
| 9 | File systems | ⭐⭐ | inode max file size; allocation-method comparison; bitmap size |
| 10 | Disk (I/O) scheduling | ⭐⭐ | total head movement; which algorithm is "elevator"/starves |

## 1. OS Basics, Dual Mode & System Calls

### 1.1 Types of OS
| Type | Key idea | ⭐ Tested fact |
|---|---|---|
| Batch | similar jobs grouped, run in sequence | no interaction; CPU idle during I/O |
| ⭐ Multiprogramming | many jobs in memory; switch when one waits | goal = **max CPU utilisation**; GATE-2002: in memory together + switch on wait + switch on exit |
| ⭐ Multitasking / time-sharing | multiprogramming + timer slices | goal = **min response time**; RR scheduler |
| Multiprocessing (tightly coupled) | ≥ 2 CPUs share memory, bus, clock | SMP (peers) vs asymmetric (master–slave); speed-up < N; graceful degradation |
| Distributed (loosely coupled) | own memory & clock per node, network | resource sharing, speed-up, reliability, communication |
| ⭐ Real-time | result **and** deadline | **Hard**: miss = failure (airbag, ABS); **Soft**: degraded quality (video) |

- ⭐ **Spooling** (Simultaneous Peripheral Operation On-Line): disk buffers I/O so one job's I/O overlaps another's computation; classic spooled device = **line printer shared by many jobs** (GATE-1996, GATE-1998); the spooler builds the job queue (NET-Dec-2006). [Src: Sanchit p.8]
- ⚠ Multiprogramming (one CPU interleaves) ≠ multiprocessing (many CPUs, true parallelism); in both, and in multitasking, ready processes must be in RAM (NET-Dec-2008).

### 1.2 Dual mode, interrupts, traps
- Hardware **mode bit**: kernel = 0, user = 1. Boot starts in kernel mode; user programs run in user mode. [Src: Sanchit p.184]
- ⭐ User → kernel switch happens only on: **system call (trap instruction), hardware interrupt, exception** (divide-by-zero, illegal access, page fault).
- **Privileged**: I/O instructions, set timer, disable interrupts, load base/limit or page-table registers, clear memory, switch to kernel mode, halt. **Not privileged**: read the clock, issue a trap/system-call instruction.
- Interrupt = asynchronous, from hardware; trap = synchronous, from software (error or system call). The timer interrupt stops a user program hogging the CPU.
- ⚠ **Mode switch ≠ context switch**: a mode switch changes privilege of the same process; a context switch changes the process. ⭐ t(mode switch) < t(context switch) (GATE-2011, NET-June-2013).

### 1.3 System calls
- Programmatic interface to OS services, usually reached through an API (POSIX, Win32, Java) that traps via a numbered system-call table; `printf()` ends in the `write()` system call [Src: ME-Delhi p.1]. Parameters go in registers, a memory block (address in a register) or the stack.

- 📌 Six categories (UNIX examples): **process control** `fork exec exit wait` · **file** `open read write close` · **device** `ioctl read write` · **information** `getpid alarm sleep` · **communication** `pipe shm_open mmap` · **protection** `chmod umask chown`.

### 1.4 OS structure
- Monolithic (MS-DOS, UNIX/Linux + loadable modules): fast, one bug can crash all. Layered: layer 0 = hardware … N = UI, each uses only lower layers.
- ⭐ **Microkernel** (Mach): only IPC + minimal scheduling/memory in the kernel; services run in user space via message passing → reliable and extensible, but slower. Windows/macOS are hybrids.

🎯 **How it's asked:** match spooling/multiprogramming/time-sharing/distributed to their descriptions (NET-June-2015); "which must be privileged?"; t1 (mode switch) vs t2 (process switch) (GATE-2011).

## 2. Processes & Threads

### 2.1 Process, PCB, states
- Program = **passive** (executable on disk); process = **active** (program in execution with PC, registers, resources). Two processes of one program have the same text section but separate data, heap, stack (ISRO-2009).
- Process image: **text** (code) · **data** (globals) · **heap** (dynamic) · **stack** (parameters, return addresses, locals). ⚠ A child's PID is not on the stack.
- **PCB** (task control block): state, PC, CPU registers, scheduling info (priority, queue pointers), memory-management info (base/limit, page/segment tables), accounting, I/O status (open files, devices). [Src: Sanchit p.19]

- 5 states: New →(admit) Ready ⭐→(**dispatch**) Running →(timer/preemption) Ready; Running →(I/O or event wait; ISRO-2013) Waiting →(completion) Ready; Running →(exit) Terminated. ⚠ No Waiting → Running, no Ready → Waiting. [Src: Sanchit p.20–22] for the diagrams of GATE-1996/2006/2009.
- ⭐ A diagram with a Running → Ready edge means **preemptive** scheduling.
- Suspend states (7-state model): Ready-Suspend, Blocked-Suspend = swapped out by the medium-term scheduler. [Src: Pearson p.5–6]
- N CPUs, n processes: running 0…N; blocked 0…n; ready 0…(n − N) if no CPU idles while work is ready (⚠ Pearson's key takes n).

### 2.2 Schedulers, dispatcher, context switch
| Scheduler | Moves | Runs | ⭐ Controls |
|---|---|---|---|
| Long-term (job) | job pool → ready queue | rarely | **degree of multiprogramming**; I/O-/CPU-bound mix |
| Short-term (CPU) | ready queue → CPU | every ~100 ms | must be fast |
| Medium-term | swaps processes out/in | as needed | "partially swaps out a process" (NET-June-2013) |

- **Dispatcher** gives the CPU to the chosen process: context switch, switch to user mode, jump to saved PC; delay = dispatch latency (NET-Nov-2017). **Context switch** = save old state to its PCB, load the new one; pure overhead.
- Queues: job queue, ready queue (linked list of PCBs), a device queue per device. [Src: Sanchit p.24–25]
- ⭐ Running process requests I/O while 3 are ready → exactly **1** process switch (ISRO-2011). A device, timer or power failure can interrupt a running process; the scheduler cannot (GATE-2001).
- 📌 n processes, each waiting on I/O a fraction p of the time → **CPU utilisation = 1 − pⁿ** (NET-Dec-2008).

### 2.3 fork(), exec(), wait()
- `fork()` creates a child with a copy of the parent's address space (modern kernels: copy-on-write). ⭐ Returns **0 in the child, the child's PID (> 0) in the parent, −1 on failure**.
- ⚠ Sanchit p.192 says fork "returns 1 to the parent" — it returns the child's PID, any positive integer.
- `exec()` replaces the image (same PID); `wait()` blocks the parent until a child exits; **zombie** = exited, not yet waited for; **orphan** = parent died first (adopted by init).
- 📌 n `fork()` calls in sequence (or in a loop run by every process) → **2ⁿ processes, 2ⁿ − 1 children**; a following `printf` prints 2ⁿ times (GATE-2008; GATE-2012: 3 forks → 7).

🔢 Worked example
```
for (i = 0; i < 10; i++) if (i % 2 == 0) fork();        // GATE-2019
  fork runs for i = 0,2,4,6,8 → n = 5 → children = 2^5 − 1 = 31
fork() && fork() || fork();
  P : fork1 → C1; P (fork1 ≠ 0) runs fork2 → C2; P: true && true → || skipped
  C2: fork2 = 0 → && false → runs fork3 → C3
  C1: fork1 = 0 → && short-circuits → runs fork3 → C4   ⇒ 5 processes, 4 children
```
- ⭐ `if (fork()==0) a = a+5; else a = a−5;` printing value and `&a`: child value x = parent value u + 10, and the printed **addresses are equal** (virtual addresses) → "u + 10 = x and v = y" (GATE-2005). ⚠ Sanchit p.195 lists two keys; this is the correct one.

### 2.4 Threads
- Thread = basic unit of CPU utilisation: thread ID, PC, register set, stack.

| Private to each thread | Shared by all threads of a process |
|---|---|
| PC, registers, **stack**, thread ID, state | code, data (globals), **heap**, open files, signals, **address space** |

- GATE-2017: of {PC, stack, address space, registers} only the address space is shared; threads share heap **and** globals. "Light-weight" = fewer resources (NET-Dec-2012); no per-thread virtual-memory state (GATE-2011).
- Benefits: responsiveness, resource sharing, economy, multiprocessor scalability.

| | User-level threads (ULT) | Kernel-level threads (KLT) |
|---|---|---|
| Managed by | thread library; kernel unaware | kernel |
| Switch | ⭐ fast — no mode switch | slower — kernel involved |
| Blocking system call | ⭐ blocks the **whole process** (many-to-one) | blocks only that thread |
| Multiprocessor parallelism | no | yes |

- ⚠ FALSE options often offered: "blocking one KLT blocks all related threads" (GATE-2007); "KLTs cannot share the code segment" (GATE-2014); "context switch is faster with kernel-supported threads" (GATE-2004).
- Models [Src: Sanchit p.199–200]: **many-to-one** (blocking call blocks all, no parallelism; green threads) · **one-to-one** (true concurrency, kernel cost limits thread count; Linux, Windows) · **many-to-many** (m ULT → ≤ m KLT, best of both).

## 3. Inter-Process Communication

### 3.1 Shared memory vs message passing
- Independent process: cannot affect or be affected by others; **cooperating** process can — needs IPC (information sharing, speed-up, modularity).

| | Shared memory | Message passing |
|---|---|---|
| Mechanism | region mapped into both address spaces (`shm_open`, `mmap`) | `send()` / `receive()` via the kernel |
| Kernel involvement | ⭐ only to **set up** the region | ⭐ system call **per message** |
| Speed | faster | slower (copying, traps) |
| Synchronization | programmer's job | built into blocking primitives |
| Best for | large data, one machine | small data, distributed systems |

### 3.2 Message-passing design choices
[Src: Pearson p.24–25]

- **Naming**: direct (`send(P, m)`, one link per pair) vs **indirect** via mailbox/port (one-to-one, many-to-one, one-to-many, many-to-many).
- **Synchronization**: blocking (synchronous) or non-blocking (asynchronous) send/receive; blocking both = **rendezvous**; non-blocking send + blocking receive is most common.
- **Buffering**: zero capacity (sender waits), bounded (blocks when full), unbounded (never blocks). Mailbox holding one null message gives mutual exclusion (receive = enter, send = exit).

### 3.3 Pipes, signals, sockets (added — not in sources)
- **Ordinary pipe** `pipe(fd)`: one-way byte stream (`fd[0]` read, `fd[1]` write), only between related (parent–child) processes, vanishes with them; two pipes for two-way talk. Empty-pipe read blocks; full-pipe write blocks.
- **Named pipe (FIFO)** `mkfifo`: has a file-system name, outlives its processes, works for unrelated processes.
- **Signals**: asynchronous notifications (SIGKILL cannot be caught); **sockets** (IP + port) and **RPC** for IPC across machines; message queues = kernel-held message lists.

🎯 **How it's asked:** "which IPC model needs a system call for every exchange?" (message passing); "message passing can be…" (blocking and non-blocking / synchronous and asynchronous); properties of an ordinary pipe.

## 4. Concurrency & Synchronization

### 4.1 Race condition and the critical-section problem
- **Race condition**: result depends on the order/speed of interleaving (GATE-1998); `count++` = load–add–store, not atomic.
- Layout: entry section → **critical section** (where shared resources are accessed) → exit → remainder. [Src: Sanchit p.69] ⚠ Sanchit p.78 keys GATE-1996 "a critical section is…" as (A) "runs in a specified time"; correct is (C) "where shared resources are accessed".

| Requirement | Meaning |
|---|---|
| ⭐ Mutual exclusion | at most one process in its CS |
| ⭐ Progress | if the CS is free, only processes wanting to enter decide who goes next, without indefinite postponement — a process outside its CS must not block others |
| Bounded waiting | a bound on entries by others after a process has asked (no starvation) |

- ⚠ Sanchit p.70 and OpSys p.20 call bounded waiting "optional". Galvin requires all three (plus no assumptions about speed or #CPUs); MCQs treat ME + progress as the minimum for a deadlock-free solution and missing BW as "starvation possible".
- **Bernstein's conditions**: P1 ∥ P2 iff R1 ∩ W2 = W1 ∩ R2 = W1 ∩ W2 = ∅; R1 ∩ R2 may be non-empty (NET-June-2015). Precedence graphs map to `parbegin/parend` or fork–join. [Src: Ace p.65]
- 🔢 GATE-2015: B = 2; P1: `C = B−1; B = 2C`; P2: `D = 2B; B = D−1` → serial orders give 3 and 4, lost updates give 2 or 3 → **3** distinct values. GATE-2019 (D = 100; +20, −50, +10): max 130, min 50 → Y − X = **80**.

### 4.2 Two-process software solutions
| Scheme (process i, other j) | Entry … exit | ME | Progress | BW |
|---|---|---|---|---|
| Lock variable | `while(lock); lock=1;` … `lock=0` | ✗ | ✓ | ✗ |
| Strict alternation | `while(turn!=i);` … `turn=j` | ✓ | ✗ (forced alternation) | ✓ |
| Flag array | `flag[i]=T; while(flag[j]);` … `flag[i]=F` | ✓ | ✗ (both set flags → deadlock) | — |
| ⭐ Peterson | `flag[i]=T; turn=j; while(flag[j] && turn==j);` … `flag[i]=F` | ✓ | ✓ | ✓ |

- Peterson: two processes only, busy waiting, may fail on modern CPUs that reorder memory operations. Predicate = `flag[j] && turn == j` (GATE-2001). [Src: Sanchit p.72–73]

🎯 **How it's asked:** given entry/exit code, pick ME/progress status — `while(S1==S2)`/`while(S1!=S2)` → ME, no progress (GATE-2010); turn-only code → violates progress (GATE-2016); CS placed inside the busy-wait loop → no ME (GATE-2015).

### 4.3 Hardware support
- **Disabling interrupts**: uniprocessor only, privileged (kernel-only). Indivisible operation = processor cannot be preempted (NET-Dec-2015).
- **TestAndSet** atomically returns the old value and sets true: `while (TestAndSet(&lock)); CS; lock = false;` — compare-and-swap and exchange work alike.
- ⭐ TSL lock: ME ✓, progress ✓, **deadlock-free, but not starvation-free and not FIFO** (GATE-2009: "I only"); it busy-waits (spinlock). GATE-2012: the Fetch_And_Add lock fails because L can be non-zero while the lock is free.

### 4.4 Semaphores
- Integer S changed only by atomic **wait (P, down)** and **signal (V, up)**. Busy-wait form `wait: while(S<=0); S--;` keeps S ≥ 0.
- Blocking form: `wait: S--; if (S<0) block;` `signal: S++; if (S<=0) wakeup one;` → ⭐ **S = −n means n processes waiting** (NET-Dec-2009). [Src: Sanchit p.94–95]
- Counting semaphore = #resource instances; binary 0/1. Initialise **1 for mutual exclusion** (NET-June-2010), **0 for ordering**.
- **Strong** (FIFO-queue) semaphore gives bounded waiting; **weak** can starve. ⚠ Sanchit p.76 says semaphores never ensure bounded waiting — true only of weak/busy-wait ones.
- ⚠ **Binary semaphore ≠ mutex**: a mutex has an owner (only the locker unlocks). OpSys p.30 treats them as the same.
- **Priority inversion**: high H waits on a lock held by low L while medium M preempts L → fix with **priority inheritance**. [Src: ME-HW p.55]

📌 Final value = initial − (#P) + (#V).

🔢 Worked examples
```
S = 7, then 20 P and 15 V      → 7 − 20 + 15 = 2                (GATE-1992)
S = 10, 6 P and 4 V            → 8                              (GATE-1998)
20 P, 12 V; largest S0 leaving ≥ 1 P blocked: S0 + 12 < 20 → 7  (GATE-2016)
S = 2 guards x = 0; W, X: x += 1;  Y, Z: x −= 2  → max x = 2    (GATE-2013)
  W reads 0, stalls holding S; Y then Z run (x = −4); W writes 1; X makes it 2
```
- GATE-2010: S0 = 1, S1 = S2 = 0; P0 loops `wait(S0); print '0'; signal(S1); signal(S2)`; P1/P2 each `wait(Si); signal(S0)` once → '0' is printed **at least twice** (at most thrice). [Src: OpSys p.40]

### 4.5 Monitors
[Src: Pearson p.24]

- Language-level ADT of shared variables + procedures; ⭐ **only one process active inside at a time** (ME automatic).
- Condition variables: `x.wait()` suspends and releases the monitor; `x.signal()` resumes one waiter — ⭐ **with no waiter the signal is lost** (semaphore V always increments). Hoare = signal-and-wait; Mesa/Java = signal-and-continue.
- Monitors and semaphores are equally powerful; producer–consumer is solvable by semaphores, event counters or monitors (NET-Dec-2005).

### 4.6 Classical problems
[Src: Sanchit p.83–91; ME-Delhi p.60]

**Producer–consumer (bounded buffer of n)** — `mutex = 1, empty = n, full = 0`
```
Producer: produce; wait(empty); wait(mutex); add;    signal(mutex); signal(full);
Consumer: wait(full); wait(mutex); remove; signal(mutex); signal(empty); consume;
```
- ⚠ Order of the two **waits** matters: `wait(mutex)` first deadlocks on a full/empty buffer (GATE-2014); the signals may be in either order.
- ⚠ Sanchit p.83 prints `wait(F)` / `wait(E)` after the CS — they must be `signal(full)` / `signal(empty)`.
- GATE-2004: K, L, M, N = P(empty), V(full), P(full), V(empty). GATE-2018 swaps the names (empty = 0, full = N) — go by meaning, not label.

**Readers–writers (first variant, readers' preference)** — `mutex = 1` (guards readcount), `wrt = 1`
```
Writer: wait(wrt); write; signal(wrt);
Reader: wait(mutex); rc++; if (rc == 1) wait(wrt); signal(mutex);
        read;
        wait(mutex); rc--; if (rc == 0) signal(wrt); signal(mutex);
```
- R–R allowed, R–W and W–W not. This variant can **starve writers** (writers'-preference variant starves readers). GATE-2007 fill-in: S1…S4 = wait(wrt), signal(mutex), wait(mutex), signal(wrt).

**Dining philosophers (5 + 5 chopsticks)** — `wait(ch[i]); wait(ch[(i+1)%5]);` → ⭐ deadlock if all lift the left one together.
- Fixes: ≤ n − 1 seated; lift both inside a CS; asymmetry (odd left-first, even right-first, or one philosopher reversed — GATE-1996). Max eating at once = ⌊n/2⌋. GATE-2000: 5 processes using m[i], m[(i+1) mod 4] → deadlock possible.

## 5. Deadlock

### 5.1 Basics
- **Deadlock**: each process in a set waits for an event only another member can cause (infinite wait); **starvation** = indefinite wait though it could proceed. [Src: Sanchit p.105–107]
- ⭐ **Coffman conditions — all four must hold together**: mutual exclusion · hold and wait · no preemption · circular wait.
- Handling: prevention, avoidance, detection + recovery, **ignorance (ostrich)** — used by most OSs incl. Linux and Windows.

### 5.2 Prevention (deny one condition)
| Condition | Denied by | Cost |
|---|---|---|
| Mutual exclusion | make resources sharable | impossible for printers — not used |
| Hold and wait | request all at start, or only when holding none | ⭐ low utilisation, starvation |
| No preemption | release held resources when a request must wait | only for state-saveable resources (CPU, memory) |
| Circular wait | ⭐ number resource types; request in increasing order | most practical |

- GATE-2015: all-at-start, increasing order, decreasing order, "only larger than any held" — **each** prevents deadlock. GATE-2008: "release all before requesting" → starvation possible, deadlock not. GATE-2000: "never request after releasing any resource" is **not** a prevention scheme.

### 5.3 Avoidance: safe state & Banker's algorithm
[Src: Sanchit p.110–114]

- Needs maximum claims in advance. **Safe state**: an order ⟨P1…Pn⟩ exists where each Pi's remaining need ≤ Available + allocations of all earlier Pj.
- ⭐ safe ⇒ no deadlock; unsafe ⇒ deadlock **possible**, not certain. Avoidance is less restrictive than prevention (GATE-2008: "prevention grants a request if the state stays safe" is the false option).
- Single instance per type: RAG with dashed **claim edges**; grant only if no cycle results. [Src: Pearson p.37]
- 📌 **Need = Max − Allocation.** Safety: Work = Available; repeatedly finish any i with Needᵢ ≤ Work, Work += Allocationᵢ; all finish ⇒ safe; ⭐ **O(m·n²)** (NET-Aug-2016).
- Request: Request ≤ Need (else error) → ≤ Available (else wait) → pretend to allocate → safe? grant : roll back.

🔢 Worked example — A = 6, B = 4 instances
| | Alloc (A B) | Max (A B) | Need (A B) |
|---|---|---|---|
| P0 | 1 0 | 3 2 | 2 2 |
| P1 | 2 1 | 2 2 | 0 1 |
| P2 | 1 1 | 4 2 | 3 1 |
| P3 | 0 1 | 1 3 | 1 2 |

Available = (6,4) − (4,3) = (2,1). P1 → Work (4,2) → P0 → (5,2) → P2 → (6,3) → P3 → (6,4): **safe, ⟨P1, P0, P2, P3⟩**.
Now P2 requests (2,1): ≤ Need ✓, ≤ Available ✓ → pretend: Available (0,0) → no Need fits → **unsafe → P2 waits**.

### 5.4 Resource-allocation graph & detection
- Circles = processes, rectangles with dots = resource instances; **request edge** Pi → Rj, **assignment edge** Rj → Pi. [Src: Sanchit p.126–127; OSNotes p.100]
- ⭐ No cycle ⇒ no deadlock. Cycle + **single-instance** resources ⇒ deadlock. Cycle with multi-instance resources ⇒ only possible (a process outside the cycle may release an instance).
- **Wait-for graph** (single instance): remove resource nodes, Pi → Pj if Pi waits for Pj; cycle ⇔ deadlock; **O(n²)**. [Src: Pearson p.38]
- Multiple instances: safety algorithm with **Request** in place of Need; unfinished processes are deadlocked; O(m·n²). Run it on every request or periodically (e.g. when CPU utilisation falls below 40%).

🔢 NET-Aug-2016: A holds R wants T; B wants T; C wants S; D holds U wants S, T; E holds T wants V; F holds W wants S; G holds V wants U. Edges D → E (T), E → G (V), G → D (U) form a cycle of single-instance resources ⇒ **D, E, G deadlocked**; the others merely wait.

### 5.5 Recovery
[Src: Sanchit p.121–122]

- **Terminate**: all deadlocked processes, or one at a time with detection re-run; victim by priority, time used/left, resources held/needed, interactive vs batch. Simplest recovery = kill a process (NET-Dec-2013).
- **Preempt resources**: pick a victim, **roll back** it (total rollback simplest), avoid **starvation** by counting rollbacks in the cost.

### 5.6 Minimum resources for deadlock freedom
📌 n processes, process i needs at most Sᵢ units of one resource type, m units in all:
deadlock impossible ⇔ **m ≥ Σ(Sᵢ − 1) + 1**, i.e. ⭐ **Σ Sᵢ < m + n** (GATE-2005). Equal demand k: m ≥ n(k − 1) + 1. [Src: ME-Delhi p.90 for the derivation]

🔢 Worked examples
- 3 processes × 3 tape units → 3·2 + 1 = **7** (GATE-2014); 6 drives, 3 each → 2n + 1 ≤ 6 → **n = 2** (GATE-1992)
- peaks 3, 4, 6 → 2 + 3 + 5 + 1 = 11 → of the options only **13** and 15 safe (GATE-1993, NET-Dec-2012)
- 3 processes, 4 units, max K each → 3(K − 1) + 1 ≤ 4 → **K = 2** (GATE-2018)
- 6 units, ≤ 2 each → safe for n ≤ 5, so **n = 6** can deadlock (GATE-2015; GATE-1998: max n = 5)

🎯 **How it's asked:** max K / min units for deadlock freedom; Banker's table → safe? which request is grantable (GATE-2014: only REQ2); "smallest x for a safe state" [Src: OpSys p.50].

## 6. CPU Scheduling

### 6.1 Terms & criteria
[Src: Sanchit p.32–34]

📌 **TAT = CT − AT = WT + BT · WT = TAT − BT · RT = (first time on CPU) − AT.** For non-preemptive algorithms RT = WT.
- Maximise utilisation and throughput; minimise TAT, WT, RT. Scheduling changes only time in the **ready queue**, never I/O time.
- Non-preemptive decisions only when the running process blocks or exits; preemptive ones also on timer expiry and on arrivals/wake-ups.

### 6.2 Algorithms
| Algorithm | Preemptive? | Picks | ⭐ Key facts |
|---|---|---|---|
| FCFS | No | earliest arrival | **convoy effect**; no starvation |
| SJF | No | shortest next burst | ⭐ **optimal average WT**; **max throughput** (GATE-2001); long jobs starve; burst must be predicted |
| SRTF | Yes | shortest remaining | optimal average WT overall (GATE-2016); starvation |
| Priority | Either | highest priority | starvation → ⭐ **aging** (NET-Dec-2012); ties → FCFS |
| Round Robin | Yes | FIFO + quantum q | best response; q → ∞ ⇒ **FCFS** (GATE-2008); tiny q ⇒ overhead |
| HRRN | No | max (W + S)/S | favours **short** jobs, limits waits of **long** ones (GATE-1990) |
| LJF / LRTF | No / Yes | longest (remaining) burst | ties → lower PID (GATE-2006 LRTF avg TAT 13) |
| Multilevel queue | between queues | fixed queue per process | system > interactive > batch; lower queues can starve |
| ⭐ MLFQ | Yes | processes move between queues | most **general** and **complex**; hogs demoted, aging promotes; not permanently assigned (NET-June-2015) [Src: Sanchit p.64] |

📌 HRRN ratio **(W + S)/S** (W = waiting so far, S = burst). Burst prediction **τₙ₊₁ = α·tₙ + (1 − α)·τₙ**.
📌 RR: each process waits ≤ (n − 1)q; a turn within t seconds with switch cost s needs **q ≤ (t − ns)/(n − 1)** (GATE-1998).
- ⭐ Starvation possible: SJF, SRTF, priority, LJF, MLQ; not FCFS, RR, HRRN (NET-Jan-2017).
- Priority ∝ waiting time, all arrive at 0, re-evaluated every T → behaves like **RR** (GATE-2013). Average TAT varies irregularly as RR q grows (NET-June-2012).
- Non-preemptive answers: FIFO (GATE-2001/2002), SJF (NET-June-2008; "no context switching", NET-July-2018).

### 6.3 🔢 One process set, five algorithms
(AT, BT, priority; 1 = highest): **P1 (0, 5, 3) · P2 (1, 3, 1) · P3 (2, 1, 4) · P4 (3, 2, 2)**

| Algorithm | Gantt chart | Avg TAT | Avg WT | Avg RT |
|---|---|---|---|---|
| FCFS | P1 0–5, P2 5–8, P3 8–9, P4 9–11 | 6.75 | 4.00 | 4.00 |
| SJF | P1 0–5, P3 5–6, P4 6–8, P2 8–11 | 6.00 | 3.25 | 3.25 |
| SRTF | P1 0–1, P2 1–2, P3 2–3, P2 3–5, P4 5–7, P1 7–11 | **5.00** | **2.25** | 0.50 |
| Priority (preemptive) | P1 0–1, P2 1–4, P4 4–6, P1 6–10, P3 10–11 | 6.25 | 3.50 | 2.25 |
| RR, q = 2 | P1 0–2, P2 2–4, P3 4–5, P1 5–7, P4 7–9, P2 9–10, P1 10–11 | 7.25 | 4.50 | 1.75 |

- Conventions used: SRTF tie at t = 3 (P2 and P4 both 2 left) → FCFS; in RR a newly arrived process joins the queue **before** the just-preempted one. HRRN at t = 5 would pick P3: ratios P2 (4+3)/3 = 2.33, P3 (3+1)/1 = 4, P4 (2+2)/2 = 2.

🎯 **How it's asked:** SRTF average TAT/WT (GATE-2014: 7.2; GATE-2016: 8.25; GATE-2017: 5.5; GATE-2019: find Z = 2); preemptive-priority avg WT (GATE-2017: 29); SRTF context switches (GATE-2006: 2); RR completion time (GATE-1996: 9). [Src: Sanchit p.39–58]

## 7. Memory Management
*(This file owns paging, TLB and VM; the COA file cross-references it.)*

### 7.1 Address binding & MMU
[Src: Pearson p.54–55]

| Binding at | Code | Logical vs physical |
|---|---|---|
| Compile time | absolute (load address known) | same; recompile if it changes |
| Load time | relocatable | same |
| ⭐ Execution time | relocatable + MMU | **differ** — required for swapping/compaction |

- Logical address = from the CPU; physical = seen by memory (MAR). MMU **relocation register**: PA = LA + base, after checking LA < limit (else trap).
- Dynamic loading (on first call), dynamic linking (stub → shared library), overlays (programmer-managed) [Src: OSNotes p.118]; swapping moves a whole process to the backing store.

### 7.2 Contiguous allocation & fragmentation
| Scheme | Fragmentation | Note |
|---|---|---|
| Fixed partitions (equal/unequal) | ⭐ **internal** | #processes ≤ #partitions; a process larger than any partition can't run |
| Variable (dynamic) partitions | ⭐ **external** | holes; **compaction** (needs execution-time binding); coalescing adjacent holes |
| Buddy system | internal (round up to 2ᵏ) | split into halves; free buddies merge quickly [Src: Pearson p.56] |

- Paging: internal only (avg ½ page per process); segmentation: external only (table in §7.6).
- Placement: **first fit** (fastest), next fit (from last position), **best fit** (smallest adequate hole; leaves slivers), **worst fit** (largest hole); first and best beat worst (Galvin).
- 📌 **50-percent rule** (first fit): N allocated blocks lose ~0.5N to fragmentation → **one-third** of memory may be unusable.

🔢 Holes in order 150K, 350K, 200K, 500K; requests 180K, 320K, 140K, 400K
- First fit: 180→350 (170 left), 320→500 (180 left), 140→150 (10 left), **400 waits**
- Best fit: 180→200, 320→350, 140→150, 400→500 → **all placed**
- Worst fit: 180→500 (320 left), 320→350 (30 left), 140→320 (180 left), **400 waits** — ⚠ no policy wins always. [Src: OpSys p.60]

### 7.3 Paging basics & page-table size
- Logical space → **pages**, physical → **frames** of the same size; per-process page table maps page → frame; LA = (p, d) → PA = (f, d). [Src: Pearson p.58; ME-Delhi p.120]

📌 Formulas (sizes in powers of 2)
- offset bits d = log₂(page size); page bits = LA bits − d; frame bits = PA bits − d
- #pages = 2^(LA bits) / page size; #frames = physical memory / frame size
- **page-table size = #pages × PTE size**; PTE ≥ frame bits + control bits (valid, dirty, reference, protection)
- Without a TLB every reference costs **2 memory accesses** (PT + data); PTBR points to the table, PTLR gives its length.

🔢 32-bit VA, 4 KB pages, 64 MB RAM: d = 12, pages = 2³²/2¹² = 2²⁰, frames = 2²⁶/2¹² = 2¹⁴ → PTE = 14 bits ≈ 2 B → **PT = 2²⁰ × 2 B = 2 MB** per process (4 MB with 4-byte PTEs). [Src: OSNotes p.135]
- Shared pages: re-entrant code is shared by pointing several page tables at the same frames.

### 7.4 Multilevel, hashed & inverted page tables
- **Hierarchical (forward-mapped)**: page the page table — p = (p1 outer index, p2 index within a page of the PT). 32-bit, 4 KB pages, 4 B PTE → 10 + 10 + 12. [Src: Pearson p.60; OSNotes p.152]
- ⭐ Reason for multilevel tables: they **reduce the memory needed for page tables** — not access time, not page faults (GATE-2009). Cost: a k-level table needs k + 1 memory accesses on a TLB miss.

📌 Entries per PT page = page size / PTE size → index bits per level = log₂(that); levels = ⌈(VA bits − d) / bits per level⌉.

🔢 GATE-2013: 46-bit VA, 4 B PTE, 3 levels, each level's table exactly one page. Page = 2ˣ → 2^(x−2) entries per page → 3(x − 2) + x = 46 → **x = 13, page = 8 KB** (layout 11 + 11 + 11 + 13).
- **Hashed page table**: hash(virtual page #) → chain of (page, frame, next); for > 32-bit spaces. [Src: OSNotes p.146]
- ⭐ **Inverted page table**: **one entry per physical frame** (pid, page #); one table for the whole system; size ∝ physical memory; lookup needs searching → hashing; sharing pages is hard. [Src: Pearson p.60–61]

### 7.5 TLB & effective access time
[Src: Pearson p.61]

- TLB = small, fully associative cache of recent PTEs (≈ 64–1,024 entries); ASIDs let entries survive a context switch, otherwise the TLB is flushed.

📌 **EAT = h(t + m) + (1 − h)(t + 2m)** (single level); for k levels the miss term is **t + (k + 1)m**. If TLB time is not given, t = 0.

🔢 t = 20 ns, m = 100 ns, h = 0.8 → 0.8(120) + 0.2(220) = **140 ns** [Src: OpSys p.80]; with a 3-level table: 0.8(120) + 0.2(20 + 400) = **180 ns**.
- ⚠ Some texts overlap TLB lookup with memory access or ignore t on a hit — follow the question's wording. To find the required hit ratio, solve the same equation for h.

### 7.6 Segmentation & segmented paging
- Programmer's view: variable-size segments (code, data, stack…). LA = (s, d); segment table entry = (**base, limit**); PA = base + d if d < limit, else trap (addressing error). [Src: Pearson p.59]
- 🔢 Segment 1: base 1400, limit 1000 → (1, 53) → 1453; (1, 1200) → trap.
- Segmented paging: LA = (s, p, d); each segment has its own page table; removes segments' external fragmentation; **3 memory accesses** without TLB. [Src: OSNotes p.158; ME-HW p.115]

| | Paging | Segmentation |
|---|---|---|
| Unit size | fixed | variable |
| Visible to programmer | no | yes |
| Fragmentation | internal | external (NET-Dec-2012) |
| Table entry | frame number | base + limit |
| Sharing / protection | per page | natural per logical unit |

## 8. Virtual Memory

### 8.1 Demand paging & page faults
[Src: Sanchit p.128–131]

- VM runs a process only partly in memory: logical space > physical, more processes in memory, less load/swap I/O.
- ⚠ GATE-2001 "which is false?" — **"VM reduces context-switching overhead"**. Sanchit p.129 keys (A) (address translation), which is a true statement.
- Demand paging = paging + **lazy swapper (pager)**; **pure** demand paging starts with zero pages; it works because of **locality** (temporal, spatial).
- Valid–invalid bit: invalid = outside the address space **or** not in memory → page-fault trap.
- Handling: trap → check (illegal → terminate) → free frame (or replace) → disk read → update tables → **restart the instruction**.

### 8.2 EAT with page faults
📌 **EAT = (1 − p) × ma + p × PFST** (PFST = page-fault service time).
📌 With dirty victims: PFST = (1 − d)·T_clean + d·T_dirty (a dirty victim needs a write-back first).
📌 Fault rate from measurements: **p = (X − M)/(D − M)** (GATE-2018).

🔢 Worked examples
- ma = 20 ns, PFST = 10 ms, 1 fault per 10⁶ accesses → (1 − 10⁻⁶)(20) + 10⁻⁶ × 10⁷ ≈ 20 + 10 = **30 ns** (GATE-2011)
- PFST 8 ms clean / 20 ms dirty, 70% dirty → 0.3(8) + 0.7(20) = **16.4 ms** (NET-Dec-2014)
- 1 µs access, 10 ms fault, 99.99% hits → 0.9999 + 0.0001 × 10,000 = **1.9999 µs** (GATE-2000)

### 8.3 Page replacement
[Src: Sanchit p.135–148]

- **Dirty (modify) bit**: write the victim back only if modified (NET-Dec-2018). Reference bit drives LRU approximations.

| Algorithm | Victim | ⭐ Facts |
|---|---|---|
| FIFO | oldest loaded page | ⭐ **Belady's anomaly** |
| Optimal (OPT) | not used for longest time **in future** | ⭐ fewest faults; needs future → benchmark (GATE-2002) |
| LRU | not used for longest time **in past** | counters or stack; stack algorithm |
| Second chance / Clock | FIFO, skipping (and clearing) ref bit 1 | LRU approximation; all bits 1 ⇒ FIFO |
| Enhanced second chance | lowest (ref, modify) class, (0,0) first | prefers clean, unused pages |
| LFU / MFU | smallest / largest use count | rare; poor OPT approximation |
| MRU | most recently used | = OPT on a cyclic sweep larger than memory (GATE-2014) |

- ⭐ **Stack algorithms** (pages held with n frames ⊆ pages held with n + 1): OPT, LRU → **never** Belady. Belady can hit any non-stack policy: FIFO, clock, random (GATE-2017: random — true; LRU — false).
- ⚠ OSNotes p.170 says Belady occurs only in FIFO-based policies, and ME-CS p.80 ties it to "stack class" algorithms. Correct rule: possible in any non-stack policy, impossible in a stack policy.

🔢 Reference string 1 2 3 4 1 2 5 1 2 3 4 5, frames initially empty
| Frames | FIFO | LRU | OPT |
|---|---|---|---|
| 3 | 9 | 10 | 7 |
| 4 | ⭐ **10** (Belady) | 8 | 6 |

FIFO, 3 frames: 1F 2F 3F 4F(−1) 1F(−2) 2F(−3) 5F(−4) 1H 2H 3F(−1) 4F(−2) 5H → 9 faults.

🎯 **How it's asked:** GATE-2010 FIFO, 4 frames, 100 distinct pages then the same in reverse → 100 + 96 = **196**; GATE-2014 OPT on 1,2,3,4,2,1,5,3,2,4,6 (3 frames) = 7; GATE-2012 on 1,2,3,2,4,1,3,2,4,1 (3 frames): OPT 5 < FIFO 6 < LRU 9; GATE-2007 LRU − OPT = 2.

### 8.4 Frame allocation, thrashing & working set
[Src: Sanchit p.149–152]

- Minimum frames per process is set by the ISA; maximum = all frames. 📌 Equal m/n; **proportional aᵢ = (sᵢ/S) × m**. ⚠ Sanchit p.149 divides sizes 20K, 30K, 40K by 100; its 6/9/15 split of 30 frames needs 20K/30K/50K.
- **Global** replacement (any frame; better throughput; a process can't control its own fault rate) vs **local** (own frames only).
- ⭐ **Thrashing** = more time paging than executing: low utilisation → OS adds processes → more faults (global replacement) → paging queue grows → utilisation falls further.
- Cures: local replacement, **working-set** model, **page-fault frequency** bounds (too high → add frame, too low → remove), suspend processes.
- **Working set** WS(t, Δ) = distinct pages in the last Δ references (WSS non-decreasing in Δ). 📌 **D = Σ WSSᵢ > m ⇒ thrashing** → suspend a process. It implements the **principle of locality** (NET-June-2013). [Src: OSNotes p.186; OpSys p.95] 🔢 Δ = 4, refs 1 2 3 1 2 4 1 4 → window (2, 4, 1, 4) → WS = {1, 2, 4}, WSS = 3.
- Small pages → less internal fragmentation, bigger page tables; large → reverse. 📌 **Optimal page size p = √(2se)** (s = avg process size, e = PTE size) [Src: Ace p.100]; s = 1 MB, e = 8 B → **4 KB**. More RAM helps because fewer faults occur (GATE-2005).

## 9. File Systems

### 9.1 Files, access methods, directories
- Attributes (name, id, type, location, size, protection, times) live in the **FCB** (UNIX: **inode**); open-file tables keep the file pointer and open count. [Src: ME-Delhi p.160]
- Access methods: **sequential** (tape model), **direct/relative** (read block n), **indexed** (index → block, e.g. ISAM).

| Directory | Structure | ⭐ Pros / cons |
|---|---|---|
| Single-level | one directory for everyone | name clashes, no grouping |
| Two-level | master directory → one directory per user | users isolated; no subgrouping [Src: Pearson p.76] |
| Tree | root, subdirectories, absolute/relative paths, current directory | grouping and fast search; no sharing |
| Acyclic graph (added — not in sources) | shared files/subdirectories via links | sharing; aliasing; dangling pointers on delete |
| General graph (added — not in sources) | cycles allowed | needs garbage collection / cycle-safe traversal |

- Hard link = another directory entry for the same inode (reference count; can't cross file systems or point to directories); soft (symbolic) link = a small file holding a path (can dangle, can cross file systems). *(added — not in sources)*

### 9.2 Allocation methods
[Src: Sanchit p.175–179; Ace p.135–138]

| Method | Directory keeps | Access | External frag | ⭐ Issues |
|---|---|---|---|---|
| Contiguous | start, length | sequential + direct, fewest seeks | **yes** | file growth; size needed up front |
| Linked | first (and last) block | sequential only | no | pointer per block; i-th block needs i reads; fragile chain |
| FAT | first block; table holds next pointers | direct if FAT cached | no | table size |
| Indexed | index-block address | direct | no | index-block overhead; big files → linked/multilevel/combined (inode) index |

- 🎯 NET-June-2014 match: contiguous → fewest disk accesses; linked → sequential only; indexed → most pointer wastage; multilevel → very large files. GATE-2017: no external fragmentation → **linked and indexed**. GATE-2008: UNIX large files → **extension of indexed**. GATE-2002: max size depends on block size, #index blocks **and** address size.
- Larger blocks → **better throughput, poorer space utilisation** (GATE-2003).

### 9.3 inode — maximum file size
- UNIX inode: attributes + 15 pointers = **12 direct, 1 single, 1 double, 1 triple indirect**.

📌 Pointers per block **n = B / a** (B = block size, a = address size). **Max file size = (D + n + n² + n³) × B** — drop the terms for missing levels. Reading a byte through a direct pointer costs 1 disk access after the inode; single 2, double 3, triple 4.

🔢 Worked examples
- GATE-2014: 12 direct + single + double, B = 4 KB, a = 4 B → n = 1024 → (12 + 1024 + 1024²) × 4 KB = 48 KB + 4 MB + 4 GB ≈ **4.0 GB**
- GATE-2012: 8 direct + single + double, B = 128 B, a = 8 B → n = 16 → (8 + 16 + 256) × 128 B = 35,840 B = **35 KB** (the 300 GB disk size is a distractor)
- GATE-2004: 10 direct + single + double + triple, 1 KB blocks, 32-bit addresses → n = 256 → ≈ 256³ × 1 KB = **2³⁴ B** [Src: ME-Delhi p.168]

### 9.4 Free-space management
[Src: Sanchit p.181–183]

| Method | Idea | Note |
|---|---|---|
| Bit vector (bitmap) | 1 bit per block | 📌 size = #blocks bits; quick to find first free / n consecutive; must sit in memory. ⚠ Galvin: 1 = free; Stallings/Pearson p.78: 0 = free — use the question's convention |
| Linked list | free blocks chained, head cached | no wasted space; traversal slow but rarely needed |
| Grouping (added — not in sources) | first free block stores addresses of n free blocks, last of which leads to the next group | finds many free blocks fast |
| Counting (added — not in sources) | (start, count) for each run of contiguous free blocks | compact when free space is contiguous |

🔢 Worked examples
- Bitmap, 1.3 GB disk, 512 B blocks → 1.3 × 2³⁰/2⁹ ≈ 2.73 × 10⁶ bits ≈ **332.8 KB** (NET-Dec-2013)
- 1 TB, 4 KB blocks → 2²⁸ bits = 2²⁵ B = **32 MB**. ⚠ Sanchit p.181 writes "256 MB" — it is 256 **Mbit**.
- FAT (GATE-2014): 100 × 10⁶ B disk, 10³ B blocks → 10⁵ entries × 4 B = 0.4 × 10⁶ B → max file = **99.6 × 10⁶ B**

## 10. Disk (I/O) Scheduling

### 10.1 Disk structure & access time
[Src: Sanchit p.170–173; Ace p.128]

- Platter → 2 surfaces → tracks → sectors; **cylinder** = same track on all surfaces — the most data readable without moving the arm (NET-Dec-2011).
- 📌 **Capacity = surfaces × tracks/surface × sectors/track × bytes/sector.**
- 📌 **Access time = seek + rotational latency + transfer**; average latency = ½ rotation = 30/RPM s; data rate = track bytes × RPM/60; transfer = bytes / data rate.
- Seek time is not linear in distance because of arm start/stop inertia (GATE-2008).

🔢 Worked examples
- 16 surfaces × 128 tracks × 256 sectors × 512 B = 2⁴⁺⁷⁺⁸⁺⁹ = 2²⁸ B = **256 MB**; sector address = 4 + 7 + 8 = **19 bits** (GATE-2006)
- 100 libraries at random places, seek 10 ms, 6000 RPM (10 ms/rev → 5 ms latency), transfer ignored → 100 × 15 ms = **1.5 s** (GATE-2011)
- seek 4 ms, 10,000 RPM (6 ms/rev), 600 sectors/track, 2000 sectors each needing a seek → 2000 × (4 + 3 + 0.01) = **14,020 ms** (GATE-2015)

### 10.2 Scheduling algorithms
[Src: Sanchit p.155–166]

| Algorithm | Rule | ⭐ Facts |
|---|---|---|
| FCFS | arrival order | fair, no starvation, most movement |
| SSTF | nearest cylinder next | SJF-like; **starvation**; not optimal; high variance; best throughput of the classic options (GATE-1999) |
| SCAN (**elevator**) | sweep to the disk end, reverse | no starvation; travels to the end even with no request there |
| C-SCAN | serve one direction, jump back to the start | ⭐ **most uniform waiting time** |
| LOOK | SCAN, reversing at the last request | no wasted travel |
| C-LOOK | C-SCAN, jumping from the last request to the first request at the other end | — |

- Galvin: SSTF or LOOK as default; SCAN/C-SCAN for heavy load. With one pending request every algorithm acts like FCFS — a single sequential process gains **0%** from SSTF (GATE-2004).
- ⚠ Count the return sweep in C-SCAN/C-LOOK head movement unless told otherwise (GATE-2018 C-LOOK answer 346 includes it).

🔢 Queue 98, 183, 37, 122, 14, 124, 65, 67; head at 53; cylinders 0–199
| Algorithm | Service order | Head movement |
|---|---|---|
| FCFS | as given | 640 |
| SSTF | 65, 67, 37, 14, 98, 122, 124, 183 | 236 |
| SCAN (toward 0) | 37, 14, →0, 65 … 183 | 53 + 183 = 236 |
| LOOK (toward 199) | 65 … 183, then 37, 14 | 130 + 169 = 299 |
| C-SCAN (toward 199) | 65 … 183, →199, jump to 0, 14, 37 | 146 + 199 + 37 = 382 |
| C-LOOK (toward 199) | 65 … 183, jump to 14, 37 | 130 + 169 + 23 = 322 |

- ⚠ Sanchit p.161 keys the C-SCAN question (head 45 moving up; requests 40, 67, 11, 240, 87; tracks 0–255) as 550. Counting the return sweep: (255 − 45) + 255 + 40 = **505**.

## Last-day revision sheet
| Topic | Formula / number to memorise |
|---|---|
| Times | TAT = CT − AT = WT + BT; WT = TAT − BT; RT = first run − AT |
| CPU utilisation | 1 − pⁿ (n processes, I/O-wait fraction p) |
| Burst prediction | τₙ₊₁ = α·tₙ + (1 − α)·τₙ |
| HRRN | (W + S)/S |
| RR | wait ≤ (n − 1)q; q ≤ (t − ns)/(n − 1) |
| fork | n forks → 2ⁿ processes, 2ⁿ − 1 children; returns 0 / child PID / −1 |
| Semaphore | final = init − #P + #V; S = −n ⇒ n blocked |
| Deadlock-free | m ≥ Σ(Sᵢ − 1) + 1 ⇔ ΣSᵢ < m + n; equal k: n(k − 1) + 1 |
| Banker's | Need = Max − Alloc; safety O(m·n²); wait-for-graph cycle check O(n²) |
| Paging | d = log₂(page); #pages = VAS/page; PT = #pages × PTE |
| Multilevel | entries per PT page = page/PTE; k levels → k + 1 accesses on TLB miss |
| TLB | EAT = h(t + m) + (1 − h)(t + (k + 1)m) |
| Page faults | EAT = (1 − p)·ma + p·PFST; p = (X − M)/(D − M) |
| Allocation | aᵢ = (sᵢ/S) × m |
| Thrashing | ΣWSSᵢ > total frames |
| Page size | optimal √(2se); paging wastes ½ page per process on average |
| 50-percent rule | ⅓ of memory lost (first fit) |
| inode | (D + n + n² + n³) × B, n = B/a; UNIX 12 + 1 + 1 + 1 |
| Bitmap | #blocks bits = #blocks/8 bytes |
| Disk | capacity = surf × tracks × sectors × bytes; access = seek + 30/RPM s + transfer; rate = track bytes × RPM/60 |

1. ⭐ Mode bit: kernel 0, user 1; entry to kernel only by system call, interrupt or exception.
2. Mode switch < context switch in cost; a system call need not cause a context switch.
3. ⭐ Ready → Running = dispatch; no Blocked → Running edge.
4. Long-term = degree of multiprogramming; medium-term = swapping; short-term = CPU.
5. ⭐ Threads share code, globals, heap, files; each has its own stack, registers, PC.
6. Many-to-one ULTs: one blocking call blocks the whole process.
7. Shared memory: syscalls only for set-up; message passing: one per message.
8. ⭐ Peterson = ME + progress + bounded waiting, two processes only; turn-only code violates progress.
9. TSL spin lock: deadlock-free, not starvation-free.
10. Semaphore init 1 for ME, 0 for ordering; mutex has an owner, binary semaphore does not.
11. Monitor: one active process; `signal` with no waiter is lost.
12. ⭐ Producer: `wait(empty)` before `wait(mutex)`, else deadlock.
13. First readers–writers starves writers; dining philosophers fixed by ≤ n − 1 seats or asymmetry.
14. Priority inversion → priority inheritance.
15. ⭐ All four Coffman conditions necessary; RAG cycle sufficient only for single instances.
16. ⭐ Safe ⇒ no deadlock; unsafe ⇒ only possible; Banker's = avoidance; most OSs ignore deadlock.
17. ⭐ SJF = minimum average WT; SRTF = its preemptive optimum; neither exactly implementable.
18. RR huge q → FCFS; starvation-free: FCFS, RR, HRRN; aging cures priority starvation.
19. MLFQ = most general and most complex scheduler.
20. Logical ≠ physical address only with execution-time binding.
21. ⭐ Fixed partitions → internal; variable → external (compaction); paging → internal only; segmentation → external only.
22. Inverted PT: one entry per frame; multilevel PT saves memory, not time.
23. ⭐ Belady: FIFO and other non-stack policies; never LRU/OPT.
24. OPT = fewest faults; MRU = OPT on cyclic sweeps larger than memory.
25. Thrashing: CPU utilisation collapses; cure by working set, PFF, local replacement, fewer processes.
26. Contiguous: fast but external fragmentation; linked: sequential only; indexed: direct, no external fragmentation.
27. Larger blocks → better throughput, worse space use.
28. ⭐ SCAN = elevator; C-SCAN = most uniform wait; SSTF can starve; one pending request ⇒ all = FCFS.
29. Spooled device = shared line printer.
30. Hard real-time: a missed deadline is a failure.

## Dropped as outside TPSC syllabus
- History/trivia: evolution narrative, punch cards, OS market shares, CLI/GUI/shell discussion, diskless-client booting (Sanchit p.1–17, 188; Ace p.146).
- COA material: Von Neumann model, registers, instruction cycle (ME-CS p.3, Ace p.2); interrupt-priority and stack-pointer PYQs (GATE-2011, GATE-2001); RAM-chip/decoder construction (Pearson PYQs, Ace, ME-HW); memory-capacity conversions (OSNotes p.112); virtually-indexed cache/page colouring (GATE-2013); TLB + cache "inline" EMAT (OSNotes p.140).
- Protection & security: access matrix, capabilities, threats (Pearson ch.5, Ace).
- I/O detail beyond disk scheduling: buffering, DMA/polling (Pearson p.80), disk interleaving (Sanchit p.172), RAID, NTFS, file organisations (pile, indexed-sequential).
- Fine VM policies: VSWS, page buffering, pre-cleaning, load control (Pearson ch.4); distributed-system design detail.
