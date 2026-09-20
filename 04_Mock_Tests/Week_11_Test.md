# Week 11 Question Bank — Software Engineering + Compiler Design

**Syllabus §10 + §7** · 153 questions · Practice set · +1 / −0.33 marking

> Definitional and scenario-heavy for Software Engineering (the largest untapped Paper-II block); concept + FIRST/FOLLOW + cyclomatic for Compiler Design. Exactly four options, one correct. Answer key and worked solutions follow the questions.

---

## Part A — Fact-finding & Information Systems

**Q1.** The tendency of people to change their behaviour when they know they are being watched, which limits direct observation, is the
(A) halo effect  (B) Hawthorne effect  (C) placebo effect  (D) bandwagon effect

**Q2.** Which fact-finding technique is cheapest for collecting quantitative data from many respondents, but suffers low response rates and no ability to probe?
(A) Interviews  (B) Questionnaires  (C) Observation  (D) Record review

**Q3.** Which information system produces predefined, routine summary and exception reports for middle management from TPS data?
(A) DSS  (B) EIS  (C) MIS  (D) ERP

**Q4.** "What happens to profit if we cut price 8% and demand rises 15%?" — this ad-hoc what-if query is best served by a
(A) TPS  (B) MIS  (C) DSS  (D) OAS

**Q5.** Joint Application Development (JAD) is best described as
(A) a facilitated workshop bringing users and developers together for fast consensus
(B) a throwaway prototype shown to one user
(C) an organisation-wide questionnaire
(D) an automated code generator

**Q6.** A system that records day-to-day operational transactions such as sales and bookings is a
(A) MIS  (B) DSS  (C) TPS  (D) EIS

**Q7.** Strategic dashboards, external data and drill-down for top management are the hallmark of a(n)
(A) TPS  (B) MIS  (C) EIS/ESS  (D) expert system

---

## Part B — Requirements & Feasibility

**Q8.** "Response time must be under 2 seconds for 95% of requests" is a
(A) functional requirement  (B) non-functional requirement  (C) business rule  (D) user story

**Q9.** Verification answers the question
(A) "Are we building the right product?"
(B) "Are we building the product right?"
(C) "Is the product affordable?"
(D) "Do users like the product?"

**Q10.** Validation, unlike verification,
(A) requires no execution of the software
(B) checks conformance to the specification only
(C) checks whether the software meets the user's actual need, and requires execution
(D) is performed only by static analysis

**Q11.** "The system shall allow a user to reset their password" is an example of a
(A) non-functional requirement  (B) functional requirement  (C) design constraint  (D) quality attribute

**Q12.** Which of the following is NOT a characteristic of a good SRS?
(A) Complete  (B) Unambiguous  (C) Verifiable  (D) Ambiguous

**Q13.** In the TELOS framework, the dimension asking "will the organisation and its users actually use the system?" is
(A) technical feasibility  (B) economic feasibility  (C) operational feasibility  (D) legal feasibility

**Q14.** Cost–benefit analysis, ROI, NPV and payback period are tools of which feasibility dimension?
(A) technical  (B) economic  (C) operational  (D) schedule

**Q15.** "The system shall be available 99.9% of the time" is a
(A) functional requirement  (B) non-functional (availability) requirement  (C) business rule  (D) test case

---

## Part C — Data Flow Diagrams

**Q16.** The level-0 DFD, showing the entire system as a single process with its external entities, is the
(A) context diagram  (B) process specification  (C) data dictionary  (D) ER diagram

**Q17.** Which of the following does a DFD deliberately NOT show?
(A) data stores  (B) external entities  (C) control flow, decisions and timing  (D) data flows

**Q18.** To model event and timing behaviour that a DFD cannot express, you use a
(A) decision table  (B) state transition diagram  (C) structure chart  (D) data dictionary

**Q19.** A process in a DFD that has inputs but produces no output is called a
(A) miracle  (B) grey hole  (C) black hole  (D) sink

**Q20.** In a DFD, a direct data flow is FORBIDDEN (it must pass through a process) between
(A) an external entity and a process
(B) a process and a data store
(C) two data stores
(D) a process and an external entity

**Q21.** The rule that inputs and outputs of a process at level n must match those of its expansion at level n+1 is called
(A) partitioning  (B) balancing  (C) levelling  (D) normalisation

**Q22.** How many rules (columns) does a decision table with 4 binary conditions have?
(A) 8  (B) 12  (C) 16  (D) 32

---

## Part D — Software Process Models & Agile

**Q23.** Which process model is explicitly risk-driven, with an explicit risk-analysis step in every cycle?
(A) Waterfall  (B) V-model  (C) Spiral  (D) RAD

**Q24.** The principal drawback of the waterfall model is that
(A) it produces no documentation
(B) working software appears only very late and late requirement changes are very expensive
(C) it cannot handle small projects
(D) it has no defined phases

**Q25.** A process model in which every development phase has a corresponding testing phase is the
(A) spiral model  (B) V-model  (C) prototyping model  (D) incremental model

**Q26.** Which model is most appropriate when the user's requirements are unclear and cannot be articulated until something concrete is seen?
(A) waterfall  (B) V-model  (C) prototyping  (D) spiral

**Q27.** Which approach is best when requirements are expected to change frequently and the customer is available?
(A) waterfall  (B) agile  (C) V-model  (D) big-bang

**Q28.** In Scrum, the Scrum Master is
(A) the project manager who assigns tasks
(B) a facilitator who removes impediments and does not assign work
(C) the person who owns and prioritises the product backlog
(D) the customer representative

**Q29.** A Scrum sprint is typically
(A) 1 day  (B) 2–4 weeks  (C) 3–6 months  (D) 1 year

**Q30.** Which statement correctly distinguishes Scrum from Kanban?
(A) Scrum uses continuous flow; Kanban uses fixed sprints
(B) Scrum uses fixed-length sprints; Kanban uses continuous flow with WIP limits
(C) both use fixed sprints
(D) both forbid WIP limits

