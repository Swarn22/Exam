# Week 6 Question Bank — Operating Systems

**Syllabus §8** · 183 questions · Practice set · +1 / −0.33 marking

> Grounded entirely in `05_Notes/Week_06_Operating_Systems.md`. Draw the Gantt chart / write out Need = Max − Alloc before answering the numericals.

---

## Part A — OS types, kernel/user mode, system calls, fork/exec

**Q1.** The primary goal of a **multiprogramming** operating system is to
(A) minimise response time
(B) maximise CPU utilisation
(C) meet hard real-time deadlines
(D) minimise the number of context switches

**Q2.** The primary goal of a **time-sharing (multitasking)** operating system is to
(A) maximise CPU utilisation
(B) minimise response time
(C) maximise batch throughput
(D) maximise total memory used

**Q3.** Which statement correctly distinguishes multiprogramming from multitasking?
(A) Multiprogramming switches only when a process blocks; multitasking also switches on a timer
(B) Multitasking never preempts a running process
(C) Multiprogramming requires multiple physical CPUs
(D) They are two names for the same thing

**Q4.** In a **hard real-time** system, a missed deadline is
(A) a tolerable performance degradation
(B) a system failure
(C) always silently ignored
(D) a way to improve throughput

**Q5.** Video streaming, where an occasional dropped frame is acceptable, is best classified as
(A) a hard RTOS
(B) a soft RTOS
(C) a batch system
(D) a distributed system

**Q6.** A characteristic of a **batch** operating system is that
(A) it relies on heavy user interaction
(B) jobs are collected and run in groups with no user interaction
(C) it preempts on every timer tick
(D) it presents many machines as one

**Q7.** Which of the following can **not** be executed in user mode?
(A) An integer addition
(B) A privileged instruction such as loading the page-table base register
(C) A normal function call
(D) Reading a general-purpose register

**Q8.** A **mode switch** (user → kernel) is triggered by all of the following **except**
(A) a system call
(B) an interrupt
(C) a trap/exception
(D) an ordinary arithmetic instruction

**Q9.** Which statement about mode switch vs context switch is TRUE?
(A) A mode switch changes which process is running
(B) A system call always causes a context switch
(C) A mode switch changes the privilege level of the same process
(D) They are identical operations

**Q10.** A **microkernel** architecture
(A) keeps all services inside the kernel
(B) runs drivers and file systems in user space — more reliable but slower due to message passing
(C) is always faster than a monolithic kernel
(D) contains no IPC mechanism

**Q11.** A **monolithic** kernel
(A) suffers heavy message-passing overhead
(B) puts all services inside the kernel — fast, but a bug anywhere can crash everything
(C) runs its drivers in user space
(D) is always more reliable than a microkernel

**Q12.** Windows NT and macOS use kernels best described as
(A) pure microkernels
(B) pure monolithic kernels
(C) hybrid kernels
(D) exokernels

**Q13.** A **system call** is
(A) merely an ordinary library function
(B) the only doorway from user mode into the kernel
(C) a hardware interrupt raised by a device
(D) the same thing as a context switch

**Q14.** Which of the following is a **process-control** system call?
(A) `open()`
(B) `chmod()`
(C) `fork()`
(D) `getpid()`

**Q15.** A successful `fork()` returns
(A) 0 to both parent and child
(B) 0 to the child and the child's PID to the parent (−1 on failure)
(C) the child's PID to the child
(D) −1 to the child on success

**Q16.** After **n** consecutive `fork()` calls, the total number of processes in existence is
(A) n
(B) 2n
(C) 2ⁿ
(D) 2ⁿ − 1

**Q17.** A program executes three `fork()` calls in a row. How many **child** processes are created?
(A) 3
(B) 7
(C) 8
(D) 6

**Q18.** The `exec()` system call
(A) creates a new process
(B) replaces the current process's memory image and does not return on success
(C) duplicates the calling process
(D) returns the child's PID

**Q19.** The standard shell pattern for running a new program is
(A) `exec()` then `fork()`
(B) `fork()` then `exec()`
(C) `wait()` then `fork()`
(D) `exec()` then `wait()`

**Q20.** A program executes four `fork()` calls in a row. How many processes exist in total afterwards?
(A) 8
(B) 15
(C) 16
(D) 32

---

## Part B — Processes, states, PCB, zombie/orphan, threads

**Q21.** The difference between a program and a process is that
(A) a program is active while a process is passive
(B) a process is a program in execution, with a PC, registers, stack and heap
(C) they are the same thing
(D) a process is a passive file on disk

**Q22.** The transition **RUNNING → READY** is caused by
(A) an I/O request
(B) preemption / expiry of the time quantum
(C) `exit()`
(D) I/O completion

**Q23.** The transition **RUNNING → WAITING (blocked)** is caused by
(A) preemption
(B) an I/O request or waiting for an event
(C) a higher-priority process arriving
(D) quantum expiry

**Q24.** The transition **WAITING → READY** is caused by
(A) I/O completion
(B) preemption
(C) dispatch to the CPU
(D) `exit()`

**Q25.** In the process state diagram there is **no direct** transition from
(A) new → ready
(B) waiting → running
(C) running → ready
(D) ready → running

**Q26.** Which of the following does the **PCB** NOT store?
(A) The program counter
(B) The process state
(C) The full source code of the program
(D) The open-file table

**Q27.** A **zombie** process is one that
(A) is a live child whose parent has died
(B) has terminated but whose parent has not yet called `wait()`
(C) is a long-running background daemon
(D) has been suspended by the scheduler

**Q28.** An **orphan** process is one that
(A) has terminated but has not been reaped
(B) is still running but whose parent has died, and is re-parented to `init`/`systemd`
(C) is a zombie
(D) is a background daemon

**Q29.** A zombie process consumes
(A) a large amount of memory
(B) significant CPU cycles
(C) only a process-table slot
(D) disk space proportional to its size

**Q30.** Threads of the same process share all of the following **except**
(A) the code (text) section
(B) the global data section
(C) the heap
(D) the stack and registers

**Q31.** Which of the following is **private** to each thread?
(A) Open files
(B) The heap
(C) The program counter
(D) The code section

**Q32.** Each thread must have its own **stack** because
(A) it saves memory
(B) each thread has its own chain of function-call activation records
(C) the heap is too small
(D) the OS forbids sharing

**Q33.** Compared with a process context switch, a **thread** context switch (within one process) is
(A) more expensive because of a TLB flush
(B) cheaper, because the address space is shared
(C) exactly the same cost
(D) impossible

**Q34.** If one thread crashes with an unhandled fault, then
(A) other threads are never affected
(B) it can bring down the whole process
(C) only the kernel is affected
(D) it automatically restarts

**Q35.** The main drawback of **user-level threads** is that
(A) they achieve true parallelism
(B) one blocking system call blocks ALL threads of the process
(C) they are known to the kernel
(D) their switching is slow

**Q36.** An advantage of **kernel-level threads** is
(A) they are invisible to the kernel
(B) true multi-core parallelism, and one thread blocking does not block the others
(C) the fastest possible switching
(D) they need no scheduling

**Q37.** A context switch is
(A) useful computation
(B) pure overhead — register save/restore, TLB flush and cache pollution
(C) the same as a mode switch
(D) essentially free

