# Week 2 Mock Test — Computer Organization & Architecture

**Syllabus §3** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — COA (Q1–Q20)

**Q1.** In which addressing mode is the effective address obtained by adding a constant displacement to the contents of a register?
(A) Immediate  (B) Direct  (C) Indexed / base-with-displacement  (D) Register direct

**Q2.** Which addressing mode is most suitable for implementing pointers and dynamically allocated data?
(A) Immediate  (B) Indirect  (C) Implied  (D) Register direct

**Q3.** A direct-mapped cache of size 8 KB uses a block size of 32 bytes. If the physical address is 32 bits wide, the numbers of bits in the tag, index and block-offset fields are respectively
(A) 19, 8, 5  (B) 18, 9, 5  (C) 19, 5, 8  (D) 20, 7, 5

**Q4.** A memory system has a cache access time of 10 ns and a main-memory access time of 100 ns. On a miss, the word is fetched from main memory *after* the cache lookup fails. If the hit ratio is 0.9, the average memory access time is
(A) 19 ns  (B) 20 ns  (C) 55 ns  (D) 100 ns

**Q5.** The maximum theoretical speedup achievable by a k-stage instruction pipeline over a non-pipelined processor is
(A) k  (B) k − 1  (C) 2k  (D) log₂ k

**Q6.** A 5-stage pipeline executes 1000 instructions with no stalls, one cycle per stage. The number of clock cycles required is
(A) 1000  (B) 1004  (C) 5000  (D) 1005

**Q7.** A "read after write" (RAW) hazard in a pipeline is also known as a
(A) true data dependency  (B) anti-dependency  (C) output dependency  (D) structural hazard

**Q8.** Operand forwarding (bypassing) in a pipelined datapath is used primarily to
(A) eliminate structural hazards
(B) reduce stalls caused by data hazards
(C) predict branch outcomes
(D) increase the clock frequency

**Q9.** Compared with hardwired control, a microprogrammed control unit is
(A) faster but less flexible
(B) slower but more flexible and easier to modify
(C) both faster and more flexible
(D) identical in speed and flexibility

**Q10.** In a stack-organised computer, arithmetic instructions such as ADD are typically
(A) three-address  (B) two-address  (C) one-address  (D) zero-address

**Q11.** A disk rotates at 6000 RPM. The average rotational latency is
(A) 2.5 ms  (B) 5 ms  (C) 10 ms  (D) 16.6 ms

**Q12.** Total disk access time is the sum of
(A) seek time + rotational latency + transfer time
(B) seek time + transfer time only
(C) rotational latency + transfer time only
(D) seek time + rotational latency only

**Q13.** In DMA, the technique in which the DMA controller takes control of the bus for one bus cycle at a time, letting the CPU continue in between, is called
(A) burst mode  (B) cycle stealing  (C) transparent mode  (D) interrupt mode

**Q14.** The principal advantage of DMA over interrupt-driven I/O is that
(A) it needs no controller hardware
(B) data transfer bypasses the CPU, reducing CPU involvement per word
(C) it is always slower but simpler
(D) it eliminates the need for main memory

**Q15.** In the write-back (copy-back) cache policy, main memory is updated
(A) on every write to the cache
(B) only when the modified block is evicted from the cache
(C) at every clock cycle
(D) never

**Q16.** Which of the following is **not** typically a characteristic of a RISC architecture?
(A) Fixed-length instructions
(B) Load/store architecture
(C) A large number of general-purpose registers
(D) A large number of complex, variable-length instructions

**Q17.** Cache memory works effectively because programs exhibit
(A) locality of reference  (B) recursion  (C) virtualisation  (D) pipelining

**Q18.** Memory interleaving is used mainly to
(A) increase memory capacity
(B) allow simultaneous/overlapped access to several memory modules, improving bandwidth
(C) reduce the number of address lines
(D) implement virtual memory

**Q19.** In a fully associative cache, a block from main memory
(A) can be placed in exactly one cache line
(B) can be placed in any cache line
(C) can be placed in one of k lines of a set
(D) cannot be replaced

**Q20.** The register that holds the address of the next instruction to be fetched is the
(A) MAR  (B) MDR  (C) Program Counter  (D) Instruction Register

---

## Part B — Paper-I (Q21–Q25)

**Q21.** Choose the correctly spelt word.
(A) Occurence  (B) Occurrence  (C) Ocurrence  (D) Occurrance

**Q22.** Identify the part containing the error: *"Neither of the two candidates (A)/ have submitted (B)/ their documents (C)/ before the deadline. (D)"*
(A) A  (B) B  (C) C  (D) D

**Q23.** Pointing to a photograph, a man said, *"She is the daughter of my grandfather's only son."* How is the woman related to the man?
(A) Sister  (B) Daughter  (C) Niece  (D) Cousin

**Q24.** A shopkeeper marks an article 40% above cost price and then allows a discount of 25%. His profit percentage is
(A) 5%  (B) 10%  (C) 15%  (D) 20%

