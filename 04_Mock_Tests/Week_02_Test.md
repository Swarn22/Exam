# Week 2 Question Bank — Computer Organization & Architecture

**Syllabus §3** · 180 questions · Practice set · +1 / −0.33 marking

> Attempt in timed batches (e.g. 30 questions in 25 minutes) to simulate exam pressure; check the key only after each batch.

---

## Part A — Basic structure, registers & the instruction cycle

**Q1.** The von Neumann bottleneck arises primarily because
(A) the CPU has too few registers
(B) instructions and data share a single memory and bus, so they cannot be fetched simultaneously
(C) the ALU is slower than main memory
(D) there is no cache between CPU and memory

**Q2.** The defining feature of the Harvard architecture is
(A) a single shared memory for instructions and data
(B) separate memories and buses for instructions and data
(C) the absence of a control unit
(D) the absence of general-purpose registers

**Q3.** A modern CPU that uses one main memory but has separate L1 instruction and L1 data caches is best described as
(A) pure von Neumann  (B) pure Harvard  (C) modified Harvard  (D) a stack architecture

**Q4.** Which pairing is correct?
(A) Architecture = pipeline/cache design; Organization = instruction set
(B) Architecture = instruction set, registers, addressing modes; Organization = pipelines, caches, buses
(C) Architecture and Organization mean the same thing
(D) Architecture = transistor layout; Organization = programming language

**Q5.** The Program Counter (PC) holds
(A) the instruction currently being executed
(B) the address of the next instruction to be fetched
(C) the data most recently read from memory
(D) the address of the top of the stack

**Q6.** The Instruction Register (IR) holds
(A) the address of the next instruction
(B) the instruction currently being executed
(C) the data being written to memory
(D) the stack pointer value

**Q7.** The Memory Address Register (MAR) holds
(A) the data being transferred  (B) the address currently being accessed  (C) the current instruction  (D) the status flags

**Q8.** The MDR (Memory Data/Buffer Register) holds
(A) the address being accessed
(B) the data being read from or written to memory
(C) the next instruction address
(D) the interrupt vector

**Q9.** Which statement is correct?
(A) PC holds the instruction; IR holds an address
(B) PC holds the address of the next instruction; IR holds the current instruction
(C) Both PC and IR hold data operands
(D) MAR holds the data being transferred

**Q10.** The basic instruction cycle repeats the sequence
(A) Decode → Fetch → Execute
(B) Fetch → Decode → Execute
(C) Execute → Fetch → Decode
(D) Fetch → Execute → Decode

**Q11.** During the fetch phase, the micro-operation `PC ← PC + 1` is performed
(A) after the instruction has executed
(B) during the fetch, before the instruction executes
(C) only when a jump occurs
(D) never; the PC is incremented by the ALU only

**Q12.** Registers can be accessed far faster than main memory chiefly because they are
(A) built from DRAM
(B) on-chip, few in number and located right next to the ALU
(C) refreshed continuously
(D) much larger than memory

---

## Part B — Instruction formats & stack machines

**Q13.** Zero-address instructions are characteristic of a
(A) three-address machine  (B) two-address machine  (C) one-address machine  (D) stack machine

**Q14.** One-address instructions are characteristic of a(n)
(A) stack machine  (B) accumulator machine  (C) general-register machine  (D) Harvard machine

**Q15.** The order in which operands and operators appear in a stack machine's program corresponds to
(A) infix notation  (B) prefix notation  (C) postfix (reverse Polish) notation  (D) random order

**Q16.** The postfix (RPN) form of `(A + B) × (C + D)` is
(A) `AB+CD+*`  (B) `ABCD+*+`  (C) `+AB*+CD`  (D) `AB*CD+`

**Q17.** On a three-address machine, the minimum number of instructions needed to compute `X = (A + B) × (C + D)` is
(A) 3  (B) 5  (C) 6  (D) 7

**Q18.** In a stack-organised computer, the `ADD` instruction
(A) adds the contents of two named registers
(B) pops the top two stack elements and pushes their sum
(C) adds an immediate value to the accumulator
(D) requires three explicit addresses

**Q19.** The purpose of an expanding (variable-length) opcode is to
(A) increase the clock frequency
(B) let instructions with fewer operands use the freed operand bits to extend the opcode
(C) reduce the number of registers
(D) add a cache to the CPU

**Q20.** With an n-bit opcode field, the number of distinct instructions that can be encoded is
(A) n  (B) 2n  (C) 2ⁿ  (D) n²

**Q21.** On a two-address machine, `ADD A, B` typically means
(A) A ← B  (B) A ← A + B  (C) B ← A + B  (D) C ← A + B

---

## Part C — Addressing modes & memory-access counts

**Q22.** In which addressing mode is the effective address obtained by adding a constant displacement to the contents of a register?
(A) Immediate  (B) Direct  (C) Indexed / base-with-displacement  (D) Register direct

**Q23.** Which addressing mode is most suitable for implementing pointers and dynamically allocated data?
(A) Immediate  (B) Indirect  (C) Implied  (D) Register direct

**Q24.** The addressing mode designed specifically for accessing array elements is
(A) Immediate  (B) Indexed  (C) Direct  (D) Implied

**Q25.** To load a constant known at assembly time, the natural mode is
(A) Immediate  (B) Direct  (C) Indirect  (D) Indexed

**Q26.** Branches and position-independent code typically use
(A) PC-relative  (B) Indirect  (C) Register direct  (D) Immediate

**Q27.** The number of memory accesses needed just to fetch the operand in (memory) indirect addressing is
(A) 0  (B) 1  (C) 2  (D) 3

**Q28.** The number of memory accesses needed to fetch the operand in register-direct addressing is
(A) 0  (B) 1  (C) 2  (D) 3

**Q29.** The number of memory accesses needed to fetch the operand in direct (absolute) addressing is
(A) 0  (B) 1  (C) 2  (D) 3

**Q30.** The fastest addressing mode (touching no memory for the operand) is
(A) Indirect  (B) Direct  (C) Register direct  (D) Indexed

**Q31.** The slowest addressing mode (most memory accesses for the operand) is
(A) Immediate  (B) Register direct  (C) Indirect  (D) Direct

**Q32.** With R1 = 1000, the instruction `LOAD R2, 20(R1)` (base + displacement) computes an effective address of
(A) 20  (B) 1000  (C) 1020  (D) 980

**Q33.** R1 = 1000, M[1000] = 2000, M[2000] = 55. The instruction `LOAD (1000)` using memory-indirect addressing loads the value
(A) 1000  (B) 2000  (C) 55  (D) undefined

**Q34.** R1 = 1000, M[1000] = 2000. The instruction `LOAD (R1)` using register-indirect addressing loads the value
(A) 1000  (B) 2000  (C) 55  (D) 20

**Q35.** Auto-increment addressing is most useful for
(A) loading constants  (B) traversing arrays / stack push-pop  (C) branches  (D) subroutine linkage

**Q36.** In immediate addressing the operand is located
(A) in a memory location  (B) in a register  (C) within the instruction itself  (D) on the stack

**Q37.** Array `int A[100]` has base address 5000 with 4 bytes per element. Using indexed addressing, the effective address of `A[10]` is
(A) 5010  (B) 5040  (C) 5400  (D) 9000

---

## Part D — RISC vs CISC

**Q38.** Which of the following is **not** typically a characteristic of a RISC architecture?
(A) Fixed-length instructions
(B) Load/store architecture
(C) A large number of general-purpose registers
(D) A large number of complex, variable-length instructions

**Q39.** In a RISC processor the instruction length is
(A) variable  (B) fixed  (C) always zero  (D) unlimited

**Q40.** In a RISC (load/store) architecture, memory is accessed by
(A) any instruction  (B) only the LOAD and STORE instructions  (C) no instruction  (D) only ALU instructions

**Q41.** The control unit typically used in a RISC processor is
(A) hardwired  (B) microprogrammed  (C) stack-based  (D) none

**Q42.** The control unit typically used in a CISC processor is
(A) hardwired  (B) microprogrammed  (C) associative  (D) none

**Q43.** In the RISC philosophy, the burden of assembling complex operations from simple instructions is placed on
(A) the hardware  (B) the compiler  (C) the memory  (D) the cache

**Q44.** Which of the following is a CISC architecture?
(A) ARM  (B) MIPS  (C) x86  (D) RISC-V

**Q45.** Internally, modern x86 processors
(A) execute CISC instructions directly with no translation
(B) translate instructions into RISC-like micro-operations
(C) contain no pipeline
(D) have no registers

---

## Part E — ALU, datapath & control unit

**Q46.** As a side effect of its operations, the ALU sets the
(A) program counter  (B) condition flags (Zero, Carry, Sign, Overflow)  (C) cache tags  (D) instruction register

**Q47.** The datapath of a processor consists of
(A) only the control signals
(B) registers, buses, multiplexers and the ALU
(C) only main memory
(D) only the opcode field

**Q48.** The function of the control unit is to
(A) perform arithmetic and logic
(B) generate the control signals that steer the datapath each cycle
(C) store program data
(D) fetch blocks from disk

**Q49.** Compared with hardwired control, a microprogrammed control unit is
(A) faster but less flexible
(B) slower but more flexible and easier to modify
(C) both faster and more flexible
(D) identical in speed and flexibility

**Q50.** Compared with microprogrammed control, hardwired control is
(A) slower  (B) faster  (C) identical in speed  (D) dependent on control memory

**Q51.** In a microprogrammed control unit, the microinstructions are stored in
(A) main memory  (B) the data cache  (C) control memory  (D) general-purpose registers

**Q52.** The Control Address Register (CAR) points to the
(A) next machine instruction in main memory
(B) current microinstruction in control memory
(C) top of the data stack
(D) next data operand

**Q53.** A horizontal microinstruction is characterised by being
(A) narrow with encoded fields
(B) wide and unencoded (one bit per control signal), giving high parallelism and needing no decoder
(C) narrow and always requiring a decoder
(D) low in parallelism

**Q54.** A vertical microinstruction is characterised by being
(A) wide and unencoded
(B) narrow with encoded fields, requiring a decoder and offering low parallelism
(C) needing no decoder
(D) offering high parallelism

**Q55.** Microprogrammed control is inherently slower than hardwired control because
(A) it uses fewer registers
(B) every control step requires an extra control-memory read
(C) it is built from DRAM
(D) it has no clock

---

## Part F — Pipelining: formulas & numericals

**Q56.** The maximum theoretical speedup of a k-stage instruction pipeline over a non-pipelined processor is
(A) k  (B) k − 1  (C) 2k  (D) log₂ k