**Q38.** Two **threads** of the same process communicate most directly via
(A) IPC mediated by the kernel
(B) shared memory, directly
(C) pipes only
(D) network sockets only

**Q39.** Two separate **processes** exchange data by
(A) sharing variables automatically
(B) inter-process communication (kernel-mediated)
(C) sharing a common stack
(D) sharing CPU registers

---

## Part C — CPU scheduling (concepts and Gantt-chart numericals)

**Q40.** Turnaround Time (TAT) equals
(A) CT − AT
(B) AT − CT
(C) CT − BT
(D) TAT − BT

**Q41.** Waiting Time (WT) equals
(A) CT − AT
(B) TAT − BT
(C) BT − TAT
(D) CT − BT

**Q42.** Response time is
(A) CT − AT
(B) (time of first CPU allocation) − AT
(C) TAT − BT
(D) the burst time

**Q43.** The main weakness of **FCFS** scheduling is
(A) starvation
(B) the convoy effect
(C) high context-switch overhead
(D) unfairness to early arrivals

**Q44.** Which algorithm gives the provably **minimum average waiting time** for jobs available together?
(A) FCFS
(B) Round Robin
(C) Shortest Job First
(D) Priority scheduling

**Q45.** SJF cannot be implemented directly because
(A) it is too slow to compute
(B) a process's future burst time is unknown
(C) it needs too much memory
(D) it causes deadlock

**Q46.** Which of the following scheduling algorithms can cause **starvation**?
(A) FCFS
(B) Round Robin
(C) SJF
(D) Both FCFS and RR

**Q47.** The **starvation-free** scheduling algorithms among the following are
(A) SJF and SRTF
(B) FCFS and Round Robin
(C) Priority and SJF
(D) SRTF and Priority

**Q48.** Starvation in **priority** scheduling is fixed by
(A) aging
(B) preemption
(C) a larger quantum
(D) switching to FCFS

**Q49.** Round Robin with a very **large** time quantum degenerates into
(A) SJF
(B) FCFS
(C) SRTF
(D) Priority scheduling

**Q50.** Round Robin with a very **small** time quantum
(A) improves throughput
(B) makes context-switch overhead dominate
(C) becomes SJF
(D) has no effect

**Q51.** SRTF is the preemptive version of
(A) FCFS
(B) SJF
(C) Round Robin
(D) Priority

**Q52.** In **HRRN**, the response ratio of a process equals
(A) BT / WT
(B) 1 + WT/BT
(C) WT − BT
(D) BT − WT

**Q53.** Which algorithm gives the best **response time** for interactive systems?
(A) FCFS
(B) SJF
(C) Round Robin
(D) HRRN

**Q54.** A **multilevel feedback queue** is characterised by
(A) fixed queues with no movement between them
(B) being adaptive, with promotion/demotion between queues — general purpose
(C) being identical to FCFS
(D) being strictly non-preemptive

**Q55.** Three processes P1, P2, P3 arrive at t = 0 (in that order) with bursts 24, 3, 3. Under **FCFS**, the average waiting time is
(A) 13 ms
(B) 17 ms
(C) 20 ms
(D) 27 ms

**Q56.** For the same three processes under FCFS, the average **turnaround** time is
(A) 17 ms
(B) 24 ms
(C) 27 ms
(D) 30 ms

**Q57.** The same three processes (24, 3, 3, all at t = 0) scheduled by **SJF** give an average waiting time of
(A) 3 ms
(B) 6 ms
(C) 9 ms
(D) 17 ms

**Q58.** The same three processes (24, 3, 3, all at t = 0) under **Round Robin, quantum = 4**, give an average waiting time of
(A) 4.33 ms
(B) 5.67 ms
(C) 6 ms
(D) 7 ms

**Q59.** For that Round Robin case (quantum 4), the average **turnaround** time is
(A) 13.5 ms
(B) 15.67 ms
(C) 16 ms
(D) 27 ms

**Q60.** Processes P1(AT 0, BT 8), P2(AT 1, BT 4), P3(AT 2, BT 9), P4(AT 3, BT 5) are scheduled by **SRTF**. The average waiting time is
(A) 5.5 ms
(B) 6.5 ms
(C) 9 ms
(D) 13 ms

**Q61.** For that same SRTF schedule, the average **turnaround** time is
(A) 11 ms
(B) 12 ms
(C) 13 ms
(D) 15 ms

**Q62.** Under **FCFS**, P1(AT 0, BT 4), P2(AT 1, BT 3), P3(AT 2, BT 1) give an average waiting time of
(A) 2.67 ms
(B) 3 ms
(C) 4 ms
(D) 5 ms

**Q63.** Under **non-preemptive SJF**, P1(AT 0, BT 7), P2(AT 2, BT 4), P3(AT 4, BT 1), P4(AT 5, BT 4) give an average waiting time of
(A) 3 ms
(B) 4 ms
(C) 5 ms
(D) 6 ms

**Q64.** Under **Round Robin, quantum = 2**, P1(BT 5), P2(BT 3), P3(BT 1), all arriving at t = 0 in that order, give an average waiting time of
(A) 4 ms
(B) 4.33 ms
(C) 5 ms
(D) 6 ms

**Q65.** Under **non-preemptive priority** (lower number = higher priority) P1(BT 4, pr 2), P2(BT 3, pr 1), P3(BT 2, pr 3), all at t = 0, the average waiting time is
(A) 3 ms
(B) 3.33 ms
(C) 4 ms
(D) 5 ms

**Q66.** The **convoy effect** refers to
(A) short processes waiting behind one long process in FCFS, inflating average waiting time
(B) starvation of long jobs in SJF
(C) circular waiting among processes
(D) excessive paging

---

## Part D — IPC, concurrency and synchronization

**Q67.** The **fastest** IPC mechanism (after setup) is
(A) message passing
(B) shared memory
(C) pipes
(D) sockets

**Q68.** Which IPC mechanism naturally **works across machines**?
(A) Shared memory
(B) Message passing
(C) Both equally
(D) Neither

**Q69.** The drawback of **shared memory** IPC is that
(A) it is the slowest mechanism
(B) the programmer must handle synchronization manually
(C) it only works across machines
(D) it needs the kernel on every access

**Q70.** A **pipe** is
(A) a bidirectional network channel
(B) a unidirectional byte stream between related processes
(C) a shared-memory region
(D) a kind of semaphore

**Q71.** A **race condition** is
(A) very fast execution
(B) a situation where the outcome depends on the timing of interleaved accesses to shared data
(C) a deadlock
(D) starvation

**Q72.** A **critical section** is
(A) the highest-priority code in a program
(B) a section of code that accesses shared data and must be executed by at most one process at a time
(C) code that runs only in the kernel
(D) an I/O routine

**Q73.** The three requirements a correct critical-section solution must satisfy are
(A) mutual exclusion, progress, bounded waiting
(B) atomicity, consistency, isolation
(C) mutual exclusion, preemption, fairness
(D) safety, liveness, throughput

**Q74.** "If no process is in the critical section, a waiting process must be able to enter (no unnecessary blocking)" describes which requirement?
(A) Mutual exclusion
(B) Progress
(C) Bounded waiting
(D) Atomicity

