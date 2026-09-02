# Week 11 Mock Test — Information Systems & Software Engineering + Compiler Design

**Syllabus §10 and §7** · 25 questions · **30 minutes** · +1 / −0.33

---

## Part A — Information Systems & Software Engineering (Q1–Q11)

**Q1.** In a Data Flow Diagram, the level-0 DFD that shows the entire system as a single process with its external entities is called the
(A) context diagram  (B) process specification  (C) data dictionary  (D) entity–relationship diagram

**Q2.** Which software process model is explicitly **risk-driven** and organises development as a series of iterative cycles?
(A) Waterfall  (B) Spiral  (C) Prototyping  (D) V-model

**Q3.** The principal drawback of the classical waterfall model is that
(A) it produces no documentation
(B) working software is available only very late, and requirements cannot easily be revised
(C) it cannot be used for large projects
(D) it requires too many programmers

**Q4.** "Response time must be under 2 seconds" is an example of a
(A) functional requirement  (B) non-functional requirement  (C) business rule  (D) user story

**Q5.** In basic COCOMO, a project classified as **organic** is typically
(A) large and highly complex with tight constraints
(B) relatively small, with a familiar problem and an experienced team
(C) embedded within rigid hardware constraints
(D) impossible to estimate

**Q6.** A program's control flow graph has 12 edges and 9 nodes. Its cyclomatic complexity is
(A) 3  (B) 4  (C) 5  (D) 21

**Q7.** Which type of **cohesion** is considered the best (strongest)?
(A) Coincidental  (B) Logical  (C) Temporal  (D) Functional

**Q8.** Which type of **coupling** is considered the worst (most undesirable)?
(A) Data coupling  (B) Stamp coupling  (C) Control coupling  (D) Content coupling

**Q9.** Boundary value analysis and equivalence class partitioning are techniques of
(A) white-box testing  (B) black-box testing  (C) unit testing only  (D) regression testing

**Q10.** In **top-down** integration testing, the modules that temporarily replace not-yet-written lower-level modules are called
(A) drivers  (B) stubs  (C) mocks only  (D) harnesses

**Q11.** Modifying software to work with a new operating system or hardware platform is classified as which type of maintenance?
(A) Corrective  (B) Adaptive  (C) Perfective  (D) Preventive

---

## Part B — Compiler Design (Q12–Q20)

**Q12.** The correct order of the first three phases of a compiler is
(A) syntax analysis → lexical analysis → semantic analysis
(B) lexical analysis → syntax analysis → semantic analysis
(C) semantic analysis → lexical analysis → syntax analysis
(D) lexical analysis → semantic analysis → syntax analysis

**Q13.** The lexical analyser is best specified and implemented using
(A) context-free grammars and pushdown automata
(B) regular expressions and finite automata
(C) attribute grammars
(D) Turing machines

**Q14.** Which of the following is produced by the syntax analysis phase?
(A) A stream of tokens  (B) A parse tree  (C) Machine code  (D) A symbol table only

**Q15.** Before a grammar can be used with a top-down (recursive descent / LL(1)) parser, it must have
(A) left recursion eliminated
(B) right recursion eliminated
(C) all terminals removed
(D) no epsilon productions at all

**Q16.** The correct ordering of parsing power, from weakest to strongest, is
(A) LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1)
(B) CLR(1) ⊂ LALR(1) ⊂ SLR(1) ⊂ LR(0)
(C) SLR(1) ⊂ LR(0) ⊂ CLR(1) ⊂ LALR(1)
(D) LALR(1) ⊂ CLR(1) ⊂ LR(0) ⊂ SLR(1)

**Q17.** In a syntax-directed definition, an attribute whose value at a node is computed from the attributes of its **children** is called
(A) an inherited attribute  (B) a synthesized attribute  (C) a global attribute  (D) a static attribute

**Q18.** `t1 = b * c` followed by `t2 = a + t1` is an example of
(A) three-address code  (B) postfix notation  (C) machine code  (D) a parse tree

**Q19.** Information about a function's parameters, local variables and return address is stored at run time in
(A) the symbol table  (B) an activation record on the stack  (C) the code segment  (D) a register file

**Q20.** Replacing the computation `x = 4 * 3` with `x = 12` at compile time is called
(A) constant folding  (B) dead code elimination  (C) strength reduction  (D) loop unrolling

---

## Part C — Paper-I (Q21–Q25)

**Q21.** Choose the word most nearly similar in meaning to **CANDID**.
(A) Deceitful  (B) Frank and honest  (C) Hesitant  (D) Formal

**Q22.** Fill in the blank: *"She is well versed ___ software engineering."*
(A) with  (B) in  (C) at  (D) on

**Q23.** If the day before yesterday was Thursday, what will be the day after tomorrow?
(A) Sunday  (B) Monday  (C) Tuesday  (D) Wednesday

**Q24.** A sum of money doubles itself in 8 years at simple interest. In how many years will it become four times?
(A) 16 years  (B) 20 years  (C) 24 years  (D) 32 years

**Q25.** Tripura merged with the Indian Union on 15 October 1949. The merger agreement was signed on behalf of Tripura by
(A) Maharaja Bir Bikram Kishore Manikya
(B) Maharani Kanchan Prava Devi
(C) Maharaja Dhanya Manikya
(D) Maharaja Radha Kishore Manikya

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | A | 6 | C | 11 | B | 16 | A | 21 | B |
| 2 | B | 7 | D | 12 | B | 17 | B | 22 | B |
| 3 | B | 8 | D | 13 | B | 18 | A | 23 | B |
| 4 | B | 9 | B | 14 | B | 19 | B | 24 | C |
| 5 | B | 10 | B | 15 | A | 20 | A | 25 | B |

---