**Q57.** A 5-stage pipeline executes 1000 instructions with no stalls, one cycle per stage. The number of clock cycles required is
(A) 1000  (B) 1004  (C) 5000  (D) 1005

**Q58.** For a k-stage pipeline running n instructions with no stalls, the number of clock cycles is
(A) k + n  (B) k + n − 1  (C) n × k  (D) n − k

**Q59.** For the same k-stage pipeline, the equivalent non-pipelined execution takes
(A) n + k cycles  (B) n × k cycles  (C) k + n − 1 cycles  (D) n cycles

**Q60.** The pipeline speedup is given by
(A) nk / (k + n − 1)  (B) k / n  (C) n / k  (D) (k + n − 1) / nk

**Q61.** Pipelining primarily improves
(A) the latency of a single instruction
(B) the throughput (instructions completed per unit time)
(C) clock skew
(D) the cache hit ratio

**Q62.** The clock period of a pipeline is determined by
(A) the sum of all stage delays
(B) the delay of the slowest stage plus latch/register overhead
(C) the delay of the fastest stage
(D) the average of the stage delays

**Q63.** A 4-stage pipeline executes 100 instructions with no stalls. The number of clock cycles is
(A) 100  (B) 103  (C) 400  (D) 104

**Q64.** A 6-stage pipeline executes 200 instructions with no stalls. The number of clock cycles is
(A) 200  (B) 205  (C) 206  (D) 1200

**Q65.** For a 5-stage pipeline running 1000 instructions, the speedup over the non-pipelined machine is approximately
(A) 5.00  (B) 4.98  (C) 2.78  (D) 10.0

**Q66.** A 5-stage pipeline runs only 5 instructions. The speedup over the non-pipelined machine is approximately
(A) 5.00  (B) 4.98  (C) 2.78  (D) 1.80

**Q67.** The four stages of a pipeline take 10, 8, 12 and 9 ns, with 1 ns latch overhead. The clock period is
(A) 12 ns  (B) 13 ns  (C) 39 ns  (D) 10 ns

**Q68.** For the pipeline of Q67, the non-pipelined execution of one instruction takes 39 ns. The maximum speedup (large n) is about
(A) 4  (B) 3  (C) 3.9  (D) 5

**Q69.** In a pipeline the clock rate for every stage is limited by
(A) the fastest stage  (B) the slowest stage  (C) the number of instructions  (D) the latch overhead alone

**Q70.** A pipeline has stage delays 60, 50, 90 and 80 ns with a 5 ns latch overhead. The clock period is
(A) 90 ns  (B) 95 ns  (C) 280 ns  (D) 285 ns

---

## Part G — Pipeline hazards

**Q71.** A "read after write" (RAW) hazard in a pipeline is also known as a
(A) true data dependency  (B) anti-dependency  (C) output dependency  (D) structural hazard

**Q72.** Operand forwarding (bypassing) in a pipelined datapath is used primarily to
(A) eliminate structural hazards
(B) reduce stalls caused by data hazards
(C) predict branch outcomes
(D) increase the clock frequency

**Q73.** A "write after read" (WAR) dependency is called a(n)
(A) true dependency  (B) anti-dependency  (C) output dependency  (D) control dependency

**Q74.** A "write after write" (WAW) dependency is called a(n)
(A) true dependency  (B) anti-dependency  (C) output dependency  (D) structural dependency

**Q75.** Which dependency **cannot** be removed by register renaming?
(A) RAW  (B) WAR  (C) WAW  (D) all can be removed

**Q76.** A structural hazard on a unified memory (an instruction fetch clashing with a data access) is best solved by
(A) branch prediction
(B) providing separate instruction and data caches
(C) operand forwarding
(D) register renaming

**Q77.** Even with full operand forwarding, a load immediately followed by an instruction using the loaded value still incurs
(A) 0 stall cycles  (B) 1 stall cycle  (C) 2 stall cycles  (D) 3 stall cycles

**Q78.** A control (branch) hazard occurs because
(A) two instructions need the same resource
(B) the next instruction to fetch is unknown until the branch is resolved
(C) an instruction needs a not-yet-produced value
(D) the cache misses

**Q79.** A common hardware/software technique to mitigate control hazards is
(A) operand forwarding  (B) branch prediction  (C) a larger cache  (D) adding more registers

**Q80.** With a delayed branch (delay slot), the instruction immediately after the branch
(A) is always flushed  (B) always executes  (C) is never fetched  (D) always stalls the pipeline

**Q81.** Which dynamic branch predictor mispredicts only once per loop (rather than twice)?
(A) 1-bit predictor  (B) 2-bit saturating counter  (C) static not-taken  (D) none of these

**Q82.** In a pipeline where 20% of instructions are branches with a 3-cycle penalty and no prediction, the average CPI is
(A) 1.6  (B) 1.06  (C) 3.0  (D) 0.6

**Q83.** For the same machine but with a branch predictor that is 90% accurate, the average CPI is
(A) 1.06  (B) 1.60  (C) 1.30  (D) 1.00

**Q84.** Register renaming can eliminate which hazards?
(A) RAW only  (B) WAR and WAW  (C) all data hazards  (D) structural hazards

---

## Part H — Memory hierarchy, locality, SRAM vs DRAM

**Q85.** Cache memory works effectively because programs exhibit
(A) locality of reference  (B) recursion  (C) virtualisation  (D) pipelining

**Q86.** Temporal locality refers to the tendency to
(A) access nearby addresses soon
(B) reuse a recently used item again soon
(C) access memory at random
(D) access only sequential addresses

**Q87.** Spatial locality refers to the tendency to
(A) reuse the same item soon
(B) access memory locations near a recently accessed one
(C) access memory at random
(D) follow no pattern

**Q88.** Caches fetch an entire block rather than a single word because of
(A) temporal locality  (B) spatial locality  (C) neither locality  (D) DRAM refresh

**Q89.** Moving down the memory hierarchy (registers → disk),
(A) capacity decreases
(B) access time increases while cost per bit decreases
(C) speed increases
(D) everything becomes faster

**Q90.** SRAM stores each bit in
(A) a capacitor  (B) a flip-flop (~6 transistors)  (C) a fuse  (D) a magnetic domain

**Q91.** DRAM needs periodic refresh because
(A) its flip-flops decay
(B) the storage capacitor leaks charge over time
(C) it is non-volatile
(D) it uses six transistors per cell

**Q92.** In a typical computer, cache is built from ____ and main memory from ____.
(A) DRAM / SRAM  (B) SRAM / DRAM  (C) DRAM / DRAM  (D) SRAM / SRAM

**Q93.** Both SRAM and DRAM are
(A) non-volatile  (B) volatile  (C) DRAM is non-volatile  (D) SRAM is non-volatile

**Q94.** DRAM achieves higher density than SRAM because each cell uses
(A) six transistors  (B) one transistor plus one capacitor  (C) no transistor  (D) a flip-flop

---

## Part I — Cache mapping & address splitting

**Q95.** A direct-mapped cache of size 8 KB uses a block size of 32 bytes. With a 32-bit physical address, the (tag, index, offset) field widths are
(A) 19, 8, 5  (B) 18, 9, 5  (C) 19, 5, 8  (D) 20, 7, 5

**Q96.** In a direct-mapped cache, a given memory block
(A) may be placed in any line
(B) maps to exactly one line (block number mod number of lines)
(C) may be placed in any of k lines of a set
(D) always occupies two lines

**Q97.** In a fully associative cache, a block from main memory
(A) can be placed in exactly one cache line
(B) can be placed in any cache line
(C) can be placed in one of k lines of a set
(D) cannot be replaced

**Q98.** In a k-way set-associative cache, a block
(A) maps to exactly one line
(B) maps to one set and may occupy any of the k lines in that set
(C) may go in any line anywhere
(D) is fixed to two lines

**Q99.** The number of sets in a set-associative cache equals
(A) number of lines × associativity
(B) number of lines ÷ associativity
(C) number of blocks × associativity
(D) the offset value

**Q100.** For a 64-byte block, the number of block-offset bits is
(A) 4  (B) 5  (C) 6  (D) 7

**Q101.** A 2-way set-associative cache has 128 lines and a 64-byte block size. The number of sets is
(A) 32  (B) 64  (C) 128  (D) 2

**Q102.** For the cache of Q101, the number of index bits is
(A) 5  (B) 6  (C) 7  (D) 8

**Q103.** A 4-way set-associative cache of 64 KB uses 32-byte blocks with a 32-bit address. The (tag, index, offset) widths are
(A) 18, 9, 5  (B) 19, 8, 5  (C) 17, 10, 5  (D) 18, 8, 6

**Q104.** A direct-mapped cache of 16 KB uses 16-byte blocks with a 32-bit address. The number of tag bits is
(A) 18  (B) 14  (C) 16  (D) 20

**Q105.** A fully associative cache of 16 KB uses 32-byte blocks with a 32-bit address. The number of tag bits is
(A) 27  (B) 19  (C) 22  (D) 32

**Q106.** A 1 MB, 4-way set-associative cache uses 64-byte blocks with a 40-bit physical address. The number of index bits is
(A) 10  (B) 12  (C) 14  (D) 16

**Q107.** For the cache of Q106, the number of tag bits is
(A) 18  (B) 20  (C) 22  (D) 24

**Q108.** If the block size is doubled while total cache size and associativity are held fixed, the number of sets
(A) doubles  (B) halves  (C) is unchanged  (D) quadruples

**Q109.** Which cache organisation has no conflict misses by definition?
(A) direct-mapped  (B) 2-way set-associative  (C) fully associative  (D) 4-way set-associative

**Q110.** A 32 KB direct-mapped cache uses 64-byte blocks with a 32-bit address. The number of index bits is
(A) 8  (B) 9  (C) 10  (D) 7

---

## Part J — Average Memory Access Time (AMAT)

**Q111.** A cache access time is 10 ns and main-memory access time is 100 ns. On a miss the word is fetched from memory **after** the cache lookup fails (hierarchical). With hit ratio 0.9, AMAT is
(A) 19 ns  (B) 20 ns  (C) 55 ns  (D) 100 ns

**Q112.** For the same figures as Q111 but with the cache and memory searched **simultaneously**, AMAT is
(A) 19 ns  (B) 20 ns  (C) 21 ns  (D) 18 ns

**Q113.** The hierarchical (sequential) AMAT formula is
(A) h·T_c + (1 − h)·T_m
(B) T_c + (1 − h)·T_m
(C) T_c + T_m
(D) h·T_m

