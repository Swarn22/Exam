# Week 12 — Master Formula Sheet & Final Revision

**All sections.** Everything worth memorising, on one page per subject. Read this cover to cover on the Saturday of Week 12, and again the evening before the exam.

> Nothing new here — every item appears in its own week's notes with explanation. This is for **recall drilling**, not learning.

---

## §1 — Probability & Statistics

📌 P(A ∪ B) = P(A) + P(B) − P(A ∩ B)
📌 P(A|B) = P(A ∩ B)/P(B)
📌 Independent: P(A ∩ B) = P(A)·P(B)
📌 **Bayes: P(Bᵢ|A) = P(A|Bᵢ)P(Bᵢ) / Σⱼ P(A|Bⱼ)P(Bⱼ)**
📌 Var(X) = E[X²] − (E[X])²
📌 E[aX+b] = aE[X]+b · **Var(aX+b) = a²Var(X)**
📌 E[X+Y] = E[X]+E[Y] always · Var(X+Y) = Var(X)+Var(Y) **only if independent**

| Distribution | Mean | Variance |
|---|---|---|
| Bernoulli | p | p(1−p) |
| **Binomial** | **np** | **np(1−p)** |
| **Poisson** | **λ** | **λ** |
| Uniform(a,b) | (a+b)/2 | (b−a)²/12 |
| **Exponential** | **1/λ** | **1/λ²** |
| Normal | μ | σ² |

📌 Normal: **68 / 95 / 99.7** within 1σ / 2σ / 3σ
📌 Mode ≈ 3·Median − 2·Mean
📌 σ = √variance; sample variance divides by **n−1**

---

## §2 — Digital Logic

📌 n-bit 2's complement range: **−2ⁿ⁻¹ to 2ⁿ⁻¹−1** (8-bit: −128 to +127)
📌 2's complement = 1's complement + 1
📌 Overflow = C_in(MSB) ⊕ C_out(MSB)
📌 **IEEE-754 single: 1+8+23, bias 127** · double: 1+11+52, bias 1023
📌 Boolean functions of n variables = **2^(2ⁿ)** · minterms = 2ⁿ
📌 A + A'B = **A + B** · (A+B+C)' = A'B'C'
📌 Universal gates: **NAND, NOR**
📌 2ⁿ:1 MUX needs **n** select lines · n-variable function needs a **2ⁿ⁻¹:1** MUX minimum
📌 Decoder: n inputs → **2ⁿ** outputs
📌 Full adder = **2 half adders + 1 OR**
📌 CLA: **Gᵢ = AᵢBᵢ (AND)**, **Pᵢ = Aᵢ⊕Bᵢ (XOR)**, Cᵢ₊₁ = Gᵢ + PᵢCᵢ
📌 JK with J=K=1 → **toggle** · race-around fixed by **master–slave**
📌 MOD-N counter needs **⌈log₂N⌉** flip-flops
📌 **Ring counter = n states; Johnson = 2n states**
📌 Ripple counter delay = **n × t_pd**; synchronous = t_pd
📌 **Moore: output = f(state). Mealy: output = f(state, input)**
📌 Gray: MSB stays, then Gᵢ = Bᵢ₊₁ ⊕ Bᵢ

**Excitation table:**

| Q→Q' | SR | JK | D | T |
|---|---|---|---|---|
| 0→0 | 0X | 0X | 0 | 0 |
| 0→1 | 10 | 1X | 1 | 1 |
| 1→0 | 01 | X1 | 0 | 1 |
| 1→1 | X0 | X0 | 1 | 0 |

---

## §3 — Computer Organization & Architecture

📌 **Pipeline cycles = k + (n − 1)** · Speedup = nk/(k+n−1) · **Max speedup = k**
📌 Clock period = max(stage delay) + latch overhead
📌 CPI with branches = 1 + f × penalty
📌 **Offset bits = log₂(block size)** · **Sets = lines / associativity** · Tag = addr − index − offset
📌 **AMAT (hierarchical) = T_c + (1−h)·T_m** · (simultaneous) = h·T_c + (1−h)·T_m
📌 Multi-level: AMAT = T_L1 + m_L1(T_L2 + m_L2·T_mem)
📌 **Avg rotational latency = ½ rotation = 30/RPM seconds**
📌 **Disk access = seek + rotational + transfer**
📌 Memory chips needed = (target capacity/chip capacity) × (target width/chip width)

