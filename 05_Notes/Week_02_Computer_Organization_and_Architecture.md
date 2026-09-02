# Week 2 — Computer Organization & Architecture

**Syllabus §3:** Machine instructions and addressing modes. ALU, data path and control unit. Instruction pipelining, pipeline hazards. Memory hierarchy: cache, main memory and secondary storage. I/O interface (interrupt and DMA mode).
**Estimated marks: ~9**

---

## 💡 What this whole subject is about

Week 1 gave you gates, adders and flip-flops. This week assembles them into a **computer**.

Two related terms, often confused:
- **Computer Architecture** — what the programmer sees: the instruction set, registers, addressing modes. *The specification.*
- **Computer Organization** — how it is actually built: pipelines, caches, buses, control unit. *The implementation.*

Two machines can share an architecture (both run x86 programs) but differ wildly in organization (a laptop chip vs a server chip).

The subject answers four questions, and this file follows them:
1. **What can the machine be told to do?** (instructions and addressing modes)
2. **What executes those instructions?** (ALU, datapath, control unit)
3. **How do we make it fast?** (pipelining, caches)
4. **How does it talk to the outside world?** (I/O, interrupts, DMA)

---

# 1. Basic structure

## 1.1 💡 The stored-program idea

Before 1945, computers were *rewired* to change what they did. Von Neumann's insight was that **instructions can be stored in memory exactly like data**. That single idea is why software exists.

The consequence is the classic five-part machine:

```
        ┌──────────────────────────────┐
        │            CPU               │
        │  ┌────────┐   ┌───────────┐  │        ┌──────────┐
Input ──┼─►│  ALU   │◄─►│ Registers │  │◄──────►│  Memory  │
        │  └────────┘   └───────────┘  │        └──────────┘
        │  ┌──────────────────────┐    │
        │  │    Control Unit      │    │
        │  └──────────────────────┘    │
        └──────────────┬───────────────┘
                       ▼
                    Output
```

## 1.2 ⭐ Von Neumann vs Harvard

### 💡 The idea

If instructions and data live in the **same** memory with **one** bus, the CPU cannot fetch an instruction and a data word simultaneously — it must take turns. That congestion is the ⭐ **von Neumann bottleneck**, and it is why memory speed, not CPU speed, limits most real programs.

The **Harvard architecture** fixes it with **separate memories and separate buses** for instructions and data.

| | **Von Neumann** | **Harvard** |
|---|---|---|
| Memory | One, shared | Separate instruction & data memories |
| Buses | One | Two |
| Can fetch instruction + data at once? | ❌ No | ✅ Yes |
| Bottleneck | ⭐ **Von Neumann bottleneck** | Avoided |
| Used in | General-purpose CPUs | DSPs, microcontrollers |

⭐ **In practice modern CPUs are hybrids:** von Neumann in main memory, but with **separate L1 instruction and L1 data caches** — a "modified Harvard" arrangement that gets both the flexibility and the parallel access.

## 1.3 ⭐ The registers

### 💡 The idea

Registers are the CPU's own tiny storage — a handful of words, right next to the ALU, accessible in a fraction of a nanosecond (versus ~100 ns for main memory). A few of them have fixed, special jobs.

| Register | Full name | ⭐ Holds |
|---|---|---|
| ⭐ **PC** | Program Counter | ⭐ **The ADDRESS of the NEXT instruction** |
| ⭐ **IR** | Instruction Register | ⭐ **The instruction currently being executed** |
| **MAR** | Memory Address Register | The address currently being accessed |
| **MDR / MBR** | Memory Data / Buffer Register | The data being read from or written to memory |
| **AC** | Accumulator | Implicit operand/result in accumulator machines |
| **SP** | Stack Pointer | Address of the top of the stack |
| **PSW / Flags** | Program Status Word | Zero, Carry, Sign, Overflow flags |

⚠ ⭐ **PC holds an ADDRESS; IR holds an INSTRUCTION.** Options swapping these appear constantly.

**Memory hook:** MAR ↔ **A**ddress, MDR ↔ **D**ata. PC **counts** through the program; IR holds the **instruction**.

## 1.4 The instruction cycle

### 💡 The idea

Every instruction goes through the same loop, forever:

📌 **FETCH → DECODE → EXECUTE**

(Expanded: Fetch → Decode → Operand fetch → Execute → Write back.)

**Fetch, as micro-operations:**
```
MAR ← PC          copy the next-instruction address into MAR
MDR ← M[MAR]      read that memory location
PC  ← PC + 1      point at the following instruction
IR  ← MDR         load the fetched instruction into IR
```

⚠ Note **PC is incremented during the fetch, before the instruction executes.** That is why a "jump" instruction works by *overwriting* the already-incremented PC, and why PC-relative addressing measures from the *next* instruction.

---

# 2. Machine instructions

## 2.1 ⭐ Instruction formats — counting addresses

### 💡 The idea

An instruction must say **what** to do (the opcode) and **to what** (the operands). Machines differ in how many operand addresses they write down, and this defines the machine's whole style.

Consider computing `X = (A + B) × (C + D)`.

**Three-address machine** (each instruction names all three locations):
```
ADD  T1, A, B      ; T1 ← A + B
ADD  T2, C, D      ; T2 ← C + D
MUL  X,  T1, T2    ; X  ← T1 × T2
```
Short programs, long instructions.

**Two-address machine** (destination doubles as a source):
```
MOV  T1, A         ; T1 ← A
ADD  T1, B         ; T1 ← T1 + B
MOV  T2, C
ADD  T2, D
MUL  T1, T2
MOV  X, T1
```

**One-address / accumulator machine** (one implicit register, the accumulator):
```
LOAD  A            ; AC ← A
ADD   B            ; AC ← AC + B
STORE T1
LOAD  C
ADD   D
MUL   T1
STORE X
```