**Q114.** The simultaneous (parallel) AMAT formula is
(A) h·T_c + (1 − h)·T_m
(B) T_c + (1 − h)·T_m
(C) T_c + T_m
(D) (1 − h)·T_c

**Q115.** With T_c = 1 ns, T_m = 100 ns and hit ratio 0.95 (hierarchical), AMAT is
(A) 5.95 ns  (B) 6 ns  (C) 5 ns  (D) 6.05 ns

**Q116.** Two-level cache: T_L1 = 1 ns (miss rate 5%), T_L2 = 10 ns (miss rate 20%), T_mem = 100 ns. AMAT is
(A) 2.5 ns  (B) 3 ns  (C) 6 ns  (D) 1.5 ns

**Q117.** With hit ratio 0.8, T_c = 20 ns and T_m = 200 ns (hierarchical), AMAT is
(A) 40 ns  (B) 60 ns  (C) 180 ns  (D) 200 ns

**Q118.** With hit ratio 0.85, T_c = 5 ns and T_m = 70 ns, cache and memory accessed **simultaneously**, AMAT is
(A) 14.75 ns  (B) 15 ns  (C) 10.75 ns  (D) 70 ns

---

## Part K — Write policies, replacement policies & the three Cs

**Q119.** In the write-back (copy-back) cache policy, main memory is updated
(A) on every write to the cache
(B) only when the modified block is evicted from the cache
(C) at every clock cycle
(D) never

**Q120.** The write-back policy requires each cache line to carry a
(A) valid bit only  (B) dirty bit  (C) tag only  (D) nothing extra

**Q121.** In the write-through policy, main memory is updated
(A) only on eviction  (B) on every write  (C) never  (D) only during refresh

**Q122.** A cache line's dirty bit is set when the line is
(A) first loaded  (B) written/modified  (C) merely read  (D) evicted

**Q123.** On a write miss, the write-allocate policy
(A) writes only to memory, skipping the cache
(B) fetches the block into the cache first, then writes
(C) ignores the write
(D) flushes the whole cache

**Q124.** The replacement policy generally giving the best practical hit rate (exploiting temporal locality) is
(A) FIFO  (B) LRU  (C) Random  (D) MRU

**Q125.** Which replacement policy can suffer from Belady's anomaly?
(A) LRU  (B) FIFO  (C) LFU  (D) Optimal

**Q126.** The Optimal (OPT/MIN) replacement policy is
(A) the cheapest to build in hardware
(B) unimplementable in practice and used only as a benchmark
(C) identical to FIFO
(D) the same as random replacement

**Q127.** A direct-mapped cache requires which replacement policy?
(A) LRU  (B) FIFO  (C) none — there is only one possible location  (D) random

**Q128.** The "three Cs" model classifies cache misses as
(A) cold, cache, conflict
(B) compulsory, capacity, conflict
(C) compulsory, capacity, coherence
(D) capacity, conflict, coherence

**Q129.** Compulsory (cold-start) misses are most directly reduced by
(A) a larger cache  (B) higher associativity  (C) a larger block size / prefetching  (D) write-back

**Q130.** Capacity misses are most directly reduced by
(A) a larger cache  (B) higher associativity  (C) a smaller block size  (D) write-through

**Q131.** Conflict misses are most directly reduced by
(A) a larger block size  (B) higher associativity  (C) write-back  (D) more frequent refresh

---

## Part L — Main memory organisation, interleaving & chip count

**Q132.** Memory interleaving is used mainly to
(A) increase memory capacity
(B) allow overlapped access to several memory banks, improving bandwidth
(C) reduce the number of address lines
(D) implement virtual memory

**Q133.** In a 4-way low-order interleaved memory, address 4 lies in bank
(A) 0  (B) 1  (C) 2  (D) 3

**Q134.** The number of chips needed to build a 16K × 8 memory from 4K × 4 chips is
(A) 4  (B) 8  (C) 16  (D) 2

**Q135.** A 16K × 8 memory requires how many address lines?
(A) 8  (B) 14  (C) 16  (D) 13

**Q136.** The number of chips needed to build a 1M × 8 memory from 256K × 1 chips is
(A) 8  (B) 16  (C) 32  (D) 4

**Q137.** The number of chips needed to build a 64K × 16 memory from 16K × 8 chips is
(A) 4  (B) 6  (C) 8  (D) 16

**Q138.** A memory with 1M (2²⁰) locations requires how many address lines?
(A) 10  (B) 16  (C) 20  (D) 24

**Q139.** In a 4-way low-order interleaved memory, address 5 lies in bank
(A) 0  (B) 1  (C) 2  (D) 3

---

## Part M — Secondary storage: the magnetic disk

**Q140.** A disk rotates at 6000 RPM. The average rotational latency is
(A) 2.5 ms  (B) 5 ms  (C) 10 ms  (D) 16.6 ms

**Q141.** Total disk access time is the sum of
(A) seek time + rotational latency + transfer time
(B) seek time + transfer time only
(C) rotational latency + transfer time only
(D) seek time + rotational latency only

**Q142.** The average rotational latency of a disk (in seconds) equals
(A) 60 / RPM  (B) 30 / RPM  (C) 15 / RPM  (D) RPM / 60

**Q143.** A 7200 RPM disk has an average rotational latency of about
(A) 8.33 ms  (B) 4.17 ms  (C) 2 ms  (D) 5 ms

**Q144.** A 15000 RPM disk has an average rotational latency of
(A) 4 ms  (B) 2 ms  (C) 1 ms  (D) 3 ms

**Q145.** Disk access time is dominated by
(A) transfer time
(B) seek time and rotational latency
(C) controller overhead
(D) decode time

**Q146.** Total disk capacity is computed as
(A) tracks × sectors
(B) surfaces × tracks/surface × sectors/track × bytes/sector
(C) sectors × bytes
(D) cylinders only

**Q147.** A cylinder on a disk is
(A) a single sector
(B) the set of same-numbered tracks across all platters (reachable without moving the head)
(C) one entire platter
(D) one read/write head

**Q148.** A disk rotates at 3000 RPM. Its average rotational latency is
(A) 5 ms  (B) 10 ms  (C) 20 ms  (D) 15 ms

---

## Part N — I/O organisation, interrupts & DMA

**Q149.** The principal advantage of DMA over interrupt-driven I/O is that
(A) it needs no controller hardware
(B) data transfer bypasses the CPU, reducing CPU involvement per word
(C) it is always slower but simpler
(D) it eliminates the need for main memory

**Q150.** The DMA technique in which the controller takes the bus for one bus cycle at a time, letting the CPU continue in between, is
(A) burst mode  (B) cycle stealing  (C) transparent mode  (D) interrupt mode

**Q151.** The main drawback of programmed I/O (polling) is that
(A) it needs a DMA controller
(B) the CPU busy-waits, wasting cycles
(C) it causes too many interrupts
(D) it has no status register

**Q152.** The main drawback of interrupt-driven I/O compared with DMA is that
(A) the CPU busy-waits
(B) the CPU still handles every single word, causing many interrupts per block
(C) it uses no interrupts
(D) it bypasses the CPU entirely

**Q153.** The I/O technique with the lowest CPU involvement is
(A) programmed I/O  (B) interrupt-driven I/O  (C) DMA  (D) polling

**Q154.** In a DMA block transfer, the number of interrupts raised to the CPU per block is
(A) zero  (B) one (at completion)  (C) one per word  (D) many

**Q155.** In DMA burst (block) mode, the controller
(A) takes one bus cycle at a time
(B) holds the bus for the entire block, stalling the CPU
(C) transfers only in idle cycles
(D) never uses the bus

**Q156.** In DMA transparent (hidden) mode, the controller
(A) holds the bus for the whole transfer
(B) transfers only in cycles when the CPU does not need the bus, causing no CPU slowdown
(C) steals one cycle at a time from a busy CPU
(D) is the fastest transfer mode

**Q157.** A non-maskable interrupt (NMI)
(A) can be disabled by software
(B) cannot be disabled and is reserved for catastrophic events
(C) always has the lowest priority
(D) is generated only by software

**Q158.** In daisy-chaining priority, the device with the highest priority is the one
(A) farthest from the CPU
(B) nearest to the CPU
(C) chosen at random
(D) all equal

**Q159.** In a vectored interrupt scheme,
(A) the ISR address is fixed and the CPU must poll to find the source
(B) the interrupting device supplies the ISR address (vector)
(C) no ISR address exists
(D) only software can trigger it

**Q160.** In memory-mapped I/O,
(A) devices live in a separate I/O address space
(B) device registers occupy ordinary memory addresses, so any load/store instruction can access them
(C) special IN/OUT instructions are mandatory
(D) devices have no addresses

**Q161.** Isolated (port-mapped) I/O is characterised by
(A) sharing the memory address space
(B) a separate I/O address space needing special IN/OUT instructions
(C) requiring no special instructions
(D) being identical to memory-mapped I/O

**Q162.** On accepting an interrupt, the CPU first saves
(A) only the PC
(B) the PC and PSW (its context)
(C) the entire cache
(D) nothing

**Q163.** Interrupts are normally honoured
(A) in the middle of an instruction
(B) after the current instruction finishes (between instructions)
(C) never during a program
(D) only at reset

**Q164.** The phrase "cycle stealing" refers to stealing
(A) CPU (execution) cycles
(B) memory/bus cycles, while the CPU keeps executing register-only work
(C) cache lines
(D) register contents

**Q165.** A software interrupt (trap) is the mechanism used to implement
(A) power-failure handling  (B) system calls  (C) divide-by-zero detection  (D) DMA transfers

---

## Part O — Paper-I (English, Reasoning, GK)

**Q166.** Choose the correctly spelt word.
(A) Occurence  (B) Occurrence  (C) Ocurrence  (D) Occurrance

**Q167.** Identify the part containing the error: *"Neither of the two candidates (A)/ have submitted (B)/ their documents (C)/ before the deadline. (D)"*
(A) A  (B) B  (C) C  (D) D

**Q168.** Pointing to a photograph, a man said, *"She is the daughter of my grandfather's only son."* How is the woman related to the man?
(A) Sister  (B) Daughter  (C) Niece  (D) Cousin

**Q169.** A shopkeeper marks an article 40% above cost price and then allows a discount of 25%. His profit percentage is
(A) 5%  (B) 10%  (C) 15%  (D) 20%

**Q170.** The highest peak of Tripura, Betlingchhip, is located in which hill range?
(A) Jampui Hills  (B) Atharamura Hills  (C) Baramura Hills  (D) Longtharai Hills