**Q1 — (A).** The **context diagram** (level-0 DFD) shows one process representing the whole system, its external entities and the data flows between them. Lower levels decompose it, and each level must be *balanced* with its parent.

**Q2 — (B).** The **spiral model** (Boehm) makes risk analysis an explicit quadrant of every cycle, and is favoured for large, high-risk projects.

**Q3 — (B).** Waterfall's sequential phases mean no executable product until late, and its rigidity makes late requirement changes expensive. It is still appropriate when requirements are genuinely stable and well understood.

**Q4 — (B).** Non-functional requirements specify *how well* the system performs (performance, reliability, security, usability), as opposed to *what* it does.

**Q5 — (B).** Organic = small team, familiar application, flexible requirements (E = 2.4 × KLOC^1.05). Semi-detached is intermediate; **embedded** is large with tight hardware/regulatory constraints and the highest exponent.

**Q6 — (C).** V(G) = E − N + 2 = 12 − 9 + 2 = **5**. Equivalently, V(G) = number of predicate nodes + 1, or the number of bounded regions + 1. It gives a lower bound on the number of test cases needed for branch coverage.

**Q7 — (D).** Cohesion, best to worst: **functional** > sequential > communicational > procedural > temporal > logical > coincidental. High cohesion is desirable.

**Q8 — (D).** Coupling, best to worst: **data** < stamp < control < external < common < **content**. Content coupling (one module directly modifying another's internals) is the worst. Good design = high cohesion, low coupling.

**Q9 — (B).** Both derive test cases from the *specification* without looking at the code — black-box. White-box techniques (statement, branch, path coverage) use the internal structure.

**Q10 — (B).** Top-down integration needs **stubs** (dummy called modules). Bottom-up integration needs **drivers** (dummy calling modules). Mixing these two up is the most common error in this topic.

**Q11 — (B).** **Adaptive** maintenance responds to changes in the environment (OS, hardware, regulations). Corrective fixes defects, perfective adds enhancements (and is usually the largest share of effort), preventive improves future maintainability.

**Q12 — (B).** Lexical → syntax → semantic → intermediate code generation → code optimisation → code generation. The first three form the analysis (front-end) phase.

**Q13 — (B).** Tokens are describable by regular expressions, which map directly to finite automata — hence tools like `lex`/`flex`. Syntax analysis needs the greater power of CFGs and pushdown automata.

**Q14 — (B).** The parser consumes the token stream and produces a **parse tree** (or syntax tree), verifying that the input conforms to the grammar.

**Q15 — (A).** Left recursion (A → Aα) makes a recursive-descent parser loop forever. It must be eliminated, and the grammar left-factored, before LL(1) parsing. Bottom-up LR parsers actually *prefer* left recursion.

**Q16 — (A).** **LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1)**. CLR(1) is the most powerful but has the largest tables; LALR(1) merges CLR states with identical cores, giving smaller tables at the cost of possible reduce–reduce conflicts — which is why `yacc`/`bison` use it.

**Q17 — (B).** **Synthesized** attributes flow *up* from children; **inherited** attributes flow *down* from the parent or siblings. A grammar using only synthesized attributes is S-attributed and can be evaluated bottom-up in a single pass.

**Q18 — (A).** Three-address code has at most one operator and up to three operands per instruction, using temporaries — the standard intermediate representation, implementable as quadruples, triples or indirect triples.

**Q19 — (B).** The **activation record** (stack frame) holds parameters, local variables, the return address, the saved frame pointer and temporaries. It is created at call time and destroyed on return — which is why recursion works. The *symbol table* is a compile-time structure.

**Q20 — (A).** **Constant folding** evaluates constant expressions at compile time. Constant *propagation* substitutes a known constant value for a variable; strength reduction replaces an expensive operation with a cheaper one (e.g. `x*2` → `x<<1`).

**Q21 — (B).** *Candid* = straightforward, **frank and honest**, especially in a way that might be uncomfortable.

**Q22 — (B).** The fixed collocation is *well versed **in*** something.

**Q23 — (B).** Day before yesterday = Thursday ⇒ yesterday = Friday ⇒ today = Saturday ⇒ tomorrow = Sunday ⇒ **day after tomorrow = Monday**. Chain the days one step at a time; off-by-one slips here are the most common way to lose an easy mark.

**Q24 — (C).** Under simple interest the interest earned each year is constant. Doubling means the interest equals the principal after 8 years. To become four times, the interest must equal 3 × principal → 3 × 8 = **24 years**.

**Q25 — (B).** Maharaja Bir Bikram Kishore Manikya died in 1947, leaving a minor heir. **Maharani Kanchan Prava Devi**, as Regent, signed the Tripura Merger Agreement, and Tripura joined the Indian Union on **15 October 1949**.

---

## Score

| | |
|---|---|
| Part A (IS & Software Engineering) | ___ / 11 |
| Part B (Compiler Design) | ___ / 9 |
| Part C (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** Software Engineering has **337 questions** waiting in `02_State_PSC_PYQs/Subject_wise/Paper2_S10_Information_Systems_and_Software_Engineering/` and **zero** GATE coverage — it is the single largest untapped block in Paper-II. If you scored below 8/11 in Part A, that folder is your highest-return next session.

**Must-memorise for SE:** cohesion and coupling orderings · maintenance types · black-box vs white-box techniques · stubs vs drivers · COCOMO modes · CMM levels 1–5 (Initial, Repeatable, Defined, Managed, Optimising) · cyclomatic complexity formula.

**For Compiler Design:** the phase order, the LR power hierarchy, FIRST/FOLLOW construction, and the named optimisations. Drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S07_Compiler_Design/` (242 questions) — but remember Theory of Computation is **not** in your syllabus, so skip automata-heavy questions.