⭐ **Zero-address / stack machine** (operands are implicitly on a stack):
```
PUSH A
PUSH B
ADD                ; pops two, pushes the sum — no addresses at all
PUSH C
PUSH D
ADD
MUL
POP  X
```
⭐ Notice that the sequence of pushes and operators is exactly **postfix (reverse Polish) notation**: `AB+CD+*`. That is the connection to Week 4's expression evaluation.

| Format | Example | ⭐ Machine type |
|---|---|---|
| ⭐ **Zero-address** | `ADD` | ⭐ **Stack machine** |
| ⭐ **One-address** | `ADD B` | ⭐ **Accumulator machine** |
| **Two-address** | `ADD A, B` | A ← A + B |
| **Three-address** | `ADD A, B, C` | General-register machine |

**Instruction length trade-off:** with an n-bit opcode you can encode 2ⁿ instructions. **Expanding opcode** reclaims unused patterns — instructions with fewer operands use the freed operand bits to extend the opcode, so you can have many 0-address instructions alongside a few 3-address ones.

## 2.2 ⭐⭐ Addressing modes

### 💡 The idea

"Where is the operand?" has many possible answers, and each answer is an **addressing mode**. They exist because different programming constructs need different access patterns — a constant, a global variable, a pointer, an array element, a local variable, a branch target.

📌 The **effective address (EA)** is the final memory address the instruction actually uses.

Let's build them up with a running example. Suppose register R1 = 1000, memory location 1000 contains 2000, and memory location 2000 contains 55.

| Mode | ⭐ Effective address | Operand value | Typical use |
|---|---|---|---|
| **Immediate** | — (operand is *in* the instruction) | e.g. `MOV R2, #5` → 5 | ⭐ **Constants** |
| **Direct / Absolute** | EA = the address field | `LOAD 1000` → 2000 | Global variables |
| ⭐ **Indirect** | EA = M[address field] | `LOAD (1000)` → 55 | ⭐ **Pointers** |
| **Register direct** | Operand is in the register | `MOV R2, R1` → 1000 | Fastest; temporaries |
| **Register indirect** | EA = contents of the register | `LOAD (R1)` → 2000 | Pointer held in a register |
| ⭐ **Indexed** | EA = base address + index register | `LOAD A(R1)` | ⭐ **Arrays** |
| ⭐ **Base + displacement** | EA = base register + constant offset | `LOAD 20(R1)` → M[1020] | ⭐ **Stack frames, struct fields** |
| **Relative (PC-relative)** | EA = PC + offset | `BRANCH +8` | ⭐ **Branches**, position-independent code |
| **Auto-increment/decrement** | EA = register; register then ±1 | `LOAD (R1)+` | Array traversal, stack push/pop |
| **Implied / Implicit** | Operand implicit in the opcode | `CLC` (clear carry), `PUSH` | Stack ops, flag ops |

### ⭐ Counting memory accesses — a favourite question

📌 How many **memory references** are needed just to fetch the operand?

| Mode | Memory accesses for the operand |
|---|---|
| Immediate | **0** (it came with the instruction) |
| Register direct | **0** |
| Direct | **1** |
| Register indirect | **1** |
| ⭐ **Indirect** | ⭐ **2** (read the pointer, then read the target) |

⚠ ⭐ **Indirect addressing is the slowest** because of that double access; **register direct is the fastest** because it touches no memory at all. This is exactly why RISC machines keep everything in registers.

🔢 **Worked example.** R1 = 1000, offset = 20, instruction `LOAD R2, 20(R1)` (base + displacement).
EA = 1000 + 20 = **1020**. R2 gets whatever is at memory address 1020.

🔢 **Array access.** `int A[100]`, base address 5000, 4 bytes per element. To read `A[i]` with i in R1:
EA = 5000 + 4×R1 → **indexed (often scaled-indexed)** addressing. This is why the mode exists.

🔢 **Struct/local variable.** A function's local variables sit at fixed offsets from the frame pointer. `LOAD R2, -8(FP)` → **base + displacement**. This is why the mode exists.

## 2.3 ⭐⭐ RISC vs CISC

### 💡 The idea

Two opposing design philosophies, and understanding *why* each exists makes the comparison table memorable.

**CISC (Complex Instruction Set Computer)** — the 1970s answer. Memory was scarce and expensive, and people wrote assembly by hand. So: make each instruction do a lot. A single VAX instruction could evaluate a polynomial. Programs were short in bytes, and the "semantic gap" between high-level languages and machine code was small.
*Cost:* instructions vary in length and take wildly different numbers of cycles, so the hardware is complex and hard to pipeline.

**RISC (Reduced Instruction Set Computer)** — the 1980s reaction. Studies found compilers used only a small fraction of CISC instructions anyway. So: make every instruction **simple, fixed-length, one cycle**, and let the **compiler** assemble complex operations from them.
*Benefit:* uniform instructions pipeline beautifully — which is the real payoff (see §4).

⭐ **The single most characteristic RISC rule: LOAD/STORE architecture.** Only two instructions touch memory (`LOAD` and `STORE`); every other instruction operates purely on registers. This keeps instruction timing uniform.

| | ⭐ **RISC** | ⭐ **CISC** |
|---|---|---|
| Instruction set | Small, simple | Large, complex |
| ⭐ **Instruction length** | ⭐ **Fixed** | ⭐ **Variable** |
| Addressing modes | Few | Many |
| ⭐ **Memory access** | ⭐ **Only LOAD/STORE** | Most instructions can access memory |
| Registers | ⭐ **Many** general-purpose | Fewer |
| Cycles per instruction | Mostly **1** (pipelined) | Varies widely |
| ⭐ **Control unit** | ⭐ **Hardwired** | ⭐ **Microprogrammed** |
| Complexity lives in | ⭐ **The compiler** | ⭐ **The hardware** |
| Code size | Larger | Smaller |
| Pipelining | ⭐ **Easy** | Hard |
| Examples | ARM, MIPS, RISC-V, SPARC, PowerPC | x86, VAX, IBM 360, 8086 |

