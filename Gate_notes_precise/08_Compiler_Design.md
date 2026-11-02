# 08 · Compiler Design — Precise Notes
> **TPSC ATO (IT) Paper-II §7** · ~6 marks (estimate) · Syllabus: *"Compiler Design — lexical analysis, parsing, syntax-directed translation; runtime environments; intermediate code generation; local optimization; data flow analyses: constant propagation, liveness analysis, common subexpression elimination"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson, Made Easy CD Notes, GATE Applied Course, Made Easy CS, Ace Academy. Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/08_Compiler_Design/` — open them for diagrams.
> Short names: Pearson = `1` · Sanchit = `2` · Ace = `3` · AppliedCourse = `4` · ekxam = `5` · MadeEasy-CS = `6` · MadeEasy-CD = `7` (PDF page numbers).

## Which notes are worth your time

| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| `1.CD.pdf` | Pearson (GATE guide) | Typed text | 71 | 4 | Widest coverage: only source for runtime storage, parameter passing, peephole, reaching-definition equations; chapter PYQs · two-column text, no liveness equations, a few slips |
| `2.CD_Sanchit_Sir_Notes.pdf` | Sanchit Sir (Knowledge Gate) | Typed text | 115 | 4 | Crisp definitions + large year-tagged GATE/NET bank · ~20 pp of ToC; **no** runtime environments or data-flow; some wrong keys (fixed below) |
| `3.Ace_Academy_Compiler_Design_Class_Notes.pdf` | Ace Academy | Handwritten, clear | 74 | 2.5 | LL(1)/LR table walk-throughs, SDT trees · mirrors Sanchit; ICG/optimisation ~10 pp; no runtime/DFA |
| `4.COMPILER_DESIGN_-_GATEApplied_course_NOTES.pdf` | GATE Applied Course | Handwritten colour, very clear | 70 | 3 | Item-set DFAs, dangling-else grammar, precedence table, S/L-attributed marker trick · stops at basic 3AC |
| `5.Compiler_Design.pdf` | Unknown (ekxam.com) | Phone photos | 41 | 1.5 | Lecture recap of Knowledge-Gate material · faded, fingers in frame, adds nothing |
| `6.Compiler_Design-CS.pdf` | Made Easy (2010) | Handwritten scan | 84 | 2 | Only scan with a runtime page (AR fields, static/stack/heap) · first quarter is ToC; cramped; garbled indirect triples |
| `7.CD_Notes.pdf` | Made Easy (2020) | Handwritten, clear | 145 | 3.5 | Dragon-book based; lexical errors; many solved GATE PYQs on parsing, SDT, SSA, DAG · no runtime, optimisation or data flow |

**If you open only one PDF besides these notes**, open **Pearson (`1.CD.pdf`) pp. 35–64** — ICG, runtime storage, parameter passing, optimisation and data flow, exactly where Sanchit is silent. For parsing/SDT drill, use Made Easy CD Notes (`7`).

## Topic map

| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | Compiler basics | ⭐⭐⭐ | match concept → phase; which phase catches an error; linker vs loader |
| 2 | Lexical analysis | ⭐⭐⭐ | count tokens; longest-match trace; is it a lexical error? |
| 3 | Grammar background | ⭐⭐ | ambiguous?; remove left recursion; precedence from grammar |
| 4 | FIRST/FOLLOW, LL(1) | ⭐⭐⭐ | FOLLOW(X); table entry; is G LL(1)? |
| 5 | Bottom-up / LR parsing | ⭐⭐⭐ | handle; SLR/LALR/CLR membership; state counts; conflicts |
| 6 | Syntax-directed translation | ⭐⭐⭐ | output printed for an input; S- vs L-attributed |
| 7 | Runtime environments | ⭐⭐ | AR fields; recursion vs allocation; scoping/parameter output |
| 8 | Intermediate code | ⭐⭐⭐ | DAG nodes; triples/quadruples; SSA count |
| 9 | Local optimisation | ⭐⭐⭐ | name the optimisation; blocks and CFG edges |
| 10 | Data-flow analysis | ⭐⭐ | direction and meet; analysis ↔ optimisation; live variables |

## 1. Compiler Basics

### 1.1 Language-processing system
- Preprocessor (macros, `#include`) → pure HLL → compiler → assembly → assembler → **relocatable** object code → linker → loader → **absolute** code in memory [Src: Sanchit p.2].
- ⭐ **Linker**: merges object modules + libraries, **resolves external references**, relocates (NET-Aug-2016). **Loader**: allocation, linking, relocation, loading [Src: Ace p.2].
- Two-pass assembler: pass 1 builds the symbol table (forward references), pass 2 emits code. Cross-compiler: runs on A, targets B.

