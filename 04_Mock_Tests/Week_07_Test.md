# Week 7 Mock Test — Databases

**Syllabus §9** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — Databases (Q1–Q20)

**Q1.** In the relational model, the number of **attributes** in a relation is called its
(A) cardinality  (B) degree  (C) domain  (D) tuple count

**Q2.** Which of the following is **not** a fundamental (primitive) operation of relational algebra?
(A) Selection (σ)  (B) Projection (π)  (C) Natural join (⋈)  (D) Set difference (−)

**Q3.** Consider `R(A, B, C, D)` with functional dependencies `A → B`, `B → C`, `C → D`. The highest normal form that R satisfies is
(A) 1NF  (B) 2NF  (C) 3NF  (D) BCNF

**Q4.** A relation is in **BCNF** if, for every non-trivial functional dependency X → Y,
(A) X is a superkey
(B) Y is a candidate key
(C) X is a prime attribute
(D) Y is a non-prime attribute

**Q5.** A relation is in **3NF** but not in BCNF when a functional dependency X → Y exists where X is not a superkey and
(A) Y is a non-prime attribute
(B) Y is a prime attribute
(C) Y is empty
(D) X is empty

**Q6.** Given `R(A, B, C)` with `AB → C` and `C → A`, the candidate keys are
(A) AB only  (B) AB and BC  (C) C only  (D) A and B

**Q7.** Which set of rules is used to infer all functional dependencies implied by a given set?
(A) Codd's rules  (B) Armstrong's axioms  (C) De Morgan's laws  (D) ACID rules

**Q8.** In SQL, the clause used to filter **groups** produced by `GROUP BY` is
(A) `WHERE`  (B) `HAVING`  (C) `ORDER BY`  (D) `DISTINCT`

**Q9.** For a table with 10 rows in which the column `marks` contains 3 NULL values, `COUNT(*)` and `COUNT(marks)` return respectively
(A) 10 and 10  (B) 10 and 7  (C) 7 and 7  (D) 7 and 10

**Q10.** A **foreign key** enforces
(A) entity integrity  (B) referential integrity  (C) domain integrity  (D) user-defined integrity

**Q11.** An entity that cannot be uniquely identified by its own attributes alone and depends on an owner entity is called a
(A) strong entity  (B) weak entity  (C) composite entity  (D) derived entity

**Q12.** Which property of B+ trees makes them preferable to B-trees for database indexing?
(A) They have a smaller height for the same order
(B) All data pointers are in the leaves, which are linked, giving efficient range queries
(C) They store no keys in internal nodes
(D) They allow duplicate keys only

**Q13.** An index in which there is an entry for **every** search-key value in the data file is called
(A) sparse index  (B) dense index  (C) clustered index  (D) secondary index

**Q14.** The **ACID** properties of a transaction are
(A) Atomicity, Consistency, Isolation, Durability
(B) Atomicity, Concurrency, Integrity, Durability
(C) Accuracy, Consistency, Isolation, Dependability
(D) Atomicity, Consistency, Indexing, Durability

**Q15.** A schedule is **conflict serializable** if and only if its precedence (serialization) graph
(A) is connected  (B) is acyclic  (C) contains a cycle  (D) is complete

**Q16.** The Two-Phase Locking (2PL) protocol guarantees
(A) conflict serializability
(B) freedom from deadlock
(C) freedom from starvation
(D) recoverability in all cases

**Q17.** In **strict** 2PL, all exclusive locks held by a transaction are released
(A) as soon as they are no longer needed
(B) at the end of the growing phase
(C) only after the transaction commits or aborts
(D) at the start of the transaction

**Q18.** A decomposition of R into R1 and R2 is **lossless** if `R1 ∩ R2` is
(A) empty
(B) a superkey of at least one of R1 or R2
(C) a non-prime attribute
(D) equal to R

**Q19.** In the three-level DBMS architecture, the ability to change the internal (physical) schema without altering the conceptual schema is called
(A) logical data independence
(B) physical data independence
(C) schema abstraction
(D) view integration

**Q20.** Which SQL join returns **all** rows from the left table plus matching rows from the right table, with NULLs where no match exists?
(A) INNER JOIN  (B) LEFT OUTER JOIN  (C) RIGHT OUTER JOIN  (D) CROSS JOIN

---

## Part B — Paper-I (Q21–Q25)

**Q21.** Choose the correctly punctuated / grammatically correct sentence.
(A) Each of the students have submitted their assignment.
(B) Each of the students has submitted his assignment.
(C) Each of the student have submitted their assignment.
(D) Each of the student has submit his assignment.

**Q22.** The idiom *"a blessing in disguise"* means
(A) an obvious advantage
(B) something that seems bad at first but turns out to be good
(C) a hidden threat
(D) a religious ceremony

**Q23.** If `A` is the brother of `B`, `B` is the sister of `C`, and `C` is the father of `D`, then how is `A` related to `D`?
(A) Father  (B) Uncle  (C) Brother  (D) Grandfather

**Q24.** A train 150 m long crosses a pole in 15 seconds. Its speed is
(A) 10 km/h  (B) 24 km/h  (C) 36 km/h  (D) 45 km/h