**Q171.** Choose the word most nearly opposite in meaning to **benevolent**.
(A) generous  (B) malevolent  (C) kind  (D) gracious

**Q172.** One word for "a person who knows and can use many languages" is
(A) linguist  (B) polyglot  (C) orator  (D) bilingual

**Q173.** In a certain code MADRAS is written as NBESBT. How is DELHI written in that code?
(A) EFMIJ  (B) EFMJI  (C) DFMIJ  (D) EFLIJ

**Q174.** A man walks 3 km due north, then turns and walks 4 km due east. How far is he from the starting point?
(A) 7 km  (B) 5 km  (C) 1 km  (D) 25 km

**Q175.** Find the next term in the series: 2, 6, 12, 20, 30, ?
(A) 40  (B) 42  (C) 44  (D) 36

**Q176.** Doctor : Hospital :: Teacher : ?
(A) Class  (B) School  (C) Student  (D) Book

**Q177.** Tripura became a full-fledged state of the Indian Union in the year
(A) 1949  (B) 1956  (C) 1963  (D) 1972

**Q178.** The capital of Tripura is
(A) Agartala  (B) Aizawl  (C) Shillong  (D) Imphal

**Q179.** The first President of India was
(A) Jawaharlal Nehru  (B) Dr. Rajendra Prasad  (C) Dr. S. Radhakrishnan  (D) Sardar Patel

**Q180.** A can do a piece of work in 10 days and B in 15 days. Working together, they finish it in
(A) 5 days  (B) 6 days  (C) 12.5 days  (D) 25 days

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 31 | C | 61 | B | 91 | B | 121 | B | 151 | B |
| 2 | B | 32 | C | 62 | B | 92 | B | 122 | B | 152 | B |
| 3 | C | 33 | C | 63 | B | 93 | B | 123 | B | 153 | C |
| 4 | B | 34 | B | 64 | B | 94 | B | 124 | B | 154 | B |
| 5 | B | 35 | B | 65 | B | 95 | A | 125 | B | 155 | B |
| 6 | B | 36 | C | 66 | C | 96 | B | 126 | B | 156 | B |
| 7 | B | 37 | B | 67 | B | 97 | B | 127 | C | 157 | B |
| 8 | B | 38 | D | 68 | B | 98 | B | 128 | B | 158 | B |
| 9 | B | 39 | B | 69 | B | 99 | B | 129 | C | 159 | B |
| 10 | B | 40 | B | 70 | B | 100 | C | 130 | A | 160 | B |
| 11 | B | 41 | A | 71 | A | 101 | B | 131 | B | 161 | B |
| 12 | B | 42 | B | 72 | B | 102 | B | 132 | B | 162 | B |
| 13 | D | 43 | B | 73 | B | 103 | A | 133 | A | 163 | B |
| 14 | B | 44 | C | 74 | C | 104 | A | 134 | B | 164 | B |
| 15 | C | 45 | B | 75 | A | 105 | A | 135 | B | 165 | B |
| 16 | A | 46 | B | 76 | B | 106 | B | 136 | C | 166 | B |
| 17 | A | 47 | B | 77 | B | 107 | C | 137 | C | 167 | B |
| 18 | B | 48 | B | 78 | B | 108 | B | 138 | C | 168 | A |
| 19 | B | 49 | B | 79 | B | 109 | C | 139 | B | 169 | A |
| 20 | C | 50 | B | 80 | B | 110 | B | 140 | B | 170 | A |
| 21 | B | 51 | C | 81 | B | 111 | B | 141 | A | 171 | B |
| 22 | C | 52 | B | 82 | A | 112 | A | 142 | B | 172 | B |
| 23 | B | 53 | B | 83 | A | 113 | B | 143 | B | 173 | A |
| 24 | B | 54 | B | 84 | B | 114 | A | 144 | B | 174 | B |
| 25 | A | 55 | B | 85 | A | 115 | B | 145 | B | 175 | B |
| 26 | A | 56 | A | 86 | B | 116 | A | 146 | B | 176 | B |
| 27 | C | 57 | B | 87 | B | 117 | B | 147 | B | 177 | D |
| 28 | A | 58 | B | 88 | B | 118 | A | 148 | B | 178 | A |
| 29 | B | 59 | B | 89 | B | 119 | B | 149 | B | 179 | B |
| 30 | C | 60 | A | 90 | B | 120 | B | 150 | B | 180 | B |

---

# 📝 Detailed Solutions

**Q1. (B)** A von Neumann machine stores instructions and data in the *same* memory and reaches it over a *single* bus. Because only one thing can travel on that bus at a time, the CPU cannot fetch an instruction and read/write a data word in the same moment — it must alternate. This traffic jam is the "von Neumann bottleneck," and it means the memory bus, not the raw speed of the CPU, sets the pace of most real programs. Options A, C and D describe real limitations in some systems, but none is *the* bottleneck named after von Neumann.

**Q2. (B)** Harvard architecture keeps instructions and data in two physically separate memories, each with its own bus. Because the two buses are independent, the processor can fetch the next instruction and read a data operand at the very same time — exactly the parallelism a von Neumann machine lacks. This is why DSPs and small microcontrollers, which need predictable back-to-back memory access, favour it. Option A is von Neumann; C and D are unrelated.

**Q3. (C)** A "modified Harvard" design keeps a single unified main memory (the von Neumann part) but splits the fastest cache level into a separate L1 instruction cache and L1 data cache (the Harvard part). This gives the best of both worlds: one flexible memory for storage, plus parallel instruction/data access at the level where speed matters most. That is precisely how nearly all modern CPUs are built, so it is neither "pure" style.

**Q4. (B)** "Architecture" is the *contract* the programmer sees — the instruction set, the registers, the addressing modes — i.e. what the machine can be told to do. "Organization" is *how that contract is implemented in hardware* — the pipelines, caches and buses inside. Two chips can share the same architecture (both run x86 code) yet be organised very differently (a phone chip vs a server chip). Option A swaps the two definitions; C and D are simply wrong.

**Q5. (B)** The Program Counter always holds the *address* of the next instruction the CPU will fetch — think of it as a bookmark pointing at the next line of the program. During each fetch it is automatically advanced, and a jump/branch works by writing a new address into it. It never holds an instruction (that is the IR) or data. Remembering "PC = address, IR = instruction" clears up the most common trap in this topic.

**Q6. (B)** The Instruction Register stores the actual instruction word that was just fetched from memory, so the control unit can decode and execute it. In the fetch micro-sequence the instruction travels memory → MDR → IR. It holds the instruction *itself*, not an address (that is the PC) and not a data operand.

**Q7. (B)** MAR = Memory *Address* Register. Whenever the CPU wants to read or write memory, it first places the target address into the MAR, which drives the address bus. The mnemonic is "MAR ↔ Address." It never holds the data being transferred — that job belongs to the MDR.

**Q8. (B)** MDR (also called MBR, Memory Buffer Register) = Memory *Data* Register. It is the temporary holding box for the data word moving between the CPU and memory: on a read the value comes memory → MDR, and on a write it goes MDR → memory. Mnemonic: "MDR ↔ Data." The address it pairs with sits in the MAR.

**Q9. (B)** This tests the single most-swapped pair. Correct: the PC holds the *address of the next instruction*, while the IR holds the *current instruction being executed*. Option A reverses them (a classic distractor), C wrongly makes both hold data, and D confuses the MAR (which holds an address, not data).

**Q10. (B)** Every instruction runs through the same endless loop: **Fetch** the instruction from memory, **Decode** it to work out what it means, then **Execute** it. (A fuller version adds operand-fetch and write-back, but the core order is Fetch → Decode → Execute.) The other options scramble this order.

**Q11. (B)** Inside the fetch phase the CPU copies the instruction's address into MAR, reads the instruction, and *then does `PC ← PC + 1`* — all before the instruction actually executes. Incrementing early is deliberate: it is why a jump instruction just overwrites the already-advanced PC, and why PC-relative offsets are measured from the *following* instruction. It is not done after execution, and it happens for every instruction, not only jumps.

**Q12. (B)** Registers are a tiny handful of storage cells fabricated on the CPU die itself, sitting right beside the ALU. Being on-chip and few in number, they can be read/written in a fraction of a nanosecond, versus roughly 100 ns for off-chip main memory. They are made from fast flip-flops (SRAM-like), not DRAM, and they are far *smaller* than memory, not larger — their smallness is part of why they are fast.

**Q13. (D)** A stack machine keeps operands on an internal stack, so an arithmetic instruction like `ADD` needs *no address fields at all* — it simply pops the top two values and pushes the result. That is what "zero-address" means. One-address = accumulator, two/three-address name their operands explicitly.

**Q14. (B)** A one-address instruction names a single memory operand; the *other* operand and the destination are an implicit special register called the **accumulator** (e.g. `ADD B` means AC ← AC + B). Hence one-address ⇒ accumulator machine. Zero-address is the stack machine, and three-address is the general-register machine.

**Q15. (C)** On a stack machine you push operands and then apply operators, and that push/operator ordering is exactly **postfix (reverse Polish) notation** — operators come *after* their operands. For example `A B + C D + *`. Infix (A+B) and prefix (+AB) are different notations that stack machines do not directly use.

**Q16. (A)** Convert step by step. `A + B` → `AB+`. `C + D` → `CD+`. Multiplying the two results puts the `*` last: `AB+CD+*`. Read it as "add A and B, add C and D, then multiply the two sums." Option B has the operators mis-grouped, and C/D are not valid postfix for this expression.

**Q17. (A)** A three-address instruction can name destination and both sources at once, so each `(x op y → z)` step is a single instruction: `ADD T1, A, B`; `ADD T2, C, D`; `MUL X, T1, T2`. That is 3 instructions — the fewest of any format. Machines with fewer address fields (two/one/zero-address) need more instructions for the same expression.

**Q18. (B)** In a stack computer `ADD` is implicit: it removes (pops) the top two stack entries, adds them, and pushes the single result back. No register names or memory addresses appear in the instruction. Option A describes a register machine, C an accumulator machine, and D a three-address machine.

**Q19. (B)** With a fixed n-bit opcode you can only ever name 2ⁿ instructions. An **expanding opcode** reclaims the bit patterns left unused by instructions that need fewer operands: those freed operand bits are folded back into the opcode field. This lets a machine have, say, many zero-address instructions *and* a few three-address ones without wasting encoding space. It has nothing to do with clock speed, register count or caches.

