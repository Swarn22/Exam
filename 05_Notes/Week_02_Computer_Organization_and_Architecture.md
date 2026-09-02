# Week 2 — Computer Organization & Architecture

**Syllabus §3:** Machine instructions and addressing modes. ALU, data path and control unit. Instruction pipelining, pipeline hazards. Memory hierarchy: cache, main memory and secondary storage. I/O interface (interrupt and DMA mode).
**Estimated marks: ~9**

---

## 1. Basic structure

### 1.1 Von Neumann vs Harvard

| | **Von Neumann** | **Harvard** |
|---|---|---|
| Memory | Single, shared for instructions and data | Separate instruction and data memories |
| Buses | One | Two |
| Bottleneck | ⭐ **Von Neumann bottleneck** (CPU–memory bandwidth) | Avoided |
| Used in | General-purpose CPUs | DSPs, microcontrollers, and internally in caches (split I/D cache) |

### 1.2 Key registers ⭐

| Register | Full name | Holds |
|---|---|---|
| **PC** | Program Counter | ⭐ Address of the **next** instruction |
| **IR** | Instruction Register | The instruction currently being executed |
| **MAR** | Memory Address Register | Address being accessed |
| **MDR / MBR** | Memory Data/Buffer Register | Data being read/written |
| **AC** | Accumulator | Operand/result in accumulator machines |
| **SP** | Stack Pointer | Top of stack |
| **PSW / Flags** | Program Status Word | Zero, carry, sign, overflow flags |

⚠ **PC holds the address; IR holds the instruction.** Frequently swapped in options.

### 1.3 Instruction cycle
**Fetch → Decode → Execute** (extended: Fetch → Decode → Operand fetch → Execute → Write-back)

Fetch micro-operations: `MAR ← PC` · `MDR ← M[MAR]` · `PC ← PC + 1` · `IR ← MDR`

---

## 2. Machine instructions

### 2.1 Instruction formats by address count ⭐

| Format | Example | Machine type |
|---|---|---|
| **Zero-address** | `ADD` | ⭐ **Stack** machine (operands implicit on stack) |
| **One-address** | `ADD B` | **Accumulator** machine |
| **Two-address** | `ADD A, B` | A ← A + B |
| **Three-address** | `ADD A, B, C` | A ← B + C; general-register machine |

🔢 Evaluating `(A+B)*(C+D)` on a stack machine uses postfix `AB+CD+*` — push/pop plus zero-address operators.

**Instruction length considerations:** opcode bits vs operand bits. With n bits of opcode you get 2ⁿ instructions. **Expanding opcode** technique reclaims unused encodings for instructions with fewer operands.

### 2.2 ⭐ Addressing modes

| Mode | Effective Address (EA) | Typical use |
|---|---|---|
| **Immediate** | Operand *is* in the instruction | Constants |
| **Direct / Absolute** | EA = address field | Global variables |
| **Indirect** | EA = M[address field] | ⭐ **Pointers** |
| **Register direct** | Operand in register | Fastest |
| **Register indirect** | EA = contents of register | Pointer in register |
| ⭐ **Indexed** | EA = base address + index register | ⭐ **Arrays** |
| ⭐ **Base + displacement** | EA = base register + constant offset | ⭐ Stack frames, records/structs |
| **Relative (PC-relative)** | EA = PC + offset | ⭐ **Branches**, position-independent code |
| **Auto-increment / decrement** | EA = register; register then ±1 | Array traversal, stack |
| **Implied / Implicit** | Operand implicit in opcode | `CLC`, stack ops |

⚠ **Indirect addressing needs an extra memory reference** (slowest); register direct needs none (fastest).
⭐ Number of memory accesses to fetch an operand: immediate 0 · direct 1 · indirect 2 · register direct 0 · register indirect 1.

🔢 If R1 = 1000, offset = 20, and the instruction is `LOAD R2, 20(R1)` → EA = 1000 + 20 = **1020**.