**Q25.** The Tripura Sundari Temple, one of the 51 Shakti Peethas, is located at
(A) Agartala  (B) Udaipur  (C) Dharmanagar  (D) Kailashahar

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 6 | B | 11 | B | 16 | A | 21 | B |
| 2 | C | 7 | B | 12 | B | 17 | C | 22 | B |
| 3 | B | 8 | B | 13 | B | 18 | B | 23 | B |
| 4 | A | 9 | B | 14 | A | 19 | B | 24 | C |
| 5 | B | 10 | B | 15 | B | 20 | B | 25 | B |

---

**Q1 — (B).** **Degree** = number of attributes (columns); **cardinality** = number of tuples (rows). Reversing these two is the single most common slip in this topic.

**Q2 — (C).** The six primitives are σ, π, ×, ∪, − and ρ. Natural join, intersection and division are all **derived** (e.g. R ⋈ S = π(σ(R × S))).

**Q3 — (B).** The only candidate key is A, and it is a single attribute, so there can be no partial dependency → **2NF** holds. But B → C is a transitive dependency (B is not a superkey, C is non-prime) → 3NF **fails**.

**Q4 — (A).** BCNF: for every non-trivial X → Y, **X must be a superkey**. It is strictly stronger than 3NF.

**Q5 — (B).** 3NF permits X → Y with a non-superkey X *provided* Y is a **prime attribute** (part of some candidate key). BCNF removes that escape clause, which is why BCNF decomposition can lose dependency preservation.

**Q6 — (B).** (AB)⁺ = ABC → AB is a key. (BC)⁺: C → A gives A, so BC → ABC → **BC is also a key**. C alone gives only CA, not B. So candidate keys are **AB and BC**.

**Q7 — (B).** Armstrong's axioms — reflexivity, augmentation and transitivity — are sound and complete for deriving the closure F⁺. Union, decomposition and pseudo-transitivity are derived rules.

**Q8 — (B).** `WHERE` filters individual rows *before* grouping; **`HAVING`** filters groups *after* aggregation. Aggregate functions may appear in HAVING but not in WHERE.

**Q9 — (B).** `COUNT(*)` counts rows = **10**. `COUNT(marks)` ignores NULLs = **7**. NULL semantics are a reliable source of exam questions.

**Q10 — (B).** A foreign key must match an existing primary key value in the referenced relation (or be NULL) — **referential integrity**. Entity integrity is the rule that a primary key cannot be NULL.

**Q11 — (B).** A **weak entity** has only a partial key and requires its identifying (owner) entity's key. It is drawn with a double rectangle and connected by a double diamond.

**Q12 — (B).** In a B+ tree every record pointer sits in a leaf, and the leaves form a linked list — so a range query descends once and then scans sideways. Internal nodes hold only keys, so the fan-out is higher and the tree shallower.

**Q13 — (B).** A **dense** index has one entry per search-key value; a **sparse** index has entries only for some values (typically one per block) and requires sequential ordering.

**Q14 — (A).** Atomicity (all or nothing), Consistency (valid state to valid state), Isolation (concurrent execution equivalent to serial), Durability (committed changes survive failure).

**Q15 — (B).** Build a node per transaction and an edge Ti → Tj for each conflicting pair where Ti acts first. The schedule is conflict serializable **iff the graph is acyclic**; a topological sort then gives the equivalent serial order.

**Q16 — (A).** 2PL (growing phase acquires, shrinking phase releases, never mixed) guarantees **conflict serializability** — but **not** freedom from deadlock. Deadlocks must still be detected or prevented separately.

**Q17 — (C).** Strict 2PL holds all **exclusive** locks until commit/abort, which guarantees cascadeless recoverable schedules. Rigorous 2PL holds *all* locks (shared too) until commit.

**Q18 — (B).** The common attributes must functionally determine at least one of the two fragments — i.e. R1 ∩ R2 must be a superkey of R1 or of R2. Otherwise the natural join produces spurious tuples.

**Q19 — (B).** **Physical** data independence: change storage structures/indexes without touching the conceptual schema. **Logical** data independence (harder to achieve) is changing the conceptual schema without touching external views.

**Q20 — (B).** LEFT OUTER JOIN preserves all left-table rows, padding unmatched right-side columns with NULL.

**Q21 — (B).** *Each* is singular and takes a singular verb: "Each of the student**s** **has** submitted **his** assignment." Note "of the students" (plural noun after *of*) but "has" (singular verb agreeing with *each*).

**Q22 — (B).** *A blessing in disguise* = something that appears unfortunate at first but proves beneficial later.

**Q23 — (B).** A and B are siblings; B is C's sister, so A is also C's sibling (brother). D is C's child, so A is D's **uncle**.

**Q24 — (C).** Crossing a pole means covering its own length: 150 m in 15 s = 10 m/s. Convert: 10 × 18/5 = **36 km/h**.

**Q25 — (B).** The **Tripura Sundari Temple** (Matabari) is at **Udaipur** in Gomati district, about 55 km from Agartala. Built in 1501 by Maharaja Dhanya Manikya, it is counted among the 51 Shakti Peethas.

---

## Score

| | |
|---|---|
| Part A (Databases) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** missed Q3–Q7 → redo functional dependencies, attribute closure and normalisation (the highest-yield DBMS block — practise finding candidate keys until it is fast); missed Q8/Q9/Q20 → redo SQL semantics; missed Q12/Q13/Q18 → redo indexing and decomposition; missed Q14–Q17 → redo transactions and concurrency control. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S09_Databases/` (302 questions).