| | Compiler | Interpreter |
|---|---|---|
| Unit | whole program | statement by statement |
| Object code | yes | no |
| Speed / memory | faster / more | slower / less |
| Errors | all after compiling | stops at first |

### 1.2 Phases

| Phase | Input → output | Key point |
|---|---|---|
| Lexical | characters → tokens | RE/DFA; strips comments |
| Syntax | tokens → parse tree | CFG/PDA |
| Semantic | tree → annotated tree | type checking, declarations |
| ICG | tree → 3AC | machine-independent |
| Optimisation | IR → better IR | optional |
| Code generation | IR → target code | register allocation = graph colouring |

- ⭐ Front end = lexical … ICG; back end = optimisation + code gen. **Retargeting**: new back end, same front end (m + n translators, not m × n). Symbol table and error handler serve all phases.
- 🎯 **How it's asked:** match (GATE-2009/2015/2016/2017): RE, DFA minimisation → lexical; PDA, LMD, production tree → parsing; type checking → semantic; activation records → runtime; data-flow analysis → optimisation; post-order traversal → expression evaluation.
- ⚠ Type checking comes **after** parsing (GATE-2018); keywords are found by the **lexer** (GATE-2011); dynamic memory allocation is **not** a compile-time task (GATE-2014).
- Pass = one full read of source/IR (may hold several phases). One-pass: faster, needs declare-before-use; multi-pass: better optimisation. ⚠ Notes disagree on which uses less memory — rely only on "one-pass is faster".

### 1.3 Symbol table and errors
- Stores name, type, scope, size, offset (+ array dimensions, parameter types) [Src: AppliedCourse p.8]; ops insert/lookup/modify/delete; ⭐ hash table most common (O(1) average).
- Parser recovery: ⭐ panic mode (skip to `;` or `}`), phrase level, error productions, global correction.

| Error | Phase |
|---|---|
| `@`/`$` in C, unterminated comment or string | lexical |
| missing `;`, unbalanced parentheses | syntax |
| undeclared variable, type mismatch | semantic |
| divide by zero, index out of bounds | run time |

## 2. Lexical Analysis

### 2.1 Tokens, lexemes, patterns
- **Lexeme** = actual text (`count`); **token** = its class ⟨id, symbol-table pointer⟩; **pattern** = the RE describing it [Src: MadeEasy-CD p.10].
- ⭐ Specified by regular expressions, implemented by a DFA; finite automata suffice even for Java (GATE-2011). The scanner also strips whitespace/comments and tracks line numbers.

### 2.2 Token counting
📌 keyword, identifier, constant, operator, each of `( ) { } [ ] , ;` = 1 · whole string literal = 1 · `++ += == <= -> &&` = 1 · comments and blanks = 0.

🔢
- `printf("i = %d, &i = %x", i, &i);` → `printf ( "…" , i , & i ) ;` = **10** (GATE-2000).
- `x = x * (a + b) - 5;` → **12** (NET-Dec-2014).
- `for (int i = 1; i <= 10; i++)` → **14**. ⚠ Pearson p.4 lists these 14 tokens but prints "13".

### 2.3 Longest match and LEX
- ⭐ **Maximal munch**: longest matching prefix wins; ties go to the earlier rule (keywords before identifiers).
- 🔢 GATE-2018: T1 = a?(b|c)\*a, T2 = b?(a|c)\*b, T3 = c?(b|a)\*c on `bbaacabc` ⇒ `bbaac` then `abc` ⇒ **T3 T3**.
- Lookahead: `+`, `<`, `int` need the next character (`+=`, `<=`, `integer`). ⚠ Fortran ignores blanks, so `DO 5 I = 1.25` is `DO5I = 1.25` (3 tokens); Pearson p.4's "5 tokens, keyword DO" is wrong.
- **LEX**: `x.l` (definitions `%%` pattern {action} `%%` code) → `lex.yy.c` → compiled scanner; `yylex()`, `yytext`, `yyleng`; builds RE → NFA → DFA.

