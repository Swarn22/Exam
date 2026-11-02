# Study Roadmap — 2 Nov 2026 → Exam on Sun 17 Jan 2027

**TPSC Assistant Technical Officer (IT)** · Written 170 marks (Paper-I 50 + Paper-II 120, OMR, 180 min) · qualifying **55% in each paper** (UR: 27.5 / 50 and 66 / 120) · negative marking assumed −1/3.

**76 days = 11 weeks.** Today (Mon 2 Nov) is Day 1. The exam date is the one you gave me — TPSC had not published it at the time of writing, so **re-check it on the admit card**, and if it moves, shift the calendar by the same number of days (the cut order in [§7](#7-if-you-fall-behind) tells you what to drop if it moves earlier).

---

## 1. The plan on one screen

| Phase | Weeks | Dates | What happens |
|---|---|---|---|
| **A · Core GATE subjects** | 1–7 | 2 Nov → 20 Dec | DL → COA → Programming & DS → Algorithms → OS → DBMS → CN, one weekly test each |
| **B · Short & non-GATE sections** | 8–9 | 21 Dec → 3 Jan | Compiler, Probability, Communication, Software Engg, Web, Cloud, Cyber Security (~45 marks, mostly definitional) |
| **C · Mocks & repair** | 10 | 4 Jan → 10 Jan | 3 repair days, Full Mock A + B, Paper-I consolidation day |
| **D · Final** | 11 | 11 Jan → 17 Jan | Full Mock C, revision sheets only, taper, **exam** |

Paper-I gets **1 hour every single day** across all four phases — it can eliminate you on its own.

### Why this order
- **Dependencies first:** Digital Logic feeds COA; C feeds Data Structures; DS feeds Algorithms; OS paging builds on COA memory.
- **The five heaviest sections (DS & Programming, Algorithms, OS, DBMS, CN ≈ 58 marks) are all done by 20 Dec**, leaving four weeks of spaced revision on them before the exam.
- **Memorisation-heavy, definitional sections go last** (Phase B), because they are what you forget fastest and they are the cheapest marks in the paper (~31 marks with no GATE overlap).

---

## 2. Your material — what to open for each section

| § | Section | Est. marks | Learn from | Then practise | Weekly test |
|---|---|---|---|---|---|
| 2 | Digital Logic | ~9 | [P01](01_Digital_Logic.md) | GATE + state PYQs `Paper2_S02_*` | T01 |
| 3 | Computer Organization & Architecture | ~9 | [P02](02_Computer_Organization_Architecture.md) | `Paper2_S03_*` | T02 |
| 5 | Data Structures & Programming (C, C++, Java) | ~14 | [P03](03_Programming_and_Data_Structures.md) | `Paper2_S05_*` | T03, T04 |
| 6 | Algorithms | ~11 | [P04](04_Algorithms.md) | `Paper2_S06_*` | T05 |
| 8 | Operating System | ~11 | [P05](05_Operating_Systems.md) | `Paper2_S08_*` | T06 |
| 9 | Databases | ~11 | [P06](06_DBMS.md) | `Paper2_S09_*` | T07 |
| 11 | Computer Networks | ~11 | [P07](07_Computer_Networks.md) | `Paper2_S11_*` | T08 |
| 7 | Compiler Design | ~6 | [P08](08_Compiler_Design.md) | `Paper2_S07_*` | T11 (part) |
| 1 | Probability & Statistics | ~7 | [P09](09_Probability_and_Statistics.md) | `Paper2_S01_*` | T09 (part) |
| 4 | Analog & Digital Communication | ~8 | [N09 Part A](../05_Notes/Week_09_Communication_and_Probability.md) | state PYQs only `Paper2_S04_*` | T09 (part) |
| 10 | Information Systems & Software Engg | ~8 | [N11 Part A](../05_Notes/Week_11_SoftwareEngineering_and_Compiler.md) | state PYQs only `Paper2_S10_*` | T11 (part) |
| 12 | Web Technologies | ~6 | [N10 Part A](../05_Notes/Week_10_Web_Cloud_CyberSecurity.md) | state PYQs only `Paper2_S12_*` | T10 |
| 14 | Cloud Technology | ~4 | [N10 Part B](../05_Notes/Week_10_Web_Cloud_CyberSecurity.md) | state PYQs only `Paper2_S14_*` | T10 |
| 13 | Cyber Security & Emerging Tech | ~5 | [N10 Part C](../05_Notes/Week_10_Web_Cloud_CyberSecurity.md) | state PYQs only `Paper2_S13_*` | T10 |
| P-I | English + Reasoning/Quant | 30 | [P10](10_General_Ability_Aptitude_English.md) + [NP1 Parts A–B](../05_Notes/Paper1_English_Reasoning_GK.md) | `Paper1_01_*`, `Paper1_02_*` | 5 Q in every test |
| P-I | GK & Current Affairs | 20 | [NP1 Part C](../05_Notes/Paper1_English_Reasoning_GK.md) + your own CA notebook | — | 5 Q in every test |

**Abbreviations used below:** **P01–P10** = files in this folder · **N09/N10/N11** = `05_Notes/Week_XX_…` · **NP1** = `05_Notes/Paper1_English_Reasoning_GK.md` · **N12** = `05_Notes/Week_12_Formula_Sheets_and_Revision.md` · **GQ** = `03_GATE_CSE_PYQs/Subject_wise/<subject>/` · **SQ** = `02_State_PSC_PYQs/Subject_wise/<subject>/` · **T01–T12** = `04_Mock_Tests/Week_XX_Test.md` · **RS** = the "Last-day revision sheet" at the end of a P-file.

Sections 4, 10, 12, 13, 14 have no notes on gatenotes.in and no GATE questions, so they are learnt from the existing detailed notes in `05_Notes/` and practised from the state-PSC PYQ folders only.

---

## 3. Daily template (≈ 34 h / week)

| Block | Mon–Fri | Sat | Sun | What you do |
|---|---|---|---|---|
| 🅰 **Paper-II — learn + practise** | 2.5 h | 5 h | 3 h | ① Read the day's P-file sections with a notebook open — copy every 📌 formula and ⚠ trap by hand (≈ 60 min). ② Solve **25–40 PYQs on the same topics**: GQ first, then SQ (≈ 75 min). ③ Log every wrong answer in the [error log](../01_Study_Plan/Weekly_Progress_Tracker.md#error-log) (≈ 15 min). |
| 🅱 **Paper-I** | 1 h | 1 h | 1 h | 20 min English · 20 min reasoning/quant · 20 min GK + current affairs, following the week's theme. Fixed time of day; never skipped. |
| 🅲 **Spaced revision** | 0.5 h | 1 h | 1 h | Re-read the **RS** of the subject(s) named in the *Revise* column — no new material. |
| 🅳 **Weekly test** | — | — | 2 h | 25-Q test timed (~35 min), then review every question including the ones you got right by luck. |

**Revision spacing:** each finished subject comes back in the *Revise* column after about **1 week, 3 weeks and 6 weeks**, and then once more in the final week. That spacing is already built into the calendar below — just follow the column.

If you are not working full-time, keep the same order and simply finish each day's block early; don't pull later subjects forward until a weekly test scores ≥ 18/25.

---

## 4. Day-by-day calendar

### Week 1 · 2–8 Nov · Digital Logic (P01)
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 2 Nov | **P01 §1** · Number systems & conversions; signed magnitude, 1's/2's complement, ranges, overflow; BCD/Gray/Excess-3 | — |
| Tue 3 Nov | **P01 §2** · Fixed point; **IEEE-754** single/double (bias, normalised/denormalised, special values); binary arithmetic, Booth | P01 today's 📌 |
| Wed 4 Nov | **P01 §3** · Boolean algebra laws, duality, canonical SOP/POS, minterms/maxterms; NAND/NOR universality, gate counting | P01 number systems |
| Thu 5 Nov | **P01 §4** · **K-maps** (4–5 variables, don't-cares, prime & essential prime implicants), Quine–McCluskey awareness | P01 Boolean algebra |
| Fri 6 Nov | **P01 §5** · Combinational: MUX/DEMUX (implementing functions), decoder/encoder/priority encoder, half/full adder, ripple vs **carry look-ahead**, comparators | P01 K-maps |
| Sat 7 Nov | **P01 §6** · Sequential: latches vs flip-flops, SR/JK/D/T characteristic + **excitation tables**, race-around, master–slave; counters (ripple/sync, mod-N, ring, Johnson), shift registers, Mealy vs Moore · **GQ + SQ `Paper2_S02` — 60 Q** | P01 combinational |
| Sun 8 Nov | **T01** + review · redo every wrong PYQ · write your own one-page DL sheet | P01 RS |

**Paper-I this week:** English — articles & prepositions · Reasoning — number/letter series, analogy · GK — **Tripura basics & geography** (NP1 §10.1–10.2).

### Week 2 · 9–15 Nov · Computer Organization & Architecture (P02)
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 9 Nov | **P02 §1–2** · Instruction formats (0/1/2/3-address), expanding opcodes; **addressing modes** & effective-address calculation | P01 RS |
| Tue 10 Nov | **P02 §3–4** · ALU & datapath; **hardwired vs microprogrammed** control (horizontal/vertical, control-word size); RISC vs CISC | P02 addressing |
| Wed 11 Nov | **P02 §5–6** · **Pipelining**: speedup, efficiency, throughput, CPI with stalls; hazards (structural, RAW/WAR/WAW, control), forwarding, branch handling | P02 control unit |
| Thu 12 Nov | **P02 §7.1–7.2** · **Cache mapping**: direct / set-associative / fully associative; tag-index-offset split; tag-directory size | P02 pipelining |
| Fri 13 Nov | **P02 §7.3–7.5, §8** · **AMAT** (hierarchical vs simultaneous), write-through/back, replacement, miss types; main memory, interleaving, chip counting | P02 cache mapping |
| Sat 14 Nov | **P02 §9–10** · Secondary storage (disk capacity, access time = seek + rotation + transfer); **I/O: programmed vs interrupt vs DMA** (cycle stealing / burst), priority interrupts · **GQ + SQ `Paper2_S03` — 60 Q** | P02 AMAT |
| Sun 15 Nov | **T02** + review · own one-page COA sheet | P02 RS · **P01 RS (1 wk)** |

**Paper-I:** English — subject–verb agreement & tenses (error spotting) · Reasoning — coding–decoding, blood relations · GK — **Tripura history** (Manikya dynasty, merger 1949, statehood 1972) (NP1 §10.3).

### Week 3 · 16–22 Nov · Programming & Data Structures (P03)
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 16 Nov | **P03 §1** · C: data types, operators & precedence, storage classes, scope/lifetime, control-flow and `++` traps | P02 RS |
| Tue 17 Nov | **P03 §2–3, §7** · C: **pointers**, arrays vs pointers, **row/column-major address calculation**, strings, struct/union & `sizeof`, dynamic memory, parameter passing; **recursion tracing** | P03 C basics |
| Wed 18 Nov | **P03 §13** · **C++, Java & OOP essentials** (state-PSC favourite) · then **T03** (C/C++/Java/OOP) + quick review | P03 pointers |
| Thu 19 Nov | **P03 §4–6** · **Stacks** (infix→postfix/prefix, evaluation), **queues** (circular, deque, priority queue), **linked lists** | P03 OOP |
| Fri 20 Nov | **P03 §8–9** · **Trees**: node/leaf/height relations, traversals, reconstruction from two traversals; **BST** | P03 stacks/queues/LL |
| Sat 21 Nov | **P03 §10–12** · **AVL** rotations; **binary heaps** (array form, insert/delete, build-heap O(n)); graph representations, BFS/DFS · **GQ + SQ `Paper2_S05` — 60 Q** | P03 trees |
| Sun 22 Nov | **T04** + review | P03 RS · **P02 RS (1 wk)** |

**Paper-I:** English — idioms & phrases (10/day) · Quant — percentages, profit & loss · Reasoning — direction sense, ranking · GK — **Tripura culture, tribes, languages, festivals** (NP1 §10.4).

### Week 4 · 23–29 Nov · Algorithms (P04)
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 23 Nov | **P04 §1–2** · Asymptotic notations, growth-rate ordering; recurrences — substitution, recursion tree, **Master theorem** | P03 RS |
| Tue 24 Nov | **P04 §3, §4.1–4.2** · Searching (binary-search comparisons); comparison sorts — bubble/selection/insertion/merge/**quick**/heap; **build the complexity table from memory** | P04 recurrences |
| Wed 25 Nov | **P04 §4.3, §5** · Counting/radix/bucket sort, Ω(n log n) bound; **hashing** — chaining, linear/quadratic probing, double hashing, load factor | P04 sorting table |
| Thu 26 Nov | **P04 §6–7** · Divide & conquer; **greedy** — fractional knapsack, activity selection, **Huffman**, job sequencing, optimal merge | P04 hashing |
| Fri 27 Nov | **P04 §8** · **Dynamic programming** — 0/1 knapsack, **LCS**, **matrix-chain**, coin change, Floyd–Warshall | P04 greedy |
| Sat 28 Nov | **P04 §9–12** · Graph algorithms — BFS/DFS applications, topological sort, **Prim vs Kruskal**, **Dijkstra** (why negative edges break it), Bellman–Ford · **GQ + SQ `Paper2_S06` — 60 Q** | P04 DP |
| Sun 29 Nov | **T05** + review | P04 RS · **P03 RS (1 wk)** · **P01 RS (3 wk)** |

**Paper-I:** English — synonyms/antonyms (build a 300-word list over Weeks 4–9) · Quant — ratio, averages, ages, mixtures · Reasoning — syllogisms, Venn diagrams · GK — **Tripura economy, schemes, IT & connectivity** (NP1 §10.5).

### Week 5 · 30 Nov – 6 Dec · Operating Systems (P05)
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 30 Nov | **P05 §1–2** · OS types, kernel vs user mode, **system calls**, `fork()` counting; process states, PCB, context switch; **threads** (user vs kernel, models) | P04 RS |
| Tue 1 Dec | **P05 §6** · **CPU scheduling** — FCFS, SJF, SRTF, priority, **Round Robin**; Gantt charts → avg WT/TAT (do 6 numericals) | P05 processes |
| Wed 2 Dec | **P05 §3, §4.1–4.5** · IPC; critical section (3 requirements), Peterson, TSL; **semaphores**, mutex, monitors | P05 scheduling |
| Thu 3 Dec | **P05 §4.6, §5** · Producer–consumer, readers–writers, dining philosophers; **deadlock** — 4 conditions, RAG, prevention, **Banker's**, detection, recovery | P05 synchronisation |
| Fri 4 Dec | **P05 §7** · Memory: contiguous allocation, fragmentation; **paging** — page-table size, multilevel paging, **TLB & EAT**; segmentation | P05 deadlock |
| Sat 5 Dec | **P05 §8–10** · **Virtual memory** — page faults, **FIFO (Belady) / OPT / LRU** traces, thrashing, working set; file systems — allocation methods, inode max file size; **disk scheduling** · **GQ + SQ `Paper2_S08` — 60 Q** | P05 paging |
| Sun 6 Dec | **T06** + review | P05 RS · **P04 RS (1 wk)** · **P02 RS (3 wk)** |

**Paper-I:** English — sentence ordering & para-jumbles · Quant — time & work, pipes · Reasoning — seating arrangement & puzzles · GK — **Northeast India: all 8 states** (NP1 §11).

### Week 6 · 7–13 Dec · Databases (P06)
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 7 Dec | **P06 §1–2** · DBMS basics, 3-schema architecture, data independence; **ER model** (attributes, cardinality, participation, weak entities) & ER → table counts | P05 RS |
| Tue 8 Dec | **P06 §3, §6** · Relational model, **keys**, integrity constraints, referential actions; **relational algebra** (joins, division, result sizes) | P06 ER |
| Wed 9 Dec | **P06 §7–8** · Tuple/domain calculus; **SQL** — joins, GROUP BY/HAVING, aggregates & NULL, nested/correlated subqueries, EXISTS/ANY/ALL, views | P06 algebra |
| Thu 10 Dec | **P06 §4, §5.1–5.3, §5.7** · **FDs**, Armstrong's axioms, attribute closure, **candidate keys**, canonical cover; **1NF → BCNF** (+4NF) | P06 SQL |
| Fri 11 Dec | **P06 §5.4–5.6, §9** · Lossless-join & dependency-preserving decomposition; file organisation, indexing (dense/sparse, primary/clustering/secondary), **B / B+ tree order** | P06 normal forms |
| Sat 12 Dec | **P06 §10–12** · **Transactions** — ACID, schedules, **conflict serializability (precedence graph)**, view serializability, recoverable/cascadeless; **2PL** variants, timestamp ordering; recovery · **GQ + SQ `Paper2_S09` — 60 Q** | P06 indexing |
| Sun 13 Dec | **T07** + review | P06 RS · **P05 RS (1 wk)** · **P03 RS (3 wk)** |

**Paper-I:** English — reading comprehension (1 passage/day) · Quant — speed-time-distance, trains, boats · Reasoning — statement–assumption/conclusion · GK — **Indian history: ancient & medieval** (NP1 §12.1–12.2).

### Week 7 · 14–20 Dec · Computer Networks (P07)
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 14 Dec | **P07 §1–2** · **OSI vs TCP/IP** (functions, protocols, PDUs per layer); packet vs circuit vs virtual-circuit switching; delays; devices | P06 RS |
| Tue 15 Dec | **P07 §3–4** · DLL framing (byte/bit stuffing); **error detection** — parity, checksum, **CRC**, Hamming distance; **stop-and-wait / GBN / SR** | P07 layering |
| Wed 16 Dec | **P07 §5** · MAC — **ALOHA** efficiencies, **CSMA/CD minimum frame size**, CSMA/CA, Ethernet frame, backoff; bridging/STP | P07 DLL |
| Thu 17 Dec | **P07 §6–7** · **IPv4** header, classful & private ranges, **CIDR / subnetting / supernetting** (20 drills), **fragmentation** offsets; IPv6 basics | P07 MAC |
| Fri 18 Dec | **P07 §8–9** · Routing — **distance vector vs link state**, count-to-infinity, RIP/OSPF/BGP, flooding; ARP, DHCP, ICMP; NAT | P07 subnetting |
| Sat 19 Dec | **P07 §10–11** · **TCP vs UDP**, TCP header, handshake & teardown, sliding window, **congestion control** (slow start, AIMD, fast retransmit — trace cwnd); sockets; **DNS, SMTP/POP3/IMAP, HTTP, FTP**, ports table · **GQ + SQ `Paper2_S11` — 60 Q** | P07 routing |
| Sun 20 Dec | **T08** + review | P07 RS · **P06 RS (1 wk)** · **P04 RS (3 wk)** |

**Paper-I:** English — qualifying words, conjunctions, modifiers · Quant — simple & compound interest · Reasoning — clocks & calendars · GK — **modern Indian history & freedom struggle** (NP1 §12.3).

### Week 8 · 21–27 Dec · Compiler · Probability · Communication
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 21 Dec | **Compiler — P08 §1–3, §4.1–4.2:** phases & their outputs, compiler vs interpreter, linker/loader; lexical analysis (token counting); grammar background — ambiguity, left recursion, left factoring; **FIRST/FOLLOW** | P07 RS |
| Tue 22 Dec | **P08 §4.3, §5–6** · **LL(1)** table & conditions; shift-reduce; **LR(0) / SLR / LALR / CLR** hierarchy and conflicts; **SDT** (S- vs L-attributed) | P08 first half |
| Wed 23 Dec | **P08 §7–10** · Runtime environments (activation records, scoping, parameter passing); **3-address code, quadruples/triples, DAG**; basic blocks, local optimisation; **data-flow (liveness, reaching definitions, available expressions)** · **GQ + SQ `Paper2_S07` — 40 Q** | P08 parsing |
| Thu 24 Dec | **Probability — P09 §1–4:** axioms, conditional probability, independence, total probability, **Bayes**; counting; random variables, expectation, variance | P08 RS |
| Fri 25 Dec 🎄 *(holiday — long day if free)* | **P09 §5–7:** **five distributions** (uniform, normal, exponential, Poisson, binomial), mean/median/mode/SD · **`Paper2_S01` — 40 Q** · then **Communication (N09 §1–2):** random signals, autocorrelation/PSD, white noise, **AM**, superheterodyne & image frequency | P09 Bayes |
| Sat 26 Dec | **Communication (N09 §3–5.3):** FM/PM & Carson's rule, **information theory** (entropy, mutual information, Shannon capacity), sampling, quantisation, PCM/DPCM/DM | P09 RS |
| Sun 27 Dec | N09 §5.4–5.8: **ASK/FSK/PSK/QAM**, MAP/ML, matched filter, BER, ISI & Nyquist, Hamming codes, **TDMA/FDMA/CDMA** · SQ `Paper2_S04` — 40 Q · **T09** (Comm + Prob) + review | N09 §10 rapid-fire · **P07 RS (1 wk)** · **P05 RS (3 wk)** |

**Paper-I:** English — one-word substitution, confusing word pairs · Quant — permutations & combinations, probability, number system · Reasoning — data sufficiency · GK — **Indian geography** (NP1 §13).

### Week 9 · 28 Dec – 3 Jan · Software Engg · Web · Cloud · Cyber Security
| Day | Paper-II block | Revise |
|---|---|---|
| Mon 28 Dec | **IS & SE (N11 §1–2):** fact-finding, requirements & SRS, feasibility, **DFDs** (levels, balancing), data dictionary, decision tables | N09 §10 + §11 traps |
| Tue 29 Dec | N11 §3–4: process models (waterfall, spiral, prototyping, RAD, V, **Agile/Scrum**), **FP & COCOMO**, PERT/CPM critical path, risk | N11 §1–2 |
| Wed 30 Dec | N11 §5–7: **cohesion & coupling order**, **cyclomatic complexity**, testing (black/white box, BVA, levels, stubs/drivers), maintenance types, CMM · SQ `Paper2_S10` — 50 Q · **T11** (SE + Compiler) + review | N11 §3–4 · **P08 RS (1 wk)** |
| Thu 31 Dec | **Web (N10 §1–5):** HTML5, CSS3 (specificity, box model), XML (well-formed vs valid, DTD vs XSD), client–server tiers, web/app/**proxy** servers, **MVC** | N11 §5–7 |
| Fri 1 Jan 🎆 *(holiday — long day if free)* | N10 §6–7: **SOAP vs REST**, JS/DOM/AJAX, sessions/cookies/JWT · SQ `Paper2_S12` — 30 Q · **Cloud (N10 §8–10):** NIST characteristics, **IaaS/PaaS/SaaS**, deployment models, hypervisors, VMs vs containers, storage types, **edge computing** · SQ `Paper2_S14` | N10 Web rapid-fire |
| Sat 2 Jan | **Cyber & emerging (N10 §11–16):** secure programming, **OWASP Top 10**, SQLi/XSS/CSRF, symmetric vs asymmetric, hashing, PKI, attacks; **IoT**, **blockchain**, **AI/ML** · SQ `Paper2_S13` — 40 Q | N10 Cloud rapid-fire |
| Sun 3 Jan | **T10** (Web + Cloud + Cyber) + review | N10 §17–18 · **P09 RS** · **P06 RS (3 wk)** |

**Paper-I:** English — mixed error-spotting sets · Quant — mensuration, data interpretation · Reasoning — mixed sets · GK — **Indian polity & economy; S&T and IT policy** (NP1 §14; DPDP Act 2023, IndiaAI, Digital India, UPI/ONDC).

### Week 10 · 4–10 Jan · Repair + Full Mocks A & B
| Day | Plan |
|---|---|
| Mon 4 Jan | **Repair 1:** read the whole error log · redo every wrong PYQ from §5/§6 · RS **P03 + P04** (6 wk) |
| Tue 5 Jan | **Repair 2:** RS **P05 + P06** · 40 mixed OS/DBMS PYQs you haven't seen |
| Wed 6 Jan | **Repair 3:** RS **P07 + P02 + P01** · 40 mixed CN/COA/DL PYQs |
| Thu 7 Jan | **Full Mock A** (state-PSC calibrated — see [blueprint](../04_Mock_Tests/Full_Length_Mock_Blueprint.md); the Kerala PSC 2026 paper is the ready-made option) · 3 h, OMR sheet, then score both papers separately |
| Fri 8 Jan | Mock A **review** (2 h) · repair the two weakest sections · Paper-I hour as usual |
| Sat 9 Jan | **Full Mock B** (mixed) in the morning · review in the afternoon · repair |
| Sun 10 Jan | **Paper-I day:** full pass of Tripura + NE GK (NP1 §10–11) · current-affairs notebook, Jan 2026 → now · English rules (P10 Part C) · 2 timed reasoning sets · **T12** (mixed) in the evening |

### Week 11 · 11–17 Jan · Mock C + final revision
| Day | Plan |
|---|---|
| Mon 11 Jan | Repair from Mock B · rapid-fire tables + traps for **§4, §10, §12, §13, §14** (N09, N10, N11) — the easiest marks in the paper |
| Tue 12 Jan | **Full Mock C** (GATE-weighted stress test) · score |
| Wed 13 Jan | Mock C review · RS **P03, P04, P05** |
| Thu 14 Jan | RS **P06, P07, P02, P01** · read the full error log once |
| Fri 15 Jan | RS **P08, P09, P10** · [N12](../05_Notes/Week_12_Formula_Sheets_and_Revision.md) master formula sheet · last GK pass: Tripura, NE, last 3 months of current affairs |
| Sat 16 Jan | **Light day (≤ 4 h):** N12 "Final 48 hours" · error log skim · pack admit card, photo ID, pens · check route & reporting time · sleep early |
| **Sun 17 Jan** | **EXAM** — arrive 60+ min early |

---

## 5. Paper-I track at a glance

English and reasoning/quant sections are in **[P10](10_General_Ability_Aptitude_English.md)**; GK sections are in **NP1** Part C.

| Week | English (20 min) | Reasoning / Quant (20 min) | GK & current affairs (20 min) |
|---|---|---|---|
| 1 | Articles, prepositions — **P10 §25–26** | Series, analogy — **§15** | Tripura basics & geography — NP1 §10.1–10.2 |
| 2 | Subject–verb agreement, tenses — **§22–23** | Coding–decoding, blood relations — **§16–17** | Tripura history — NP1 §10.3 |
| 3 | Idioms & phrases — **§27** | Direction, ranking — **§18–19** · %, profit & loss — **§3** | Tripura culture, tribes, languages — NP1 §10.4 |
| 4 | Synonyms / antonyms list — **§29** | Syllogism, Venn — **§20–21** · ratio, averages, mixtures — **§5–7** | Tripura economy, schemes — NP1 §10.5 |
| 5 | Sentence & para ordering — **§30** | Seating, puzzles — **§19** · time & work — **§8** | Northeast India (8 states) — NP1 §11 |
| 6 | Comprehension — **§30** | Statement–conclusion — **§21** · TSD, trains, boats — **§9–10** | Indian history, ancient/medieval — NP1 §12.1–12.2 |
| 7 | Qualifying words, conjunctions — **§24** | Clocks & calendars — **§12** · SI/CI — **§4** | Modern history, freedom struggle — NP1 §12.3 |
| 8 | One-word substitution, confusables — **§28–29** | Data sufficiency — **§21** · number system, P&C — **§1, §11** | Indian geography — NP1 §13 |
| 9 | Mixed error spotting — **§22–24** | HCF/LCM — **§2** · mensuration, DI — **§13–14** | Polity, economy, S&T, IT policy — NP1 §14 |
| 10 | Timed mixed sets | Timed mixed sets | **Current-affairs consolidation** — NP1 §15 |
| 11 | P10 revision sheet only | Light sets | Tripura + NE + last 3 months |

Every day: **10 new words/idioms** into a notebook (re-read on Sundays) and **15 timed reasoning/quant questions** from `Paper1_02_*`. Keep a one-line-per-day current-affairs notebook with emphasis on **Tripura, the Northeast and IT/technology**.

---

## 6. Targets and checkpoints

| When | Check | Target | If you miss it |
|---|---|---|---|
| Every Sunday | Weekly test | **≥ 18 / 25** | Re-read that week's RS + redo wrong PYQs in Monday's 🅲 slot |
| Sun 6 Dec (end Wk 5) | Paper-I share of tests so far | ≥ 3 / 5 average | Move 30 min/day from 🅰 to Paper-I until it recovers |
| Thu 7 Jan | Mock A | P-I ≥ **32**, P-II ≥ **75** | Push §5/§6/§8/§9/§11 in Mon 11 Jan's repair slot |
| Tue 12 Jan | Mock C (harder than the real paper) | P-II ≥ **66** | Stop learning new detail; revise RS files and rapid-fire tables only |

Log every score in [Weekly_Progress_Tracker.md](../01_Study_Plan/Weekly_Progress_Tracker.md). Track **silly errors** and **concept gaps** separately — only concept gaps need re-study.

---

## 7. If you fall behind

Sunday afternoons and the two holidays (25 Dec, 1 Jan) are your buffer. If you are more than two days behind, cut in this order — **never cut the Paper-I hour or a weekly test**:

1. **Drop first:** Compiler optimisation/data-flow detail, Communication derivations, anything in P09 beyond Bayes + the five distributions.
2. **Compress next:** do Web + Cloud in one day (Thu 31 Dec), and Software Engg in two (Mon–Tue 28–29 Dec).
3. **Protect at all costs:** Programming & DS, Algorithms, OS, DBMS, CN (~58 marks), plus the ~31 easy marks of §4/§10/§12/§13/§14 from their rapid-fire tables.

If the exam moves **later**, insert the extra days into Week 10 as more repair + one more full mock. If it moves **earlier**, shorten Week 10 first, never Week 11's taper.

---

## 8. Exam day (from the advertisement)

- The venue **closes 10 minutes before the start** — no exceptions. Arrive 60+ minutes early.
- **No mobile phone or electronic device anywhere on campus** (possession can mean debarment).
- **No jacket, coat or pullover** in the hall — in mid-January in Tripura, wear a warm full-sleeve shirt instead.
- Answers in English only; OMR — **check the question number against the OMR row every 10 questions**.
- Time plan (rehearsed in the mocks): Paper-I 40 min → Paper-II quick questions 80 min → flagged numericals 45 min → OMR check + calculated guesses 15 min.
- Guessing rule at −1/3: attempt only if you can eliminate at least two options.

Full detail: [12_Week_Study_Plan.md §8](../01_Study_Plan/12_Week_Study_Plan.md#8-exam-day-mechanics).