**Q31.** The sprint retrospective, unlike the sprint review, focuses on improving the
(A) product increment  (B) process  (C) product backlog  (D) budget

---

## Part E — Estimation & COCOMO

**Q32.** Which size metric is language-independent and can be measured from the requirements stage?
(A) LOC  (B) function points  (C) number of classes  (D) bytes of source

**Q33.** Which of the following is NOT one of the five function-point component types?
(A) External Inputs (EI)  (B) External Outputs (EO)  (C) Internal Logical Files (ILF)  (D) Cyclomatic complexity

**Q34.** If UFP = 200 and the 14 general system characteristics sum to 35, the adjusted FP is
(A) 130  (B) 200  (C) 270  (D) 235

**Q35.** In COCOMO, an organic-mode project is characterised by
(A) large size with tight hardware constraints
(B) a small team, familiar problem and flexible requirements
(C) unfamiliar embedded software
(D) mixed-experience teams with rigid constraints

**Q36.** The basic COCOMO effort equation for an organic project is
(A) E = 3.6 × KLOC^1.20  (B) E = 3.0 × KLOC^1.12  (C) E = 2.4 × KLOC^1.05  (D) E = 2.5 × KLOC^0.38

**Q37.** For an organic project of 32 KLOC (32^1.05 ≈ 37.4), the estimated effort is approximately
(A) 45 person-months  (B) 90 person-months  (C) 140 person-months  (D) 32 person-months

**Q38.** Because the COCOMO exponent b > 1 for all three modes, effort grows ___ with size.
(A) linearly  (B) sub-linearly  (C) super-linearly (a diseconomy of scale)  (D) not at all

---

## Part F — Scheduling, Risk & Metrics

**Q39.** Which chart shows task durations and overlap clearly but does NOT clearly show dependencies or the critical path?
(A) PERT chart  (B) Gantt chart  (C) CPM network  (D) DFD

**Q40.** PERT uses ___ time estimates, whereas CPM uses ___ estimates.
(A) deterministic; probabilistic
(B) probabilistic; deterministic
(C) single; single
(D) random; random

**Q41.** For t_o = 4, t_m = 6, t_p = 14, the PERT expected time t_e is
(A) 6  (B) 7  (C) 8  (D) 9

**Q42.** The critical path in a project network is the
(A) shortest path
(B) longest path, determining the minimum project duration
(C) path with maximum slack
(D) path with the fewest activities

**Q43.** In a network with paths A→C→D = 12 days, B→C→D = 11 days and B→E→D = 13 days, the project duration is
(A) 11 days  (B) 12 days  (C) 13 days  (D) 36 days

**Q44.** Risk exposure is computed as
(A) probability + loss  (B) probability × potential loss  (C) loss − probability  (D) loss / probability

**Q45.** If 60 defects are found before delivery and 15 are reported after delivery, the Defect Removal Efficiency (DRE) is
(A) 0.20  (B) 0.75  (C) 0.80  (D) 1.00

---

## Part G — Design & Coding

**Q46.** The single most important pair of design goals is
(A) low cohesion, high coupling
(B) high cohesion, low coupling
(C) high cohesion, high coupling
(D) low cohesion, low coupling

**Q47.** Which type of cohesion is the strongest (best)?
(A) coincidental  (B) logical  (C) temporal  (D) functional

**Q48.** Which type of cohesion is the weakest (worst)?
(A) functional  (B) sequential  (C) coincidental  (D) communicational

**Q49.** Which type of coupling is the best (most desirable)?
(A) content  (B) common  (C) data  (D) control

**Q50.** Which type of coupling is the worst (most undesirable)?
(A) data  (B) stamp  (C) control  (D) content

**Q51.** A control flow graph has 12 edges and 9 nodes. Its cyclomatic complexity is
(A) 3  (B) 4  (C) 5  (D) 21

**Q52.** A program has three `if` statements and no other branching. Its cyclomatic complexity is
(A) 3  (B) 4  (C) 6  (D) 8

**Q53.** A code review that is formal, checklist-driven and led by a moderator with recorded defects is a(n)
(A) walkthrough  (B) inspection  (C) desk check  (D) pair-programming session

---

## Part H — Testing

**Q54.** Boundary value analysis and equivalence class partitioning are techniques of
(A) white-box testing  (B) black-box testing  (C) unit testing only  (D) mutation testing

**Q55.** Which defect can black-box testing find but white-box testing inherently cannot?
(A) an untested branch
(B) missing functionality that was never coded
(C) unreachable code
(D) a logic error in existing code

**Q56.** The correct causal chain of terms is
(A) failure → fault → error
(B) error → fault → failure
(C) fault → error → failure
(D) error → failure → fault

**Q57.** The coverage criteria from weakest to strongest are
(A) path < condition < branch < statement
(B) statement < branch < condition < path
(C) branch < statement < path < condition
(D) condition < path < statement < branch

**Q58.** Achieving 100% statement coverage
(A) always implies 100% branch coverage
(B) does not imply 100% branch coverage
(C) is impossible to achieve
(D) implies 100% path coverage

**Q59.** In top-down integration testing, not-yet-written lower-level modules are replaced by
(A) drivers  (B) stubs  (C) mocks only  (D) harnesses

**Q60.** Bottom-up integration testing requires
(A) stubs  (B) drivers  (C) neither  (D) both always

**Q61.** Alpha testing is performed
(A) at the customer's site by end users
(B) at the developer's site, with developers present
(C) automatically by the compiler
(D) only after general release

**Q62.** Which testing determines system behaviour BEYOND its limits, to find the breaking point?
(A) load testing  (B) stress testing  (C) smoke testing  (D) sanity testing

**Q63.** Re-running existing tests after a change, to confirm nothing previously working has broken, is
(A) smoke testing  (B) regression testing  (C) stress testing  (D) exploratory testing

---

## Part I — Implementation & Maintenance