⚠ Modern x86 chips are CISC on the outside but internally **translate instructions into RISC-like micro-operations** — so the debate is settled in practice, with RISC principles winning inside the chip.

---

# 3. ALU, datapath and control unit

## 💡 The idea

Three pieces work together:

- **ALU (Arithmetic Logic Unit)** — the calculator. Performs add, subtract, increment, AND, OR, XOR, NOT, shift. Sets the **condition flags** (Zero, Carry, Sign, Overflow) as a side effect. Built from Week 1's adders and gates.
- **Datapath** — the plumbing. Registers, buses, multiplexers and the ALU: everything data can flow *through*. It is entirely combinational plus registers, and it has no idea what it is doing.
- **Control unit** — the conductor. For each instruction, in each clock cycle, it asserts the right control signals: "open this MUX", "tell the ALU to subtract", "write the result into R3".

**Analogy:** the datapath is a railway network; the control unit is the signalman deciding which points to switch, cycle by cycle.

## 3.1 ⭐⭐ Hardwired vs microprogrammed control

### 💡 The idea — two ways to build the conductor

**Hardwired control:** the control unit is a **fixed logic circuit** (gates and flip-flops) whose inputs are the opcode and the current step, and whose outputs are the control signals. It is designed once, in silicon.
- ✅ **Fast** — signals appear after a couple of gate delays.
- ❌ Changing the instruction set means **redesigning the hardware**. Impractical for a large, irregular instruction set.

**Microprogrammed control:** the control signals for each step are stored as a word in a small, fast internal memory called **control memory**. Each such word is a **microinstruction**; the sequence for one machine instruction is a **microprogram**. A **Control Address Register (CAR)** points at the current microinstruction.

Essentially, the control unit becomes a tiny computer running a tiny program that interprets the real instructions.
- ✅ ⭐ **Flexible** — to change or add an instruction you rewrite the microcode, not the silicon. (This is how Intel ships microcode updates to fix CPU bugs.)
- ❌ ⭐ **Slower** — every step needs an extra control-memory read.

| | ⭐ **Hardwired** | ⭐ **Microprogrammed** |
|---|---|---|
| Implementation | Fixed combinational/sequential logic | Microinstructions in **control memory** |
| ⭐ Speed | ⭐ **Faster** | ⭐ **Slower** (extra memory lookup) |
| ⭐ Flexibility | Difficult to modify | ⭐ **Easy — rewrite the microcode** |
| Design effort for complex ISAs | Very high | Lower |
| ⭐ Suits | ⭐ **RISC** | ⭐ **CISC** |

### ⭐ Horizontal vs vertical microinstructions

A microinstruction has to encode which control signals to assert. Two encodings:

| | ⭐ **Horizontal** | ⭐ **Vertical** |
|---|---|---|
| Encoding | ⭐ **One bit per control signal** (unencoded) | Signals grouped into **encoded fields** |
| Word width | ⭐ **Wide** | ⭐ **Narrow** |
| Decoder needed? | ❌ No | ✅ Yes |
| ⭐ Parallelism | ⭐ **High** — can assert many signals at once | ⭐ **Low** — one signal per field |
| Speed | Faster | Slower (decode step) |
| Control memory size | Larger | Smaller |

**Memory hook:** *horizontal* = a long horizontal row of bits = wide = parallel.

---

# 4. ⭐⭐ Pipelining

## 4.1 💡 The idea — the laundry analogy

You have four loads of washing. Each load needs: **wash (30 min) → dry (30) → fold (30) → put away (30)**.

**Sequentially:** finish load 1 completely (2 hours), then start load 2. Four loads = **8 hours**. The dryer sits idle three-quarters of the time.

**Pipelined:** as soon as load 1 leaves the washer, put load 2 in. Now all four machines run at once on different loads.
```
Time:    0    30   60   90   120  150  180  210
Load 1:  Wash Dry  Fold Away
Load 2:       Wash Dry  Fold Away
Load 3:            Wash Dry  Fold Away
Load 4:                 Wash Dry  Fold Away
```
Four loads = **3.5 hours**, not 8.

⭐ **Crucial insight: pipelining does NOT make any single load faster** — load 1 still takes 2 hours. It increases **throughput** (loads finished per hour), not **latency**.

That is exactly what instruction pipelining does. The classic 5-stage RISC pipeline:

📌 **IF** (Instruction Fetch) → **ID** (Instruction Decode / register read) → **EX** (Execute / ALU) → **MEM** (Memory access) → **WB** (Write Back to register)

```
Instr 1:  IF  ID  EX  MEM WB
Instr 2:      IF  ID  EX  MEM WB
Instr 3:          IF  ID  EX  MEM WB
Instr 4:              IF  ID  EX  MEM WB
Cycle:    1   2   3   4   5   6   7   8
```

⭐ This is also **why RISC's fixed-length, uniform instructions matter**: every instruction takes the same path through the same five stages, so the pipeline never stalls for structural reasons.

## 4.2 ⭐⭐ The formulas

For a **k-stage** pipeline executing **n** instructions, one cycle per stage, no stalls:

| Quantity | ⭐ Formula | Where it comes from |
|---|---|---|
| ⭐ **Pipelined cycles** | ⭐ **k + (n − 1)** | k cycles to fill the pipeline for instruction 1, then 1 cycle for each of the remaining n−1 |
| Non-pipelined cycles | **n × k** | each instruction runs to completion alone |
| ⭐ **Speedup** | ⭐ **S = nk / (k + n − 1)** | ratio of the two |
| ⭐ **Maximum speedup** | ⭐ **k** (as n → ∞) | the (n−1) term dominates the denominator |
| **Efficiency** | η = S / k | how close you get to the ideal |
| **Throughput** | n / total time | instructions completed per unit time |

📌 **Clock period of a pipeline = max(stage delay) + latch/register overhead**

