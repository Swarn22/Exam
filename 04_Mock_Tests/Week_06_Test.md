# Week 6 Mock Test — Operating Systems

**Syllabus §8** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — Operating Systems (Q1–Q20)

**Q1.** Three processes P1, P2, P3 arrive at time 0 in that order with CPU bursts of 24, 3 and 3 ms. Under **FCFS** scheduling, the average waiting time is
(A) 13 ms  (B) 17 ms  (C) 20 ms  (D) 27 ms

**Q2.** Which scheduling algorithm gives the provably **minimum** average waiting time for a given set of processes available at the same time?
(A) FCFS  (B) Round Robin  (C) Shortest Job First  (D) Priority scheduling

**Q3.** In Round Robin scheduling, if the time quantum is made very large, the algorithm degenerates to
(A) SJF  (B) FCFS  (C) Priority scheduling  (D) SRTF

**Q4.** Which of the following is **not** one of the four necessary conditions for deadlock?
(A) Mutual exclusion  (B) Hold and wait  (C) Preemption  (D) Circular wait

**Q5.** The Banker's algorithm is used for deadlock
(A) prevention  (B) avoidance  (C) detection  (D) recovery

**Q6.** The three requirements a solution to the critical-section problem must satisfy are
(A) mutual exclusion, progress, bounded waiting
(B) mutual exclusion, preemption, fairness
(C) atomicity, consistency, isolation
(D) safety, liveness, throughput

**Q7.** A counting semaphore initialised to 3 permits how many processes to be in the critical section simultaneously?
(A) 1  (B) 2  (C) 3  (D) Unlimited

**Q8.** Belady's anomaly — where increasing the number of frames increases the number of page faults — can occur in
(A) LRU  (B) Optimal (OPT)  (C) FIFO  (D) All of the above

**Q9.** The Optimal page replacement algorithm cannot be implemented in practice because
(A) it is too slow
(B) it requires knowledge of future references
(C) it needs too much memory
(D) it causes thrashing

**Q10.** A system spends most of its time swapping pages in and out rather than executing instructions. This condition is called
(A) starvation  (B) deadlock  (C) thrashing  (D) fragmentation

**Q11.** Consider a system with a 32-bit virtual address, a page size of 4 KB and a page table entry of 4 bytes. The size of a single-level page table for one process is
(A) 1 MB  (B) 2 MB  (C) 4 MB  (D) 8 MB

**Q12.** The TLB (Translation Lookaside Buffer) is
(A) a cache for recently used page table entries
(B) a region of secondary storage
(C) part of the file system
(D) a buffer for I/O devices

**Q13.** Paging suffers primarily from ___ fragmentation, while segmentation suffers primarily from ___ fragmentation.
(A) external, internal  (B) internal, external  (C) internal, internal  (D) external, external

**Q14.** Which disk scheduling algorithm may cause **starvation** of requests far from the current head position?
(A) FCFS  (B) SSTF  (C) SCAN  (D) C-SCAN

**Q15.** The SCAN disk scheduling algorithm is also known as the
(A) shortest-seek algorithm  (B) elevator algorithm  (C) circular algorithm  (D) priority algorithm

**Q16.** Which file allocation method supports efficient direct (random) access **without** external fragmentation?
(A) Contiguous allocation  (B) Linked allocation  (C) Indexed allocation  (D) None

**Q17.** Which of the following is **not** shared between threads of the same process?
(A) Code section  (B) Data section  (C) Open files  (D) Stack and registers

**Q18.** In UNIX, a successful `fork()` system call returns
(A) 0 to both parent and child
(B) 0 to the child and the child's PID to the parent
(C) the child's PID to both
(D) −1 to the child

**Q19.** A process that has finished execution but whose entry still remains in the process table because the parent has not read its exit status is called a
(A) orphan process  (B) zombie process  (C) daemon process  (D) suspended process

**Q20.** The transition of a process from the **running** state to the **ready** state is caused by
(A) an I/O request
(B) preemption / expiry of the time quantum
(C) process termination
(D) completion of I/O

---

## Part B — Paper-I (Q21–Q25)

**Q21.** Choose the word most nearly similar in meaning to **ALLEVIATE**.
(A) Aggravate  (B) Relieve  (C) Postpone  (D) Accuse

**Q22.** Fill in the blank: *"He insisted ___ paying the entire bill himself."*
(A) to  (B) for  (C) on  (D) at

**Q23.** Statements: *All engineers are graduates. Some graduates are teachers.* Which conclusion necessarily follows?
(A) All engineers are teachers
(B) Some engineers are teachers
(C) No engineer is a teacher
(D) None of the above necessarily follows

**Q24.** If the cost price of 15 articles equals the selling price of 12 articles, the profit percentage is
(A) 20%  (B) 25%  (C) 30%  (D) 33⅓%