**Q64.** Which changeover strategy has the LOWEST risk (but the highest cost)?
(A) direct  (B) parallel  (C) phased  (D) pilot

**Q65.** The highest-risk changeover strategy, with no fallback, is
(A) parallel  (B) pilot  (C) direct/plunge  (D) phased

**Q66.** Porting an application to a new operating system is which type of maintenance?
(A) corrective  (B) adaptive  (C) perfective  (D) preventive

**Q67.** Adding a new report that users requested is which type of maintenance?
(A) corrective  (B) adaptive  (C) perfective  (D) preventive

**Q68.** Fixing a crash reported by a user is which type of maintenance?
(A) corrective  (B) adaptive  (C) perfective  (D) preventive

**Q69.** Refactoring a tangled module so future changes are easier is
(A) corrective  (B) adaptive  (C) perfective  (D) preventive

**Q70.** Which maintenance category consumes the LARGEST share of maintenance effort (~50–65%)?
(A) corrective  (B) adaptive  (C) perfective  (D) preventive

**Q71.** Maintenance typically consumes what share of a software system's total lifecycle cost?
(A) 10–20%  (B) 30–40%  (C) 60–70%  (D) under 10%

---

## Part J — Software Quality & CMM

**Q72.** In CMM/CMMI, level 5 is
(A) Initial  (B) Defined  (C) Managed  (D) Optimising

**Q73.** CMM level 1 (Initial) is characterised by
(A) quantitative process control
(B) ad-hoc, chaotic processes relying on individual heroics
(C) a documented, standardised process
(D) continuous process improvement

**Q74.** At which CMM level are process and product quantitatively measured and controlled?
(A) 2 (Repeatable)  (B) 3 (Defined)  (C) 4 (Managed/Quantitative)  (D) 5 (Optimising)

**Q75.** SQA (Software Quality Assurance) is
(A) product-oriented and detective
(B) process-oriented and preventive
(C) identical to testing
(D) performed only after release

**Q76.** Given MTTF = 950 hours and MTTR = 50 hours, the availability is
(A) 90%  (B) 95%  (C) 99%  (D) 5%

**Q77.** MTBF equals
(A) MTTF − MTTR  (B) MTTF + MTTR  (C) MTTF / MTTR  (D) MTTR − MTTF

---

## Part K — Compiler Phases & Errors

**Q78.** The correct order of the first three phases of a compiler is
(A) syntax → lexical → semantic
(B) lexical → syntax → semantic
(C) semantic → lexical → syntax
(D) lexical → semantic → syntax

**Q79.** The full phase order of a compiler is
(A) lexical → syntax → semantic → intermediate code → optimisation → code generation
(B) lexical → semantic → syntax → code generation → optimisation → intermediate code
(C) syntax → lexical → semantic → optimisation → code generation → intermediate code
(D) semantic → syntax → lexical → intermediate code → code generation → optimisation

**Q80.** The output of the lexical analysis phase is a
(A) parse tree  (B) token stream  (C) symbol table  (D) three-address code

**Q81.** The front end of a compiler comprises phases
(A) 1–4 (source-dependent, machine-independent)
(B) 5–6 only
(C) 1–2 only
(D) 3–6

**Q82.** With m source languages and n target machines, the "m + n" saving comes from
(A) writing m × n complete compilers
(B) sharing one intermediate representation between m front ends and n back ends
(C) using a single-pass compiler
(D) skipping optimisation

**Q83.** Which two components span ALL phases of a compiler?
(A) parser and lexer
(B) symbol table manager and error handler
(C) optimiser and code generator
(D) linker and loader

**Q84.** An undeclared variable is detected by
(A) lexical analysis  (B) syntax analysis  (C) semantic analysis  (D) the linker

**Q85.** A type mismatch such as `int x = "hello";` is
(A) a lexical error  (B) a syntax error  (C) a semantic error  (D) a runtime error

**Q86.** A missing semicolon is detected by
(A) lexical analysis  (B) syntax analysis  (C) semantic analysis  (D) run time

**Q87.** The malformed token `12abc` is caught by
(A) lexical analysis  (B) syntax analysis  (C) semantic analysis  (D) the loader

**Q88.** An array index going out of bounds is detected at
(A) lexical analysis  (B) syntax analysis  (C) semantic analysis  (D) run time

**Q89.** Which translates and executes a program statement by statement rather than as a whole?
(A) compiler  (B) interpreter  (C) assembler  (D) linker

**Q90.** Which system program combines object modules and resolves external references?
(A) loader  (B) linker  (C) preprocessor  (D) assembler

---

## Part L — Lexical Analysis

**Q91.** Lexical analysis is specified with ___ and implemented with ___.
(A) CFGs; pushdown automata
(B) regular expressions; finite automata
(C) attribute grammars; Turing machines
(D) decision tables; DFAs

**Q92.** In `int x = 10;` the number of tokens is
(A) 4  (B) 5  (C) 6  (D) 3

**Q93.** The actual character sequence matched, such as `count`, is the
(A) token  (B) lexeme  (C) pattern  (D) symbol

**Q94.** The rule describing the set of valid lexemes, e.g. `letter(letter|digit)*`, is the
(A) token  (B) lexeme  (C) pattern  (D) handle

**Q95.** By the maximal-munch (longest-match) rule, `>=` is recognised as
(A) two tokens `>` and `=`  (B) one token  (C) a syntax error  (D) a lexeme with no token

**Q96.** Why is lexical analysis kept as a separate phase from parsing?
(A) regular expressions cannot express nested/balanced constructs, which need a CFG
(B) parsing is always faster than lexing
(C) tokens require Turing machines
(D) both phases use exactly the same formalism

**Q97.** The tool that generates a scanner automatically from a regular-expression specification is
(A) yacc  (B) lex/flex  (C) bison  (D) ANTLR

---

## Part M — Parsing