### 2.3 ⭐ RISC vs CISC

| | **RISC** | **CISC** |
|---|---|---|
| Instruction set | Small, simple | Large, complex |
| Instruction length | **Fixed** | **Variable** |
| Addressing modes | Few | Many |
| Memory access | ⭐ **Only LOAD/STORE** | Most instructions can access memory |
| Registers | **Many** GPRs | Fewer |
| Cycles per instruction | Mostly **1** (pipelined) | Varies, many |
| Control unit | **Hardwired** | Usually **microprogrammed** |
| Complexity in | Compiler | Hardware |
| Examples | ARM, MIPS, RISC-V, SPARC | x86, VAX, IBM 360 |

---

## 3. ALU, data path and control unit

**ALU:** performs arithmetic (add, subtract, increment) and logic (AND, OR, XOR, NOT, shift) operations; sets condition flags.

**Data path:** registers + ALU + buses + multiplexers — the components data flows through.

**Control unit:** generates the control signals that drive the data path.

### 3.1 ⭐ Hardwired vs microprogrammed control

| | **Hardwired** | **Microprogrammed** |
|---|---|---|
| Implementation | Fixed combinational/sequential logic | Microinstructions in **control memory** |
| Speed | ⭐ **Faster** | ⭐ **Slower** (extra control-memory lookup) |
| Flexibility / modifiability | Difficult (redesign hardware) | ⭐ **Easy** (rewrite microcode) |
| Cost of design | High for complex ISAs | Lower for complex ISAs |
| Suits | **RISC** | **CISC** |

**Microinstruction formats:**
- **Horizontal:** one bit per control signal → wide words, **more parallelism**, faster, less encoding.
- **Vertical:** encoded fields → narrow words, needs a decoder, **less parallelism**, more compact.

**Control memory** holds the microprogram; the **Control Address Register (CAR)** points to the next microinstruction.

---

## 4. ⭐ Pipelining

### 4.1 Concept
Overlap the execution of multiple instructions by splitting into stages. Classic 5-stage RISC pipeline:
**IF** (instruction fetch) → **ID** (decode/register read) → **EX** (execute/ALU) → **MEM** (memory access) → **WB** (write back)

### 4.2 📌 Formulas

For **k** stages and **n** instructions, 1 cycle per stage:

| Quantity | Formula |
|---|---|
| ⭐ **Cycles (pipelined)** | **k + (n − 1)** |
| Cycles (non-pipelined) | n × k |
| ⭐ **Speedup** | **S = nk / (k + n − 1)** |
| ⭐ **Maximum speedup** (n → ∞) | **k** |
| Efficiency | η = S / k |
| Throughput | n / (total time) |

**Clock period** of a pipeline = max(stage delay) + latch/register overhead.

🔢 5-stage pipeline, 1000 instructions, no stalls → cycles = 5 + 999 = **1004**.
🔢 Speedup = (1000 × 5)/1004 ≈ **4.98** (approaching the ideal 5).

🔢 **Non-uniform stages:** stage delays 10, 8, 12, 9 ns with 1 ns latch overhead → clock period = 12 + 1 = **13 ns** (the slowest stage governs). This is why designers split slow stages.

### 4.3 ⭐ Pipeline hazards

**(a) Structural hazards** — two instructions need the same hardware resource in the same cycle.
*Fix:* duplicate resources (separate instruction and data caches/memory ports), or stall.

**(b) Data hazards** — an instruction needs a result not yet available.

| Type | Name | Removable by renaming? |
|---|---|---|
| ⭐ **RAW** (Read After Write) | **True data dependency** | ❌ No — a genuine dependency |
| **WAR** (Write After Read) | Anti-dependency | ✅ Yes |
| **WAW** (Write After Write) | Output dependency | ✅ Yes |