**Q75.** "There is a limit on how many other processes may enter before a waiting process gets its turn" describes which requirement?
(A) Mutual exclusion
(B) Progress
(C) Bounded waiting
(D) Fairness

**Q76.** **Peterson's solution**
(A) uses only a `turn` variable
(B) uses only a `flag[]` array
(C) uses both a `flag[]` array and a `turn` variable and satisfies all three requirements
(D) relies on a hardware test-and-set instruction

**Q77.** The strict-alternation solution (a single `turn` variable) fails which requirement?
(A) Mutual exclusion
(B) Progress
(C) Bounded waiting
(D) None — it is correct

**Q78.** A **binary** semaphore takes values
(A) 0 … n
(B) 0 or 1
(C) −1 to 1
(D) any integer

**Q79.** A **counting** semaphore initialised to **n** allows
(A) exactly 1 process into the critical section
(B) n processes into the critical section simultaneously
(C) unlimited processes
(D) 0 processes

**Q80.** The key difference between a semaphore and a mutex is that
(A) a semaphore has ownership
(B) a mutex has ownership — only the thread that locked it may unlock it
(C) both have ownership
(D) neither has ownership

**Q81.** The `wait(S)` / `P(S)` operation on a semaphore
(A) increments S
(B) blocks while S ≤ 0, then decrements S
(C) sets S to 0
(D) is the release operation

**Q82.** In the producer–consumer solution, the three semaphores are initialised to
(A) mutex = 0, empty = 0, full = n
(B) mutex = 1, empty = n, full = 0
(C) mutex = 1, empty = 0, full = n
(D) mutex = n, empty = 1, full = 1

**Q83.** If the producer executes `wait(mutex)` **before** `wait(empty)`, then when the buffer is full the result is
(A) it works fine
(B) deadlock
(C) starvation but no deadlock
(D) a harmless race

**Q84.** In producer–consumer, the safe rule is to acquire ___ before the mutex.
(A) the `full` semaphore always
(B) the counting semaphore (`empty`/`full`)
(C) nothing — order is irrelevant
(D) the signal

**Q85.** In the **readers-priority** variant of the readers–writers problem,
(A) readers can starve
(B) writers can starve
(C) it deadlocks
(D) there is no starvation problem

**Q86.** In the dining-philosophers problem, deadlock occurs when
(A) all five philosophers simultaneously pick up their left fork (circular wait)
(B) one philosopher eats forever
(C) the forks are shareable
(D) there are too few philosophers

**Q87.** A standard solution to dining-philosophers deadlock is
(A) let every philosopher pick up left then right
(B) make odd philosophers pick left-then-right and even ones right-then-left (asymmetric ordering)
(C) remove all the forks
(D) provide an unlimited number of forks

**Q88.** A **monitor** is
(A) a hardware register
(B) a high-level construct that guarantees only one process executes inside it at a time, using condition variables
(C) exactly the same as a semaphore
(D) a scheduling algorithm

**Q89.** A **spinlock**
(A) blocks and puts the thread to sleep
(B) busy-waits in a tight loop and is efficient only for very short critical sections
(C) is another name for a counting semaphore
(D) disables paging

---

## Part E — Deadlock and Banker's algorithm

**Q90.** Which of the following is **not** one of the four necessary conditions for deadlock?
(A) Mutual exclusion
(B) Hold and wait
(C) Preemption
(D) Circular wait

**Q91.** Regarding preemption, the actual deadlock condition is
(A) preemption
(B) no preemption
(C) full preemption
(D) partial preemption

**Q92.** Deadlock is defined as
(A) a process waiting for I/O to complete
(B) a set of processes each holding a resource and each waiting for a resource held by another, so none can proceed
(C) low CPU utilisation
(D) indefinite postponement of one process

**Q93.** In a **resource-allocation graph** with a **single instance** of each resource type, a cycle means
(A) no deadlock
(B) deadlock
(C) only the possibility of deadlock
(D) a safe state

**Q94.** In a RAG with **multiple instances** per resource type, a cycle is
(A) sufficient for deadlock
(B) necessary but not sufficient for deadlock
(C) impossible
(D) irrelevant to deadlock

**Q95.** The Banker's algorithm is a deadlock ___ technique.
(A) prevention
(B) avoidance
(C) detection
(D) recovery

**Q96.** In the Banker's algorithm, `Need[i][j]` equals
(A) Max − Available
(B) Max − Allocation
(C) Allocation − Max
(D) Available − Max

**Q97.** The difference between prevention and avoidance is that
(A) both make a condition impossible
(B) prevention makes one of the four conditions impossible by design, while avoidance allows all four but checks each request
(C) avoidance ignores the conditions entirely
(D) they are the same

**Q98.** The most **practical** deadlock-prevention technique is
(A) breaking mutual exclusion
(B) imposing a total ordering on resource types (breaking circular wait)
(C) requesting all resources at once
(D) preempting printers

**Q99.** A **safe** state implies
(A) deadlock is certain
(B) no deadlock
(C) deadlock is possible
(D) thrashing

**Q100.** An **unsafe** state implies
(A) deadlock is certain
(B) deadlock is possible but not certain
(C) no deadlock can occur
(D) the state is actually safe

**Q101.** The "ostrich algorithm" (ignoring deadlock) is used by
(A) hard real-time systems
(B) general-purpose OSs such as Linux and Windows
(C) the Banker's algorithm
(D) all microkernels

**Q102.** To break the **hold-and-wait** condition, a system can
(A) require each process to request all its resources at once, up front
(B) make resources shareable
(C) impose an ordering on resources
(D) preempt resources

**Q103.** Deadlock **recovery** may involve
(A) ignoring the deadlock
(B) terminating processes or preempting/rolling back resources
(C) requesting all resources up front
(D) aging

**Q104.** A system has 3 resource types A, B, C with **Available = (3, 3, 2)** and:

| P | Allocation | Max |
|---|---|---|
| P0 | 0 1 0 | 7 5 3 |
| P1 | 2 0 0 | 3 2 2 |
| P2 | 3 0 2 | 9 0 2 |
| P3 | 2 1 1 | 2 2 2 |
| P4 | 0 0 2 | 4 3 3 |

The state is
(A) unsafe
(B) safe, with safe sequence P1 → P3 → P4 → P0 → P2
(C) deadlocked
(D) safe, with P0 running first

**Q105.** In the system of Q104, the **Need** vector of P0 is
(A) (7, 5, 3)
(B) (7, 4, 3)
(C) (0, 1, 0)
(D) (7, 3, 3)

**Q106.** In the system of Q104, **P1 requests (1, 0, 2)**. After the safety check, the request is
(A) denied — it leads to an unsafe state
(B) granted — the resulting state is still safe
(C) invalid — it exceeds P1's declared need
(D) the cause of immediate deadlock

**Q107.** Starting the safety algorithm of Q104 with Work = (3, 3, 2), the **first** process that can be run is
(A) P0
(B) P1
(C) P2
(D) P4

---

## Part F — Memory management, paging and TLB

**Q108.** The **first-fit** placement strategy allocates
(A) the smallest hole big enough
(B) the first hole big enough
(C) the largest hole
(D) the last hole