**Q20. (C)** An opcode field of n bits has 2ⁿ possible bit patterns, and each distinct pattern can name one instruction — so 2ⁿ instructions maximum. For example, 4 opcode bits allow 2⁴ = 16 instructions. Answers n, 2n and n² do not match how binary encoding works.

**Q21. (B)** On a two-address machine the destination operand doubles as one of the sources to save an address field, so `ADD A, B` means "A ← A + B" (add B into A, overwriting A). This is why two-address code needs extra MOV instructions to preserve values. `A ← B` is a MOV, and the others name a wrong destination.

**Q22. (C)** Here the effective address is computed as *register contents + a constant offset carried in the instruction* — the base-plus-displacement (a form of indexed) mode. It is the everyday mode for reaching an array element (base + scaled index) or a field inside a stack frame/struct (frame pointer + fixed offset). Immediate has no memory address, direct uses only the address field, and register-direct's operand is in the register itself.

**Q23. (B)** A pointer *is* an address stored in memory, and dereferencing it means "go to the address that this location holds." That double step — read the pointer, then read what it points to — is exactly **indirect addressing** (EA = M[address field]). Immediate is for constants, indexed for arrays, register-direct for temporaries.

**Q24. (B)** **Indexed** addressing forms EA = base address + index register, so incrementing the index register walks through consecutive array elements. That is literally why the mode exists. Immediate handles constants, direct handles single globals, and implied has no operand address.

**Q25. (A)** A constant whose value is known when the program is assembled is simply embedded inside the instruction word — that is **immediate** addressing (e.g. `MOV R2, #5`). No memory or register access is needed to fetch it. Direct/indirect/indexed all point at memory, which is unnecessary for a fixed constant.

**Q26. (A)** Branches specify their target as an *offset from the current PC*, i.e. **PC-relative** addressing (EA = PC + offset). Because the target is expressed relatively, the same code runs correctly wherever it is loaded, which also gives position-independent code. The other modes fix an absolute location and lack this relocatability.

**Q27. (C)** Memory-indirect addressing needs **two** memory reads to get the operand: first read the pointer stored at the address field, then read the actual data at the address the pointer gave. That double trip is why indirect is the slowest mode. (Immediate and register-direct need 0; direct and register-indirect need 1.)

**Q28. (A)** In register-direct addressing the operand is *already sitting in a CPU register*, so fetching it requires **zero** memory accesses. This is exactly why RISC machines keep working values in registers — it is the fastest possible operand access.

**Q29. (B)** Direct (absolute) addressing puts the operand's address straight in the instruction, so the CPU makes **one** memory read to fetch the operand. Compare: register-direct = 0, indirect = 2. One access sits neatly in the middle.

**Q30. (C)** **Register-direct** is fastest because the operand lives in a register and needs *no* memory access at all (0 references). Indirect (2 accesses) is slowest, and direct/indexed touch memory once, so all are slower than register-direct.

**Q31. (C)** **Indirect** is slowest because it makes two memory references per operand (read the pointer, then read the target). Immediate and register-direct make none, and direct makes one, so indirect loses every time on speed.

**Q32. (C)** Base-plus-displacement means EA = (contents of the base register) + (the constant displacement). Here R1 = 1000 and the displacement = 20, so EA = 1000 + 20 = **1020**. R2 then receives whatever data lives at memory address 1020.

**Q33. (C)** Memory-indirect works in two hops. Hop 1: the address field is 1000, so read M[1000] = 2000 (that is the pointer). Hop 2: go to address 2000 and read M[2000] = **55**, the actual operand. So the value loaded is 55, not the intermediate 2000.