| Concept | Answer |
|---|---|
| PC holds | Next instruction address |
| Zero-address | Stack machine |
| Pointers / arrays / branches | Indirect / indexed / PC-relative |
| RISC | Fixed length, load-store, many registers, hardwired |
| Microprogrammed | Slower, more flexible |
| Horizontal microinstruction | Wider, more parallel |
| RAW | True dependency; fix by forwarding |
| Write-back | Updates on eviction, needs dirty bit |
| Cache built from / main memory | SRAM / DRAM (needs refresh) |
| Cycle stealing | One bus cycle at a time |
| Three Cs | Compulsory, capacity, conflict |

---

## §4 — Analog & Digital Communication

📌 **AM bandwidth = 2f_m** · DSB-SC = 2f_m · **SSB = f_m**
📌 **P_total = P_c(1 + μ²/2)** · at μ=1, sidebands carry **33.3%** · η = μ²/(2+μ²)
📌 **Carson's rule: BW = 2(Δf + f_m)** · β = Δf/f_m
📌 AM IF = **455 kHz**; FM IF = 10.7 MHz · **Image = f_s + 2f_IF**
📌 **Entropy H = −Σp log₂p** · **H_max = log₂M**
📌 **Shannon: C = B log₂(1 + S/N)** · **Nyquist: C = 2B log₂L**
📌 SNR(dB) = 10 log₁₀(S/N)
📌 **Sampling: f_s ≥ 2f_m** · bits/sample **n = log₂L** · bit rate = f_s × n
📌 **PCM SNR(dB) = 6.02n + 1.76** (≈6 dB per bit)
📌 Quantisation noise = Δ²/12
📌 **Bit rate = baud rate × log₂M**
📌 Raised cosine BW = (1+α)·R_s/2
📌 **White noise: flat PSD** · **S_Y(f) = |H(f)|²S_X(f)** · PSD = FT(autocorrelation)
📌 **Hamming: 2ʳ ≥ m + r + 1** · detect d: d_min ≥ d+1 · **correct d: d_min ≥ 2d+1**
📌 Matched filter **maximises output SNR** (= 2E/N₀)
📌 MAP uses priors; **ML = MAP when priors are equal**
📌 DM: slope overload (step too small) vs granular noise (step too large)
📌 Modulation noise ranking: **PSK best, ASK worst**; QAM most bandwidth-efficient
📌 FDMA = frequency, TDMA = time, **CDMA = full bandwidth + orthogonal codes**

---

## §5 — Data Structures & Programming

📌 Row-major A[i][j] = Base + (i×ncols + j)×size
📌 Column-major A[i][j] = Base + (j×nrows + i)×size
📌 `p + n` advances by **n × sizeof(*p)** bytes
📌 Max nodes, binary tree height h (root=0) = **2^(h+1) − 1** · max at level i = 2ⁱ
📌 **n-node binary tree has n+1 NULL pointers** and n−1 edges
📌 Full binary tree: **leaves = internal + 1**
📌 Distinct binary trees with n nodes = **Catalan C(n) = (2n)!/(n!(n+1)!)**
📌 Heap (0-based): children **2i+1, 2i+2**; parent ⌊(i−1)/2⌋
📌 **Build-heap = O(n)**; insert/delete = O(log n)
📌 Max edges simple undirected = **n(n−1)/2**; directed = n(n−1)
📌 Sum of degrees = 2|E| · tree has n−1 edges
📌 Adjacency matrix O(V²) / list O(V+E)
📌 Circular queue **full: (rear+1)%n == front**; capacity **n−1**
📌 Load factor α = n/m
📌 Towers of Hanoi = **2ⁿ − 1** moves