**Q109.** The **best-fit** strategy allocates
(A) the first hole big enough
(B) the smallest hole big enough
(C) the largest hole
(D) a random hole

**Q110.** The **worst-fit** strategy allocates
(A) the largest hole
(B) the smallest hole big enough
(C) the first hole
(D) an exactly-sized hole

**Q111.** Free holes are 100, 500, 200, 300, 600 KB. A process needs 212 KB. **Best fit** allocates the ___ KB hole.
(A) 500
(B) 300
(C) 600
(D) 200

**Q112.** For the same holes and request, **first fit** allocates the ___ KB hole.
(A) 500
(B) 300
(C) 600
(D) 200

**Q113.** For the same holes and request, **worst fit** allocates the ___ KB hole.
(A) 500
(B) 300
(C) 600
(D) 200

**Q114.** **Internal fragmentation** is
(A) free memory split into small non-contiguous pieces
(B) space wasted inside an allocated block that is larger than requested
(C) always caused by segmentation
(D) the same as external fragmentation

**Q115.** **External fragmentation** is
(A) waste inside an allocated block
(B) enough total free memory that is split into non-contiguous pieces, none large enough
(C) caused by paging
(D) the same as internal fragmentation

**Q116.** **Paging** primarily causes ___ fragmentation.
(A) external
(B) internal
(C) both equally
(D) no

**Q117.** **Segmentation** primarily causes ___ fragmentation.
(A) internal
(B) external
(C) no
(D) both equally

**Q118.** **Compaction** cures
(A) internal fragmentation
(B) external fragmentation
(C) thrashing
(D) deadlock

**Q119.** In paging, the number of **offset bits** equals
(A) log₂(number of pages)
(B) log₂(page size)
(C) the page size in bytes
(D) log₂(number of frames)

**Q120.** With a 32-bit virtual address, 4 KB page size and 4-byte page-table entry, the size of a **single-level page table per process** is
(A) 1 MB
(B) 2 MB
(C) 4 MB
(D) 8 MB

**Q121.** For that same configuration, the number of pages (page-table entries) is
(A) 2¹⁰
(B) 2¹²
(C) 2²⁰
(D) 2²²

**Q122.** With a page size of 1 KB, the number of offset bits is
(A) 8
(B) 10
(C) 12
(D) 1024

**Q123.** The **TLB** is
(A) a region of secondary storage
(B) a small, fast associative cache of recently used page-table entries
(C) part of the file system
(D) a buffer for I/O devices

**Q124.** On a **TLB hit**, address translation
(A) requires two extra memory accesses
(B) requires no extra memory reference
(C) always triggers a page fault
(D) requires a disk access

**Q125.** With TLB access = 20 ns, memory access = 100 ns and hit ratio = 80% (TLB searched first; on a miss the page table is read, then the data), the **effective access time** is
(A) 120 ns
(B) 136 ns
(C) 140 ns
(D) 160 ns

**Q126.** **Multi-level page tables** exist mainly to
(A) speed up the TLB
(B) avoid the huge single-level table for sparse address spaces, allocating inner tables only for used ranges
(C) increase fragmentation
(D) replace the TLB

**Q127.** **Segmentation** divides the address space into
(A) fixed-size arbitrary slices
(B) logically meaningful, variable-size units (code, data, stack)
(C) equal-size frames
(D) fixed pages

**Q128.** The **valid/invalid bit** in a page-table entry indicates
(A) whether the page has been modified
(B) whether the page is currently in memory
(C) the protection level
(D) the reference count

**Q129.** The **dirty (modified) bit** is used to
(A) decide whether an evicted page must be written back to disk
(B) count how many times a page is referenced
(C) set the protection level
(D) perform address translation

---

## Part G — Virtual memory, page replacement and thrashing

**Q130.** **Virtual memory** allows
(A) a process's logical address space to exceed physical RAM, keeping active pages in RAM and the rest on disk
(B) the CPU to run faster
(C) more physical registers
(D) programs to run without any paging

**Q131.** **Demand paging** means
(A) loading all pages at program start
(B) loading a page only when it is actually referenced
(C) never paging
(D) loading pages only on exit

**Q132.** A **page fault** occurs when
(A) the valid bit of the referenced page is 1
(B) the valid bit of the referenced page is 0 (the page is not in memory)
(C) the dirty bit is set
(D) there is a TLB hit

**Q133.** After servicing a page fault, the OS
(A) terminates the process
(B) restarts the faulting instruction
(C) skips the faulting instruction
(D) ignores the reference

**Q134.** With memory access = 100 ns, page-fault service = 8 ms and a fault rate of 0.001, the **effective access time** is approximately
(A) 108 ns
(B) 800 ns
(C) 8099.9 ns
(D) 80 µs

**Q135.** **Belady's anomaly** can occur in which page-replacement algorithm?
(A) LRU
(B) OPT
(C) FIFO
(D) All of them

**Q136.** Belady's anomaly is the phenomenon that
(A) more frames give fewer page faults
(B) more frames give MORE page faults
(C) fewer frames give fewer faults
(D) frame count and faults are unrelated

**Q137.** The algorithms provably **immune** to Belady's anomaly (stack algorithms) are
(A) FIFO
(B) LRU and OPT
(C) clock only
(D) FIFO and LRU

**Q138.** **OPT** is unimplementable because it
(A) is too slow
(B) requires knowledge of future references
(C) needs too much memory
(D) causes thrashing

**Q139.** The best **practical** page-replacement algorithm, thanks to temporal locality, is
(A) FIFO
(B) OPT
(C) LRU
(D) MFU

**Q140.** The **clock (second-chance)** algorithm
(A) is exact LRU
(B) is FIFO plus a reference bit, cheaply approximating LRU
(C) is OPT
(D) evicts a random page

**Q141.** For the reference string 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5, **FIFO with 3 frames** produces
(A) 8 faults
(B) 9 faults
(C) 10 faults
(D) 12 faults

**Q142.** For the same reference string, **FIFO with 4 frames** produces
(A) 8 faults
(B) 9 faults
(C) 10 faults
(D) 12 faults

**Q143.** **Thrashing** is the condition where
(A) there are too many context switches
(B) the system spends more time paging than executing
(C) the disk is full
(D) processes deadlock

**Q144.** Thrashing is cured by
(A) admitting more processes
(B) the working-set model / reducing the degree of multiprogramming
(C) using smaller frames
(D) disabling the TLB

**Q145.** The **working set** of a process is
(A) all of the process's pages
(B) the set of pages it referenced in its last Δ references
(C) the set of free frames
(D) its page table

**Q146.** Under a **local** replacement policy,
(A) any frame in the system may be evicted
(B) a process may only evict its own frames
(C) no replacement ever occurs
(D) only global frames are used

---

## Part H — File systems, disk scheduling and RAID

**Q147.** A **hard link** is
(A) a file containing a path string
(B) another directory entry pointing to the same inode
(C) something that works across file systems
(D) a link that can dangle

**Q148.** A **soft (symbolic) link** is
(A) another entry pointing to the same inode
(B) a file containing a path string, which dangles if the original is deleted
(C) unable to cross file systems
(D) something that increases the inode's link count

