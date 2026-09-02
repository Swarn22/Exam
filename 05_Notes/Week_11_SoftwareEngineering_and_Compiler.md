# Week 11 — Information Systems & Software Engineering + Compiler Design

**Syllabus §10:** Information gathering, requirement and feasibility analysis, data flow diagrams, process specifications, input/output design, process life cycle, planning and managing the project, design, coding, testing, implementation, maintenance.
**Syllabus §7:** Lexical analysis, parsing, syntax-directed translation. Runtime environments. Intermediate code generation. Local optimization. Data flow analyses: constant propagation, liveness analysis, common subexpression elimination.

**Estimated marks: ~8 + ~6 = ~14**

---

## 💡 Why Part A deserves your time

⭐ **Software Engineering has ZERO GATE coverage but 337 questions in the state-PSC corpus** (ISRO 52 + NIELIT 70 + UGC-NET 215).

It is the **largest untapped block in Paper-II**, it is entirely **definitional**, and it needs no mathematics. If you are short of time this week, do Part A first.

---

# PART A — INFORMATION SYSTEMS & SOFTWARE ENGINEERING

## 💡 What software engineering is

Writing a 200-line program alone is **programming**. Building a system of 200,000 lines with 30 people over two years, which must still be maintainable in a decade, is **software engineering** — and it needs process, not just coding skill.

⭐ **The historical motivation ("the software crisis", 1968):** projects were routinely late, over budget, and delivered software that did not work. Studies found that most defects originated in **requirements**, not code — and that the **cost of fixing a defect rises roughly tenfold at each later stage**:

```
Requirements  →  Design  →  Coding  →  Testing  →  Production
    ₹1            ₹10        ₹100      ₹1,000      ₹10,000
```

⭐ **That cost curve explains almost every practice in this section** — why you write an SRS before coding, why you review designs, why testing is layered, and why "shift left" is the modern watchword.

---

## 1. ⭐ Information gathering and system analysis

## 1.1 ⭐ Fact-finding techniques

### 💡 The idea

Before building anything, you must find out what the users actually need — and users are notoriously bad at articulating that. Hence several complementary techniques.

| Technique | ⭐ Best for | 💡 Note |
|---|---|---|
| ⭐ **Interviews** | Depth, follow-up, clarification | Structured / unstructured / semi-structured. Rich but **time-consuming** |
| ⭐ **Questionnaires** | Many respondents, quantitative data | Cheap at scale, but **low response rates** and **no ability to probe** |
| ⭐ **Observation** | Seeing what people **actually do** | ⭐ Reveals the gap between what users *say* they do and what they *really* do. ⚠ Suffers the **Hawthorne effect** — people behave differently when watched |
| ⭐ **Record / document review** | Existing forms, reports, procedures | Factual and historical; shows the real data volumes |
| **JAD (Joint Application Development)** | Fast consensus | Facilitated workshops with users and developers together |
| **Prototyping** | Unclear requirements | Show something concrete and let users react |
| Brainstorming, site visits, background reading | | |

⭐ **Best practice is to combine them:** interview to understand, observe to verify, review records to quantify.

## 1.2 ⭐ Types of information system

### 💡 The idea

Different levels of an organisation need different information. An operator needs today's transactions; a director needs five-year trends.

| System | Serves | ⭐ Purpose |
|---|---|---|
| **TPS** (Transaction Processing System) | Operational staff | Records **day-to-day transactions** (sales, bookings) |
| ⭐ **MIS** (Management Information System) | Middle management | ⭐ **ROUTINE summary and exception REPORTS** from TPS data |
| ⭐ **DSS** (Decision Support System) | Management | ⭐ **SEMI-STRUCTURED, non-routine decisions** — what-if analysis, models, simulations |
| ⭐ **EIS / ESS** (Executive Support System) | Top management | **Strategic dashboards**, external data, drill-down |
| **ERP** | The whole enterprise | Integrated cross-functional system |
| **KMS, OAS, Expert Systems** | | Knowledge, office automation, rule-based advice |

⚠⚠ ⭐ **MIS vs DSS — a standard comparison.** MIS produces **predefined, routine reports**; DSS supports **ad-hoc analytical decisions** with models and what-if capability.

🔢 "Monthly sales by region" → **MIS**. "What happens to profit if we cut price 8% and demand rises 15%?" → **DSS**.

## 1.3 ⭐⭐ Requirements

### 💡 The two kinds

📌 ⭐ **FUNCTIONAL requirements** — *what* the system must **do**. Features, computations, data processing, use cases.
📌 ⭐ **NON-FUNCTIONAL requirements (NFRs)** — *how well* it does it. ⭐ **Performance, reliability, availability, security, usability, scalability, maintainability, portability**, plus legal/regulatory compliance.

### 🔢 Classify these — the standard exam format

| Requirement | ⭐ Type |
|---|---|
| "The system shall allow a user to reset their password" | ⭐ **Functional** |
| "Response time must be under 2 seconds for 95% of requests" | ⭐ **NON-functional** (performance) |
| "The system shall be available 99.9% of the time" | ⭐ **NON-functional** (availability) |
| "The system shall generate a monthly sales report" | **Functional** |
| "All passwords shall be stored using bcrypt" | **NON-functional** (security) |
| "The interface shall be usable by a clerk after 30 minutes of training" | **NON-functional** (usability) |

⭐ **The test: if it describes a FEATURE, it is functional. If it describes a QUALITY or CONSTRAINT, it is non-functional.**

### ⭐ The requirements process

**Elicitation → Analysis → Specification → VALIDATION → Management**

⚠⚠ ⭐ **Verification vs validation — asked in both this section and the testing section:**
📌 ⭐ **VERIFICATION: "Are we building the product RIGHT?"** — does it match the specification? (Reviews, inspections, static analysis. **No code execution.**)
📌 ⭐ **VALIDATION: "Are we building the RIGHT product?"** — does it meet the user's actual need? (Actual testing. **Requires execution.**)

💡 You can build something perfectly to a specification that was wrong all along — that passes verification and fails validation.

### ⭐⭐ The SRS

📌 ⭐ **SRS (Software Requirements Specification)** — the output of the requirements phase. It is the **contract** between customer and developer, and the **baseline** for design and testing.

⭐ **Characteristics of a good SRS — asked directly:**
📌 ⭐ **Complete · Consistent · Unambiguous · Verifiable/testable · Traceable · Modifiable · Ranked for importance and stability · Correct**

💡 **Why "verifiable" matters most in practice:** "the system shall be user-friendly" is **not** verifiable — you cannot write a test for it. "A trained clerk shall complete a booking in under 90 seconds" is.

## 1.4 ⭐ Feasibility study

### 💡 The idea

Before committing money, ask whether the project is possible **at all** — along five independent dimensions.

| Type | ⭐ The question |
|---|---|
| ⭐ **Technical** | Can it be built with available technology and skills? |
| ⭐ **Economic / financial** | Do the benefits justify the cost? (⭐ **cost–benefit analysis**, ROI, NPV, payback period) |
| ⭐ **Operational** | Will the organisation and its users **actually use** it? |
| ⭐ **Schedule** | Can it be delivered in time to be useful? |
| ⭐ **Legal** | Does it comply with laws, contracts and regulations? |

⭐ **Mnemonic: TELOS** — **T**echnical, **E**conomic, **L**egal, **O**perational, **S**chedule.

💡 ⭐ **Operational feasibility is the one people forget** — and the most common cause of expensive failure. A technically perfect system that staff refuse to use has failed completely.

---

## 2. ⭐⭐⭐ Data Flow Diagrams (DFD)

### 💡 What a DFD is

📌 A DFD is the central tool of **structured analysis**. It shows **how DATA MOVES through a system** — where it comes from, what transforms it, where it is stored, and where it goes.

⭐ **What it shows:** *what* the system does with data.
⚠⚠ ⭐ **What it does NOT show: CONTROL FLOW, DECISIONS, LOOPS, or TIMING/SEQUENCE.**

💡 **Why not:** a DFD is deliberately a *data* model, not a *procedural* one. It says "these two processes both receive customer data" without implying which runs first. ⭐ **For event and timing behaviour you need a separate STATE TRANSITION DIAGRAM.**

⭐ **This limitation is the most-asked DFD question.**

## 2.1 ⭐⭐ The four symbols

| Symbol | Yourdon/DeMarco | Gane–Sarson | ⭐ Meaning |
|---|---|---|---|
| ⭐ **Process** | Circle / bubble | Rounded rectangle | ⭐ **TRANSFORMS input data into output** |
| ⭐ **Data flow** | Labelled arrow | Labelled arrow | ⭐ **Data in MOTION** |
| ⭐ **Data store / warehouse** | Two parallel lines | Open-ended rectangle | ⭐ **Data at REST** |
| ⭐ **External entity / terminator** | Rectangle | Square | ⭐ **A source or sink OUTSIDE the system boundary** |

⭐ Only four symbols exist — that is the whole notation.

## 2.2 ⭐⭐⭐ Levels

| Level | ⭐ Name | ⭐ Content |
|---|---|---|
| ⭐ **Level 0** | ⭐ **CONTEXT DIAGRAM** | ⭐ **The ENTIRE SYSTEM as ONE single process**, with all external entities and the data flows between them. ⭐ **NO data stores are shown** |
| **Level 1** | Top level | The main sub-processes (typically **3–7**) |
| **Level 2, 3…** | Detailed | Progressive decomposition of individual processes |

```
Level 0 (context):
    [Customer] ──order──►( 0. Order System )──invoice──►[Customer]
                                │
                          ──report──►[Management]

Level 1:
    [Customer] ──order──►(1. Validate)──►(2. Process)──►(3. Invoice)──►[Customer]
                                              ↕
                                        ═ Order File ═
```

⭐ **The rules:**

📌 ⭐ **BALANCING:** the inputs and outputs of a process at level n must **match exactly** the net inputs and outputs of its expansion at level n+1. If level 0 shows two inputs, the level-1 expansion must show the same two.

📌 ⭐ **Every process must have at least one input AND one output.** Violations have memorable names:
- ⚠ ⭐ **BLACK HOLE** — a process with inputs but **no output**
- ⚠ ⭐ **MIRACLE** — a process with outputs but **no input**
- ⚠ ⭐ **GREY HOLE** — output that could not possibly be produced from the given input

📌 ⭐ **Forbidden data flows — data cannot flow DIRECTLY between:**
- ⭐ two **external entities**
- ⭐ two **data stores**
- ⭐ a **data store and an external entity**
⭐ **Every such flow must pass THROUGH a process.**

💡 **Why:** the DFD models *your system*. Two external entities talking to each other is outside your system; and data does not move from one store to another by itself — some process must move it.

📌 **Numbering:** level-1 processes are 1, 2, 3; their children are 1.1, 1.2, 2.1…

## 2.3 ⭐ Supporting tools

| Tool | ⭐ Purpose |
|---|---|
| ⭐ **Process specification (mini-spec)** | Describes the **logic** of a **primitive** (undecomposed) process — via structured English, pseudocode, decision tables or decision trees |
| ⭐ **Data dictionary** | Defines **every data element and structure**: name, aliases, type, length, permitted values, composition |
| ⭐ **Decision table** | Condition stubs + action stubs. 📌 ⭐ **For n binary conditions there are 2ⁿ rules/columns** |
| **Decision tree** | The graphical equivalent — better when decisions are **sequential** |
| **Structure chart** | Hierarchical module decomposition (a **design** tool, not analysis) |
| **ER diagram** | The **data** model, complementing the DFD's **process** model |
| ⭐ **State transition diagram** | ⭐ **Event and timing behaviour — exactly what a DFD lacks** |

🔢 A decision table with 3 binary conditions has **2³ = 8** rules.

## 2.4 Input/output design

**Input design goals:** accuracy · minimum data entry · ease of use · ⭐ **validation at the point of entry**.
**Techniques:** form design · ⭐ **input validation** (range checks, format checks, ⭐ **check digits**) · codes · default values · drop-downs in preference to free text.

**Output design goals:** the **right content**, to the **right user**, at the **right time**, in the **right medium**.
Output types: internal · external · **turnaround** (goes out and comes back with data added). Reports vs dashboards vs ad-hoc queries.

**Code design types:** sequence · block · group classification · significant digit · mnemonic · ⭐ **check digit** (a computed digit that detects transcription errors — as in Aadhaar and ISBN numbers).

---

## 3. ⭐⭐⭐ Software process models

### 💡 The idea

A **process model** prescribes the order and manner of the activities: requirements, design, coding, testing, deployment, maintenance. Different models suit different risk profiles — which is why several exist rather than one "best" one.

## 3.1 ⭐⭐ The models

### ⭐ Waterfall (classical linear)

Strictly sequential phases, each completed and signed off before the next begins.
```
Requirements → Design → Coding → Testing → Deployment → Maintenance
```
✅ Simple to manage; heavily documented; works when requirements are genuinely stable.
❌ ⭐ **Its central weakness: NO WORKING SOFTWARE UNTIL VERY LATE**, and **requirement changes are ruinously expensive** because they invalidate completed phases. There is no iteration.

