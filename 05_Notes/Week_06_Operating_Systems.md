# Week 6 — Operating Systems

**Syllabus §8:** System calls, processes, threads, inter-process communication, concurrency and synchronization. Deadlock. CPU and I/O scheduling. Memory management and virtual memory. File systems.
**Estimated marks: ~11 — the most numerical section in the paper**

---

## 💡 What an operating system is

Hardware is difficult and hostile: you have one CPU, a fixed amount of RAM, and devices with intricate protocols. Yet twenty programs appear to run at once, each behaving as if it owns the machine.

The **operating system** creates that illusion. It has two jobs:

1. ⭐ **Resource manager** — decides who gets the CPU, how much memory, which disk blocks. It **shares** limited hardware among competing programs, fairly and safely.
2. ⭐ **Abstraction layer** — hides hardware detail. Your program calls `write()`; it does not need to know whether the target is an SSD, a network socket or a printer.

Everything in this file is one of those two jobs:
- **Processes, threads, scheduling** → sharing the CPU
- **Synchronization, deadlock** → sharing data safely
- **Memory management, virtual memory** → sharing RAM
- **File systems, disk scheduling** → sharing storage

---

# 1. Fundamentals

## 1.1 Types of OS

| Type | 💡 Characteristic |
|---|---|
| **Batch** | Jobs collected and run in groups; no user interaction |
| ⭐ **Multiprogramming** | Several programs in memory; when one blocks on I/O, the CPU switches to another. ⭐ **Goal: maximise CPU utilisation** |
| ⭐ **Multitasking / time-sharing** | Rapid switching gives every user the illusion of a dedicated machine. ⭐ **Goal: minimise response time** |
| **Multiprocessing** | Multiple physical CPUs |
| ⭐ **Real-time (RTOS)** | ⭐ **Hard RTOS** — a missed deadline is a system failure (pacemaker, airbag). ⭐ **Soft RTOS** — deadlines preferred but not fatal (video streaming) |
| **Distributed** | Independent machines presented as one system |
| **Embedded** | Dedicated function, tightly resource-constrained |

⚠ ⭐ **Multiprogramming vs multitasking:** both keep several programs in memory, but multiprogramming switches only when a program **blocks**, whereas multitasking switches on a **timer** as well. Multitasking is multiprogramming plus preemption.

## 1.2 ⭐ Kernel mode vs user mode

### 💡 The idea

If any program could execute any instruction, one buggy program could halt the machine, read another's memory, or reprogram the disk controller. So the CPU has (at least) two **privilege levels**:

- ⭐ **User mode** — restricted. Cannot execute privileged instructions (halt, set the page table, access I/O ports directly).
- ⭐ **Kernel mode** — unrestricted. Only OS code runs here.

⭐ A **mode switch** (user → kernel) happens on a **system call**, an **interrupt**, or a **trap/exception**.

⚠⚠ ⭐ **A mode switch is NOT a context switch.** A mode switch changes the *privilege level* of the *same* process. A context switch changes *which process* is running. A system call causes a mode switch but usually not a context switch.

**Kernel architectures:**

| Architecture | 💡 Note |
|---|---|
| **Monolithic** | All services inside the kernel. Fast (no message passing), but a bug anywhere can crash everything. Linux is largely monolithic (with modules) |
| ⭐ **Microkernel** | Only the bare minimum in the kernel (IPC, scheduling, basic memory); drivers and file systems run as **user-space** processes. ⭐ **More reliable and modular**, but slower due to message-passing overhead |
| **Hybrid** | Windows NT, macOS |

## 1.3 ⭐⭐ System calls

### 💡 The idea

📌 A **system call** is the **only** doorway from user mode into the kernel. When your C program calls `printf`, the library eventually issues a `write()` system call, which traps into the kernel, which talks to the device.

| Category | ⭐ Examples |
|---|---|
| **Process control** | ⭐ `fork()`, `exec()`, `wait()`, `exit()`, `abort()` |
| **File management** | `open()`, `read()`, `write()`, `close()`, `lseek()` |
| **Device management** | `ioctl()`, `read()`, `write()` |
| **Information** | `getpid()`, `alarm()`, `time()` |
| **Communication** | `pipe()`, `shmget()`, `mmap()`, `send()`, `recv()` |
| **Protection** | `chmod()`, `umask()`, `chown()` |

### ⭐⭐ `fork()` — the one that gets asked

💡 `fork()` **duplicates** the calling process. After it returns, there are **two** nearly identical processes, both executing the next line. The only way to tell them apart is the return value:

📌 ⭐ **`fork()` returns 0 to the CHILD, the child's PID to the PARENT, and −1 on failure.**

```c
pid_t p = fork();
if (p == 0)      { /* child code  */ }
else if (p > 0)  { /* parent code */ }
else             { /* fork failed */ }
```

### 🔢 The counting question

```c
fork();
fork();
fork();
```
How many processes exist?

```
Start:        1 process
After fork 1: 2 processes    (both continue to the next line)
After fork 2: 4 processes
After fork 3: 8 processes
```
📌 ⭐ **n consecutive `fork()` calls → 2ⁿ total processes, i.e. 2ⁿ − 1 CHILDREN.**

🔢 Three forks → **8 processes**, **7 children**.

⚠ Read the question: "how many processes are created" usually means the **children** (2ⁿ − 1); "how many processes exist" means 2ⁿ.

### ⚠ `exec()` — often confused with `fork()`

⭐ **`exec()` REPLACES the current process's memory image with a new program.** It does **not** create a process, and on success it **never returns** (there is nothing to return to — the old program is gone).

⭐ The standard shell pattern is `fork()` then `exec()`: fork to get a new process, exec to make it run the desired program.

---

# 2. ⭐⭐ Processes and threads

## 2.1 💡 What a process is

📌 A **program** is a passive file on disk. A **process** is a program **in execution** — it has a program counter, registers, a stack, a heap, and a place in the OS's tables.

One program can produce many processes (three browser windows = three processes running the same program).

## 2.2 ⭐⭐ Process states

```
                    admitted            dispatch              exit
     NEW ──────────────────► READY ──────────────────► RUNNING ─────────► TERMINATED
                               ▲   ◄──────────────────┘  │
                               │    ⭐ PREEMPTION         │ ⭐ I/O REQUEST
                               │    (quantum expiry)      │ or event wait
                               │                          ▼
                               └──────── WAITING / BLOCKED
                                      I/O completion
```

⭐⭐ **Two transitions get confused constantly. Learn them separately:**

| Transition | ⭐ Cause |
|---|---|
| ⭐ **RUNNING → READY** | ⭐ **PREEMPTION** — the time quantum expired, or a higher-priority process arrived. *The process is still able to run; it just lost the CPU.* |
| ⭐ **RUNNING → WAITING** | ⭐ **An I/O REQUEST** or waiting for an event. *The process cannot run even if given the CPU.* |
| WAITING → READY | I/O completed |
| RUNNING → TERMINATED | `exit()` |

⚠ There is **no** WAITING → RUNNING transition — a process that finishes waiting must go through READY and be scheduled again.

## 2.3 Process Control Block (PCB)

The OS's record for one process:
- Process ID and **state**
- **Program counter** and CPU registers (saved on a context switch)
- Scheduling information (priority, queue pointers)
- Memory-management information (page tables, base/limit registers)
- Accounting information (CPU time used)
- I/O status and the **open-file table**

## 2.4 ⭐ Zombie and orphan processes

### 💡 The idea

When a child finishes, its **exit status** must be reported to its parent. So the OS cannot fully delete the child until the parent calls `wait()`.

| Term | 💡 Meaning |
|---|---|
| ⭐ **Zombie** | ⭐ The child has **TERMINATED**, but the parent has not yet called `wait()`. Its PCB entry lingers, holding the exit status. *Dead child, live parent.* |
| ⭐ **Orphan** | ⭐ The child is **STILL RUNNING**, but its **parent has died**. It is re-parented to `init`/`systemd`. *Live child, dead parent.* |
| **Daemon** | A long-running background service process |