⭐ The **slowest stage sets the clock** for everyone. This is why designers split slow stages — a pipeline is only as fast as its worst stage.

### 🔢 Worked examples

🔢 **5-stage pipeline, 1000 instructions, no stalls.**
Cycles = k + (n−1) = 5 + 999 = **1004**
Non-pipelined = 1000 × 5 = 5000
Speedup = 5000/1004 ≈ **4.98** — very close to the theoretical maximum of 5, because n ≫ k.

🔢 **Same pipeline, only 5 instructions.**
Cycles = 5 + 4 = 9. Speedup = 25/9 ≈ **2.78** — far from 5, because the fill time is a large fraction of the total. ⭐ **Pipelining pays off only for long instruction streams.**

🔢 **Non-uniform stage delays.** Stages take 10, 8, 12, 9 ns, with 1 ns latch overhead.
Clock period = max(10, 8, 12, 9) + 1 = **13 ns**.
Non-pipelined instruction time = 10 + 8 + 12 + 9 = 39 ns.
Speedup ≈ 39/13 = **3** (not 4, because the stages are unbalanced). ⭐ **Balanced stages give better speedup.**

🔢 **Throughput.** 1004 cycles at 13 ns = 13,052 ns for 1000 instructions ≈ **76.6 million instructions/second**.

## 4.3 ⭐⭐ Pipeline hazards

### 💡 The idea

The laundry analogy breaks down when loads interfere with each other. In a processor, three kinds of interference — called **hazards** — force the pipeline to stall (insert "bubbles"), destroying the speedup.

### (a) ⭐ Structural hazards

**Two instructions need the same hardware resource in the same cycle.**

🔢 With a single unified memory, in cycle 4 instruction 1 is in **MEM** (reading data) while instruction 4 is in **IF** (reading an instruction). Both need the memory port. One must wait.

⭐ **Fix: duplicate the resource.** ⭐ **Separate instruction and data caches** solve exactly this — which is the practical reason for the modified-Harvard organisation mentioned in §1.2. Other fixes: multiple register file ports, pipelined functional units.

### (b) ⭐⭐ Data hazards

**An instruction needs a value that an earlier, still-in-flight instruction has not produced yet.**

🔢 ```
ADD R1, R2, R3    ; R1 ← R2 + R3
SUB R4, R1, R5    ; needs R1 — but ADD only writes R1 in its WB stage
```
```
ADD:  IF  ID  EX  MEM  WB
                        ↑ R1 written here
SUB:      IF  ID  EX  MEM  WB
               ↑ R1 needed here — two cycles too early
```

⭐ **Three kinds of dependency:**

| Type | Full name | Example | ⭐ Removable by register renaming? |
|---|---|---|---|
| ⭐ **RAW** | **Read After Write** — ⭐ **true data dependency** | `ADD R1,..` then `SUB ..,R1,..` | ⭐ **❌ NO — genuine** |
| **WAR** | Write After Read — **anti-dependency** | `SUB ..,R1,..` then `ADD R1,..` | ✅ Yes |
| **WAW** | Write After Write — **output dependency** | `ADD R1,..` then `MUL R1,..` | ✅ Yes |

⭐ **Why the distinction matters:** WAR and WAW are only conflicts over the *name* R1, not over the *value*. Give the second instruction a different physical register and the conflict vanishes — that is **register renaming**. RAW is a real flow of data and cannot be renamed away.

⭐ **Fixes for RAW:**
1. ⭐ **Operand forwarding (bypassing)** — the main fix. Don't wait for the value to reach the register file; route the ALU output **directly** to the next instruction's ALU input.
```
ADD:  IF  ID  EX ──┐ MEM  WB
                   │ forward
SUB:      IF  ID  EX  MEM  WB
```
2. **Stalls / bubbles** — insert NOPs.
3. **Compiler instruction reordering** — move independent instructions into the gap.

⚠ ⭐ **Forwarding cannot fully eliminate the LOAD-USE hazard.** A load's data is only available after **MEM**, so an instruction immediately using it must still stall one cycle:
```
LW  R1, 0(R2)     IF  ID  EX  MEM ──┐ WB
                                    │ earliest available
ADD R3, R1, R4        IF  ID  ***  EX  ...    ← one stall
```
Compilers try to fill that slot with an unrelated instruction.

### (c) ⭐ Control (branch) hazards

**After a branch, the pipeline does not know which instruction to fetch next** until the branch condition is resolved — several stages later. Meanwhile it has already fetched instructions that may be wrong and must be discarded (**flushed**).

⭐ **Fixes:**
- **Stall/flush** — simple, expensive.
- ⭐ **Branch prediction:**
  - *Static:* always-taken, always-not-taken, or "backward taken, forward not taken" (loops branch backward, so this is a good heuristic).
  - *Dynamic:* a **1-bit predictor** (remember what happened last time — mispredicts twice per loop) or a ⭐ **2-bit saturating counter** (must be wrong twice to change its mind — mispredicts once per loop). A **Branch Target Buffer (BTB)** caches the target address too.
- ⭐ **Delayed branch (delay slot)** — the instruction right after the branch **always executes**, and the compiler fills that slot with something useful. Used in MIPS.
- **Early branch resolution** — compute the condition in ID instead of EX, cutting the penalty.

📌 **Average CPI with branches = 1 + (branch frequency × branch penalty)**

🔢 20% of instructions are branches, penalty 3 cycles, no prediction:
CPI = 1 + 0.2 × 3 = **1.6** — a 60% slowdown from branches alone.

🔢 Same, but with a predictor that is 90% accurate:
CPI = 1 + 0.2 × 0.10 × 3 = **1.06**. ⭐ That is why branch prediction is worth so much silicon.

---

# 5. ⭐⭐ Memory hierarchy

## 5.1 💡 The idea — why a hierarchy at all

Memory technology forces an unavoidable trade-off:

- **Fast memory is expensive and small.** (SRAM: ~1 ns, but ~6 transistors per bit.)
- **Cheap memory is large and slow.** (Disk: terabytes for pennies, but ~10 ms.)

You cannot have all three of fast, big and cheap. So instead of choosing, computers use **all of them at once**, arranged in layers, with the fast-and-small layers holding the data you are most likely to need next.

```
     ┌─────────────┐   ~0.3 ns    bytes        most expensive/bit
     │  Registers  │
     ├─────────────┤   ~1 ns      64 KB
     │   L1 cache  │
     ├─────────────┤   ~4 ns      512 KB
     │   L2 cache  │
     ├─────────────┤   ~15 ns     8 MB
     │   L3 cache  │
     ├─────────────┤   ~80 ns     16 GB
     │ Main memory │
     ├─────────────┤   ~100 µs    1 TB
     │     SSD     │
     ├─────────────┤   ~10 ms     4 TB
     │ Magnetic disk│
     └─────────────┘              cheapest/bit
```

Going **down**: capacity ↑, cost per bit ↓, access time ↑.

### ⭐ Why it works: locality of reference

The hierarchy would be useless if programs accessed memory randomly. They do not. Real programs exhibit:

⭐ **Temporal locality** — *"if you used it, you'll use it again soon."*
🔢 A loop counter `i` is read and written on every one of a million iterations. The instructions of the loop body are executed a million times.

⭐ **Spatial locality** — *"if you used it, you'll use its neighbour soon."*
🔢 `for (i=0; i<n; i++) sum += A[i];` touches A[0], A[1], A[2]… in order. Instructions are also normally executed in sequence.

⭐ **Spatial locality is why caches fetch a whole BLOCK (typically 64 bytes), not a single word.** Fetching A[0] brings A[1] through A[15] along for free.

## 5.2 ⭐ SRAM vs DRAM

### 💡 The idea

| | ⭐ **SRAM** (Static RAM) | ⭐ **DRAM** (Dynamic RAM) |
|---|---|---|
| Stores a bit in | A **flip-flop** (~6 transistors) | A **capacitor + 1 transistor** |
| ⭐ **Refresh needed?** | ❌ **No** — the flip-flop holds itself | ⭐ **✅ YES** — the capacitor leaks, so every cell must be rewritten every few milliseconds |
| Speed | ⭐ **Fast** | Slower (and unavailable during refresh) |
| Density | Low | ⭐ **High** (1 transistor per bit) |
| Cost per bit | High | Low |
| ⭐ **Used for** | ⭐ **Cache** | ⭐ **Main memory** |

⚠ Both are **volatile** — they lose data when power is removed. "Dynamic" refers to the refresh requirement, not to anything about the data.

## 5.3 ⭐⭐⭐ Cache mapping

### 💡 The idea

Main memory is huge; the cache is tiny. So **many memory blocks must compete for each cache slot**. The mapping policy decides where a given memory block is allowed to sit.

Three policies, on a spectrum:

**1. Direct mapped** — each memory block has exactly **one** allowed cache line, chosen by `block number mod number_of_lines`.
- ✅ Simplest and fastest lookup (check one line, one comparator).
- ❌ ⭐ Two hot blocks that map to the same line evict each other endlessly — **conflict misses**, even with the rest of the cache empty.

**2. Fully associative** — a block may go in **any** line.
- ✅ No conflict misses at all.
- ❌ Finding a block means comparing its tag against **every** line simultaneously — one comparator per line. Only feasible for tiny caches (e.g. the TLB).

**3. ⭐ k-way set associative** — the practical compromise. The cache is divided into **sets** of k lines each. A block maps to one **set** (like direct mapped), but within that set it may occupy any of the k lines (like fully associative).
- Typical real caches are 4-way, 8-way or 16-way.

### ⭐⭐ Splitting the address

The physical address is chopped into fields:

```
Direct mapped / set associative:
┌──────────┬───────────────┬────────┐
│   TAG    │ INDEX (line   │ BLOCK  │
│          │  or set no.)  │ OFFSET │
└──────────┴───────────────┴────────┘

Fully associative (no index — could be anywhere):
┌────────────────────────────┬────────┐
│            TAG             │ OFFSET │
└────────────────────────────┴────────┘
```

📌 ⭐ **Offset bits = log₂(block size in bytes)** — identifies the byte within the block
📌 ⭐ **Index bits = log₂(number of lines)** [direct mapped] **or log₂(number of sets)** [set associative]
📌 ⭐ **Number of sets = number of lines ÷ associativity**
📌 ⭐ **Tag bits = total address bits − index bits − offset bits**

### 🔢 Worked example 1 — direct mapped

**8 KB cache, 32-byte blocks, 32-bit physical address.**

```
Offset = log₂(32)          = 5 bits
Lines  = 8192 / 32 = 256   → Index = log₂(256) = 8 bits
Tag    = 32 − 8 − 5        = 19 bits
```

Answer: ⭐ **tag 19, index 8, offset 5**

Check: 19 + 8 + 5 = 32 ✅

### 🔢 Worked example 2 — set associative

**2-way set associative, 128 lines total, 64-byte blocks.**

```
Sets   = 128 / 2 = 64      → Index = log₂(64) = 6 bits
Offset = log₂(64)          = 6 bits
```
⭐ Number of **sets = 64**.

⚠ ⭐ **The block size affects the OFFSET, not the number of sets.** A question that hands you a block size while asking only for the set count is testing precisely this — the answer needs only lines and associativity.

### 🔢 Worked example 3 — full breakdown

**4-way set associative, 64 KB cache, 32-byte blocks, 32-bit address.**
```
Lines  = 65536 / 32 = 2048
Sets   = 2048 / 4   = 512   → Index = 9 bits
Offset = log₂(32)   = 5 bits
Tag    = 32 − 9 − 5 = 18 bits
```

## 5.4 ⭐⭐ Average Memory Access Time (AMAT)