**Q149.** If the original file is deleted, a **hard link** to it
(A) dangles
(B) still works — the data survives and the link count simply decreases
(C) is deleted as well
(D) becomes a soft link

**Q150.** Which file-allocation method supports efficient **direct access WITHOUT external fragmentation**?
(A) Contiguous
(B) Linked
(C) Indexed
(D) None

**Q151.** The main weakness of **linked** allocation is
(A) external fragmentation
(B) no direct/random access — you must follow the pointer chain
(C) inability to grow files
(D) wasting a whole index block

**Q152.** The main weakness of **contiguous** allocation is
(A) no direct access
(B) external fragmentation, and files cannot easily grow
(C) it needs an index block
(D) slow sequential reads

**Q153.** **Indexed** allocation
(A) gives O(1) direct access with no external fragmentation, at the cost of an index block
(B) supports only sequential access
(C) suffers external fragmentation
(D) cannot grow files

**Q154.** The UNIX **inode** uses
(A) only direct block pointers
(B) direct pointers plus single, double and triple indirect pointers
(C) a linked list of blocks
(D) contiguous allocation only

**Q155.** An inode has 10 direct pointers, 1 single-indirect and 1 double-indirect pointer. With a 4 KB block and 4-byte pointers, the maximum file size is approximately
(A) 4 MB
(B) 4 GB
(C) 40 KB
(D) 4 TB

**Q156.** With a 4 KB block and 4-byte pointers, the number of pointers held in one index block is
(A) 256
(B) 512
(C) 1024
(D) 4096

**Q157.** A common **free-space management** technique is
(A) the page table
(B) a bit vector / bitmap (one bit per block)
(C) the TLB
(D) the inode

**Q158.** Which disk-scheduling algorithm may **starve** requests far from the current head position?
(A) FCFS
(B) SSTF
(C) SCAN
(D) C-SCAN

**Q159.** The **SCAN** disk-scheduling algorithm is also known as the
(A) shortest-seek algorithm
(B) elevator algorithm
(C) circular algorithm
(D) priority algorithm

**Q160.** The advantage of **C-SCAN** over SCAN is
(A) it always moves the head less
(B) more uniform waiting times across cylinders
(C) it starves far requests
(D) it never reverses

**Q161.** **LOOK** differs from SCAN in that it
(A) travels to the physical end of the disk
(B) reverses at the last request rather than the disk end
(C) jumps back to cylinder 0
(D) serves requests randomly

**Q162.** Head at cylinder 53; request queue 98, 183, 37, 122, 14, 124, 65, 67 (disk 0–199). Under **FCFS**, the total head movement is
(A) 236 cylinders
(B) 640 cylinders
(C) 331 cylinders
(D) 382 cylinders

**Q163.** For the same queue, under **SSTF**, the total head movement is
(A) 236 cylinders
(B) 640 cylinders
(C) 331 cylinders
(D) 208 cylinders

**Q164.** For the same queue, under **SCAN moving downward first** (to 0, then reversing up), the total head movement is
(A) 236 cylinders
(B) 331 cylinders
(C) 382 cylinders
(D) 640 cylinders

**Q165.** For the same queue, under **C-SCAN** (upward to 199, jump to 0, continue upward), the total head movement is
(A) 236 cylinders
(B) 331 cylinders
(C) 382 cylinders
(D) 640 cylinders

**Q166.** **RAID 0** uses
(A) mirroring
(B) striping with no redundancy
(C) distributed parity
(D) double parity

**Q167.** **RAID 1** uses
(A) striping
(B) mirroring, surviving one disk failure
(C) parity
(D) no redundancy

**Q168.** **RAID 5** is characterised by
(A) needing ≥ 3 disks, striping with distributed parity, surviving one disk failure
(B) mirroring only
(C) no redundancy
(D) surviving two simultaneous failures

---

## Part I — Paper-I (English, Reasoning, GK)

**Q169.** Choose the word most nearly similar in meaning to **ALLEVIATE**.
(A) Aggravate
(B) Relieve
(C) Postpone
(D) Accuse

**Q170.** Fill in the blank: *"He insisted ___ paying the entire bill himself."*
(A) to
(B) for
(C) on
(D) at

**Q171.** Choose the word most nearly **opposite** in meaning to **PROLIFIC**.
(A) Fertile
(B) Unproductive
(C) Abundant
(D) Productive

**Q172.** Government by the wealthy is called
(A) plutocracy
(B) aristocracy
(C) autocracy
(D) theocracy

**Q173.** The idiom **"to bite the bullet"** means
(A) to eat very fast
(B) to face a difficult situation bravely
(C) to tell a lie
(D) to give up

**Q174.** Statements: *All engineers are graduates. Some graduates are teachers.* Which conclusion necessarily follows?
(A) All engineers are teachers
(B) Some engineers are teachers
(C) No engineer is a teacher
(D) None of the above necessarily follows

**Q175.** Find the next term: 2, 6, 12, 20, 30, ?
(A) 40
(B) 42
(C) 44
(D) 46

**Q176.** If the cost price of 15 articles equals the selling price of 12 articles, the profit percentage is
(A) 20%
(B) 25%
(C) 30%
(D) 33⅓%

**Q177.** A train 120 m long moving at 54 km/h crosses a pole in
(A) 6 s
(B) 8 s
(C) 10 s
(D) 12 s

**Q178.** Find the odd one out.
(A) 3
(B) 5
(C) 9
(D) 7

**Q179.** The average of the first ten natural numbers (1 to 10) is
(A) 5
(B) 5.5
(C) 6
(D) 55

**Q180.** The famous rock-cut sculptures and carvings of **Unakoti** are located in which state?
(A) Assam
(B) Meghalaya
(C) Tripura
(D) Mizoram

**Q181.** The capital of **Tripura** is
(A) Agartala
(B) Aizawl
(C) Imphal
(D) Shillong

**Q182.** Pointing to a photograph, a man says, *"She is the daughter of my grandfather's only son."* How is the woman related to the man?
(A) Sister
(B) Daughter
(C) Mother
(D) Cousin