*Fixes:* ⭐ **operand forwarding / bypassing** (route the ALU result directly to the next instruction's input), stalls/bubbles, compiler instruction reordering, register renaming.
⚠ Forwarding removes most RAW stalls but **cannot fully remove the load-use hazard** — a load's data is only available after MEM, so one stall cycle remains.

**(c) Control (branch) hazards** — the next instruction address is unknown until the branch resolves.
*Fixes:* stall/flush, **branch prediction** (static: always-taken/not-taken; dynamic: 1-bit, 2-bit saturating counters, branch target buffer), **delayed branch** (delay slot filled by the compiler), early branch resolution.

📌 With branch penalty **p** and branch frequency **f**: average CPI = 1 + f × p.

🔢 If 20% of instructions are branches with a 3-cycle penalty and no prediction: CPI = 1 + 0.2 × 3 = **1.6**.

---

## 5. ⭐ Memory hierarchy

### 5.1 The hierarchy

| Level | Typical access time | Size | Cost/bit |
|---|---|---|---|
| Registers | < 1 ns | bytes | Highest |
| Cache L1 / L2 / L3 | 1–20 ns | KB–MB | |
| Main memory (DRAM) | 50–100 ns | GB | |
| SSD | ~100 μs | GB–TB | |
| Magnetic disk | ~10 ms | TB | |
| Tape | seconds | TB+ | Lowest |

As you go **down**: capacity ↑, cost/bit ↓, access time ↑.

⭐ **Locality of reference** is what makes the hierarchy work:
- **Temporal locality:** a recently accessed item is likely to be accessed again (loops, variables).
- **Spatial locality:** items near a recently accessed address are likely to be accessed (arrays, sequential code).

### 5.2 SRAM vs DRAM ⭐

| | **SRAM** | **DRAM** |
|---|---|---|
| Storage element | Flip-flop (6 transistors) | Capacitor + 1 transistor |
| Refresh needed | ❌ No | ⭐ **Yes** (periodically) |
| Speed | Faster | Slower |
| Density | Lower | Higher |
| Cost | Higher | Lower |
| Used for | **Cache** | **Main memory** |

### 5.3 ⭐⭐ Cache mapping

Physical address is split into fields. Let block size = 2^b bytes, number of lines = 2^l, address = m bits.

| Mapping | Address fields | Blocks per set | Comparators |
|---|---|---|---|
| **Direct mapped** | Tag \| **Line/Index** \| Offset | 1 | 1 |
| **Fully associative** | Tag \| Offset (no index) | all | one per line |
| **k-way set associative** | Tag \| **Set** \| Offset | k | k |

📌 **Offset bits = log₂(block size)**
📌 **Index bits = log₂(number of lines)** (direct mapped) or **log₂(number of sets)** (set associative)
📌 **Number of sets = number of lines / associativity**
📌 **Tag bits = address bits − index bits − offset bits**

🔢 **Direct-mapped, 8 KB cache, 32-byte blocks, 32-bit address.**
Offset = log₂32 = **5**. Lines = 8192/32 = 256 → index = log₂256 = **8**. Tag = 32 − 8 − 5 = **19**.

🔢 **2-way set associative, 128 lines, 64-byte blocks.**
Sets = 128/2 = **64** → set bits = 6; offset = log₂64 = **6**.

⚠ Block size affects the **offset**, not the number of sets. A question giving block size when asking only for the set count is testing whether you know that.

### 5.4 ⭐ Average Memory Access Time (AMAT)

Two conventions exist — **read the question wording carefully**:

📌 **Hierarchical / sequential** (check cache first, then memory on miss):
**AMAT = T_cache + (1 − h) × T_memory**

📌 **Simultaneous / parallel** (both started together):
**AMAT = h × T_cache + (1 − h) × T_memory**

🔢 T_cache = 10 ns, T_mem = 100 ns, h = 0.9:
- Hierarchical → 10 + 0.1 × 100 = **20 ns**
- Simultaneous → 0.9×10 + 0.1×100 = **19 ns**

📌 Multi-level: AMAT = T_L1 + m_L1 × (T_L2 + m_L2 × T_mem)

**Hit ratio h = hits / total accesses.** Miss ratio = 1 − h.

### 5.5 Cache write policies ⭐

| Policy | Memory updated | Pros | Cons |
|---|---|---|---|
| **Write-through** | On **every** write | Memory always consistent; simple | More memory traffic |
| ⭐ **Write-back** | ⭐ **Only on eviction** of a dirty block | Far fewer memory writes | Memory temporarily stale; needs a **dirty bit** |

**On a write miss:** *write-allocate* (fetch the block first, usual with write-back) vs *no-write-allocate / write-around* (write straight to memory, usual with write-through).

### 5.6 Replacement policies

| Policy | Note |
|---|---|
| **LRU** (Least Recently Used) | Best practical performance; costly to implement exactly |
| **FIFO** | Simple; can suffer Belady's anomaly |
| **LFU** (Least Frequently Used) | Counter-based |
| **Random** | Cheapest hardware |
| **Optimal (OPT/MIN)** | Theoretical benchmark only — needs future knowledge |

⚠ In a **direct-mapped** cache there is no replacement policy — there is only one possible location.

### 5.7 The three Cs (types of cache miss)

| Miss | Cause | Reduced by |
|---|---|---|
| **Compulsory** (cold) | First-ever reference to a block | Larger block size, prefetching |
| **Capacity** | Cache too small to hold the working set | Larger cache |
| **Conflict** | Several blocks map to the same set | Higher associativity |

### 5.8 Main memory organisation

- **Memory interleaving:** consecutive addresses are spread across separate modules (banks) so accesses overlap → higher bandwidth. *Low-order interleaving* puts consecutive words in different banks.
- **Memory chip sizing:** 🔢 to build 16K × 8 memory from 4K × 4 chips → need (16K/4K) × (8/4) = 4 × 2 = **8 chips**, arranged in 4 rows × 2 columns.
- **Address lines** for N locations = log₂N; **data lines** = word width.

### 5.9 Secondary storage — magnetic disk ⭐

**Geometry:** platters → tracks (concentric rings) → sectors. The same track across all platters forms a **cylinder**.

📌 **Disk access time = Seek time + Rotational latency + Transfer time** (+ controller overhead)

📌 ⭐ **Average rotational latency = ½ × (time for one rotation) = 30/RPM seconds**

🔢 6000 RPM → 100 rotations/s → one rotation = 10 ms → **average rotational latency = 5 ms**.

📌 **Transfer time = (bytes to transfer / bytes per track) × rotation time**

🔢 Disk capacity = surfaces × tracks/surface × sectors/track × bytes/sector.

---

## 6. ⭐ I/O organisation

### 6.1 Three I/O techniques

| Technique | How | CPU involvement | Speed |
|---|---|---|---|
| **Programmed I/O** (polling) | CPU repeatedly checks the status flag | ⭐ **Highest** — CPU busy-waits | Slowest |
| **Interrupt-driven I/O** | Device interrupts the CPU when ready | Moderate — CPU handles **each word** | Medium |
| ⭐ **DMA** | DMA controller transfers directly to/from memory | ⭐ **Lowest** — one interrupt per **block** | Fastest |

### 6.2 Interrupts

**Sequence:** device raises interrupt → CPU finishes the current instruction → saves PC and PSW → identifies the source → jumps via the **interrupt vector table** to the ISR → executes ISR → restores context → returns.

| Type | Meaning |
|---|---|
| **Maskable** | Can be disabled by software |
| **Non-maskable (NMI)** | Cannot be disabled (power failure, hardware error) |
| **Vectored** | Device supplies the ISR address |
| **Non-vectored** | Fixed ISR address; CPU must poll to identify the device |
| **Software interrupt / trap** | Generated by an instruction (system calls) |

**Daisy chaining** is a hardware priority scheme: the device closest to the CPU has the highest priority.

### 6.3 ⭐ DMA (Direct Memory Access)

The DMA controller takes over the bus and moves data between an I/O device and memory without CPU involvement per word. The CPU programs the DMA with: source/destination address, word count, and direction.

| Mode | Behaviour |
|---|---|
| ⭐ **Cycle stealing** | DMA takes **one bus cycle at a time**, interleaving with CPU activity |
| ⭐ **Burst / block mode** | DMA holds the bus for the **whole block**; fastest transfer, but the CPU stalls |
| **Transparent mode** | DMA transfers only when the CPU is not using the bus; no CPU slowdown, slowest |

⚠ **Cycle stealing steals memory cycles, not CPU cycles** — the CPU keeps executing whenever it does not need the bus.

**I/O addressing:**
- **Memory-mapped I/O:** device registers occupy memory addresses; ordinary load/store instructions work; consumes address space.
- **Isolated / port-mapped I/O:** separate I/O address space with special `IN`/`OUT` instructions.

---

## 7. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| PC holds | Address of next instruction |
| Zero-address instructions | Stack machine |
| One-address instructions | Accumulator machine |
| Mode for pointers | Indirect |
| Mode for arrays | Indexed |
| Mode for branches | PC-relative |
| Memory refs for indirect operand fetch | 2 |
| RISC memory access | Load/store only |
| Microprogrammed control | Slower, more flexible |
| Horizontal microinstruction | Wider, more parallel |
| Pipeline cycles (k stages, n instr) | k + n − 1 |
| Max pipeline speedup | k |
| RAW | True dependency; not removable by renaming |
| Fix for data hazard | Operand forwarding |
| Offset bits | log₂(block size) |
| Sets | lines / associativity |
| AMAT (hierarchical) | T_c + (1−h)·T_m |
| Write-back updates memory | On eviction (dirty bit) |
| Direct-mapped replacement policy | None needed |
| DRAM needs | Refresh |
| Cache is made of | SRAM |
| Avg rotational latency | ½ rotation = 30/RPM s |
| Disk access time | Seek + rotational + transfer |
| Cycle stealing | One bus cycle at a time |
| Lowest CPU involvement I/O | DMA |
| NMI | Cannot be masked |

---

## 8. Common traps ⚠

1. **PC vs IR vs MAR vs MDR** — know exactly what each holds.
2. **AMAT convention** — hierarchical (T_c + miss×T_m) vs simultaneous (h·T_c + miss·T_m). The question must tell you; if it says "searched in cache first, then memory", it is hierarchical.
3. **Block size does not change the number of sets** — it changes the offset field.
4. **Speedup approaches k, it never exceeds k.**
5. **Cycles = k + n − 1**, not k + n or n×k.
6. **Cycle stealing ≠ burst mode.** Cycle stealing interleaves; burst holds the bus.
7. **Write-back needs a dirty bit; write-through does not.**
8. **Belady's anomaly is a FIFO property** — LRU and OPT are stack algorithms and immune.
9. **Rotational latency is half a rotation on average**, not a full one.
10. **Forwarding does not eliminate the load-use stall.**

---

## 9. Practice

- GATE: [`Paper2_S03_Computer_Organization_and_Architecture/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S03_Computer_Organization_and_Architecture/) — **251 questions**
- State-PSC level: [`Paper2_S03_.../`](../02_State_PSC_PYQs/Subject_wise/Paper2_S03_Computer_Organization_and_Architecture/) — **245 questions**
- Test: [`Week_02_Test.md`](../04_Mock_Tests/Week_02_Test.md)

**Priority order if short on time:** cache address splitting & AMAT → addressing modes → pipeline formulas & hazards → DMA/interrupts → disk access time → hardwired vs microprogrammed → RISC vs CISC.
