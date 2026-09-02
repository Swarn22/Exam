# Week 11 — Information Systems & Software Engineering + Compiler Design

**Syllabus §10:** Information gathering, requirement and feasibility analysis, data flow diagrams, process specifications, input/output design, process life cycle, planning and managing the project, design, coding, testing, implementation, maintenance.
**Syllabus §7:** Lexical analysis, parsing, syntax-directed translation. Runtime environments. Intermediate code generation. Local optimization. Data flow analyses: constant propagation, liveness analysis, common subexpression elimination.

**Estimated marks: ~8 + ~6 = ~14**

> ⭐ **Software Engineering has ZERO GATE coverage but 337 questions in the state-PSC corpus** (ISRO 52 + NIELIT 70 + UGC-NET 215). It is the single largest untapped block in Paper-II and is entirely definitional. Prioritise Part A.

---

# PART A — INFORMATION SYSTEMS & SOFTWARE ENGINEERING

## 1. ⭐ Information gathering & system analysis

### 1.1 Fact-finding techniques

| Technique | Use | Note |
|---|---|---|
| ⭐ **Interviews** | Depth, clarification | Structured / unstructured / semi-structured; time-consuming |
| ⭐ **Questionnaires** | Many respondents, quantitative | Cheap at scale; low response rate, no follow-up |
| ⭐ **Observation** | See actual practice | Reveals what people *do* vs what they *say*; **Hawthorne effect** |
| ⭐ **Record/document review** | Existing forms, reports, procedures | Historical, factual |
| **JAD (Joint Application Development)** | Facilitated group workshops | Fast consensus |
| **Prototyping** | Elicit requirements by showing something | Good for unclear requirements |
| **Brainstorming, site visits, background reading** | | |

### 1.2 ⭐ Types of information system

| System | Serves | Purpose |
|---|---|---|
| **TPS** (Transaction Processing System) | Operational staff | Records day-to-day transactions |
| ⭐ **MIS** (Management Information System) | Middle management | Routine summary/exception reports |
| ⭐ **DSS** (Decision Support System) | Management | Semi-structured decisions; what-if analysis, models |
| ⭐ **EIS / ESS** (Executive Support System) | Top management | Strategic dashboards, external data |
| **ERP** | Whole enterprise | Integrated cross-functional |
| **KMS, OAS, Expert Systems** | | |

⚠ **MIS produces routine reports; DSS supports non-routine analytical decisions.** A standard comparison question.

### 1.3 ⭐⭐ Requirements

📌 ⭐ **Functional requirements** — *what* the system must **do** (features, computations, data processing, use cases).
📌 ⭐ **Non-functional requirements (NFRs)** — *how well* it does it: ⭐ **performance, reliability, availability, security, usability, scalability, maintainability, portability**, legal/regulatory compliance.

🔢 "The system shall allow a user to reset their password" = **functional**.
🔢 "Response time must be under 2 seconds for 95% of requests" = ⭐ **non-functional**.
🔢 "The system shall be available 99.9% of the time" = **non-functional**.

**Requirements engineering process:** elicitation → analysis → specification → **validation** → management.
⚠ **Verification** asks "are we building the product right?"; ⭐ **Validation** asks "are we building the right product?"

⭐ **SRS (Software Requirements Specification)** — the output of the requirements phase; the contract between customer and developer, and the baseline for design and testing.

⭐ **Characteristics of a good SRS:** ⭐ **complete · consistent · unambiguous · verifiable/testable · traceable · modifiable · ranked for importance and stability · correct**.

### 1.4 ⭐ Feasibility study

| Type | Question |
|---|---|
| ⭐ **Technical** | Can it be built with available technology and skills? |
| ⭐ **Economic / financial** | Do the benefits justify the cost? (⭐ **cost–benefit analysis**, ROI, NPV, payback period) |
| ⭐ **Operational** | Will the organisation and users actually use it? |
| ⭐ **Schedule** | Can it be delivered in time? |
| ⭐ **Legal** | Does it comply with laws, contracts and regulations? |

⭐ Mnemonic: **TELOS** (Technical, Economic, Legal, Operational, Schedule).

---

## 2. ⭐⭐ Data Flow Diagrams (DFD)

📌 A DFD is a **structured-analysis** tool showing how data moves through a system. It shows **what** the system does, not **how** or in what order.

### 2.1 ⭐ Four symbols

| Symbol | Yourdon/DeMarco | Meaning |
|---|---|---|
| ⭐ **Process** | Circle / bubble | Transforms input data into output |
| ⭐ **Data flow** | Arrow (labelled) | Data in motion |
| ⭐ **Data store / warehouse** | Two parallel lines / open rectangle | Data at rest |
| ⭐ **External entity / terminator** | Rectangle / square | Source or sink outside the system |

*(Gane–Sarson uses rounded rectangles for processes and squares for entities — the semantics are identical.)*

### 2.2 ⭐⭐ Levels

| Level | Name | Content |
|---|---|---|
| ⭐ **Level 0** | ⭐ **Context diagram** | ⭐ **The ENTIRE system as ONE process**, with all external entities and the flows between them. **No data stores** shown |
| **Level 1** | Top level | The main sub-processes (typically 3–7) |
| **Level 2, 3…** | Detailed | Progressive decomposition of individual processes |

⭐ **Rules:**
- ⭐ **Balancing:** the inputs and outputs of a process at level n must **match exactly** the net inputs and outputs of its expansion at level n+1.
- Every process must have at least one input **and** one output.
  ⚠ A process with only inputs is a **black hole**; with only outputs, a **miracle**; unchanged data passing through is a **grey hole**.
- ⭐ **Data cannot flow directly between two external entities**, between two data stores, or from a data store to an external entity — it must pass through a **process**.
- Numbering: level-1 processes are 1, 2, 3; their children are 1.1, 1.2, …

⚠ ⭐ **A DFD does NOT show control flow, decisions, loops, or timing/sequence.** That is the most common DFD question.

### 2.3 ⭐ Supporting tools