| Structure | Search | Insert | Delete |
|---|---|---|---|
| BST average / **worst** | O(log n) / **O(n)** | same | same |
| AVL, Red-black | O(log n) | O(log n) | O(log n) |
| Heap | O(n) | O(log n) | O(log n) |
| **Hash (average)** | **O(1)** | O(1) | O(1) |

📌 **Inorder of a BST = sorted** · Unique tree from **inorder + pre/post**; ⚠ **preorder+postorder is NOT enough**
📌 BFS = queue; DFS = stack · Topological sort needs a **DAG**
📌 Linear probing → **primary** clustering; quadratic → **secondary**; double hashing → neither
📌 Postfix of A+B*C = **ABC*+**
📌 AVL balance factor ∈ {−1, 0, +1}; min nodes N(h) = N(h−1)+N(h−2)+1

**OOP/Java:** overloading = compile-time; overriding = run-time (vtable) · `::` `.` `.*` `?:` `sizeof` not overloadable · **final/finally/finalize** · String immutable · private = same class only · checked exceptions must be declared · Java char = 2 bytes · no multiple class inheritance (diamond problem)

---

## §6 — Algorithms

📌 **Growth: 1 < log log n < log n < √n < n < n log n < n² < n³ < 2ⁿ < n! < nⁿ**

**Master theorem** for T(n) = aT(n/b) + f(n), compare f(n) with n^(log_b a):

| Recurrence | Answer |
|---|---|
| 2T(n/2) + n | **Θ(n log n)** |
| 2T(n/2) + 1 | **Θ(n)** |
| T(n/2) + 1 | **Θ(log n)** |
| 2T(n/2) + n² | Θ(n²) |
| 4T(n/2) + n | Θ(n²) |
| 7T(n/2) + n² | Θ(n^2.81) — Strassen |
| T(n−1) + 1 / T(n−1) + n / 2T(n−1)+1 | O(n) / O(n²) / O(2ⁿ) |

📌 **Comparison sort lower bound = Ω(n log n)**

| Sort | Best | Avg | **Worst** | **Space** | **Stable** |
|---|---|---|---|---|---|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| **Insertion** | **O(n)** | O(n²) | O(n²) | O(1) | ✅ |
| **Merge** | n log n | n log n | **n log n** | **O(n)** | ✅ |
| **Quick** | n log n | **n log n** | **O(n²)** | O(log n) | ❌ |
| **Heap** | n log n | n log n | **n log n** | **O(1)** | ❌ |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) | ✅ |

📌 Unstable: **quick, heap, selection, shell** · Not in-place: **merge**
📌 Max-min comparisons = **3n/2 − 2**
📌 Binary search comparisons = ⌈log₂(n+1)⌉

| Algorithm | Complexity | Technique | Negative edges |
|---|---|---|---|
| **Prim** | O(E log V) | Greedy | — |
| **Kruskal** | O(E log E), union–find | Greedy | — |
| **Dijkstra** | O(E log V) | Greedy | ❌ **No** |
| **Bellman–Ford** | **O(VE)** | DP | ✅ (detects −cycles) |
| **Floyd–Warshall** | **O(V³)** | DP | ✅ |
| BFS/DFS, topological sort | O(V+E) | — | — |
| **0/1 knapsack** | O(nW) pseudo-poly | DP | — |
| **LCS** | O(mn) | DP | — |
| **Matrix chain** | O(n³) | DP | — |
| **Huffman** | O(n log n) | Greedy | — |

📌 MST has **V−1** edges; unique if all weights distinct
📌 **Fractional knapsack = greedy; 0/1 knapsack = DP**
📌 DP needs **optimal substructure + overlapping subproblems**
📌 **NP-complete = in NP AND NP-hard** · SAT was first (Cook–Levin)
📌 Euler circuit ∈ P; **Hamiltonian circuit is NP-complete**

---

## §7 — Compiler Design