**Q98.** For the grammar `E → E + E | E * E | id`, the string `id + id * id` has
(A) one parse tree  (B) two parse trees  (C) no parse tree  (D) infinitely many terminals

**Q99.** The dangling-else ambiguity is conventionally resolved by matching each `else` to the
(A) outermost `then`  (B) nearest unmatched `then`  (C) first `then`  (D) last `then` in the file

**Q100.** Left recursion must be eliminated before which kind of parsing?
(A) LR bottom-up  (B) top-down / LL(1)  (C) LALR  (D) operator precedence

**Q101.** Which statement about left recursion is correct?
(A) LR parsers cannot handle it
(B) LR parsers handle it naturally; only top-down parsers need it removed
(C) it must be removed for all parsers
(D) it is required for LL(1)

**Q102.** Which of the following is NEVER a member of a FOLLOW set?
(A) $  (B) a terminal  (C) ε  (D) )

**Q103.** FOLLOW(start symbol) always contains
(A) ε  (B) $  (C) the empty set  (D) all terminals

**Q104.** For the grammar `E → TE'`, `E' → +TE' | ε`, `T → FT'`, `T' → *FT' | ε`, `F → (E) | id`, FIRST(E) is
(A) { +, ε }  (B) { (, id }  (C) { *, id }  (D) { $, ) }