### 2.4 Lexical errors
- Only when **no pattern matches**: illegal character, unterminated comment/string, malformed literal, over-long identifier [Src: MadeEasy-CD p.12–13].
- ⚠ Not lexical: `fi (a == b)` (`fi` is a valid identifier), missing `;`. MadeEasy-CD p.13 calls `salary = 10,000;` a lexical error — the scanner emits `10` `,` `000`; the parser rejects it.
- Recovery: panic mode, delete, insert, replace, transpose a character.

## 3. Grammar Background for Parsing

### 3.1 Derivations and ambiguity
- ⭐ Top-down parsers trace the **LMD** (GATE-2000); bottom-up trace the **RMD in reverse**.
- One parse tree ⇔ one LMD ⇔ one RMD. **Ambiguous** = some string has ≥ 2 parse trees.
- ⚠ "Unambiguous grammar has the same LMD and RMD" is **false** (GATE-2001, NET-Aug-2016).
- Classic ambiguous: `E → E+E | E*E | id`, `S → SS | a`, `S → aSbS | bSaS | ε`, `A → AA | (A) | ε` (GATE-2005), dangling else `S → iEtS | iEtSeS | a`.
- ⭐ A useful non-terminal both left- and right-recursive ⇒ ambiguous. Ambiguous ⇒ never LL(k)/LR(k) (GATE-2001). Inherently ambiguous CFLs exist (GATE-2004).
- Precedence by layering `E → E+T | T, T → T*F | F, F → (E) | id`: deeper = higher precedence; left recursion = left associative.
- 🎯 GATE-2014 `S → T*P, T → U | T*U, P → Q+P | Q` ⇒ `+` right-, `*` left-associative. GATE-2016 (+ high/left, − mid/right, × low): 2 − 5 + 1 − 7 × 3 = **9**.
- Dangling else: else binds to the nearest unmatched then (matched/open grammar) [Src: AppliedCourse p.25].

### 3.2 Left recursion and left factoring
📌 A → Aα₁ | … | Aαₘ | β₁ | … | βₙ ⇒ A → β₁A′ | … | βₙA′ ; A′ → α₁A′ | … | αₘA′ | ε
📌 A → αβ₁ | αβ₂ ⇒ A → αA′ ; A′ → β₁ | β₂
- `E → E+T | T` ⇒ `E → TE′, E′ → +TE′ | ε` (GATE-2017 asks the equivalent grammar). Indirect recursion: substitute first.
- Left recursion loops recursive descent; LR parsers are fine with it.
- `S → iEtS | iEtSeS | a` ⇒ `S → iEtSS′ | a, S′ → eS | ε` — still ambiguous, not LL(1) (GATE-2007).
- ⚠ Removing left recursion **and** factoring does not guarantee LL(1) (GATE-2003, NET-Dec-2012).

## 4. Top-Down Parsing — FIRST, FOLLOW, LL(1)

### 4.1 Recursive descent
- One procedure per non-terminal; brute force backtracks (exponential; `S → cAd, A → ab | a` on `cad`) [Src: Sanchit p.40]. Predictive (no backtracking) = LL(1); table-driven = explicit stack.
- ⭐ Recursive descent is top-down; operator-precedence, LR, LALR are bottom-up (GATE-2007).

### 4.2 FIRST and FOLLOW
📌 **FIRST(α)**: terminals beginning strings from α (+ ε if α ⇒* ε). For X → Y₁…Yₖ add FIRST(Y₁) − {ε}; if Y₁ ⇒* ε add FIRST(Y₂) − {ε}, …; ε only if all Yᵢ ⇒* ε.
📌 **FOLLOW(A)**: (1) $ ∈ FOLLOW(S); (2) B → αAβ ⇒ FIRST(β) − {ε} ⊆ FOLLOW(A); (3) B → αA, or β ⇒* ε ⇒ FOLLOW(B) ⊆ FOLLOW(A). ⭐ ε is never in FOLLOW.

🔢 `E → TE′, E′ → +TE′ | ε, T → FT′, T′ → *FT′ | ε, F → (E) | id`