**Q183.** Which of the following words is spelt **correctly**?
(A) Occassion
(B) Occasion
(C) Ocasion
(D) Occassion

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 32 | B | 63 | B | 94 | B | 125 | C | 156 | C |
| 2 | B | 33 | B | 64 | B | 95 | B | 126 | B | 157 | B |
| 3 | A | 34 | B | 65 | B | 96 | B | 127 | B | 158 | B |
| 4 | B | 35 | B | 66 | A | 97 | B | 128 | B | 159 | B |
| 5 | B | 36 | B | 67 | B | 98 | B | 129 | A | 160 | B |
| 6 | B | 37 | B | 68 | B | 99 | B | 130 | A | 161 | B |
| 7 | B | 38 | B | 69 | B | 100 | B | 131 | B | 162 | B |
| 8 | D | 39 | B | 70 | B | 101 | B | 132 | B | 163 | A |
| 9 | C | 40 | A | 71 | B | 102 | A | 133 | B | 164 | A |
| 10 | B | 41 | B | 72 | B | 103 | B | 134 | C | 165 | C |
| 11 | B | 42 | B | 73 | A | 104 | B | 135 | C | 166 | B |
| 12 | C | 43 | B | 74 | B | 105 | B | 136 | B | 167 | B |
| 13 | B | 44 | C | 75 | C | 106 | B | 137 | B | 168 | A |
| 14 | C | 45 | B | 76 | C | 107 | B | 138 | B | 169 | B |
| 15 | B | 46 | C | 77 | B | 108 | B | 139 | C | 170 | C |
| 16 | C | 47 | B | 78 | B | 109 | B | 140 | B | 171 | B |
| 17 | B | 48 | A | 79 | B | 110 | A | 141 | B | 172 | A |
| 18 | B | 49 | B | 80 | B | 111 | B | 142 | C | 173 | B |
| 19 | B | 50 | B | 81 | B | 112 | A | 143 | B | 174 | D |
| 20 | C | 51 | B | 82 | B | 113 | C | 144 | B | 175 | B |
| 21 | B | 52 | B | 83 | B | 114 | B | 145 | B | 176 | B |
| 22 | B | 53 | C | 84 | B | 115 | B | 146 | B | 177 | B |
| 23 | B | 54 | B | 85 | B | 116 | B | 147 | B | 178 | C |
| 24 | A | 55 | B | 86 | A | 117 | B | 148 | B | 179 | B |
| 25 | B | 56 | C | 87 | B | 118 | B | 149 | B | 180 | C |
| 26 | C | 57 | A | 88 | B | 119 | B | 150 | C | 181 | A |
| 27 | B | 58 | B | 89 | B | 120 | C | 151 | B | 182 | A |
| 28 | B | 59 | B | 90 | C | 121 | C | 152 | B | 183 | B |
| 29 | C | 60 | B | 91 | B | 122 | B | 153 | A | | |
| 30 | D | 61 | C | 92 | B | 123 | B | 154 | B | | |
| 31 | C | 62 | A | 93 | B | 124 | B | 155 | B | | |

---

# 📝 Detailed Solutions

**Q1. (B)** Multiprogramming keeps several programs in memory and switches to another when one blocks on I/O — its stated goal is to maximise CPU utilisation.

**Q2. (B)** Time-sharing switches rapidly (on a timer) so each user feels they have a dedicated machine; its goal is to minimise response time.

**Q3. (A)** Both keep several programs in memory, but multiprogramming switches only when a program blocks, whereas multitasking also switches on a timer — multitasking is multiprogramming plus preemption.

**Q4. (B)** In a hard RTOS a missed deadline is a system failure (pacemaker, airbag). Soft RTOS merely prefers deadlines.

**Q5. (B)** A dropped video frame is undesirable but not fatal — a classic soft real-time workload.

**Q6. (B)** Batch systems collect jobs and run them in groups with no user interaction.

**Q7. (B)** User mode cannot run privileged instructions such as halting the CPU, setting the page table, or direct I/O.

**Q8. (D)** Mode switches are caused by system calls, interrupts and traps/exceptions — not by ordinary arithmetic.

**Q9. (C)** A mode switch changes the privilege level of the same process; a context switch changes which process runs. A system call causes a mode switch but usually not a context switch.

**Q10. (B)** A microkernel keeps only the minimum (IPC, scheduling, basic memory) in the kernel; drivers and file systems run in user space — more reliable and modular, but slower due to message passing.

**Q11. (B)** A monolithic kernel puts all services inside the kernel: fast (no message passing) but a bug anywhere can crash everything.

**Q12. (C)** Windows NT and macOS are hybrid kernels.

**Q13. (B)** A system call is the only doorway from user mode into the kernel.

**Q14. (C)** `fork()` is a process-control call; `open()` is file management, `chmod()` is protection, `getpid()` is information.

**Q15. (B)** `fork()` returns 0 to the child, the child's PID to the parent, and −1 on failure.

**Q16. (C)** n consecutive forks yield 2ⁿ total processes (and 2ⁿ − 1 children).

**Q17. (B)** Three forks → 2³ = 8 processes, so 8 − 1 = 7 children.

**Q18. (B)** `exec()` replaces the current process image with a new program; it does not create a process and does not return on success.

**Q19. (B)** The shell forks to get a new process, then execs to make it run the desired program.

**Q20. (C)** Four forks → 2⁴ = 16 processes in existence.

**Q21. (B)** A program is a passive file; a process is a program in execution with a PC, registers, stack and heap.

**Q22. (B)** Running → ready is preemption (quantum expiry or a higher-priority arrival) — the process can still run, it just lost the CPU.

**Q23. (B)** Running → waiting is caused by an I/O request or waiting for an event — the process cannot run even if given the CPU.

**Q24. (A)** Waiting → ready happens when the awaited I/O completes.

**Q25. (B)** There is no waiting → running transition; a process finishing a wait must go through ready and be rescheduled.

**Q26. (C)** The PCB stores state, PC, registers, scheduling and memory info and the open-file table — not the program's source code.

**Q27. (B)** A zombie has terminated but the parent has not yet called `wait()`; its PCB slot lingers holding the exit status. Dead child, live parent.

**Q28. (B)** An orphan is still running but its parent died, so it is re-parented to `init`/`systemd`. Live child, dead parent.

**Q29. (C)** A zombie uses no memory or CPU — only a process-table slot.

**Q30. (D)** Threads share code, data, heap and open files; each has its own stack, registers and PC.

**Q31. (C)** The program counter is private per thread (as are the stack and registers).

**Q32. (B)** Each thread runs its own sequence of function calls and needs its own chain of activation records, so the stack must be private.

**Q33. (B)** A thread switch within a process is cheap because the address space (and page tables/TLB) is shared.

**Q34. (B)** Threads share the address space, so one thread's fatal fault can kill the whole process.

**Q35. (B)** With user-level threads, one blocking system call blocks all threads, and there is no true multi-core parallelism.

**Q36. (B)** Kernel-level threads give true parallelism, and one thread blocking does not block the others.

**Q37. (B)** A context switch is pure overhead: register save/restore, TLB flush and cache pollution.

**Q38. (B)** Threads of one process share memory and communicate directly via that shared memory.

**Q39. (B)** Separate processes have separate address spaces and must use kernel-mediated IPC.

**Q40. (A)** TAT = CT − AT (total time in the system).

**Q41. (B)** WT = TAT − BT (time in the system minus time actually served).

**Q42. (B)** Response time = first CPU allocation − AT.

**Q43. (B)** FCFS's weakness is the convoy effect: one long job at the front delays everyone.

**Q44. (C)** SJF is provably optimal for average waiting time.

**Q45. (B)** SJF needs future burst times, which the OS cannot know — it can only estimate them.

**Q46. (C)** SJF (like SRTF and priority) can starve long jobs; FCFS and RR do not starve.

**Q47. (B)** FCFS and Round Robin are starvation-free.

**Q48. (A)** Aging gradually raises a waiting process's priority so it eventually runs.

**Q49. (B)** With a quantum larger than every burst, no one is preempted, so RR becomes FCFS.

**Q50. (B)** A tiny quantum makes context-switch overhead dominate.

**Q51. (B)** SRTF (shortest remaining time first) is the preemptive form of SJF.

**Q52. (B)** HRRN picks the highest response ratio = 1 + WT/BT.

