# 06 · Database Management Systems — Precise Notes
> **TPSC ATO (IT) Paper-II §9** · ~11 marks (estimate) · Syllabus: *"Databases — ER model; relational model: relational algebra, tuple calculus, SQL; integrity constraints, normal forms; file organization, indexing (B and B+ trees); transactions and concurrency control"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson GATE guide, Made Easy class notes (ME-Class, ME-2012, ME-Notebook), Cam-Notes (6.DBMS_Notes). Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/06_DBMS/` (PDF page numbers) — open them for diagrams.

## Which notes are worth your time
| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 1.DBMS.pdf (**Pearson**) | Pearson GATE guide | Typed, two-column | 97 | 3.5 | Hashing, index numericals, TRC/DRC examples, PYQs to 2017 · thin SQL theory, a few wrong statements |
| 2.DBMS_Sanchit_Sir_Notes.pdf (**Sanchit**) | Knowledge Gate | Typed slides | 232 | 4 | Year-tagged GATE/NET PYQs on ER, keys, NF, indexing, transactions, RA · **no SQL**, calculus only named, many unsolved PYQs |
| 3.Made_Easy_Class_DBMS.pdf (**ME-Class**) | Made Easy class | Handwritten scan, dotted noise | 325 | 4 | Deepest: SQL NULL/HAVING/nesting, TRC quantifier traps, ER→table merging, B/B+ order variants · noisy, long |
| 4.Ace_Academy_DMBS_Class_Notes.pdf (**Ace**) | ACE Academy | Handwritten photocopy | 94 | 2.5 | Short FD, lossless, join, index notes · messy, thin |
| 5.DBMS-CS.pdf (**ME-WikiEngg**) | Made Easy (Wiki Engg scan) | Faded scan | 296 | 2 | Anomalies, MVD, logs, multiple granularity · very low density, loose claims |
| 6.DBMS_Notes.pdf (**Cam-Notes**) | Unattributed, Korth-based | Clean CamScanner handwriting | 181 | 4 | Cleanest full syllabus: ER→tables, NF shortcut, TRC vs DRC, SQL, index numericals · one shaky 1:1 table-count note |
| 7.DBMS-NOTES.pdf (**ME-Notebook**) | Made Easy notebook | Neat blue ink | 216 | 3 | Very legible basics, F⁺ counting, spanned/unspanned, recovery · shallow |
| 8.DBMS_Hand_Written_Notes_Made_Easy.pdf (**ME-2012**) | Made Easy 2012 class | Phone photos, watermark | 135 | 3 | Division derivation, I/O-cost formulas, 2PL Venn · cluttered photos |
| 9.DBMS.pdf (**ekxam**) | Unattributed | Phone photos, many sideways | 159 | 1.5 | Navathe-style PYQ solutions · mostly unreadable |

**If you open only one PDF besides these notes:** open **6.DBMS_Notes.pdf (Cam-Notes)**. It is clean, follows Korth's order and fills Sanchit's gaps (SQL, TRC/DRC, index numericals). For GATE-depth traps, use **ME-Class pp.130–175 (SQL/TRC) and pp.230–250 (B/B+ trees)**.

## Topic map
| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | DBMS basics, 3-schema, independence | ⭐⭐ | Definition; "which independence is harder?" |
| 2 | ER model, ER → tables | ⭐⭐⭐ | Minimum number of tables; weak-entity facts; symbols |
| 3 | Keys, integrity constraints | ⭐⭐⭐ | Count super keys; cascade-delete chains |
| 4 | FDs, closure, keys, minimal cover | ⭐⭐⭐ | Find keys / closure / irreducible set |
| 5 | Normal forms, lossless, dependency preservation | ⭐⭐⭐ | Highest NF; "lossless and/or DP?" |
| 6 | Relational algebra | ⭐⭐⭐ | Meaning of an expression; tuple count; division |
| 7 | Tuple & domain calculus | ⭐⭐ | Equivalent query; safe expression |
| 8 | SQL | ⭐⭐⭐ | Output of a query; GROUP BY/HAVING; NULL; ANY/ALL/EXISTS |
| 9 | File organisation, indexing, B/B+ | ⭐⭐⭐ | B+ order; index blocks/accesses; dense vs sparse |
| 10 | Transactions, serializability | ⭐⭐⭐ | ACID owner; precedence graph; recoverable/cascadeless |
| 11 | Concurrency control, deadlock | ⭐⭐⭐ | 2PL variants; TO/Thomas; wait-die vs wound-wait |
| 12 | Log-based recovery | ⭐ | Undo/redo lists after a checkpoint |

---

## 1. DBMS basics & relational model
### 1.1 DBMS vs file system
- A file system brings redundancy and inconsistency, needs one program per query, has **no data independence**, and offers little concurrency, recovery or fine-grained security.
- A DBMS controls redundancy, gives declarative queries, provides concurrency control, log-based recovery, views/GRANT security, and indexing to cut I/O cost. [Src: ME-2012 p.1]
- Database system = DB + DBMS. **Metadata** lives in the **data dictionary / catalog**.
- **Schema** = intension, changes rarely. **Instance / state** = extension, changes constantly.

### 1.2 Three-schema architecture & data independence
- **External** (many views) ↔ **Conceptual** (one logical schema) ↔ **Internal** (storage, access paths), joined by two mappings. [Src: Pearson p.3]
- 📌 ⭐ **Physical independence**: change the internal schema (add an index, reorganise files) without touching the conceptual schema. Easier.
- 📌 ⭐ **Logical independence**: change the conceptual schema without touching views or programs. **Harder**.

### 1.3 Data models, languages, DBA
- Model categories (Navathe): **conceptual** (ER) · **representational** (relational, network, hierarchical) · **physical**.
- Hierarchical = tree (IMS) · network = graph (CODASYL) · ⭐ relational (Codd 1970) · object/object-relational. ER model: Chen 1976.
- **DBA** (added, Korth): defines the schema, storage and access methods; grants authorisation; handles backup and tuning.
- **DDL** writes the dictionary. **DML** is procedural (RA: *how*) or declarative (calculus, SQL: *what*).

### 1.4 Relational terminology
- Tuple = row · attribute = column · **domain** = atomic permitted values · **degree** = number of columns · **cardinality** = number of rows.
- 📌 A relation ⊆ D1 × D2 × … × Dn (NET-JUNE-2013). No duplicate tuples; row and column order irrelevant; atomic values.

---

## 2. ER model
### 2.1 Notation (Chen)
| Construct | Symbol | Relational mapping |
|---|---|---|
| ⭐ Weak entity / identifying relationship | **Double rectangle / double diamond** | Own table, PK = owner PK + partial key |
| Key / partial key | Underline / **dashed underline** | PK / part of PK |
| ⭐ Multivalued attribute | **Double ellipse** | **Separate table** (owner PK, value) |
| Composite attribute | Ellipse with sub-ellipses | Flattened into columns |
| ⭐ Derived attribute | **Dashed ellipse** | Usually not stored |
| Total participation | **Double line** | NOT NULL FK |
| Descriptive attribute | Ellipse on a diamond | Column of the relationship |

[Src: Sanchit p.5–9; Cam-Notes p.12] An ER diagram shows entity *sets* (schema), not individual entities.

### 2.2 Relationships
- Degree: unary/recursive (needs role names), binary, ternary (⚠ not equal to three binaries).
- Cardinality: 1:1, 1:N, N:1, M:N. In Korth the arrow points to the "one" side.
- Participation: total (min ≥ 1) vs partial (min 0). ⚠ (min,max) labels read the opposite way to 1/N labels. [Src: Sanchit p.20–21]
- On M:N, a descriptive attribute **must stay on the relationship** (GATE-2005 "rent" → Lodging).
- 🎯 GATE-2018: R many-to-one E1→E2, both total → every E1 relates to **exactly one** E2. GATE-2017: R merges into A when R is **many-to-one from A** and A is total.

### 2.3 Weak entity sets
- 📌 PK = owner PK + discriminator. The identifying relationship is many-to-one weak → owner; the weak side is **total**; deleting the owner deletes its weak entities; a weak set can own another weak set. [Src: Sanchit p.25–27]
- ⚠ NET-DEC-2015 FALSE option: "weak tuples are **not** partitioned by their owner tuples" (they are).

### 2.4 Generalisation, specialisation, aggregation (added — not in sources)
- **Specialisation** is top-down, **generalisation** bottom-up; both are drawn as **ISA**, and subclasses inherit attributes. Constraints: **disjoint/overlapping**, **total/partial**.
- Mapping options: (a) superclass table + subclass tables keyed by the superclass PK; (b) subclass tables only (if total + disjoint); (c) one table with a type column.
- **Aggregation**: treat a relationship as an entity so it can join another relationship.

### 2.5 ⭐ ER → minimum tables
| Situation | Tables | Rule |
|---|---|---|
| Each strong entity | 1 | — |
| 1:1 (both partial, or one side total) | 2 | R → FK in either side / in the **total** side |
| 1:1, both total | **1** | Merge both |
| 1:N | 2 | R → FK in the **N side** [Src: ME-Class p.190] |
| M:N | **3** | R table, PK = both PKs |
| Multivalued attribute | +1 each | — |
| Weak + owner | 2 | Identifying relationship merges into the weak table |
| Unary 1:N / M:N | 1 / 2 | Self-FK / (sup, sub) table [Src: ME-Class p.195] |
| n-ary relationship | n + 1 | — |

- ⚠ Cam-Notes p.20 counts "1:1, one side total" as 1 table. The standard answer is 2.
- 🔢 Two entities with R1 1:N and R2 M:N → **3** (GATE-2005, NET-2015/17). E1–E2 M:N plus E1–E3 1:N → **4** (GATE-2015). 1:m with one multivalued attribute → **3** (GATE-2004).
- Fan/chasm traps (occasional): ambiguous fan-out of 1:N paths / missing path through partial participation. [Src: Sanchit p.29–30]

---

## 3. Keys & integrity constraints
### 3.1 Keys
| Key | Meaning |
|---|---|
| Super key | X⁺ = all attributes |
| ⭐ Candidate key | **Minimal** super key |
| Primary / alternate | Chosen CK (no NULLs) / the CKs not chosen |
| Foreign key | Refers to a key of some relation (possibly itself = recursive) |
| Prime attribute | Member of **any** CK |

- 📌 PK ⊆ CK ⊆ SK (NET-JAN-2017). No proper superset of a CK is a CK (NET-JULY-2016).
- GATE-2011: a joint bank-account number is not a CK. GATE-2014: an instance key needs X ≠ 19.

### 3.2 ⭐ Counting keys
- 📌 One CK of k attributes among n: **2ⁿ⁻ᵏ** super keys (GATE-2014: R(EFGH), key E → **8**).
- 📌 Two CKs: 2ⁿ⁻|K1| + 2ⁿ⁻|K2| − 2ⁿ⁻|K1∪K2|. Every attribute a key: 2ⁿ − 1. Max CKs = C(n, ⌊n/2⌋).
- 🔢 R(ABCD) with CKs A and BC → 8 + 4 − 2 = **10**.

### 3.3 Integrity constraints
- **Domain** (type, CHECK, NOT NULL) · **key/UNIQUE** · ⭐ **entity integrity**: PK never NULL · ⭐ **referential integrity**: FK is NULL or matches an existing key · **semantic** (marks ≤ 100) via CHECK / ASSERTION / TRIGGER.
- ⭐ RI is violated by an **insert into the child** or a **delete from the parent** (NET-JULY-2018), and by key updates. DROP TABLE fails on a table referenced by an FK (NET-JUNE-2015).

### 3.4 Referential actions
- NO ACTION/RESTRICT (reject) · **ON DELETE CASCADE** (delete children, recursively) · **ON DELETE SET NULL** · SET DEFAULT · ON UPDATE CASCADE.
- 🔢 GATE-2005: in a self-referencing cascade table, deleting (2,4) removes (5,2), (7,2) and then **(9,5)**.
- 🔢 GATE-2017: T2.S → T1.P with **SET NULL**. Deleting (3,8) from T1 only nulls T2 rows, so **0** extra T1 rows are deleted.

---

## 4. Functional dependencies
### 4.1 Basics & Armstrong's axioms
- X → Y: tuples equal on X are equal on Y. Trivial if Y ⊆ X.
- ⚠ An instance can only **disprove** an FD; FDs belong to the schema. [Src: ME-Class p.30] An all-distinct column determines everything (GATE-2000 → YZ → X, Y → Z).
- Axioms (Armstrong 1974, **sound + complete**): **reflexivity** (Y ⊆ X ⇒ X → Y), **augmentation** (X → Y ⇒ XZ → YZ), **transitivity**.
- Derived rules: **union**, **decomposition** (X → YZ ⇒ X → Y), **pseudo-transitivity** (X → Y, WY → Z ⇒ WX → Z), **composition** (X → Y, Z → W ⇒ XZ → YW).
- ⚠ XY → Z does **not** give X → Z.

### 4.2 Closure & equivalence
- 📌 X⁺: keep adding the RHS of FDs whose LHS ⊆ the current set. X is a super key ⇔ X⁺ = R.
- 📌 F ≡ G ⇔ each set's FDs follow from the other.
- 📌 Number of FDs in F⁺ = Σ over subsets X of 2^|X⁺|. For R(ABC), {A→B, B→C} → **43**. [Src: ME-Notebook p.75]

### 4.3 ⭐ Candidate keys (shortcut)
1. Attributes never on an RHS are in **every** key.
2. Attributes only on an RHS are in **none**.
3. Grow the essential set with the remaining attributes; keep the minimal sets. Swap trick: key K and Y → A (A ∈ K) ⇒ test (K − A) ∪ Y.
- 🔢 GATE-2005: R(ABCDEH), {A→B, BC→D, E→C, D→A}. E and H are essential; (EH)⁺ = EHC. AEH, BEH, DEH all reach everything → **3 keys**.
- 🔢 GATE-2013: {CH→G, A→BC, B→CFH, E→A, F→EG}, D essential → AD, BD, ED, FD = **4**.

### 4.4 Canonical (minimal) cover
1. Split each RHS to single attributes.
2. Drop **extraneous LHS** attributes.
3. Drop **redundant FDs**.
4. Merge FDs with the same LHS.
- Do step 2 before step 3; the result is not unique. [Src: ME-Class p.50]
- 🔢 GATE-2017: {V→W, VW→X, Y→VX, Y→Z}. W is extraneous (V⁺ ∋ W) → V→X. Then Y→X is redundant → **{V→W, V→X, Y→V, Y→Z}**.
- GATE-2014: AB→E is not derivable from {AB→C, D→E, E→C}, so it is not redundant.

🎯 **How it's asked:** FDs satisfied by an instance (GATE-2000/02); candidate keys (GATE-2005/13/14, NET ×4); irreducible set (GATE-2017); match Armstrong rules (NET-DEC-2013).

---

## 5. Normalisation
### 5.1 Definitions
Anomalies (insert/delete/update) come from FDs whose LHS is not a key. ⚠ Normalisation does **not** reduce joins (NET-AUG-2016).

| NF | Condition (every non-trivial X → A) |
|---|---|
| 1NF | Atomic values |
| 2NF | No non-prime A depending on a **proper subset of a CK** |
| 3NF | X super key **or** A prime |
| ⭐ BCNF | X **super key** |
| 4NF | Every non-trivial MVD X →→ Y has X a super key |
| 5NF | Every JD is implied by the candidate keys |

### 5.2 ⭐ Highest-NF shortcut [Src: Cam-Notes p.70]
After finding the CKs, classify each FD; the relation sits at the weakest result.
- X super key → BCNF-ok.
- X not a super key, A prime → violates BCNF only (still 3NF).
- X a proper subset of a CK, A non-prime → violates **2NF**.
- Otherwise (non-key → non-prime) → violates **3NF**.
- 🔢 R(ABCD), {AB→C, AB→D, C→A, D→B}: CKs AB, AD, BC, CD, so everything is prime; C→A → **3NF, not BCNF** (NET-DEC-2014).
- 🔢 GATE-2020: (rollno, courseid, email) with email → rollno → **3NF not BCNF**. R(ABCD) with {AB→D, A→C} → **1NF** (partial).

### 5.3 Facts MCQs love
- ⭐ A two-attribute relation is in BCNF. All attributes prime ⇒ ≥ 3NF. All CKs single-attribute ⇒ ≥ 2NF. 3NF + all CKs single-attribute ⇒ BCNF.
- ⭐ A prime attribute **can** be transitively dependent on a key in 3NF, **never** in BCNF (GATE-2017).
- BCNF has zero FD redundancy (GATE-2002). ER-derived relations are in 1NF (NET-2018). 3NF is the "adequate" design form (NET-2013).

### 5.4 ⭐ Lossless join
- Lossy joins add **spurious** tuples: r ⊂ r1 ⋈ r2 (GATE-2005).
- 📌 Binary test: R1 ∪ R2 = R, R1 ∩ R2 ≠ ∅, and **(R1 ∩ R2) → R1 or (R1 ∩ R2) → R2**. For more pieces, merge pairs that pass the test (or use the chase). [Src: ME-Class p.60]
- 🔢 R(ABCDE), {AD→B, C→DE, B→AE, AE→C}; ABD + ACDE share AD, AD⁺ = all → lossless (NET-2016). {B→C, D→A} into BC, AD → no common attribute → lossy.
- 🔢 {AB→C, C→D, B→E} into ABC, CD, BE: C→D merges to ABCD, then B→E merges BE → **lossless**.

### 5.5 Dependency preservation
- 📌 (F1 ∪ … ∪ Fn)⁺ = F⁺, where Fi = projection of F⁺ on Ri; FDs may be inferred across pieces (NET-DEC-2010).
- Test X → Y: Z = X; repeat Z ∪= ((Z ∩ Ri)⁺ ∩ Ri) until stable; preserved iff Y ⊆ Z.
- 🔢 GATE-2019: X(PQRS), {QR→S, R→P, S→Q} into PR, QRS → lossless + DP, but QRS is not BCNF (S→Q) → "II only". GATE-2001: {A→B, C→D} into AB, CD → **DP but lossy**.

### 5.6 Guarantees
- ⭐ 3NF synthesis is **always lossless + DP**. BCNF is **always lossless**, DP **not guaranteed** (GATE-2005). GATE-2001: {AB→C, C→AD} has no lossless DP BCNF decomposition.
- ⚠ Sanchit p.99 keys GATE-2002 ("tell the BCNF decomposition from the 3NF one") as *Lossless-join*. Both are lossless, so the correct test is **(C) BCNF definition**.

### 5.7 MVD, 4NF, 5NF (brief)
- X →→ Y: X fixes a *set* of Y values independent of the rest (two independent multivalued facts in one table). [Src: Sanchit p.86–88]
- Every FD is an MVD. ⚠ X →→ BC does **not** split (X → BC does). [Src: ME-Class p.100]
- 📌 Fagin: (XY, X(R − Y)) is lossless ⇔ X →→ Y. MVD ⊂ JD. NET-DEC-2005 match: 2NF ↔ no partial, 3NF ↔ no transitive, 4NF ↔ no MVD, 5NF ↔ no JD.

🎯 **How it's asked:** highest NF (GATE-2004/08/09/20, NET ×6); FALSE NF statement (GATE-2005/12/17); lossless/DP of a decomposition (GATE-2001/19, NET-2016/17).

---

## 6. Relational algebra
### 6.1 Operators
- 📌 Fundamental set **{σ, π, ∪, −, ×, ρ}**. ∩ = R − (R − S); ⋈θ = σθ(R × S); ÷ is derived.
- σ is commutative and can be cascaded. **π removes duplicates**. ∪, ∩ and − need **union-compatible** inputs.
- ⚠ Sanchit p.201 caps π at n − 1 columns; in fact π may list all n attributes.
- Natural join: equality on **all** common names, keeps one copy. No common attribute → **×**; all attributes common → **∩**.
- RA works on sets, SQL on bags.

### 6.2 Outer joins
- ⟕ keeps unmatched left tuples (NULL-padded), ⟖ the right ones, ⟗ both.
- 🔢 GATE-2015: R1 = {(1,5), (3,7)}, R2(A,C) = {(1,7), (4,9)} → ⟗ = {(1,5,7), (3,7,NULL), (4,NULL,9)}.
- 🔢 NET-2016: T1(P,R) = {(10,5), (15,8), (25,6)}, T2(A,C) = {(10,6), (25,3), (10,5)} → ⋈P=A gives 3, left outer join 4, ⋈(P=A ∧ R=C) 1.

### 6.3 ⭐ Division
- 📌 **R(A,B) ÷ S(B) = π_A(R) − π_A((π_A(R) × S) − R)** = the A values paired with **every** B.
- 🔢 E = {s1c1, s1c2, s1c3, s2c1, s2c2, s3c1}, C = {c1, c2, c3} → {s1}. [Src: ME-2012 p.45]
- The shape "A − π(…)" reads "for all": GATE-2014 → employees older than **all** their dependents; GATE-2004 → girls scoring above **all** boys; GATE-2007 → courses with a **proper subset** of female students.

### 6.4 ⭐ Result-size bounds (|R| = m, |S| = n)
| Expression | Min | Max |
|---|---|---|
| σ(R), R − S | 0 | m |
| π(R) | 1 (m ≥ 1) | m (= m if a key is projected) |
| R ∪ S / R ∩ S | max(m,n) / 0 | m+n / min(m,n) |
| R × S | m·n | m·n |
| R ⋈ S | 0 | m·n (GATE-1999) |
| R ⟕ S / R ⟗ S | m / max(m,n) | max(m·n, m) / max(m·n, m+n) |
| R ÷ S | 0 | ⌊m/n⌋ |

- 📌 Join attribute = key of S, and R holds a non-NULL FK to it → exactly **m** rows. GATE-2010: B→A→C makes B the key of R → max **100**.

### 6.5 Equivalences & limits
- σ_{A=a}(r ⋈ s) = σ_{A=a}(r) ⋈ s (GATE-2001). π_A1(π_A2 r) = π_A1(r) if A1 ⊆ A2 (GATE-2014).
- ⚠ σ_c(π_L R) ≠ π_L(σ_c R) when c uses attributes outside L (GATE-1998).
- FK B → C ⇒ π_B(r1) − π_C(r2) = ∅ (GATE-2004/12).
- ⚠ Basic RA cannot express **SUM** (GATE-2000) or **reachability / transitive closure** (GATE-2001).

---

## 7. Relational calculus (TRC & DRC)
- **TRC** { t | P(t) } ranges over tuples; **DRC** { ⟨x1..xn⟩ | P } ranges over domain values. Both non-procedural.
- 🔢 Names with marks > 10 [Src: Cam-Notes p.86]
  - TRC: { t | ∃s ∈ Student (s.marks > 10 ∧ t.name = s.name) }
  - DRC: { ⟨n⟩ | ∃r, m (⟨r,n,m⟩ ∈ Student ∧ m > 10) }
- Division: { s | s ∈ Sailors ∧ ∀b ∈ Boats ∃r ∈ Reserves (r.sid = s.sid ∧ r.bid = b.bid) }. [Src: Pearson p.25]
- ⚠ Restricted "for all" needs **→**: ∀c ∈ Course (c.inst = 'Korth' → ∃e …). Using ∧ forces every course to be Korth's. [Src: ME-Class p.175]
- "At least two": ∃x∃y(P(x) ∧ P(y) ∧ x ≠ y). "Exactly one": ∃x(P(x) ∧ ∀y(P(y) → y = x)). [Src: ME-Class p.170]
- 📌 **Safe** = finite result drawn from dom(P). { t | ¬(t ∈ R) } is unsafe (GATE-2017 asks which queries are safe).
- ⭐ RA ≡ safe TRC ≡ safe DRC (relational completeness). SQL adds aggregates, grouping and bags.

---

## 8. SQL
### 8.1 Command classes
- **DDL**: CREATE, ALTER, DROP, TRUNCATE, RENAME · **DML**: SELECT, INSERT, UPDATE, DELETE · **DCL**: GRANT, REVOKE · **TCL**: COMMIT, ROLLBACK, SAVEPOINT.
- DELETE (DML) supports WHERE, can roll back and fires triggers. TRUNCATE (DDL) removes all rows but keeps the structure. DROP (DDL) removes rows and structure.
- ⚠ Pearson p.30 writes `DELETE * FROM t` and `INNER JOIN … WHERE`. The standard forms are `DELETE FROM t` and `JOIN … ON`.

### 8.2 ⭐ Evaluation order & grouping
📌 **FROM → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY** [Src: ME-Class p.140; Cam-Notes p.98]
- WHERE filters rows (no aggregates); HAVING filters groups.
- Non-aggregated SELECT columns must be in GROUP BY; GROUP BY columns **need not** be selected (GATE-2012).
- ⚠ ME-Class p.140 says HAVING is "always with GROUP BY" and can't use plain attributes. Standard SQL allows **HAVING without GROUP BY** (whole table = one group; GATE-2012 P is true), and grouping columns may appear in HAVING.
- ⭐ SELECT = RA projection **keeping duplicates** (GATE-2015). LIKE: `%` any string, `_` one character. BETWEEN is inclusive. ORDER BY defaults to ASC.

### 8.3 ⭐ NULLs & aggregates
- Any comparison with NULL (even NULL = NULL) gives **UNKNOWN**; WHERE keeps only TRUE.
- F ∧ U = F, T ∨ U = T, NOT U = U. Use IS NULL.
- ⚠ `x NOT IN (… NULL …)` is never TRUE → **empty result**. [Src: ME-Class p.165]
- GROUP BY puts NULLs in one group. UNIQUE allows several NULLs.
- Aggregates **ignore NULLs** except **COUNT(\*)**. On empty input: COUNT → 0, SUM/AVG/MAX/MIN → **NULL**. AVG(c) = SUM(c)/COUNT(c). [Src: Pearson p.23]

### 8.4 Joins, set operations
- JOIN … ON, NATURAL JOIN, USING, LEFT/RIGHT/FULL OUTER, CROSS (= ×), self-join with aliases.
- UNION, INTERSECT and EXCEPT drop duplicates. The ALL forms keep them: m + n, min(m,n), max(0, m − n) copies.
- ⭐ GATE-2014: `R WHERE a IN (SELECT a FROM S)` ≡ joining R with `(SELECT DISTINCT a FROM S)`. A plain join duplicates R rows.

### 8.5 ⭐ Subqueries
| Construct | True when |
|---|---|
| IN / NOT IN | ≡ `= ANY` / `<> ALL` (a NULL in the list kills NOT IN) |
| > ANY (Q) | x > min; **FALSE if Q empty** |
| > ALL (Q) | x > max; **TRUE if Q empty** |
| EXISTS (Q) | Q returns ≥ 1 row |
| = (scalar Q) | Q must return one row, else **error** |

- A correlated subquery is re-run per outer row; an uncorrelated one runs once, first. [Src: ME-Class p.150]
- Max: `cap >= ALL (SELECT cap …)` (GATE-2015). Second highest: `MAX(sal) WHERE sal < (SELECT MAX(sal) …)`.
- Division: `NOT EXISTS (all courses EXCEPT this student's courses)`. [Src: ME-Class p.160]
- GATE-2009: nested NOT IN … NOT IN (non-blue parts) = suppliers of **only blue** parts.

### 8.6 Views, triggers
- A **view** is virtual and gives security plus **logical independence**; a materialised view is stored.
- Updatable view: one base table, no aggregate/GROUP BY/DISTINCT. `WITH CHECK OPTION` rejects rows that fall outside the view.
- **Assertion** = DB-wide CHECK. **Trigger** = Event–Condition–Action rule (active database). [Src: Pearson p.13]

### 8.7 🔢 Output-of-query patterns
- GATE-2011 Loan_Records: (Borrower, Manager) NATURAL JOIN (Manager, Amount) → Sunderajan 2×2 + Ramgopal 1×1 = **5**.
- GATE-2017: AVG of per-dept counts {4,3,3,2,1} = **2.6**. GATE-2011: inserts (MX+1, 2·MY+1) → Y = 2ˣ − 1, so X = 7 → **127**.
- GATE-2006 ranking: `count(B) WHERE A.bal <= B.bal` ranks tied leaders 2. `1 + count(… <)` loses the top customer (no join row). **Neither** is correct.

---

## 9. File organisation & indexing
### 9.1 Files & hashing
- 📌 bfr = ⌊B/R⌋ (unspanned); blocks b = ⌈r/bfr⌉. Spanned: ⌈r·R/B⌉. 🔢 4000 × 100 B, B = 512 → spanned **782**, unspanned **800**. [Src: ME-Notebook p.120]
- Heap: linear search (avg b/2). Sorted: **⌈log₂ b⌉** on the ordering field only. ⚠ Sanchit p.108's second "unordered … O(log₂ n)" should read **ordered**.
- Static hash: about 1 access for equality. Collisions: open addressing / chaining / multiple hashing. Load 0.7–0.9, M prime.
- **Extendible hashing**: 2ᵈ directory (global depth d, local d′); it doubles when a bucket with d′ = d overflows; 2 accesses. **Linear hashing** has no directory. [Src: Pearson p.84–85]
- ⭐ Hashing wins for equality, ordered indexes for **range** (GATE-2011).

### 9.2 ⭐ Index types
| Index | File ordered on it? | Field | Dense? | Entries |
|---|---|---|---|---|
| Primary | Yes | Key | Sparse | = number of **blocks** |
| Clustering | Yes | Non-key | Sparse | = **distinct values** |
| Secondary | No | Key / non-key | **Dense** | = **records** / distinct values (via indirection) |

- At most **one** primary-or-clustering index per file (one physical order); any number of secondary indexes. "Clustered" = data in index order (GATE-2013/15); clustering = non-key + ordering (GATE-2008). [Src: Sanchit p.106–112]
- ⚠ Sanchit p.112 says the file is ordered on the secondary-index field. It is **not**, which is why the index must be dense. Sanchit p.111 calls clustering "sparse and dense"; Navathe: **non-dense**.

### 9.3 ⭐ Index cost numericals
- 📌 Single-level: **⌈log₂ bᵢ⌉ + 1** accesses.
- 📌 Multilevel: fan-out fo = ⌊B/(key + pointer)⌋; levels t = ⌈log_fo(entries)⌉; accesses **t + 1**.
- 🔢 r = 30,000, R = 100, B = 1024, key 9, pointer 6 → b = 3000, bfrᵢ = 68.
  - Primary index: 45 blocks → **7** accesses (vs 12 without). [Src: Cam-Notes p.160]
  - Secondary index: 442 blocks → 10. Multilevel 442 → 7 → 1 → **4**.
- 🔢 GATE-2008: 16384 × 32 B records, B = 1024, 6 + 10 B entries → secondary index **256** first-level blocks, **4** second-level.

### 9.4 B-tree vs B+ tree
| | B-tree | B+ tree |
|---|---|---|
| Record pointers | Every node | **Leaves only** |
| Leaves linked | No | ⭐ Yes → fast **range** queries (GATE-1999) |
| Internal fan-out | Lower | Higher → shorter tree |

- Both are height-balanced: all paths are equal (GATE-2016). They are preferred to BSTs because disks move **blocks** and are slow (GATE-2000/05).
- ⚠ GATE-2019: "non-leaf nodes point to data records" is **false** for B+. Nodes settle about 69 % full. [Src: Sanchit p.117]

### 9.5 ⭐ Order calculations
**Definition used:** order **p = max child pointers per node** (Navathe; Korth's n). ⚠ Some books use max keys, or min keys d (2d max). Read the question. [Src: ME-Class p.240]
- Internal node: ≤ p children and ≤ p − 1 keys; non-root ≥ ⌈p/2⌉ children / ⌈p/2⌉ − 1 keys; root ≥ 2 children. B+ leaf: ⌈p_leaf/2⌉ … p_leaf keys.
- 📌 B-tree: **p·Pb + (p−1)(K + Pr) ≤ B** · B+ internal: **p·Pb + (p−1)K ≤ B** · B+ leaf: **p_leaf(K + Pr) + Pb ≤ B**.
- 🔢 Answers: GATE-2017 **52**; GATE-2015 (max keys, non-leaf) **50**; GATE-2007 (leaf) **63**; GATE-2006 **34**; GATE-2004 (B+) **26**; GATE-2004 (B-tree) **23**; GATE-2002 **43**; GATE-2010 (max 5 keys → min) **2**. [Src: Sanchit p.124–126]
- 📌 h levels: B-tree max keys **pʰ − 1**, min keys **2⌈p/2⌉ʰ⁻¹ − 1**.

### 9.6 Insertion & deletion
- On overflow, **split**. In a B-tree and in B+ internal nodes the middle key **moves up**; in a B+ leaf it is **copied up**.
- Splits propagate; height grows only at the **root**. [Src: ME-Class p.230; Pearson p.88–89]
- 📌 Max new nodes per insertion with h levels = **h + 1** (GATE-2005: 4 levels → 5). GATE-2008: order 4, 10 insertions → max **5** splits.
- Delete: borrow from a sibling, else merge (may propagate; height shrinks at the root).

🎯 **How it's asked:** B+ order from sizes (GATE-2002/04/06/07/15/17); index levels/blocks (GATE-2008); dense/sparse/clustered definitions; "why B+?" (GATE-1999/2000/05/16/19).

---

## 10. Transactions
### 10.1 ACID & states
| Property | Meaning | Ensured by |
|---|---|---|
| Atomicity | All or nothing | Recovery manager |
| ⭐ Consistency | Run alone, keeps constraints (A+B constant, GATE-2015) | **Programmer** |
| Isolation | Concurrent ≡ some serial order | **Concurrency control** |
| Durability | Committed changes survive | Recovery manager |

- ⚠ Pearson p.65 defines Consistency as serial-order equivalence. That is **Isolation**. Deadlock-freedom is not ACID (GATE-2016).
- States: Active → Partially committed → Committed; failure → Failed → Aborted. [Src: Sanchit p.131]

### 10.2 Anomalies
- **Lost update** (WW) · **dirty read / temporary update** (WR from uncommitted) · **unrepeatable read** (RW between two reads) · **phantom** (a predicate re-read sees inserted/deleted rows).
- ⚠ Sanchit p.135 equates unrepeatable and phantom reads. Phantoms involve **new rows** and need predicate/index locking.
- Isolation levels (added): Read Uncommitted < Read Committed (no dirty reads) < Repeatable Read < Serializable (no phantoms).

### 10.3 Schedules
- Serial schedules for n transactions: **n!**. 📌 All schedules = (Σnᵢ)! / Π(nᵢ!).
- 🔢 5 + 3 operations → 56 schedules, 54 non-serial. GATE-2017 → **54** conflict-serializable.

### 10.4 ⭐ Conflict & view serializability
- Conflict = different transactions, same item, at least one write.
- 📌 **Precedence graph**: Ti → Tj when Ti's conflicting operation comes first. **Acyclic ⇔ CS**; serial order = **topological sort** (GATE-2016). [Src: Sanchit p.140, 157]
- 🔢 GATE-2014: r1x r2x w1x r3x w2x → T1⇄T2 cycle → not CS. r2x w2x r3x r1x w1x → T2→T3→T1 → CS.
- View equivalence: same **initial read**, same **reads-from**, same **final write**.
- 📌 CS ⊂ VS. VS-but-not-CS ⇒ a **blind write**. VS testing is NP-complete. [Src: Sanchit p.147]

### 10.5 ⭐ Recoverability
- **Recoverable**: Tj reads from Ti ⇒ Ti commits first.
- **Cascadeless**: read only committed data.
- **Strict**: no read **or write** of X until its last writer ends.
- 📌 Strict ⊂ Cascadeless ⊂ Recoverable. A schedule can be CS yet non-recoverable.

| Problem | Removed by serializable? | recoverable? | cascadeless? | strict? |
|---|---|---|---|---|
| Lost update, unrepeatable read | ✅ | ❌ | ❌ | ❌ |
| Commit after a dirty read (irrecoverable) | ❌ | ✅ | ✅ | ✅ |
| Cascading rollback | ❌ | ❌ | ✅ | ✅ |
| Undo erasing another transaction's write | ❌ | ❌ | ❌ | ✅ |

[Adapted from Src: ME-Class p.310]
- GATE-2008: reading uncommitted data → irrecoverable. GATE-2015: T2 commits after reading T1's write, then T1 fails → **non-recoverable**. GATE-2016: no cascading abort, not strict.

---

## 11. Concurrency control
### 11.1 Locking
- S is compatible only with S. **2PL** = growing phase then shrinking phase; the **lock point** fixes the serial order. Upgrades only while growing. [Src: Sanchit p.170]

| Variant | CS | Deadlock-free | Strict/cascadeless |
|---|---|---|---|
| Basic 2PL | ✅ | ❌ | ❌ |
| Conservative (all locks up front) | ✅ | ✅ | ❌ |
| ⭐ Strict (X locks to commit) | ✅ | ❌ | ✅ |
| Rigorous (all locks to commit; order = commit order) | ✅ | ❌ | ✅ |

- GATE-2016: ordered locking, then release all → serializable + deadlock-free. GATE-2019: strict 2PL → CS + recoverable.
- Locking and TO are **pessimistic**; validation is **optimistic** (NET-2014).
- **Tree protocol**: X locks only; lock a node only while holding its parent; no relocking → CS + **deadlock-free**, but not recoverable. [Src: Sanchit p.179–180]

### 11.2 ⭐ Timestamp ordering & Thomas write rule
- **read(Q)**: if TS(Ti) < W-TS(Q), roll back Ti; else read and set R-TS = max(R-TS, TS(Ti)).
- **write(Q)**: if TS(Ti) < R-TS(Q), roll back Ti.
- **write(Q)**: if TS(Ti) < W-TS(Q), roll back Ti — but under **Thomas, ignore the write**.
- **write(Q)** otherwise: write and set W-TS = TS(Ti). A rolled-back transaction restarts with a **new** timestamp.
- Basic TO gives **CS + deadlock-free**, but may be non-recoverable and can starve long transactions (GATE-2010).
- 📌 Thomas accepts some **VS-not-CS** schedules (GATE-2019) and allows every schedule that basic TO allows. [Src: Sanchit p.162–165]

### 11.3 Validation & multiple granularity
- **Validation**: read → validate → write phases; cheap when conflicts are rare; cascadeless. **Multiversion**: reads never wait.
- **Granularity locks** IS/IX/S/SIX/X: acquire root→leaf, release leaf→root. [Src: Sanchit p.186–188]

| Requested ↓ / held → | IS | IX | S | SIX | X |
|---|---|---|---|---|---|
| IS | ✅ | ✅ | ✅ | ✅ | ❌ |
| IX | ✅ | ✅ | ❌ | ❌ | ❌ |
| S | ✅ | ❌ | ✅ | ❌ | ❌ |
| SIX | ✅ | ❌ | ❌ | ❌ | ❌ |
| X | ❌ | ❌ | ❌ | ❌ | ❌ |

### 11.4 ⭐ Deadlock handling
| Ti requests an item held by Tj | Ti older | Ti younger |
|---|---|---|
| **Wait-die** (non-pre-emptive) | Ti waits | Ti dies |
| **Wound-wait** (pre-emptive) | Tj wounded | Ti waits |

- 📌 "Old waits, young dies" / "old wounds, young waits". Only the younger transaction is rolled back, and it restarts with its **old** timestamp → no starvation.
- 🔢 GATE-2017: "TS(T2) < TS(T1) ⇒ kill holder T1, else T2 waits" = wound-wait → **deadlock- and starvation-free**.
- Other options: timeouts; **detection** via a **wait-for graph** (cycle ⇔ deadlock), then victim selection and total/partial rollback. [Src: Sanchit p.181–185]

🎯 **How it's asked:** which protocol gives CS + deadlock-freedom (GATE-2010, NET-2014/15); strict 2PL / Thomas statements (GATE-2019); identify the scheme (GATE-2017).

---

## 12. Log-based recovery (brief)
- Log: ⟨T start⟩, ⟨T, X, old, new⟩, ⟨T commit⟩. **Undo** goes backward (old values); **redo** goes forward (new values). [Src: Sanchit p.155]
- 📌 **WAL**: the log record reaches stable storage before the data page, and the log before commit.
- Deferred update = **NO-UNDO/REDO** (NET-2006). Immediate update = **UNDO/REDO**. Shadow paging = NO-UNDO/NO-REDO.
- **Checkpoint**: committed before it → nothing; committed after it → **redo**; uncommitted → **undo**. 🔢 GATE-2015 → Undo {T3, T1}, Redo {T2}.
- ⚠ ME-WikiEngg p.170 says the log is removed after commit. It is kept for redo and truncated only after a checkpoint or backup.

---

## Last-day revision sheet
| Item | Formula / number |
|---|---|
| Super keys (1 CK, k of n attributes) | 2ⁿ⁻ᵏ |
| Super keys (CKs K1, K2) | 2ⁿ⁻\|K1\| + 2ⁿ⁻\|K2\| − 2ⁿ⁻\|K1∪K2\| |
| Max candidate keys | C(n, ⌊n/2⌋) |
| FDs in F⁺ | Σ over subsets X of 2^\|X⁺\| |
| Lossless (binary) | (R1∩R2) → R1 or → R2 |
| Division | π_A(R) − π_A((π_A(R) × S) − R) |
| Join size | 0 … m·n; = m if FK → key |
| Schedules | (Σnᵢ)!/Π nᵢ! ; serial k! |
| Blocks | ⌈r / ⌊B/R⌋⌉ |
| Index access | ⌈log₂ bᵢ⌉ + 1 ; multilevel t + 1 |
| B-tree node | p·Pb + (p−1)(K+Pr) ≤ B |
| B+ internal / leaf | p·Pb + (p−1)K ≤ B / n(K+Pr) + Pb ≤ B |
| Min children / keys (non-root) | ⌈p/2⌉ / ⌈p/2⌉ − 1 |
| B-tree keys, h levels | max pʰ − 1, min 2⌈p/2⌉ʰ⁻¹ − 1 |
| New nodes per insert | h + 1 |
| Fill factor / hash load | ≈ 69 % / 0.7–0.9 |

1. ⭐ Physical independence is easier than logical independence.
2. ⭐ Weak entity: double rectangle; PK = owner PK + partial key; total participation.
3. ⭐ Tables: M:N → 3; 1:N → 2; 1:1 both total → 1; multivalued attribute → +1.
4. ⭐ Entity integrity: PK not NULL. RI is broken by a child insert or a parent delete.
5. Attributes never on an RHS are in every key.
6. ⭐ 3NF: LHS super key or RHS prime. BCNF: LHS super key.
7. ⭐ A two-attribute relation is in BCNF; all-prime ⇒ ≥ 3NF.
8. ⭐ 3NF is always lossless + DP; BCNF may lose DP.
9. A lossy join adds spurious tuples.
10. X →→ BC does not split.
11. π removes duplicates; SQL SELECT keeps them.
12. Natural join with no common column = ×.
13. Basic RA has no SUM and no transitive closure.
14. RA ≡ safe TRC ≡ safe DRC; restricted ∀ uses →.
15. ⭐ FROM, WHERE, GROUP BY, HAVING, SELECT, ORDER BY.
16. ⭐ HAVING without GROUP BY is legal.
17. ⭐ Aggregates ignore NULL except COUNT(*); empty input → COUNT 0, others NULL.
18. ⭐ NOT IN over a NULL → empty; > ALL(∅) = TRUE; > ANY(∅) = FALSE.
19. DELETE = DML; TRUNCATE/DROP = DDL.
20. ⭐ Primary and clustering indexes are sparse; secondary indexes are dense.
21. ⭐ B+: data in leaves, linked leaves → range queries; hashing → equality.
22. ⭐ A, D → recovery manager; I → concurrency control; C → programmer.
23. ⭐ Acyclic precedence graph ⇔ CS; VS-not-CS has a blind write.
24. ⭐ Strict ⊂ cascadeless ⊂ recoverable.
25. ⭐ 2PL ⇒ CS, not deadlock-free; strict 2PL ⇒ recoverable.
26. ⭐ TO ⇒ CS + deadlock-free; Thomas ⇒ VS.
27. ⭐ Wait-die: old waits. Wound-wait: old wounds.
28. Wait-for graph cycle ⇔ deadlock.
29. Deferred update = no-undo; WAL = log before data.
30. Codd 1970 · Chen 1976 · Armstrong 1974 · SQL from SEQUEL (IBM System R).

## Dropped as outside TPSC syllabus
- Data warehousing, OLAP/OLTP, data mining, special DB types (multimedia, deductive, temporal, GIS) — Ace pp.1–2.
- Distributed DB / 2-phase commit — Sanchit p.195.
- Query optimisation and cost (nested-loop buffers GATE-2014, query plans GATE-2006, selectivity GATE-2007, heuristic rewriting) — Sanchit pp.127, 229–231; Cam-Notes pp.80, 110. Kept only the σ/π equivalences in §6.5.
- Disk hardware timing, memory hierarchy, OS file allocation, AVL-on-disk digression — Pearson pp.81–83; ME-Class p.225.
- Snapshot isolation, multiversion internals, B+-tree concurrency, degree-two consistency — Sanchit pp.192–193.
- Lamport clocks, ODBC, DFD "black hole", vendor datatypes — scattered PYQ items.