### ⭐ Prototyping

Build a quick prototype, show it to users, and refine — either discarding it (throwaway) or growing it (evolutionary).
✅ ⭐ **Best when requirements are UNCLEAR** and users cannot articulate what they want until they see something.
❌ Users may mistake the prototype for the product; documentation is often poor; can encourage endless tinkering.

### ⭐ Iterative / Incremental

Deliver in successive increments, each adding functionality to a working system.
✅ Working software early; feedback each increment.
❌ Needs a sound architecture designed up front.

### ⭐⭐ Spiral (Boehm)

Iterative, with each loop passing through four quadrants:
📌 ⭐ **Planning → RISK ANALYSIS → Engineering → Evaluation**

⭐⭐ **Its defining characteristic: it is RISK-DRIVEN.** Every single cycle contains an explicit risk-analysis step, and the riskiest items are tackled first.
✅ ⭐ **Best for large, expensive, high-risk projects.**
❌ Costly; needs genuine risk-assessment expertise; complex to manage.

### ⭐⭐ V-model

Waterfall bent into a V, with a ⭐ **testing phase MIRRORING every development phase**:
```
Requirements ─────────────────► Acceptance testing
   Design ─────────────────► System testing
     Architecture ────────► Integration testing
        Module design ──► Unit testing
              Coding
```
⭐ **Its defining characteristic: test planning for each phase happens DURING that phase**, not at the end.
✅ Excellent for **safety-critical and high-reliability** systems.
❌ As rigid as waterfall.

### RAD (Rapid Application Development)
Parallel development of components by multiple teams, heavy reuse, and JAD workshops.
✅ Very fast for modular systems. ❌ Needs skilled teams and highly committed users.

### ⭐⭐ Agile

Iterative, incremental and **adaptive**, prioritising working software and responsiveness over documentation and planning.
✅ ⭐ **Best when requirements are changing** and the customer is available.
❌ Less documentation; hard to fix cost and scope in advance; scaling to large teams is difficult.

### Others
**RUP** — use-case driven, architecture-centric, four phases (inception, elaboration, construction, transition).
⭐ **DevOps** — integrates development and operations; CI/CD, automation, infrastructure as code, continuous monitoring.

## 3.2 ⭐⭐⭐ The three identifications that get asked

| The clue in the question | ⭐ The model |
|---|---|
| ⭐ **"Risk-driven"** / "risk analysis in every cycle" | ⭐ **SPIRAL** |
| ⭐ **"A testing phase for every development phase"** | ⭐ **V-MODEL** |
| ⭐ **"Working software only at the very end"** / "no iteration" | ⭐ **WATERFALL** |
| "Requirements are unclear" | ⭐ **PROTOTYPING** |
| "Requirements change frequently" | ⭐ **AGILE** |
| "Large, high-risk, expensive" | **SPIRAL** |
| "Safety-critical" | **V-MODEL** |

## 3.3 ⭐⭐ Agile in detail

⭐ **The Agile Manifesto's four values** — each favours the left over the right:
1. **Individuals and interactions** over processes and tools
2. ⭐ **WORKING SOFTWARE** over comprehensive documentation
3. ⭐ **CUSTOMER COLLABORATION** over contract negotiation
4. ⭐ **RESPONDING TO CHANGE** over following a plan

⚠ The manifesto says the right-hand items still have value — just less.

### ⭐⭐ Scrum

| Element | ⭐ Meaning |
|---|---|
| ⭐ **Sprint** | A **fixed-length** iteration, typically ⭐ **2–4 weeks**, producing a potentially shippable increment |
| ⭐ **Product backlog** | The **prioritised** list of all desired work, owned by the **Product Owner** |
| **Sprint backlog** | The items selected for the current sprint |
| ⭐ **Product Owner** | Decides ⭐ **WHAT** to build and its priority |
| ⭐ **Scrum Master** | ⭐ **A FACILITATOR** who removes impediments — ⚠ **NOT a manager** and does not assign work |
| **Development Team** | Self-organising; decides **how** to build it |
| ⭐ **Daily stand-up (daily scrum)** | ⭐ **A 15-minute** synchronisation meeting |
| **Sprint review** | Demonstrate the increment to stakeholders |
| ⭐ **Sprint retrospective** | ⭐ **Improve the PROCESS** (as distinct from the review, which inspects the product) |
| ⭐ **Burndown chart** | Remaining work plotted over time |
| **Velocity** | Story points completed per sprint — used for forecasting |

⚠ ⭐ **Sprint review inspects the PRODUCT; sprint retrospective inspects the PROCESS.**

### ⭐ Other Agile methods

⭐ **XP (Extreme Programming)** — **pair programming**, **TDD**, continuous integration, small frequent releases, aggressive refactoring, on-site customer.
⭐ **Kanban** — a visual board with ⭐ **WIP (work-in-progress) LIMITS** and **continuous flow**.
Lean · Crystal · FDD.

⚠⚠ ⭐ **Scrum uses FIXED-LENGTH SPRINTS; Kanban uses CONTINUOUS FLOW with WIP limits and no sprints.**

---

## 4. ⭐⭐⭐ Project planning, estimation and management

## 4.1 ⭐⭐ Size estimation

### 💡 The problem

To estimate effort and cost you must first estimate **size**. But how do you measure the size of software that does not exist yet?

⭐ **LOC (Lines of Code)** — count the lines.
❌ ⭐ **Three fatal flaws:** it is **language-dependent** (1 line of Python ≈ 5 of Java); it can only be counted **accurately after coding**, which is far too late; and it **rewards verbosity** (a programmer writing worse, longer code appears more productive).

⭐⭐ **Function Point (FP) analysis** — measure the **functionality delivered from the user's viewpoint**.
✅ ⭐ **Language-INDEPENDENT** and ⭐ **measurable from the REQUIREMENTS stage** — which is exactly when you need an estimate.

📌 ⭐ **The five function types counted:**
1. ⭐ **EI** — External Inputs (data entering, e.g. a form)
2. ⭐ **EO** — External Outputs (data leaving, e.g. a report)
3. ⭐ **EQ** — External Inquiries (an input/output pair with no processing, e.g. a lookup)
4. ⭐ **ILF** — Internal Logical Files (data maintained inside the system)
5. ⭐ **EIF** — External Interface Files (data referenced from outside)

📌 **UFP (Unadjusted Function Points)** = Σ (count × complexity weight)
📌 ⭐ **FP = UFP × VAF**, where **VAF = 0.65 + 0.01 × Σ(14 general system characteristics, each rated 0–5)**
📌 ⭐ **So VAF ranges from 0.65 (all zeros) to 1.35 (all fives)** — an adjustment of ±35%.

🔢 UFP = 200, and the 14 characteristics sum to 35 → VAF = 0.65 + 0.35 = 1.00 → **FP = 200**.
🔢 UFP = 200, characteristics sum to 70 → VAF = 0.65 + 0.70 = 1.35 → **FP = 270**.

⚠ ⭐ **The exam point: function points are language-independent and available EARLY; LOC is neither.**

## 4.2 ⭐⭐⭐ COCOMO

📌 **COCOMO = COnstructive COst MOdel** (Barry Boehm, 1981) — an empirical model relating **effort** to **size**, calibrated from 63 real projects.

### ⭐⭐ The three project modes

| Mode | ⭐ Characteristics | Typical size | **a** | **b** |
|---|---|---|---|---|
| ⭐ **Organic** | ⭐ **Small team, FAMILIAR problem, flexible requirements**, in-house | 2–50 KLOC | **2.4** | **1.05** |
| ⭐ **Semi-detached** | ⭐ **Medium size, MIXED experience, some rigid constraints** | 50–300 KLOC | **3.0** | **1.12** |
| ⭐ **Embedded** | ⭐ **Large, TIGHT hardware/regulatory constraints, complex, unfamiliar** | > 300 KLOC | **3.6** | **1.20** |

🔢 A payroll system for your own company → **organic**. A new banking transaction system → **semi-detached**. Flight-control software → **embedded**.

### ⭐⭐ The formulas

📌 ⭐ **Effort E = a × (KLOC)^b** person-months
📌 ⭐ **Development time D = c × (E)^d** months
  *(organic c = 2.5, d = 0.38; semi-detached d = 0.35; embedded d = 0.32)*
📌 ⭐ **Average staff size = E / D** persons
📌 **Productivity = KLOC / E**

### 🔢 Worked example

**An organic project of 32 KLOC.**
```
E = 2.4 × 32^1.05
  32^1.05 ≈ 37.4
E ≈ 2.4 × 37.4 ≈ 90 person-months

D = 2.5 × 90^0.38
  90^0.38 ≈ 5.6
D ≈ 2.5 × 5.6 ≈ 14 months

Average staff = 90 / 14 ≈ 6.4 persons
```
⭐ **Effort ≈ 90 person-months, duration ≈ 14 months, team ≈ 6 people.**

### 💡⭐ Why the exponent b > 1 matters

⭐ **All three modes have b > 1**, so effort grows **SUPER-LINEARLY** with size — a **diseconomy of scale**.

💡 **Why:** doubling the code more than doubles the effort, because communication paths, integration complexity and coordination overhead grow faster than the code. ⭐ **Embedded has the largest exponent (1.20), so it is the most sensitive to size.**