**Q53. (C)** Round Robin gives the best response time — no process waits more than one quantum-round for some CPU.

**Q54. (B)** MLFQ is adaptive, promoting/demoting processes between queues; it is the general-purpose scheduler.

**Q55. (B)** FCFS Gantt: P1 0–24, P2 24–27, P3 27–30. WT = 0, 24, 27 → average = 51/3 = **17 ms**.

**Q56. (C)** TAT = 24, 27, 30 → average = 81/3 = **27 ms**.

**Q57. (A)** SJF order P2, P3, P1: WT = 0, 3, 6 → average = 9/3 = **3 ms**.

**Q58. (B)** RR q = 4 Gantt: P1 0–4, P2 4–7, P3 7–10, P1 10–30. CT = 30, 7, 10; TAT = 30, 7, 10; WT = 6, 4, 7 → average = 17/3 ≈ **5.67 ms**.

**Q59. (B)** TAT = 30, 7, 10 → average = 47/3 ≈ **15.67 ms**.

**Q60. (B)** SRTF Gantt: P1 0–1, P2 1–5, P4 5–10, P1 10–17, P3 17–26. WT = 9, 0, 15, 2 → average = 26/4 = **6.5 ms**.

**Q61. (C)** TAT = 17, 4, 24, 7 → average = 52/4 = **13 ms**.

**Q62. (A)** FCFS Gantt: P1 0–4, P2 4–7, P3 7–8. TAT = 4, 6, 6; WT = 0, 3, 5 → average = 8/3 ≈ **2.67 ms**.

**Q63. (B)** SJF: P1 0–7; then among P2(4), P3(1), P4(4) pick P3 7–8, then P2 8–12, then P4 12–16. WT = 0, 6, 3, 7 → average = 16/4 = **4 ms**.

**Q64. (B)** RR q = 2: P1 0–2, P2 2–4, P3 4–5, P1 5–7, P2 7–8, P1 8–9. CT = 9, 8, 5; WT = 4, 5, 4 → average = 13/3 ≈ **4.33 ms**.

**Q65. (B)** Non-preemptive priority: P2(pr1) 0–3, P1(pr2) 3–7, P3(pr3) 7–9. WT = 0, 3, 7 → average = 10/3 ≈ **3.33 ms**.

**Q66. (A)** The convoy effect is short jobs queued behind one long job under FCFS, inflating the average waiting time.

**Q67. (B)** Shared memory is the fastest IPC — after setup there is no kernel involvement.

**Q68. (B)** Message passing works across machines (shared memory does not).

**Q69. (B)** Shared memory requires the programmer to handle synchronization manually.

**Q70. (B)** A pipe is a unidirectional byte stream between related processes.

**Q71. (B)** A race condition is when the outcome depends on the timing of interleaved accesses to shared data.

**Q72. (B)** A critical section is code touching shared data; only one process may execute it at a time.

**Q73. (A)** The three requirements are mutual exclusion, progress and bounded waiting. Option B lists ACID (DBMS).

**Q74. (B)** "No unnecessary blocking when the CS is free" is the **progress** requirement.

**Q75. (C)** A bound on how many others enter before a waiting process runs is **bounded waiting** (no starvation).

**Q76. (C)** Peterson's solution combines a `flag[]` array and a `turn` variable and satisfies all three requirements.

**Q77. (B)** Strict alternation fails progress: a process can only enter every second time and blocks if the other never wants in.

**Q78. (B)** A binary semaphore is 0 or 1.

**Q79. (B)** A counting semaphore initialised to n admits n processes concurrently.

**Q80. (B)** A mutex has ownership — only the locking thread may unlock it; a semaphore has no owner.

**Q81. (B)** `wait(S)`: block while S ≤ 0, then decrement S.

**Q82. (B)** Producer–consumer uses mutex = 1, empty = n, full = 0.

**Q83. (B)** Acquiring the mutex before `empty` means a full buffer leaves the producer holding the mutex forever — deadlock.

**Q84. (B)** Always acquire the counting semaphore (empty/full) before the mutex.

**Q85. (B)** In the readers-priority variant, a continuous stream of readers can starve writers.

**Q86. (A)** Deadlock arises when all five philosophers pick up their left fork at once — a circular wait.

**Q87. (B)** The asymmetric solution (odd: left-then-right, even: right-then-left) breaks the circular wait.

**Q88. (B)** A monitor is a high-level construct ensuring one process inside at a time, using condition variables.

**Q89. (B)** A spinlock busy-waits; it is efficient only for critical sections shorter than a context switch.

**Q90. (C)** The four conditions are mutual exclusion, hold-and-wait, **no preemption**, and circular wait. "Preemption" is the opposite of the real condition.

**Q91. (B)** The condition is **no preemption** — resources cannot be forcibly taken away.

**Q92. (B)** Deadlock: processes each holding a resource and each waiting for one held by another, so none proceed.

**Q93. (B)** With single instances, a cycle in the RAG is equivalent to deadlock.

**Q94. (B)** With multiple instances, a cycle is necessary but not sufficient — a spare instance held outside the cycle may resolve it.

**Q95. (B)** Banker's algorithm is deadlock avoidance — it grants a request only if the system stays in a safe state.

**Q96. (B)** Need = Max − Allocation.

**Q97. (B)** Prevention makes a condition impossible by design; avoidance allows all four but checks each request for safety.

**Q98. (B)** Imposing a total ordering on resource types (breaking circular wait) is the most practical prevention technique.

**Q99. (B)** A safe state guarantees no deadlock (a safe sequence exists).

**Q100. (B)** An unsafe state means deadlock is possible, not certain.

**Q101. (B)** General-purpose OSs (Linux, Windows) use the ostrich algorithm — ignore deadlock and reboot if needed.

**Q102. (A)** Breaking hold-and-wait means requesting all resources at once, up front.

**Q103. (B)** Recovery terminates processes or preempts/rolls back resources (needs checkpointing).

**Q104. (B)** Need vectors: P0(7,4,3), P1(1,2,2), P2(6,0,0), P3(0,1,1), P4(4,3,1). Work = (3,3,2): P1 runs → (5,3,2); P3 → (7,4,3); P4 → (7,4,5); P0 → (7,5,5); P2 → (10,5,7). Safe, sequence **P1 → P3 → P4 → P0 → P2**.

**Q105. (B)** Need(P0) = Max(7,5,3) − Alloc(0,1,0) = **(7,4,3)**.

**Q106. (B)** Request (1,0,2) ≤ Need(1,2,2) and ≤ Available(3,3,2). Pretend-grant: Available (2,3,0), P1 Alloc (3,0,2), Need (0,2,0). Safety: P1 (0,2,0) ≤ (2,3,0) → (5,3,2) → P3 → (7,4,3) → rest satisfiable. **Safe → grant.**

**Q107. (B)** From Work (3,3,2), P0's Need (7,4,3) exceeds it, but P1's Need (1,2,2) ≤ (3,3,2) — P1 runs first.

**Q108. (B)** First fit takes the first hole big enough (fastest search).

**Q109. (B)** Best fit takes the smallest hole big enough.

**Q110. (A)** Worst fit takes the largest hole.

**Q111. (B)** Best fit for 212 KB → smallest hole ≥ 212 = the **300** KB hole.