**Q25.** The highest peak of Tripura, Betlingchhip, is located in which hill range?
(A) Jampui Hills  (B) Atharamura Hills  (C) Baramura Hills  (D) Longtharai Hills

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | C | 6 | B | 11 | B | 16 | D | 21 | B |
| 2 | B | 7 | A | 12 | A | 17 | A | 22 | B |
| 3 | A | 8 | B | 13 | B | 18 | B | 23 | A |
| 4 | B | 9 | B | 14 | B | 19 | B | 24 | A |
| 5 | A | 10 | D | 15 | B | 20 | C | 25 | A |

---

**Q1 — (C).** EA = contents of a register + displacement. This is the workhorse mode for array element access and stack-frame variables.

**Q2 — (B).** In indirect addressing the instruction gives the address *of the address*, which is exactly what a pointer dereference does.

**Q3 — (A).** Block size 32 B → offset = log₂32 = **5** bits. Lines = 8 KB / 32 B = 256 → index = log₂256 = **8** bits. Tag = 32 − 8 − 5 = **19** bits.

**Q4 — (B).** Sequential (hierarchical) lookup: AMAT = Tc + (1 − h)·Tm = 10 + 0.1 × 100 = **20 ns**. *Note:* if the question had said the two are searched simultaneously, it would be h·Tc + (1−h)·Tm = 19 ns — option A. **Always read which access model is stated.**

**Q5 — (A).** Ideal speedup of a k-stage pipeline tends to **k** as the instruction count grows large.

**Q6 — (B).** Cycles = k + (n − 1) = 5 + 999 = **1004**. The first instruction takes k cycles to fill the pipeline; each subsequent one completes in 1.

**Q7 — (A).** RAW is a genuine producer–consumer dependency and cannot be removed by renaming. WAR (anti-) and WAW (output) dependencies are name dependencies and *can* be removed by register renaming.

**Q8 — (B).** Forwarding routes an ALU result straight to a later instruction's input rather than waiting for write-back, removing most RAW stalls. It cannot remove the load-use stall entirely.

**Q9 — (B).** Microprogrammed control stores control signals as microinstructions in control memory — slower (an extra memory lookup) but easy to modify, which is why CISC designs favour it.

**Q10 — (D).** A stack machine's ADD implicitly pops its two operands and pushes the result, so no addresses appear in the instruction — **zero-address**.

**Q11 — (B).** 6000 RPM = 100 rotations/second → one rotation = 10 ms. Average rotational latency is **half** a rotation = **5 ms**.

**Q12 — (A).** Seek (move the head to the track) + rotational latency (wait for the sector) + transfer (read the data). Controller overhead is sometimes added as a fourth term.

**Q13 — (B).** Cycle stealing takes one bus cycle at a time, interleaving with CPU activity. Burst mode holds the bus until the whole block has moved — faster transfer, but the CPU stalls.

**Q14 — (B).** With interrupt-driven I/O the CPU handles every word; DMA moves the whole block and interrupts the CPU only once, at completion.

**Q15 — (B).** Write-back defers the memory update until eviction, using a dirty bit — fewer memory writes, but memory is temporarily stale. Option A describes write-through.

**Q16 — (D).** Complex, variable-length instructions are the defining feature of **CISC**. A, B and C are all RISC hallmarks.

**Q17 — (A).** Temporal locality (recently used data is reused) and spatial locality (nearby addresses are used soon) are what make caching work at all.

**Q18 — (B).** Interleaving spreads consecutive addresses across separate modules so their access times overlap, raising effective bandwidth.

**Q19 — (B).** Fully associative = any block anywhere, which minimises conflict misses but requires comparing the tag against every line. Direct-mapped is (A); k-way set associative is (C).

**Q20 — (C).** The Program Counter (a.k.a. Instruction Pointer). MAR holds the address being accessed, MDR the data, and IR the instruction currently being decoded.

**Q21 — (B).** **Occurrence** — double *c*, double *r*, ending *-ence*.

**Q22 — (B).** *Neither of* takes a **singular** verb: "Neither of the two candidates **has** submitted…". A classic subject–verb agreement trap.

**Q23 — (A).** "My grandfather's only son" is the man's own father. So the woman is his father's daughter — his **sister**.

**Q24 — (A).** Take CP = 100. Marked price = 140. After 25% discount, SP = 140 × 0.75 = 105. Profit = 5 on 100 = **5%**.

**Q25 — (A).** **Betlingchhip** (about 939 m), Tripura's highest point, lies in the **Jampui Hills** in North Tripura along the Mizoram border. Atharamura, Baramura and Longtharai are the state's other main ranges.

---

## Score

| | |
|---|---|
| Part A (COA) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** missed Q3/Q4/Q15/Q19 → redo cache organisation (the highest-yield COA sub-topic); missed Q5–Q8 → redo pipelining and hazards; missed Q11–Q14 → redo I/O and secondary storage. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S03_Computer_Organization_and_Architecture/` (251 questions).