📌 **Phases: Lexical → Syntax → Semantic → ICG → Optimisation → Code generation**
📌 Front end = 1–4; back end = 5–6
📌 **Undeclared variable / type mismatch = SEMANTIC error**
📌 Lexical analysis: **regular expressions → DFA**; longest-match rule
📌 **Left recursion must go for LL; LR handles it**
📌 **ε is never in FOLLOW**; FOLLOW(start) ∋ `$`
📌 **LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1)** · yacc uses **LALR(1)** · SLR and LALR have the **same state count**
📌 Ambiguous or left-recursive ⇒ **not LL(1)**
📌 Bottom-up = **rightmost derivation in reverse**
📌 **Synthesized = from children (bottom-up); inherited = from parent/siblings**
📌 S-attributed ⊂ L-attributed; terminals have only synthesized attributes
📌 **Quadruples reorder easily; triples do not; indirect triples do both**
📌 DAG exposes common subexpressions
📌 **Basic block = one entry, one exit**; leaders = first instruction, jump targets, instructions after jumps
📌 **Constant folding** (4*3→12) vs **constant propagation** (a=5 ⇒ b=a+2 → b=5+2)
📌 **Strength reduction:** x*2 → x<<1
📌 Activation record = run-time (stack); symbol table = compile-time
📌 C: **static scoping, call by value**

| Data-flow analysis | Direction | Meet | Enables |
|---|---|---|---|
| Reaching definitions | Forward | ∪ | Constant/copy propagation |
| **Live variables** | **BACKWARD** | ∪ | **Dead code elim., register allocation** |
| **Available expressions** | Forward | **∩** | **CSE** |

---

## §8 — Operating Systems

📌 **TAT = CT − AT** · **WT = TAT − BT** · Response time = first CPU − AT
📌 n `fork()` calls → **2ⁿ** processes
📌 `fork()`: **0 to child, PID to parent**
📌 **Running→Ready = preemption; Running→Waiting = I/O**
📌 **SJF gives minimum average WT** · RR with huge quantum → FCFS
📌 Starvation-free: FCFS, RR · fix priority starvation with **aging**
📌 **Critical section: mutual exclusion, progress, bounded waiting**
📌 Counting semaphore init n ⇒ n processes allowed
📌 **Deadlock: mutual exclusion, hold-and-wait, NO preemption, circular wait**
📌 **Banker's = avoidance** · Need = Max − Allocation · safe ⇒ no deadlock (converse false)
📌 **Paging → internal; segmentation → external** fragmentation
📌 Page table size = (VA space / page size) × PTE size
📌 **EAT with TLB = h(t_TLB + t_mem) + (1−h)(t_TLB + 2t_mem)**
📌 EAT with page faults = (1−p)t_mem + p·t_fault
📌 **Belady's anomaly = FIFO only** (LRU and OPT are stack algorithms)
📌 **OPT is unimplementable** (needs the future)
📌 Thrashing → **working set model** / PFF
📌 **Indexed allocation** = direct access + no external fragmentation
📌 **SSTF starves; SCAN = elevator; C-SCAN = uniform wait**
📌 Threads share code/data/heap/files; **own stack, registers, PC**
📌 **Zombie = dead child, live parent; orphan = live child, dead parent**

---

## §9 — Databases

📌 **Degree = columns; cardinality = rows** · R × S: degree adds, cardinality multiplies
📌 **Primitives: σ, π, ×, ∪, −, ρ** (join/∩/÷ are derived)
📌 **M:N ⇒ 3 tables; 1:N ⇒ 2 tables (FK on N side)**
📌 Weak entity PK = owner PK + partial key
📌 **PK cannot be NULL** (entity integrity); FK may be NULL (referential integrity)
📌 Clause order: **FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY**
📌 **COUNT(*) includes NULLs; COUNT(col) excludes them**; SUM/AVG/MIN/MAX ignore NULLs
📌 **`= NULL` never matches** — use `IS NULL`
📌 **HAVING filters groups; WHERE filters rows**
📌 DELETE (DML, rollback-able) / TRUNCATE (DDL, all rows) / **DROP (DDL, structure too)**
📌 **Armstrong: reflexivity, augmentation, transitivity**
📌 **2NF: no partial dependency · 3NF: no transitive (X super key OR Y prime) · BCNF: X must be super key**
📌 Single-attribute candidate key ⇒ automatically **2NF** · 2-attribute relation ⇒ always **BCNF**
📌 **Lossless ⟺ R1∩R2 is a super key of R1 or R2**
📌 **3NF: lossless + dependency-preserving always possible. BCNF: dependency preservation NOT guaranteed**
📌 **ACID: Atomicity, Consistency, Isolation, Durability**
📌 Conflict ⟺ different transactions, same item, at least one write (read–read never conflicts)
📌 **Conflict serializable ⟺ precedence graph is ACYCLIC**
📌 **Conflict ⊂ View serializable**
📌 Strict ⊂ Cascadeless ⊂ Recoverable
📌 **2PL ⇒ conflict serializability, NOT deadlock freedom**
📌 **Conservative 2PL = deadlock-free; strict 2PL = cascadeless**
📌 **B+ tree: data in leaves only, leaves linked ⇒ range queries**; higher fan-out, shallower
📌 Internal node order: p·P + (p−1)·K ≤ block size
📌 Secondary index must be **dense**; at most **one clustered** index per table
📌 **WAL: log before data**