**Q112. (A)** First fit scans 100, 500, … → the first hole ≥ 212 is **500** KB.

**Q113. (C)** Worst fit → the largest hole = **600** KB.

**Q114. (B)** Internal fragmentation is space wasted inside an allocated block larger than requested.

**Q115. (B)** External fragmentation is enough total free memory split into non-contiguous pieces, none large enough.

**Q116. (B)** Paging uses fixed frames, so the last page is partly wasted → internal fragmentation.

**Q117. (B)** Segmentation uses variable-size segments, leaving awkward gaps → external fragmentation.

**Q118. (B)** Compaction slides processes together to merge holes, curing external fragmentation.

**Q119. (B)** Offset bits = log₂(page size).

**Q120. (C)** Pages = 2³²/2¹² = 2²⁰; table size = 2²⁰ × 4 bytes = 2²² = **4 MB** per process.

**Q121. (C)** Number of pages = 2³²/2¹² = **2²⁰**.

**Q122. (B)** log₂(1 KB) = log₂(1024) = **10** offset bits.

**Q123. (B)** The TLB is a small, fast associative cache of recently used page-table entries.

**Q124. (B)** On a TLB hit, translation needs no extra memory reference.

**Q125. (C)** EAT = 0.8 × (20 + 100) + 0.2 × (20 + 100 + 100) = 0.8 × 120 + 0.2 × 220 = 96 + 44 = **140 ns**.

**Q126. (B)** Multi-level tables avoid the huge single-level table, allocating inner tables only for used ranges.

**Q127. (B)** Segmentation divides the space into logically meaningful, variable-size units.

**Q128. (B)** The valid/invalid bit says whether the page is currently in memory.

**Q129. (A)** The dirty bit tells whether an evicted page must be written back to disk.

**Q130. (A)** Virtual memory lets the logical space exceed physical RAM, keeping active pages in RAM and the rest on disk.

**Q131. (B)** Demand paging loads a page only when it is referenced.

**Q132. (B)** A page fault occurs when the referenced page's valid bit is 0.

**Q133. (B)** After a fault the OS restarts the faulting instruction (it never completed).

**Q134. (C)** EAT = 0.999 × 100 + 0.001 × 8,000,000 = 99.9 + 8000 = **8099.9 ns** (≈ 8.1 µs).

**Q135. (C)** Belady's anomaly occurs in FIFO.

**Q136. (B)** Belady's anomaly: more frames give more page faults.

**Q137. (B)** LRU and OPT are stack algorithms and are immune to Belady's anomaly.

**Q138. (B)** OPT needs knowledge of future references, so it is only a benchmark.

**Q139. (C)** LRU is the best practical algorithm thanks to temporal locality (approximated by clock).

**Q140. (B)** Clock/second-chance is FIFO plus a reference bit, cheaply approximating LRU.

**Q141. (B)** FIFO, 3 frames: faults on 1,2,3,4,1,2,5,(hit 1),(hit 2),3,4,(hit 5) = **9 faults**.

**Q142. (C)** FIFO, 4 frames: 1,2,3,4,(hit 1),(hit 2),5,1,2,3,4,5 = **10 faults** — more frames, more faults (Belady).

**Q143. (B)** Thrashing is when the system spends more time paging than executing.

**Q144. (B)** The working-set model (and reducing multiprogramming) cures thrashing.

**Q145. (B)** The working set is the set of pages referenced in the last Δ references.

**Q146. (B)** Local replacement lets a process evict only its own frames.

**Q147. (B)** A hard link is another directory entry pointing to the same inode.

**Q148. (B)** A soft link is a file containing a path string; it dangles if the original is deleted.

**Q149. (B)** Deleting the original leaves a hard link working — the data survives and the link count decreases.

**Q150. (C)** Indexed allocation gives direct access with no external fragmentation.

**Q151. (B)** Linked allocation has no direct access — you must follow the pointer chain.

**Q152. (B)** Contiguous allocation suffers external fragmentation and files cannot easily grow.

**Q153. (A)** Indexed allocation gives O(1) direct access and no external fragmentation, at the cost of the index block.

**Q154. (B)** The inode uses direct pointers plus single, double and triple indirect pointers.

**Q155. (B)** Pointers/block = 1024. Direct = 10 × 4 KB = 40 KB; single = 1024 × 4 KB = 4 MB; double = 1024² × 4 KB = 4 GB → total ≈ **4 GB**.

**Q156. (C)** 4096 / 4 = **1024** pointers per block.

**Q157. (B)** A bit vector/bitmap (one bit per block) is a standard free-space technique.

**Q158. (B)** SSTF can starve far requests as nearer ones keep arriving.

**Q159. (B)** SCAN is the elevator algorithm.

**Q160. (B)** C-SCAN gives more uniform waiting times than SCAN.

**Q161. (B)** LOOK reverses at the last request rather than the disk end.

**Q162. (B)** FCFS: |53−98|+|98−183|+|183−37|+|37−122|+|122−14|+|14−124|+|124−65|+|65−67| = 45+85+146+85+108+110+59+2 = **640**.

**Q163. (A)** SSTF: 53→65→67→37→14→98→122→124→183 = 12+2+30+23+84+24+2+59 = **236**.

**Q164. (A)** SCAN downward first: 53→0 then up to 183 = (53−0) + (183−0) = 53 + 183 = **236**.

**Q165. (C)** C-SCAN upward: (199−53) + (199−0) + (37−0) = 146 + 199 + 37 = **382**.

**Q166. (B)** RAID 0 is striping with no redundancy.

**Q167. (B)** RAID 1 is mirroring, surviving one disk failure.

**Q168. (A)** RAID 5 needs ≥ 3 disks and uses striping with distributed parity, surviving one failure.

**Q169. (B)** *Alleviate* = to relieve; *aggravate* is the trap antonym.

**Q170. (C)** The fixed collocation is *insist on* (doing) something.

**Q171. (B)** *Prolific* means highly productive; its opposite is *unproductive/barren*.

**Q172. (A)** Government by the wealthy is a plutocracy.

**Q173. (B)** "Bite the bullet" means to face a difficult situation bravely.

**Q174. (D)** "Some graduates are teachers" does not guarantee any are engineers, so nothing necessarily follows.

**Q175. (B)** The pattern is n² + n: 2, 6, 12, 20, 30, **42** (= 6² + 6).

**Q176. (B)** CP of 15 = SP of 12 → SP of 1 = 15/12 = 1.25, profit 0.25 on CP 1 = **25%**.

**Q177. (B)** 54 km/h = 15 m/s; 120 m ÷ 15 m/s = **8 s**.

**Q178. (C)** 3, 5, 7 are prime; **9** is not — the odd one out.

**Q179. (B)** Sum 1..10 = 55; average = 55/10 = **5.5**.

**Q180. (C)** Unakoti's Shaiva rock-cut carvings are in **Tripura**.

**Q181. (A)** The capital of Tripura is **Agartala**.

**Q182. (A)** "My grandfather's only son" is the man's father; his daughter is the man's **sister**.

**Q183. (B)** The correct spelling is **Occasion**.

---

**Total: 183 questions** (168 Operating Systems + 15 Paper-I).