**Q34. (B)** Register-indirect means the register holds the address of the operand. Here R1 = 1000, so the effective address is 1000, and the value loaded is M[1000] = **2000**. There is only one memory access (unlike memory-indirect's two), so we stop at 2000 and do not chase it further to 55.

**Q35. (B)** Auto-increment addressing uses a register as a pointer and then automatically adds the element size to it, so each access is ready to grab the *next* element. That makes it ideal for **walking through arrays** and for stack push/pop operations. It is not how constants, branches or subroutine calls are addressed.

**Q36. (C)** In immediate addressing the operand value is stored *inside the instruction word itself* (e.g. the `#5` in `MOV R2, #5`), so it comes along for free with no separate memory or register fetch. It is not in memory, a register, or on the stack.

**Q37. (B)** Indexed EA = base + (index × element size). The element size is 4 bytes and the index is 10, so the offset is 4 × 10 = 40. EA = 5000 + 40 = **5040**. (Distractor 5010 forgets to scale by element size; 5400 mis-scales; 9000 wrongly multiplies.)

**Q38. (D)** RISC deliberately keeps instructions *few, simple, and fixed-length*. A large set of complex, variable-length instructions is the hallmark of **CISC**, the opposite philosophy — so D is the odd one out. Fixed length (A), load/store design (B), and many registers (C) are all genuine RISC traits.

**Q39. (B)** RISC uses **fixed-length** instructions (e.g. every instruction 32 bits). Uniform length means every instruction is fetched and decoded the same way and takes the same path through the pipeline, which is what makes clean pipelining possible. CISC uses variable-length instructions.

**Q40. (B)** RISC is a "load/store architecture": *only* the LOAD and STORE instructions touch memory, and every other instruction operates purely on registers. Keeping memory access to two well-defined instructions makes instruction timing uniform and pipelining easy. In CISC, by contrast, many instructions can read/write memory directly.

**Q41. (A)** Because RISC has a small, regular instruction set, its control signals can be produced by a fast, fixed logic circuit — a **hardwired** control unit — giving high speed. CISC, with its large irregular instruction set, leans on microprogrammed control instead.

**Q42. (B)** CISC instruction sets are large and irregular, so building the control logic in fixed silicon would be enormously complex. Instead CISC uses **microprogrammed** control, where each instruction's control steps are stored as microcode in a small control memory — easier to design and to patch, at the cost of speed.

**Q43. (B)** RISC keeps the hardware simple and shifts the hard work of building complex operations onto **the compiler**, which strings together many simple instructions. CISC does the reverse: complexity lives in the hardware. Memory and cache are storage, not where this complexity is placed.

**Q44. (C)** **x86** (like VAX and the IBM 360) is a classic CISC architecture with variable-length, complex instructions. ARM, MIPS and RISC-V are all RISC designs with fixed-length, simple instructions.

**Q45. (B)** Modern x86 chips present a CISC instruction set on the outside but, inside, a decoder **translates each instruction into one or more simple RISC-like micro-operations** that a fast RISC-style core executes and pipelines. So in practice RISC principles won *inside* the chip. They certainly do pipeline and have registers, ruling out C and D.

**Q46. (B)** Besides computing a result, the ALU automatically sets the **condition flags** — Zero, Carry, Sign, Overflow — that summarise the outcome (e.g. was the result zero, did it overflow). Later conditional-branch instructions test these flags. The ALU does not set the PC, cache tags, or IR.

**Q47. (B)** The datapath is all the hardware that data physically flows *through*: the **registers, buses, multiplexers and the ALU**. It is essentially combinational logic plus registers and has no idea what it is doing on its own. The control signals that steer it come from a separate unit (the control unit), and memory/opcode are not the datapath itself.

**Q48. (B)** The control unit is the conductor: for each instruction, in each clock cycle, it **asserts the right control signals** ("select this MUX input," "make the ALU subtract," "write into R3") to steer the datapath. It does not itself do arithmetic (the ALU does), store program data (memory/registers do), or read disk.

**Q49. (B)** In microprogrammed control the signals for each step are read from a control memory, adding a lookup each cycle — so it is **slower** than hardwired. But because behaviour is defined by microcode rather than fixed wiring, you can change or add instructions just by rewriting the microcode — so it is **more flexible and easier to modify** (this is how CPU microcode updates fix bugs).

**Q50. (B)** Hardwired control is a fixed gate-and-flip-flop circuit, so its control signals appear after just a couple of gate delays with no memory lookup — making it **faster** than microprogrammed control. The trade-off is that changing the instruction set means redesigning the hardware.

**Q51. (C)** In a microprogrammed design the microinstructions live in a small, fast internal memory dedicated to the control unit, called **control memory** (or control store). It is separate from main memory, the data cache and the general registers.

**Q52. (B)** Just as a PC points at the next machine instruction, the **Control Address Register (CAR)** points at the **current microinstruction inside control memory**, sequencing the microprogram step by step. It does not address main memory, the data stack, or operands.

**Q53. (B)** A **horizontal** microinstruction is **wide and unencoded** — it has one bit per control signal, so the bit is fed directly to its signal with **no decoder** needed, and many signals can be asserted at once (**high parallelism**). Memory hook: "horizontal = a long horizontal row of bits = wide = parallel." The trade-off is a large control memory.

**Q54. (B)** A **vertical** microinstruction is **narrow**: control signals are packed into small **encoded fields**, so a **decoder** is required to expand each field back into individual signals, and only a few signals can fire per field (**low parallelism**). It saves control-memory width at the cost of a decode step and less parallelism.

**Q55. (B)** The inherent slowdown comes from the extra work per step: in microprogrammed control **every control step must first read a microinstruction from control memory** before the signals can be applied. Hardwired control skips this lookup, which is why it is faster. Register count, memory type and the clock are not the cause.

**Q56. (A)** As the number of instructions grows large, a k-stage pipeline can complete roughly one instruction per cycle instead of one every k cycles, so the speedup approaches **k**. Formally, speedup = nk/(k+n−1) → k as n → ∞. The maximum equals the number of stages; it never exceeds k.

**Q57. (B)** Use pipelined cycles = k + (n − 1). The first instruction needs all k = 5 cycles to fill the pipeline; each of the remaining 999 finishes one per cycle. So cycles = 5 + 999 = **1004**. (5000 would be the non-pipelined figure; 1000 and 1005 come from mis-remembering the formula.)

**Q58. (B)** The standard result is **k + n − 1**. Intuition: it takes k cycles for the very first instruction to pass through all k stages, and after that the pipeline delivers one finished instruction every cycle, i.e. (n − 1) more cycles. Adding gives k + (n − 1). Common wrong answers are k + n and n × k.

**Q59. (B)** Without pipelining, each instruction runs completely on its own through all k stages before the next one starts, so total time = **n × k** cycles. This is the baseline we compare the pipelined k + n − 1 against to get the speedup.

**Q60. (A)** Speedup = (non-pipelined cycles) ÷ (pipelined cycles) = (n × k) ÷ (k + n − 1) = **nk / (k + n − 1)**. For large n this tends to k. The other options are upside-down or otherwise not this ratio.

**Q61. (B)** Pipelining overlaps stages of different instructions, so more instructions *finish per unit time* — it raises **throughput**. It does **not** shorten how long a single instruction takes end-to-end (its latency is unchanged, or even slightly worse due to latch overhead). Think of the laundry analogy: overlapping loads finishes the batch sooner without making any one load wash faster.

**Q62. (B)** All stages share one clock, and every stage must finish within one clock tick, so the period must be as long as the **slowest stage's delay, plus the latch/register overhead** added between stages. Summing or averaging the stages is wrong; the fastest stage doesn't set the limit. This is why designers try to split slow stages.

**Q63. (B)** Cycles = k + (n − 1) = 4 + (100 − 1) = 4 + 99 = **103**. (400 is the non-pipelined n × k; 104 mis-adds; 100 ignores fill time.)

**Q64. (B)** Cycles = k + (n − 1) = 6 + (200 − 1) = 6 + 199 = **205**. (1200 is non-pipelined; 206 over-adds by one.)

**Q65. (B)** Speedup = nk/(k+n−1) = (1000 × 5)/(5 + 1000 − 1) = 5000/1004 ≈ **4.98**. This is very close to the theoretical maximum of 5 because n (1000) is far larger than k (5), so the fill time is negligible.

**Q66. (C)** With only 5 instructions the pipeline's fill time is a big fraction of the total. Pipelined cycles = k + n − 1 = 5 + 4 = 9; non-pipelined = n × k = 25. Speedup = 25/9 ≈ **2.78** — well short of 5, showing pipelining pays off only for long instruction streams.

**Q67. (B)** The clock must accommodate the slowest stage plus latch overhead. Slowest stage = max(10, 8, 12, 9) = 12 ns; add the 1 ns latch overhead → **13 ns**. (39 ns is the sum of all stages, which would apply only without pipelining.)

**Q68. (B)** For large n, speedup ≈ (non-pipelined time per instruction) ÷ (clock period) = 39 ÷ 13 = **3**. Note it is only 3, not 4, because the unbalanced stages (one at 12 ns) inflate the clock period — balanced stages would give a better speedup.

**Q69. (B)** Since every stage is clocked together and each must complete within one tick, the **slowest stage** dictates the clock for all of them — a pipeline is only as fast as its worst stage. The fastest stage and the instruction count don't set the clock, and latch overhead is only an add-on.

**Q70. (B)** Clock period = (slowest stage) + (latch overhead) = max(60, 50, 90, 80) + 5 = 90 + 5 = **95 ns**. (280 is the sum of stages; 285 adds latch to that sum, which is wrong for a pipeline.)

**Q71. (A)** RAW ("read after write") means an instruction needs to *read* a value that an earlier instruction hasn't *written* yet — a genuine producer-to-consumer flow of data, i.e. a **true data dependency**. Because it reflects real data flow, it cannot be removed by renaming (unlike WAR/WAW). It is a data hazard, not a structural one.

**Q72. (B)** Operand forwarding (bypassing) routes an ALU result *directly* to the input of a following instruction instead of making it wait until the result is written back to the register file. This eliminates most of the stalls caused by **data (RAW) hazards**. It does nothing for structural hazards or branch prediction and doesn't change clock frequency.

**Q73. (B)** WAR ("write after read") is an **anti-dependency**: a later instruction wants to *write* a register that an earlier instruction still needs to *read* first. It is only a conflict over the register *name*, not over an actual value, so register renaming can remove it.

**Q74. (C)** WAW ("write after write") is an **output dependency**: two instructions write the same register and must do so in program order so the final value is correct. Like WAR, it is a name conflict, not a data-flow conflict, so renaming can eliminate it.

**Q75. (A)** **RAW** is a true data dependency — the second instruction genuinely needs the value the first produces — so no amount of renaming can remove the real flow of data. WAR and WAW are mere name conflicts (both instructions just happen to use the same register name), so giving one a fresh physical register makes them vanish. Hence only RAW resists renaming.

**Q76. (B)** A structural hazard is two instructions needing the *same hardware* at once — e.g. one instruction reading data from memory (MEM stage) while another fetches an instruction (IF stage) through a single memory port. The fix is to *duplicate the resource*: **separate instruction and data caches** give each its own port, so both accesses proceed. Forwarding and renaming fix data hazards, and prediction fixes control hazards.

**Q77. (B)** A load's data only becomes available after its MEM stage, one stage later than an ALU result. So if the very next instruction needs that loaded value, forwarding cannot deliver it in time and the pipeline must insert **1 stall cycle** (the load-use hazard). Compilers try to fill that one slot with an unrelated instruction.

**Q78. (B)** A control (branch) hazard happens because right after a branch the CPU **doesn't yet know which instruction to fetch next** — the branch condition and target aren't resolved until a later stage. Meanwhile it may have already fetched wrong instructions that must be discarded (flushed). Option A is a structural hazard, C is a data hazard, D is a cache miss.

**Q79. (B)** **Branch prediction** — guessing the branch outcome and target so the pipeline keeps fetching useful instructions — is the main way to hide control-hazard penalties (along with delay slots). Forwarding and extra registers address data hazards, and a bigger cache addresses miss rates, none of which fix branches.

**Q80. (B)** With a delayed branch the instruction placed in the "delay slot" right after the branch **always executes**, regardless of whether the branch is taken. The compiler tries to fill that slot with a genuinely useful instruction so the cycle isn't wasted. MIPS famously used this technique. It is neither flushed nor stalled.

**Q81. (B)** A **2-bit saturating counter** must guess wrong *twice* before it flips its prediction, so in a loop it mispredicts only on the final (exit) iteration — about **once per loop**. A 1-bit predictor flips after a single miss, so it mispredicts twice per loop (once on entry, once on exit). Hence the 2-bit scheme is more accurate.

**Q82. (A)** Use CPI = 1 + (branch frequency × branch penalty). Here that is 1 + (0.20 × 3) = 1 + 0.6 = **1.6**. The extra 0.6 is a 60% slowdown caused by branches alone when there is no prediction.

**Q83. (A)** Now only the *mispredicted* branches pay the penalty. Misprediction rate = 1 − 0.90 = 0.10. CPI = 1 + (branch frequency × misprediction rate × penalty) = 1 + (0.20 × 0.10 × 3) = 1 + 0.06 = **1.06**. Dropping from 1.6 to 1.06 shows why branch predictors are worth so much hardware.

**Q84. (B)** Register renaming gives an instruction a fresh physical register, which cures the *name* conflicts — **WAR and WAW**. It cannot cure RAW, which is a real data dependency, nor structural hazards, which are about hardware resources. So the answer is WAR and WAW only.

**Q85. (A)** Caches only help because real programs don't touch memory randomly — they show **locality of reference**: they reuse recent data (temporal) and touch nearby data (spatial). Keeping that "likely-to-be-used" data in a small fast cache pays off precisely because of this predictability. Recursion, virtualisation and pipelining are unrelated to *why* caching works.

**Q86. (B)** **Temporal** locality = "if you used it, you'll probably use it again soon." A loop counter or the loop body's instructions are accessed over and over across iterations, so keeping them cached avoids repeated slow memory trips. Option A describes spatial locality.

**Q87. (B)** **Spatial** locality = "if you used one location, you'll probably use its neighbours soon." Walking through `A[0], A[1], A[2] …` or executing instructions in sequence are typical examples. This is why fetching a whole block of nearby bytes into the cache is worthwhile. Option A is temporal locality.

**Q88. (B)** Caches fetch an entire block (say 64 bytes) rather than a single word to exploit **spatial locality**: bringing in `A[0]` also brings its neighbours `A[1]…A[15]`, which the program is likely to need next — for free. Temporal locality justifies *keeping* data, but fetching *neighbours* is the spatial idea.

**Q89. (B)** As you descend the hierarchy (registers → caches → RAM → SSD → disk), capacity **increases**, cost per bit **decreases**, and access time **increases** (gets slower). Option B states this correctly; A, C and D each get the direction of a trend backwards.

**Q90. (B)** SRAM ("static" RAM) stores each bit in a little **flip-flop built from about six transistors**, which holds its value on its own as long as power is applied — so it needs no refresh and is fast, but takes lots of area. DRAM, by contrast, uses a leaky capacitor. SRAM's flip-flop cell is why it is used for cache.

**Q91. (B)** DRAM stores each bit as a tiny charge on a **capacitor**, and that charge **leaks away** within milliseconds. So every cell must be periodically read and rewritten ("refreshed") to keep its data — that refresh requirement is exactly what "dynamic" refers to. SRAM's flip-flops don't leak, so they need no refresh.

**Q92. (B)** Cache needs to be fast, so it is built from **SRAM**; main memory needs to be large and cheap, so it is built from **DRAM**. This matches the speed-vs-density trade-off between the two technologies. Option A reverses them.

**Q93. (B)** Both SRAM and DRAM are **volatile** — cut the power and both lose their contents. "Dynamic" in DRAM refers only to its need for refresh, not to any non-volatility. Neither retains data without power, unlike flash or disk.

**Q94. (B)** DRAM packs more bits per unit area because each cell is just **one transistor plus one capacitor** — far smaller than SRAM's ~six-transistor flip-flop. This higher density (and lower cost per bit) is why main memory uses DRAM. Options A and D describe SRAM.

**Q95. (A)** Split the 32-bit address into offset, index, tag. Offset = log₂(block size) = log₂32 = **5** bits. Number of lines = cache size ÷ block size = 8 KB ÷ 32 B = 8192/32 = 256 lines, so index = log₂256 = **8** bits. Tag = 32 − 8 − 5 = **19** bits. Check: 19 + 8 + 5 = 32 ✓.

**Q96. (B)** In a **direct-mapped** cache each memory block has exactly **one** allowed line, chosen by (block number mod number of lines). It is the simplest and fastest to look up (one comparator), but two hot blocks mapping to the same line evict each other repeatedly (conflict misses). "Any line" is fully associative; "any of k lines in a set" is set-associative.

**Q97. (B)** In a **fully associative** cache a block may be placed in **any** line, so there are no forced collisions and hence no conflict misses. The price is that finding a block requires comparing its tag against every line at once (one comparator per line), which is only practical for small caches like the TLB.

**Q98. (B)** In a **k-way set-associative** cache a block first maps to exactly one **set** (like direct-mapped), but *within* that set it may occupy **any of the k lines** (like fully associative). This compromise cuts conflict misses versus direct-mapped while staying cheaper than fully associative. It is not "one line" (that's direct) nor "any line anywhere" (that's fully associative).

**Q99. (B)** Sets group lines together, k lines per set, so the **number of sets = number of lines ÷ associativity (k)**. For example, 128 lines that are 2-way associative give 128/2 = 64 sets. The index field then selects among these sets.

**Q100. (C)** The offset field identifies a byte within a block, so its width = log₂(block size in bytes) = log₂64 = **6** bits. (2⁶ = 64 bytes.) Block size drives the offset only — not the number of sets.

**Q101. (B)** Number of sets = lines ÷ associativity = 128 ÷ 2 = **64**. Note the 64-byte block size is a *deliberate distractor* here: block size affects the offset field, **not** the set count, which depends only on lines and associativity.

**Q102. (B)** The index selects which set, so index bits = log₂(number of sets). From Q101 there are 64 sets, so index = log₂64 = **6** bits.

**Q103. (A)** Lines = 64 KB ÷ 32 B = 65536/32 = 2048. Sets = lines ÷ associativity = 2048 ÷ 4 = 512, so index = log₂512 = **9** bits. Offset = log₂32 = **5** bits. Tag = 32 − 9 − 5 = **18** bits. Check: 18 + 9 + 5 = 32 ✓.

**Q104. (A)** Offset = log₂(16-byte block) = **4** bits. Lines = 16 KB ÷ 16 B = 16384/16 = 1024, so index = log₂1024 = **10** bits (direct-mapped, so lines = sets). Tag = 32 − 10 − 4 = **18** bits. Check: 18 + 10 + 4 = 32 ✓.

**Q105. (A)** A fully associative cache has **no index field** (a block can go anywhere), so the address splits only into tag + offset. Offset = log₂(32-byte block) = 5 bits. Tag = 32 − 5 = **27** bits. Check: 27 + 5 = 32 ✓.

**Q106. (B)** Lines = 1 MB ÷ 64 B = 1,048,576/64 = 16,384. Sets = lines ÷ associativity = 16,384 ÷ 4 = 4,096. Index = log₂4096 = **12** bits.

**Q107. (C)** Continue from Q106. Offset = log₂(64-byte block) = 6 bits; index = 12 bits. Tag = total − index − offset = 40 − 12 − 6 = **22** bits.

**Q108. (B)** Keep cache size and associativity fixed. Doubling the block size halves the number of lines (lines = cache size ÷ block size), and since sets = lines ÷ associativity, the number of sets also **halves**. (Meanwhile the offset grows by one bit.) This is a favourite trap because people forget block size changes the line/set count when total size is held constant.

**Q109. (C)** A **fully associative** cache lets a block sit in any line, so blocks never collide over a fixed slot — it has **no conflict misses** by definition. Direct-mapped and low-associativity caches all can suffer conflict misses. (Only compulsory and capacity misses remain in a fully associative cache.)

**Q110. (B)** Offset = log₂(64-byte block) = 6 bits. Lines = 32 KB ÷ 64 B = 32768/64 = 512 (direct-mapped, so sets = lines). Index = log₂512 = **9** bits. (Tag would be 32 − 9 − 6 = 17, but the question asks only for index.)

**Q111. (B)** The wording "fetched from memory *after* the cache lookup fails" signals the **hierarchical** model: AMAT = T_cache + (miss rate) × T_memory. Miss rate = 1 − 0.9 = 0.1, so AMAT = 10 + 0.1 × 100 = 10 + 10 = **20 ns**. (If accessed in parallel it would be 19 ns — always read the wording.)

**Q112. (A)** "Simultaneously" signals the **parallel** model: AMAT = h × T_cache + (1 − h) × T_memory = 0.9 × 10 + 0.1 × 100 = 9 + 10 = **19 ns**. The difference from Q111 is that on a hit you don't add the full memory time, and here the hit term is weighted by h rather than paid in full.

**Q113. (B)** In the hierarchical/sequential model you always spend the cache time first, and *only on a miss* do you additionally pay the memory time: **AMAT = T_c + (1 − h)·T_m**. The cache term is unconditional because you always look in the cache first.

**Q114. (A)** In the simultaneous/parallel model both lookups start together, so the access time is a straight weighted average: **AMAT = h·T_c + (1 − h)·T_m** — hit fraction pays cache time, miss fraction pays memory time. Notice the cache term here is multiplied by h, unlike the hierarchical formula.

**Q115. (B)** Hierarchical: AMAT = T_c + (1 − h)·T_m = 1 + (1 − 0.95) × 100 = 1 + 0.05 × 100 = 1 + 5 = **6 ns**.

**Q116. (A)** Work outward using AMAT = T_L1 + m_L1 × (T_L2 + m_L2 × T_mem). Inner part: T_L2 + m_L2 × T_mem = 10 + 0.20 × 100 = 10 + 20 = 30. Then AMAT = 1 + 0.05 × 30 = 1 + 1.5 = **2.5 ns**.

**Q117. (B)** Hierarchical: AMAT = T_c + (1 − h)·T_m = 20 + (1 − 0.8) × 200 = 20 + 0.2 × 200 = 20 + 40 = **60 ns**.

**Q118. (A)** "Simultaneously" ⇒ parallel model: AMAT = h·T_c + (1 − h)·T_m = 0.85 × 5 + 0.15 × 70 = 4.25 + 10.5 = **14.75 ns**.

**Q119. (B)** In **write-back**, a write updates only the cached copy; main memory is refreshed **only when that block is later evicted** from the cache. This slashes memory traffic (a variable written a million times in a loop hits memory just once on eviction), at the cost of memory being temporarily stale. Option A ("every write") describes write-through.

**Q120. (B)** Write-back needs a **dirty bit** per line to record whether the line has been modified since it was loaded. On eviction, if the dirty bit is set the block must be written back to memory; if it is clean it can simply be discarded. Without the dirty bit the cache couldn't tell which blocks need saving.

**Q121. (B)** In **write-through** every write goes to both the cache and main memory immediately, so memory is always consistent with the cache. This is simple and multiprocessor-friendly but generates more memory traffic. Updating "only on eviction" is write-back.

**Q122. (B)** The dirty bit is **set the moment the line is written/modified**, marking that the cached copy now differs from memory. It is then checked at eviction time to decide whether a write-back is needed. Merely loading or reading a line does not set it.

**Q123. (B)** With **write-allocate**, a write that misses first **brings the whole block into the cache**, then performs the write there (so subsequent writes/reads to the block hit). It is usually paired with write-back. The alternative, no-write-allocate, writes straight to memory and skips the cache.

**Q124. (B)** **LRU (Least Recently Used)** evicts the block unused for the longest time, which exploits temporal locality and gives the best practical hit rates. True LRU is expensive to implement exactly, so real caches approximate it. FIFO/Random are cheaper but weaker, and MRU is rarely useful.

**Q125. (B)** **FIFO** (evict the oldest resident) can suffer **Belady's anomaly**: adding more cache frames can *increase* the number of misses — a counter-intuitive quirk. Stack-based policies like LRU and OPT are provably immune to it.

**Q126. (B)** The **Optimal (OPT/MIN)** policy evicts the block that will be needed furthest in the future. That requires knowing the future, so it is **unimplementable in practice** and used only as a theoretical benchmark to judge how close real policies get. It is not cheap hardware, nor the same as FIFO or random.

**Q127. (C)** A direct-mapped cache gives each block exactly one legal line, so on a miss there is **no choice** about what to evict — the incoming block simply overwrites whatever is in that one line. Hence **no replacement policy is needed**. Replacement policies matter only when a set has multiple lines (associative caches).

**Q128. (B)** The three Cs are **Compulsory** (first-ever access to a block, unavoidable), **Capacity** (working set bigger than the cache), and **Conflict** (too many blocks map to the same set). It's a handy framework for diagnosing *why* misses happen. "Coherence" is a fourth C only in multiprocessor discussions, not the classic three.

**Q129. (C)** Compulsory (cold-start) misses are the first reference to a block and can't be avoided outright, but they are reduced by **larger blocks (which bring in more data per miss) and prefetching** (fetching data before it's needed). A larger cache helps capacity misses, and associativity helps conflict misses.

