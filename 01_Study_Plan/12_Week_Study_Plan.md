# TPSC Assistant Technical Officer (IT) — 12-Week Study Plan

**Exam:** Assistant Technical Officer, Group-B Gazetted — Department of Industries & Commerce (Information Technology), Govt. of Tripura
**Advertisement:** TPSC Advt. No. 02/2026, dated 27/04/2026 — **220 posts**
**Selection:** Written 170 marks (MCQ, OMR, 3 hours) + Interview/Personality Test 30 marks = 200
**Plan window:** Mon **07 Sep 2026** → Sun **29 Nov 2026** (12 weeks)

> **Status note.** The application window (12 May – 05 Jun 2026) has closed, and the advertisement does not fix a written-exam date. This plan therefore assumes the written exam falls **on or after early December 2026**. If TPSC announces an earlier date, use the compression rules in [§9](#9-if-your-timeline-shrinks).

---

## 1. The two numbers that decide everything

| | Paper-I (GAT) | Paper-II (Technical) |
|---|---|---|
| Questions | 50 × 1 mark | 120 × 1 mark |
| Time | 180 minutes, **combined** | |
| **UR qualifying (55% *each subject*)** | **27.5 / 50** | **66 / 120** |
| **SC/ST/PH qualifying (45% *each subject*)** | **22.5 / 50** | **54 / 120** |

Two consequences that should shape every week of your prep:

1. **Paper-I can eliminate you on its own.** Clause (b) on page 2 of the advertisement sets the minimum **in each subject**, not on the aggregate. A 100/120 in Paper-II does not rescue a 25/50 in Paper-I. Engineers routinely under-prepare the GK/Tripura portion and get filtered out here. Paper-I gets a **non-negotiable daily slot** in this plan, all 12 weeks.
2. **Negative marking applies** (Annexure-B, Part-II, clause v: "Negative Marking on MCQ question (for wrong answer) will remain as per TPSC norms"). TPSC has not published the ratio in this advertisement; **assume 1/3** and plan your guessing accordingly. See [§8](#8-exam-day-mechanics).

Only **3× the number of vacancies** are called for interview, category-wise. With 220 posts that is a wide net — but the qualifying cut-offs above are the real gate.

---

## 2. Estimated weightage (Paper-II, 120 marks)

TPSC has **not** published a section-wise breakup. The following is my estimate, derived from the syllabus ordering in Annexure-C and from how comparable state-PSC / PSU technical papers distribute marks. **Treat it as a planning aid, not a fact.**

| # | Section | Est. marks | Priority |
|---|---|---|---|
| 5 | Data Structures & Programming (C, C++, Java, recursion) | ~14 | 🔴 Highest |
| 6 | Algorithms | ~11 | 🔴 Highest |
| 8 | Operating System | ~11 | 🔴 Highest |
| 9 | Databases | ~11 | 🔴 Highest |
| 11 | Computer Networks | ~11 | 🔴 Highest |
| 2 | Digital Logic | ~9 | 🟠 High |
| 3 | Computer Organization & Architecture | ~9 | 🟠 High |
| 4 | Analog & Digital Communication | ~8 | 🟠 High |
| 10 | Information Systems & Software Engineering | ~8 | 🟠 High |
| 1 | Probability & Statistics | ~7 | 🟡 Medium |
| 7 | Compiler Design | ~6 | 🟡 Medium |
| 12 | Web Technologies | ~6 | 🟡 Medium |
| 13 | Cyber Security & Emerging Technologies | ~5 | 🟡 Medium |
| 14 | Cloud Technology | ~4 | 🟡 Medium |
| | **Total** | **120** | |

**Paper-I (50 marks) is fixed by the advertisement:** English 15, General Mental Ability & Logical Reasoning 15, General Knowledge & Current Affairs 20.

### Two scope decisions worth money

- **Theory of Computation is NOT in the syllabus.** Annexure-C lists no automata, regular languages, or decidability section. If you are working from GATE material, **skip the ToC chapter entirely** — that is roughly 293 GATE questions you do not need. (It is filed under `ZZ_Outside_TPSC_Syllabus_optional` for exactly this reason.) The only grammar you need is the parsing background inside Compiler Design.
- **Engineering Mathematics is only Probability & Statistics.** Section 1 lists random variables, distributions, mean/median/mode/SD, conditional probability and Bayes. **Linear algebra, calculus and discrete mathematics are out of scope.** Do not spend a week on matrices and eigenvalues.

Conversely, five sections have **no GATE coverage at all** and are easy to neglect: Analog & Digital Communication (4), Information Systems & Software Engineering (10), Web Technologies (12), Cyber Security & Emerging Tech (13), Cloud Technology (14). That is **~31 marks — a quarter of Paper-II.** They are also the *easiest* marks in the paper, because the questions are definitional rather than analytical. Weeks 9–11 are built around them.

---

## 3. Weekly time budget

The default assumes you are working full-time.

| | Weekday (Mon–Fri) | Saturday | Sunday | Week total |
|---|---|---|---|---|
| Paper-II (core subject) | 2.5 h | 5 h | 3 h | ~20.5 h |
| Paper-I (daily, non-negotiable) | 1.0 h | 1 h | 1 h | ~7 h |
| Revision of previous weeks | 0.5 h | 1 h | 1 h | ~4.5 h |
| **Weekly test + review** | — | — | 2 h | 2 h |
| **Total** | **4 h** | **7 h** | **7 h** | **~34 h** |

**The 1-hour daily Paper-I slot is the single highest-ROI habit in this plan.** Split it: 20 min English, 20 min reasoning/aptitude, 20 min GK + current affairs. Do it at a fixed time; do not let Paper-II bleed into it.

---

## 4. Recurring weekly rhythm

| Day | Focus |
|---|---|
| **Mon–Wed** | New concepts for the week's subject + worked examples — read that week's file in [`05_Notes/`](../05_Notes/), copying every formula table into a notebook by hand |
| **Thu** | PYQ drilling: the week's subject from `03_GATE_CSE_PYQs/Subject_wise/` |
| **Fri** | PYQ drilling: the week's subject from `02_State_PSC_PYQs/Subject_wise/` (state-PSC/ISRO/NIELIT/UGC-NET level — closer to the actual difficulty of this paper) |
| **Sat** | Deep-work block: weak sub-topics + formula/one-liner sheet for the subject |
| **Sun AM** | **Weekly Mock Test** — `04_Mock_Tests/Week_XX_Test.md`, timed, no notes |
| **Sun PM** | Test review + spaced revision of all earlier weeks |

**Rule: never mark a week "done" until its mock test is attempted under timing and reviewed.** The review is worth more than the attempt.

---

## 5. The 12 weeks

### Week 1 — Digital Logic + Number Systems
**Mon 07 Sep – Sun 13 Sep 2026** · Syllabus §2 · *~9 marks*

- Number representations: unsigned, signed magnitude, 1's & 2's complement, ranges, overflow detection
- Fixed-point and **IEEE-754 floating point** (single/double precision, bias, normalization) — a perennial favourite
- Boolean algebra, De Morgan, canonical SOP/POS, minterms/maxterms
- **K-map minimisation** up to 5 variables, don't-cares, prime implicants; Quine–McCluskey (awareness level)
- Combinational: multiplexer/demux, encoder/decoder (incl. priority encoder), comparators, implementing functions using MUX
- Adders: half/full, ripple-carry, **carry look-ahead** (propagate/generate, delay counting)
- Sequential: SR/JK/D/T flip-flops, excitation tables, race-around and master-slave
- Counters (ripple, synchronous, mod-N), shift registers, ring/Johnson counters
- Finite state machines: Mealy vs Moore, state-table → circuit

**Deliverable:** a one-page sheet of gate counts, flip-flop excitation tables and IEEE-754 layout.
**Test:** `04_Mock_Tests/Week_01_Test.md`

---

### Week 2 — Computer Organization & Architecture
**Mon 14 Sep – Sun 20 Sep 2026** · Syllabus §3 · *~9 marks*

- Machine instructions and **addressing modes** (immediate, direct, indirect, indexed, base+offset, auto-increment) — know the effective-address computation cold
- Instruction formats, RISC vs CISC, register organisation
- ALU design, data path and control unit: **hardwired vs microprogrammed** control, horizontal/vertical microinstructions
- **Instruction pipelining:** stages, speedup/efficiency/throughput formulas, ideal vs actual CPI
- **Pipeline hazards:** structural, data (RAW/WAR/WAW), control; operand forwarding, stalls, branch prediction, delay slots
- Memory hierarchy: **cache** — direct-mapped, set-associative, fully associative; tag/index/offset splitting; hit ratio; **average memory access time**; write-through vs write-back; replacement policies (LRU, FIFO, optimal)
- Main memory organisation, interleaving; secondary storage (disk geometry, access time = seek + rotational latency + transfer)
- **I/O:** programmed I/O, interrupt-driven I/O, **DMA** (cycle stealing vs burst)

**Highest-yield sub-topics:** cache address splitting, AMAT, pipeline speedup, addressing modes. Expect at least one numerical.
**Test:** `04_Mock_Tests/Week_02_Test.md`

---

### Week 3 — Programming in C, C++, Java & OOP
**Mon 21 Sep – Sun 27 Sep 2026** · Syllabus §5 (part) · *~7 of the ~14 DS&Prog marks*

- C: data types, storage classes (`auto`/`static`/`extern`/`register`), scope & lifetime
- **Pointers** — pointer arithmetic, pointer-to-pointer, arrays vs pointers, function pointers, `void*`
- Arrays (1-D/2-D), row-major vs column-major **address calculation**, strings
- Structures, unions, bit-fields; `sizeof` and padding
- Functions: call by value vs reference, **recursion** — trace-the-output questions, tail recursion, recursion vs iteration
- Dynamic memory: `malloc`/`calloc`/`realloc`/`free`, dangling pointers, memory leaks
- Operator precedence/associativity, type promotion, pre/post increment traps
- **OOP concepts:** class/object, encapsulation, abstraction, **inheritance** (types), **polymorphism** (compile-time vs run-time), virtual functions & vtable, abstract classes, overloading vs overriding
- Java specifics: JVM/JRE/JDK, bytecode, garbage collection, `final`/`finally`/`finalize`, interfaces vs abstract classes, exception hierarchy, `String` immutability, access modifiers

**Note:** State-PSC papers ask far more **Java and OOP definitional** questions than GATE does. Give the ISRO/NIELIT/UGC-NET Java and OOP PDFs real time — they are in `02_State_PSC_PYQs/Subject_wise/Paper2_S05_.../`.
**Test:** `04_Mock_Tests/Week_03_Test.md`

---

### Week 4 — Data Structures
**Mon 28 Sep – Sun 04 Oct 2026** · Syllabus §5 (part) · *~7 of the ~14 DS&Prog marks*

- Arrays, **stacks** (infix→postfix/prefix, expression evaluation, balanced parentheses), **queues** (circular, deque, priority queue)
- **Linked lists:** singly, doubly, circular; insert/delete/reverse; floating-point-free pointer manipulation questions
- **Trees:** terminology, height/depth/level, number of nodes/leaves relations, binary tree properties
- Traversals — inorder, preorder, postorder, level-order; **reconstructing a tree from two traversals**
- **Binary Search Trees:** search/insert/delete, successor/predecessor, worst vs average height
- Balanced trees: AVL (rotations LL/RR/LR/RL), awareness of red-black and B/B+ trees (B+ trees also recur in DBMS indexing)
- **Binary heaps:** build-heap, heapify, insert/extract-min complexity, heap-sort, array representation, `heapify` cost = O(n)
- **Graphs:** adjacency matrix vs list (space/time trade-offs), BFS/DFS and their trees, connected components, cycle detection, topological sort
- Hashing: hash functions, **collision resolution** (chaining, linear/quadratic probing, double hashing), load factor, clustering

**Test:** `04_Mock_Tests/Week_04_Test.md`

---

### Week 5 — Algorithms
**Mon 05 Oct – Sun 11 Oct 2026** · Syllabus §6 · *~11 marks*

- Asymptotic notation: **O, Ω, Θ, o, ω**; comparing growth rates; worst/average/best case
- **Recurrence relations:** substitution, recursion tree, **Master theorem** (all three cases + when it does not apply)
- **Searching:** linear, binary search (iterative/recursive, number of comparisons)
- **Sorting:** bubble, selection, insertion, merge, quick (pivot choice, worst case), heap, counting/radix/bucket; **stability**, in-place property, comparison-based lower bound Ω(n log n)
- **Divide & conquer:** merge sort, quick sort, binary search, Strassen (awareness)
- **Greedy:** fractional knapsack, activity selection, **Huffman coding**, job sequencing; why greedy fails for 0/1 knapsack
- **Dynamic programming:** 0/1 knapsack, LCS, matrix chain multiplication, coin change, Floyd–Warshall; optimal substructure & overlapping subproblems
- **Graph algorithms:** BFS/DFS applications, **MST — Prim & Kruskal** (and their complexities), **shortest paths — Dijkstra** (why not with negative edges), **Bellman–Ford**, Floyd–Warshall
- Hashing complexity; awareness of P, NP, NP-complete, NP-hard (definitional only)

**This is the highest-density week.** Expect direct complexity-table questions — memorise the table of best/average/worst for all sorts and graph algorithms.
**Test:** `04_Mock_Tests/Week_05_Test.md`

---

### Week 6 — Operating Systems
**Mon 12 Oct – Sun 18 Oct 2026** · Syllabus §8 · *~11 marks*

- OS functions, types (batch, multiprogramming, time-sharing, real-time, distributed); **system calls**, user vs kernel mode
- **Processes:** PCB, process states & transitions, context switching; **threads** — user vs kernel level, multithreading models
- **CPU scheduling:** FCFS, SJF, SRTF, priority, **Round Robin**, multilevel queue/feedback; compute **average waiting time & turnaround time** from Gantt charts; convoy effect, starvation, aging
- **IPC:** shared memory vs message passing, pipes
- **Synchronisation:** critical section and its 3 requirements, Peterson's solution, **semaphores** (binary/counting), mutex, monitors; classical problems — **producer–consumer, readers–writers, dining philosophers**
- **Deadlock:** 4 necessary conditions, resource-allocation graph, prevention, avoidance (**Banker's algorithm** — work through it numerically), detection, recovery
- **Memory management:** contiguous allocation, first/best/worst fit, internal vs external fragmentation, compaction; **paging** (page table, TLB, effective access time), **segmentation**, segmented paging
- **Virtual memory:** demand paging, **page-fault handling**, page-replacement algorithms — FIFO (and **Belady's anomaly**), Optimal, LRU, clock; thrashing, working set
- **File systems:** file allocation (contiguous, linked, indexed), directory structures, inodes, free-space management; disk scheduling — FCFS, SSTF, SCAN, C-SCAN, LOOK

**Numerical-heavy.** Practise Gantt charts, page-replacement traces and Banker's algorithm until they are mechanical.
**Test:** `04_Mock_Tests/Week_06_Test.md`

---

### Week 7 — Databases
**Mon 19 Oct – Sun 25 Oct 2026** · Syllabus §9 · *~11 marks*

- DBMS vs file system, 3-level architecture, data independence, DBA roles
- **ER model:** entities, attributes (composite/derived/multivalued), relationships, cardinality, participation, weak entities, **ER → relational mapping**
- **Relational model:** relations, keys — super/candidate/primary/foreign/composite; **integrity constraints** (entity, referential, domain)
- **Relational algebra:** σ, π, ×, ⋈ (natural/theta/outer), ∪, −, ÷; **tuple & domain relational calculus**
- **SQL:** DDL/DML/DCL/TCL, joins (inner/left/right/full), **GROUP BY + HAVING**, aggregate functions, nested & correlated subqueries, `EXISTS`/`IN`/`ANY`/`ALL`, views, `NULL` semantics (a classic trap)
- **Normalisation:** functional dependencies, **Armstrong's axioms**, attribute closure, finding candidate keys, canonical cover; **1NF, 2NF, 3NF, BCNF**, 4NF/multivalued dependencies; **lossless-join and dependency-preserving decomposition**
- **File organisation & indexing:** heap/sequential/hash files; **B-tree and B+-tree** (order, insertion/deletion, why B+ for DB indexing); primary/secondary/clustered/dense/sparse indexes
- **Transactions:** ACID, schedules, **conflict serializability & precedence graphs**, view serializability, recoverable/cascadeless schedules
- **Concurrency control:** **2-phase locking** (basic/strict/rigorous), lock compatibility, deadlock in DBMS, timestamp ordering; log-based recovery, checkpoints

**Highest-yield:** normalisation/candidate keys, conflict serializability, SQL output questions, B+ tree order calculations.
**Test:** `04_Mock_Tests/Week_07_Test.md`

---

### Week 8 — Computer Networks
**Mon 26 Oct – Sun 01 Nov 2026** · Syllabus §11 · *~11 marks*

- **Layering:** OSI 7 layers vs TCP/IP stack — functions and protocols **per layer** (rote-learn this; it is asked directly)
- Switching: **packet vs circuit vs virtual-circuit**, store-and-forward, transmission vs propagation delay
- **Data link layer:** framing (character/bit stuffing), **error detection — parity, checksum, CRC**, Hamming distance & error correction; flow control — stop-and-wait, **Go-Back-N, Selective Repeat** (window sizes, efficiency, sequence-number bits)
- **MAC:** ALOHA (pure/slotted, efficiency 18.4%/36.8%), **CSMA/CD** and minimum frame size, CSMA/CA, Ethernet frame format, bridges, switches, collision vs broadcast domains
- **Network layer:** **IPv4 header**, **classful vs CIDR**, **subnetting & supernetting** (drill this hard), fragmentation (MTU, offset, flags), IPv6 basics
- Routing: shortest path (**Dijkstra**), flooding, **distance vector** (count-to-infinity, split horizon), **link state**, RIP/OSPF/BGP; **NAT**
- Support protocols: **ARP, RARP, DHCP, ICMP**
- **Transport layer:** UDP vs TCP, **TCP header**, 3-way handshake & connection teardown, sequence/ack numbers, **flow control (sliding window)**, **congestion control — slow start, AIMD, congestion avoidance, fast retransmit/recovery**; sockets, ports
- **Application layer:** **DNS** (hierarchy, iterative vs recursive, record types), **SMTP/POP3/IMAP**, **HTTP** (methods, status codes, persistent vs non-persistent, HTTPS), **FTP** (control vs data connection)

**Subnetting and CIDR are the single most reliably-asked topic in this section.** Be able to compute network address, broadcast address, usable hosts and subnet mask in under 30 seconds.
**Test:** `04_Mock_Tests/Week_08_Test.md`

---

### Week 9 — Analog & Digital Communication + Probability & Statistics
**Mon 02 Nov – Sun 08 Nov 2026** · Syllabus §4 and §1 · *~8 + ~7 = ~15 marks*

**Communication (Mon–Thu)** — this is an *ECE* section inside a CS paper. Most CS graduates skip it; ~8 marks is too many to donate. Aim for definitional and formula-level mastery, not derivations.
- Random signals: **autocorrelation and power spectral density**, properties of **white noise**, filtering of random signals through LTI systems
- **Amplitude modulation:** AM, DSB-SC, SSB; modulation index, power and bandwidth of AM; envelope vs coherent detection
- **Angle modulation:** FM and PM, frequency deviation, modulation index, **Carson's rule** bandwidth; narrowband vs wideband FM
- **Superheterodyne receiver:** block diagram, IF, image frequency
- **Information theory:** self-information, **entropy**, mutual information, **channel capacity** (Shannon–Hartley `C = B log₂(1 + S/N)`), source coding
- **Digital communication:** sampling theorem & Nyquist rate, quantisation and quantisation noise, **PCM, DPCM**, delta modulation
- **Digital modulation:** **ASK, FSK, PSK (BPSK/QPSK), QAM, MAP and ML decoding**, matched filter receiver, **bandwidth/SNR/BER** relationships
- **Error correction:** parity, **Hamming codes** (syndrome decoding, `2^r ≥ m+r+1`), block codes
- Timing & frequency synchronisation, **inter-symbol interference (ISI)** and mitigation (pulse shaping, equalisation, Nyquist criterion)
- **Multiple access: TDMA, FDMA, CDMA** basics

**Probability & Statistics (Fri–Sun)** — the entirety of "Engineering Mathematics" in this syllabus.
- Random variables (discrete/continuous), PMF/PDF/CDF, expectation and variance, linearity of expectation
- **Distributions: uniform, normal, exponential, Poisson, binomial** — mean, variance and when each applies
- **Mean, median, mode, standard deviation**; grouped data
- **Conditional probability, independence, total probability, and Bayes' theorem** — Bayes is asked almost every time

**Test:** `04_Mock_Tests/Week_09_Test.md`

---

### Week 10 — Web Technologies + Cloud Technology + Cyber Security & Emerging Tech
**Mon 09 Nov – Sun 15 Nov 2026** · Syllabus §12, §14, §13 · *~6 + ~4 + ~5 = ~15 marks*

These three are **pure scoring sections** — definitional, no numericals, and directly relevant to the Directorate of IT's actual work. Do not treat them as filler.

**Web Technologies (Mon–Tue)**
- **HTML5:** semantic elements, forms & input types, canvas, audio/video, local vs session storage, doctype
- **CSS3:** selectors and specificity, box model, positioning, flexbox/grid, media queries, responsive design
- **XML:** well-formed vs valid, DTD vs XSD, XSLT, XPath; XML vs JSON
- **Client–server computing:** thin vs thick clients, 2-tier vs 3-tier vs n-tier architecture
- **Web server vs application server vs proxy server** (forward vs reverse proxy, caching)
- **MVC architecture** — model, view, controller responsibilities; MVC vs MVP vs MVVM
- **Web services:** SOAP vs REST, WSDL, UDDI, HTTP verbs and REST constraints, statelessness, JSON payloads, API basics
- **Frontend technologies:** JavaScript fundamentals, DOM, AJAX, jQuery, awareness of React/Angular/Vue; session vs cookie, JWT

**Cloud Technology (Wed–Thu)**
- **Service models: IaaS, PaaS, SaaS** (and who manages what — a guaranteed question) plus FaaS/serverless
- **Deployment models:** public, private, hybrid, community cloud
- Essential characteristics (NIST): on-demand self-service, broad network access, resource pooling, rapid elasticity, measured service
- **Virtualisation:** hypervisors type-1 vs type-2, VMs vs **containers/Docker**, orchestration (Kubernetes) at awareness level
- **Compute, network and storage management:** block vs file vs object storage, load balancing, auto-scaling, CDN
- Cloud migration, SLA, multi-tenancy, vendor lock-in
- **Edge computing:** definition, latency motivation, edge vs fog vs cloud, use cases
- Government context: MeghRaj / NIC cloud, data localisation

**Cyber Security & Emerging Technologies (Fri–Sun)**
- **Secure programming:** input validation, output encoding, parameterised queries, least privilege, secure defaults, buffer overflow, race conditions
- **OWASP Top 10** — learn all ten by name and one-line description (**Broken Access Control, Cryptographic Failures, Injection, Insecure Design, Security Misconfiguration, Vulnerable & Outdated Components, Identification & Authentication Failures, Software & Data Integrity Failures, Security Logging & Monitoring Failures, SSRF**). Understand **SQL injection and XSS** properly.
- Cryptography basics: symmetric vs asymmetric, DES/AES, RSA, hashing (MD5/SHA), digital signatures, PKI & certificates, SSL/TLS
- Attacks: phishing, MITM, DoS/DDoS, ransomware, privilege escalation; firewalls, IDS/IPS, VPN
- **IoT:** architecture layers (perception/network/application), sensors & actuators, protocols (MQTT, CoAP, Zigbee, BLE), IoT security concerns
- **Blockchain:** distributed ledger, blocks & hash chaining, consensus (PoW, PoS), smart contracts, permissioned vs permissionless, immutability
- **AI:** AI vs ML vs deep learning, supervised/unsupervised/reinforcement learning, neural network basics, common applications; Indian AI/IT policy awareness (IT Act 2000, DPDP Act 2023, CERT-In)

**Test:** `04_Mock_Tests/Week_10_Test.md`

---

### Week 11 — Information Systems & Software Engineering + Compiler Design
**Mon 16 Nov – Sun 22 Nov 2026** · Syllabus §10 and §7 · *~8 + ~6 = ~14 marks*

**IS & Software Engineering (Mon–Thu)** — another zero-GATE-overlap, high-scoring section. ISRO/NIELIT/UGC-NET have ~340 questions here; use them.
- **Information gathering:** interviews, questionnaires, observation, record review
- **Requirement analysis:** functional vs non-functional requirements, **SRS** and its characteristics; **feasibility analysis** — technical, economic, operational, schedule, legal
- **Data flow diagrams:** context diagram (level 0), levelling, balancing rules, Gane–Sarson vs Yourdon symbols; process specifications, decision tables and decision trees, data dictionary
- Input/output design, form design, code design
- **Process life-cycle models:** waterfall, prototyping, incremental, **spiral (risk-driven)**, RAD, V-model, **Agile/Scrum** (sprints, backlog, roles), DevOps awareness
- **Planning & estimation:** LOC vs **function points**, **COCOMO** (basic/intermediate; organic/semi-detached/embedded), **Gantt & PERT/CPM**, critical path, risk management
- **Design:** modularity, **cohesion (7 types) and coupling (6 types)** — know the best-to-worst ordering, it is asked directly; abstraction, information hiding, architectural styles
- **Testing:** unit/integration/system/acceptance; **black-box (equivalence partitioning, boundary value analysis, cause-effect) vs white-box (statement/branch/path coverage, cyclomatic complexity = E − N + 2)**; alpha vs beta; regression testing; top-down vs bottom-up integration, stubs & drivers
- **Implementation & maintenance:** deployment strategies (direct, parallel, phased, pilot); maintenance types — **corrective, adaptive, perfective, preventive**; software quality — ISO 9126, **CMM levels 1–5**, SQA

**Compiler Design (Fri–Sun)**
- Compiler **phases** and their inputs/outputs; front end vs back end; passes; symbol table
- **Lexical analysis:** tokens/lexemes/patterns, regular expressions → DFA, `lex`, longest-match rule
- **Parsing:** CFGs, derivations, parse trees, **ambiguity**, left recursion elimination, left factoring
  - **Top-down:** recursive descent, **LL(1)** — **FIRST and FOLLOW sets**, parsing table construction and conflict detection
  - **Bottom-up:** shift-reduce, handles, **LR(0), SLR(1), CLR(1), LALR(1)** — the power hierarchy and typical conflict questions
- **Syntax-directed translation:** synthesised vs inherited attributes, S-attributed and L-attributed definitions, annotated parse trees
- **Intermediate code:** three-address code, quadruples/triples/indirect triples, syntax trees, DAG representation
- **Runtime environments:** activation records, static vs dynamic scoping, stack vs heap allocation, parameter passing (call by value/reference/name/value-result)
- **Code optimisation:** basic blocks & flow graphs, **local optimisation**, constant folding & **constant propagation**, common subexpression elimination, dead code elimination, strength reduction, loop optimisations
- **Data flow analysis:** reaching definitions, **liveness analysis**, available expressions; the general data-flow framework

**Test:** `04_Mock_Tests/Week_11_Test.md`

---

### Week 12 — Consolidation, Full-Length Mocks & Weak-Area Repair
**Mon 23 Nov – Sun 29 Nov 2026**

No new material. This week converts knowledge into marks.

| Day | Plan |
|---|---|
| **Mon** | Full-length **Mock A** (170 Q / 180 min) → detailed review the same evening |
| **Tue** | Repair the two weakest sections from Mock A + revise formula sheets |
| **Wed** | Full-length **Mock B** → review |
| **Thu** | Repair + revise all Paper-I material (GK compilation, Tripura specials) |
| **Fri** | Full-length **Mock C** → review |
| **Sat** | Read every one-page subject sheet you wrote in Weeks 1–11, end-to-end |
| **Sun** | Light revision only. Error log re-read. Sleep on schedule. |

Blueprints and assembly instructions: `04_Mock_Tests/Full_Length_Mock_Blueprint.md`
**Test:** `04_Mock_Tests/Week_12_Test.md` (mixed full-syllabus rapid test)

---

## 6. The Paper-I daily track (all 12 weeks)

Run this every single day inside the 1-hour slot. Rotate the GK theme weekly.

**English (20 min/day)** — Synonyms & antonyms, common phrases & idioms, prepositions & articles, comprehension passages, ordering of words in a sentence, ordering of sentences, spotting errors, qualifying words.
*Method:* 10 new words/idioms daily in a notebook + 1 comprehension passage + 5 error-spotting sentences. Revisit the notebook every Sunday.

**General Mental Ability & Logical Reasoning (20 min/day)** — Series, analogy, coding-decoding, blood relations, direction sense, syllogisms, seating arrangement, puzzles, Venn diagrams, data interpretation, clocks & calendars, percentages, ratio, averages, time-speed-distance, time & work, profit & loss, simple/compound interest, permutations & combinations, number system.
*Method:* 15 timed questions daily. Use the Analytical/Quantitative Aptitude PDFs in both PYQ folders.

**General Knowledge & Current Affairs (20 min/day)** — 20 marks, the largest single block in Paper-I.

| Week | GK theme |
|---|---|
| 1–2 | **Tripura:** geography, rivers, districts, climate, demographics, tribes, languages |
| 3–4 | **Tripura:** history — Manikya dynasty, merger with India (1949), statehood (1972), Tripura Rebellion |
| 5–6 | **Tripura:** polity & economy — governance, schemes, IT/electronics policy, Agartala–Akhaura link, bamboo/rubber/tea |
| 7 | **Northeast India:** all 8 states — capitals, CMs, governors, festivals, national parks, Look/Act East Policy, NEC |
| 8 | **Indian History:** ancient, medieval, modern; freedom movement milestones |
| 9 | **Indian Geography:** physiography, rivers, climate, soils, minerals, agriculture |
| 10 | **Polity & Economy:** Constitution, fundamental rights & duties, DPSP, Parliament, judiciary, budget basics |
| 11 | **Science & Technology + IT-specific current affairs:** Digital India, IndiaAI Mission, DPDP Act 2023, ONDC, UPI, 5G/6G, ISRO missions, semiconductor mission |
| 12 | **Consolidated revision** of the whole current-affairs compilation |

*Current affairs window:* maintain a running note from **roughly December 2025 to the exam date**, with emphasis on the last 6 months and on **Tripura + Northeast + IT/technology**. One monthly compilation + one daily newspaper/aggregator pass is enough; do not over-invest here at the cost of Paper-II.

**Desirable (not tested, but stated in the advertisement):** knowledge of **Bengali or Kokborok**. It carries no written marks — but it is a legitimate talking point in the 30-mark interview, which is 15% of the final merit.

---

## 7. Study resources mapped to this plan

**Your local PYQ corpus (already downloaded):**

| Need | Folder |
|---|---|
| **Learn/revise a subject** | ⭐ **`05_Notes/Week_XX_<subject>.md`** — detailed notes for every syllabus section |
| Master formula sheet (all subjects) | `05_Notes/Week_12_Formula_Sheets_and_Revision.md` |
| Paper-I: English, reasoning, Tripura/NE/India GK | `05_Notes/Paper1_English_Reasoning_GK.md` |
| GATE questions for a subject | `03_GATE_CSE_PYQs/Subject_wise/<subject>/` |
| Full GATE papers, 2000–2026 | `03_GATE_CSE_PYQs/Year_wise/Question_Papers/` |
| State-PSC-level questions for a subject | `02_State_PSC_PYQs/Subject_wise/<subject>/` |
| Actual state PSC IT-post papers | `02_State_PSC_PYQs/Papers/Kerala_PSC/` |
| Weekly tests | `04_Mock_Tests/` |

**The notes in [`05_Notes/`](../05_Notes/) are written to be sufficient on their own for this exam.** The books below are optional depth for topics where you want more than the notes give — do not treat them as prerequisites.

**Standard books (use selectively — do not read cover to cover):**

| Subject | Book |
|---|---|
| Digital Logic | Morris Mano, *Digital Design* |
| COA | Morris Mano, *Computer System Architecture* / Hamacher |
| Programming & DS | Kanetkar, *Let Us C*; Tanenbaum/Horowitz–Sahni for DS |
| Algorithms | Cormen (CLRS) — selected chapters only |
| OS | Galvin, *Operating System Concepts* |
| DBMS | Korth / Navathe |
| Networks | Forouzan, *Data Communications and Networking* (best fit for this syllabus level) |
| Communication | Simon Haykin, *Communication Systems* (formula-level only) |
| Software Engineering | Pressman / Rajib Mall |
| Compiler | Aho–Ullman (Dragon Book), Ch. 1–9 selectively |
| Web/Cloud/Security | Any current UGC-NET Paper-II guide + OWASP and NIST reference pages |
| Tripura GK | A Tripura-specific GK compilation + Tripura Economic Review |

---

## 8. Exam day mechanics

Straight from the advertisement — these cost people their candidature every year:

- **The venue closes 10 minutes before the scheduled start.** "No functionary has any Authority in this regard." Plan to arrive **60+ minutes** early.
- **Mobile phones and all electronic gadgets are banned in the entire campus** — not just the hall. Possession means confiscation and possible debarment from future TPSC exams. Leave the phone in the vehicle or at home.
- **No jacket, coat, pullover** or similar garments are allowed in the hall. Dress accordingly regardless of November/December weather.
- All questions must be **answered only in English**.
- It is an **OMR-based** exam — practise darkening bubbles and, critically, **keeping the answer sheet aligned with the question number**. One misaligned row destroys a paper.
- Admit card is mandatory; admission is provisional in all respects.

**Time strategy for 170 questions in 180 minutes (~63 seconds/question):**

| Pass | What | Budget |
|---|---|---|
| 1 | Paper-I (50 Q) — mostly recall, fast | 40 min |
| 2 | Paper-II, all questions you can do in under a minute | 80 min |
| 3 | Flagged numericals (OS/CN/COA/DBMS) | 45 min |
| 4 | OMR verification and calculated guesses | 15 min |

**Guessing rule (assuming 1/3 negative):** attempt if you can eliminate at least two options; skip blind guesses. Given the 55%/45% *per-subject* qualifying rule, accuracy matters more than attempt count.

---

## 9. If your timeline shrinks

If TPSC announces a date that gives you fewer than 12 weeks, cut in this order — **never cut Paper-I**:

1. **Drop first:** Compiler Design optimisation/data-flow detail, Communication derivations, Probability beyond Bayes and the five named distributions.
2. **Compress next:** merge Week 11 into Week 10 (both are definitional), and merge Week 9's two halves into 4 days.
3. **Protect at all costs:** Data Structures & Programming, Algorithms, OS, DBMS, Networks (~58 marks together), plus the entire Paper-I hour.
4. **Still take every weekly test.** If you must choose between a chapter and a test, take the test.

---

## 10. Weekly checkpoint

Log these in `Weekly_Progress_Tracker.md` every Sunday night:

- Mock score, split as Paper-I / Paper-II
- Marks lost to **silly errors** vs **genuine gaps** (track separately — they need different fixes)
- Every wrong answer copied into a single **error log** file, with the correct reasoning in one line
- One sub-topic named for re-revision next week

**If your Paper-I mock score is below 30/50 by the end of Week 6, stop and rebalance** — move 30 minutes of Paper-II time into Paper-I until it recovers. Paper-I is the elimination gate.

---

*Plan generated 01 Sep 2026 from TPSC Advt. No. 02/2026 (Annexures A, B and C). Weightage figures in §2 are estimates and are labelled as such; all rules, dates, marks and eligibility statements are taken directly from the advertisement.*