⚠⚠ ⭐ **Brooks's law: "Adding manpower to a late software project makes it later."**
💡 **Why:** new people must be trained (consuming the existing team's time), and communication paths grow as n(n−1)/2. This is the practical corollary of b > 1.

⭐ **The three COCOMO levels:** **Basic** (size only) → **Intermediate** (adds 15 **cost drivers** / an Effort Adjustment Factor) → **Detailed/Complete** (cost drivers applied per phase). **COCOMO II** modernises it for modern practices.

## 4.3 ⭐⭐⭐ Scheduling

### ⭐ Gantt chart

A bar chart of tasks against a calendar.
✅ Shows **duration, overlap and progress** clearly; excellent for communication.
❌ ⚠ ⭐ **Does NOT clearly show DEPENDENCIES or the CRITICAL PATH.**

### ⭐⭐ PERT and CPM

Activity **network** diagrams, which **do** show dependencies.

| | ⭐ **PERT** | ⭐ **CPM** |
|---|---|---|
| ⭐ **Time estimates** | ⭐ **PROBABILISTIC** (three-point) | ⭐ **DETERMINISTIC** (single estimate) |
| ⭐ **Focus** | ⭐ **Time and UNCERTAINTY** | ⭐ **Time–COST trade-off** |
| Suits | **Research / novel** projects (never done before) | **Repetitive / well-understood** projects |
| Orientation | Event-oriented | Activity-oriented |

### ⭐⭐ The PERT formula

📌 ⭐ **Expected time t_e = (t_optimistic + 4 × t_most_likely + t_pessimistic) / 6**
📌 ⭐ **Standard deviation σ = (t_pessimistic − t_optimistic) / 6**; variance = σ²

💡 **Why the weights 1-4-1:** it is a weighted average that gives the most likely estimate four times the weight of the extremes — a discrete approximation to a beta distribution.

🔢 **t_o = 4, t_m = 6, t_p = 14 days:**
```
t_e = (4 + 4(6) + 14) / 6 = (4 + 24 + 14)/6 = 42/6 = 7 days
σ   = (14 − 4)/6 = 1.67 days
```
⭐ **Expected duration 7 days, σ ≈ 1.67 days.** Note t_e (7) exceeds t_m (6) because the pessimistic tail is long.

### ⭐⭐⭐ The critical path

📌 ⭐⭐ **The critical path is the LONGEST path through the network.** It determines the **minimum possible project duration**.

⚠⚠ ⭐ **LONGEST, not shortest.** This is the most common error in this topic.

💡 **Why the longest:** the project cannot finish until *every* path finishes, so the project duration equals the duration of the slowest (longest) chain of dependent activities.

📌 ⭐ **Activities on the critical path have ZERO slack (float).** Delaying any of them delays the whole project by the same amount.
📌 ⭐ **Slack / float = Latest Start − Earliest Start = Latest Finish − Earliest Finish**

### 🔢 Worked example

Activities: A(3 days) → C(4); B(2) → C; C → D(5); B → E(6); E → D.
```
Path 1: A → C → D  =  3 + 4 + 5 = 12 days
Path 2: B → C → D  =  2 + 4 + 5 = 11 days
Path 3: B → E → D  =  2 + 6 + 5 = 13 days   ⭐ LONGEST
```
⭐ **Critical path = B → E → D, project duration = 13 days.** Activities B, E and D have **zero slack**; A has slack of 13 − 12 = **1 day**.

⭐ **Crashing** — shortening the critical path by adding resources (CPM's time–cost trade-off).

## 4.4 ⭐ Risk management

⭐ **The four steps:**
1. **Risk identification** — what could go wrong?
2. **Risk analysis** — probability × impact
3. ⭐ **Risk prioritisation** — 📌 ⭐ **Risk Exposure = probability × potential loss**
4. ⭐ **RMMM** — Risk Mitigation, Monitoring and Management

🔢 A 30% chance of losing a key developer, costing ₹5 lakh in delay → Risk Exposure = 0.3 × 5,00,000 = **₹1,50,000**. Compare that with the cost of mitigation (cross-training) to decide.

**Risk categories:** project risks (schedule, budget, staffing) · technical risks · business risks · known / predictable / unpredictable.
⭐ **Response strategies:** **avoid** · **transfer** (insure, outsource) · **mitigate** (reduce probability or impact) · **accept**.

## 4.5 Configuration management and metrics

⭐ **SCM (Software Configuration Management)** — controls change to all project artefacts: **version control**, ⭐ **BASELINES** (a formally reviewed, frozen version), **change control** (a Change Control Board), configuration audit, status accounting. Tools: Git, SVN.

💡 **Why baselines matter:** without them, "the requirements" means something different to every team member.

**Metrics:** process / project / product metrics · size (LOC, FP) · quality (defect density, MTTF, MTBF) · ⭐ **cyclomatic complexity** (§5.4).
📌 ⭐ **Defect Removal Efficiency (DRE) = E / (E + D)**, where E = errors found **before** delivery and D = defects found **after**. ⭐ **DRE = 1 is the ideal** (nothing escaped to the customer).

🔢 60 defects found in testing, 15 reported by users → DRE = 60/75 = **0.80**.

---

## 5. ⭐⭐⭐ Design and coding

## 5.1 ⭐ Design principles

| Principle | 💡 Meaning |
|---|---|
| ⭐ **Abstraction** | Work at the appropriate level of detail; hide the rest |
| ⭐ **Modularity** | Decompose the system into manageable, separately comprehensible units |
| ⭐ **Information hiding** | A module's internals are **inaccessible**; its **interface is the only contract**. (Parnas, 1972 — the ancestor of encapsulation) |
| **Stepwise refinement** | Elaborate progressively from abstract to concrete |
| ⭐ **Functional independence** | Each module does one thing, with minimal reliance on others — achieved through **high cohesion and low coupling** |
| **Separation of concerns** | Different responsibilities in different places |
| **Anticipation of change** | Isolate what is likely to change |

📌 ⭐⭐ **The single most important design goal: HIGH COHESION and LOW COUPLING.**

💡 **What that means in plain terms:**
- ⭐ **Cohesion** = how strongly related the things **INSIDE one module** are. High is good.
- ⭐ **Coupling** = how strongly **DIFFERENT modules DEPEND on each other**. Low is good.

💡 **Why it matters:** a highly cohesive, loosely coupled module can be understood, tested, replaced and reused **on its own**. A module that does five unrelated things and reaches into three other modules' internals can only be understood by reading the whole system.

## 5.2 ⭐⭐⭐ Cohesion — best to worst

| Rank | Type | 💡 Description |
|---|---|---|
| ⭐ **1 — BEST** | ⭐ **Functional** | ⭐ **All elements contribute to a SINGLE, well-defined task.** e.g. `calculateInterest()` |
| 2 | **Sequential** | The output of one element is the input of the next |
| 3 | **Communicational** | Elements operate on the **same data** |
| 4 | **Procedural** | Elements must execute in a certain **sequence**, but are otherwise unrelated |
| 5 | **Temporal** | Elements are related only by being executed at the **same time** — e.g. an `initialise()` routine doing five unrelated setups |
| 6 | **Logical** | Elements perform **logically similar** functions selected by a **flag** — e.g. `handleAll(type)` with a giant switch |
| ⭐ **7 — WORST** | ⭐ **Coincidental** | ⭐ **NO meaningful relationship at all** — a grab-bag `Utils` module |

⭐ **Mnemonic (best → worst): F S C P T L C**
**F**unctional **S**equential **C**ommunicational **P**rocedural **T**emporal **L**ogical **C**oincidental

## 5.3 ⭐⭐⭐ Coupling — best to worst

| Rank | Type | 💡 Description |
|---|---|---|
| ⭐ **1 — BEST** | ⭐ **Data** | ⭐ **Modules communicate only through SIMPLE PARAMETERS** — e.g. `sqrt(x)` |
| 2 | **Stamp / data-structure** | An **entire data structure** is passed but only part of it is used |
| 3 | ⭐ **Control** | One module passes a **FLAG that controls the other's internal logic** — the caller must know how the callee works |
| 4 | **External** | Modules share an externally imposed format, protocol or device |
| 5 | **Common / global** | Modules share **global data** — a change by one silently affects all |
| ⭐ **6 — WORST** | ⭐ **Content** | ⭐ **One module DIRECTLY REFERENCES or MODIFIES another's INTERNALS** — total loss of encapsulation |

⭐ **Mnemonic (best → worst): D S C E C C**
**D**ata **S**tamp **C**ontrol **E**xternal **C**ommon **C**ontent

⚠⚠ ⭐ **Both orderings are asked directly and frequently. The two facts to be certain of:**
📌 ⭐ **FUNCTIONAL cohesion is BEST; COINCIDENTAL is WORST.**
📌 ⭐ **DATA coupling is BEST; CONTENT coupling is WORST.**

## 5.4 ⭐⭐⭐ Cyclomatic complexity (McCabe)

### 💡 The idea

📌 **Cyclomatic complexity measures the number of LINEARLY INDEPENDENT PATHS through a program's control flow graph** — in effect, how many decisions it contains.

💡 **Why anyone cares:** it is a **lower bound on the number of test cases needed for branch coverage**, and it correlates with how hard the code is to understand and maintain. Complexity above ~10 is a refactoring signal.

📌 ⭐ **Three equivalent formulas — use whichever the question makes easiest:**
1. ⭐ **V(G) = E − N + 2P** (E = edges, N = nodes, P = connected components; **for a single program P = 1, so V(G) = E − N + 2**)
2. ⭐ **V(G) = (number of PREDICATE / decision nodes) + 1**
3. ⭐ **V(G) = (number of BOUNDED REGIONS in the planar flow graph) + 1**

### 🔢 Worked examples

🔢 **A flow graph with 12 edges and 9 nodes:**
```
V(G) = E − N + 2 = 12 − 9 + 2 = 5
```
⭐ **Answer: 5** — at least 5 test cases are needed for branch coverage.

🔢 **A program with three `if` statements and no other branching:**
```
V(G) = predicates + 1 = 3 + 1 = 4
```

🔢 **A program with one `if-else` and one `while` loop:**
```
Predicate nodes: the if condition, the while condition = 2
V(G) = 2 + 1 = 3
```

⚠ Note a **compound condition** like `if (a && b)` counts as **two** predicates, because it contains two decisions.

## 5.5 Architecture, design approaches and coding

**Architectural styles:** layered · client–server · ⭐ **MVC** (Week 10) · repository/data-centred · pipe-and-filter · event-driven · **microservices** · SOA.

⭐ **Top-down design** (functional decomposition — start with the whole and break it down) vs **bottom-up design** (build reusable primitives first).
⭐ **Structured design** (DFD → structure chart, via transform analysis and transaction analysis) vs ⭐ **object-oriented design** (UML, classes and responsibilities).

⭐ **UML diagrams:**
- **Structural:** class, object, component, deployment, package
- **Behavioural:** ⭐ **use case**, sequence, activity, state, collaboration

⭐ **Design patterns — the three categories:**
- ⭐ **Creational:** Singleton, Factory, Abstract Factory, Builder, Prototype
- ⭐ **Structural:** Adapter, Decorator, Facade, Proxy, Composite, Bridge
- ⭐ **Behavioural:** Observer, Strategy, Command, Iterator, State, Template Method

⭐ **SOLID principles:** **S**ingle responsibility · **O**pen/closed · **L**iskov substitution · **I**nterface segregation · **D**ependency inversion.

⭐ **Code review — two forms, and the distinction is asked:**
- ⭐ **Walkthrough** — **informal**, led by the **author**, who explains the code
- ⭐ **Inspection** — **formal**, **checklist-driven**, with a **moderator**, defined roles and recorded defects. More effective, more expensive

**Also:** coding standards and guidelines · refactoring · documentation.

---

## 6. ⭐⭐⭐ Testing

## 6.1 ⭐ Terminology

⚠⚠ ⭐ **Four terms in a causal chain — routinely confused:**
📌 ⭐ **ERROR** (a **human** mistake) → **FAULT / DEFECT / BUG** (the resulting **flaw in the artefact**) → **FAILURE** (the **observable** incorrect behaviour when the fault is executed) → **CONSEQUENCE**

🔢 A programmer misreads a specification (**error**), writing `>` instead of `>=` (**fault**). The fault sits harmlessly until an input hits the boundary, when the program returns a wrong answer (**failure**).

📌 ⭐ **Dijkstra: "Testing can only show the PRESENCE of defects, never their ABSENCE."**
💡 Exhaustive testing is impossible (a program with two 32-bit inputs has 2⁶⁴ possible inputs), so testing is always sampling. This is why *reviews and inspections* matter alongside testing.

## 6.2 ⭐⭐⭐ Black-box vs white-box

### 💡 The idea

⭐ **Black-box testing** — you can see only the **specification**. You feed in inputs and check the outputs, knowing nothing about the internals.
⭐ **White-box (structural / glass-box) testing** — you can see the **code**, and design tests to exercise its structure.

⭐ They find **different kinds** of defect, which is why both are needed:
- Black-box finds ⭐ **MISSING functionality** (something the spec required but the code never implements) — white-box can never find this, because there is no code to look at
- White-box finds ⭐ **unreachable code, logic errors and untested branches** — black-box may never trigger these

| | ⭐ **Black-box (functional)** | ⭐ **White-box (structural)** |
|---|---|---|
| Basis | ⭐ **The SPECIFICATION only** | ⭐ **The internal CODE structure** |
| Performed by | Testers, users | Developers |
| ⭐ **Techniques** | ⭐ **Equivalence class partitioning · BOUNDARY VALUE ANALYSIS · cause-effect graphing · decision table testing · state transition testing · error guessing** | ⭐ **Statement coverage · branch/decision coverage · condition coverage · path coverage · data-flow testing · loop testing · mutation testing** |
| Finds | ⭐ **Missing functionality** | ⭐ **Logic and structural errors** |

## 6.3 ⭐⭐ The two key black-box techniques

### ⭐ Equivalence Class Partitioning

💡 Divide the input domain into **classes that the program should treat identically**, then test **one representative from each** — plus each invalid class. Testing more values from the same class adds no information.

🔢 A field accepts ages 18–60:
```
Invalid class:  < 18       → test 10
Valid class:    18–60      → test 35
Invalid class:  > 60       → test 75
```
⭐ Three test cases instead of forty-three.

### ⭐⭐ Boundary Value Analysis (BVA)

💡 ⭐ **Experience shows most defects cluster at the BOUNDARIES of ranges** — off-by-one errors, `>` instead of `>=`, loops running one iteration too few. So test **at and around each boundary**.

🔢 **For a valid range of 1 to 100, test:**
```
0    ← just below the lower boundary (invalid)
1    ← at the lower boundary
2    ← just above the lower boundary
50   ← a nominal middle value
99   ← just below the upper boundary
100  ← at the upper boundary
101  ← just above the upper boundary
```
⭐ **Seven test cases** — the standard BVA set.

⭐ **Both BVA and equivalence partitioning are BLACK-BOX techniques** (they derive tests from the specification's ranges, not from the code).

## 6.4 ⭐⭐⭐ Coverage criteria

### 💡 The hierarchy

📌 ⭐ **Weakest → strongest: STATEMENT < BRANCH/DECISION < CONDITION < PATH coverage**

### ⚠⚠⭐ Why 100% statement coverage ≠ 100% branch coverage

```c
if (x > 0) {
    y = 1;          // this statement
}
// no else branch
```
🔢 A single test with `x = 5` executes **every statement** → ⭐ **100% statement coverage**.
But the **false** branch (x ≤ 0) has never been taken → ⭐ **only 50% branch coverage**.

⭐ **This is one of the most reliably asked testing questions.**

**Path coverage** is the strongest but generally **infeasible**: a loop that can run 0–1000 times contributes 1001 paths, and paths multiply across a program.

⭐ **Mutation testing** — deliberately inject small faults ("mutants") into the code and check whether the test suite **detects** them. ⭐ It measures the **quality of the TEST SUITE**, not of the program.

**Grey-box testing** combines black- and white-box knowledge.

## 6.5 ⭐⭐⭐ Levels of testing

| Level | ⭐ Scope | Performed by |
|---|---|---|
| ⭐ **Unit testing** | An **individual module/function in ISOLATION** | Developer (white-box) |
| ⭐ **Integration testing** | The **INTERFACES between modules** | Developers/testers |
| ⭐ **System testing** | The **complete integrated system against the SRS** | Independent test team (black-box) |
| ⭐ **Acceptance testing** | ⭐ **The CUSTOMER's confirmation that it meets their needs** | ⭐ **The customer/user** |

## 6.6 ⭐⭐⭐ Integration strategies — stubs vs drivers

### 💡 The idea

You cannot test a top-level module before its subordinates exist — and vice versa. So you build temporary stand-ins.

📌 ⭐⭐ **STUB = a dummy CALLED module** (a fake subordinate that returns a canned value)
📌 ⭐⭐ **DRIVER = a dummy CALLING module** (a fake superior that invokes the module under test)

```
TOP-DOWN integration:              BOTTOM-UP integration:

     [Main]  ← real                     [DRIVER]  ← dummy caller
        │                                   │
    ┌───┴───┐                           ┌───┴───┐
  STUB    STUB  ← dummies             [Mod A] [Mod B]  ← real
                                       (already built)
```

| Strategy | Order | ⭐ **Needs** | 💡 Advantage |
|---|---|---|---|
| ⭐ **Top-down** | Highest modules first | ⭐ **STUBS** | ⭐ Validates the **architecture and control logic early**; a working skeleton exists from the start |
| ⭐ **Bottom-up** | Lowest modules first | ⭐ **DRIVERS** | ⭐ Validates the **low-level utilities early**; allows parallel work on independent branches |
| **Sandwich / hybrid** | Both ends toward the middle | Both | Combines the advantages |
| **Big-bang** | Everything at once | Neither | ⚠ Defects are **very hard to localise** |

⚠⚠⚠ ⭐ **TOP-DOWN needs STUBS; BOTTOM-UP needs DRIVERS.**
⭐ **This is the single most common error in the entire Software Engineering section.**

💡 **How to never forget it:** in **top**-down you start at the **top**, so what is missing is **below** you — the things you *call*. A dummy called module is a **stub**. (Alliteration helps: **top → stub** are both short words; **bottom → driver** drives *up*.)

## 6.7 ⭐⭐ Alpha vs beta testing

| | ⭐ **Alpha testing** | ⭐ **Beta testing** |
|---|---|---|
| ⭐ **Where** | ⭐ **At the DEVELOPER'S site** | ⭐ **At the CUSTOMER'S site** |
| By whom | Internal staff / selected users, ⭐ **with developers present** | ⭐ **Real end users**, developers **absent** |
| Environment | Controlled | Real-world, uncontrolled |
| Stage | Before beta | The last stage before general release |

⭐ **Both are forms of ACCEPTANCE testing.**
💡 The point of beta testing is exposure to **environments and usage patterns the developers never imagined** — which is precisely why the developers must not be there controlling it.

## 6.8 ⭐ Other testing types

| Type | ⭐ Purpose |
|---|---|
| ⭐ **Regression testing** | ⭐ **RE-RUN existing tests after a CHANGE**, to confirm nothing previously working has broken. *(The most important type in maintenance — see §7.2.)* |
| ⭐ **Smoke testing** | A quick "is this build even viable?" check ("build verification") |
| **Sanity testing** | A narrow check that one specific fix works |
| ⭐ **Performance testing** | Response time and throughput under **expected** load |
| ⭐ **Load vs Stress testing** | ⭐ **LOAD = behaviour at expected PEAK. STRESS = behaviour BEYOND limits, to find the breaking point** |
| **Volume testing** | Behaviour with very large data volumes |
| ⭐ **Security testing** | Vulnerabilities; penetration testing |
| **Usability testing** | Ease of use with real users |
| **Compatibility / portability** | Across platforms, browsers, devices |
| **Recovery testing** | Behaviour after induced failures |
| ⭐ **Mutation testing** | Evaluates the **test suite's** quality |
| **Exploratory / ad-hoc** | Unscripted, experience-driven |
| ⭐ **TDD (Test-Driven Development)** | ⭐ **Write the FAILING TEST FIRST, then the code** — red → green → refactor |

**Test artefacts:** test plan · test case (ID, preconditions, inputs, **expected** output, actual output) · test suite · test harness.
**Defect life cycle:** New → Assigned → Open → Fixed → Retest → Verified → **Closed** (or Reopened / Deferred / Rejected / Duplicate).

---

## 7. ⭐⭐⭐ Implementation and maintenance

## 7.1 ⭐⭐ Deployment / changeover strategies

### 💡 The idea

The old system works; the new one is untested in reality. How you switch over determines your exposure if the new system fails.

| Strategy | 💡 Description | ⭐ Risk | Cost |
|---|---|---|---|
| ⭐ **Direct / plunge / big-bang** | Switch the old system off, the new one on | ⭐ **HIGHEST** — no fallback | ⭐ **Lowest** |
| ⭐ **Parallel** | ⭐ **Run BOTH systems simultaneously and compare results** | ⭐ **LOWEST** — the old system is a safety net | ⭐ **Highest** (double the work) |
| ⭐ **Phased / staged** | Introduce module by module | Moderate | Moderate |
| ⭐ **Pilot** | Deploy fully, but in ⭐ **ONE location/group first** | Moderate | Moderate; excellent for learning |

⚠ ⭐ **The exam pairing: PARALLEL = lowest risk, highest cost. DIRECT = highest risk, lowest cost.**

**Also required at implementation:** user **training** · documentation (user manual, system manual, operations manual) · **data conversion/migration** · site preparation.

## 7.2 ⭐⭐⭐ Maintenance types

### 💡 The idea

Software is "finished" and then changes for the rest of its life. The four reasons have distinct names, and exams test them as **scenarios**.

| Type | ⭐ Trigger | ⭐ Share of maintenance effort |
|---|---|---|
| ⭐ **Corrective** | ⭐ **FIXING REPORTED DEFECTS** | ~20% |
| ⭐ **Adaptive** | ⭐ **A CHANGE IN THE ENVIRONMENT** — new OS, new hardware, new regulations, a changed external interface | ~25% |
| ⭐ **Perfective / enhancive** | ⭐ **NEW or IMPROVED FUNCTIONALITY or performance requested by users** | ⭐ **~50–65% — the LARGEST** |
| ⭐ **Preventive** | ⭐ **RESTRUCTURING/refactoring to improve FUTURE maintainability** (re-engineering, reverse engineering) | ~5% |

### 🔢⭐ Classify these — the standard question format

| Scenario | ⭐ Type |
|---|---|
| Porting the application to a new operating system | ⭐ **Adaptive** |
| Fixing a crash reported by a user | ⭐ **Corrective** |
| Adding a new report the users asked for | ⭐ **Perfective** |
| Refactoring a tangled module so future changes are easier | ⭐ **Preventive** |
| Updating the tax calculation because the tax law changed | ⭐ **Adaptive** |
| Making a slow query 10× faster | ⭐ **Perfective** |
| Upgrading a library because the old one is unsupported | **Adaptive** |
| Adding comments and documentation to legacy code | **Preventive** |

⭐ **The distinguishing test:**
- ⭐ **Adaptive = the ENVIRONMENT changed** (something outside your control)
- ⭐ **Perfective = the USERS want more** (an enhancement)
- ⭐ **Corrective = something was BROKEN**
- ⭐ **Preventive = nothing is wrong yet**, you are protecting the future

⚠ ⭐ These four are asked constantly and the wording is always a scenario, never a definition.

📌 ⭐ **Maintenance consumes 60–70% of a software system's TOTAL lifecycle cost** — more than the original development.

💡 **Why so much:** the system runs for a decade or more, the environment keeps shifting, and every change must be made in code the original authors have long left. This is also why **maintainability** is an explicit design goal.

📌 ⭐ **Software does not "wear out", but it DOES deteriorate** — repeated modification increases disorder. ⭐ **Lehman's laws** capture this: *continuing change* (a system must keep changing or become less useful) and *increasing complexity* (unless work is done to reduce it).

⭐ **Legacy system options:** scrap · continue maintaining · **re-engineer** · replace.
⭐ **Reverse engineering** recovers design/specification **from** existing code. **Re-engineering** restructures and rewrites while preserving functionality. **Forward engineering** builds anew.

## 7.3 ⭐⭐ Software quality

⭐ **McCall's / ISO 9126 quality factors:**
📌 ⭐ **Functionality · Reliability · Usability · Efficiency · Maintainability · Portability**

### ⭐⭐⭐ CMM / CMMI — the five maturity levels

### 💡 The idea

The **Capability Maturity Model** (SEI, Carnegie Mellon) rates an **organisation's software PROCESS**, not its products. The insight is that consistently good software comes from a **repeatable, measured process**, not from heroic individuals.

| Level | ⭐ Name | ⭐ Characteristic |
|---|---|---|
| ⭐ **1** | ⭐ **Initial** | ⭐ **Ad-hoc, chaotic; success depends on individual HEROICS.** No process discipline. *(No key process areas required.)* |
| ⭐ **2** | ⭐ **Repeatable / Managed** | Basic project management (cost, schedule, requirements tracking). ⭐ **Past successes can be REPEATED** on similar projects |
| ⭐ **3** | ⭐ **Defined** | ⭐ **A DOCUMENTED, STANDARDISED process across the whole organisation**, tailored per project |
| ⭐ **4** | ⭐ **Managed / Quantitatively Managed** | ⭐ **Process and product are MEASURED and QUANTITATIVELY CONTROLLED** — decisions from data, not opinion |
| ⭐ **5** | ⭐ **Optimising** | ⭐ **CONTINUOUS process improvement**, defect prevention, technology innovation |

⚠ ⭐ **There is no level 0**, and ⭐ **level 5 is "Optimising" — do not stop at level 4.** Both details are asked.

⭐ **Memory hook for the progression:** chaos → repeat → document → measure → improve.

**Other standards:** ISO 9001 · ISO/IEC 25010 · Six Sigma.
⚠ ⭐ **SQA vs SQC:**
- ⭐ **SQA (Quality Assurance)** is **PROCESS**-oriented and **PREVENTIVE** — build it right so defects do not occur
- ⭐ **SQC (Quality Control)** is **PRODUCT**-oriented and **DETECTIVE** — find the defects that did occur

⭐ **Reliability metrics:**
📌 **MTTF** = Mean Time To Failure · **MTTR** = Mean Time To Repair
📌 ⭐ **MTBF = MTTF + MTTR**
📌 ⭐ **Availability = MTTF / (MTTF + MTTR) × 100%**

🔢 MTTF = 950 hours, MTTR = 50 hours → MTBF = **1000 hours**; Availability = 950/1000 = **95%**.

---

# PART B — COMPILER DESIGN

## 💡 What a compiler does

You write `x = a + b * 2;` and the machine needs `MUL R1, R2, #2 / ADD R3, R0, R1 / ST x, R3`.

⭐ **A compiler bridges that gap in stages, each solving one problem:**
1. Split the character stream into meaningful words (**lexical analysis**)
2. Check the words form a grammatical structure (**syntax analysis**)
3. Check the structure makes *sense* — types, declarations (**semantic analysis**)
4. Translate into a simple machine-independent form (**intermediate code**)
5. Improve it (**optimisation**)
6. Emit target machine code (**code generation**)

⭐ **Why stages rather than one pass?** Each stage needs a different formal tool — regular expressions for words, context-free grammars for structure, attribute grammars for meaning. Separating them makes each tractable, and lets you swap the front end (new language) or the back end (new CPU) independently.

---

## 8. ⭐⭐⭐ Phases of a compiler

| # | Phase | ⭐ Input | ⭐ Output |
|---|---|---|---|
| ⭐ **1** | ⭐ **Lexical analysis (scanning)** | Character stream | ⭐ **TOKEN stream** |
| ⭐ **2** | ⭐ **Syntax analysis (parsing)** | Tokens | ⭐ **PARSE TREE / syntax tree** |
| ⭐ **3** | ⭐ **Semantic analysis** | Parse tree | Annotated tree; ⭐ **TYPE CHECKING** |
| 4 | **Intermediate code generation** | Annotated tree | ⭐ **Three-address code** |
| 5 | **Code optimisation** | Intermediate code | Optimised intermediate code |
| 6 | **Target code generation** | Optimised IR | Assembly / machine code |

📌 ⭐⭐ **Memorise the order: LEXICAL → SYNTAX → SEMANTIC → INTERMEDIATE CODE → OPTIMISATION → CODE GENERATION**

⭐ **Front end vs back end:**
📌 ⭐ **FRONT END = phases 1–4** — source-language dependent, machine **independent**
📌 ⭐ **BACK END = phases 5–6** — machine **dependent**

💡 ⭐ **Why the split matters:** with m languages and n target machines you need **m + n** components (m front ends, n back ends sharing one intermediate representation) rather than **m × n** complete compilers. This is exactly why GCC and LLVM can support dozens of languages on dozens of architectures.

⭐ **Two components span ALL phases:** the ⭐ **symbol table manager** and the ⭐ **error handler**.

## 8.1 ⭐⭐⭐ Which phase detects which error

> ⭐ **A guaranteed question. Learn the four rows.**

| Error | ⭐ Detected by |
|---|---|
| Invalid character; malformed number or identifier (`12abc`, `@#$`) | ⭐ **LEXICAL analysis** |
| Missing semicolon; unbalanced parentheses; wrong statement structure | ⭐ **SYNTAX analysis** |
| ⭐ **UNDECLARED VARIABLE** · ⭐ **TYPE MISMATCH** · wrong number of arguments · multiple declaration of the same name | ⭐ **SEMANTIC analysis** |
| Array index out of bounds; division by zero; null dereference | ⭐ **RUN TIME** |

### ⚠⚠⭐ Why an undeclared variable is a SEMANTIC error, not a syntax error

```c
int x = y + 1;    // y was never declared
```
- The **lexer** happily tokenises `y` as a perfectly valid identifier — nothing is wrong with its spelling
- The **parser** sees `identifier + constant`, which is grammatically correct — nothing is wrong with its structure
- ⭐ Only **semantic analysis**, which **consults the symbol table**, discovers that `y` has no declaration

⭐ **The general rule: syntax analysis checks FORM; semantic analysis checks MEANING — and meaning requires the symbol table.**

🔢 Similarly, `int x = "hello";` is syntactically flawless and semantically wrong → ⭐ **semantic error**.

## 8.2 ⭐ Related terms

| Term | 💡 Meaning |
|---|---|
| ⭐ **Compiler** | Translates the **WHOLE program before execution**. Faster execution; all errors reported at once |
| ⭐ **Interpreter** | Translates and executes ⭐ **statement by statement**. Slower execution, but ⭐ **easier debugging** and more portable |
| **Assembler** | Assembly language → machine code |
| **Linker** | Combines object modules and **resolves external references** |
| **Loader** | Loads the executable into memory and starts it |
| **Preprocessor** | Macro expansion and file inclusion — runs **before** the compiler |
| **Cross compiler** | Runs on machine A, generates code for machine B (essential for embedded development) |
| ⭐ **Pass** | One complete traversal of the source or IR. A ⭐ **single-pass** compiler is fast but **limits optimisation** (you cannot optimise what you have not yet seen) |
| **Bootstrapping** | Writing a compiler for a language *in that language* |

⭐ **Symbol table** — the compiler's central database of identifiers: name, type, scope, memory offset, size, and (for functions) parameter details. Usually implemented as a **hash table**. Used from lexical analysis right through to code generation.

---

## 9. ⭐⭐ Lexical analysis

### 💡 What the scanner does

It groups characters into **tokens**, strips **whitespace and comments**, expands macros, and enters identifiers into the symbol table.

```
Input:   int count = 10;
Output:  <keyword,int> <id,count> <op,=> <const,10> <punct,;>
```

## 9.1 ⭐⭐ Token, lexeme, pattern

| Term | ⭐ Meaning | Example |
|---|---|---|
| ⭐ **Token** | ⭐ **The CATEGORY** | `identifier`, `keyword`, `operator`, `constant` |
| ⭐ **Lexeme** | ⭐ **The ACTUAL character sequence matched** | `count`, `while`, `+`, `42` |
| ⭐ **Pattern** | ⭐ **The RULE describing the set of valid lexemes** | `letter(letter\|digit)*` |

🔢 In `int x = 10;` the tokens are: `keyword(int)`, `id(x)`, `operator(=)`, `constant(10)`, `punct(;)` → ⭐ **5 tokens**.
🔢 In `if (a >= b) x = 1;` → `if`, `(`, `a`, `>=`, `b`, `)`, `x`, `=`, `1`, `;` → **10 tokens** *(note `>=` is ONE token, not two)*.

## 9.2 ⭐⭐ The formal tools

📌 ⭐⭐ **Lexical analysis is SPECIFIED with REGULAR EXPRESSIONS and IMPLEMENTED with FINITE AUTOMATA (DFA).**

⚠ ⭐ **Why lexical analysis is a separate phase from parsing:** regular expressions are sufficient to describe tokens (an identifier, a number) but **cannot** express nested or balanced constructs. `((a+b)*c)` requires counting, which regular languages cannot do — that needs a **context-free grammar and a pushdown automaton**. Hence two distinct phases with two distinct formalisms.

⭐ **The longest-match (maximal munch) rule:** the scanner always takes the **LONGEST** possible lexeme.

🔢 Why this matters:
- `>=` is one token, not `>` followed by `=`
- `elsex` is a single **identifier**, not `else` followed by `x`
- `123abc` — the scanner tries to take the longest number and then reports a **lexical error**

⭐ **Rule priority:** among equal-length matches, the rule listed **first** wins — which is how `while` is recognised as a keyword rather than an identifier.

**Tools:** ⭐ **`lex` / `flex`** generate a scanner automatically from a regular-expression specification.
**Input buffering:** a two-buffer scheme with sentinels minimises I/O overhead.

---

## 10. ⭐⭐⭐ Syntax analysis (parsing)

### 💡 What the parser does

It takes the token stream and checks that it forms a valid sentence of the language, producing a **parse tree** that exposes the structure.

## 10.1 ⭐ Context-free grammars

📌 **G = (V, T, P, S)** — variables/non-terminals, terminals, productions, start symbol.

**Derivations:** leftmost / rightmost. **Sentential forms.**
⭐ **Parse tree** (concrete — shows every production) vs ⭐ **abstract syntax tree** (operators as internal nodes; redundant punctuation removed).

## 10.2 ⭐⭐ Ambiguity

📌 ⭐ **A grammar is AMBIGUOUS if some string has MORE THAN ONE parse tree** (equivalently, more than one leftmost derivation).

🔢 **The classic example:**
```
E → E + E | E * E | id
```
For `id + id * id` there are **two** parse trees:
```
     +                        *
   /   \                    /   \
  id    *        vs        +     id
      /   \              /   \
    id    id            id    id
   (= id + (id*id))     (= (id+id) * id)
```
⭐ These compute **different values** — 2 + 3 × 4 is either 14 or 20. An ambiguous grammar makes the language's meaning undefined.

⭐ **The fix: introduce precedence LEVELS and associativity via extra non-terminals:**
```
E → E + T | T          (+ is lower precedence, left-associative)
T → T * F | F          (* is higher precedence, left-associative)
F → ( E ) | id
```
💡 Because `*` appears **deeper** in the grammar, it binds more tightly — the structure now enforces precedence.

⭐ **The dangling-else problem** — the other classic ambiguity:
```
if C1 then if C2 then S1 else S2
```
Does the `else` belong to the inner or outer `if`? ⭐ **Convention: the `else` matches the NEAREST unmatched `then`.**

⚠ ⭐ **Ambiguity is a property of the GRAMMAR, not of the language** — you can often rewrite the grammar. But some languages are **inherently ambiguous** (no unambiguous grammar exists for them).

## 10.3 ⭐⭐ Grammar transformations for top-down parsing

### ⭐⭐ Left recursion elimination

⚠ ⭐ **Required, because `A → Aα` makes a recursive-descent parser loop forever** — to parse an A, it first tries to parse an A, with no input consumed.

📌 ⭐ **Replace `A → Aα | β` with:**
```
A  → β A'
A' → α A' | ε
```

🔢 `E → E + T | T` becomes:
```
E  → T E'
E' → + T E' | ε
```
💡 The recursion has been turned from **left** into **right**, which a top-down parser handles fine (it consumes a `T` before recursing).

### ⭐ Left factoring

⚠ Required when two productions share a **common prefix**, so the parser cannot choose between them on one lookahead token.

📌 ⭐ **Replace `A → αβ₁ | αβ₂` with:**
```
A  → α A'
A' → β₁ | β₂
```

🔢 `S → if E then S | if E then S else S` becomes
```
S  → if E then S S'
S' → else S | ε
```

⚠⚠ ⭐ **BOTTOM-UP (LR) PARSERS PREFER LEFT RECURSION** — they handle it naturally and it keeps the parse stack shallow. ⭐ **Only TOP-DOWN parsers need it removed.** This asymmetry is frequently asked.

## 10.4 ⭐⭐⭐ FIRST and FOLLOW sets

### 💡 Why they exist

A predictive parser must decide **which production to use** based on the next input token. That decision needs two pieces of information:
- **FIRST** — which tokens can *begin* each alternative?
- **FOLLOW** — if an alternative can derive nothing (ε), which tokens can legitimately come *next*?

### ⭐ FIRST(α)

📌 ⭐ **The set of TERMINALS that can BEGIN a string derived from α** (plus **ε** if α can derive the empty string).

**Rules:**
1. FIRST(terminal `a`) = {a}
2. For `A → X₁X₂…Xₙ`: add FIRST(X₁) minus ε. If X₁ ⇒* ε, also add FIRST(X₂), and so on. If **all** of X₁…Xₙ can derive ε, add **ε**.

### ⭐ FOLLOW(A)

📌 ⭐ **The set of TERMINALS that can appear IMMEDIATELY TO THE RIGHT of A in some derivation.**

**Rules:**
1. ⭐ **FOLLOW(start symbol) contains `$`** (end of input)
2. For `A → αBβ`: add **FIRST(β) minus ε** to FOLLOW(B)
3. For `A → αB`, or `A → αBβ` where **β ⇒* ε**: add ⭐ **FOLLOW(A)** to FOLLOW(B)

⚠⚠ ⭐ **ε is NEVER in a FOLLOW set** (but `$` can be). ε *can* be in a FIRST set.
💡 **Why:** FOLLOW answers "what real token comes next?" — and ε is not a token, it is the absence of one.

### 🔢⭐⭐ The standard worked example

**Grammar:**
```
E  → T E'
E' → + T E' | ε
T  → F T'
T' → * F T' | ε
F  → ( E ) | id
```

**FIRST sets** — work bottom-up:
- FIRST(F) = { **(**, **id** } (directly from its two productions)
- FIRST(T') = { **\***, **ε** }
- FIRST(T) = FIRST(F) = { (, id } (since `T → F T'` starts with F)
- FIRST(E') = { **+**, **ε** }
- FIRST(E) = FIRST(T) = { (, id }

**FOLLOW sets** — work top-down:
- FOLLOW(E) = { **$** } (start symbol), and from `F → ( E )` add **)** → { **)**, **$** }
- FOLLOW(E') : from `E → T E'` (E' at the end) add FOLLOW(E) → { **)**, **$** }
- FOLLOW(T) : from `E → T E'` add FIRST(E')−ε = {+}; E' ⇒* ε so also add FOLLOW(E) → { **+**, **)**, **$** }
- FOLLOW(T') : from `T → F T'` add FOLLOW(T) → { **+**, **)**, **$** }
- FOLLOW(F) : from `T → F T'` add FIRST(T')−ε = {\*}; T' ⇒* ε so also add FOLLOW(T) → { **\***, **+**, **)**, **$** }

| Non-terminal | ⭐ FIRST | ⭐ FOLLOW |
|---|---|---|
| **E** | { (, id } | { ), $ } |
| **E'** | { +, ε } | { ), $ } |
| **T** | { (, id } | { +, ), $ } |
| **T'** | { *, ε } | { +, ), $ } |
| **F** | { (, id } | { *, +, ), $ } |

⭐ **This is THE standard example — work it through by hand until you can reproduce it from the grammar alone.**

## 10.5 ⭐⭐ Top-down parsing

| Parser | 💡 Note |
|---|---|
| **Recursive descent (with backtracking)** | One function per non-terminal; tries alternatives and backtracks. **Inefficient** |
| ⭐ **Predictive parser / LL(1)** | ⭐ **NO backtracking** — uses **one lookahead token** and a parsing table |

📌 ⭐ **LL(1) means: L**eft-to-right scan, **L**eftmost derivation, **1** lookahead token.

⭐ **Building the LL(1) parsing table** — for each production `A → α`:
- For each terminal `a` in **FIRST(α)**, set **M[A, a] = A → α**
- If **ε ∈ FIRST(α)**, then for each `b` in ⭐ **FOLLOW(A)**, set **M[A, b] = A → α**

📌 ⭐ **A grammar is LL(1) ⟺ no table entry contains two productions** (no conflicts).

⭐ **Equivalently, for `A → α | β`:**
1. FIRST(α) ∩ FIRST(β) = ∅
2. If β ⇒* ε, then FIRST(α) ∩ FOLLOW(A) = ∅

⚠⚠ ⭐ **An AMBIGUOUS or LEFT-RECURSIVE grammar can NEVER be LL(1).**

## 10.6 ⭐⭐⭐ Bottom-up parsing (shift-reduce / LR)

### 💡 The idea

Instead of starting from the start symbol and predicting downwards, start from the **input tokens** and combine them upwards into non-terminals until you reach the start symbol.

📌 ⭐ **Bottom-up parsing produces a RIGHTMOST DERIVATION IN REVERSE.**

⭐ **Four actions:**
- ⭐ **SHIFT** — push the next input token onto the stack
- ⭐ **REDUCE** — replace a **handle** on top of the stack with the non-terminal that produces it
- **ACCEPT** — success
- **ERROR**

📌 ⭐ **A HANDLE is a substring matching the right-hand side of a production, whose reduction is a correct step in the reverse rightmost derivation.** (Not every matching substring is a handle — position matters.)

📌 ⭐ **LR(k) means: L**eft-to-right scan, **R**ightmost derivation in reverse, **k** lookahead tokens.

### ⭐⭐⭐ The power hierarchy

📌 ⭐⭐ **LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1) [= LR(1)]**

| Parser | Item type | ⭐ Lookahead used for reduction | ⭐ Number of states | 💡 Note |
|---|---|---|---|---|
| **LR(0)** | LR(0) items | ⭐ **None** | Fewest | Weakest |
| ⭐ **SLR(1)** | LR(0) items | ⭐ **The FOLLOW set** of the non-terminal | ⭐ **Same as LR(0)** | "Simple LR" — cheap but crude |
| ⭐ **LALR(1)** | LR(1) items, ⭐ **states with identical CORES MERGED** | Merged lookaheads | ⭐ **SAME as SLR** | ⭐ **Used by `yacc`/`bison`** — the best power/size trade-off. ⭐ **Merging can introduce REDUCE–REDUCE conflicts but NEVER shift–reduce conflicts** |
| ⭐ **CLR(1)** | LR(1) items | ⭐ **Exact lookahead per item** | ⭐ **MOST** | Most powerful, largest tables |

⚠⚠ ⭐ **Number of states: SLR = LALR ≤ CLR.** ⭐ **SLR and LALR have IDENTICAL state counts** (LALR is built by merging CLR states down to the LR(0) state set). CLR generally has more. This is asked directly.

💡 **Why LALR is the practical choice:** it has SLR's small tables but nearly CLR's power. The merging occasionally creates a reduce–reduce conflict, but for real programming-language grammars this almost never happens.

### ⭐ Conflicts

- ⭐ **Shift–reduce conflict** — the parser could either shift or reduce (the **dangling else** is the classic case; `yacc` resolves it by preferring **shift**)
- ⭐ **Reduce–reduce conflict** — two different reductions are possible

### ⭐⭐ LL vs LR

| | ⭐ **LL (top-down)** | ⭐ **LR (bottom-up)** |
|---|---|---|
| Derivation | **Leftmost** | ⭐ **Rightmost in REVERSE** |
| Tree built | Root → leaves | ⭐ **Leaves → root** |
| ⭐ **Left recursion** | ⭐ **MUST be removed** | ⭐ **Handled naturally** |
| Left factoring | Required | Not required |
| Power | Weaker | ⭐ **Stronger** |
| Hand-coding | ⭐ **Easier** | Harder — use a generator |

⭐ **Operator precedence parsing** — a simple bottom-up technique driven by a precedence-relation table. ⚠ Cannot handle **ε-productions** or the unary-minus ambiguity.

**Parser generators:** ⭐ **`yacc`/`bison` (LALR(1))** · ANTLR (LL(*)).

---

## 11. ⭐⭐ Syntax-directed translation (SDT)

### 💡 The idea

A parse tree tells you the *structure*. But to generate code you must **compute things** over that structure — types, values, addresses. **SDT** attaches **attributes** to grammar symbols and **semantic rules** to productions, so information flows through the tree.

## 11.1 ⭐⭐⭐ Synthesized vs inherited attributes

| | ⭐ **Synthesized** | ⭐ **Inherited** |
|---|---|---|
| ⭐ **Computed from** | ⭐ **The node's CHILDREN** | ⭐ **The node's PARENT and/or SIBLINGS** |
| ⭐ **Information flows** | ⭐ **UPWARD** (bottom-up) | ⭐ **DOWNWARD / sideways** |
| Evaluated by | A **bottom-up** traversal | Top-down / mixed traversal |

### 🔢 Examples that make the distinction clear

🔢 **Synthesized** — computing an expression's value:
```
E → E₁ + T    { E.val = E₁.val + T.val }
```
The parent's value comes **from its children**. ⭐ Classic synthesized attribute.

🔢 **Inherited** — propagating a declaration's type:
```
D → T L       { L.type = T.type }
L → L₁ , id   { L₁.type = L.type;  addtype(id.entry, L.type) }
```
In `int a, b, c;` the type `int` is known at `T` and must flow **down** into the identifier list. ⭐ Classic inherited attribute.

📌 ⭐ **TERMINALS only ever have SYNTHESIZED attributes** — supplied by the lexer (e.g. `id.lexval`). A terminal has no children to inherit from and nothing below it.

## 11.2 ⭐⭐ S-attributed and L-attributed definitions

📌 ⭐ **S-attributed definition — uses ONLY SYNTHESIZED attributes.**
✅ ⭐ Can be evaluated in a **single BOTTOM-UP pass**, so it works directly with **LR parsers** and `yacc`.

📌 ⭐ **L-attributed definition — each inherited attribute of a symbol depends only on the PARENT and on SIBLINGS TO ITS LEFT.**
✅ ⭐ Can be evaluated in a **single LEFT-TO-RIGHT depth-first pass**, so it works with **LL parsers**.

📌 ⭐⭐ **Every S-attributed definition is L-attributed, but NOT conversely.**
💡 *Why:* S-attributed has no inherited attributes at all, so the L-condition is trivially satisfied.

**Annotated parse tree** — a parse tree with all attribute values filled in.
**Dependency graph** — shows which attribute depends on which; ⭐ **it must be ACYCLIC** for evaluation to be possible.
**Translation scheme** — an SDD with semantic **actions** embedded at specific positions inside the production body (`A → α {action} β`).

---

## 12. ⭐⭐ Intermediate code generation

### 💡 Why an intermediate representation at all

⭐ **Three reasons:**
1. **Machine independence** — the front end need know nothing about the target CPU
2. **Easier optimisation** — a simple, uniform IR is far easier to analyse than either source code or assembly
3. ⭐ **Retargetability** — **m + n** translators instead of **m × n** (§8)

## 12.1 ⭐⭐ Three-address code (TAC)

📌 ⭐ **Each instruction has AT MOST ONE OPERATOR and at most three addresses** (typically result, operand1, operand2), using **temporaries** to hold intermediate values.

### 🔢 Worked example

**Source:** `a = b * c + b * d`

```
t1 = b * c
t2 = b * d
t3 = t1 + t2
a  = t3
```
⭐ Each line has exactly one operator — which is why it is trivially close to machine instructions.

🔢 **`x = (a + b) * (c - d)`:**
```
t1 = a + b
t2 = c - d
t3 = t1 * t2
x  = t3
```

**Instruction forms:** `x = y op z` · `x = op y` · `x = y` · `goto L` · `if x relop y goto L` · `param x` / `call p, n` / `return y` · `x = y[i]` / `x[i] = y` · `x = &y` / `x = *y` / `*x = y`.

## 12.2 ⭐⭐⭐ Three implementations of TAC

| Representation | ⭐ Structure | ⭐ Trade-off |
|---|---|---|
| ⭐ **Quadruples** | ⭐ **(op, arg1, arg2, RESULT)** — explicit temporary names | ⭐ **Instructions can be MOVED/REORDERED easily** (best for optimisation). ❌ Uses more space |
| ⭐ **Triples** | ⭐ **(op, arg1, arg2)** — the result is referenced by the **triple's POSITION/INDEX** | ✅ Compact. ⚠ ⭐ **Moving an instruction BREAKS all references to it** |
| ⭐ **Indirect triples** | Triples **plus a separate LIST OF POINTERS** giving the order | ⭐ **Compact AND reorderable — the best of both** |

### 🔢 Illustrating the difference

For `a = b * c + b * d`:

**Quadruples:**
```
     op    arg1  arg2  result
(0)  *     b     c     t1
(1)  *     b     d     t2
(2)  +     t1    t2    t3
(3)  =     t3    -     a
```

**Triples:**
```
     op    arg1  arg2
(0)  *     b     c
(1)  *     b     d
(2)  +     (0)   (1)     ← refers to triples by POSITION
(3)  =     a     (2)
```

⚠ ⭐ **Now try to move instruction (0) to a different position.** With quadruples, `t1` is a name and nothing breaks. With triples, every `(0)` reference becomes wrong, and every subsequent index shifts.

⭐ **That is the whole exam point: quadruples are easily reorderable; plain triples are not; indirect triples fix it by adding an indirection layer.**

## 12.3 ⭐ Other intermediate representations

**Syntax tree / AST** — structural, close to the source.
⭐ **DAG (Directed Acyclic Graph)** — like a syntax tree but with ⭐ **common subexpressions SHARED**, so redundancy is exposed structurally.

🔢 For `a = b * c + b * c`:
```
Syntax tree:              DAG:
      =                        =
     / \                      / \
    a   +                    a   +
       / \                      / \
      *   *                      \ /
     /\   /\                      *      ⭐ ONE shared node
    b  c b  c                    / \
                                b   c
```
⭐ **The DAG immediately reveals that `b * c` is computed twice** — which is exactly what common subexpression elimination needs to know.

**SSA (Static Single Assignment)** — every variable is assigned exactly once, which greatly simplifies data-flow analysis. Used by LLVM and modern JITs.
**Postfix notation · bytecode.**

⭐ **Backpatching** — when generating code for boolean expressions and control flow, the jump **targets are not yet known**. Backpatching emits the jumps with blank targets, keeps a list of them, and fills them in once the destination is generated — avoiding a second pass.

---

## 13. ⭐⭐ Runtime environments

### 💡 The idea

The compiler must decide, at compile time, how the program's data will be laid out at run time — and generate code that manages it.

## 13.1 ⭐ Storage allocation

| Area | ⭐ Holds | Allocation |
|---|---|---|
| **Code / text** | Machine instructions | Static |
| **Static / global** | Globals, static variables | Static (fixed at compile time) |
| ⭐ **Stack** | ⭐ **ACTIVATION RECORDS for procedure calls** | Automatic, LIFO |
| ⭐ **Heap** | Dynamically allocated data | Manual or garbage-collected |

## 13.2 ⭐⭐ The activation record (stack frame)

📌 ⭐ **Contents, in typical order:**
```
┌──────────────────────┐
│  Returned value      │
│  Actual parameters   │
│  Control link        │  ← the CALLER's frame pointer (dynamic link)
│  Access link         │  ← for non-local access (static link)
│  Saved machine status│  ← including the RETURN ADDRESS
│  Local data          │
│  Temporaries         │
└──────────────────────┘
```

⭐ **Created on procedure ENTRY, destroyed on RETURN.**
💡 ⭐ **This is exactly why recursion works:** each invocation gets its **own** frame with its **own** copy of the parameters and locals, so ten nested calls have ten independent sets of variables. (Same point as Week 3's recursion trace, seen from the compiler's side.)

⚠⚠ ⭐ **The ACTIVATION RECORD is a RUN-TIME structure on the STACK. The SYMBOL TABLE is a COMPILE-TIME structure.** They hold superficially similar information (names, types) and are constantly confused.

**Activation tree** — represents the nesting of procedure activations during one execution.
**Display** — an array of frame pointers giving fast access to enclosing scopes with nested procedures.

## 13.3 ⭐⭐⭐ Static vs dynamic scoping

| | ⭐ **Static (lexical) scoping** | ⭐ **Dynamic scoping** |
|---|---|---|
| ⭐ **A name refers to** | ⭐ **The declaration in the enclosing block IN THE SOURCE TEXT** | ⭐ **The declaration in the MOST RECENT ACTIVATION on the call stack** |
| ⭐ **Resolved at** | ⭐ **COMPILE time** | ⭐ **RUN time** |
| Used by | ⭐ **C, C++, Java, and virtually all modern languages** | Older Lisp, some shell scripts, Perl's `local` |

### 🔢⭐⭐ The standard example

```c
int x = 10;                        // global

void f() { printf("%d", x); }      // which x?

void g() { int x = 20; f(); }      // local x = 20, then calls f

int main() { g(); }
```

⭐ **Static scoping prints 10.** `f` is written at the top level of the file, so its `x` is resolved (at compile time) to the **global** x. `g`'s local x is irrelevant — it is not lexically visible from f.

⭐ **Dynamic scoping would print 20.** At run time the most recent activation containing an `x` is `g`'s, so `f` would see 20.

💡 ⭐ **Why static scoping won:** you can determine what every name refers to by **reading the source**, without knowing the call history. Dynamic scoping makes a function's behaviour depend on **who called it**, which is nearly impossible to reason about.

## 13.4 ⭐⭐⭐ Parameter passing mechanisms

| Mechanism | ⭐ Semantics | Languages |
|---|---|---|
| ⭐ **Call by value** | A **COPY** is passed; the caller's variable is unaffected | ⭐ **C, Java (primitives)** |
| ⭐ **Call by reference** | The **ADDRESS** is passed; changes are visible to the caller | C++ (`&`), Pascal (`var`), Fortran |
| ⭐ **Call by value-result (copy-restore)** | Copy **in** on entry, ⭐ **copy BACK on return** | Ada (`in out`), some Fortran |
| ⭐ **Call by name** | The **argument EXPRESSION is substituted textually** and ⭐ **RE-EVALUATED at every use** | Algol 60 (mostly of theoretical interest) |
| **Call by sharing** | The reference value is copied (mutate yes, reassign no) | Java (objects), Python |

### 🔢⭐⭐ The distinguishing example

```c
int a = 1;
int arr[] = {1, 2, 3};       // arr[0]=1, arr[1]=2, arr[2]=3

void f(int x) {
    x = x + 1;
    a = a + 1;
}

f(arr[a]);                    // a is 1, so the argument is arr[1] = 2
```

| Mechanism | ⭐ What happens |
|---|---|
| ⭐ **Call by VALUE** | `arr[1]`'s value (2) is **copied** into x. x becomes 3 locally and is discarded. `a` becomes 2. ⭐ **`arr` is UNCHANGED** |
| ⭐ **Call by REFERENCE** | x is an alias for `arr[1]` (bound **once**, at call time). `arr[1]` becomes 3. `a` becomes 2 |
| ⭐ **Call by VALUE-RESULT** | x = 2 → becomes 3 → **copied back** to `arr[1]` on return. Same final result as reference here, but the write happens at **return**, not immediately |
| ⭐ **Call by NAME** | x is literally the **text `arr[a]`**, re-evaluated at each use. `x = x + 1` runs **after** `a` might change, so it may read `arr[1]` and write `arr[2]` — ⭐ **a DIFFERENT array element** |

⭐⭐ **The exam point: call by name and call by value-result give DIFFERENT results whenever the argument is a SUBSCRIPTED VARIABLE whose index changes during the call.** That is precisely why exam questions use `arr[a]` with `a` being modified.

**Garbage collection:** **reference counting** (simple, but ⚠ fails on cyclic structures) · **mark-and-sweep** · **copying/generational** (exploits the fact that most objects die young) · mark-compact.

---

## 14. ⭐⭐⭐ Code optimisation

## 14.1 ⭐ The criteria

⭐ **An optimisation must:**
1. ⭐ **PRESERVE the program's MEANING (semantics)** — correctness first, always
2. Produce a measurable improvement **on average**
3. Be worth its own compilation cost

## 14.2 ⭐⭐ Basic blocks and flow graphs

📌 ⭐ **A BASIC BLOCK is a maximal sequence of consecutive instructions with ONE ENTRY POINT (the first instruction) and ONE EXIT POINT (the last)** — no jumps in except at the start, and none out except at the end.

💡 **Why they matter:** inside a basic block, control flow is completely straight-line, so you can reason about it very simply. All **local** optimisation happens within a basic block.

⭐ **Identifying LEADERS (the first instruction of each block) — three rules:**
1. ⭐ The **FIRST** instruction of the program
2. ⭐ Any instruction that is the **TARGET of a jump**
3. ⭐ Any instruction **IMMEDIATELY FOLLOWING a jump** (conditional or unconditional)

Each leader begins a block extending to just before the next leader.

### 🔢 Worked example

```
1.  i = 1
2.  j = 1
3.  t1 = 10 * i
4.  t2 = t1 + j
5.  if t2 < 100 goto 8
6.  j = j + 1
7.  goto 3
8.  i = i + 1
9.  goto 2
```
**Leaders:**
- **1** (first instruction)
- **2** (target of `goto 2` at line 9)
- **3** (target of `goto 3` at line 7)
- **6** (immediately follows the conditional jump at line 5)
- **8** (target of the `goto 8` at line 5)

⭐ **Blocks: {1}, {2}, {3,4,5}, {6,7}, {8,9}** — five basic blocks.

📌 **Control Flow Graph (CFG):** basic blocks as nodes, with edges for possible control transfers. ⭐ **Loops appear as strongly connected subgraphs with a single entry (the loop HEADER).**

## 14.3 ⭐⭐⭐ The optimisation techniques

| Technique | 💡 Description | 🔢 Example |
|---|---|---|
| ⭐ **Constant folding** | ⭐ **Evaluate a CONSTANT EXPRESSION at compile time** | `x = 4 * 3` → **`x = 12`** |
| ⭐ **Constant propagation** | ⭐ **Replace a VARIABLE known to hold a constant with that constant** | `a = 5; b = a + 2;` → `b = 5 + 2` → (then folding) `b = 7` |
| ⭐ **Common Subexpression Elimination (CSE)** | Reuse a previously computed identical expression | `x = b*c + d; y = b*c + e;` → `t = b*c; x = t+d; y = t+e;` |
| ⭐ **Dead code elimination** | Remove code whose result is **never used**, or which is **unreachable** | `x = 5;` when x is never read again |
| ⭐ **Copy propagation** | After `x = y`, use `y` wherever `x` appears | Enables further dead-code removal |
| ⭐ **Strength reduction** | ⭐ **Replace an EXPENSIVE operation with a CHEAPER one** | `x * 2` → **`x << 1`**; `x²` → `x*x`; a multiplication in a loop → repeated addition |
| ⭐ **Code motion / loop-invariant code motion** | ⭐ **Move a computation that does not change OUT of a loop** ("hoisting") | `for(...) { t = a*b; ... }` → `t = a*b; for(...) { ... }` |
| **Induction variable elimination** | Simplify variables that change by a fixed amount per iteration | |
| **Loop unrolling** | Replicate the loop body to reduce loop-control overhead | Trades code size for speed |
| **Loop fusion / jamming** | Merge adjacent loops with the same bounds | |
| **Function inlining** | Replace a call with the function's body | Removes call overhead; increases size |
| **Tail recursion elimination** | Convert tail recursion into a loop | Avoids stack growth (Week 3) |
| **Algebraic simplification** | `x + 0` → `x`; `x * 1` → `x`; `x * 0` → `0` | |
| ⭐ **Peephole optimisation** | Local improvements over a small **sliding window of TARGET code**: redundant load/store elimination, unreachable code, flow-of-control simplification, machine idioms | |

### ⚠⚠⭐ Constant folding vs constant propagation

⭐ These are **applied together** and **constantly confused**:
- ⭐ **FOLDING evaluates a constant EXPRESSION** — `4 * 3` becomes `12`. No variables involved.
- ⭐ **PROPAGATION substitutes a constant VALUE for a VARIABLE** — knowing `a = 5`, rewrite `a + 2` as `5 + 2`.

🔢 Together: `a = 5; b = a * 3;`
→ **propagation** gives `b = 5 * 3`
→ **folding** gives `b = 15`
→ **dead code elimination** may then remove `a = 5` if `a` is never used again.

## 14.4 ⭐ Scope of optimisation

| Scope | 💡 Extent |
|---|---|
| ⭐ **LOCAL optimisation** | ⭐ **Within a SINGLE BASIC BLOCK** — ⭐ **this is what the syllabus names** |
| **Global optimisation** | Across basic blocks within one procedure — ⭐ **requires DATA FLOW ANALYSIS** (§15) |
| **Interprocedural** | Across procedure boundaries |

Also: **machine-dependent** (register allocation, instruction scheduling, peephole) vs **machine-independent** (everything in §14.3).

## 14.5 ⭐ Register allocation

📌 ⭐ **Goal: keep frequently used values in REGISTERS to minimise memory traffic.**

⭐ **Solved by GRAPH COLOURING:**
1. Build a **register interference graph** — one node per value, with an edge between two values that are **live at the same time** (they cannot share a register)
2. **Colour** the graph with k colours, where k = the number of available registers
3. ⭐ Values that cannot be coloured are **SPILLED** to memory

💡 ⭐ **This is why LIVENESS analysis (§15) matters** — you cannot build the interference graph without knowing which values are simultaneously live.

---

## 15. ⭐⭐⭐ Data flow analysis

### 💡 The idea

**Local** optimisation (within one basic block) is easy — control flow is straight-line. But to optimise **across** blocks you must know things like *"could this variable hold a constant here, considering every path that reaches this point?"*

📌 ⭐ **Data flow analysis gathers information about how data flows along the paths of the control flow graph**, by setting up equations and solving them **iteratively to a FIXED POINT** (repeat until nothing changes).

📌 **The general form of a forward equation:**
**OUT[B] = GEN[B] ∪ (IN[B] − KILL[B])**
💡 *"What holds at the end of this block = what this block newly generates, plus what came in and was not destroyed here."*

## 15.1 ⭐⭐ The three analyses named in the syllabus

### ⭐ (a) Reaching definitions

📌 **The question: WHICH DEFINITIONS of a variable MAY REACH this point?**

- ⭐ **Direction: FORWARD** · ⭐ **Meet operator: UNION (∪)** — a **"MAY"** (existential) property
- 📌 `OUT[B] = GEN[B] ∪ (IN[B] − KILL[B])`; `IN[B] = ∪ OUT[P]` over all **predecessors** P
- ⭐ **Enables: constant propagation, copy propagation**, and detecting use of possibly-uninitialised variables

💡 **Why UNION:** you want to know if a definition reaches along **any** path, so you take the union over predecessors.

### ⭐⭐ (b) Liveness analysis (live variable analysis)

📌 ⭐ **A variable is LIVE at a point if there is a path from that point to a USE of it, with NO INTERVENING REDEFINITION.** Otherwise it is **DEAD**.

- ⭐ **Direction: BACKWARD** · ⭐ **Meet operator: UNION (∪)** — a "may" property
- 📌 `IN[B] = USE[B] ∪ (OUT[B] − DEF[B])`; `OUT[B] = ∪ IN[S]` over all **successors** S
- ⭐⭐ **Enables: DEAD CODE ELIMINATION and REGISTER ALLOCATION**

💡 ⭐ **Why liveness runs BACKWARD:** "will this value be used **later**?" is a question about the **future** of the program. So information must flow from successors back toward predecessors.

💡 **Why it enables both optimisations:**
- If a variable is **dead** immediately after an assignment, the assignment is **useless** → dead code elimination
- Two variables that are **never simultaneously live** can share a register → register allocation (§14.5)

### 🔢 Worked liveness example

```
1:  x = 1          // x defined
2:  y = x + 2      // x USED here  →  x is live over 1..2
3:  x = 5          // x REDEFINED  →  the value from line 1 is now DEAD
4:  z = y          // y USED here  →  y is live over 2..4
5:  print z        // z used
```
- The definition at line 1 is **live** until line 2, then **dead** (line 3 overwrites it)
- ⭐ **If line 2 did not exist, `x = 1` would be dead code and removable**
- `y` is live from line 2 to line 4
- `x` is dead after line 3 (never used again) → ⭐ **`x = 5` is dead code**

### ⭐ (c) Available expressions

📌 **The question: has this expression ALREADY been computed on EVERY path to here, with no operand redefined since?**

- ⭐ **Direction: FORWARD** · ⭐⭐ **Meet operator: INTERSECTION (∩)** — a **"MUST"** (universal) property
- 📌 `IN[B] = ∩ OUT[P]` over all **predecessors** P
- ⭐⭐ **Enables: COMMON SUBEXPRESSION ELIMINATION**

💡 ⭐ **Why INTERSECTION and not union:** you may only reuse a previously computed value if it was computed on **EVERY** path reaching this point. If even one path skips the computation, the value may not exist — so you need the intersection.

## 15.2 ⭐⭐⭐ The summary table — memorise it

| Analysis | ⭐ Direction | ⭐ Meet operator | May / Must | ⭐ Enables |
|---|---|---|---|---|
| ⭐ **Reaching definitions** | **Forward** | **∪ (union)** | May | Constant / copy propagation |
| ⭐ **Live variables** | ⭐ **BACKWARD** | **∪ (union)** | May | ⭐ **Dead code elimination, register allocation** |
| ⭐ **Available expressions** | **Forward** | ⭐ **∩ (INTERSECTION)** | Must | ⭐ **Common subexpression elimination** |
| **Very busy / anticipated expressions** | Backward | ∩ | Must | Code hoisting |

⚠⚠ ⭐ **The two facts that carry most of the marks in this topic:**
📌 ⭐ **LIVENESS is the BACKWARD one.**
📌 ⭐ **AVAILABLE EXPRESSIONS is the INTERSECTION one.**

💡 **A pattern worth noticing:** *may* analyses use **union** (does it hold on **some** path?); *must* analyses use **intersection** (does it hold on **all** paths?).

**Other concepts:** `u-d` chains (use-definition) and `d-u` chains · ⭐ **dominators** (node A dominates B if **every** path from entry to B passes through A) · **natural loops** and **back edges** · **SSA form** (simplifies all of the above by giving each variable exactly one definition).

---

# 16. ⭐ Rapid-fire facts

## Software Engineering

| Fact | Value |
|---|---|
| Defect cost rises | ~10× per later stage |
| Interview vs questionnaire | Depth / scale |
| Observation problem | **Hawthorne effect** |
| MIS vs DSS | **Routine reports / ad-hoc analytical decisions** |
| "Response < 2 s" | ⭐ **NON-functional** requirement |
| "Shall generate a report" | Functional requirement |
| **Verification / validation** | ⭐ **Building it right / building the right thing** |
| SRS produced in | Requirement analysis phase |
| Good SRS characteristics | Complete, consistent, unambiguous, **verifiable**, traceable, modifiable, ranked |
| **TELOS** | Technical, Economic, Legal, Operational, Schedule |
| **Level-0 DFD** | ⭐ **Context diagram — whole system as ONE process, NO data stores** |
| **DFD does NOT show** | ⭐ **Control flow, decisions, loops, timing** |
| DFD symbols (only 4) | Process, data flow, data store, external entity |
| DFD forbidden flows | Entity→entity, store→store, store→entity |
| Balancing | Inputs/outputs match between levels |
| Process with no output | **Black hole** |
| Timing behaviour needs | **State transition diagram** |
| Decision table, n conditions | **2ⁿ** rules |
| **"Risk-driven"** | ⭐ **SPIRAL** |
| **"Testing mirrors development"** | ⭐ **V-MODEL** |
| **"No working software until late"** | ⭐ **WATERFALL** |
| "Requirements unclear" | **Prototyping** |
| Spiral quadrants | Planning, **risk analysis**, engineering, evaluation |
| Agile values | Working software, customer collaboration, responding to change |
| Scrum sprint length | **2–4 weeks** |
| Scrum Master is | A **facilitator**, not a manager |
| Daily stand-up length | **15 minutes** |
| Sprint review / retrospective | **Product / process** |
| Scrum vs Kanban | Fixed sprints / **continuous flow with WIP limits** |
| **Language-independent size metric** | ⭐ **Function points** |
| FP function types | EI, EO, EQ, ILF, EIF |
| VAF range | **0.65 to 1.35** |
| **COCOMO organic** | ⭐ **E = 2.4 × KLOC^1.05** |
| COCOMO modes | **Organic, semi-detached, embedded** |
| COCOMO exponent b | **> 1 → diseconomy of scale** |
| Staff size | E / D |
| **Brooks's law** | Adding people to a late project makes it **later** |
| **PERT expected time** | ⭐ **(t_o + 4t_m + t_p)/6** |
| PERT σ | (t_p − t_o)/6 |
| **Critical path** | ⭐ **LONGEST path; ZERO slack** |
| Slack | LS − ES = LF − EF |
| **PERT vs CPM** | ⭐ **Probabilistic / deterministic** |
| Gantt chart does NOT show | **Dependencies, critical path** |
| Risk exposure | Probability × loss |
| DRE | E/(E+D) |
| Design goal | ⭐ **High cohesion, low coupling** |
| **Best / worst cohesion** | ⭐ **Functional / coincidental** |
| **Best / worst coupling** | ⭐ **Data / content** |
| Cohesion order | F S C P T L C |
| Coupling order | D S C E C C |
| **Cyclomatic complexity** | ⭐ **E − N + 2 = predicates + 1 = regions + 1** |
| Walkthrough vs inspection | Informal, author-led / **formal, checklist, moderator** |
| Error → fault → failure | Human mistake → flaw → observable behaviour |
| Testing shows | **Presence**, never absence, of defects |
| **BVA, equivalence partitioning** | ⭐ **BLACK-box** |
| Statement/branch/path coverage | **WHITE-box** |
| **Coverage strength** | ⭐ **statement < branch < condition < path** |
| **100% statement coverage** | ⭐ **Does NOT imply 100% branch coverage** |
| BVA for range 1–100 | 0, 1, 2, 50, 99, 100, 101 |
| Mutation testing evaluates | The **test suite** |
| **Top-down integration needs** | ⭐ **STUBS** |
| **Bottom-up integration needs** | ⭐ **DRIVERS** |
| Stub / driver | Dummy **called** / dummy **calling** module |
| **Alpha / beta testing** | ⭐ **Developer's site / customer's site** |
| Re-run tests after a change | ⭐ **Regression testing** |
| **Load vs stress** | ⭐ **At limits / BEYOND limits** |
| TDD | Write the **failing test first** |
| Acceptance testing done by | The **customer** |
| **Lowest-risk changeover** | ⭐ **Parallel** (highest cost) |
| Highest-risk changeover | **Direct/plunge** |
| **Porting to a new OS** | ⭐ **ADAPTIVE** maintenance |
| **Adding a requested feature** | ⭐ **PERFECTIVE** maintenance |
| Fixing a reported bug | **Corrective** |
| Refactoring for the future | **Preventive** |
| **Largest maintenance share** | ⭐ **Perfective (~50–65%)** |
| Maintenance share of lifecycle cost | **60–70%** |
| Lehman's laws | Continuing change, increasing complexity |
| Recovers design from code | **Reverse engineering** |
| ISO 9126 factors | Functionality, reliability, usability, efficiency, maintainability, portability |
| **CMM levels** | ⭐ **1 Initial, 2 Repeatable, 3 Defined, 4 Managed/Quantitative, 5 Optimising** |
| SQA vs SQC | Process/preventive vs **product/detective** |
| **Availability** | ⭐ **MTTF/(MTTF+MTTR)** |
| MTBF | MTTF + MTTR |

## Compiler Design

| Fact | Value |
|---|---|
| **Phase order** | ⭐ **Lexical → syntax → semantic → ICG → optimise → codegen** |
| **Front end / back end** | ⭐ **Phases 1–4 / 5–6** |
| Why the split | **m + n** instead of m × n translators |
| Span all phases | **Symbol table + error handler** |
| **Undeclared variable** | ⭐ **SEMANTIC error** |
| **Type mismatch** | ⭐ **SEMANTIC error** |
| Missing semicolon | **Syntax** error |
| `12abc` | **Lexical** error |
| Array index out of bounds | **Run time** |
| Compiler vs interpreter | Whole program / **statement by statement** |
| Resolves external references | **Linker** |
| Single-pass compiler | Fast but **limits optimisation** |
| **Lexical analysis specified by** | ⭐ **Regular expressions → DFA** |
| Why lexing is separate | RE cannot express **nested/balanced** constructs |
| **Longest-match rule** | ⭐ **Maximal munch** (`>=` is one token) |
| Token vs lexeme vs pattern | Category / actual text / rule |
| Terminals have | ⭐ **Only synthesized attributes** |
| **Left recursion** | ⭐ **Must be removed for LL; LR prefers it** |
| Left factoring fixes | Common **prefix** |
| **ε in FOLLOW sets** | ⭐ **NEVER** (but `$` can be) |
| FOLLOW(start) contains | **$** |
| **LL(1)** | Left-to-right, **leftmost**, 1 lookahead |
| Ambiguous grammar is LL(1)? | ⭐ **Never** |
| Left-recursive grammar is LL(1)? | Never |
| **Bottom-up produces** | ⭐ **Rightmost derivation in REVERSE** |
| Shift-reduce actions | Shift, reduce, accept, error |
| Handle | Substring whose reduction is a correct step |
| **Parser power order** | ⭐ **LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1)** |
| **yacc/bison uses** | ⭐ **LALR(1)** |
| **Same number of states** | ⭐ **SLR and LALR** |
| LALR merging can create | ⭐ **Reduce–reduce** conflicts only |
| Dangling else is a | **Shift–reduce** conflict |
| **Synthesized attribute** | ⭐ **From CHILDREN (bottom-up)** |
| **Inherited attribute** | ⭐ **From PARENT/SIBLINGS** |
| **S-attributed** | Only synthesized; **single bottom-up pass**; works with LR |
| **L-attributed** | Parent + **left** siblings; single left-to-right pass; works with LL |
| S-attributed ⊂ L-attributed | ⭐ **Yes (one-way)** |
| Dependency graph must be | **Acyclic** |
| Three-address code | ≤ 1 operator per instruction |
| **Easiest TAC form to reorder** | ⭐ **QUADRUPLES** |
| Triples reference results by | **Position/index** |
| **Compact AND reorderable** | ⭐ **Indirect triples** |
| **Shares common subexpressions** | ⭐ **DAG** |
| Fills in unknown jump targets | **Backpatching** |
| SSA | Each variable assigned once |
| **Run-time call info in** | ⭐ **Activation record (STACK)** |
| Symbol table is | ⭐ **A COMPILE-TIME structure** |
| Activation record contents | Params, control link, return address, locals, temporaries |
| Why recursion works | Each call gets its **own** frame |
| **C uses** | ⭐ **Static scoping, call by value** |
| Static scoping resolved at | **Compile** time |
| Dynamic scoping resolved at | **Run** time |
| Call by name | Argument **re-evaluated at each use** |
| Call by value-result | Copy in, **copy back at return** |
| Reference counting fails on | **Cyclic** structures |
| **Basic block** | ⭐ **One entry, one exit** |
| Leaders | First instruction, jump targets, instructions **after** jumps |
| **`x = 4*3` → `x = 12`** | ⭐ **Constant FOLDING** |
| **`a=5; b=a+2` → `b=5+2`** | ⭐ **Constant PROPAGATION** |
| **`x*2` → `x<<1`** | ⭐ **Strength reduction** |
| Moving invariant code out of a loop | **Code motion / hoisting** |
| Sliding window on target code | **Peephole** optimisation |
| **Local optimisation scope** | ⭐ **A single basic block** |
| Global optimisation requires | ⭐ **Data flow analysis** |
| **Register allocation via** | ⭐ **Graph colouring** (needs liveness) |
| Uncolourable value is | **Spilled** |
| **Reaching definitions** | Forward, ∪, may |
| **Liveness analysis** | ⭐ **BACKWARD, ∪** — dead code + register allocation |
| **Available expressions** | ⭐ **Forward, ∩ (INTERSECTION)** — CSE |
| May analyses use / must use | **Union / intersection** |
| Dominator | Every path from entry passes through it |

---

# 17. ⚠ Common traps

**Software Engineering**
1. ⭐⭐⭐ **TOP-DOWN needs STUBS; BOTTOM-UP needs DRIVERS.** The most common error in this section.
2. ⭐⭐ **Functional cohesion is BEST, coincidental WORST; data coupling BEST, content WORST.**
3. ⭐⭐ **The critical path is the LONGEST path**, not the shortest.
4. ⭐⭐ **Adaptive = ENVIRONMENT change; perfective = ENHANCEMENT; corrective = BUG; preventive = future-proofing.**
5. ⭐ **Verification = building it right; validation = building the right thing.**
6. ⭐ **Level-0 DFD = context diagram, and shows NO data stores.**
7. ⭐⭐ **A DFD shows no control flow, decisions or timing** — that needs a state transition diagram.
8. ⭐⭐ **100% statement coverage ≠ 100% branch coverage.**
9. ⭐ **Alpha at the DEVELOPER's site, beta at the CUSTOMER's.**
10. ⭐ **CMM level 4 is "Managed/Quantitative"; level 5 is "Optimising"** — do not stop at 4, and there is no level 0.
11. ⭐ **Spiral is risk-driven; V-model mirrors testing; waterfall delivers late.**
12. ⭐ **Function points are language-independent and available early; LOC is neither.**
13. **Parallel changeover = lowest risk, highest cost.**
14. **BVA and equivalence partitioning are black-box, not white-box.**
15. **Scrum Master is a facilitator, not a manager.**

**Compiler Design**
16. ⭐⭐⭐ **Undeclared variables and type mismatches are SEMANTIC errors**, not syntax errors.
17. ⭐⭐ **ε is NEVER in a FOLLOW set** (but `$` can be).
18. ⭐⭐ **LR parsers HANDLE left recursion; LL parsers CANNOT.**
19. ⭐⭐ **LALR has the SAME number of states as SLR**, not as CLR.
20. ⭐ **LALR merging can create reduce–reduce conflicts, never shift–reduce.**
21. ⭐⭐⭐ **LIVENESS analysis is BACKWARD.**
22. ⭐⭐⭐ **AVAILABLE EXPRESSIONS uses INTERSECTION**, not union.
23. ⭐⭐ **Constant folding ≠ constant propagation.**
24. ⭐ **Quadruples are reorderable; plain triples are not.**
25. ⭐ **The activation record is RUN-TIME (stack); the symbol table is COMPILE-TIME.**
26. ⭐ **Static scoping resolves by source text; dynamic by the call stack.**
27. **Bottom-up parsing gives a rightmost derivation in REVERSE.**
28. **A single-pass compiler limits optimisation.**

---

# 18. Practice

**Software Engineering — ⭐ the biggest untapped block in Paper-II:**
- [`Paper2_S10_Information_Systems_and_Software_Engineering/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S10_Information_Systems_and_Software_Engineering/) — ⭐ **337 questions** (ISRO 52 + NIELIT 70 + UGC-NET 215)
- ⚠ ⭐ **Zero GATE coverage.** If you have time for only one folder this week, this is it.

**Compiler Design:**
- GATE: [`Paper2_S07_Compiler_Design/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S07_Compiler_Design/) — **242 questions**
- State-PSC level: [`Paper2_S07_Compiler_Design/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S07_Compiler_Design/) — **170 questions**
- ⚠ ⭐ **Skip the automata-heavy questions** — Theory of Computation is **not** in the TPSC syllabus. You need only the CFG/parsing background covered here.

Test: [`Week_11_Test.md`](../04_Mock_Tests/Week_11_Test.md)

**Priority order if short on time:**
⭐ **SE** — cohesion/coupling orderings → maintenance types (as scenarios) → black-box vs white-box techniques → **stubs vs drivers** → process-model identification (spiral/V/waterfall) → CMM levels → cyclomatic complexity → COCOMO modes → critical path → DFD rules and limitations.
⭐ **Compiler** — the phase order and which phase catches which error → FIRST/FOLLOW construction → the LR power hierarchy → synthesized vs inherited attributes → the named optimisations (folding vs propagation) → **the data-flow analysis summary table**.