| NT | FIRST | FOLLOW |
|---|---|---|
| E | ( id | ) $ |
| E′ | + ε | ) $ |
| T | ( id | + ) $ |
| T′ | * ε | + ) $ |
| F | ( id | * + ) $ |

- 🎯 GATE-2017 `P → xQRS, Q → yz | z, R → w | ε, S → y` ⇒ FOLLOW(Q) = {w, y}. GATE-2019 `S → Aa, A → BD, B → b | ε, D → d | ε` ⇒ FOLLOW(B) = {d, a}.

### 4.3 LL(1)
- L = left-to-right, L = leftmost derivation, 1 lookahead; table rows = NTs, columns = terminals + $ [Src: Sanchit p.52–56].
- 📌 **Fill:** A → α goes to M[A, a] for a ∈ FIRST(α); if ε ∈ FIRST(α), also to M[A, b] for b ∈ FOLLOW(A).
- 📌 **LL(1) ⇔ no multiple entries ⇔** for each A → α | β: FIRST(α) ∩ FIRST(β) = ∅; at most one ⇒* ε; if β ⇒* ε then FIRST(α) ∩ FOLLOW(A) = ∅.
- ⭐ Left-recursive, ambiguous or not left-factored ⇒ instantly not LL(1).
- 🔢 `S → aSbS | bSaS | ε`: FOLLOW(S) = {a, b, $} ⇒ M[S, a] = {S → aSbS, S → ε} ⇒ **not LL(1)**.
- 🔢 `S → AaAb | BbBa, A → ε, B → ε`: FIRSTs {a}, {b} disjoint ⇒ **LL(1)** (but not SLR(1), §5.3).
- 🎯 GATE-2006 `S → FR, R → *S | ε, F → id` ⇒ M[S, id] = S → FR, M[R, $] = R → ε. GATE-2010 `S → aSa | bS | c` is LL(1) and LR(1). GATE-2015 `S → F | H, F → p | c, H → d | c` is ambiguous ⇒ neither.

## 5. Bottom-Up Parsing

### 5.1 Shift-reduce, handles, operator precedence
- Actions: shift, reduce, accept, error; conflicts S/R and R/R.
- ⭐ **Handle** = production to reduce next **plus its position** (GATE-2008). **Viable prefix** = stack-able prefix of a right-sentential form; the stack always holds one (GATE-2015); they form a regular set (LR(0) DFA).
- 🎯 GATE-2005 `E → E+n | E×n | n` on `n+n×n` ⇒ handles n, E+n, E×n. GATE-2013: max reductions for n tokens (no ε/single-symbol rules) = **n − 1**.
- ⚠ Sanchit p.39/62 give O(n⁴)/O(n³) for parsers — LL(1)/LR parse in **O(n)**; O(n³) is general CFG parsing (CYK).
- **Operator grammar**: no ε-production, no two adjacent NTs (GATE-2004). Relations ⋖ (shift), ≐, ⋗ (reduce) between terminals [Src: AppliedCourse p.58]; handles some ambiguous grammars.

### 5.2 LR items and tables
- 📌 LR(k): Left-to-right, Rightmost derivation in reverse, k lookahead. Augment S′ → S. A → XYZ has 4 LR(0) items; A → ε has 1.
- closure(I): A → α·Bβ adds all B → ·γ. goto(I, X) = closure{A → αX·β} [Src: Sanchit p.66–69; AppliedCourse p.45].

| Parser | Items | Reduce A → α· entered under |
|---|---|---|
| LR(0) | LR(0) | whole row |
| SLR(1) | LR(0) | FOLLOW(A) |
| CLR(1) | LR(0) item + lookahead | its lookahead |
| LALR(1) | CLR sets with equal cores merged | union of lookaheads |

- LR(1) closure: [A → α·Bβ, a] adds [B → ·γ, b] for b ∈ FIRST(βa). ⚠ Ace p.40 puts "accept" across the whole I₁ row — only under $.
- 📌 **#states: LR(0) = SLR = LALR ≤ CLR** (GATE-2003, 2005): `S → (S) | a` 6/6/10; `S → AA, A → aA | b` 7/7/10 [Src: AppliedCourse p.52; MadeEasy-CD p.115].
- 🎯 GATE-2019 `S → (L) | id, L → L,S | S`: GOTO(I₀, `(`) has **5** items.