**Q130. (A)** Capacity misses happen when the program's working set is simply **bigger than the cache**, so the direct cure is a **larger cache**. Associativity targets conflict misses, and block size targets compulsory misses — neither addresses raw capacity.

**Q131. (B)** Conflict misses occur when too many blocks compete for the same set, so the cure is **higher associativity** (more lines per set, so competing blocks can coexist). At the extreme, a fully associative cache eliminates conflict misses entirely. Block size and write policy don't address conflicts.

**Q132. (B)** Memory interleaving spreads consecutive addresses across several separate memory **banks**, so accesses to nearby addresses can proceed in **overlap** rather than one after another — raising effective memory **bandwidth**. That is exactly what filling a cache block (several consecutive words) needs. It doesn't add capacity or reduce address lines.

**Q133. (A)** In low-order interleaving the bank is chosen by (address mod number of banks). With 4 banks, address 4 → 4 mod 4 = 0, so it lands in **bank 0**. (Addresses 0 and 4 share bank 0, 1 and 5 share bank 1, and so on.)

**Q134. (B)** Chips = (capacity ratio) × (width ratio). Capacity ratio = 16K ÷ 4K = 4 (rows needed to reach the depth). Width ratio = 8 ÷ 4 = 2 (chips side-by-side to reach the word width). Total = 4 × 2 = **8 chips**, arranged as 4 rows of 2.

**Q135. (B)** Address lines = log₂(number of locations). Here there are 16K = 16,384 = 2¹⁴ locations, so **14 address lines** are needed (and 8 data lines for the 8-bit word). Distractor 13 would only address 8K.

**Q136. (C)** Capacity ratio = 1M ÷ 256K = 4. Width ratio = 8 ÷ 1 = 8. Chips = 4 × 8 = **32**. (The ×1 chips are only one bit wide, so it takes 8 of them side-by-side just to make one 8-bit word.)

**Q137. (C)** Capacity ratio = 64K ÷ 16K = 4. Width ratio = 16 ÷ 8 = 2. Chips = 4 × 2 = **8**, arranged as 4 rows of 2.

**Q138. (C)** Address lines = log₂(number of locations) = log₂(2²⁰) = **20**. A million locations (2²⁰) needs 20 address bits to name them all uniquely.

**Q139. (B)** Bank = address mod number of banks = 5 mod 4 = 1, so address 5 lies in **bank 1**. (In 4-way interleaving, banks repeat every 4 addresses: 4→bank 0, 5→bank 1, 6→bank 2, 7→bank 3.)