⚠ ⭐ **Zombie and orphan are opposite situations.** Zombie = dead child; orphan = dead parent.

⚠ A zombie consumes no memory or CPU — only a process-table slot. But a program that forks endlessly without reaping can exhaust the process table.

## 2.5 ⭐⭐ Threads

### 💡 The idea

A process is expensive: its own address space, its own page tables. But often you want **several flows of control inside one program**, sharing data — a web server handling 100 connections, a word processor spell-checking while you type.

A **thread** is a lightweight flow of execution **inside** a process. All threads of a process share its memory.

⭐⭐ **What is shared and what is private — the most-asked thread question:**

| ⭐ **SHARED** among threads of a process | ⭐ **PRIVATE** to each thread |
|---|---|
| Code section (text) | ⭐ **Stack** |
| Data section (globals) | ⭐ **Registers** |
| ⭐ **Heap** | ⭐ **Program counter** |
| Open files, signals | Thread ID |
| | Thread-local storage |

💡 **Why the stack must be private:** each thread executes its own sequence of function calls, so each needs its own chain of activation records. Sharing a stack would be incoherent.

💡 **Why the heap is shared:** that is the *point* — threads collaborate on shared data structures. (And it is also why synchronization, §5, becomes necessary.)

### ⭐ Process vs thread

| | **Process** | ⭐ **Thread** |
|---|---|---|
| Address space | Own | ⭐ **Shared with peers** |
| Creation cost | High | ⭐ **Low** |
| Context switch cost | High (page tables, TLB flush) | ⭐ **Low** (same address space) |
| Communication | ⭐ **Needs IPC** (kernel-mediated) | ⭐ **Direct via shared memory** |
| Fault isolation | ⭐ **One crash does not affect others** | ⭐ **One crash can kill the whole process** |
| Also called | Heavyweight process | Lightweight process (LWP) |

### Thread models

| Model | 💡 Note |
|---|---|
| **User-level threads** | Managed by a library, invisible to the kernel. Fast to switch. ⚠ **But one blocking system call blocks ALL threads**, and no true multi-core parallelism |
| **Kernel-level threads** | Known to the kernel. Slower switching, but ⭐ **true parallelism** and one thread blocking does not block others |
| **Many-to-one / one-to-one / many-to-many** | Mappings between user and kernel threads |

## 2.6 Context switch

⭐ **Saving the current process's state into its PCB and loading the next process's state.**

⭐ **It is pure overhead** — no useful work is done during it. The cost includes register saves/restores, **TLB flush**, and **cache pollution** (the new process's data evicts the old process's). This is why an excessively small time quantum destroys performance.

---

# 3. ⭐⭐⭐ CPU scheduling

## 3.1 💡 The idea and the terminology

With several processes READY, which gets the CPU? That decision is **scheduling**, and different policies optimise different things.

📌 ⭐ **The four quantities, and how they relate:**

| Term | ⭐ Definition |
|---|---|
| **Arrival Time (AT)** | When the process entered the ready queue |
| **Burst Time (BT)** | CPU time the process needs |
| **Completion Time (CT)** | When it finished |
| ⭐ **Turnaround Time (TAT)** | ⭐ **CT − AT** — total time in the system |
| ⭐ **Waiting Time (WT)** | ⭐ **TAT − BT** — time spent waiting, not executing |
| **Response Time** | First CPU allocation − AT |

💡 **Why WT = TAT − BT:** the total time you were in the system, minus the time you were actually being served, is the time you spent waiting. ✅

⭐ **The exam method, always:**
1. Draw the **Gantt chart**
2. Read off **CT** for each process
3. Compute **TAT = CT − AT**
4. Compute **WT = TAT − BT**
5. Average

Do not try to shortcut this. The Gantt chart takes 30 seconds and prevents every arithmetic slip.

## 3.2 ⭐⭐ The algorithms

| Algorithm | Preemptive? | Selects | ✅ Pros | ❌ Cons |
|---|---|---|---|---|
| ⭐ **FCFS** | ❌ Non-preemptive | Earliest arrival | Simple, fair, ⭐ **no starvation** | ⭐ **Convoy effect**; poor average WT |
| ⭐ **SJF** | ❌ Non-preemptive | Shortest **burst** | ⭐ **Provably minimum average WT** | Burst time unknown in advance; ⭐ **starves long jobs** |
| ⭐ **SRTF** | ✅ Preemptive | Shortest **remaining** time | Optimal among preemptive | Starvation; high switching overhead |
| **Priority** | Both variants exist | Highest priority | Flexible | ⭐ **Starvation** — fixed by ⭐ **AGING** |
| ⭐ **Round Robin** | ✅ Preemptive | Next in queue, fixed **quantum** | ⭐ **Good response time**, no starvation, fair | Higher average TAT; overhead if the quantum is tiny |
| **Multilevel queue** | ✅ | Fixed queues per job class | Separates interactive from batch | Inflexible |
| **Multilevel feedback queue** | ✅ | Queues with promotion/demotion | ⭐ **Adaptive** — general purpose; learns job behaviour | Complex to tune |
| **HRRN** | ❌ | Highest **response ratio** (1 + WT/BT) | Balances short and long jobs; no starvation | Needs burst estimates |

### 💡 The convoy effect (FCFS's weakness)

One long process at the front makes everyone behind it wait — like a slow lorry on a single-lane road with a queue of cars behind it. The **average** waiting time becomes terrible even though nobody is treated unfairly.

### 💡 Why SJF is optimal
Serving the shortest job first minimises the total waiting time, because a short job's completion frees the CPU sooner for everyone else. Formally, this is a classic exchange argument: swapping any longer-before-shorter pair always reduces the total wait.

⚠ ⭐ **But SJF is not implementable directly** — the OS cannot know a process's future burst time. Real systems **estimate** it from past behaviour (exponential averaging), which is what multilevel feedback queues effectively do.

### 💡 The Round Robin quantum trade-off

⭐ **Quantum too large** → nobody is ever preempted → RR **degenerates into FCFS**.
⭐ **Quantum too small** → context-switch overhead dominates; the CPU spends its time switching rather than computing.

Typical real quantum: 10–100 ms, chosen so that ~80% of bursts finish within one quantum.

⭐ **Starvation-free: FCFS and Round Robin.** ⭐ **Starvation-prone: SJF, SRTF, priority.**
⭐ **The fix for priority starvation is AGING** — gradually increase the priority of a process the longer it waits, so it eventually runs.

## 3.3 🔢 Worked example 1 — FCFS and the convoy effect

Three processes arrive at t = 0 in the order P1, P2, P3 with bursts 24, 3, 3.

**Gantt chart:**
```
│    P1    │ P2 │ P3 │
0         24   27   30
```

| Process | AT | BT | CT | TAT = CT−AT | WT = TAT−BT |
|---|---|---|---|---|---|
| P1 | 0 | 24 | 24 | 24 | **0** |
| P2 | 0 | 3 | 27 | 27 | **24** |
| P3 | 0 | 3 | 30 | 30 | **27** |

⭐ **Average WT = (0 + 24 + 27)/3 = 51/3 = 17 ms**
⭐ **Average TAT = (24 + 27 + 30)/3 = 81/3 = 27 ms**

**Now compare SJF** (same processes, order P2, P3, P1):
```
│ P2 │ P3 │    P1    │
0    3    6         30
```
WT: P2 = 0, P3 = 3, P1 = 6 → ⭐ **Average WT = 3 ms**

⭐ **17 ms vs 3 ms from reordering alone.** That is the convoy effect, and why SJF is optimal.

## 3.4 🔢 Worked example 2 — Round Robin

Same processes, **quantum = 4**.