### 5.3 Conflicts and hierarchy
- S/R: complete A → α· with shift on a, where a ∈ FOLLOW(A) (SLR) or a = lookahead (CLR). R/R: two complete items sharing a FOLLOW symbol/lookahead.
- ⭐ LALR merging creates only **R/R** conflicts; LALR has S/R iff CLR has (GATE-2008). ⚠ Sanchit p.80: "no RR in CLR ⇒ no SR in LALR" — correct: no **S/R** in CLR ⇒ no S/R in LALR.
- 📌 LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ CLR(1); LL(1) ⊂ LR(1) but incomparable with SLR/LALR. ⭐ SLR easiest, CLR most powerful (GATE-2015, 2017).

| Grammar | Verdict |
|---|---|
| `E → T+E \| T, T → id` | SLR(1), not LR(0) |
| `S → L=R \| R, L → *R \| id, R → L` | LALR(1), not SLR(1) [Src: Pearson p.16] |
| `S → Aa \| bAc \| dc \| bda, A → d` | LALR(1), not SLR(1) |
| `S → Aa \| bAc \| Bc \| bBa, A → d, B → d` | CLR(1), not LALR(1) |
| `S → AaAb \| BbBa, A → ε, B → ε` | LL(1), LALR(1), not SLR(1) |

- 🎯 GATE-2013: merging LR(1) sets with equal cores (lookaheads c/d vs $) — "cannot merge" / "creates conflict" claims all false.
- ⭐ YACC = **Yet Another Compiler-Compiler** (⚠ Pearson p.16: "Yet another Compiler") → **LALR(1)** parser `y.tab.c`; S/R resolved as shift, R/R by earlier rule; `%left %right` set associativity.

## 6. Syntax-Directed Translation

### 6.1 Attributes
- **SDD** = grammar + attributes + rules (no order); **SDT scheme** = actions `{…}` embedded in RHS (order fixed) [Src: Pearson p.26–28].
- ⭐ **Synthesized** ← children; **inherited** ← parent/siblings; terminals: synthesized only.
- Annotated parse tree shows attribute values; evaluation order = topological sort of the dependency graph (cycle ⇒ none).

| | S-attributed | L-attributed |
|---|---|---|
| Attributes | synthesized only | + inherited from parent or **left** siblings |
| Actions | end of RHS | anywhere |
| Evaluated | post-order, during LR parse | depth-first left-to-right (LL) |

- ⭐ S-attributed ⊂ L-attributed [Src: AppliedCourse p.66]. Bottom-up evaluation of inherited attributes needs L-attributed (GATE-2003), via markers M → ε.
- Classic inherited: `D → T L {L.in = T.type}; L → L₁ , id {L₁.in = L.in; addtype(id, L.in)}` (GATE-2019). Using a right sibling breaks L-attribution.

### 6.2 Tracing
📌 Parse with **this** grammar's precedence; fire each action when the depth-first walk reaches it (end-of-RHS = at reduction).
- 🔢 GATE-2003 `E → TR, R → +T {print('+')} R | ε, T → num {print}`: `9+5+2` ⇒ `9 5 + 2 +`.
- 🔢 GATE-2006 `S → ER, R → *E {print('*')} R | ε, E → F+E {print('+')} | F, F → (S) | id {print}`: `2*3+4` ⇒ `2 3 4 + *`.
- 🔢 GATE-2016 `S → aA {1} | a {2}, A → Sb {3}` bottom-up on `aab` ⇒ `2 3 1`.
- 🔢 GATE-2004 `#` = × (E-level), `&` = + (T-level): 2#3&5#6&4 = 2 × 8 × 10 = **160**.
- 🔢 GATE-2003 `E → id {E.place = id.place}` emits nothing ⇒ `X := Y + Z` gives `t1 = Y + Z; X = t1`. ⚠ Sanchit p.94 keys (C); correct is (B).

## 7. Runtime Environments

### 7.1 Storage allocation
Layout: code | static data | heap → … ← stack [Src: Pearson p.45].

| | Static | Stack | Heap |
|---|---|---|---|
| Bound | compile time | per call | on request |
| Freed | never | at return (LIFO) | any order / GC |
| Recursion | ✗ | ✓ | ✓ |
| Example | FORTRAN 77, C `static` | locals | `malloc`, `new` |