---

## §10 — Information Systems & Software Engineering

📌 **Level-0 DFD = context diagram** (whole system as one process, no data stores)
📌 DFD shows **no control flow, decisions or timing**; no entity→entity or store→store flows
📌 **Spiral = risk-driven · V-model = testing mirrors development · Waterfall = late software**
📌 SRS: complete, consistent, unambiguous, verifiable, traceable, modifiable, ranked
📌 **TELOS** feasibility · Function points are language-independent
📌 **COCOMO: organic 2.4×KLOC^1.05 · semi-detached 3.0^1.12 · embedded 3.6^1.20**
📌 **PERT t_e = (t_o + 4t_m + t_p)/6**; σ = (t_p−t_o)/6
📌 **Critical path = LONGEST path, zero slack** · PERT probabilistic, CPM deterministic
📌 **Cohesion best→worst: Functional, Sequential, Communicational, Procedural, Temporal, Logical, Coincidental**
📌 **Coupling best→worst: Data, Stamp, Control, External, Common, Content**
📌 **V(G) = E − N + 2 = predicates + 1 = regions + 1**
📌 Black-box: BVA, equivalence partitioning, decision tables · White-box: statement/branch/path coverage
📌 **Coverage strength: statement < branch < condition < path**
📌 **Top-down → STUBS; bottom-up → DRIVERS**
📌 **Alpha = developer's site; beta = customer's site**
📌 **Load = at limits; stress = beyond limits**
📌 **Corrective (bugs) · Adaptive (environment) · Perfective (enhancements, largest) · Preventive (future-proofing)**
📌 Maintenance = 60–70% of lifecycle cost
📌 **CMM: 1 Initial · 2 Repeatable · 3 Defined · 4 Managed/Quantitative · 5 Optimising**
📌 **Availability = MTTF/(MTTF+MTTR)**; MTBF = MTTF + MTTR
📌 Changeover: **parallel = lowest risk; direct = highest**
📌 Verification = building it right; **Validation = building the right thing**

---

## §11 — Computer Networks

📌 **OSI 7 layers** (Physical, Data link, Network, Transport, Session, Presentation, Application) · **TCP/IP 4**; session+presentation absent
📌 Routing = network (3) · framing = data link (2) · encryption = presentation (6)
📌 **Hub = L1, Switch = L2, Router = L3** · **only routers separate broadcast domains**
📌 **Transmission delay = L/B; propagation delay = d/v** · BDP = bandwidth × RTT
📌 **Shannon C = B log₂(1+S/N)** · **Nyquist C = 2B log₂L**
📌 **Detect d: d_min ≥ d+1 · Correct d: d_min ≥ 2d+1** · Hamming: 2ʳ ≥ m+r+1
📌 **Efficiency η = W/(1+2a)**, a = T_prop/T_trans · optimum W = 1+2a
📌 **GBN: sender N, receiver 1, max window 2ᵐ−1** · **SR: both N, max 2ᵐ⁻¹**
📌 **Pure ALOHA 18.4% (1/2e); slotted 36.8% (1/e)**
📌 **Min frame size = 2 × T_prop × Bandwidth** → Ethernet **64 bytes**; MTU 1500; MAC 48 bits
📌 **IPv4 header 20–60 B; IPv6 fixed 40 B** · Total length field max 65,535
📌 **Fragment offset in 8-byte units** · MF=1 except last · **reassembly only at destination**
📌 **Usable hosts = 2^(32−prefix) − 2**