**Gantt chart:**
```
│ P1 │ P2 │ P3 │        P1        │
0    4    7    10                30
```
(P1 uses 4, is preempted; P2 needs only 3 and finishes; P3 needs only 3 and finishes; P1 resumes with 20 left.)

| Process | AT | BT | CT | TAT | WT |
|---|---|---|---|---|---|
| P1 | 0 | 24 | 30 | 30 | **6** |
| P2 | 0 | 3 | 7 | 7 | **4** |
| P3 | 0 | 3 | 10 | 10 | **7** |

⭐ **Average WT = 17/3 ≈ 5.67 ms** · Average TAT = 47/3 ≈ 15.67 ms

⭐ Note RR's average WT (5.67) sits between FCFS (17) and SJF (3), but its **response time** is the best of the three — no process waits more than one quantum-round before getting some CPU. That is the point of RR for interactive systems.

## 3.5 🔢 Worked example 3 — SRTF with staggered arrivals

| Process | AT | BT |
|---|---|---|
| P1 | 0 | 8 |
| P2 | 1 | 4 |
| P3 | 2 | 9 |
| P4 | 3 | 5 |

**Reasoning:** at t=0 only P1 exists → run P1. At t=1, P2 arrives needing 4 < P1's remaining 7 → **preempt**, run P2. At t=2, P3 arrives needing 9 > P2's remaining 3 → keep P2. At t=3, P4 arrives needing 5 > P2's remaining 2 → keep P2. At t=5 P2 finishes; remaining are P1 (7), P3 (9), P4 (5) → run P4. At t=10 P4 finishes → run P1 (7). At t=17 → run P3.

```
│P1│  P2  │   P4   │    P1    │     P3     │
0  1      5       10          17          26
```

| Process | AT | BT | CT | TAT | WT |
|---|---|---|---|---|---|
| P1 | 0 | 8 | 17 | 17 | **9** |
| P2 | 1 | 4 | 5 | 4 | **0** |
| P3 | 2 | 9 | 26 | 24 | **15** |
| P4 | 3 | 5 | 10 | 7 | **2** |

⭐ **Average WT = (9+0+15+2)/4 = 26/4 = 6.5 ms** · Average TAT = 52/4 = **13 ms**

## 3.6 I/O scheduling
Processes alternate between **CPU bursts** and **I/O bursts**. A good scheduler keeps both the CPU and the devices busy by mixing **CPU-bound** processes (long CPU bursts) with **I/O-bound** ones (short CPU bursts, frequent I/O). Multilevel feedback queues naturally promote I/O-bound processes, since they yield before their quantum expires.

---

# 4. ⭐ Inter-Process Communication (IPC)

## 💡 The idea

Processes have **separate address spaces** by design (that is what makes them safe). So how do two cooperating processes exchange data? The OS must provide a channel.