### 💡 The idea

The cache is fast but sometimes misses; memory is slow but always has the data. The **average** access time depends on how often you hit.

⚠ ⭐ **Two conventions exist and they give different answers. The question must tell you which — read the wording carefully.**

📌 ⭐ **Hierarchical / sequential** (look in the cache first; on a miss, *then* go to memory):
**AMAT = T_cache + (1 − h) × T_memory**

📌 ⭐ **Simultaneous / parallel** (both lookups start at the same time):
**AMAT = h × T_cache + (1 − h) × T_memory**

🔢 **T_cache = 10 ns, T_memory = 100 ns, hit ratio h = 0.9:**
- **Hierarchical:** 10 + 0.1 × 100 = 10 + 10 = ⭐ **20 ns**
- **Simultaneous:** 0.9 × 10 + 0.1 × 100 = 9 + 10 = ⭐ **19 ns**

⭐ **Wording that signals hierarchical:** *"the word is first searched in the cache; if not found, it is fetched from main memory"*, or *"on a miss the block is then brought from memory"*.
⭐ **Wording that signals simultaneous:** *"the cache and main memory are accessed in parallel"*, or the question simply gives you "cache access time" and "memory access time" with no ordering language and expects the weighted average.

📌 **Multi-level caches:** AMAT = T_L1 + m_L1 × (T_L2 + m_L2 × T_memory), where m = miss rate.

🔢 T_L1 = 1 ns (miss rate 5%), T_L2 = 10 ns (miss rate 20%), T_mem = 100 ns:
AMAT = 1 + 0.05 × (10 + 0.20 × 100) = 1 + 0.05 × 30 = **2.5 ns**

📌 **Hit ratio h = hits / total accesses.** Miss ratio = 1 − h.

## 5.5 ⭐ Cache write policies

### 💡 The idea

Reads are easy. **Writes** raise a question: when the CPU writes to a cached location, should main memory be updated immediately?

| Policy | Memory updated | ✅ Pros | ❌ Cons |
|---|---|---|---|
| **Write-through** | On **every** write | Memory is always consistent; simple; easy for multiprocessors | Lots of memory traffic |
| ⭐ **Write-back** (copy-back) | ⭐ **Only when the block is EVICTED** | ⭐ **Far fewer memory writes** (a loop writing the same variable a million times touches memory once) | Memory is temporarily **stale**; needs a ⭐ **DIRTY BIT** per line to know whether the block was modified |

⭐ **The dirty bit** is the giveaway. It is set when a line is written, and checked on eviction: if clean, just overwrite it; if dirty, write it back to memory first.

**On a write MISS**, a second choice:
- **Write-allocate:** fetch the block into the cache first, then write. Usually paired with write-back.
- **No-write-allocate / write-around:** write straight to memory, skip the cache. Usually paired with write-through.

## 5.6 ⭐ Replacement policies

When a set is full and a new block arrives, which existing block is evicted?

| Policy | Rule | Note |
|---|---|---|
| ⭐ **LRU** (Least Recently Used) | Evict the one unused for longest | ⭐ Best practical performance (exploits temporal locality); exact implementation is expensive, so real caches approximate it |
| **FIFO** | Evict the oldest resident | Simple; ⚠ can suffer **Belady's anomaly** |
| **LFU** (Least Frequently Used) | Evict the least-used | Needs counters; a once-hot block can linger |
| **Random** | Pick at random | Cheapest hardware, surprisingly decent |
| **Optimal (OPT/MIN)** | Evict the one needed furthest in the future | ⭐ **Unimplementable** — requires knowing the future. Used only as a benchmark |

⚠ ⭐ **A direct-mapped cache has NO replacement policy** — there is only one legal location, so there is no choice to make.

## 5.7 ⭐ The three Cs — types of cache miss

### 💡 A useful diagnostic framework

| Miss type | Cause | ⭐ Reduced by |
|---|---|---|
| ⭐ **Compulsory** (cold-start) | The **first ever** reference to a block. Unavoidable | Larger block size, prefetching |
| ⭐ **Capacity** | The working set is **bigger than the cache** | ⭐ **A larger cache** |
| ⭐ **Conflict** | Too many blocks map to the **same set** (even with room elsewhere) | ⭐ **Higher associativity** |

⚠ ⭐ A **fully associative** cache has **no conflict misses** by definition. If a question says "increasing associativity removed the misses", they were conflict misses.

## 5.8 Main memory organisation

**Memory interleaving:** consecutive addresses are spread across separate memory **banks**, so their accesses overlap in time.

🔢 With 4-way low-order interleaving, address 0 is in bank 0, address 1 in bank 1, address 2 in bank 2, address 3 in bank 3, address 4 back in bank 0. Reading four consecutive words starts all four banks nearly at once instead of waiting 4 × 80 ns serially. ⭐ **Purpose: higher memory bandwidth**, which is exactly what cache block fills need.

📌 **Memory chip count:**
**chips = (target capacity ÷ chip capacity) × (target word width ÷ chip word width)**

🔢 Build a **16K × 8** memory from **4K × 4** chips:
- Capacity: 16K/4K = **4** rows
- Width: 8/4 = **2** columns
- Total = 4 × 2 = **8 chips**, arranged as 4 rows of 2.

📌 **Address lines** for N locations = log₂N. **Data lines** = word width.
🔢 A 16K × 8 memory needs log₂(16384) = **14 address lines** and **8 data lines**.

## 5.9 ⭐ Secondary storage — the magnetic disk

### 💡 The physical picture

A stack of spinning **platters**. Each surface has concentric rings called **tracks**, each divided into **sectors** (the smallest readable unit, traditionally 512 bytes). The same track number across all platters forms a **cylinder** — reachable without moving the head, hence a useful unit for allocation.

A read/write **head** on a moving arm must physically travel to the right track, then wait for the right sector to rotate underneath it. Both of those are **mechanical**, which is why disks are a million times slower than RAM.