| Prefix | Mask (last octet) | Addresses | Usable |
|---|---|---|---|
| /25 | 128 | 128 | 126 |
| **/26** | **192** | 64 | **62** |
| **/27** | **224** | 32 | **30** |
| /28 | 240 | 16 | 14 |
| /29 | 248 | 8 | 6 |
| **/30** | **252** | 4 | **2** |
| /20 | 255.255.240.0 | 4096 | 4094 |
| /22 | 255.255.252.0 | 1024 | 1022 |

📌 Private: 10.0.0.0/8 · 172.16.0.0/12 · 192.168.0.0/16 · **Loopback 127.0.0.0/8**
📌 Routing lookup = **longest prefix match**
📌 **RIP = distance vector, infinity 16 · OSPF = link state (Dijkstra) · BGP = path vector, exterior**
📌 Count-to-infinity = distance vector; fixes = split horizon, poison reverse
📌 **ARP: IP→MAC · DHCP: DORA (67/68) · ping uses ICMP**
📌 **TCP header 20–60 B; UDP 8 B** · TCP: 3-way setup, 4-way teardown
📌 **Slow start = exponential; congestion avoidance = linear (AIMD)**; fast retransmit on **3 duplicate ACKs**; timeout ⇒ cwnd = 1
📌 Effective window = min(rwnd, cwnd)

📌 **Ports: FTP 20/21 · SSH 22 · Telnet 23 · SMTP 25 · DNS 53 · DHCP 67/68 · HTTP 80 · POP3 110 · IMAP 143 · HTTPS 443**
📌 DNS uses **UDP 53**; records A, AAAA, CNAME, MX, NS, PTR, SOA
📌 HTTP: 2xx success, 3xx redirect, **4xx client (404)**, **5xx server (500)**
📌 **SMTP sends; POP3/IMAP retrieve** (IMAP keeps mail on the server)
📌 **FTP uses two connections** (21 control, 20 data)

---

## §12/13/14 — Web, Cyber Security, Cloud

📌 **Box model: content → padding → border → margin**
📌 **Specificity: !important > inline > ID > class > element > universal**
📌 **Well-formed** (syntax) vs **valid** (conforms to DTD/XSD); XSD is written in XML
📌 **XSLT transforms; XPath navigates**
📌 **Forward proxy hides clients; reverse proxy fronts servers (load balancing)**
📌 Web server = static; application server = business logic
📌 **MVC: Model = data/logic, View = UI, Controller = handles input**
📌 **REST = architectural style (stateless, JSON, HTTP); SOAP = protocol (XML, WSDL, UDDI)**
📌 **PUT idempotent; POST not**
📌 localStorage persists; sessionStorage per-tab; cookies ~4 KB, sent every request

📌 **IaaS: customer manages OS+app+data · PaaS: app+data only · SaaS: nothing**
📌 NIST 5 characteristics: on-demand self-service, broad network access, resource pooling, rapid elasticity, measured service
📌 Deployment: public, private, hybrid, community
📌 **Type-1 hypervisor = bare metal (ESXi/Hyper-V/Xen/KVM); Type-2 = hosted (VirtualBox)**
📌 **Containers share the host kernel (light); VMs have their own OS (better isolation)** · Kubernetes orchestrates; pod = smallest unit
📌 **Block (databases) · File (shared) · Object (flat, HTTP, S3)**
📌 **Edge < Fog < Cloud** in latency; edge reduces latency and bandwidth
📌 Scale up = vertical; scale out = horizontal