| Mechanism | 💡 How it works | Trade-off |
|---|---|---|
| ⭐ **Shared memory** | Both processes map the **same physical region** into their address spaces | ⭐ **Fastest** — after setup, no kernel involvement at all. ❌ But the programmer must handle **synchronization** (§5) manually |
| ⭐ **Message passing** | `send()` / `receive()` through the kernel | ⭐ Slower (kernel copies data), ✅ but needs no explicit synchronization and ⭐ **works across machines** |
| **Pipes** | A unidirectional byte stream between **related** processes (the shell's `\|`). **Named pipes (FIFOs)** work between unrelated processes | Simple, stream-oriented |
| **Sockets** | Bidirectional, network-capable | The basis of all networking |
| **Signals** | Asynchronous notifications (`SIGKILL`, `SIGTERM`, `SIGINT`) | Carries almost no data — just an event |
| **Message queues, semaphores** | System V / POSIX IPC objects | |

⭐ **Shared memory vs message passing is the classic comparison:** shared memory is faster but needs synchronization; message passing is slower but safer and distributable.

**Message passing options:** **blocking (synchronous)** vs **non-blocking (asynchronous)** send/receive; **direct** addressing (name the process) vs **indirect** (via a mailbox).

---

# 5. ⭐⭐⭐ Concurrency and synchronization

## 5.1 💡 The race condition — the problem being solved

Two threads share `balance = 1000`. Both execute `balance = balance + 100`.

That single line is really **three** machine operations:
```
1. LOAD  balance into a register
2. ADD   100
3. STORE the register back to balance
```

If the two threads interleave badly:
```
Thread A: LOAD  (reads 1000)
Thread B: LOAD  (reads 1000)     ← both read the SAME old value
Thread A: ADD   → 1100
Thread B: ADD   → 1100
Thread A: STORE → balance = 1100
Thread B: STORE → balance = 1100  ← A's update is LOST
```
⭐ **Two deposits of 100 produced one increase of 100.** The final answer depends on timing — a **race condition**.

📌 ⭐ The section of code that touches shared data is the **critical section**, and the problem is ensuring only one process executes it at a time.

## 5.2 ⭐⭐ The three requirements

📌 ⭐ **Any correct solution to the critical-section problem must satisfy:**

| Requirement | 💡 Meaning |
|---|---|
| ⭐ **1. Mutual exclusion** | **At most one** process in the critical section at a time |
| ⭐ **2. Progress** | If no process is in the critical section, a waiting process **must be able to enter**. ⭐ *No unnecessary blocking* |
| ⭐ **3. Bounded waiting** | There is a **limit** on how many others may enter before a waiting process gets its turn. ⭐ *No starvation* |

💡 **Why all three are needed:** mutual exclusion alone is satisfiable by never letting anyone in. Progress prevents that degenerate "solution". Bounded waiting prevents an unlucky process from being passed over forever.

⚠⚠ ⭐ **Do not confuse these with DBMS's ACID properties** (Atomicity, Consistency, Isolation, Durability — Week 7). Exam options mix the two lists deliberately.

## 5.3 Software solutions

**Attempt 1 — strict alternation (a `turn` variable):**
```
while (turn != me) ;      // wait
critical_section();
turn = other;
```
✅ Mutual exclusion. ❌ ⭐ **Progress fails** — if the other process never wants to enter, I can only go every second time, and I block waiting for a turn that never comes.

**Attempt 2 — flags only:** both set `flag[me] = true` and wait for the other's flag to clear. ❌ Can **deadlock** — both set their flag simultaneously and wait forever.

⭐ **Peterson's solution (two processes)** — combines both ideas: a `flag[]` array *and* a `turn` variable.
```
flag[i] = true;
turn = j;                          // politely offer the turn to j
while (flag[j] && turn == j) ;     // wait only if j wants it AND it's j's turn
critical_section();
flag[i] = false;
```
⭐ **Satisfies all THREE requirements.** ⚠ It relies on atomic loads/stores and on the compiler/CPU not reordering the instructions (real code needs memory barriers).

**Lamport's Bakery algorithm** generalises this to n processes (each takes a "ticket number" like at a bakery counter).

## 5.4 Hardware support

Atomic instructions the CPU provides: **Test-and-Set**, **Compare-and-Swap (CAS)**, **Swap/Exchange**. These read and modify a memory location in one indivisible step.

A ⭐ **spinlock** is built on them and **busy-waits** in a tight loop. Efficient only when the critical section is very short (shorter than a context switch), otherwise it wastes CPU.

⚠ Disabling interrupts enforces mutual exclusion only on a **uniprocessor** — useless with multiple cores.

## 5.5 ⭐⭐ Semaphores

### 💡 The idea

A **semaphore** is an integer that can only be touched through two **atomic** operations:

```
wait(S)   / P(S):   while (S <= 0) ;  S--;      // acquire
signal(S) / V(S):   S++;                        // release
```

💡 **Analogy: a car park with S free spaces.** `wait()` takes a space (blocking if none are free); `signal()` frees one. The counter *is* the number of available permits.

| Type | Range | ⭐ Use |
|---|---|---|
| ⭐ **Binary semaphore** | 0 or 1 | Mutual exclusion (behaves like a mutex) |
| ⭐ **Counting semaphore** | 0 … n | ⭐ Controls access to **n identical resources** |

📌 ⭐ **A counting semaphore initialised to n allows n processes into the critical section simultaneously.**

⚠ ⭐ **Semaphore vs mutex:** a **mutex has OWNERSHIP** — only the thread that locked it may unlock it. A semaphore has no owner and may be signalled by any process. A mutex is for mutual exclusion; a semaphore is for signalling and resource counting.

⭐ **Monitor** — a higher-level construct: shared data plus procedures, with the language/runtime guaranteeing that **only one process executes inside the monitor at a time**. Uses **condition variables** with `wait()` and `signal()`. Java's `synchronized` is essentially a monitor.

## 5.6 ⭐⭐ The classical problems

### ⭐ (a) Producer–Consumer (bounded buffer)

A producer adds items to a buffer of size n; a consumer removes them. The producer must block when the buffer is full; the consumer when it is empty.

**Three semaphores:**
```
mutex = 1        // protects the buffer itself
empty = n        // number of empty slots
full  = 0        // number of filled slots
```

```
Producer:                        Consumer:
  wait(empty);                     wait(full);
  wait(mutex);                     wait(mutex);
    add item to buffer;              remove item from buffer;
  signal(mutex);                   signal(mutex);
  signal(full);                    signal(empty);
```

💡 **Why `empty` and `full` are separate counters:** `empty` blocks the producer when there is no room; `full` blocks the consumer when there is nothing to take. `mutex` separately ensures they never modify the buffer simultaneously.

⚠⚠ ⭐ **The order of the two `wait()`s matters.** If the producer did `wait(mutex)` **before** `wait(empty)`, then when the buffer is full it would hold the mutex while blocking on `empty` — and the consumer could never acquire the mutex to make room. ⭐ **Deadlock.** Always acquire the counting semaphore **before** the mutex.

### ⭐ (b) Readers–Writers

Many readers may read **concurrently** (reading does not modify anything). A writer needs **exclusive** access.

| Variant | Priority | ⭐ Problem |
|---|---|---|
| First | Readers | ⭐ **Writers can starve** (a continuous stream of readers never lets a writer in) |
| Second | Writers | ⭐ **Readers can starve** |
| Third | Neither | No starvation |

### ⭐ (c) Dining Philosophers

Five philosophers around a table, five forks between them. Each needs **both adjacent forks** to eat.

⭐ **The deadlock:** if all five simultaneously pick up their **left** fork, every philosopher holds one fork and waits forever for the right one. ⭐ **Circular wait** — a perfect illustration of the deadlock conditions in §6.

⭐ **Three standard solutions:**
1. **Allow at most 4 philosophers at the table** — then at least one can always get both forks (breaks circular wait via a resource limit)
2. **Pick up both forks only if BOTH are free**, atomically (breaks hold-and-wait)
3. ⭐ **Asymmetric solution** — odd-numbered philosophers pick up **left then right**; even-numbered pick up **right then left** (breaks circular wait by imposing an ordering)

### (d) Sleeping Barber — coordinating a barber and a bounded waiting room.

---

# 6. ⭐⭐⭐ Deadlock

## 6.1 💡 The idea

📌 **Deadlock: a set of processes each holding a resource and each waiting for a resource held by another — so none can ever proceed.**

💡 **Everyday analogy: a narrow bridge with a car from each end.** Each car occupies half the bridge (holds a resource) and needs the other half (waits for a resource the other holds). Neither will reverse. Nobody moves, ever.

## 6.2 ⭐⭐ The four necessary conditions

📌 ⭐ **ALL FOUR must hold simultaneously for deadlock to occur:**

| # | Condition | 💡 Meaning |
|---|---|---|
| ⭐ **1** | ⭐ **Mutual exclusion** | At least one resource is **non-shareable** — only one process may use it at a time |
| ⭐ **2** | ⭐ **Hold and wait** | A process **holds** at least one resource while **waiting** for another |
| ⭐ **3** | ⭐ **NO preemption** | Resources **cannot be forcibly taken away** — only released voluntarily |
| ⭐ **4** | ⭐ **Circular wait** | A cycle of processes P₀ → P₁ → … → Pₙ → P₀, each waiting for the next's resource |

⚠⚠ ⭐ **Condition 3 is "NO PREEMPTION".** Options that say simply "preemption" are stating the **opposite** of the actual condition. ⭐ **This is the most common trap in the entire Operating Systems section.**

💡 **Why all four are necessary:** remove any one and deadlock becomes impossible. Shareable resources → no exclusion problem. Request everything at once → no hold-and-wait. Preemptible resources → the OS can break the tie. No cycle → someone at the end of the chain can always proceed.

## 6.3 ⭐ Resource Allocation Graph (RAG)

Processes are circles, resource types are rectangles (with a dot per instance).
- **Request edge** P → R
- **Assignment edge** R → P

📌 ⭐ **With SINGLE instances of each resource type: a cycle ⟺ deadlock.**
📌 ⭐ **With MULTIPLE instances: a cycle is NECESSARY but NOT SUFFICIENT.**

💡 **Why multiple instances break the equivalence:** a cycle may involve a resource type with a spare instance held by a process *outside* the cycle. When that process releases it, the cycle resolves. So the cycle was a false alarm.

## 6.4 ⭐⭐ The four handling strategies

| Strategy | 💡 Approach | Cost |
|---|---|---|
| ⭐ **Prevention** | ⭐ **Structurally make one of the four conditions IMPOSSIBLE, in advance** | Low resource utilisation |
| ⭐ **Avoidance** | ⭐ **Decide DYNAMICALLY, per request:** grant it only if the system stays in a **safe state** → ⭐ **Banker's algorithm** | Needs advance knowledge of maximum needs |
| **Detection** | Let deadlock happen; find it with a **wait-for graph** or the detection algorithm | Detection algorithm overhead |
| **Recovery** | Terminate processes, or **preempt/roll back** resources (needs checkpointing). Victim chosen by cost | Lost work |
| **Ignore** | ⭐ The **ostrich algorithm** — what most general-purpose OSs (Linux, Windows) actually do, on the grounds that deadlock is rare and a reboot is cheaper than the machinery | Occasional hang |

⭐ **Prevention techniques, by condition:**
- Break **mutual exclusion** → make resources shareable (rarely possible)
- Break **hold-and-wait** → require a process to request **all** its resources at once, up front (poor utilisation)
- Break **no preemption** → allow the OS to take resources back (only works for preemptible resources like CPU or memory, not printers or locks)
- ⭐ Break **circular wait** → impose a **total ordering on resource types** and require requests in increasing order. *This is the most practical prevention technique, and it is what real lock-ordering conventions do.*

⚠⚠ ⭐ **Prevention vs avoidance:** prevention makes a condition *impossible* by design; **avoidance** allows all four conditions but *checks each request* to keep the system safe. ⭐ **Banker's algorithm is AVOIDANCE, not prevention.**

## 6.5 ⭐⭐⭐ Banker's algorithm

### 💡 The idea

💡 **Analogy: a banker with limited cash and several borrowers.** Each borrower declares a maximum credit line up front. The banker grants a withdrawal only if, afterwards, there is still some order in which **every** borrower could be fully funded and repay. Otherwise the request is refused (the borrower waits) — even if the cash is physically available.

**Data structures:**
- **Available[m]** — units of each resource type currently free
- **Max[n][m]** — each process's declared maximum need
- **Allocation[n][m]** — what each process currently holds
- 📌 ⭐ **Need[i][j] = Max[i][j] − Allocation[i][j]**

### ⭐ The safety algorithm

```
Work = Available
Finish[i] = false for all i

repeat:
    find a process i with Finish[i] == false and Need[i] ≤ Work
    if found:
        Work = Work + Allocation[i]      // pretend it finishes and releases
        Finish[i] = true
    else: break

if all Finish[i] == true → the state is SAFE (and the order found is a SAFE SEQUENCE)
else                     → UNSAFE
```

💡 **Reading the loop:** find someone you can fully satisfy right now; assume they finish and return everything; that gives you more resources, which may let you satisfy the next process; repeat.

### 🔢 Full worked example

3 resource types A, B, C. **Available = (3, 3, 2).**

| P | Allocation (A B C) | Max (A B C) | ⭐ Need = Max − Alloc |
|---|---|---|---|
| P0 | 0 1 0 | 7 5 3 | **7 4 3** |
| P1 | 2 0 0 | 3 2 2 | **1 2 2** |
| P2 | 3 0 2 | 9 0 2 | **6 0 0** |
| P3 | 2 1 1 | 2 2 2 | **0 1 1** |
| P4 | 0 0 2 | 4 3 3 | **4 3 1** |

**Run the safety algorithm.** Work = (3, 3, 2).

| Step | Try | Need ≤ Work? | Action | New Work |
|---|---|---|---|---|
| 1 | P0: (7,4,3) | 7 > 3 ❌ | skip | (3,3,2) |
| | P1: (1,2,2) | ✅ | run P1, add its Allocation (2,0,0) | **(5,3,2)** |
| 2 | P0: (7,4,3) | ❌ | skip | |
| | P2: (6,0,0) | 6 > 5 ❌ | skip | |
| | P3: (0,1,1) | ✅ | run P3, add (2,1,1) | **(7,4,3)** |
| 3 | P0: (7,4,3) | ✅ | *could run, but let's continue in index order* | |
| | P4: (4,3,1) | ✅ | run P4, add (0,0,2) | **(7,4,5)** |
| 4 | P0: (7,4,3) | ✅ | run P0, add (0,1,0) | **(7,5,5)** |
| 5 | P2: (6,0,0) | ✅ | run P2, add (3,0,2) | **(10,5,7)** |

All five finished → ⭐ **the state is SAFE**, with safe sequence **P1 → P3 → P4 → P0 → P2**.

### 🔢 Now handle a request

**P1 requests (1, 0, 2).**
1. Is Request ≤ Need? (1,0,2) ≤ (1,2,2) ✅
2. Is Request ≤ Available? (1,0,2) ≤ (3,3,2) ✅
3. **Pretend to grant it:** Available becomes (2,3,0); P1's Allocation becomes (3,0,2); P1's Need becomes (0,2,0).
4. Run the safety algorithm on this new state. Work = (2,3,0): P1's Need (0,2,0) ≤ Work ✅ → Work = (5,3,2) → P3 (0,1,1) ✅ → Work = (7,4,3) → P0, P2, P4 all satisfiable.
⭐ **Safe → grant the request.**

### ⭐ Safe vs unsafe vs deadlocked

📌 ⭐ **SAFE state ⇒ NO deadlock** (a safe sequence exists, so the OS can always avoid it).
📌 ⭐ **UNSAFE state ⇒ deadlock is POSSIBLE, not certain.**

⚠ ⭐ That asymmetry is asked directly. An unsafe state may still resolve happily if processes request less than their declared maximum — the algorithm is conservative because it plans for the worst case.

**Deadlock prevention in DBMS** uses different, timestamp-based schemes — see Week 7's wait-die and wound-wait.

---

# 7. ⭐⭐⭐ Memory management

## 7.1 💡 The core problem

Several processes must share one physical RAM. Three requirements:
1. **Relocation** — a program must run wherever it is loaded, not at a fixed address
2. **Protection** — process A must not be able to read or write process B's memory
3. **Efficient use** — do not waste RAM

## 7.2 Contiguous allocation and its placement strategies

The simplest scheme: give each process one contiguous block.

| Strategy | Rule | 💡 Note |
|---|---|---|
| **First fit** | The first hole big enough | ⭐ Fastest search |
| **Best fit** | The **smallest** hole big enough | ⚠ Sounds best, but ⭐ **leaves tiny useless slivers** and is slow (must scan all holes) |
| **Worst fit** | The **largest** hole | Generally the worst performer — destroys big holes |
| **Next fit** | First fit, resuming from where the last search stopped | Spreads allocation |

🔢 Holes of 100, 500, 200, 300, 600 KB; a process needs 212 KB:
- **First fit** → the 500 KB hole (leaving 288)
- **Best fit** → the 300 KB hole (leaving 88)
- **Worst fit** → the 600 KB hole (leaving 388)

## 7.3 ⭐⭐ Fragmentation

### 💡 The two kinds

⭐ **Internal fragmentation** — the allocated block is **larger than requested**, and the leftover is **inside** the block, unusable by anyone else.
🔢 A process needs 4100 bytes; pages are 4096 bytes, so it gets 2 pages = 8192 bytes. **4092 bytes are wasted inside** the second page.

⭐ **External fragmentation** — there **is** enough total free memory, but it is **split into non-contiguous pieces**, none big enough.
🔢 Free holes of 50 KB, 60 KB, 40 KB = 150 KB free. A 100 KB process **cannot be loaded**, despite 150 KB being available.

📌 ⭐⭐ **PAGING → INTERNAL fragmentation** (fixed-size frames, so the last page is partly wasted)
📌 ⭐⭐ **SEGMENTATION → EXTERNAL fragmentation** (variable-size segments leave awkward gaps)

⚠ **Memorise this pairing — it is asked almost every exam.**

⭐ **Compaction** cures external fragmentation by sliding all processes together to merge the holes. But it requires **relocatable** code and is expensive (all that copying), so it is rarely done at run time.

## 7.4 ⭐⭐⭐ Paging

### 💡 The idea

External fragmentation exists because processes need **contiguous** memory. Paging removes that requirement:

- Divide the **logical** address space into fixed-size **PAGES**
- Divide **physical** memory into equal-size **FRAMES**
- A **page table** per process maps page numbers → frame numbers

⭐ **A process's pages can now be scattered anywhere in physical memory** — contiguity is no longer needed, so external fragmentation vanishes entirely.

```
Logical (process view)        Page table        Physical memory
   Page 0  ─────────────────►  0 → 5   ────────►  Frame 5
   Page 1  ─────────────────►  1 → 2   ────────►  Frame 2
   Page 2  ─────────────────►  2 → 9   ────────►  Frame 9
```
The process sees a neat contiguous space; the reality is scattered.

### ⭐ Address translation

A logical address splits into two fields:
```
┌──────────────────┬──────────────┐
│  Page number (p) │  Offset (d)  │
└──────────────────┴──────────────┘
```
The page number indexes the page table to get a frame number; the offset is copied unchanged (a byte's position within a page is the same as within a frame).

📌 ⭐ **Offset bits = log₂(page size)**
📌 ⭐ **Number of pages = virtual address space ÷ page size**
📌 ⭐ **Page table size = number of pages × size of one page-table entry**

### 🔢⭐ The classic sizing question

**32-bit virtual address, 4 KB page size, 4-byte page-table entry.**
```
Offset bits      = log₂(4096) = 12
Page number bits = 32 − 12 = 20
Number of pages  = 2²⁰ = 1,048,576
Page table size  = 2²⁰ × 4 bytes = 2²² = 4 MB
```
⭐ Answer: **4 MB — PER PROCESS.**

⭐ **Why this matters:** with 100 processes that is 400 MB of page tables, most of it for address ranges the processes never touch. This impracticality is precisely why **multi-level page tables**, **inverted page tables** and **hashed page tables** exist.

### 🔢 Multi-level paging

**Two-level, 32-bit address, 4 KB pages, 1024 entries per table:**
```
Offset      = 12 bits
Inner index = log₂(1024) = 10 bits
Outer index = 32 − 12 − 10 = 10 bits
```
⭐ Now the outer table has only 1024 entries (4 KB), and inner tables are allocated **only for address ranges actually in use**. Sparse address spaces cost almost nothing.

### ⭐ Page-table entry fields

Frame number · ⭐ **valid/invalid bit** (is this page in memory?) · protection bits (read/write/execute) · ⭐ **dirty (modified) bit** (has it been written? — needed to decide whether to write it back on eviction) · **reference bit** (used by LRU approximations) · caching-disabled bit.

### ⭐⭐ TLB (Translation Lookaside Buffer)

### 💡 The problem it solves

Every memory access now needs **two** memory accesses: one to read the page table, one to get the data. That doubles memory latency — unacceptable.

⭐ **The TLB is a small, very fast, fully-associative CACHE of recently used page-table entries**, inside the MMU.

⭐ On a **TLB hit**, translation costs no extra memory reference at all. Because of locality of reference (Week 2), hit rates of 95–99% are typical.

📌 ⭐ **Effective Access Time (EAT) with a TLB, single-level page table:**
**EAT = h × (t_TLB + t_mem) + (1 − h) × (t_TLB + 2·t_mem)**

💡 **Reading it:** on a hit you pay the TLB lookup plus one memory access for the data. On a miss you pay the TLB lookup, **one memory access to read the page table**, and then one for the data — hence 2·t_mem.

### 🔢 Worked example

**TLB access 20 ns, memory access 100 ns, hit ratio 80%.**
```
EAT = 0.8 × (20 + 100) + 0.2 × (20 + 100 + 100)
    = 0.8 × 120 + 0.2 × 220
    = 96 + 44
    = 140 ns
```
⭐ Answer: **140 ns**

⚠⚠ ⭐ **Variants of this formula appear, and the question must tell you which model to use:**
- Some texts **omit the TLB time on a miss** (assuming the TLB and page table are searched in parallel): `EAT = 0.8(120) + 0.2(200) = 136 ns`
- Some **omit TLB time entirely**: `EAT = 0.8(100) + 0.2(200) = 120 ns`

⭐ **Read the wording. If it says "the TLB is searched first, and on a miss the page table is accessed", use the formula above.**

## 7.5 ⭐ Segmentation

### 💡 The idea

Paging is invisible to the programmer — pages are arbitrary fixed slices with no relation to program structure. **Segmentation** instead divides memory into **logically meaningful, variable-size** units: a code segment, a data segment, a stack segment, one per function or object.

Address = **segment number | offset**. A **segment table** holds a **base** and a **limit** per segment.

✅ **Advantages:** protection and sharing are natural (mark the code segment read-only and share it between processes running the same program); segments match the programmer's mental model.
❌ ⭐ **Suffers EXTERNAL fragmentation** because segments vary in size.

⭐ **Segmented paging** combines both: divide memory into segments, then **page each segment**. This gets segmentation's logical structure with paging's freedom from external fragmentation. Used by x86.

## 7.6 ⭐⭐⭐ Virtual memory

### 💡 The idea

Physical RAM is 8 GB but you want to run a program needing 20 GB — or twenty programs each needing 1 GB.

⭐ **Virtual memory** lets a process's logical address space **exceed** physical memory, by keeping only the **actively used** pages in RAM and the rest on disk (the **swap space** or **backing store**).

⭐ **Why it works:** the **locality of reference** principle again. At any moment a process is only touching a small **working set** of its pages. The rest can sit on disk unnoticed.

⭐ **Demand paging:** do not load a page until it is actually referenced. Programs start faster, and pages that are never touched are never loaded.

### ⭐ Page fault handling

📌 A **page fault** occurs when a referenced page's **valid bit is 0** — it is not in memory.

**The sequence:**
1. The MMU raises a trap to the OS
2. The OS checks the reference is **legal** (within the process's address space) — if not, segmentation fault
3. Find a **free frame**; if none, run **page replacement** (§7.7) to evict one
4. If the evicted page is **dirty**, write it to disk first
5. **Schedule a disk read** for the wanted page — the process blocks
6. Update the page table (set the frame number, valid bit = 1)
7. ⭐ **Restart the faulting instruction** (it never completed)

📌 ⭐ **EAT with page faults = (1 − p) × t_memory + p × t_page_fault_service**

### 🔢⭐ The eye-opening calculation

**Memory access 100 ns, page fault service 8 ms (= 8,000,000 ns), fault rate p = 0.001 (0.1%).**
```
EAT = 0.999 × 100 + 0.001 × 8,000,000
    = 99.9 + 8000
    = 8099.9 ns ≈ 8.1 μs
```
⭐ **A 0.1% fault rate makes memory 81× slower than the 100 ns baseline.**

💡 **Why so brutal:** a page fault costs a **disk access**, which is ~80,000 times slower than RAM. Even a rare fault dominates the average. ⭐ **This is why fault rates must be kept in the 10⁻⁶ range**, and why thrashing (§7.8) is catastrophic.

🔢 **Working backwards:** for EAT ≤ 110 ns (10% degradation), we need `100 + p × 8,000,000 ≤ 110` → **p ≤ 1.25 × 10⁻⁶** — fewer than one fault per 800,000 accesses.

## 7.7 ⭐⭐⭐ Page replacement algorithms

### 💡 The idea

Memory is full and a new page must come in. Which resident page do you evict? A good choice is one that will not be needed soon.

| Algorithm | Rule | ⭐ Belady's anomaly? |
|---|---|---|
| ⭐ **FIFO** | Evict the **oldest** resident page | ⭐ **✅ YES** |
| ⭐ **Optimal (OPT/MIN)** | Evict the page whose **next use is furthest in the future** | ❌ No |
| ⭐ **LRU** | Evict the **least recently used** | ❌ No |
| **LFU / MFU** | Least / most frequently used | Possible |
| **Clock / Second chance** | FIFO + a **reference bit**: give a page a second chance if its bit is set | Approximates LRU cheaply |

⭐ **OPT is unimplementable** — it requires knowing the future reference string. It exists purely as a **benchmark**: if your algorithm is close to OPT, it is good.

⭐ **LRU is the best practical algorithm**, because temporal locality means recently used pages are likely to be used again. Exact LRU needs a timestamp or a stack update on **every** memory reference, which is too expensive in hardware — so real systems use **clock/second-chance** approximations.

### ⭐⭐ Belady's anomaly

📌 ⭐ **Belady's anomaly: giving the process MORE frames causes MORE page faults.**

This is deeply counter-intuitive — more memory should never hurt. But it happens.

📌 ⭐ **It occurs in FIFO. It CANNOT occur in LRU or OPT**, because those are **stack algorithms**: the set of pages held with n frames is always a **subset** of the set held with n+1 frames, so extra frames can only help.

### 🔢⭐⭐ The standard demonstration

**Reference string: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5**

**FIFO with 3 frames:**

| Ref | Frames (oldest → newest) | Fault? |
|---|---|---|
| 1 | [1] | ✅ |
| 2 | [1, 2] | ✅ |
| 3 | [1, 2, 3] | ✅ |
| 4 | [2, 3, 4] — evict 1 | ✅ |
| 1 | [3, 4, 1] — evict 2 | ✅ |
| 2 | [4, 1, 2] — evict 3 | ✅ |
| 5 | [1, 2, 5] — evict 4 | ✅ |
| 1 | [1, 2, 5] | hit |
| 2 | [1, 2, 5] | hit |
| 3 | [2, 5, 3] — evict 1 | ✅ |
| 4 | [5, 3, 4] — evict 2 | ✅ |
| 5 | [5, 3, 4] | hit |

⭐ **FIFO, 3 frames: 9 faults**

**FIFO with 4 frames:**

| Ref | Frames | Fault? |
|---|---|---|
| 1 | [1] | ✅ |
| 2 | [1,2] | ✅ |
| 3 | [1,2,3] | ✅ |
| 4 | [1,2,3,4] | ✅ |
| 1 | hit | |
| 2 | hit | |
| 5 | [2,3,4,5] — evict 1 | ✅ |
| 1 | [3,4,5,1] — evict 2 | ✅ |
| 2 | [4,5,1,2] — evict 3 | ✅ |
| 3 | [5,1,2,3] — evict 4 | ✅ |
| 4 | [1,2,3,4] — evict 5 | ✅ |
| 5 | [2,3,4,5] — evict 1 | ✅ |

⭐ **FIFO, 4 frames: 10 faults**

⭐⭐ **9 faults with 3 frames, 10 faults with 4 frames. Belady's anomaly demonstrated.** ✅

**Same string, LRU with 3 frames: 10 faults. OPT with 3 frames: 7 faults.**

⚠ ⭐ Note that here **LRU (10) is worse than FIFO (9)**. LRU is usually better, but not always — the guarantee is only that LRU never suffers Belady's anomaly, not that it always wins.

## 7.8 ⭐⭐ Thrashing

### 💡 The idea

📌 ⭐ **Thrashing: the system spends more time paging than executing.**

**How it spirals:**
1. Too many processes are admitted, so each gets very few frames
2. Each process faults constantly (its working set does not fit)
3. Processes block on disk I/O, so CPU utilisation **drops**
4. ⭐ The OS sees low CPU utilisation and — trying to help — **admits more processes**
5. Which makes everything worse. **Collapse.**

⭐ The signature is a graph where CPU utilisation rises with the degree of multiprogramming, peaks, then **falls off a cliff**.

### ⭐ Cures

| Cure | 💡 How |
|---|---|
| ⭐ **Working set model** | Track the set of pages a process referenced in its last **Δ** references — its **working set**. Give each process enough frames for its working set. If the total demand exceeds available frames, ⭐ **suspend a process** |
| **Page-Fault Frequency (PFF)** | Monitor each process's fault rate; give more frames if it is too high, take frames away if too low |
| Reduce the degree of multiprogramming | Directly, by suspending/swapping out processes |
| Add physical memory | The blunt fix |

⭐ **Frame allocation policies:** equal vs proportional (by process size).
⭐ **Local replacement** (a process may only evict its **own** frames — isolates processes from each other) vs **global replacement** (any frame may be taken — better utilisation, but one greedy process can cause another to thrash).

---

# 8. ⭐⭐ File systems

## 8.1 Concepts

**File attributes:** name, identifier (inode number), type, location, size, protection, timestamps.
**Operations:** create, open, read, write, seek, close, delete, truncate.
**Access methods:** **sequential** · **direct/random** · **indexed**.
**Directory structures:** single-level → two-level → **tree** → **acyclic graph** (shared subdirectories) → general graph.

⭐ **Hard link vs symbolic (soft) link:**

| | ⭐ **Hard link** | ⭐ **Soft / symbolic link** |
|---|---|---|
| What it is | Another **directory entry pointing to the same inode** | A **file containing a path string** |
| Across file systems | ❌ No | ✅ Yes |
| If the original is deleted | ⭐ The data **survives** (the inode's link count just decreases) | ⭐ The link **dangles** (broken) |
| Can link to a directory | Usually not | ✅ Yes |

## 8.2 ⭐⭐ File allocation methods

### 💡 The three approaches

**Contiguous allocation** — store the whole file in consecutive blocks.
```
File A: blocks 5,6,7,8      File B: blocks 12,13
```
✅ Excellent sequential reads (no seeking); direct access is trivial arithmetic.
❌ ⭐ **External fragmentation**; and a file **cannot easily grow** (the neighbouring blocks may be occupied).

**Linked allocation** — each block contains a pointer to the next.
```
File A: 5 → 19 → 3 → 27 → NULL
```
✅ No external fragmentation; files grow freely.
❌ ⭐ **Direct access is impossible** — to read block 50 you must follow 50 pointers. ⚠ And one corrupted pointer loses the entire rest of the file. (**FAT** is a variant that keeps all the pointers in one table, which helps.)

⭐ **Indexed allocation** — one **index block** holds all the file's block pointers.
```
File A's index block: [5, 19, 3, 27, ...]
```
✅ ⭐ **Direct access in O(1)** (just look up the i-th pointer) **AND no external fragmentation**.
❌ The index block itself is overhead, and a small file wastes a whole index block.

| Method | ⭐ Direct access | ⭐ External fragmentation | File growth |
|---|---|---|---|
| **Contiguous** | ✅ Yes | ⭐ **✅ Suffers** | ❌ Hard |
| **Linked** | ⭐ **❌ No** | ❌ None | ✅ Easy |
| ⭐ **Indexed** | ⭐ **✅ Yes** | ⭐ **❌ None** | ✅ Easy |

⭐ **Exam answer: "which method supports efficient direct access WITHOUT external fragmentation?" → INDEXED allocation.**

### ⭐ The UNIX inode

An inode holds a file's attributes plus a clever hybrid of pointers:
- ~**12 direct** block pointers (small files need nothing more)
- 1 **single-indirect** pointer (→ a block full of pointers)
- 1 **double-indirect** pointer (→ a block of pointers to blocks of pointers)
- 1 **triple-indirect** pointer

⭐ **Why this design:** small files (the vast majority) are accessed with **zero** extra reads; huge files are still possible.

### 🔢 Maximum file size calculation

**10 direct pointers, 1 single-indirect, 1 double-indirect. Block size 4 KB, pointer size 4 bytes.**
```
Pointers per block = 4096 / 4 = 1024

Direct:            10 × 4 KB          = 40 KB
Single indirect:   1024 × 4 KB        = 4 MB
Double indirect:   1024 × 1024 × 4 KB = 4 GB
                                  Total ≈ 4 GB + 4 MB + 40 KB
```
⭐ Answer: **≈ 4 GB**

**Free-space management:** **bit vector / bitmap** (one bit per block — simple and allows fast contiguous-run searches) · linked list of free blocks · grouping · counting.

## 8.3 ⭐⭐ Disk scheduling

### 💡 The idea

Recall from Week 2 that disk access is dominated by **seek time** — physically moving the arm. Several requests are typically pending, and the **order** you serve them in dramatically changes total head movement.

| Algorithm | Rule | ⭐ Starvation? | 💡 Note |
|---|---|---|---|
| **FCFS** | Serve in arrival order | ❌ No | Fair, but the head may swing wildly across the disk |
| ⭐ **SSTF** | **Shortest Seek Time First** — nearest request | ⭐ **✅ YES** | Good throughput, but a request at the far edge can be postponed forever as nearer ones keep arriving |
| ⭐ **SCAN** | Sweep to one end serving requests, then **reverse** | ❌ No | ⭐ **The "ELEVATOR" algorithm** — a lift goes all the way up, then all the way down |
| ⭐ **C-SCAN** | Sweep one way serving, then **jump back to the start without serving** | ❌ No | ⭐ **More UNIFORM wait times** — every cylinder is visited at the same interval |
| **LOOK / C-LOOK** | Like SCAN/C-SCAN but reverse at the **last request**, not the physical disk end | ❌ No | Less wasted movement |

⭐ **SSTF starves; SCAN and C-SCAN bound the wait.** That is the standard exam contrast.
⭐ **Why C-SCAN over SCAN:** in SCAN, a cylinder just behind the head gets served twice in quick succession (on the way out and back), while one just ahead waits a full sweep. C-SCAN's one-directional service makes the waiting time uniform.

### 🔢⭐ The standard numerical

**Head at cylinder 53. Request queue: 98, 183, 37, 122, 14, 124, 65, 67. Disk has cylinders 0–199.**

**FCFS** — serve in order:
```
53→98→183→37→122→14→124→65→67
Movement = 45 + 85 + 146 + 85 + 108 + 110 + 59 + 2
```
⭐ **Total = 640 cylinders**

**SSTF** — always nearest:
```
53→65→67→37→14→98→122→124→183
Movement = 12 + 2 + 30 + 23 + 84 + 24 + 2 + 59
```
⭐ **Total = 236 cylinders**

**SCAN** — ⚠ ⭐ **the answer depends on the initial DIRECTION, so the question must state it.**

*Moving **downward** first (the standard textbook version):*
```
53→37→14→0→[reverse]→65→67→98→122→124→183
Movement = (53 − 0) + (183 − 0) = 53 + 183
```
⭐ **Total = 236 cylinders**

*Moving **upward** first:*
```
53→65→67→98→122→124→183→199→[reverse]→37→14
Movement = (199 − 53) + (199 − 14) = 146 + 185
```
⭐ **Total = 331 cylinders**

*(**LOOK** variant — reverse at the **last request** instead of the disk end. Downward-first: (53−14) + (183−14) = 39 + 169 = **208**.)*

**C-SCAN** (upward to 199, jump to 0, continue upward):
```
53→65→67→98→122→124→183→199→[jump to 0]→14→37
Movement = (199 − 53) + (199 − 0) + (37 − 0) = 146 + 199 + 37
```
⭐ **Total = 382 cylinders**

⚠ ⭐ **Always state your assumption about whether the head travels to the physical end (SCAN/C-SCAN) or only to the last request (LOOK/C-LOOK)** — both conventions appear, and the numbers differ.

## 8.4 RAID levels (awareness)

| Level | 💡 Technique | Redundancy |
|---|---|---|
| **RAID 0** | **Striping** — data split across disks | ⭐ **None** — pure performance; one disk failure loses everything |
| **RAID 1** | **Mirroring** — full copies | Survives 1 failure; 50% capacity overhead |
| ⭐ **RAID 5** | Striping + **distributed parity** | ⭐ Needs **≥ 3 disks**; survives **1** failure |
| **RAID 6** | Double distributed parity | Survives **2** failures |
| **RAID 10** | Mirrored stripes | Performance + redundancy, 50% overhead |

---

# 9. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| Multiprogramming goal / multitasking goal | Maximise CPU utilisation / minimise response time |
| Mode switch vs context switch | Privilege change vs **process** change |
| Microkernel | Services in **user space**; more reliable, slower |
| `fork()` returns | **0 to child, PID to parent**, −1 on failure |
| n forks → processes / children | **2ⁿ / 2ⁿ − 1** |
| `exec()` | **Replaces** the image; does not create a process |
| **Running → Ready** | ⭐ **Preemption** |
| **Running → Waiting** | ⭐ **I/O request** |
| Zombie | **Terminated**, parent hasn't `wait()`ed |
| Orphan | **Parent died** |
| Threads share | Code, data, **heap**, files |
| Threads own | ⭐ **Stack, registers, PC** |
| TAT / WT | CT − AT / TAT − BT |
| Minimum average WT | ⭐ **SJF** |
| FCFS problem | **Convoy effect** |
| RR with huge quantum | Becomes **FCFS** |
| Starvation-free | **FCFS, Round Robin** |
| Priority starvation fix | ⭐ **Aging** |
| Best response time | Round Robin |
| Fastest IPC | **Shared memory** |
| Works across machines | Message passing |
| Critical-section requirements | ⭐ **Mutual exclusion, progress, bounded waiting** |
| Peterson's solution | Satisfies **all three** |
| Counting semaphore init n | Allows **n** processes |
| Semaphore vs mutex | No ownership / **has ownership** |
| Producer–consumer semaphores | mutex=1, empty=n, full=0 |
| Wrong wait() order causes | **Deadlock** |
| Dining philosophers deadlock | All grab the **left** fork |
| Deadlock conditions | Mutual exclusion, hold-and-wait, ⭐ **NO preemption**, circular wait |
| Cycle in RAG, single instance | ⭐ **Deadlock** |
| Cycle, multiple instances | Necessary, **not sufficient** |
| Banker's algorithm is | ⭐ **AVOIDANCE** |
| Need | Max − Allocation |
| Safe state | ⭐ **No deadlock** |
| Unsafe state | Deadlock **possible**, not certain |
| Most practical prevention | **Ordering resource types** |
| ⭐ Paging fragmentation | ⭐ **Internal** |
| ⭐ Segmentation fragmentation | ⭐ **External** |
| Compaction cures | External fragmentation |
| Offset bits | log₂(page size) |
| Page table size (32-bit, 4 KB, 4 B PTE) | ⭐ **4 MB** |
| TLB is | A **cache of page-table entries** |
| EAT with TLB | h(t_TLB + t_mem) + (1−h)(t_TLB + 2t_mem) |
| Page fault trigger | **Valid bit = 0** |
| After servicing a fault | ⭐ **Restart the instruction** |
| ⭐ Belady's anomaly | ⭐ **FIFO only** |
| Immune to Belady's | **LRU, OPT** (stack algorithms) |
| Unimplementable replacement | ⭐ **Optimal (OPT)** |
| Best practical replacement | **LRU** (approximated by clock) |
| Thrashing cure | ⭐ **Working set model** |
| Direct access, no external fragmentation | ⭐ **Indexed allocation** |
| No direct access | Linked allocation |
| inode structure | Direct + single/double/triple indirect |
| Hard link vs soft link | Same inode / path string |
| Elevator algorithm | ⭐ **SCAN** |
| Disk scheduling with starvation | ⭐ **SSTF** |
| Most uniform wait | **C-SCAN** |
| RAID 0 / 1 / 5 | Striping / mirroring / striping + distributed parity |

---

# 10. ⚠ Common traps

1. ⭐⭐ **"NO preemption" is the deadlock condition** — not "preemption".
2. ⭐⭐ **Running → Ready is PREEMPTION; Running → Waiting is I/O.**
3. ⭐⭐ **Belady's anomaly occurs in FIFO only** — LRU and OPT are immune.
4. ⭐⭐ **Paging = internal fragmentation; segmentation = external.**
5. ⭐ **Banker's algorithm is avoidance, not prevention.**
6. ⭐ **Safe ⇒ no deadlock, but unsafe does NOT guarantee deadlock.**
7. ⭐ **Threads share the heap but NOT the stack.**
8. ⭐ **A mode switch is not a context switch.**
9. ⭐ **`exec()` does not create a process** — it replaces the image.
10. ⭐ **EAT formulas vary by model** — check whether TLB time is counted on a miss and whether the searches are parallel.
11. ⭐ **Zombie vs orphan are opposite** situations.
12. ⭐ **Semaphore ≠ mutex** — mutexes have ownership.
13. **A cycle with multiple resource instances is not sufficient for deadlock.**
14. **In the producer–consumer solution, acquire the counting semaphore BEFORE the mutex.**
15. **Critical-section requirements ≠ ACID properties.**
16. **SCAN vs LOOK** — does the head go to the disk end or only to the last request? State your assumption.
17. **SJF is optimal but not implementable** (burst times are unknown).

---

# 11. Practice

- GATE: [`Paper2_S08_Operating_System/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S08_Operating_System/) — **343 questions**
- State-PSC level: [`Paper2_S08_Operating_System/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S08_Operating_System/) — **463 questions**
- Test: [`Week_06_Test.md`](../04_Mock_Tests/Week_06_Test.md)

**Priority order if short on time:** ⭐ **scheduling Gantt-chart numericals** → page-replacement traces & Belady's anomaly → the four deadlock conditions + Banker's algorithm → paging sizing + TLB EAT → the three critical-section requirements & classical problems → disk scheduling numericals → file allocation methods.

⭐ **This is the most numerical section in Paper-II.** Practise Gantt charts, page-replacement traces, Banker's algorithm and disk-scheduling totals until they are mechanical. They are guaranteed marks if you can execute them in under two minutes.