📌 ⭐ **Disk access time = Seek time + Rotational latency + Transfer time** (+ controller overhead)

| Component | What it is |
|---|---|
| ⭐ **Seek time** | Moving the arm to the correct track — usually the largest term |
| ⭐ **Rotational latency** | Waiting for the sector to spin under the head |
| **Transfer time** | Actually reading the bits as they pass |

📌 ⭐ **Average rotational latency = ½ × (time for one full rotation)**

*Why half?* On average the sector you want is half a revolution away — sometimes it is just arriving, sometimes you just missed it.

📌 ⭐ **Average rotational latency (seconds) = 30 / RPM**
*(one rotation = 60/RPM seconds; half of that = 30/RPM)*

🔢 **6000 RPM disk:**
- 6000 rotations/minute = 100 rotations/second → one rotation = **10 ms**
- ⭐ Average rotational latency = 10/2 = **5 ms**

🔢 **7200 RPM disk:** 30/7200 s = **4.17 ms**

📌 **Transfer time = (bytes to transfer ÷ bytes per track) × rotation time**

🔢 Disk: 7200 RPM, 500 sectors/track, 512 bytes/sector, average seek 5 ms. Read one sector:
- Rotation = 60/7200 = 8.33 ms → rotational latency = **4.17 ms**
- Transfer = (1/500) × 8.33 = **0.017 ms**
- Total ≈ 5 + 4.17 + 0.02 = **≈ 9.2 ms**

⭐ Note how the transfer time is negligible — disk performance is dominated by **seek and rotation**, which is why sequential access is orders of magnitude faster than random access, and why Week 6's disk scheduling algorithms exist.

📌 **Disk capacity = surfaces × tracks/surface × sectors/track × bytes/sector**

---

# 6. ⭐⭐ I/O organisation

## 6.1 💡 The idea — three ways to move data

A keyboard produces a few bytes per second; a disk produces hundreds of megabytes per second. The CPU runs billions of cycles per second. Getting data between them without wasting the CPU is the problem.

**Method 1 — Programmed I/O (polling).** The CPU repeatedly reads the device's status register: *"Ready yet? Ready yet? Ready yet?"*
- ✅ Trivially simple.
- ❌ ⭐ The CPU **busy-waits**, doing nothing useful. Terrible for slow devices.

**Method 2 — Interrupt-driven I/O.** The CPU issues the request and goes off to do other work. When the device is ready it raises an **interrupt** line; the CPU suspends what it was doing, services the device, and resumes.
- ✅ The CPU is free while waiting.
- ❌ ⭐ The CPU still handles **every single word**. For a disk block of 4096 bytes that is thousands of interrupts.

**Method 3 — ⭐ DMA (Direct Memory Access).** A dedicated **DMA controller** is given the source, destination and byte count, and then transfers the whole block between the device and memory **without the CPU touching the data at all**. The CPU is interrupted **once**, at the end.
- ✅ ⭐ Minimal CPU involvement, highest throughput.

| Technique | CPU involvement | Interrupts per block | Speed |
|---|---|---|---|
| **Programmed I/O** | ⭐ **Highest** — busy-waits | 0 (but CPU blocked) | Slowest |
| **Interrupt-driven** | Moderate — per **word** | Many | Medium |
| ⭐ **DMA** | ⭐ **Lowest** — per **block** | ⭐ **One** | ⭐ **Fastest** |

## 6.2 ⭐ Interrupts

### How it works — the sequence

1. The device asserts the interrupt request line.
2. The CPU **finishes the current instruction** (interrupts are honoured between instructions, so the machine is in a clean state).
3. The CPU **saves the context** — PC and PSW onto the stack.
4. It **identifies the source** — either the device supplies a vector (vectored) or the CPU polls (non-vectored).
5. It jumps via the **interrupt vector table** to the **Interrupt Service Routine (ISR)**.
6. The ISR runs, servicing the device.
7. The context is **restored** and the interrupted program resumes as if nothing happened.

| Type | Meaning |
|---|---|
| **Maskable** | Can be disabled by software when the CPU is doing something uninterruptible |
| ⭐ **Non-maskable (NMI)** | ⭐ **Cannot be disabled** — reserved for catastrophes (power failure, memory parity error) |
| **Vectored** | The device supplies the ISR address → fast |
| **Non-vectored** | Fixed ISR address; the CPU must poll to find who interrupted → slower |
| **Software interrupt / trap** | Generated by an instruction — this is how **system calls** work (Week 6) |
| **Exception** | Generated by an error (divide by zero, page fault) |

⭐ **Priority schemes:** when several devices interrupt at once, priority decides who wins.
- **Daisy chaining** — devices are wired in a chain; the acknowledgement signal passes down it, so the device **closest to the CPU has the highest priority**.
- **Priority encoder** (§5.2 of Week 1) — hardware picks the highest-numbered active request.
- Multiple interrupt lines at different priority levels.

## 6.3 ⭐⭐ DMA

### How it works

The CPU programs the DMA controller with:
- **source / destination address** in memory
- **word count**
- **direction** (read or write)
then goes back to work. The DMA controller becomes a **bus master**, moving data directly between the device and memory, and interrupts the CPU only when the count reaches zero.

### ⭐ The three transfer modes

| Mode | Behaviour | Trade-off |
|---|---|---|
| ⭐ **Cycle stealing** | The DMA takes the bus for ⭐ **ONE bus cycle at a time**, releasing it in between so the CPU can continue | Transfer is slower, but the CPU keeps running (just a bit slower) |
| ⭐ **Burst / block mode** | The DMA holds the bus for the ⭐ **ENTIRE block** | ⭐ **Fastest transfer**, but the CPU **stalls** for the duration |
| **Transparent / hidden mode** | The DMA transfers only in cycles when the CPU does not need the bus | ⭐ **Zero CPU slowdown**, but the slowest transfer |