📌 **OWASP 2021: A01 Broken Access Control, A02 Cryptographic Failures, A03 Injection, A04 Insecure Design, A05 Security Misconfiguration, A06 Vulnerable Components, A07 Auth Failures, A08 Integrity Failures, A09 Logging Failures, A10 SSRF**
📌 **SQL injection fix = parameterised queries** · **XSS fix = output encoding + CSP**
📌 XSS attacks the browser; SQLi attacks the database; CSRF exploits an authenticated session
📌 **Symmetric: 1 key, fast, n(n−1)/2 keys, AES/DES** · **Asymmetric: key pair, slow, 2n keys, RSA/ECC/DH**
📌 **Digital signature = hash encrypted with the SENDER'S PRIVATE key** → authentication + integrity + non-repudiation, **NOT confidentiality**
📌 Encrypt for confidentiality = **receiver's public key**
📌 MD5/SHA-1 broken; use SHA-256; passwords need **salt + bcrypt/Argon2**
📌 **CIA: Confidentiality, Integrity, Availability** · DDoS attacks availability
📌 **IDS detects/alerts; IPS blocks** · Worm self-replicates, virus needs a host
📌 IT Act 2000; DPDP Act 2023; CERT-In

📌 **MQTT: pub/sub, TCP, broker · CoAP: request/response, UDP**
📌 IoT layers: perception → network → processing → application
📌 **Blockchain immutability = each block stores the previous block's hash**
📌 **PoW (Bitcoin, energy-intensive) vs PoS (Ethereum, efficient)** · smart contracts = Solidity on Ethereum
📌 **AI ⊃ ML ⊃ Deep Learning**
📌 **Supervised = labelled · Unsupervised (k-means, PCA) = unlabelled · Reinforcement = rewards**
📌 **CNN = images · RNN/LSTM = sequences · Transformer = LLMs**
📌 **Precision = TP/(TP+FP) · Recall = TP/(TP+FN) · F1 = harmonic mean**
📌 **Overfitting = low train error, high test error** → regularisation, dropout, more data

---

## Paper-I quick recall

📌 **English 15 · Reasoning 15 · GK & Current Affairs 20 = 50**
📌 **UR must score ≥ 27.5/50 in Paper-I AND ≥ 66/120 in Paper-II — independently**

**Tripura essentials:**

| Fact | Answer |
|---|---|
| Merger with India | **15 October 1949** |
| Union Territory | 1956 |
| **Full statehood** | **21 January 1972** |
| Capital | Agartala |
| Districts | **8** |
| Highest peak | **Betlingchhip**, Jampui Hills |
| Longest river | **Gomati** |
| International border | **Bangladesh** (3 sides, ~856 km) |
| Indian neighbours | Assam, Mizoram |
| Official languages | Bengali, English, **Kokborok** (Tibeto-Burman) |
| Lake palace | **Neermahal**, Rudrasagar Lake, Melaghar |
| Rock carvings | **Unakoti** |
| Shakti Peetha | **Tripura Sundari Temple, Udaipur** |
| Last ruling dynasty | **Manikya** |
| Merger signed by | **Maharani Kanchan Prava Devi** (Regent) |
| Rail link to Bangladesh | **Agartala–Akhaura** (2023) |

---

## Final 48 hours

**Do:**
- Read this sheet cover to cover, twice.
- Re-read your **error log** in [Weekly_Progress_Tracker.md](../01_Study_Plan/Weekly_Progress_Tracker.md).
- Skim the ⭐ items in each week's notes.
- Revise the Paper-I GK compilation (the largest single Paper-I block, and the most forgettable).
- Confirm the exam centre, route, and admit card. Sleep on schedule.

**Do not:**
- Start any new topic.
- Take a fresh full-length mock the day before.
- Stay up late "finishing" a subject.

**Exam-day reminders (from the advertisement):**
- ⚠ The venue **closes 10 minutes before** the scheduled start. Arrive 60+ minutes early.
- ⚠ **Mobile phones and electronic gadgets are banned in the entire campus** — confiscation and possible debarment.
- ⚠ **No jacket, coat or pullover** in the hall.
- Answer **in English only**. OMR — keep the row alignment correct.
- 170 questions in 180 minutes ≈ **63 seconds each**. Paper-I first (40 min), then Paper-II in two passes, then 15 minutes for OMR verification.
- Negative marking assumed **1/3** — attempt only when you can eliminate at least two options.