- 🎯 GATE-2014: true — static allocation of all data makes recursion impossible; dynamic allocation of ARs is essential. False — GC, or "both heap and stack", is essential.
- Heap issues: fragmentation, dangling pointers, leaks; reference counting fails on cycles.

### 7.2 Activation record
- Activation tree: pre-order = calls, post-order = returns; control stack holds live ARs.
- 📌 Fields: actual parameters · return value · **control link** (caller's AR) · **access link** (enclosing scope's AR) · saved status (return address, registers) · locals · temporaries [Src: MadeEasy-CS p.82].

### 7.3 Scoping, access links, display (added — not in sources)
- **Static**: name binds to the nearest textually enclosing declaration (C, Java). **Dynamic**: to the most recent active one in the call chain (early LISP, APL).

🔢
```
int x = 10;
void f() { print(x); }
void g() { int x = 20; f(); }
main()   { g(); f(); }
```
Static ⇒ `10 10`; dynamic ⇒ `20 10`.
- Access link: name at depth d used at depth n ⇒ **n − d** hops. Display D[i] → latest AR at depth i (O(1) access).
- 🎯 GATE-2012: Main → A1 → A2 → A21 → A1 ⇒ links A1→Main, A2→Main, A21→A2, A1→Main [Src: Pearson p.66].

### 7.4 Parameter passing

| Method | Passed | Actual changes |
|---|---|---|
| Value | copy | never |
| Reference | address | immediately (aliasing) |
| Value-result | copy in, copy back | at return |
| Name | thunk, re-evaluated per use | like text substitution (Algol 60) |

🔢
```
int a = 2;
void f(int x) { x = x + 1; a = a + 10; print(x); }
main() { f(a); print(a); }
```
value `3 12` · reference `13 13` · value-result `3 3` · name `13 13`.
- Name ≠ reference for `swap(i, a[i])`: the final `a[i]` uses the new i.
- ⚠ Value-result = reference unless aliased [Src: Pearson p.43]. C is call-by-value only; Java passes references by value.

## 8. Intermediate Code Generation

### 8.1 Forms and DAG
- Syntax tree/DAG (graphical); postfix, 3AC (linear). ⭐ IR enables retargeting and a reusable machine-independent optimiser (GATE-2014, 2008).
- Syntax tree: operators inside, operands at leaves, no NTs [Src: AppliedCourse p.65]. ⚠ Pearson p.35 calls the DAG "low-level" — it is high-level.
- Postfix: `(a+b)*(a+b+c)` ⇒ `ab+ab+c+*`.
- 📌 **DAG** shares common subexpressions (node with > 1 parent); nodes = distinct leaves + distinct (op, children).
- 🔢 `a + a*(b−c) + (b−c)*d`: syntax tree 13 nodes, DAG **9** [Src: Pearson p.35].
- Block DAG reuses a node only if operands are unchanged: `a = b−c; b = a−c; e = b−c; f = a−c` ⇒ f shares b's node; e is new because b changed [Src: MadeEasy-CD p.141].
- 🎯 GATE-2014 `a = b+c; c = a+d; d = b+c; e = d−b; a = e+b` ⇒ **6 nodes, 6 edges** (uses algebra).

### 8.2 Three-address code
- ≤ 1 operator per RHS: `x = y op z`, `x = op y`, `x = y`, `goto L`, `if x relop y goto L`, `param`/`call`, `x = y[i]`, `x = *p` [Src: Pearson p.36].

| | Quadruples | Triples | Indirect triples |
|---|---|---|---|
| Fields | op, arg1, arg2, result | op, arg1, arg2 | triples + pointer list |
| Temps | named | positions (n) | positions |
| Reordering | ⭐ easy | hard | easy |
| Space | most | least | middle |

- ⚠ MadeEasy-CS p.74 draws indirect triples with temporaries — they add only a pointer list.
- 🔢 `a = b * −c + b * −c` triples: (0) uminus c · (1) * b (0) · (2) uminus c · (3) * b (2) · (4) + (1) (3) · (5) = a (4).

### 8.3 SSA and backpatching
- **SSA**: each variable assigned once; φ-functions at joins.
- 🔢 GATE-2016 `x = u−t; y = x*v; x = y+w; y = t−z; y = x*y` ⇒ x1, x2, y1, y2, y3 + u, t, v, w, z = **10** variables.
- 🔢 GATE-2015: temporaries for `q + r/3 + s − t*5 + u*v/w` = one per operator = **8**.
- **Backpatching**: emit jumps with blank targets, fill later via `makelist`, `merge`, `backpatch` — one-pass booleans/control flow [Src: Pearson p.41].