⚠ ⭐ **"Cycle stealing" steals MEMORY/BUS cycles, not CPU cycles.** The CPU keeps executing whenever it is doing register-only work and does not need the bus. This is exactly what the phrase is testing.

### ⭐ How devices are addressed

| Scheme | Description | ✅ / ❌ |
|---|---|---|
| ⭐ **Memory-mapped I/O** | Device registers occupy ordinary **memory addresses** | ✅ Any load/store instruction works; no special instructions needed. ❌ Consumes address space |
| ⭐ **Isolated / port-mapped I/O** | Devices live in a **separate I/O address space** | ✅ No address space lost. ❌ Needs special `IN`/`OUT` instructions and an extra control line |

⭐ ARM and most RISC machines use **memory-mapped I/O**; x86 has both.

---

# 7. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| Von Neumann bottleneck | One shared bus for instructions and data |
| Harvard architecture | Separate instruction and data memories |
| PC holds | **Address of the next instruction** |
| IR holds | The current instruction |
| MAR / MDR | Address / Data being accessed |
| Zero-address instructions | **Stack machine** |
| One-address instructions | **Accumulator machine** |
| Stack machine ordering | Postfix / reverse Polish |
| Mode for pointers | **Indirect** |
| Mode for arrays | **Indexed** |
| Mode for local variables / struct fields | Base + displacement |
| Mode for branches | PC-relative |
| Memory accesses for indirect operand | **2** |
| Memory accesses for register direct | 0 |
| RISC memory access | **Load/store only** |
| RISC instruction length | Fixed |
| RISC control unit | Hardwired |
| CISC control unit | Microprogrammed |
| Microprogrammed control | Slower, more flexible |
| Horizontal microinstruction | Wider, more parallel, no decoder |
| Pipeline cycles (k stages, n instr) | **k + n − 1** |
| Non-pipelined cycles | n × k |
| Pipeline speedup | nk/(k+n−1) |
| **Maximum speedup** | **k** |
| Pipeline clock period | max(stage delay) + latch overhead |
| RAW | True dependency; **not** removable by renaming |
| WAR / WAW | Anti / output dependency; removable by renaming |
| Fix for data hazard | **Operand forwarding** |
| Hazard forwarding can't fix | **Load-use** (1 stall remains) |
| Fix for structural hazard | Duplicate the resource (separate I/D caches) |
| Fix for control hazard | Branch prediction, delay slot |
| CPI with branches | 1 + (frequency × penalty) |
| Cache exists because of | **Locality of reference** |
| Fetch a whole block because of | **Spatial** locality |
| Cache made of / main memory made of | **SRAM / DRAM** |
| DRAM needs | **Refresh** |
| Offset bits | log₂(block size) |
| Index bits | log₂(lines) or log₂(sets) |
| **Number of sets** | **lines ÷ associativity** |
| Tag bits | address − index − offset |
| **AMAT (hierarchical)** | **T_c + (1−h)·T_m** |
| AMAT (simultaneous) | h·T_c + (1−h)·T_m |
| Write-back updates memory | **On eviction**; needs a **dirty bit** |
| Write-through updates memory | Every write |
| Direct-mapped replacement policy | **None needed** |
| Fully associative has no | **Conflict misses** |
| Three Cs | Compulsory, capacity, conflict |
| Conflict misses reduced by | Higher associativity |
| Interleaving improves | Memory **bandwidth** |
| Chips needed | (capacity ratio) × (width ratio) |
| **Avg rotational latency** | **½ rotation = 30/RPM s** |
| Disk access time | Seek + rotational + transfer |
| Dominant disk cost | Seek + rotation (not transfer) |
| Lowest CPU involvement I/O | **DMA** |
| CPU busy-waits in | Programmed I/O (polling) |
| **Cycle stealing** | One bus cycle at a time; CPU continues |
| **Burst mode** | DMA holds the bus for the whole block |
| NMI | Cannot be masked |
| Daisy chain priority | Nearest device to the CPU wins |
| Memory-mapped I/O | Devices share the memory address space |

---

# 8. ⚠ Common traps

1. ⭐ **PC vs IR vs MAR vs MDR** — know exactly what each holds.
2. ⭐ **AMAT convention** — hierarchical `T_c + miss×T_m` vs simultaneous `h·T_c + miss·T_m`. Read the wording; both appear as options.
3. ⭐ **Block size does not change the number of sets** — it changes the offset field.
4. ⭐ **Pipeline cycles = k + n − 1**, not k + n or n × k.
5. **Maximum speedup approaches k; it never exceeds k.**
6. ⭐ **Cycle stealing ≠ burst mode.** Cycle stealing interleaves one cycle at a time; burst holds the bus throughout.
7. **Write-back needs a dirty bit; write-through does not.**
8. **Forwarding does not eliminate the load-use stall.**
9. ⭐ **RAW is the only dependency that renaming cannot remove.**
10. ⭐ **Rotational latency is HALF a rotation on average**, not a full one.
11. **Direct-mapped caches have no replacement policy.**
12. **Fully associative caches have no conflict misses.**
13. **A slow pipeline stage sets the clock for every stage.**
14. **Microprogrammed = slower but flexible** (people often reverse this because "programmed" sounds modern).

---

# 9. Practice

- GATE: [`Paper2_S03_Computer_Organization_and_Architecture/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S03_Computer_Organization_and_Architecture/) — **251 questions**
- State-PSC level: [`Paper2_S03_.../`](../02_State_PSC_PYQs/Subject_wise/Paper2_S03_Computer_Organization_and_Architecture/) — **245 questions**
- Test: [`Week_02_Test.md`](../04_Mock_Tests/Week_02_Test.md)

**Priority order if short on time:** cache address splitting & AMAT → pipeline formulas and the three hazards → addressing modes (and memory-access counts) → DMA modes & interrupts → disk access time → hardwired vs microprogrammed → RISC vs CISC → the three Cs.