**Q140. (B)** First find one rotation's time: 6000 RPM = 6000/60 = 100 rotations per second, so one rotation = 1/100 s = 10 ms. On average the desired sector is **half a rotation** away, so average rotational latency = 10/2 = **5 ms**. (Equivalently 30/RPM s = 30/6000 = 0.005 s.)

**Q141. (A)** Total disk access time = **seek time** (move the arm to the right track) + **rotational latency** (wait for the sector to spin under the head) + **transfer time** (read the bits as they pass), plus optional controller overhead. Leaving out any of the three main terms (as in B, C, D) is incorrect.

**Q142. (B)** One full rotation takes 60/RPM seconds; on average you wait for half a rotation, so average rotational latency = ½ × (60/RPM) = **30/RPM seconds**. This is the handy shortcut formula for these problems.

**Q143. (B)** Average rotational latency = 30/RPM = 30/7200 = 0.004167 s ≈ **4.17 ms**. (8.33 ms would be a *full* rotation, the classic trap — remember it's *half* a rotation on average.)

**Q144. (B)** Average rotational latency = 30/RPM = 30/15000 = 0.002 s = **2 ms**. Faster spin (higher RPM) means shorter latency.

**Q145. (B)** Disk performance is dominated by the two **mechanical** delays — **seek time and rotational latency** — which are typically milliseconds. Transfer time (actually reading the bits) is usually tiny by comparison. This is exactly why sequential access is far faster than random access and why disk-scheduling algorithms focus on reducing seeks.

**Q146. (B)** Total capacity = **surfaces × tracks per surface × sectors per track × bytes per sector**. Multiply the counts at each level of the disk geometry to get total bytes. The other options omit one or more of these factors.

**Q147. (B)** A **cylinder** is the set of tracks with the *same track number across all platters/surfaces* — the tracks that lie directly above/below one another. Because the head assembly reaches all of them without moving the arm, a cylinder is a convenient unit for allocating related data (no extra seeks). It is not a single sector, platter, or head.

**Q148. (B)** 3000 RPM = 3000/60 = 50 rotations per second, so one rotation = 1/50 s = 20 ms. Average rotational latency = half a rotation = 20/2 = **10 ms**. (Equivalently 30/3000 = 0.010 s.)

**Q149. (B)** With interrupt-driven I/O the CPU must handle every single word of a transfer. **DMA** hands the whole block to a dedicated controller that moves data directly between the device and memory, so the **CPU is bypassed per word** and interrupted only once at the end — far less CPU overhead. DMA still needs controller hardware and memory, ruling out A and D.

**Q150. (B)** **Cycle stealing** is the DMA mode where the controller grabs the bus for just **one bus cycle at a time** and releases it in between, letting the CPU keep running (a little more slowly). Burst mode instead holds the bus for the whole block; transparent mode uses only idle bus cycles.

**Q151. (B)** In programmed I/O the CPU sits in a loop repeatedly polling the device's status register ("ready yet?"), so it **busy-waits and wastes cycles** doing no useful work — terrible for slow devices. It needs no DMA controller and causes no interrupts; those aren't its drawback.

**Q152. (B)** Interrupt-driven I/O frees the CPU while waiting, but the CPU **still handles every single word** when the device is ready, which for a large block means **thousands of interrupts** and a lot of overhead. DMA avoids this by transferring the whole block itself and interrupting only once. The CPU does not busy-wait in interrupt-driven I/O (that's programmed I/O).

**Q153. (C)** **DMA** has the lowest CPU involvement: the CPU just sets up the transfer, then the DMA controller moves the entire block and interrupts the CPU only at completion. Programmed I/O (busy-waiting) and interrupt-driven I/O (per-word handling) both demand far more CPU attention.

**Q154. (B)** In a DMA block transfer the CPU is interrupted exactly **once — at completion**, when the DMA controller's word count reaches zero. That single interrupt is the whole point: contrast interrupt-driven I/O, which interrupts once per word.

**Q155. (B)** In **burst (block) mode** the DMA controller seizes the bus and **holds it for the entire block**, transferring all words back-to-back. This gives the fastest transfer, but the **CPU is stalled** the whole time because it can't use the bus. (Taking one cycle at a time is cycle stealing; using idle cycles is transparent mode.)

**Q156. (B)** In **transparent (hidden) mode** the DMA controller transfers **only during cycles when the CPU doesn't need the bus**, so the CPU never slows down at all. The trade-off is the slowest transfer, since the DMA must wait for idle moments. It is neither bus-hogging (burst) nor forced cycle-by-cycle stealing.

**Q157. (B)** A **non-maskable interrupt (NMI)** **cannot be disabled/masked by software**; it is reserved for catastrophic events like power failure or a memory parity error that must be handled no matter what the CPU is doing. Maskable interrupts, by contrast, can be temporarily switched off. An NMI is high, not low, priority.

**Q158. (B)** In **daisy chaining**, devices are wired in a chain and the interrupt-acknowledge signal passes from one to the next starting at the CPU. The device **nearest the CPU sees the acknowledge first**, so it has the **highest priority**; devices further down the chain rank lower. So proximity to the CPU determines priority.

**Q159. (B)** In a **vectored** interrupt the interrupting device itself **supplies the address (vector) of its ISR**, so the CPU can jump straight to the correct handler — fast. In a non-vectored scheme the ISR address is fixed and the CPU must poll devices to find who interrupted — slower.

**Q160. (B)** **Memory-mapped I/O** puts device registers at **ordinary memory addresses**, so any normal load/store instruction can read or write a device — no special I/O instructions needed. The cost is that some of the address space is consumed by devices. (A separate I/O space with IN/OUT is isolated I/O.)

**Q161. (B)** **Isolated (port-mapped) I/O** places devices in a **separate I/O address space**, distinct from memory, so it needs **special IN/OUT instructions** and an extra control line to say "this access is I/O, not memory." The benefit is that no memory address space is lost. It is the opposite of memory-mapped I/O.

**Q162. (B)** When the CPU accepts an interrupt it must be able to resume the interrupted program exactly, so it first **saves its context — the PC and the PSW (status/flags)** — typically onto the stack. After the ISR runs, this context is restored. Saving only the PC (A) or nothing (D) would lose the flags and corrupt the resumed program.

**Q163. (B)** Interrupts are honoured **between instructions — after the current instruction finishes** — so the machine is left in a clean, well-defined state that can be safely saved and later resumed. Interrupting mid-instruction would leave partial results and make resumption unreliable.

**Q164. (B)** "Cycle stealing" steals **memory/bus cycles, not CPU (execution) cycles.** The DMA controller borrows the bus for a memory cycle, but the CPU **keeps executing** whenever it is doing register-only work that doesn't need the bus — it only pauses when it actually needs the bus that DMA is using. This wording distinction is exactly what the term tests.

**Q165. (B)** A **software interrupt (trap)** is deliberately triggered by an instruction, and this is precisely how **system calls** work: a user program executes a trap to switch into the operating system to request a service. Power failure is an NMI, divide-by-zero is an exception, and DMA uses a hardware interrupt — none of those is a software trap.

**Q166. (B)** The correctly spelt word is **Occurrence** — it has a double *c*, a double *r*, and ends in *-ence*. The other spellings drop one of the doubled letters or use the wrong ending.

**Q167. (B)** "Neither of …" takes a **singular** verb, so it must be "Neither of the two candidates **has** submitted …," not "have submitted." The error is therefore in part **B**. This is a common subject–verb agreement trap because "candidates" (plural) sits nearby and tempts a plural verb.

**Q168. (A)** Unpack the clue: "my grandfather's only son" must be the speaker's own **father** (the grandfather has just one son). So the woman is "the daughter of my father" — i.e. the man's **sister**.

**Q169. (A)** Take cost price = 100. Marked 40% above cost → marked price = 140. A 25% discount gives selling price = 140 × (1 − 0.25) = 140 × 0.75 = 105. Profit = 105 − 100 = 5 on a cost of 100, i.e. **5%**.

**Q170. (A)** **Betlingchhip** (about 939 m), the highest point in Tripura, lies in the **Jampui Hills** in the north of the state along the Mizoram border. Atharamura, Baramura and Longtharai are Tripura's other main ranges but are lower.

**Q171. (B)** "Benevolent" means kind and well-meaning, so its opposite is **malevolent**, meaning wishing harm to others. Generous, kind and gracious are all *synonyms* of benevolent, not antonyms.

**Q172. (B)** A **polyglot** is a person who knows and can use many languages. A "linguist" studies language (and can loosely mean the same, but polyglot is the precise one-word term), an "orator" is a skilled public speaker, and "bilingual" means knowing only two languages.

**Q173. (A)** The code shifts each letter forward by **+1** (M→N, A→B, D→E, R→S, A→B, S→T, confirming the rule on MADRAS→NBESBT). Apply +1 to each letter of DELHI: D→E, E→F, L→M, H→I, I→J, giving **EFMIJ**.

**Q174. (B)** North then east make a right angle, so the start, the turning point and the end form a right triangle with legs 3 km and 4 km. The straight-line distance is the hypotenuse = √(3² + 4²) = √(9 + 16) = √25 = **5 km** (a 3-4-5 triangle).

**Q175. (B)** Look at the differences between terms: 6−2=4, 12−6=6, 20−12=8, 30−20=10 — increasing by 2 each time, so the next difference is 12 and the next term is 30 + 12 = **42**. (Equivalently the terms are n(n+1): 1·2, 2·3, 3·4, 4·5, 5·6, 6·7 = 42.)

**Q176. (B)** The relationship is "professional : place where they work." A doctor works in a **hospital**, so by analogy a teacher works in a **school**. "Student" is a person, "class"/"book" are not the workplace in the intended sense.

**Q177. (D)** Tripura became a **full-fledged state** of the Indian Union on 21 January **1972**, under the North-Eastern Areas (Reorganisation) Act. (Before that it was a Union Territory.)

**Q178. (A)** The capital of Tripura is **Agartala**. (Aizawl is the capital of Mizoram, Shillong of Meghalaya, and Imphal of Manipur.)

**Q179. (B)** **Dr. Rajendra Prasad** was the first President of India, serving from 1950 to 1962. (Nehru was the first Prime Minister, Radhakrishnan the second President, and Patel the first Deputy PM/Home Minister.)

**Q180. (B)** Add their one-day work rates: A does 1/10 per day and B does 1/15 per day, so together = 1/10 + 1/15 = 3/30 + 2/30 = 5/30 = 1/6 of the work per day. The whole job therefore takes **6 days**.