## 9. Local Optimisation

### 9.1 Basic blocks
- ⭐ Basic block: entered only at the first, left only at the last statement.
- 📌 **Leaders:** first statement · jump target · statement after a jump.
- Flow graph edge Bi → Bj if Bj can follow Bi. Back edge to a dominator ⇒ loop [Src: Pearson p.60].
- 🔢 GATE-2015: `1 i=1 · 2 j=1 · 3–8 body · 9 if j<=5 goto 3 · 10 i=i+1 · 11 if i<5 goto 2` ⇒ leaders 1, 2, 3, 10 ⇒ 4 blocks + entry + exit = **6 nodes, 7 edges**.

### 9.2 Transformations

| Optimisation | Example |
|---|---|
| Constant folding | `x = 2*3+4` → `x = 10` |
| Constant propagation | `pi = 3.14; a = pi*r` → `a = 3.14*r` |
| Copy propagation | `y = x; z = y+1` → `z = x+1` |
| CSE | `t2 = a+b` → `t2 = t1` |
| Dead-code elimination | drop unused results, `if (0) {…}` |
| Strength reduction | `x*2` → `x<<1`; `x²` → `x*x` |
| Algebraic simplification | `x+0`, `x*1` → `x` |
| Code motion | hoist loop invariants |
| Induction-variable | `t = 4*i` → `t = t+4` |
| Loop unrolling / jamming | fewer tests (NET-Dec-2015) / merge loops [Src: Sanchit p.109] |

- ⚠ `x = 4*5 ⇒ 20` is **folding**, not CSE (GATE-2014). `P*32 → P<<5` is strength reduction (NET-Aug-2016).
- 🎯 GATE-2006: `x += 4*j + 5*i; y += 7 + 4*j` in a loop has invariant, CSE and strength-reduction scope; the false option is **dead code**. ⚠ Sanchit p.114 keys (B); correct is (D).
- **Peephole** (machine-dependent, small window): redundant load/store, jump-to-jump, unreachable code, machine idioms (`INC`) [Src: Pearson p.49].

## 10. Data-Flow Analysis

### 10.1 Framework
- Forward: OUT = gen ∪ (IN − kill), IN = meet of predecessors. Backward: IN = use ∪ (OUT − def), OUT = meet of successors.
- Meet **∪** = may (some path); **∩** = must (all paths). Iterate to a fixed point.

📌

| Analysis | Direction | Meet | Enables |
|---|---|---|---|
| Reaching definitions | forward | ∪ | constant propagation, ud-chains |
| Live variables | backward | ∪ | dead code, register allocation |
| Available expressions | forward | ∩ | global CSE |
| Very busy expressions | backward | ∩ | code hoisting |

- 🎯 GATE-2014: available expressions → CSE and liveness → dead-code elimination are both true.
- **Reaching definitions**: d of x reaches p if some path d → p has no other definition of x; kill[B] = other definitions of variables B defines [Src: Pearson p.63].

### 10.2 Liveness (equations added — not in sources)
- x is live at p if its value may be used before being redefined. use[B] = read before written; def[B] = written before read.
- 📌 OUT[B] = ∪ IN[succ]; IN[B] = use[B] ∪ (OUT[B] − def[B]).

🔢 `B1: i=0; s=0` → `B2: if i≥n goto B4` → `B3: s=s+i; i=i+1; goto B2` · `B4: return s`
- use: B2 {i, n}, B3 {s, i}, B4 {s}; def: B1 {i, s}.
- IN[B4] = {s}; iterating ⇒ IN[B2] = IN[B3] = {i, n, s}; IN[B1] = {n}.
- 🎯 GATE-2015: variables live at both block 2 and block 3 ⇒ {r, u} [Src: Pearson p.67].

### 10.3 Available expressions — CSE (added — not in sources)
- `x op y` available at p if computed on every path to p with no later write to x or y.
- 📌 IN[B] = ∩ OUT[pred]; OUT[B] = e_gen ∪ (IN − e_kill); OUT[entry] = ∅, others start at U. Available recomputation ⇒ reuse the temp.