| Tool | Purpose |
|---|---|
| ⭐ **Process specification (mini-spec)** | Describes the logic of a primitive (undecomposed) process — structured English, pseudocode, decision tables or decision trees |
| ⭐ **Data dictionary** | Defines every data element and structure (name, aliases, type, length, values, composition) |
| ⭐ **Decision table** | Condition stubs and action stubs; ⭐ **for n binary conditions there are 2ⁿ rules/columns** |
| **Decision tree** | Graphical equivalent; better for sequential decisions |
| **Structure chart** | Hierarchical module decomposition (design, not analysis) |
| **ER diagram** | Data model (complements the DFD's process model) |
| **State transition diagram** | Event/time-dependent behaviour — supplies what a DFD lacks |

### 2.4 Input/output design
**Input design goals:** accuracy, minimum data entry, ease of use, validation at source. Techniques: form design, **input validation** (batch/interactive), check digits, codes, default values, drop-downs over free text.
**Output design:** the right content to the right user at the right time; output types (internal/external/turnaround), media, layout, reports vs dashboards vs queries.
**Codes:** sequence, block, group classification, significant digit, mnemonic, check digit.

---

## 3. ⭐⭐ Software process models

### 3.1 ⭐ Comparison table

| Model | Key idea | Best when | Weakness |
|---|---|---|---|
| ⭐ **Waterfall (classical linear)** | Strictly sequential phases | Requirements **stable and well understood**; short, familiar projects | ⭐ **No working software until late; requirement changes are very expensive; no iteration** |
| **Iterative / Incremental** | Deliver in increments, each adding functionality | Core requirements clear, extras evolving | Needs good architecture upfront |
| ⭐ **Prototyping** | Build a throwaway/evolutionary prototype to clarify requirements | ⭐ **Requirements unclear** | Prototype may be mistaken for the product; poor documentation |
| ⭐ **Spiral (Boehm)** | ⭐ **RISK-DRIVEN**, iterative cycles with 4 quadrants: ⭐ **planning → risk analysis → engineering → evaluation** | ⭐ **Large, expensive, high-risk projects** | Costly; needs risk-assessment expertise; complex to manage |
| ⭐ **V-model** | Waterfall with a ⭐ **testing phase mirroring every development phase** | Safety-critical, high-reliability systems | Rigid, like waterfall |
| **RAD** | Rapid parallel development with reusable components and JAD | Modular systems, tight deadlines | Needs skilled teams and committed users |
| ⭐ **Agile / Scrum** | ⭐ **Iterative, incremental, adaptive**; working software over documentation | Changing requirements, customer available | Less documentation; hard to scale/predict cost |
| **RUP** | Use-case driven, architecture-centric, 4 phases | Large OO projects | Heavyweight |
| ⭐ **DevOps** | Development + operations integration; CI/CD, automation | Continuous delivery | Cultural change required |

⭐ **The three most-asked identifications:**
- "**Risk-driven**" → ⭐ **Spiral**
- "Testing phase for every development phase" → ⭐ **V-model**
- "Working software only at the very end" → ⭐ **Waterfall**

**Waterfall phases:** Requirement analysis & specification → Design → Coding/Implementation → Testing → Deployment → **Maintenance**.

### 3.2 ⭐ Agile

⭐ **The Agile Manifesto's four values** — favouring:
1. **Individuals and interactions** over processes and tools
2. ⭐ **Working software** over comprehensive documentation
3. ⭐ **Customer collaboration** over contract negotiation
4. ⭐ **Responding to change** over following a plan

⭐ **Scrum:**

| Element | Meaning |
|---|---|
| ⭐ **Sprint** | A fixed-length iteration, typically **2–4 weeks**, producing a potentially shippable increment |
| ⭐ **Product backlog** | Prioritised list of all desired work, owned by the Product Owner |
| **Sprint backlog** | Items selected for the current sprint |
| ⭐ **Roles** | ⭐ **Product Owner** (what/priority) · ⭐ **Scrum Master** (facilitator, removes impediments — *not* a manager) · **Development Team** |
| ⭐ **Ceremonies** | Sprint planning · ⭐ **Daily stand-up/scrum (15 min)** · Sprint review (demo) · Sprint retrospective (process improvement) |
| ⭐ **Burndown chart** | Remaining work over time |
| **Velocity** | Story points completed per sprint |

**Other Agile methods:** ⭐ **XP (Extreme Programming)** — pair programming, TDD, continuous integration, small releases, refactoring · **Kanban** — visual board, WIP limits, continuous flow (no fixed sprints) · Lean · Crystal · FDD.
⚠ **Scrum uses fixed-length sprints; Kanban uses continuous flow with WIP limits.**

---

## 4. ⭐⭐ Project planning, estimation & management

### 4.1 ⭐ Size estimation

**LOC (Lines of Code)** — simple to measure but language-dependent, can only be counted accurately *after* coding, and rewards verbosity.

⭐ **Function Point (FP) analysis** — language-independent, measurable from the **requirements** stage.
📌 Five function types: ⭐ **External Inputs (EI) · External Outputs (EO) · External Inquiries (EQ) · Internal Logical Files (ILF) · External Interface Files (EIF)**
📌 **UFP** = Σ (count × weight) → **FP = UFP × VAF**, where VAF = 0.65 + 0.01 × Σ(14 general system characteristics, each 0–5)
📌 So VAF ranges from **0.65 to 1.35**.

⚠ **Function points are language-independent and available early; LOC is neither.** That contrast is the exam point.

### 4.2 ⭐⭐ COCOMO (COnstructive COst MOdel — Boehm, 1981)

⭐ **Three project modes:**

| Mode | Characteristics | a | b |
|---|---|---|---|
| ⭐ **Organic** | ⭐ **Small team, familiar problem, flexible requirements** (2–50 KLOC) | 2.4 | 1.05 |
| ⭐ **Semi-detached** | ⭐ **Medium size, mixed experience, some rigid constraints** (50–300 KLOC) | 3.0 | 1.12 |
| ⭐ **Embedded** | ⭐ **Large, tight hardware/regulatory constraints, complex** (> 300 KLOC) | 3.6 | 1.20 |

📌 ⭐ **Basic COCOMO effort: E = a × (KLOC)^b person-months**
📌 ⭐ **Development time: D = c × (E)^d months** (organic c=2.5, d=0.38; semi-detached d=0.35; embedded d=0.32)
📌 ⭐ **Average staff size = E / D persons**
📌 **Productivity = KLOC / E**

🔢 Organic project, 32 KLOC: E = 2.4 × 32^1.05 ≈ 2.4 × 37.4 ≈ **91 person-months**.
D = 2.5 × 91^0.38 ≈ 2.5 × 5.6 ≈ **14 months**. Staff ≈ 91/14 ≈ **6.5 people**.

⭐ **Note the exponents b > 1** for all three modes — effort grows **super-linearly** with size (diseconomy of scale). Embedded has the largest exponent, so it is most sensitive to size.

**Three COCOMO levels:** **Basic** (size only) → **Intermediate** (adds 15 cost drivers/EAF) → **Detailed/Complete** (cost drivers per phase). **COCOMO II** modernises it.
⚠ ⭐ **Brooks's law:** "Adding manpower to a late software project makes it later" — because of communication overhead and ramp-up time.

### 4.3 ⭐ Scheduling

⭐ **Gantt chart** — a bar chart of tasks against a calendar; shows **duration, overlap and progress**, but ⚠ **does not clearly show dependencies or the critical path**.

⭐ **PERT / CPM** — activity network diagrams that **do** show dependencies.

| | ⭐ **PERT** | ⭐ **CPM** |
|---|---|---|
| Time estimates | ⭐ **Probabilistic** (three-point) | ⭐ **Deterministic** (single estimate) |
| Focus | ⭐ **Time / uncertainty** | ⭐ **Time–cost trade-off** |
| Suits | Research/novel projects | Repetitive/well-understood projects |
| Orientation | Event-oriented | Activity-oriented |

📌 ⭐ **PERT expected time: t_e = (t_optimistic + 4·t_most-likely + t_pessimistic) / 6**
📌 **Standard deviation σ = (t_p − t_o)/6**; variance = σ²

🔢 t_o = 4, t_m = 6, t_p = 14 days → t_e = (4 + 24 + 14)/6 = 42/6 = **7 days**; σ = (14−4)/6 = **1.67 days**.

📌 ⭐ **Critical path = the LONGEST path through the network** — it determines the minimum project duration.
📌 ⭐ **Activities on the critical path have ZERO slack/float.** Delaying any of them delays the whole project.
📌 **Slack / float = Latest Start − Earliest Start = Latest Finish − Earliest Finish**

⚠ **Longest**, not shortest — the most common error in this topic.

### 4.4 ⭐ Risk management
**Steps:** risk **identification** → risk **analysis** (probability × impact) → risk **prioritisation** (⭐ **Risk Exposure = probability × loss**) → risk **mitigation, monitoring and management (RMMM)**.
**Risk categories:** project risks (schedule, budget, staffing) · technical risks · business risks · known/predictable/unpredictable.
**Strategies:** avoid · transfer · mitigate · accept.

### 4.5 Configuration management & metrics
⭐ **SCM (Software Configuration Management):** version control, **baselines**, change control (CCB), configuration audit, status accounting. Tools: Git, SVN.
**Metrics:** process / project / product metrics · size (LOC, FP) · quality (defect density, DRE, MTTF, MTBF) · ⭐ **Cyclomatic complexity** (see §5.4).
📌 **Defect Removal Efficiency (DRE) = E / (E + D)**, where E = errors found before delivery, D = defects found after.

---

## 5. ⭐⭐ Design and coding

### 5.1 ⭐ Design principles
⭐ **Abstraction** · ⭐ **Modularity** (decompose into manageable units) · ⭐ **Information hiding** (a module's internals are inaccessible; the interface is the only contract) · **stepwise refinement** · **functional independence** (achieved through high cohesion and low coupling) · separation of concerns · **anticipation of change**.

📌 ⭐ **The single most important design goal: HIGH COHESION and LOW COUPLING.**

### 5.2 ⭐⭐ Cohesion (within a module) — best to worst

| Rank | Type | Description |
|---|---|---|
| ⭐ **1 (BEST)** | ⭐ **Functional** | All elements contribute to a **single, well-defined task** |
| 2 | **Sequential** | Output of one element is the input of the next |
| 3 | **Communicational** | Elements operate on the **same data** |
| 4 | **Procedural** | Elements follow a required **sequence of execution** |
| 5 | **Temporal** | Elements are related only by being executed at the **same time** (e.g. an `init()` routine) |
| 6 | **Logical** | Elements perform **logically similar** functions, selected by a flag (e.g. a generic `handleAll(type)`) |
| ⭐ **7 (WORST)** | ⭐ **Coincidental** | ⭐ **No meaningful relationship** — a grab-bag utility module |

⭐ Mnemonic (best → worst): **F**unctional **S**equential **C**ommunicational **P**rocedural **T**emporal **L**ogical **C**oincidental

### 5.3 ⭐⭐ Coupling (between modules) — best to worst

| Rank | Type | Description |
|---|---|---|
| ⭐ **1 (BEST)** | ⭐ **Data** | Modules communicate only via **simple parameters** |
| 2 | **Stamp / data-structure** | An entire **data structure** is passed but only part is used |
| 3 | ⭐ **Control** | One module passes a **flag** that controls the other's internal logic |
| 4 | **External** | Modules share an externally imposed format/protocol/device |
| 5 | **Common / global** | Modules share **global data** |
| ⭐ **6 (WORST)** | ⭐ **Content** | ⭐ **One module directly references or modifies another's internals** |

⭐ Mnemonic (best → worst): **D**ata **S**tamp **C**ontrol **E**xternal **C**ommon **C**ontent

⚠ ⭐ **Both orderings are asked directly and frequently.** Memorise which end is best: **functional cohesion is best, coincidental worst; data coupling is best, content worst.**

### 5.4 ⭐⭐ Cyclomatic complexity (McCabe)

📌 ⭐ **V(G) = E − N + 2P** (E = edges, N = nodes, P = connected components; for a single program P = 1, so **V(G) = E − N + 2**)
📌 ⭐ **V(G) = number of predicate (decision) nodes + 1**
📌 ⭐ **V(G) = number of bounded regions in the planar flow graph + 1**

🔢 A flow graph with **12 edges and 9 nodes** → V(G) = 12 − 9 + 2 = **5**.
🔢 A program with 3 `if` statements and no other branching → V(G) = 3 + 1 = **4**.

⭐ **Interpretation:** V(G) is the number of **linearly independent paths**, and hence a **lower bound on the test cases needed for branch coverage**. Complexity above ~10 is generally considered a refactoring signal.

### 5.5 Architectural and design approaches
**Architectural styles:** layered · client–server · **MVC** · repository/data-centred · pipe-and-filter · event-driven · microservices · service-oriented (SOA).
⭐ **Top-down (functional decomposition) vs bottom-up design.** **Structured design** (DFD → structure chart via transform/transaction analysis) vs **object-oriented design** (UML).
**UML diagrams:** structural — class, object, component, deployment, package; behavioural — **use case**, sequence, activity, state, collaboration.
⭐ **Design patterns:** **creational** (Singleton, Factory, Builder, Prototype) · **structural** (Adapter, Decorator, Facade, Proxy, Composite) · **behavioural** (Observer, Strategy, Command, Iterator, State).
**SOLID principles:** Single responsibility · Open/closed · Liskov substitution · Interface segregation · Dependency inversion.
**Coding:** coding standards and guidelines · code review (⭐ **walkthrough** = informal, author-led; ⭐ **inspection** = formal, checklist-driven, moderated) · refactoring · documentation.

---

## 6. ⭐⭐ Testing

### 6.1 ⭐ Terminology
⚠ ⭐ **Error** (human mistake) → **Fault/Defect/Bug** (the flaw in the artefact) → **Failure** (observable incorrect behaviour) → **Consequence**.
📌 ⭐ **Testing can only show the *presence* of defects, never their absence** (Dijkstra).

### 6.2 ⭐⭐ Black-box vs white-box

| | ⭐ **Black-box (functional)** | ⭐ **White-box (structural / glass-box)** |
|---|---|---|
| Basis | ⭐ **Specification only** — internals unknown | ⭐ **Internal code structure** |
| Performed by | Testers, users | Developers |
| Techniques | ⭐ **Equivalence class partitioning · Boundary value analysis · Cause-effect graphing · Decision table testing · State transition testing · Error guessing · Orthogonal arrays** | ⭐ **Statement coverage · Branch/decision coverage · Condition coverage · Path coverage · Data-flow testing · Loop testing · Mutation testing** |
| Finds | Missing functionality | Logic and structural errors, unreachable code |

⭐ **Boundary Value Analysis (BVA):** most defects cluster at the **boundaries** of input ranges.
🔢 For a valid input range 1–100, test: **0, 1, 2, 50, 99, 100, 101** (just below, at, and just above each boundary).

⭐ **Equivalence Class Partitioning:** divide inputs into classes that should be handled identically, then test **one value per class** plus invalid classes. For range 1–100: classes are `<1`, `1–100`, `>100`.

⭐ **Coverage hierarchy (weakest → strongest):** **statement < branch/decision < condition < path coverage**
⚠ ⭐ **100% statement coverage does NOT imply 100% branch coverage** (an `if` with no `else` can have every statement executed while the false branch is never taken). Path coverage is the strongest but generally infeasible (loops give unbounded paths).

**Grey-box testing** combines both.

### 6.3 ⭐⭐ Levels of testing

| Level | Scope | Performed by |
|---|---|---|
| ⭐ **Unit testing** | Individual module/function in isolation | Developer (white-box) |
| ⭐ **Integration testing** | Interfaces between modules | Developers/testers |
| ⭐ **System testing** | The complete integrated system against the SRS | Independent test team (black-box) |
| ⭐ **Acceptance testing** | Customer's confirmation that it meets their needs | ⭐ **Customer/user** |

⭐ **Integration strategies:**

| Strategy | Order | ⭐ Needs |
|---|---|---|
| ⭐ **Top-down** | Highest modules first | ⭐ **STUBS** (dummy *called* modules) |
| ⭐ **Bottom-up** | Lowest modules first | ⭐ **DRIVERS** (dummy *calling* modules) |
| **Sandwich / hybrid** | Both ends toward the middle | Both |
| **Big-bang** | Everything at once | Neither — but defects are very hard to localise |

⚠ ⭐ **Top-down needs stubs; bottom-up needs drivers.** Swapping these is the most common error in the entire Software Engineering section.
⭐ **Top-down** validates the architecture/control logic early; **bottom-up** validates the low-level utilities early and allows earlier parallel work.

⭐ **Alpha vs beta testing:**

| | ⭐ **Alpha testing** | ⭐ **Beta testing** |
|---|---|---|
| Where | ⭐ **At the developer's site** | ⭐ **At the customer's site** |
| By whom | Internal staff / selected users, with developers present | ⭐ **Real end users**, developers absent |
| Stage | Before beta | Before general release |

Both are forms of **acceptance testing**.

### 6.4 ⭐ Other testing types

| Type | Purpose |
|---|---|
| ⭐ **Regression testing** | ⭐ **Re-run existing tests after a change** to ensure nothing previously working has broken |
| ⭐ **Smoke testing** | A quick "is the build even viable?" check ("build verification") |
| **Sanity testing** | Narrow check that a specific fix works |
| ⭐ **Performance testing** | Response time and throughput under expected load |
| ⭐ **Load vs Stress testing** | ⭐ **Load** = behaviour at expected peak; ⭐ **Stress** = behaviour **beyond** limits, to find the breaking point |
| **Volume testing** | Large data volumes |
| ⭐ **Security testing** | Vulnerabilities, penetration testing |
| **Usability testing** | Ease of use |
| **Compatibility / portability testing** | Across platforms and browsers |
| **Recovery testing** | Behaviour after failures |
| ⭐ **Mutation testing** | Deliberately inject faults to evaluate the **test suite's** quality |
| **Exploratory / ad-hoc testing** | Unscripted |
| ⭐ **TDD** | Write the failing test **before** the code (red → green → refactor) |

**Test artefacts:** test plan · test case (ID, inputs, expected output, actual output) · test suite · test harness · defect/bug report and life cycle (New → Assigned → Open → Fixed → Retest → Verified → Closed / Reopened / Deferred / Rejected).

### 6.5 ⭐ Verification vs validation
📌 ⭐ **Verification** = "Are we building the product **right**?" — reviews, inspections, walkthroughs, static analysis. **Static**, no code execution.
📌 ⭐ **Validation** = "Are we building the **right** product?" — actual testing against user needs. **Dynamic**, requires execution.

---

## 7. ⭐⭐ Implementation and maintenance

### 7.1 ⭐ Deployment / changeover strategies

| Strategy | Description | Risk |
|---|---|---|
| ⭐ **Direct / plunge / big-bang** | Old system off, new system on | ⭐ **Highest risk**, lowest cost |
| ⭐ **Parallel** | Both systems run simultaneously and results are compared | ⭐ **Lowest risk**, highest cost |
| ⭐ **Phased / staged** | Introduce module by module | Moderate |
| ⭐ **Pilot** | Deploy fully, but in **one location/group** first | Moderate; good for learning |

**Also:** user training, documentation (user manual, system manual, operations manual), data conversion/migration, site preparation.

### 7.2 ⭐⭐ Maintenance types

| Type | Trigger | ⭐ Share of effort |
|---|---|---|
| ⭐ **Corrective** | ⭐ **Fixing reported defects** | ~20% |
| ⭐ **Adaptive** | ⭐ **Changes in the ENVIRONMENT** — new OS, hardware, regulations, external interfaces | ~25% |
| ⭐ **Perfective / enhancive** | ⭐ **New/improved functionality or performance requested by users** | ⭐ **~50–65% — the LARGEST** |
| ⭐ **Preventive** | ⭐ **Restructuring/refactoring to improve future maintainability** (re-engineering, reverse engineering) | ~5% |

⚠ ⭐ **Adaptive = environment change; Perfective = enhancement; Corrective = bug fix; Preventive = future-proofing.** These four are asked constantly, usually as a scenario ("porting to a new OS is which type?" → **adaptive**).

📌 ⭐ **Maintenance consumes 60–70% of total software life-cycle cost** — more than development.
📌 **Software does not "wear out" but it does deteriorate** — repeated changes increase entropy (⭐ **Lehman's laws** of continuing change and increasing complexity).
⭐ **Legacy system options:** scrap · continue maintaining · **re-engineer** · replace.
**Reverse engineering** recovers design from code; **re-engineering** restructures and rewrites; **forward engineering** builds anew.

### 7.3 ⭐ Software quality

⭐ **McCall's / ISO 9126 quality factors:** ⭐ **functionality · reliability · usability · efficiency · maintainability · portability**

⭐ **CMM / CMMI — the five maturity levels (memorise the order and names):**

| Level | Name | Characteristic |
|---|---|---|
| ⭐ **1** | ⭐ **Initial** | ⭐ **Ad-hoc, chaotic; success depends on individual heroics** |
| ⭐ **2** | ⭐ **Repeatable / Managed** | Basic project management; ⭐ **past successes can be repeated** |
| ⭐ **3** | ⭐ **Defined** | ⭐ **Documented, standardised organisation-wide process** |
| ⭐ **4** | ⭐ **Managed / Quantitatively Managed** | ⭐ **Process and product are MEASURED and quantitatively controlled** |
| ⭐ **5** | ⭐ **Optimising** | ⭐ **Continuous process improvement**, defect prevention, innovation |

⚠ There is no "level 0", and level 1 requires no key process areas.

**Other standards:** ISO 9001 · ISO/IEC 25010 · Six Sigma · **SQA (Software Quality Assurance)** — process-oriented, preventive — vs **SQC (Quality Control)** — product-oriented, detective.
⭐ **Reliability metrics:** **MTTF** (mean time to failure) · **MTTR** (mean time to repair) · **MTBF = MTTF + MTTR** · 📌 **Availability = MTTF/(MTTF + MTTR) × 100%**

---

# PART B — COMPILER DESIGN

## 8. ⭐⭐ Phases of a compiler

| # | Phase | Input | Output |
|---|---|---|---|
| ⭐ **1** | ⭐ **Lexical analysis (scanning)** | Character stream | ⭐ **Token stream** |
| ⭐ **2** | ⭐ **Syntax analysis (parsing)** | Tokens | ⭐ **Parse tree / syntax tree** |
| ⭐ **3** | ⭐ **Semantic analysis** | Parse tree | Annotated tree; ⭐ **type checking** |
| 4 | **Intermediate code generation** | Annotated tree | ⭐ **Three-address code** |
| 5 | **Code optimisation** | Intermediate code | Optimised intermediate code |
| 6 | **Target code generation** | Optimised IR | Assembly/machine code |

📌 ⭐ **Memorise the order: Lexical → Syntax → Semantic → Intermediate code → Optimisation → Code generation.**

⭐ **Front end** = phases 1–4 (source-language dependent, machine independent).
⭐ **Back end** = phases 5–6 (machine dependent).
⭐ This split is why one front end can serve many targets, and one back end many languages.

**Two supporting components spanning all phases:** ⭐ **symbol table manager** and ⭐ **error handler**.

⭐⭐ **Which phase detects which error — a guaranteed question:**

| Error | ⭐ Detected by |
|---|---|
| Invalid character, malformed number/identifier (`12abc`) | ⭐ **Lexical analysis** |
| Missing semicolon, unbalanced parentheses, wrong statement structure | ⭐ **Syntax analysis** |
| ⭐ **Undeclared variable**, ⭐ **type mismatch**, wrong number of arguments, multiple declaration | ⭐ **Semantic analysis** |
| Array index out of bounds, division by zero, null dereference | **Run time** |

⚠ ⭐ **An undeclared variable is a SEMANTIC error, not syntactic.** The lexer happily tokenises the name and the parser accepts the grammar — only semantic analysis consults the symbol table.

### 8.1 Related terms

| Term | Meaning |
|---|---|
| ⭐ **Compiler** | Translates the **whole program** before execution; faster execution, errors reported all at once |
| ⭐ **Interpreter** | Translates and executes **statement by statement**; slower, but easier debugging and portable |
| **Assembler** | Assembly → machine code |
| **Linker** | Combines object modules and resolves external references |
| **Loader** | Loads the executable into memory |
| **Preprocessor** | Macro expansion, file inclusion (runs before the compiler) |
| **Cross compiler** | Runs on one machine, generates code for another |
| **Pass** | One complete traversal of the source/IR. A **single-pass** compiler is fast but limits optimisation |
| **Bootstrapping** | Writing a compiler for a language in that language |

⭐ **Symbol table:** stores identifier name, type, scope, memory offset, size, and (for functions) parameter details. Implemented with hash tables (usual), linked lists or trees. Used from lexical analysis through code generation.

---

## 9. ⭐ Lexical analysis

📌 The scanner groups characters into **tokens**, strips whitespace and comments, expands macros, and records identifiers in the symbol table.

⭐ **Three key terms:**

| Term | Meaning | Example |
|---|---|---|
| ⭐ **Token** | The **category** | `identifier`, `keyword`, `operator`, `constant`, `punctuation` |
| ⭐ **Lexeme** | The **actual character sequence** matched | `count`, `while`, `+`, `42` |
| ⭐ **Pattern** | The **rule** describing the lexeme set | `letter(letter|digit)*` |

🔢 In `int x = 10;` the tokens are: `keyword(int)`, `id(x)`, `operator(=)`, `constant(10)`, `punct(;)` — **5 tokens**.

📌 ⭐ **Lexical analysis is specified with REGULAR EXPRESSIONS and implemented with FINITE AUTOMATA (DFA).**
⚠ Regular expressions are sufficient for tokens but **cannot** express nested/balanced constructs — that needs a CFG and a pushdown automaton, which is why syntax analysis is a separate phase.

⭐ **Longest-match (maximal munch) rule:** the scanner takes the **longest** possible lexeme. This is why `>=` is one token, not `>` followed by `=`, and why `elsex` is an identifier rather than `else` + `x`.
**Rule priority:** among equal-length matches, the rule listed first wins (so keywords beat identifiers).

**Tools:** `lex` / `flex` generate a scanner from a regular-expression specification.
**Input buffering:** two-buffer scheme with sentinels reduces I/O.

---

## 10. ⭐⭐ Syntax analysis (parsing)

### 10.1 Context-free grammars
📌 **G = (V, T, P, S)** — variables/non-terminals, terminals, productions, start symbol.
**Derivations:** leftmost/rightmost; **sentential forms**; **parse tree** (concrete) vs **abstract syntax tree** (operators as internal nodes, no redundant punctuation).

⭐ **Ambiguous grammar:** some string has **more than one parse tree** (equivalently, more than one leftmost derivation).
🔢 `E → E + E | E * E | id` is ambiguous — `id + id * id` has two parse trees. Fixed by introducing precedence levels and associativity:
```
E → E + T | T        (+ left-associative, lower precedence)
T → T * F | F        (* left-associative, higher precedence)
F → ( E ) | id
```
⭐ **The dangling-else problem** is the classic ambiguity: `if C1 then if C2 then S1 else S2` — the `else` is conventionally matched to the **nearest unmatched `then`**.
⚠ Ambiguity is a property of the **grammar**, not the language; some languages are **inherently ambiguous** (no unambiguous grammar exists).

### 10.2 ⭐ Grammar transformations for top-down parsing

⭐ **Left recursion elimination** — required, because `A → Aα` makes a recursive-descent parser loop forever.
📌 Replace `A → Aα | β` with:
```
A  → β A'
A' → α A' | ε
```
🔢 `E → E + T | T` becomes `E → T E'` and `E' → + T E' | ε`.

⭐ **Left factoring** — required when two productions share a prefix, so the parser cannot choose on one lookahead token.
📌 Replace `A → αβ₁ | αβ₂` with `A → αA'` and `A' → β₁ | β₂`.

⚠ ⭐ **Bottom-up (LR) parsers actually PREFER left recursion** — they handle it naturally and it keeps the stack shallow. Only top-down parsers need it removed.

### 10.3 ⭐⭐ FIRST and FOLLOW sets

📌 ⭐ **FIRST(α)** = the set of terminals that can begin a string derived from α (plus ε if α ⇒* ε).
**Rules:** FIRST(terminal a) = {a}. For `A → X₁X₂…Xₙ`: add FIRST(X₁) minus ε; if X₁ ⇒* ε, also add FIRST(X₂), and so on; if all can derive ε, add ε.

📌 ⭐ **FOLLOW(A)** = the set of terminals that can appear **immediately to the right of A** in some derivation.
**Rules:**
1. ⭐ **FOLLOW(start symbol) contains `$`** (end of input).
2. For `A → αBβ`: add FIRST(β) minus ε to FOLLOW(B).
3. For `A → αB`, or `A → αBβ` where β ⇒* ε: add **FOLLOW(A)** to FOLLOW(B).

⚠ ⭐ **ε is never in a FOLLOW set** (but `$` can be). ε can be in a FIRST set.

🔢 **Grammar:** `E → T E'` · `E' → + T E' | ε` · `T → F T'` · `T' → * F T' | ε` · `F → ( E ) | id`

| Non-terminal | FIRST | FOLLOW |
|---|---|---|
| E | { (, id } | { ), $ } |
| E' | { +, ε } | { ), $ } |
| T | { (, id } | { +, ), $ } |
| T' | { *, ε } | { +, ), $ } |
| F | { (, id } | { *, +, ), $ } |

**This is the standard example — work it through by hand until you can reproduce it.**

### 10.4 ⭐ Top-down parsing

| Parser | Note |
|---|---|
| **Recursive descent (with backtracking)** | One function per non-terminal; backtracking is inefficient |
| ⭐ **Predictive parser / LL(1)** | ⭐ **No backtracking**; uses one lookahead token and a parsing table |

📌 ⭐ **LL(1):** **L**eft-to-right scan, **L**eftmost derivation, **1** lookahead token.

⭐ **LL(1) parsing table construction:** for each production `A → α`:
- For each terminal a in FIRST(α), set **M[A, a] = A → α**.
- If ε ∈ FIRST(α), then for each b in **FOLLOW(A)**, set **M[A, b] = A → α**.

⭐ **A grammar is LL(1) ⟺ no table entry has two productions.** Equivalently, for `A → α | β`:
1. FIRST(α) ∩ FIRST(β) = ∅
2. If β ⇒* ε, then FIRST(α) ∩ FOLLOW(A) = ∅

⚠ ⭐ **An ambiguous or left-recursive grammar can NEVER be LL(1).**

### 10.5 ⭐⭐ Bottom-up parsing (shift-reduce / LR)

📌 Builds the parse tree from the leaves upward; produces a **rightmost derivation in reverse**.

⭐ **Four actions:** ⭐ **shift** (push the next input token) · ⭐ **reduce** (replace a handle on the stack with its non-terminal) · **accept** · **error**.
📌 ⭐ **Handle** = a substring matching the right side of a production whose reduction is a step in the reverse rightmost derivation.

⭐ **LR(k):** **L**eft-to-right scan, **R**ightmost derivation in reverse, **k** lookahead.

⭐⭐ **The power hierarchy — memorise it:**

📌 ⭐ **LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1) [= LR(1)]**

| Parser | Item type | Lookahead used for reduction | States | Note |
|---|---|---|---|---|
| **LR(0)** | LR(0) items | None | Fewest | Weakest |
| ⭐ **SLR(1)** | LR(0) items | ⭐ **FOLLOW set** of the non-terminal | Same as LR(0) | Simple LR |
| ⭐ **LALR(1)** | LR(1) items, ⭐ **merged states with identical cores** | Merged lookaheads | ⭐ **Same as SLR** | ⭐ **Used by `yacc`/`bison`** — best power/size trade-off; merging can introduce ⭐ **reduce–reduce** conflicts but never shift–reduce conflicts |
| ⭐ **CLR(1)** | LR(1) items | ⭐ **Exact lookahead** per item | ⭐ **Most** | Most powerful, largest tables |

⭐ **Number of states:** SLR = LALR ≤ CLR. (SLR and LALR have identical state counts; CLR generally has more.)

⭐ **Conflicts:**
- ⭐ **Shift–reduce conflict:** the parser can either shift or reduce (e.g. the dangling else).
- ⭐ **Reduce–reduce conflict:** two different reductions are possible.

⭐ **Comparison of the two approaches:**

| | **LL (top-down)** | **LR (bottom-up)** |
|---|---|---|
| Derivation | Leftmost | ⭐ **Rightmost in reverse** |
| Tree built | Root → leaves | ⭐ **Leaves → root** |
| Left recursion | ⭐ **Must be removed** | ⭐ **Handled naturally** |
| Left factoring | Required | Not required |
| Power | Weaker | ⭐ **Stronger** |
| Hand-coding | Easier | Harder (use a generator) |

⭐ **Operator precedence parsing:** a simple bottom-up technique using a precedence relation table; cannot handle ε-productions or unary minus ambiguity.

**Parser generators:** `yacc`/`bison` (LALR(1)), ANTLR (LL(*)).

---

## 11. ⭐ Syntax-directed translation (SDT)

📌 A **syntax-directed definition (SDD)** attaches **attributes** to grammar symbols and **semantic rules** to productions.

⭐⭐ **Two attribute kinds:**

| | ⭐ **Synthesized** | ⭐ **Inherited** |
|---|---|---|
| Computed from | ⭐ **The node's CHILDREN** | ⭐ **The node's PARENT and/or SIBLINGS** |
| Information flows | ⭐ **Upward** | ⭐ **Downward/sideways** |
| Evaluated by | ⭐ **Bottom-up** traversal | Top-down / mixed |

⭐ **S-attributed definition:** uses **only synthesized** attributes → can be evaluated in a **single bottom-up pass**, so it works with LR parsers and `yacc`.
⭐ **L-attributed definition:** each inherited attribute of a symbol depends only on the parent and on **siblings to its LEFT** → can be evaluated in a **single left-to-right depth-first pass**, so it works with LL parsers.

📌 ⭐ **Every S-attributed definition is L-attributed, but not conversely.**

⭐ **Terminals only ever have synthesized attributes** (supplied by the lexer, e.g. `id.lexval`).
**Annotated parse tree:** a parse tree with attribute values filled in. **Dependency graph:** shows attribute evaluation order; it must be **acyclic**.
**Translation scheme:** an SDD with semantic **actions** embedded at specific positions in the production body.

🔢 Classic S-attributed example: `E → E₁ + T { E.val = E₁.val + T.val }` — `val` is synthesized.
🔢 Classic inherited example: `D → T L { L.type = T.type }` — the declaration type flows **down** into the identifier list.

---

## 12. ⭐ Intermediate code generation

⭐ **Why an intermediate representation?** Machine independence, easier optimisation, and **m + n** translators instead of **m × n** for m languages and n targets (retargetability).

### 12.1 ⭐ Three-address code (TAC)
📌 Each instruction has **at most one operator and at most three addresses** (usually: result, operand1, operand2), using **temporaries** for intermediate values.

🔢 `a = b * c + b * d` becomes:
```
t1 = b * c
t2 = b * d
t3 = t1 + t2
a  = t3
```

**Instruction forms:** `x = y op z` · `x = op y` · `x = y` · `goto L` · `if x relop y goto L` · `param x` / `call p, n` / `return y` · `x = y[i]` / `x[i] = y` · `x = &y` / `x = *y` / `*x = y`.

### 12.2 ⭐ Implementations of TAC

| Representation | Structure | Note |
|---|---|---|
| ⭐ **Quadruples** | `(op, arg1, arg2, result)` | ⭐ **Explicit temporary names → instructions can be MOVED/reordered easily** (best for optimisation); uses more space |
| ⭐ **Triples** | `(op, arg1, arg2)` — the result is referenced by the triple's **position/index** | Compact, but ⭐ **moving an instruction breaks all references** |
| ⭐ **Indirect triples** | Triples plus a separate **list of pointers** giving the order | ⭐ **Compact AND reorderable** — the best of both |

⚠ ⭐ **Quadruples are easiest to reorder; plain triples are not.** That trade-off is the exam point.

### 12.3 Other IRs
**Syntax tree / AST** · ⭐ **DAG (Directed Acyclic Graph)** — like a syntax tree but with **common subexpressions shared**, so it exposes redundancy directly · postfix notation · **SSA (Static Single Assignment)** — each variable assigned exactly once, simplifying data-flow analysis · bytecode.

🔢 For `a = b * c + b * c`, the DAG has a **single** `b * c` node with two parents — immediately revealing the common subexpression.

**Backpatching:** fills in jump targets for boolean expressions and control flow whose destinations are not yet known, avoiding a second pass.

---

## 13. ⭐ Runtime environments

### 13.1 ⭐ Storage allocation

| Area | Holds | Allocation |
|---|---|---|
| **Code / text** | Machine instructions | Static |
| **Static / global** | Globals, static variables | Static (compile time) |
| ⭐ **Stack** | ⭐ **Activation records** for procedure calls | Automatic, LIFO |
| ⭐ **Heap** | Dynamically allocated data | Manual or garbage-collected |

### 13.2 ⭐ Activation record (stack frame)

⭐ **Contents (typical order):** return value · **actual parameters** · **control link** (dynamic link — caller's frame pointer) · **access link** (static link — for non-local access) · **saved machine status** (including the **return address**) · **local data** · **temporaries**.

⭐ **Created on procedure entry, destroyed on return** — which is exactly what makes recursion work: each invocation gets its own frame with its own copy of the locals.
⚠ ⭐ **The activation record is a RUN-TIME structure on the stack; the symbol table is a COMPILE-TIME structure.** A common confusion.

**Activation tree** — represents the nesting of procedure activations during a run.
**Display** — an array of frame pointers for fast non-local access with nested procedures.

### 13.3 ⭐⭐ Static vs dynamic scoping

| | ⭐ **Static (lexical) scoping** | ⭐ **Dynamic scoping** |
|---|---|---|
| A name refers to | The declaration in the **enclosing block in the SOURCE TEXT** | The declaration in the **most recent ACTIVATION on the call stack** |
| Resolved at | ⭐ **Compile time** | ⭐ **Run time** |
| Used by | ⭐ **C, C++, Java, most modern languages** | Older Lisp, some shell scripts, Perl's `local` |

🔢 ```
int x = 10;
void f() { printf("%d", x); }
void g() { int x = 20; f(); }
```
⭐ **Static scoping prints 10** (f sees the global x from its source position); **dynamic scoping would print 20** (the most recent activation's x). This exact example is a standard question.

### 13.4 ⭐⭐ Parameter passing mechanisms

| Mechanism | Semantics | Languages |
|---|---|---|
| ⭐ **Call by value** | A **copy** is passed; the caller's variable is unaffected | ⭐ **C, Java (for primitives)** |
| ⭐ **Call by reference** | The **address** is passed; changes are visible to the caller | C++ (`&`), Pascal (`var`), Fortran |
| ⭐ **Call by value-result (copy-restore)** | Copy in on entry, **copy back on return** | Ada (`in out`), Fortran variants |
| ⭐ **Call by name** | The argument **expression is substituted textually** and **re-evaluated at every use** | Algol 60 (mostly of theoretical interest) |
| **Call by sharing** | The reference value is copied (object can be mutated, not reassigned) | Java (objects), Python |

🔢 Classic distinguishing example:
```
int a = 1; int arr[] = {1, 2, 3};
void f(int x) { x = x + 1; a = a + 1; }
f(arr[a]);
```
Call by **value**: `arr[1]` (=2) is copied; `a` becomes 2; `arr` unchanged.
Call by **reference**: `arr[1]` becomes 3; `a` becomes 2.
Call by **name**: `x` is literally `arr[a]`, re-evaluated after `a` changes — so different array elements may be read and written.
⭐ **Call by name and call by value-result give different results whenever the argument is a subscripted variable whose index changes** — this is the standard exam trap.

**Garbage collection:** reference counting (simple, fails on cycles) · mark-and-sweep · copying/generational · mark-compact.

---

## 14. ⭐⭐ Code optimisation

### 14.1 Criteria
⭐ An optimisation must **preserve program meaning (semantics)**, produce a measurable improvement on average, and be worth its compilation cost.

### 14.2 ⭐ Basic blocks and flow graphs

📌 ⭐ **Basic block:** a maximal sequence of consecutive instructions with **one entry point (the first instruction) and one exit point (the last)** — no jumps in except at the start, none out except at the end.

⭐ **Identifying leaders (the first instruction of each block):**
1. The **first** instruction of the program.
2. Any instruction that is the **target of a jump**.
3. Any instruction **immediately following a jump** or conditional jump.

Each leader begins a block that extends to just before the next leader.

📌 **Control Flow Graph (CFG):** basic blocks as nodes; edges represent possible control transfer. **Loops** appear as strongly connected subgraphs with a single entry (**header**).

### 14.3 ⭐⭐ Optimisation techniques

| Technique | Description | Example |
|---|---|---|
| ⭐ **Constant folding** | Evaluate **constant expressions at compile time** | `x = 4 * 3` → `x = 12` |
| ⭐ **Constant propagation** | Replace a **variable** known to hold a constant with that constant | `a = 5; b = a + 2;` → `b = 5 + 2` → `b = 7` |
| ⭐ **Common Subexpression Elimination (CSE)** | Reuse a previously computed identical expression | `t = b*c; x = t + d; y = t + e;` |
| ⭐ **Dead code elimination** | Remove code whose result is **never used**, or which is unreachable | `x = 5;` when x is never read again |
| ⭐ **Copy propagation** | After `x = y`, use `y` in place of `x` | Enables further dead-code removal |
| ⭐ **Strength reduction** | Replace an expensive operation with a cheaper one | `x * 2` → `x << 1`; `x²` → `x * x`; multiplication in a loop → addition |
| ⭐ **Code motion / loop-invariant code motion** | Move computations that do not change inside a loop **out of** the loop | Hoisting |
| **Induction variable elimination** | Simplify variables that change by a fixed amount per iteration | |
| **Loop unrolling** | Replicate the loop body to cut loop-control overhead | Trades size for speed |
| **Loop fusion / jamming** | Merge adjacent loops with the same bounds | |
| **Loop invariant / unswitching** | | |
| **Function inlining** | Replace a call with the body | Removes call overhead |
| **Tail recursion elimination** | Convert tail recursion into a loop | Avoids stack growth |
| **Algebraic simplification** | `x + 0` → `x`; `x * 1` → `x`; `x * 0` → `0` | |
| **Peephole optimisation** | Local, sliding-window improvements on target code: redundant load/store elimination, unreachable code, flow-of-control optimisation, algebraic simplification, machine idioms | |

⚠ ⭐ **Constant folding vs constant propagation:** folding evaluates a constant **expression**; propagation substitutes a constant **value for a variable**. They are usually applied together and are constantly confused.

⭐ **Scope of optimisation:**
- ⭐ **Local optimisation** — within a **single basic block** (this is what the syllabus names).
- **Global optimisation** — across basic blocks within a procedure (requires data-flow analysis).
- **Interprocedural** — across procedures.
- **Machine-dependent** (register allocation, instruction scheduling, peephole) vs **machine-independent**.

⭐ **Register allocation:** minimise memory traffic by keeping hot values in registers. Solved by **graph colouring** on the **register interference graph** (built from liveness information); values that cannot be coloured are **spilled** to memory.

---

## 15. ⭐⭐ Data flow analysis

📌 Gathers information about how data flows along the paths of a control flow graph — the foundation for global optimisation. Solved iteratively to a **fixed point** using equations of the form
📌 **OUT[B] = GEN[B] ∪ (IN[B] − KILL[B])**

### 15.1 ⭐ The three analyses named in the syllabus

⭐ **(a) Reaching definitions** — *which definitions of a variable may reach this point?*
- Direction: ⭐ **forward** · Meet operator: ⭐ **union (∪)** — a "may" (existential) property
- 📌 `OUT[B] = GEN[B] ∪ (IN[B] − KILL[B])`; `IN[B] = ∪ OUT[P]` over predecessors P
- **Enables:** constant propagation, copy propagation, detecting use of possibly-uninitialised variables

⭐ **(b) Liveness analysis (live variable analysis)** — *is this variable's current value used again later on some path?*
📌 ⭐ **A variable is LIVE at a point if there is a path from that point to a USE of it, with no intervening redefinition.** Otherwise it is **dead**.
- Direction: ⭐ **BACKWARD** · Meet operator: ⭐ **union (∪)** — a "may" property
- 📌 `IN[B] = USE[B] ∪ (OUT[B] − DEF[B])`; `OUT[B] = ∪ IN[S]` over successors S
- ⭐ **Enables: dead code elimination and register allocation** (two variables can share a register if they are never simultaneously live)

⭐ **(c) Available expressions** — *has this expression already been computed on every path to here, with no operand redefined since?*
- Direction: ⭐ **forward** · Meet operator: ⭐ **INTERSECTION (∩)** — a "must" (universal) property
- 📌 `IN[B] = ∩ OUT[P]` over predecessors P
- ⭐ **Enables: common subexpression elimination**

⭐⭐ **Summary table — memorise it:**

| Analysis | ⭐ Direction | ⭐ Meet operator | May/Must | Enables |
|---|---|---|---|---|
| ⭐ **Reaching definitions** | Forward | ∪ (union) | May | Constant/copy propagation |
| ⭐ **Live variables** | ⭐ **BACKWARD** | ∪ (union) | May | ⭐ **Dead code elimination, register allocation** |
| ⭐ **Available expressions** | Forward | ⭐ **∩ (intersection)** | Must | ⭐ **CSE** |
| **Very busy / anticipated expressions** | Backward | ∩ | Must | Code hoisting |

⚠ ⭐ **Liveness is the backward one; available expressions is the intersection one.** Those two facts carry most of the marks in this topic.

🔢 **Liveness example:**
```
1: x = 1        // x defined
2: y = x + 2    // x used → x live at 1..2
3: x = 5        // x redefined; old x now dead
4: z = y        // y used → y live at 2..4
5: print z
```
After line 2, the value assigned at line 1 is dead. `y` is live from line 2 to line 4.

**Other concepts:** `u-d` chains (use-definition) and `d-u` chains · **dominators** (node A dominates B if every path from entry to B goes through A) · natural loops and back edges · **SSA form** (simplifies all of the above).

---

## 16. Rapid-fire facts ⭐

### Software Engineering

| Fact | Value |
|---|---|
| Level-0 DFD | Context diagram (whole system as one process) |
| DFD does NOT show | Control flow, decisions, timing |
| DFD symbols | Process, data flow, data store, external entity |
| DFD rule | No direct entity→entity or store→store flow |
| Balancing | Inputs/outputs match between levels |
| Risk-driven model | Spiral |
| Testing mirrors development | V-model |
| No working software until late | Waterfall |
| Requirements unclear → use | Prototyping |
| SRS produced in | Requirement analysis phase |
| "Response < 2 s" | Non-functional requirement |
| TELOS | Technical, Economic, Legal, Operational, Schedule |
| Language-independent size metric | Function points |
| COCOMO organic | E = 2.4(KLOC)^1.05 |
| COCOMO modes | Organic, semi-detached, embedded |
| PERT expected time | (t_o + 4t_m + t_p)/6 |
| Critical path | **Longest** path; zero slack |
| PERT vs CPM | Probabilistic vs deterministic |
| Gantt chart shows | Duration, not dependencies |
| Best / worst cohesion | Functional / coincidental |
| Best / worst coupling | Data / content |
| Design goal | High cohesion, low coupling |
| Cyclomatic complexity | E − N + 2 = predicates + 1 |
| BVA, equivalence partitioning | Black-box |
| Statement/branch/path coverage | White-box |
| Coverage strength | Statement < branch < condition < path |
| Top-down integration needs | **Stubs** |
| Bottom-up integration needs | **Drivers** |
| Alpha / beta testing | Developer's site / customer's site |
| Re-run tests after a change | Regression testing |
| Load vs stress | At limits vs beyond limits |
| Verification / validation | Right way / right product |
| Porting to a new OS | **Adaptive** maintenance |
| Adding a requested feature | **Perfective** maintenance |
| Largest maintenance share | Perfective (~50–65%) |
| Maintenance share of lifecycle cost | 60–70% |
| CMM level 3 / 5 | Defined / Optimising |
| Availability | MTTF/(MTTF+MTTR) |
| Lowest-risk changeover | Parallel |
| Scrum sprint length | 2–4 weeks |

### Compiler Design

| Fact | Value |
|---|---|
| Phase order | Lexical → syntax → semantic → ICG → optimise → codegen |
| Front end / back end | Phases 1–4 / 5–6 |
| Undeclared variable error | **Semantic** |
| Missing semicolon | Syntax |
| `12abc` | Lexical |
| Lexical analysis specified by | Regular expressions → DFA |
| Longest-match rule | Maximal munch |
| Token vs lexeme | Category vs actual text |
| Left recursion | Must be removed for LL, fine for LR |
| ε in FOLLOW sets | Never (but `$` can be) |
| FOLLOW(start) contains | `$` |
| LL(1) | Left-to-right, leftmost, 1 lookahead |
| Ambiguous grammar is LL(1)? | Never |
| Bottom-up produces | Rightmost derivation in reverse |
| Parser power order | LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1) |
| yacc/bison uses | LALR(1) |
| Same number of states | SLR and LALR |
| Synthesized attribute | From children (bottom-up) |
| Inherited attribute | From parent/siblings |
| S-attributed | Only synthesized; single bottom-up pass |
| Terminals have | Only synthesized attributes |
| Easiest TAC form to reorder | Quadruples |
| Compact and reorderable | Indirect triples |
| Shares common subexpressions | DAG |
| Run-time call info stored in | Activation record (stack) |
| C uses | Static scoping, call by value |
| `x = 4*3` → `x = 12` | Constant folding |
| `a=5; b=a+2` → `b=5+2` | Constant propagation |
| `x*2` → `x<<1` | Strength reduction |
| Basic block | One entry, one exit |
| Liveness analysis direction | **Backward**, union |
| Available expressions | Forward, **intersection** |
| Reaching definitions | Forward, union |
| Liveness enables | Dead code elimination, register allocation |
| Register allocation via | Graph colouring |

---

## 17. Common traps ⚠

**Software Engineering**
1. ⭐ **Top-down needs stubs; bottom-up needs drivers.**
2. ⭐ **Functional cohesion is best, coincidental worst; data coupling best, content worst.**
3. ⭐ **Critical path is the LONGEST path.**
4. ⭐ **Adaptive = environment change; perfective = enhancement.**
5. **Verification = building it right; validation = building the right thing.**
6. **Level-0 DFD = context diagram, and shows no data stores.**
7. **A DFD shows no control flow or sequence.**
8. **100% statement coverage ≠ 100% branch coverage.**
9. **Alpha at the developer's site, beta at the customer's.**
10. **CMM level 4 is "Managed/Quantitative", level 5 is "Optimising"** — do not stop at 4.
11. **Spiral is risk-driven; V-model mirrors testing.**
12. **Function points are language-independent; LOC is not.**

**Compiler Design**
13. ⭐ **Undeclared variables and type mismatches are SEMANTIC errors.**
14. ⭐ **ε is never in a FOLLOW set.**
15. ⭐ **LR parsers handle left recursion; LL parsers cannot.**
16. ⭐ **LALR has the same number of states as SLR**, not as CLR.
17. **LALR merging can create reduce–reduce conflicts, never shift–reduce.**
18. ⭐ **Liveness analysis is BACKWARD.**
19. ⭐ **Available expressions uses INTERSECTION**, not union.
20. **Constant folding ≠ constant propagation.**
21. **Quadruples are reorderable; plain triples are not.**
22. **The activation record is run-time; the symbol table is compile-time.**
23. **Static scoping resolves by source text, dynamic by call stack.**

---

## 18. Practice

**Software Engineering** — ⭐ **the biggest untapped block in Paper-II:**
- [`Paper2_S10_Information_Systems_and_Software_Engineering/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S10_Information_Systems_and_Software_Engineering/) — ⭐ **337 questions** (ISRO 52 + NIELIT 70 + UGC-NET 215)
- ⚠ **Zero GATE coverage.** If you only have time for one folder this week, it is this one.

**Compiler Design:**
- GATE: [`Paper2_S07_Compiler_Design/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S07_Compiler_Design/) — **242 questions**
- State-PSC level: [`Paper2_S07_Compiler_Design/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S07_Compiler_Design/) — **170 questions**
- ⚠ **Skip automata-heavy questions** — Theory of Computation is **not** in the TPSC syllabus. You need only the CFG/parsing background.

Test: [`Week_11_Test.md`](../04_Mock_Tests/Week_11_Test.md)

**Priority order if short on time:**
**SE** — cohesion/coupling orderings → maintenance types → black-box vs white-box techniques → stubs vs drivers → process models (spiral/V/waterfall identification) → CMM levels → cyclomatic complexity → COCOMO modes → critical path → DFD rules.
**Compiler** — phase order and which phase catches which error → FIRST/FOLLOW → LR power hierarchy → synthesized vs inherited attributes → the named optimisations → the data-flow analysis summary table.