**Q25.** The famous rock-cut sculptures and carvings of Unakoti are located in which state?
(A) Assam  (B) Meghalaya  (C) Tripura  (D) Mizoram

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 6 | A | 11 | C | 16 | C | 21 | B |
| 2 | C | 7 | C | 12 | A | 17 | D | 22 | C |
| 3 | B | 8 | C | 13 | B | 18 | B | 23 | D |
| 4 | C | 9 | B | 14 | B | 19 | B | 24 | B |
| 5 | B | 10 | C | 15 | B | 20 | B | 25 | C |

---

**Q1 — (B).** Waiting times: P1 = 0, P2 = 24, P3 = 27. Average = (0 + 24 + 27)/3 = 51/3 = **17 ms**. This is the classic convoy-effect illustration — had the short jobs run first, the average would drop to 3 ms.

**Q2 — (C).** SJF is provably optimal for average waiting time. Its drawback is that burst lengths must be known (or predicted) in advance, and long jobs can starve.

**Q3 — (B).** With a quantum longer than every burst, no process is ever preempted, so RR behaves exactly like **FCFS**. A very small quantum, conversely, maximises context-switch overhead.

**Q4 — (C).** The four conditions are mutual exclusion, hold and wait, **no preemption**, and circular wait. Option C states the opposite of the actual condition.

**Q5 — (B).** Banker's algorithm checks whether granting a request leaves the system in a *safe state* — it **avoids** deadlock at run time, using advance knowledge of maximum needs.

**Q6 — (A).** Mutual exclusion (one at a time), progress (no unnecessary blocking), bounded waiting (no starvation). Option C lists ACID properties from DBMS.

**Q7 — (C).** A counting semaphore initialised to n admits **n** concurrent processes. Initialised to 1, it is a binary semaphore / mutex.

**Q8 — (C).** **FIFO** exhibits Belady's anomaly. LRU and OPT are *stack algorithms*, which are provably immune to it.

**Q9 — (B).** OPT evicts the page that will be referenced furthest in the future — unknowable at run time. It is used only as a benchmark for other algorithms.

**Q10 — (C).** Thrashing: the degree of multiprogramming exceeds available frames, so the page-fault rate explodes and CPU utilisation collapses. Fixed by working-set or page-fault-frequency control.

**Q11 — (C).** Pages = 2³²/2¹² = 2²⁰ entries. Size = 2²⁰ × 4 bytes = 2²² = **4 MB**. This impracticality is exactly why multi-level and inverted page tables exist.

**Q12 — (A).** The TLB is a small, fast associative cache of page-table entries. On a TLB hit, address translation costs no extra memory reference.

**Q13 — (B).** Paging uses fixed-size frames, so the last page of a process is partly wasted → **internal** fragmentation. Segmentation uses variable-size segments, leaving unusable gaps → **external** fragmentation.

**Q14 — (B).** SSTF always picks the nearest request, so a request at the far end of the disk can be postponed indefinitely. SCAN/C-SCAN bound the wait by sweeping the full range.

**Q15 — (B).** SCAN moves the head in one direction servicing requests, then reverses — like a lift. C-SCAN returns to the start without servicing, giving more uniform wait times.

**Q16 — (C).** Indexed allocation keeps all block pointers in an index block: direct access is O(1) and blocks need not be contiguous. Contiguous allocation gives direct access but suffers external fragmentation; linked allocation avoids fragmentation but only supports sequential access.

**Q17 — (D).** Threads share code, data, heap and open files, but each has its **own stack, registers and program counter**. That is precisely what makes a thread a separate flow of control.

**Q18 — (B).** `fork()` returns **0 in the child** and the **child's PID in the parent** (−1 on failure). This asymmetry is how the two branches distinguish themselves.

**Q19 — (B).** A **zombie** has terminated but not been reaped by `wait()`. An *orphan* is the opposite — a live child whose parent died, which then gets adopted by `init`.

**Q20 — (B).** Running → ready happens on preemption (quantum expiry or a higher-priority arrival). Running → **waiting/blocked** is what an I/O request causes — the most common wrong answer here.

**Q21 — (B).** *Alleviate* = to make less severe, to **relieve**. *Aggravate* is its antonym — the deliberate trap.

**Q22 — (C).** The fixed collocation is *insist **on** (doing) something*.

**Q23 — (D).** "Some graduates are teachers" does not guarantee those teachers are among the engineers. No conclusion **necessarily** follows. Only possibilities, not certainties, can be drawn here.

**Q24 — (B).** Let CP of 1 article = 1, so CP of 15 = 15 = SP of 12 → SP of 1 = 15/12 = 1.25. Profit = 0.25 on CP 1 = **25%**.

**Q25 — (C).** **Unakoti**, in Unakoti district of **Tripura**, holds a large group of Shaiva rock-cut carvings and stone images, dated to around the 7th–9th centuries. It is on India's UNESCO tentative list and is one of the state's most-asked GK items.

---

## Score

| | |
|---|---|
| Part A (Operating Systems) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** missed Q1–Q3 → practise Gantt charts until average waiting/turnaround time is mechanical; missed Q4–Q7 → redo deadlock and synchronisation (work Banker's algorithm numerically); missed Q8–Q13 → redo virtual memory and paging; missed Q14–Q16 → redo disk scheduling and file systems. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S08_Operating_System/` (343 questions).