### 10.4 Constant propagation (added — not in sources)
- Forward lattice: UNDEF (⊤) > constant > NAC (⊥).
- 📌 UNDEF ∧ c = c; c ∧ c = c; c₁ ∧ c₂ = NAC; NAC ∧ v = NAC. `x = y op z` folds if both constant.
- 🔢 Paths giving `c = a+b` (a=2, b=3) and `c = 5` meet ⇒ c = 5 ⇒ `d = c*2` folds to `d = 10`; `c = 6` on one path ⇒ NAC.
- Monotone, not distributive.

## Last-day revision sheet

| Item | Memorise |
|---|---|
| Left recursion | `A → Aα \| β` ⇒ `A → βA′, A′ → αA′ \| ε` |
| Left factoring | `A → αβ₁ \| αβ₂` ⇒ `A → αA′, A′ → β₁ \| β₂` |
| LL(1) test | disjoint FIRSTs; ≤ 1 nullable; FIRST(α) ∩ FOLLOW(A) = ∅ |
| LL(1) table | #NT × (#terminals + 1) |
| Reduce entries | LR(0) row · SLR FOLLOW · CLR/LALR lookahead |
| LR(1) lookahead | FIRST(βa) |
| States | LR(0) = SLR = LALR ≤ CLR (6/6/10; 7/7/10) |
| Power | LR(0) ⊂ SLR ⊂ LALR ⊂ CLR; LL(1) ⊂ LR(1) |
| Max reductions | n − 1 |
| Tokens | literal = 1, `<=` = 1, comments = 0 |
| DAG nodes | distinct leaves + distinct (op, children) |
| SSA temps | = operators |
| Access hops | n − d |
| Reaching / live / available | fwd ∪ / bwd ∪ / fwd ∩ |

1. ⭐ Lexer ⇔ RE/DFA; parser ⇔ CFG/PDA.
2. ⭐ Linker resolves externals; loader allocates, links, relocates, loads.
3. Top-down = LMD; bottom-up = reverse RMD.
4. ⭐ Ambiguous ⇒ not LL(k)/LR(k).
5. Unambiguous ⇒ unique LMD and unique RMD.
6. Left-recursion removal + factoring ≠ LL(1).
7. ⭐ ε ∉ FOLLOW; $ ∈ FOLLOW(S).
8. Every LL(1) grammar is LR(1).
9. ⭐ YACC → LALR(1); LEX → `lex.yy.c`.
10. ⭐ LALR merging ⇒ R/R only.
11. Handle = production + position.
12. Operator grammar: no ε, no adjacent NTs.
13. ⭐ Synthesized ← children; inherited ← parent/left siblings.
14. ⭐ S-attributed ⊂ L-attributed.
15. Static allocation forbids recursion.
16. ⭐ AR = params, return value, control link, access link, status, locals, temps.
17. Static scope = text; dynamic = call chain.
18. Value-result copies back at return; name re-evaluates per use.
19. ⭐ Quadruples reorder easily; triples compact; indirect triples both.
20. ⭐ DAG ⇒ common subexpressions.
21. SSA: one assignment per variable.
22. Backpatching fills jump targets later.
23. ⭐ `4*5 → 20` folding; `x*2 → x<<1` strength reduction.
24. Peephole is machine-dependent.
25. ⭐ Liveness → dead code; available expressions → CSE; reaching definitions → constant propagation.
26. Register allocation = graph colouring.
27. LL(1)/LR parsing is linear time.

## Dropped as outside TPSC syllabus
- **ToC**: Sanchit pp.16–18, 29–36 (Chomsky types, CFG simplification, CNF/GNF, decidability, CYK); MadeEasy-CS pp.1–~25, 68, 81 (counting DFAs, RE from FA, reduced CFGs); MadeEasy-CD p.40.
- **Target code generation**: next-use, code-generator algorithm, register descriptors, spill/register-count PYQs (Pearson pp.44–48, 67).
- **Global loop theory**: dominator trees, natural-loop and u-d chain algorithms (Pearson pp.60–64).
- **Pearson ICG extras**: declaration offsets, OO 3AC, switch tables, type expressions.
- **Program-correctness loop invariants** (MadeEasy-CS p.81).
- File `5` duplicates Sanchit; not cited.
