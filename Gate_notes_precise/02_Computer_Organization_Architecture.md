# 02 · Computer Organization & Architecture — Precise Notes

> **TPSC ATO (IT) Paper-II §3** · ~9 marks (estimate) · Syllabus: *"Computer Organization and Architecture — machine instructions and addressing modes; ALU, data path and control unit; instruction pipelining, pipeline hazards; memory hierarchy: cache, main memory and secondary storage; I/O interface (interrupt and DMA mode)"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson (`1.`), Vishvadeep (`7.`), ME-class (`3.` Made Easy class), Shared (`6.`), Ace (`4.`). Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/02_COA/` — open them for diagrams.
> Cross-refs: floating point / IEEE-754 → `01_Digital_Logic.md` · paging, TLB, virtual memory → `05_Operating_Systems.md`.

## Which notes are worth your time

| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| `2.COA_Sanchit_Sir_Notes.pdf` | Sanchit Jain (Knowledge Gate) | Typed slides | 145 | 4 | GATE/NET-tagged PYQs per topic, cache-mapping tables, disk/DMA numericals · thin on datapath, chips, interleaving, branch handling; a few slips (corrected below) |
| `1.COA.pdf` | Pearson GATE guide | Typed book | 75 | 4 | Clean definitions; branch handling, interrupt priority, DMA configurations, disk formula; PYQs with keys · dry, no shortcuts |
| `7.CO_Vishvadeep_sir_Notes.pdf` | Vishvadeep Gothi (Unacademy) | Handwritten scan, neat | 152 | 4 | Memory-chip arrangement, DRAM refresh, multilevel AMAT, disk, microcode encoding, CPI with stalls · off-syllabus extras |
| `3.CO_Made_Easy_Class_Latest_Notes.pdf` | Made Easy classroom | Handwritten scan | 256 | 4 | Derivations: expanding opcode, refs per mode, register windows, WT/WB timing · no index, long, light on disk/DMA |
| `6.CO_Shared_Notes.pdf` | Student copy of Vishvadeep's course | Handwritten scan (colour) | 170 | 3 | Same examples as #7, neater · duplicate — open one of #6/#7 |
| `8.Computer_Organisation_Hand_Written_Notes_Made_Easy.pdf` | Made Easy classroom (another student) | Phone photos | 142 | 3 | Expanding-opcode ranges, shift/rotate · subset of #3, cluttered |
| `4.Ace_Academy_CO_Class_Notes.pdf` | Ace Academy | Faint photocopy | 152 | 2 | Booth recoding · hard to read, sparse, some wrong claims |
| `5.Computer_Organization-CS.pdf` | Wiki Engineering (raghul.org) | Handwritten scan | 186 | 2 | CPU-time basics · messy, mixes in 8086/8051 |

**If you open only one PDF besides these notes:** Vishvadeep (#7). It is compact and easy to read, and it is strongest exactly where Sanchit is weakest (main-memory chips/refresh, disk, multilevel caches, microcode sizing). Use Pearson (#1) only for looking up definitions.

## Topic map

| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | Instruction formats | ⭐⭐ | count of 1-address instructions, immediate-field width |
| 2 | Addressing modes, RISC/CISC | ⭐⭐⭐ | match mode ↔ use, EA value, RISC traits |
| 3 | ALU & datapath | ⭐ | overflow rule, Booth worst case, datapath cycles |
| 4 | Control unit | ⭐⭐ | hardwired vs micro, horizontal vs vertical, word size |
| 5 | Pipelining | ⭐⭐⭐ | time / speedup / throughput with latch delay |
| 6 | Hazards | ⭐⭐⭐ | RAW/WAR/WAW, cycles with forwarding, branch CPI |
| 7 | Cache | ⭐⭐⭐ | tag/index/offset, tag directory, AMAT, misses in a sequence |
| 8 | Main memory | ⭐⭐ | chips + decoder, refresh, interleaving |
| 9 | Disk | ⭐⭐ | capacity, access time, sector number |
| 10 | I/O, interrupts, DMA | ⭐⭐⭐ | mode comparison, interrupt sequence, DMA % CPU time |

## 1. Machine instructions & formats

### 1.1 Registers, instruction cycle
- ⭐ **PC** = address of the *next* instruction · **IR** = current instruction · **MAR** = address sent to memory · **MDR/MBR** = data to/from memory · **AC** = implied operand · **PSW** = flags Z, S, C, V, P.
- Fetch: `MAR ← PC; MDR ← M[MAR], PC ← PC + step; IR ← MDR` → decode → (indirect: fetch EA) → execute → check interrupt **[Src: Sanchit p.127–128]**.
- 📌 PC step = instruction length. Fixed length L from start S → legal PC = S + kL (GATE-2006: 24-bit instructions from 300 → **600**).
- ⚠ Some notes (Sanchit p.91) say IR holds "the address of the current register". IR actually holds the current *instruction*.

### 1.2 Number of address fields

| Type | X = (A+B)×(C+D) | # | Feature |
|---|---|---|---|
| 3-address | ADD R1,A,B · ADD R2,C,D · MUL X,R1,R2 | 3 | shortest program, longest instruction |
| 2-address | MOV R1,A · ADD R1,B · MOV R2,C · ADD R2,D · MUL R1,R2 · MOV X,R1 | 6 | first operand is also destination |
| 1-address | LOAD A · ADD B · STORE T · LOAD C · ADD D · MUL T · STORE X | 7 | implied accumulator |
| 0-address | PUSH A · PUSH B · ADD · PUSH C · PUSH D · ADD · MUL · POP X | 8 | stack, postfix; only PUSH/POP have addresses |

**[Src: Sanchit p.93–99]**
- ⭐ Fewer address fields → shorter instructions, longer programs.
- ⚠ In a 3-address format each field is a memory operand **or** a register, never an implied accumulator (GATE-2015).

### 1.3 Field widths, expanding opcode
- 📌 Register field = ⌈log₂ #registers⌉ · address field = log₂ #addressable units · opcode = ⌈log₂ #instructions⌉.
- 📌 **Expanding opcode:** a 2-address opcode has n − 2a bits → 2^(n−2a) patterns; free = patterns − used; possible 1-address instructions = free × 2^a. Check: Σ(count × 2^(operand bits)) ≤ 2^n.
- 🔢 32-bit instruction, 12-bit address, 250 two-address instructions → 2⁸ − 250 = 6 free → 6 × 2¹² = **24,576** one-address.
- 🔢 GATE-2018: 16-bit format, 16 int regs (4 b), 64 FP regs (6 b): 2¹⁶ − (4·2¹² + 8·2¹² + 14·2¹⁰) = 2,048 → 1F instructions = 2,048/2⁶ = **32**.
- 🎯 **How it's asked:** immediate width: 32-bit word, 40 instructions, 24 regs, 2 reg operands → **16** (GATE-2016). 64 regs, 45 instructions → max unsigned immediate **16383** (GATE-2014). Byte-aligned 34-bit instruction × 100 → **500 B** (GATE-2016).

## 2. Addressing modes & ISA style

### 2.1 Modes

| Mode | Operand / EA | Memory refs* | Typical use |
|---|---|---|---|
| Implied | implicit in opcode | 0 | accumulator/stack ops |
| Immediate | operand = field | 0 | ⭐ constants |
| Register | in R | 0 | fastest |
| Direct | EA = A | 1 | ⭐ globals |
| Indirect | EA = M[A] | 2 | ⭐ pointers, passing arrays |
| Register indirect | EA = R | 1 | pointer without full address |
| Auto-inc/dec | EA = R; R ± item size | 1 | ⭐ loops, stacks |
| Indexed | EA = A + R_index | 1 | ⭐ arrays (A = base) |
| Base | EA = R_base + A | 1 | ⭐ relocation, `X(R1)` |
| PC-relative | EA = PC(updated) + A | 1 | ⭐ branches |

*for the operand, after instruction fetch. **[Src: Pearson p.6–8]**
- ⭐ Run-time relocation: **base** and **PC-relative** (GATE-2004).
- ⭐ Matching (GATE-2000/2001): indirect ↔ pointers/array parameters · indexed ↔ arrays · base ↔ relocatable code · immediate ↔ constants · auto-decrement ↔ loops.
- ⭐ `LW R1, 20(R2)` = base/displacement (GATE-2011). The auto-increment step = data-item size (GATE-2008).
- ⚠ Some notes (Sanchit p.108) define implied mode as "operand in the instruction itself". That is immediate mode; in implied mode the operand is implicit in the opcode.
- 📌 PC-relative uses the PC *after* fetch: 2-word instruction at 900, offset 20 → EA = **922**.
- 📌 Average operand-fetch time = Σ(mode fraction × its memory refs) × memory cycle **[Src: ME-class p.110]**.

### 2.2 RISC vs CISC

| | RISC | CISC |
|---|---|---|
| Instructions / modes | few; 3–5 modes | 100–250; 5–20 modes |
| Length | ⭐ fixed | variable |
| Memory access | ⭐ LOAD/STORE only | ALU ops on memory |
| CPI | ≈ 1, pipelined | multi-cycle |
| Registers | many | few |
| Control | ⭐ hardwired | ⭐ microprogrammed |

- 📌 Overlapped register windows: window = L + 2C + G; file = (L + C)·W + G. 🔢 G 10, L 10, C 6, W 8 → 32 and **138** **[Src: ME-class p.135]**.
- ⚠ Some notes (Ace p.2) say RISC needs no extra registers. In fact RISC uses large register files.

## 3. ALU and datapath
> 2's complement, adders and IEEE-754 are in `01_Digital_Logic.md`.

### 3.1 ALU
- 📌 ⭐ Overflow V = C_in(MSB) ⊕ C_out(MSB): only when both operands have the same sign and the result's sign differs. Carry ≠ overflow.
- Arithmetic right shift copies the sign bit (÷2, rounds toward −∞); arithmetic left shift = ×2 if no overflow; rotate loses no bit.
- **Booth:** look at (Qₙ, Qₙ₊₁): 01 → add M, 10 → subtract M, 00/11 → nothing; then arithmetic shift right **[Src: Pearson p.18]**.
- 📌 Add/sub count = number of 0↔1 transitions (append 0 on the right). ⭐ Worst case 0101…; best case long runs. 🔢 0111 1110 → 1 sub + 1 add.

### 3.2 Datapath
- 📌 MUX-based common bus: k registers × n bits → **n MUXes of k×1**, ⌈log₂ k⌉ select lines (tri-state buffers are the alternative) **[Src: Sanchit p.122]**.
- Single bus, ALU fed by temp Y, result in Z: `ADD R3,R1,R2` = 3 steps (R1out,Yin → R2out,Add,Zin → Zout,R3in). A three-bus datapath takes 1 step **[Src: Pearson p.22]**.
- Fetch (single bus): PCout,MARin,Read,Add(+4),Zin → Zout,PCin,WMFC → MDRout,IRin.
- 🎯 **How it's asked:** `add R0,R1` on a single-bus datapath → **3** cycles (GATE-2005). `MBR ← PC; MAR ← X; PC ← Y; M ← MBR` = initiating interrupt service (GATE-2013).

## 4. Control unit

### 4.1 Hardwired vs microprogrammed

| | Hardwired | Microprogrammed |
|---|---|---|
| Signals from | gates + decoders + sequence counter | control words in control memory |
| Speed | ⭐ fastest | slower |
| Modification | redesign | rewrite control memory |
| Used in | ⭐ RISC | ⭐ CISC |

**[Src: Pearson p.23–24; Sanchit p.142–143]**
- Micro CU: CAR → control memory → µIR; the sequencer picks CAR + 1, the branch field (condition true) or the opcode mapping. Proposed by Wilkes, 1951.
- Microinstruction = [condition select | control field | next address] **[Src: Sanchit p.144]**.

### 4.2 Horizontal vs vertical

| | Horizontal | Vertical |
|---|---|---|
| Encoding | 1 bit per signal | encoded fields + decoder |
| Word | long | short |
| Parallelism | ⭐ high | limited |
| Speed | faster | slower |

- ⭐ Coaching order (ME-class p.150): speed vertical < horizontal < hardwired; flexibility hardwired < horizontal < vertical.
- ⚠ "Vertical is more flexible" (Sanchit p.143) is the coaching view. Textbooks call horizontal more flexible in signal combinations, so answer by the option's wording.

### 4.3 Control-word sizing
- 📌 Horizontal word = #signals + condition-select bits + next-address bits; next-address bits = ⌈log₂ control-memory words⌉.
- 📌 Vertical group of n mutually exclusive signals = ⌈log₂ n⌉ bits, or ⌈log₂(n + 1)⌉ if "none active" must be encodable **[Src: Vishvadeep p.40]**.
- 🔢 GATE-2008: 140 × 7 = 980 words → 10 bits; word = 125 + 10 = **135**, CAR **10**.
- 🔢 GATE-2004: 26 = 13 + X + Y, Y = log₂ 8 = 3 → X = 10 → **1024** words.
- 🔢 GATE-1996: 25 signals, ≤ 2 active → 2 × 5 = **10** bits. Groups 30/90/20/10/50 → 5+7+5+4+6 = **27** bits (Pearson).

## 5. Instruction pipelining
k stages, n instructions, stage delays tᵢ, latch delay d.
- 📌 τ = max tᵢ + d · T_pipe = (k + n − 1)τ · T_nonpipe = n·Σtᵢ (no latches; or nkτ if stated per-cycle).
- 📌 Speedup S = T_nonpipe/T_pipe → Σtᵢ/τ for large n. Balanced, d = 0: nk/(k + n − 1) → ⭐ **k (maximum)**.
- 📌 Efficiency = S/k · throughput = n/T_pipe → 1/τ · CPU time = IC × CPI × clock period.
- ⭐ Pipelining raises throughput, not one instruction's latency; a single instruction runs slower because of the latches **[Src: Sanchit p.71–75]**.
- 🔢 GATE-2004: 150/120/160/140 + 5 ns → τ 165; 1000 items → 1003 × 165 = **165.5 µs**.
- 🔢 GATE-2008: 10 ns single cycle → stages 2.5/1.5/2/1.5/2.5 + 0.5 → τ 3 → S = **3.33**.
- 🔢 GATE-2016: 800/500/400/300 ps, first stage split 600 + 350 → throughput **+33.3 %**.
- 🔢 GATE-2015: 2.5 GHz with CPI 4 vs 5-stage at 2 GHz → 1.6/0.5 = **3.2**.
- 🎯 **How it's asked:** highest clock = smallest maximum stage (GATE-2014). D1 (3,2,4,2,3) vs D2 (8×2) on 100 instructions → 202 ns saved (GATE-2005). Unequal per-instruction stage times → draw the space-time chart (4 + ΣPO = **219**, GATE-2018).
- ⚠ Sanchit p.75–76 has arithmetic slips: 1/15 ns = **66.7 MHz** (not 0.66 GHz); 100 instructions at τ 165 average (4 + 99) × 165/100 = **169.95 ns** (not 169.25).

## 6. Pipeline hazards

### 6.1 Types

| Hazard | Cause | Remedies |
|---|---|---|
| Structural | two instructions need one resource | duplicate (⭐ split I/D cache), stall |
| Data | operand not ready | forwarding, interlock stall, reordering/NOPs |
| Control | branch outcome/target unknown | flush, prediction, delayed branch, BTB |

### 6.2 Data hazards (J after I)

| Hazard | Dependence | Example (I: R2 ← R1 + R3) |
|---|---|---|
| ⭐ RAW | true: O(I) ∩ I(J) ≠ ∅ | J: R4 ← R2 + R3 |
| WAR | anti: I(I) ∩ O(J) ≠ ∅ | J: R3 ← R4 + R5 |
| WAW | output: O(I) ∩ O(J) ≠ ∅ | J: R2 ← R4 + R5 |

**[Src: Sanchit p.86–89]**
- ⭐ An in-order 5-stage pipeline stalls only on RAW. WAR and WAW need out-of-order or unequal-latency execution (fixed by register renaming). ⚠ "Anti-dependence always causes a hazard" is **false**.
- 📌 Forwarding: ALU→ALU RAW costs 0 stalls. ⭐ A **load-use** dependence still costs 1 stall. Delayed load = the compiler fills the slot after a load.
- 🎯 **How it's asked:** total cycles with forwarding and multi-cycle EX: **15** (GATE-2010), **13** (GATE-2015). A dependent instruction's execute starts the cycle after the producer finishes.

### 6.3 Control hazards
- 📌 Branch resolved in stage s → penalty s − 1 cycles. CPI = 1 + branch fraction × penalty (× misprediction rate if predicted).
- 🔢 GATE-2006: resolved in stage 3, 20 % branches → CPI 1.4 → **1.4 s** for 10⁹ instructions at 1 GHz.
- 🔢 GATE-2014: 6 stages, 25 % incur 2 stalls → CPI 1.5 → S = **4**.
- 🔢 GATE-2013: τ = 11 ns, 12 instructions, I4 → I9 (resolved in stage 4) → 15 cycles = **165 ns**.
- Static: stall, ⭐ predict-not-taken, predict-taken, by opcode. Dynamic: ⭐ 2-bit predictor (flips after two mispredictions), branch history table. Also BTB, loop buffer, ⭐ **delayed branch** (compiler fills slots after the branch) **[Src: Pearson p.49–51]**.
- ⚠ Some notes (Sanchit p.83) list delayed load as a control-hazard fix. Delayed load fixes the load-use *data* hazard; the control-hazard counterpart is the delayed branch.

## 7. Memory hierarchy & cache

### 7.1 Hierarchy, locality
- Registers → cache (SRAM) → main (DRAM) → disk → tape: going down, cost/bit ↓, capacity ↑, access time ↑.
- Access methods: random (RAM), direct (disk), sequential (tape), associative (CAM/TLB).
- ⭐ Temporal locality → LRU. ⭐ Spatial locality → multi-word blocks (GATE-2001). Locality justifies having a cache (GATE-1995).

### 7.2 Mapping, address split
PA bits, block B, cache C, N = C/B lines, k ways.

| | Direct | k-way set assoc. | Fully assoc. |
|---|---|---|---|
| Placement | block mod N | set = block mod (N/k) | anywhere |
| Address | Tag \| Line \| Offset | Tag \| Set \| Offset | Tag \| Offset |
| Tag bits | PA − log₂C | PA − log₂C + log₂k | PA − log₂B |
| Comparators | 1 | k | N |
| Replacement policy | none | needed | needed |
| Hit latency | MUX + comparator | MUX + comparator + OR | comparator + OR |
| Misses | ⭐ conflict-prone | fewer conflicts | no conflict misses |

**[Src: Sanchit p.12–27; Pearson p.62–64]**
- 📌 ⭐ Doubling associativity (same C, B): tag +1, set bits −1. The CPU–memory data-bus width is unaffected (GATE-2014).
- 📌 Block j → lines (j mod v)·k … (j mod v)·k + k − 1 (GATE-2013).
- 📌 Tag directory = N × (tag + valid + dirty + replacement bits).
- 🔢 GATE-2011: 8 KB direct, 32 B blocks, 32-bit PA → tag 19, + valid + dirty → 21 × 256 = **5376 bits**.
- 🔢 GATE-2012: 256 KB 4-way, 32 B, 32-bit → tag **16**; (16 + 2 + 1 + 1) × 8192 = **160 Kbits**.
- 🎯 **How it's asked:** 40-bit PA, 512 KB 8-way → tag 40 − 19 + 3 = **24** (GATE-2016). Direct tag 10 → 16-way tag **14** (GATE-2017). Tag = P − N + log₂K (GATE-2018). Split E201F into tag/line (GATE-2015). "Which block is not in cache at the end?" (GATE-2007, 2009).
- ⚠ Some notes (Sanchit p.17) say "n tag bits → n comparators". Read this as one n-bit comparator; direct mapping needs a single tag comparator.

### 7.3 Average access time

| Organisation | Cache + MM | Three levels |
|---|---|---|
| ⭐ Simultaneous | H·Tc + (1 − H)·Tm | H₁T₁ + (1−H₁)H₂T₂ + (1−H₁)(1−H₂)T₃ |
| ⭐ Hierarchical | Tc + (1 − H)·Tm | T₁ + (1−H₁)T₂ + (1−H₁)(1−H₂)T₃ |

**[Src: Sanchit p.38–39]**
- 📌 Miss-penalty form: AMAT = hit time + miss rate × miss penalty. Average cost/bit = ΣCᵢSᵢ/ΣSᵢ.
- ⚠ Some notes (Sanchit p.38) print the hierarchical formula (with T₁+T₂ sums) under *simultaneous* access. The correct simultaneous form has no sums.
- Choosing the formula: "hierarchical"/"L1 first"/block-transfer data → hierarchical; "ignoring search time" → simultaneous. The keys for GATE-2004 (**12.6 ns**) and NET-Dec-2018 (**7.55 ns**) both use the simultaneous form.
- Block transfer: miss penalty = latency + block/bandwidth: 64 B, 32 ns, 1 GB/s → **96 ns** (GATE-2006).
- 🔢 GATE-2017: L1 1, L2 8, penalty 18, m₁ = 2m₂, AMAT 2 → 1 + m₁(8 + 18m₂) = 2 → m₁ = **0.111**, m₂ = 0.056.
- 🔢 GATE-2014: reads 1/5 ns, writes 2/10 ns (hit/miss), 160 reads + 40 writes, H 0.9 → **1.68 ns**.

### 7.4 Write policies

| | Write-through | Write-back |
|---|---|---|
| MM updated | every write | when a dirty block is evicted |
| Extra bit | — | ⭐ dirty bit |
| Traffic | high | low |
| MM state | always current | stale until eviction |
| Write-miss pairing | no-write-allocate | write-allocate |

- 📌 WT: T = f_r[H·Tc + (1 − H)(Tc + Tm)] + f_w·Tm (write time = max(Tc, Tm)) **[Src: ME-class p.250]**. 🔢 NET-Dec-2014: 50/300 ns, 75 % reads, H 0.8 → **157.5 ns**.
- 📌 WB miss = Tc + (1 + dirty fraction) × block-transfer time.
- Inclusion (L1 ⊆ L2) needs only L2 ≥ L1 in size (GATE-2008). Exclusion: L2 holds L1's victims.
- ⚠ Some notes (Sanchit p.41) call write-through/write-back coherence methods. They are write policies; multiprocessor coherence (snooping, MESI) is separate.

### 7.5 Replacement, misses
- FIFO, ⭐ LRU, LFU, random, optimal (benchmark).
- ⚠ Sanchit p.32 says FIFO *will* show Belady's anomaly with more lines. It only *can*; LRU and optimal never do.
- 📌 3 Cs: **compulsory** (first touch; ↓ bigger blocks) · **capacity** (↓ bigger cache) · **conflict** (↓ associativity; none in FA).
- ⭐ Smaller block → lower miss penalty (GATE-2014); bigger block → better spatial locality, fewer blocks.
- 🎯 **How it's asked:** 2-way, 4 blocks, LRU, 8,12,0,12,8 → **4** misses (GATE-2004); conflict misses in a repeated pattern → **76** (GATE-2017).

## 8. Main memory

### 8.1 Technologies

| | SRAM | DRAM |
|---|---|---|
| Cell | flip-flop (~6 T) | 1 T + capacitor |
| Refresh | no | ⭐ yes |
| Speed / cost / density | fast, costly, low | slow, cheap, high |
| Use | cache | main memory |

- ROM types: PROM (once), EPROM (UV erase), EEPROM (electrical, byte-wise), flash (block erase).
- 📌 Address bits = log₂(size/addressable unit): 4 GB, 2-byte words, word-addressable → **31** (GATE-2016).

### 8.2 Chip count
- 📌 #chips = (W × w)/(Wc × wc). Rows (series, decoded) = W/Wc; chips per row (parallel) = w/wc.
- 📌 Address lines = log₂W; common to all chips = log₂Wc; decoder = log₂(W/Wc) → W/Wc **[Src: Vishvadeep p.65–66]**.
- 🔢 128×8 chips for 2048 B → **16** chips, 11 lines, 7 common, **4×16** decoder. 1 MB from 256K×1 → **32**.

### 8.3 DRAM refresh
- One refresh refreshes one row; chips refresh in parallel → total = rows per chip × refresh time.
- 🔢 GATE-2010: 1M×1 chips with 1K rows, 100 ns → **100 × 2¹⁰ ns**. GATE-2005: 100 refreshes/ms × 100 ns → **1 %**.

### 8.4 Memory interleaving (added — not in sources)

| | Low-order | High-order |
|---|---|---|
| Module bits | low log₂m (address mod m) | high log₂m |
| Consecutive words | different modules | same module |
| Gain | ⭐ overlapped block fetch, more bandwidth | easy expansion |

- 📌 m-way low-order: an m-word block takes ≈ T_access + m·t_transfer instead of m·T_access.
- 🎯 **How it's asked:** 8 modules, bus 100 ns per write, module busy 600 ns → the bus limits → **10,000** stores/ms (GATE-2004) **[Src: Vishvadeep p.67]**.

## 9. Secondary storage (disk)
- Platter → 2 surfaces → tracks → sectors. **Cylinder** = the same track on all surfaces (#cylinders = tracks per surface). ⭐ The sector is the smallest unit transferred **[Src: Vishvadeep p.113; Pearson p.66]**.
- 📌 Capacity = surfaces × tracks × sectors × bytes per sector.
- 📌 R = 60/RPM s; ⭐ average rotational latency = R/2; data rate = bytes per track × rev/s; sector transfer = R/sectors.
- 📌 ⭐ Access time = seek + R/2 + transfer (+ controller).
- 📌 n contiguous sectors: seek + R/2 + n·t_s. n random sectors: n(seek + R/2 + t_s) **[Src: Vishvadeep p.116]**.
- 📌 ⟨c,h,s⟩ → (c·heads + h)·sectors + s.
- Seek time isn't linear in distance because of arm inertia (GATE-2008).
- 🔢 GATE-2007: 16 × 128 × 256 × 512 B = **256 MB**, sector address **19** bits.
- 🔢 GATE-2015: 15000 RPM, seek = 2 × latency, 512 B at 50 MB/s, controller 10× → 4 + 2 + 0.01 + 0.10 ≈ **6.1 ms**.
- 🔢 GATE-2015: seek 4, 10000 RPM, 600 sectors/track, 2000 random sectors → 2000 × 7.01 = **14020 ms**.
- 🔢 GATE-2009: 63 sectors, 20 surfaces, ⟨400,16,29⟩ → **505037**.

## 10. I/O interface, interrupts, DMA

### 10.1 Interface, I/O addressing
- An interface handles differences in speed, data format, signal type and operating mode; it has data, status and control registers **[Src: Sanchit p.46–49]**.

| | ⭐ Memory-mapped | ⭐ Isolated (port-mapped) |
|---|---|---|
| Address space | shared with memory | separate |
| Instructions | ordinary memory instructions | IN/OUT only |
| Control lines | MEMRD/MEMWR | extra IORD/IOWR (IO/M̄) |
| Trade-off | all modes usable; loses addresses | full memory space |

- IOP = processor with DMA capability that runs its own I/O programs.
- **Strobe**: one line, no acknowledgement. **Handshaking**: data-valid + data-accepted lines **[Src: Sanchit p.52–56]**.

### 10.2 Transfer modes

| | Programmed | Interrupt-driven | DMA |
|---|---|---|---|
| Readiness | CPU polls (busy wait) | device interrupts | DMAC |
| Data moved by | CPU | CPU in ISR | DMAC, device ↔ memory |
| CPU busy | whole transfer | per byte/word | start + end only |
| Suits | slow, simple | medium | ⭐ fast block (disk) |

- ⭐ Programmed I/O raises no interrupts.
- 🎯 **How it's asked:** 10 KB/s device, 4 µs interrupt overhead → gain **25** over polling (GATE-2005). Program loop 3502 cycles vs DMA 1020 → **3.4** (GATE-2011).

### 10.3 Interrupts
- ⭐ Sequence: finish current instruction → push PC/PSW → load ISR address → run ISR → restore (QPTRS, GATE-2018). ⭐ Interrupts are checked **after the current instruction finishes** (GATE-2009).
- Mano: IEN (ION/IOF) and FGI/FGO flags; the interrupt cycle saves PC in M[0] and jumps to 1 **[Src: Sanchit p.139–140]**.
- Maskable vs **non-maskable** (NMI: power failure) · **vectored** (device supplies ISR address) vs non-vectored (fixed address) · hardware vs software/trap.

| Priority | How | Note |
|---|---|---|
| Polling | ISR tests devices in order | ⭐ slow |
| ⭐ Daisy chain | INTA passes device to device; the first requester keeps it and sends its vector | fixed, non-uniform priority (GATE-1996) |
| Parallel | mask register + priority encoder | fast |

**[Src: Sanchit p.61–62]**

### 10.4 DMA
- Device request → DMAC bus request → CPU grants bus → DMAC transfers, updating address/count → count = 0 → interrupt to CPU **[Src: Sanchit p.64; Pearson p.39]**.

| Mode | Bus use | Note |
|---|---|---|
| ⭐ Burst | whole block | fastest; CPU locked out |
| ⭐ Cycle stealing | one cycle per word | CPU slowed slightly |
| Transparent | only idle CPU cycles | no slowdown |

- ⚠ Some notes (Sanchit p.65) describe "DMA only during decode/execute, when the CPU doesn't need the bus" as cycle stealing. That is **transparent** DMA; cycle stealing forces the CPU to give up a cycle.
- Single-bus detached DMA uses 2 bus cycles per word.
- 📌 Burst CPU % = overhead/(overhead + transfer) · cycle stealing % = memory cycle/word interval · bus grants = ⌈size/2^(count bits)⌉.
- 🔢 GATE-2004: 20 KB at 10 MB/s (2 ms) vs 2 µs setup → **0.1 %**. GATE-2016: 16-bit counter, 29,154 KB → **456**.
- 🔢 GATE-2005: 25.6 MB/s disk, 4-byte words, 40 ns memory cycle → **≈ 25 %** blocked.
- ⭐ Highest I/O bandwidth = block-transfer DMA + vectored interrupts (GATE-2006-IT).

## Last-day revision sheet

| Item | Formula |
|---|---|
| Expanding opcode | next count = free patterns × 2^(freed bits) |
| Register windows | L + 2C + G ; file (L + C)W + G |
| Overflow | C_in(MSB) ⊕ C_out(MSB) |
| Booth ops | 0↔1 transitions; worst 0101… |
| MUX bus | n MUXes of k×1 |
| Horizontal word | signals + condition + log₂(CM words) |
| Vertical field | ⌈log₂ n⌉ (⌈log₂(n+1)⌉ with "none") |
| Pipeline | τ = max + latch ; (k + n − 1)τ |
| Speedup | nk/(k+n−1) → k ; Σtᵢ/τ |
| Efficiency / throughput | S/k ; → 1/τ |
| CPI with stalls | 1 + Σ freq × stalls ; S = k/CPI |
| Branch penalty | resolve stage − 1 |
| Tag | direct PA − log₂C ; k-way + log₂k ; FA PA − log₂B |
| Tag directory | N × (tag + control bits) |
| AMAT | simultaneous H·Tc + (1−H)Tm ; hierarchical Tc + (1−H)Tm |
| WT average | f_r[H·Tc + (1−H)(Tc+Tm)] + f_w·Tm |
| Chips / decoder | (W·w)/(Wc·wc) ; log₂(W/Wc) → W/Wc |
| Disk | seek + (60/RPM)/2 + transfer ; rate = track bytes × rev/s |
| ⟨c,h,s⟩ | (c·H + h)·S + s |
| DMA | burst overhead/(overhead + transfer) ; stealing cycle/interval |

1. ⭐ PC = next-instruction address; IR = current instruction.
2. ⭐ 0-address = stack; only PUSH/POP carry addresses.
3. ⭐ Indirect mode = two memory references.
4. ⭐ Base and PC-relative modes give relocation; indexed suits arrays.
5. ⭐ RISC: load/store, fixed length, hardwired, CPI ≈ 1; CISC: microprogrammed.
6. ⭐ Horizontal = 1 bit per signal, fast and parallel; vertical = encoded, needs decoder.
7. ⭐ Maximum pipeline speedup = number of stages.
8. ⭐ Pipelining improves throughput, not latency.
9. ⭐ RAW true, WAR anti, WAW output; in-order 5-stage pipelines see only RAW.
10. ⭐ Forwarding removes ALU→ALU stalls; load-use still costs 1.
11. ⭐ Split I/D caches remove the memory structural hazard.
12. ⭐ Delayed branch fills the slot after a branch.
13. A 2-bit predictor flips after two mispredictions.
14. ⭐ Spatial locality → blocks; temporal → LRU.
15. ⭐ Direct mapping: no replacement policy, conflict misses.
16. ⭐ Fully associative: N comparators, no conflict misses.
17. ⭐ Doubling associativity: tag +1, index −1.
18. ⭐ Write-back needs a dirty bit; write-through keeps MM current.
19. ⭐ FIFO can show Belady's anomaly; LRU and optimal can't.
20. Inclusion needs only L2 ≥ L1.
21. ⭐ DRAM: capacitor, refresh, main memory; SRAM: flip-flop, cache.
22. ⭐ Low-order interleaving puts consecutive words in different modules.
23. ⭐ Disk access = seek + rotational latency + transfer.
24. ⭐ Memory-mapped I/O uses memory instructions; isolated I/O uses IN/OUT.
25. ⭐ Programmed I/O busy-waits and raises no interrupts.
26. ⭐ An interrupt is serviced after the current instruction completes.
27. ⭐ Daisy chain: priority fixed by position.
28. ⭐ Vectored interrupt: the device gives the ISR address.
29. ⭐ Burst DMA for disks; cycle stealing takes one cycle per word.
30. ⭐ Strobe has no acknowledgement; handshaking adds one.

## Dropped as outside TPSC syllabus
- IEEE-754 / floating point (Sanchit p.1–6, Vishvadeep p.145, Pearson ch.2): see `01_Digital_Logic.md`.
- Number systems, complement arithmetic, BCD, multiply/divide flowcharts, carry look-ahead (Pearson ch.2, ME-class p.8, Ace): Digital Logic.
- Virtual memory, paging, TLB, page faults, swap space (Sanchit p.8–9, p.70; Ace): `05_Operating_Systems.md`.
- Flynn's taxonomy, vector/array processors (Pearson ch.4, Vishvadeep p.118).
- Non-linear pipelines, reservation tables, collision vectors (Vishvadeep p.140, Shared p.160).
- Re-order buffers and out-of-order internals (ME-class p.205); multiprocessor coherence protocols.
- Amdahl's law and MIPS (`8.` p.125, Vishvadeep p.35). For the record: S = 1/((1 − f) + f/s).
- 8085/8086/8051 and 8251/8255/8259/8237 peripheral chips (`5.`, `8.` p.140).
- Mano basic-computer instruction micro-ops beyond the fetch and interrupt cycles (Sanchit p.129–137).
- Tape/floppy/optical media details (Pearson ch.5); C-programming PYQs inside Pearson.