**Q105.** For the same grammar, FOLLOW(E) is
(A) { +, * }  (B) { ), $ }  (C) { (, id }  (D) { ε, $ }

**Q106.** For the same grammar, FIRST(T') is
(A) { *, ε }  (B) { +, ε }  (C) { (, id }  (D) { *, id }

**Q107.** LL(1) stands for
(A) Left-to-right scan, Leftmost derivation, 1 lookahead token
(B) Left-to-right scan, rightmost derivation, 1 lookahead
(C) two leftmost passes
(D) Last-in Last-out, 1 symbol

**Q108.** Bottom-up parsing produces a
(A) leftmost derivation
(B) rightmost derivation in reverse
(C) leftmost derivation in reverse
(D) random derivation

**Q109.** The parser power hierarchy, from weakest to strongest, is
(A) LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1)
(B) CLR(1) ⊂ LALR(1) ⊂ SLR(1) ⊂ LR(0)
(C) SLR(1) ⊂ LR(0) ⊂ CLR(1) ⊂ LALR(1)
(D) LALR(1) ⊂ SLR(1) ⊂ LR(0) ⊂ CLR(1)

**Q110.** The `yacc`/`bison` parser generators produce which type of parser?
(A) LL(1)  (B) LR(0)  (C) LALR(1)  (D) recursive descent

**Q111.** Which two parsers have the same number of states?
(A) LR(0) and CLR(1)  (B) SLR(1) and LALR(1)  (C) LL(1) and CLR(1)  (D) CLR(1) and LALR(1)

**Q112.** Merging states during LALR(1) construction can introduce
(A) shift–reduce conflicts
(B) reduce–reduce conflicts, but never shift–reduce conflicts
(C) both kinds equally
(D) no conflicts at all

---

## Part N — Syntax-Directed Translation & Intermediate Code

**Q113.** An attribute whose value at a node is computed from the attributes of its children is
(A) inherited  (B) synthesized  (C) global  (D) static

**Q114.** An attribute computed from a node's parent and/or siblings is
(A) synthesized  (B) inherited  (C) local  (D) terminal

**Q115.** An S-attributed definition uses only ___ attributes and can be evaluated in a single ___ pass.
(A) inherited; top-down
(B) synthesized; bottom-up
(C) inherited; bottom-up
(D) synthesized; top-down

**Q116.** Which statement about S-attributed and L-attributed definitions is TRUE?
(A) every L-attributed definition is S-attributed
(B) every S-attributed definition is L-attributed, but not conversely
(C) they are unrelated
(D) neither can be evaluated in one pass

**Q117.** `t1 = b * c` followed by `t2 = a + t1` is an example of
(A) three-address code  (B) postfix notation  (C) machine code  (D) a parse tree

**Q118.** Which three-address-code representation uses (op, arg1, arg2, result) and is the easiest to move/reorder?
(A) triples  (B) quadruples  (C) indirect triples  (D) DAG

**Q119.** In plain triples, a computed result is referenced by
(A) an explicit temporary name
(B) the triple's position/index
(C) a separate pointer list
(D) a register number

**Q120.** Which representation is both compact AND easily reorderable?
(A) quadruples  (B) plain triples  (C) indirect triples  (D) syntax tree

**Q121.** Which intermediate representation exposes common subexpressions by sharing nodes?
(A) parse tree  (B) DAG  (C) postfix notation  (D) quadruples

---

## Part O — Runtime Environments

**Q122.** At run time, a function's parameters, local variables and return address are stored in
(A) the symbol table
(B) an activation record on the stack
(C) the code segment
(D) a register file

**Q123.** The symbol table is a ___ structure, whereas the activation record is a ___ structure.
(A) run-time; compile-time
(B) compile-time; run-time
(C) both run-time
(D) both compile-time

**Q124.** In static (lexical) scoping, a name refers to
(A) the most recent activation on the call stack
(B) the declaration in the enclosing block in the source text, resolved at compile time
(C) a randomly chosen declaration
(D) always the global declaration

**Q125.** For the classic example (global `x = 10`; `f()` prints x; `g()` sets local `x = 20` then calls `f`), static scoping prints
(A) 10  (B) 20  (C) 30  (D) undefined

**Q126.** In call by value,
(A) the address of the argument is passed
(B) a copy is passed and the caller's variable is unaffected
(C) the argument expression is re-evaluated at each use
(D) the value is copied back on return

**Q127.** Call by name differs from call by value-result notably when the argument is
(A) a constant
(B) a subscripted variable whose index changes during the call
(C) a global variable
(D) a string literal

---

## Part P — Optimisation & Data Flow Analysis

**Q128.** A basic block is a maximal instruction sequence with
(A) many entry and exit points
(B) one entry point and one exit point
(C) no jumps at all anywhere in the program
(D) exactly one instruction

**Q129.** Which of the following is NOT a rule for identifying a leader of a basic block?
(A) the first instruction of the program
(B) the target of a jump
(C) the instruction immediately following a jump
(D) every arithmetic instruction

**Q130.** Replacing `x = 4 * 3` with `x = 12` at compile time is
(A) constant folding  (B) constant propagation  (C) strength reduction  (D) dead code elimination

**Q131.** Given `a = 5; b = a + 2;`, rewriting it as `b = 5 + 2` is
(A) constant folding  (B) constant propagation  (C) common subexpression elimination  (D) code motion

**Q132.** Replacing `x * 2` with `x << 1` is
(A) constant folding  (B) strength reduction  (C) dead code elimination  (D) copy propagation

**Q133.** Moving a loop-invariant computation out of a loop is
(A) loop unrolling  (B) code motion / hoisting  (C) strength reduction  (D) function inlining

**Q134.** Local optimisation is confined to
(A) a single basic block
(B) an entire procedure
(C) the whole program
(D) across procedure boundaries

**Q135.** Register allocation is commonly solved by
(A) graph colouring, spilling values that cannot be coloured
(B) sorting the variables
(C) hashing the identifiers
(D) backpatching

**Q136.** Liveness (live-variable) analysis is
(A) forward, union  (B) backward, union  (C) forward, intersection  (D) backward, intersection

**Q137.** Available-expressions analysis uses which meet operator, and enables what?
(A) union; dead code elimination
(B) intersection; common subexpression elimination
(C) union; register allocation
(D) intersection; constant propagation

**Q138.** Liveness analysis directly enables
(A) common subexpression elimination
(B) dead code elimination and register allocation
(C) constant folding only
(D) parsing

---

## Part Q — Paper-I (English, Reasoning, GK)

**Q139.** Choose the word most nearly similar in meaning to **CANDID**.
(A) Deceitful  (B) Frank and honest  (C) Hesitant  (D) Formal

**Q140.** Fill in the blank: *"She is well versed ___ software engineering."*
(A) with  (B) in  (C) at  (D) on

**Q141.** If the day before yesterday was Thursday, what will be the day after tomorrow?
(A) Sunday  (B) Monday  (C) Tuesday  (D) Wednesday

**Q142.** A sum of money doubles itself in 8 years at simple interest. In how many years will it become four times?
(A) 16 years  (B) 20 years  (C) 24 years  (D) 32 years

**Q143.** The Tripura Merger Agreement (Tripura joined the Indian Union on 15 October 1949) was signed on behalf of Tripura by
(A) Maharaja Bir Bikram Kishore Manikya
(B) Maharani Kanchan Prava Devi
(C) Maharaja Dhanya Manikya
(D) Maharaja Radha Kishore Manikya

**Q144.** Choose the antonym of **BENEVOLENT**.
(A) Generous  (B) Kind  (C) Malevolent  (D) Charitable

**Q145.** One word for "a person who can speak many languages":
(A) linguist  (B) polyglot  (C) bilingual  (D) orator

**Q146.** Find the next term of the series: 2, 6, 12, 20, 30, ___
(A) 36  (B) 40  (C) 42  (D) 46

**Q147.** The capital of Tripura is
(A) Aizawl  (B) Agartala  (C) Imphal  (D) Shillong

**Q148.** The idiom "to bury the hatchet" means
(A) to dig a hole  (B) to make peace  (C) to hide evidence  (D) to start a fight

**Q149.** Pointing to a photograph, a man said, "She is the daughter of my grandfather's only son." How is she related to him?
(A) Sister  (B) Mother  (C) Daughter  (D) Aunt

**Q150.** In a certain code, `FACE` is written as `GBDF`. How is `HEAD` written in that code?
(A) IFBE  (B) GDBC  (C) IFCE  (D) IECB

**Q151.** The official languages of Tripura are
(A) Hindi and English
(B) Bengali and Kokborok
(C) Assamese and Bengali
(D) Manipuri and Bengali

**Q152.** Complete the analogy: Doctor : Hospital :: Teacher : ___
(A) Book  (B) School  (C) Student  (D) Class

**Q153.** A train 150 m long crosses a pole in 15 seconds. Its speed in km/h is
(A) 24  (B) 36  (C) 40  (D) 54

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 32 | B | 63 | B | 94 | C | 125 | A |
| 2 | B | 33 | D | 64 | B | 95 | B | 126 | B |
| 3 | C | 34 | B | 65 | C | 96 | A | 127 | B |
| 4 | C | 35 | B | 66 | B | 97 | B | 128 | B |
| 5 | A | 36 | C | 67 | C | 98 | B | 129 | D |
| 6 | C | 37 | B | 68 | A | 99 | B | 130 | A |
| 7 | C | 38 | C | 69 | D | 100 | B | 131 | B |
| 8 | B | 39 | B | 70 | C | 101 | B | 132 | B |
| 9 | B | 40 | B | 71 | C | 102 | C | 133 | B |
| 10 | C | 41 | B | 72 | D | 103 | B | 134 | A |
| 11 | B | 42 | B | 73 | B | 104 | B | 135 | A |
| 12 | D | 43 | C | 74 | C | 105 | B | 136 | B |
| 13 | C | 44 | B | 75 | B | 106 | A | 137 | B |
| 14 | B | 45 | C | 76 | B | 107 | A | 138 | B |
| 15 | B | 46 | B | 77 | B | 108 | B | 139 | B |
| 16 | A | 47 | D | 78 | B | 109 | A | 140 | B |
| 17 | C | 48 | C | 79 | A | 110 | C | 141 | B |
| 18 | B | 49 | C | 80 | B | 111 | B | 142 | C |
| 19 | C | 50 | D | 81 | A | 112 | B | 143 | B |
| 20 | C | 51 | C | 82 | B | 113 | B | 144 | C |
| 21 | B | 52 | B | 83 | B | 114 | B | 145 | B |
| 22 | C | 53 | B | 84 | C | 115 | B | 146 | C |
| 23 | C | 54 | B | 85 | C | 116 | B | 147 | B |
| 24 | B | 55 | B | 86 | B | 117 | A | 148 | B |
| 25 | B | 56 | B | 87 | A | 118 | B | 149 | A |
| 26 | C | 57 | B | 88 | D | 119 | B | 150 | A |
| 27 | B | 58 | B | 89 | B | 120 | C | 151 | B |
| 28 | B | 59 | B | 90 | B | 121 | B | 152 | B |
| 29 | B | 60 | B | 91 | B | 122 | B | 153 | B |
| 30 | B | 61 | B | 92 | B | 123 | B | | |
| 31 | B | 62 | B | 93 | B | 124 | B | | |

---

# 📝 Detailed Solutions

**Q1. (B)** The Hawthorne effect is people behaving differently because they are being watched, which limits the reliability of direct observation.

**Q2. (B)** Questionnaires are cheap at scale for quantitative data from many respondents, but suffer low response rates and cannot probe or follow up like interviews.

**Q3. (C)** MIS produces predefined, routine summary and exception reports for middle management from TPS data. DSS, by contrast, supports ad-hoc analytical decisions.

**Q4. (C)** A what-if / model-based analytical query is a semi-structured, non-routine decision — the province of a DSS, not routine MIS reporting.

**Q5. (A)** JAD is a facilitated workshop that brings users and developers together to reach consensus quickly.

**Q6. (C)** A TPS records the operational day-to-day transactions (sales, bookings).

**Q7. (C)** Strategic dashboards, external data and drill-down for top management describe an EIS/ESS.

**Q8. (B)** "Response time under 2 s" describes how well the system performs (performance), so it is non-functional. If it described a feature it would be functional.

**Q9. (B)** Verification = "are we building the product right?" — conformance to the specification, via reviews/inspections, with no execution.

**Q10. (C)** Validation = "are we building the right product?" — it checks the user's actual need and requires executing the software.

**Q11. (B)** Resetting a password is a feature the system must do, hence a functional requirement.

**Q12. (D)** A good SRS is complete, consistent, unambiguous, verifiable, traceable, modifiable and correct. "Ambiguous" is the opposite of a desirable property.

**Q13. (C)** Operational feasibility asks whether the organisation and its users will actually use the system — the most commonly forgotten dimension.

**Q14. (B)** Cost–benefit, ROI, NPV and payback are economic (financial) feasibility tools.

**Q15. (B)** A 99.9% availability target is a quality/constraint, so it is a non-functional (availability) requirement.

**Q16. (A)** The level-0 DFD is the context diagram: the whole system as one process with external entities, and no data stores shown.

**Q17. (C)** A DFD is a data model and deliberately shows no control flow, decisions, loops or timing — those need a state transition diagram.

**Q18. (B)** Event and timing behaviour, which the DFD lacks, is captured by a state transition diagram.

**Q19. (C)** A process with inputs but no output is a black hole (miracle = output with no input; grey hole = output not derivable from input).

**Q20. (C)** Data cannot flow directly between two data stores (nor entity→entity, nor store→entity); every such flow must pass through a process.

**Q21. (B)** Balancing requires that a process's inputs/outputs at level n match those of its expansion at level n+1.

**Q22. (C)** A decision table with n binary conditions has 2ⁿ rules; 2⁴ = 16.

**Q23. (C)** The spiral model is risk-driven: every cycle passes through planning → risk analysis → engineering → evaluation.

**Q24. (B)** Waterfall delivers no working software until very late, and late requirement changes invalidate completed phases, making them very expensive.

**Q25. (B)** The V-model pairs a testing phase with every development phase (acceptance↔requirements, system↔design, etc.).

**Q26. (C)** Prototyping is best when requirements are unclear and users cannot articulate needs until they see something concrete.

**Q27. (B)** Agile is adaptive and best when requirements change frequently and the customer is available.

**Q28. (B)** The Scrum Master is a facilitator who removes impediments; they are not a manager and do not assign work.

**Q29. (B)** A sprint is a fixed-length iteration, typically 2–4 weeks.

**Q30. (B)** Scrum uses fixed-length sprints; Kanban uses continuous flow with WIP limits and no sprints.

**Q31. (B)** The retrospective inspects and improves the process; the review inspects the product increment.

**Q32. (B)** Function points are language-independent and measurable from the requirements stage; LOC is neither.

**Q33. (D)** The five FP component types are EI, EO, EQ, ILF, EIF. Cyclomatic complexity is a design metric, not an FP type.

**Q34. (B)** VAF = 0.65 + 0.01×35 = 1.00, so FP = UFP × VAF = 200 × 1.00 = 200.

**Q35. (B)** Organic = small team, familiar problem, flexible requirements (a = 2.4, b = 1.05).

**Q36. (C)** Organic effort is E = 2.4 × KLOC^1.05 person-months.

**Q37. (B)** E = 2.4 × 32^1.05 ≈ 2.4 × 37.4 ≈ 90 person-months.

**Q38. (C)** With b > 1, effort grows super-linearly with size — a diseconomy of scale (embedded has the largest exponent, 1.20).

**Q39. (B)** A Gantt chart shows durations, overlap and progress but not dependencies or the critical path; PERT/CPM networks show those.

**Q40. (B)** PERT is probabilistic (three-point estimates); CPM is deterministic (single estimates).

**Q41. (B)** t_e = (t_o + 4t_m + t_p)/6 = (4 + 24 + 14)/6 = 42/6 = 7.

**Q42. (B)** The critical path is the longest path through the network; it determines the minimum project duration. (Longest, not shortest.)

**Q43. (C)** The longest path B→E→D = 2+6+5 = 13 days is the critical path, so the project duration is 13 days.

**Q44. (B)** Risk exposure = probability × potential loss.

**Q45. (C)** DRE = E/(E+D) = 60/(60+15) = 60/75 = 0.80.

**Q46. (B)** The central design goal is high cohesion and low coupling — modules that are self-contained and minimally dependent.

**Q47. (D)** Cohesion best→worst: functional > sequential > communicational > procedural > temporal > logical > coincidental. Functional is best.

**Q48. (C)** Coincidental cohesion (no meaningful relationship) is the worst.

**Q49. (C)** Coupling best→worst: data < stamp < control < external < common < content. Data coupling is best.

**Q50. (D)** Content coupling (one module directly referencing/modifying another's internals) is the worst.

**Q51. (C)** V(G) = E − N + 2 = 12 − 9 + 2 = 5.

**Q52. (B)** V(G) = predicate nodes + 1 = 3 + 1 = 4.

**Q53. (B)** An inspection is formal, checklist-driven, moderator-led with recorded defects; a walkthrough is informal and author-led.

**Q54. (B)** BVA and equivalence class partitioning derive tests from the specification's ranges, so they are black-box techniques.

**Q55. (B)** Black-box testing can reveal missing functionality (something the spec required but was never coded); white-box has no code to inspect for it.

**Q56. (B)** The chain is error (human mistake) → fault/defect (flaw in the artefact) → failure (observable wrong behaviour).

**Q57. (B)** Coverage strength, weakest→strongest: statement < branch/decision < condition < path.

**Q58. (B)** 100% statement coverage does not imply 100% branch coverage: an `if` with no `else` can execute all statements with one test while never taking the false branch.

**Q59. (B)** Top-down integration needs stubs (dummy called modules).

**Q60. (B)** Bottom-up integration needs drivers (dummy calling modules).

**Q61. (B)** Alpha testing is at the developer's site with developers present; beta is at the customer's site.

**Q62. (B)** Stress testing pushes the system beyond its limits to find the breaking point; load testing checks behaviour at expected peak.

**Q63. (B)** Regression testing re-runs existing tests after a change to confirm nothing previously working has broken.

**Q64. (B)** Parallel changeover runs both systems at once, giving the lowest risk (the old system is a safety net) at the highest cost.

**Q65. (C)** Direct/plunge changeover switches off the old and on the new with no fallback — the highest risk, lowest cost.

**Q66. (B)** Porting to a new OS is adaptive maintenance (the environment changed).

**Q67. (C)** Adding a requested report is perfective maintenance (new/improved functionality users want).

**Q68. (A)** Fixing a reported crash is corrective maintenance (something was broken).

**Q69. (D)** Refactoring to ease future changes, when nothing is currently wrong, is preventive maintenance.

**Q70. (C)** Perfective maintenance is the largest share, ~50–65%.

**Q71. (C)** Maintenance consumes about 60–70% of a system's total lifecycle cost.

**Q72. (D)** CMM level 5 is Optimising (continuous process improvement). Do not stop at level 4.

**Q73. (B)** CMM level 1 (Initial) is ad-hoc and chaotic, with success depending on individual heroics.

**Q74. (C)** Level 4 (Managed/Quantitatively Managed) measures and quantitatively controls process and product.

**Q75. (B)** SQA is process-oriented and preventive; SQC is product-oriented and detective.

**Q76. (B)** Availability = MTTF/(MTTF+MTTR) = 950/1000 = 0.95 = 95%.

**Q77. (B)** MTBF = MTTF + MTTR.

**Q78. (B)** The first three phases are lexical → syntax → semantic analysis.

**Q79. (A)** Full order: lexical → syntax → semantic → intermediate code generation → optimisation → code generation.

**Q80. (B)** Lexical analysis outputs a token stream from the character stream.

**Q81. (A)** The front end is phases 1–4 (source-dependent, machine-independent); the back end is phases 5–6.

**Q82. (B)** Sharing one IR lets m front ends and n back ends combine as m + n components instead of m × n complete compilers.

**Q83. (B)** The symbol table manager and the error handler span all phases.

**Q84. (C)** An undeclared variable is a semantic error: it is spelled correctly (lexer OK) and grammatically placed (parser OK); only the symbol-table check in semantic analysis catches it.

**Q85. (C)** A type mismatch is a semantic error — syntactically valid but meaningless.

**Q86. (B)** A missing semicolon is a structural (syntax) error caught by the parser.

**Q87. (A)** `12abc` is a malformed token, caught by lexical analysis (maximal munch then error).

**Q88. (D)** Array index out of bounds is a run-time error.

**Q89. (B)** An interpreter translates and executes statement by statement; a compiler translates the whole program first.

**Q90. (B)** The linker combines object modules and resolves external references; the loader places the executable in memory.

**Q91. (B)** Lexical analysis is specified by regular expressions and implemented with finite automata (DFA).

**Q92. (B)** `int`, `x`, `=`, `10`, `;` = 5 tokens.

**Q93. (B)** The lexeme is the actual character sequence matched (e.g., `count`).

**Q94. (C)** The pattern is the rule describing the set of valid lexemes (e.g., `letter(letter|digit)*`).

**Q95. (B)** By maximal munch, the scanner takes the longest lexeme, so `>=` is a single token.

**Q96. (A)** Regular expressions suffice for tokens but cannot express nested/balanced constructs, which need a CFG and pushdown automaton — hence two phases.

**Q97. (B)** `lex`/`flex` generate a scanner from a regular-expression specification; `yacc`/`bison` and ANTLR are parser generators.

**Q98. (B)** With the ambiguous `E → E+E | E*E | id`, `id + id * id` has two parse trees (grouping as `id+(id*id)` or `(id+id)*id`).

**Q99. (B)** The dangling `else` matches the nearest unmatched `then` (yacc resolves the shift–reduce conflict by preferring shift).

**Q100. (B)** Left recursion must be removed for top-down/LL(1) parsing, else recursive descent loops forever.

**Q101. (B)** LR (bottom-up) parsers handle left recursion naturally; only top-down parsers require its removal.

**Q102. (C)** ε is never in a FOLLOW set (FOLLOW answers "which real token comes next?"); `$` and terminals can be.

**Q103. (B)** FOLLOW(start symbol) always contains `$` (end of input).

**Q104. (B)** FIRST(E) = FIRST(T) = FIRST(F) = { (, id }.

**Q105. (B)** FOLLOW(E) = { $ } (start symbol) plus `)` from `F → ( E )` = { ), $ }.

**Q106. (A)** FIRST(T') = { *, ε } (from `T' → *FT' | ε`).

**Q107. (A)** LL(1) = Left-to-right scan, Leftmost derivation, 1 lookahead token.

**Q108. (B)** Bottom-up (shift-reduce/LR) parsing produces a rightmost derivation in reverse.

**Q109. (A)** LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1) [= LR(1)].

**Q110. (C)** `yacc`/`bison` produce LALR(1) parsers — the best power/table-size trade-off.

**Q111. (B)** SLR(1) and LALR(1) have the same number of states (both built on the LR(0) state set); CLR(1) generally has more.

**Q112. (B)** LALR state merging can introduce reduce–reduce conflicts but never shift–reduce conflicts.

**Q113. (B)** An attribute computed from a node's children is synthesized (information flows upward).

**Q114. (B)** An attribute computed from the parent and/or siblings is inherited (flows downward/sideways).

**Q115. (B)** An S-attributed definition uses only synthesized attributes and is evaluable in a single bottom-up pass (works with LR/yacc).

**Q116. (B)** Every S-attributed definition is L-attributed (it has no inherited attributes, so the L-condition is trivially met), but not conversely.

**Q117. (A)** Each instruction has at most one operator using temporaries — this is three-address code.

**Q118. (B)** Quadruples (op, arg1, arg2, result) use explicit temporary names, so instructions can be reordered without breaking references.

**Q119. (B)** Plain triples reference a result by the triple's position/index, so moving an instruction breaks all references to it.

**Q120. (C)** Indirect triples add a pointer list giving order — compact like triples yet reorderable like quadruples.

**Q121. (B)** A DAG shares common subexpressions as one node, exposing redundancy for CSE.

**Q122. (B)** Parameters, locals and the return address live in an activation record on the stack, created on entry and destroyed on return.

**Q123. (B)** The symbol table is a compile-time structure; the activation record is a run-time structure on the stack.

**Q124. (B)** Static (lexical) scoping resolves a name to the enclosing block in the source text, at compile time.

**Q125. (A)** Static scoping prints 10: `f` is written at the top level, so its `x` binds to the global x; `g`'s local x is not lexically visible. (Dynamic scoping would print 20.)

**Q126. (B)** Call by value passes a copy; the caller's variable is unaffected.

**Q127. (B)** Call by name (text re-evaluated at each use) and call by value-result diverge when the argument is a subscripted variable such as `arr[a]` whose index `a` changes during the call.

**Q128. (B)** A basic block is a maximal straight-line sequence with one entry (first instruction) and one exit (last).

**Q129. (D)** Leaders are: the first instruction, any jump target, and any instruction immediately following a jump. An ordinary arithmetic instruction is not a leader.

**Q130. (A)** Evaluating a constant expression (`4 * 3` → `12`) at compile time is constant folding — no variables involved.

**Q131. (B)** Substituting a variable's known constant value (`a = 5` ⇒ `a + 2` → `5 + 2`) is constant propagation.

**Q132. (B)** Replacing an expensive operation with a cheaper one (`x * 2` → `x << 1`) is strength reduction.

**Q133. (B)** Moving a loop-invariant computation out of the loop is code motion / loop-invariant code hoisting.

**Q134. (A)** Local optimisation operates within a single basic block — exactly what the syllabus names.

**Q135. (A)** Register allocation is solved by graph colouring on the interference graph; values that cannot be coloured are spilled to memory.

**Q136. (B)** Liveness analysis is backward (it asks about future uses) and uses union (a "may" property).

**Q137. (B)** Available expressions uses intersection ("must" hold on every path) and enables common subexpression elimination.

**Q138. (B)** Liveness enables dead code elimination (dead value after assignment) and register allocation (values never simultaneously live can share a register).

**Q139. (B)** *Candid* means straightforward, frank and honest.

**Q140. (B)** The fixed collocation is *well versed **in*** something.

**Q141. (B)** Day before yesterday = Thursday ⇒ yesterday = Friday ⇒ today = Saturday ⇒ tomorrow = Sunday ⇒ day after tomorrow = Monday.

**Q142. (C)** Under simple interest the yearly interest is constant. Doubling means interest = principal after 8 years; four times needs interest = 3 × principal → 3 × 8 = 24 years.

**Q143. (B)** With Maharaja Bir Bikram having died in 1947 leaving a minor heir, Maharani Kanchan Prava Devi as Regent signed the Tripura Merger Agreement; Tripura joined on 15 October 1949.

**Q144. (C)** *Malevolent* (wishing harm) is the antonym of *benevolent* (wishing good).

**Q145. (B)** A *polyglot* speaks many languages.

**Q146. (C)** The series is n(n+1): 2, 6, 12, 20, 30, so the next is 6×7 = 42.

**Q147. (B)** The capital of Tripura is Agartala.

**Q148. (B)** "To bury the hatchet" means to make peace / end a quarrel.

**Q149. (A)** "My grandfather's only son" is the speaker's father; his daughter is the speaker's sister.

**Q150. (A)** Each letter shifts +1: H→I, E→F, A→B, D→E, giving IFBE.

**Q151. (B)** The official languages of Tripura are Bengali and Kokborok.

**Q152. (B)** A doctor works in a hospital as a teacher works in a school.

**Q153. (B)** Speed = 150/15 = 10 m/s = 10 × 18/5 = 36 km/h.
