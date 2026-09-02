# Week 7 — Databases

**Syllabus §9:** ER-model. Relational model: relational algebra, tuple calculus, SQL. Integrity constraints, normal forms. File organization, indexing (e.g. B and B+ trees). Transactions and concurrency control.
**Estimated marks: ~11**

---

## 1. Fundamentals

### 1.1 DBMS vs file system

| | File system | DBMS |
|---|---|---|
| Redundancy | High | Controlled |
| Consistency | Hard to enforce | Constraints enforced |
| Concurrency | Manual | Built-in control |
| Recovery | Manual | Log-based |
| Query capability | Program-specific | Declarative (SQL) |
| Security | File-level | Fine-grained |

### 1.2 ⭐ Three-level (ANSI/SPARC) architecture

| Level | Also called | Content |
|---|---|---|
| **External** | View level | What each user group sees; multiple views |
| **Conceptual** | Logical level | Whole-database logical structure; entities, relationships, constraints |
| **Internal** | Physical level | Storage structures, file organisation, indexes |

⭐ **Data independence:**
- ⭐ **Physical data independence** — change the **internal** schema (indexes, storage) without altering the conceptual schema. *Easier to achieve.*
- ⭐ **Logical data independence** — change the **conceptual** schema without altering external views. *Harder.*

**Schema** = the structure (definition, changes rarely). **Instance** = the actual data at a moment.
**Roles:** DBA (administration, security, tuning) · database designer · application programmer · end user.

**Data models:** hierarchical (tree) · network (graph) · **relational** (tables) · object-oriented · object-relational.

---

## 2. ⭐ ER model

### 2.1 Components

| Component | Symbol | Notes |
|---|---|---|
| **Strong entity** | Rectangle | Has its own key |
| ⭐ **Weak entity** | **Double** rectangle | ⭐ No key of its own; depends on an **identifying/owner** entity; has a **partial key** (dashed underline) |
| **Attribute** | Ellipse | |
| **Key attribute** | Underlined ellipse | |
| **Composite attribute** | Ellipse with sub-ellipses | e.g. Name → First, Last |
| **Multivalued attribute** | **Double** ellipse | e.g. PhoneNumbers |
| **Derived attribute** | **Dashed** ellipse | e.g. Age (from DOB) |
| **Relationship** | Diamond | |
| ⭐ **Identifying relationship** | **Double** diamond | Connects a weak entity to its owner |

### 2.2 ⭐ Cardinality and participation

**Cardinality ratios:** 1:1 · 1:N · N:1 · **M:N**
**Participation:** **total** (double line — every entity must participate, existence dependency) vs **partial** (single line).
**Degree of a relationship:** unary (recursive) · binary · ternary · n-ary.

### 2.3 ⭐ ER → relational mapping rules

| ER construct | Relational result |
|---|---|
| Strong entity | Its own table; key → primary key |
| ⭐ **Weak entity** | Own table with **(owner's PK + partial key)** as the composite primary key; owner's PK is also a foreign key |
| **1:1 relationship** | Add the FK to either side (prefer the side with **total** participation) — no separate table needed |
| **1:N relationship** | ⭐ Add the FK on the **N side** (the "many" side) — no separate table needed |
| ⭐ **M:N relationship** | ⭐ **A separate table** with both PKs as a composite key |
| **Multivalued attribute** | ⭐ **A separate table** (entity PK + the attribute) |
| Composite attribute | Flatten into its component columns |
| Derived attribute | Usually **not** stored |
| n-ary relationship (n ≥ 3) | A separate table with all participating PKs |

📌 ⭐ **Minimum number of tables:** two entities with a **1:N** or **1:1** relationship need only **2** tables; an **M:N** relationship needs **3**.

**Specialisation / generalisation:** IS-A hierarchies with disjoint/overlapping and total/partial constraints. **Aggregation** treats a relationship as a higher-level entity.

---

## 3. ⭐ Relational model

### 3.1 Terminology ⭐

| Term | Meaning |
|---|---|
| **Relation** | Table |
| **Tuple** | Row |
| **Attribute** | Column |
| ⭐ **Degree / arity** | ⭐ **Number of attributes (columns)** |
| ⭐ **Cardinality** | ⭐ **Number of tuples (rows)** |
| **Domain** | Set of permitted values for an attribute |

⚠ **Degree = columns, cardinality = rows.** Reversing these is the single most common slip in this topic.

🔢 R has 5 tuples and degree 3; S has 3 tuples and degree 2.
**R × S** has cardinality 5 × 3 = **15** and degree 3 + 2 = **5**.

### 3.2 ⭐ Keys

| Key | Definition |
|---|---|
| **Super key** | Any attribute set that uniquely identifies a tuple |
| ⭐ **Candidate key** | A **minimal** super key (no proper subset is a super key) |
| **Primary key** | The chosen candidate key; ⭐ **cannot be NULL** |
| **Alternate key** | Candidate keys not chosen as primary |
| ⭐ **Foreign key** | An attribute referencing another relation's primary key; ⭐ **may be NULL** |
| **Composite key** | A key of more than one attribute |
| **Prime attribute** | An attribute belonging to **some** candidate key |
| **Non-prime attribute** | Not part of any candidate key |

### 3.3 ⭐ Integrity constraints

| Constraint | Rule |
|---|---|
| **Domain integrity** | Values must come from the declared domain/type |
| ⭐ **Entity integrity** | ⭐ **The primary key cannot be NULL** (and must be unique) |
| ⭐ **Referential integrity** | ⭐ **A foreign key must match an existing PK value or be NULL** |
| Key constraint | Candidate key values are unique |

**On delete/update of a referenced tuple:** `CASCADE` · `SET NULL` · `SET DEFAULT` · `RESTRICT`/`NO ACTION`.

### 3.4 ⭐ Relational algebra

⭐ **Six fundamental (primitive) operations:**
📌 **σ (selection) · π (projection) · × (Cartesian product) · ∪ (union) · − (set difference) · ρ (rename)**

⭐ **Derived operations:** ⋈ (join, all kinds), ∩ (intersection), ÷ (division).
⚠ **Natural join, intersection and division are NOT primitive** — a very common question.

| Operation | Notation | Meaning |
|---|---|---|
| **Selection** | σ_condition(R) | Chooses **rows**; degree unchanged |
| **Projection** | π_attributes(R) | Chooses **columns**; ⭐ **removes duplicates** |
| **Cartesian product** | R × S | Every pair; degree = sum, cardinality = product |
| **Theta join** | R ⋈_θ S | σ_θ(R × S) |
| **Equi join** | R ⋈ S with `=` | Theta join using equality only |
| ⭐ **Natural join** | R ⋈ S | Equi-join on **all common attributes**, keeping one copy of each |
| **Left/right/full outer join** | ⟕ ⟖ ⟗ | Preserves unmatched tuples, padding with NULL |
| **Division** | R ÷ S | Tuples in R associated with **all** tuples of S ("for all" queries) |

⚠ ∪, ∩, − require **union-compatible** relations (same degree, corresponding domains).
⚠ Relational algebra is **set-based** (duplicates removed); SQL is **bag-based** (duplicates kept unless `DISTINCT`).

📌 **Cardinality bounds for a natural join:** 0 ≤ |R ⋈ S| ≤ |R| × |S|. If the join attribute is a **key of S and a foreign key in R**, then |R ⋈ S| = |R|.

**Relational calculus** (non-procedural, declarative):
- **Tuple relational calculus (TRC):** variables range over **tuples** — `{t | P(t)}`
- **Domain relational calculus (DRC):** variables range over **domain values**
- ⭐ Relational algebra, TRC and DRC (safe expressions) are **equivalent in expressive power** — this is *relational completeness*. Algebra is **procedural**; calculus is **declarative**.

---

## 4. ⭐⭐ SQL

### 4.1 Command categories ⭐

| Category | Commands | Note |
|---|---|---|
| ⭐ **DDL** (Definition) | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` | Auto-commit; structure |
| ⭐ **DML** (Manipulation) | `SELECT`, `INSERT`, `UPDATE`, `DELETE` | Data |
| **DCL** (Control) | `GRANT`, `REVOKE` | Privileges |
| **TCL** (Transaction) | `COMMIT`, `ROLLBACK`, `SAVEPOINT` | Transactions |

⭐ ⚠ **`DELETE` vs `TRUNCATE` vs `DROP`:**

| | `DELETE` | `TRUNCATE` | `DROP` |
|---|---|---|---|
| Type | DML | **DDL** | **DDL** |
| Removes | Selected rows (`WHERE`) | **All rows** | ⭐ **Rows + table structure** |
| `WHERE` clause | ✅ | ❌ | ❌ |
| Rollback-able | ✅ | ❌ (generally) | ❌ |
| Speed | Slow (row by row, logged) | Fast | Fast |
| Table remains | ✅ | ✅ | ❌ |

### 4.2 ⭐ Logical order of clause evaluation

📌 **FROM → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT**

⭐ This order explains two exam favourites:
- ⚠ **Aggregate functions cannot appear in `WHERE`** (aggregation has not happened yet) — use `HAVING`.
- ⚠ **Column aliases defined in `SELECT` cannot be used in `WHERE`**, but can be used in `ORDER BY`.

⭐ **`WHERE` filters rows; `HAVING` filters groups.**

### 4.3 ⭐ Aggregate functions and NULL

`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`

⭐⚠ **NULL handling — a guaranteed question area:**
- ⭐ **`COUNT(*)` counts all rows, including those with NULLs.**
- ⭐ **`COUNT(column)` ignores NULLs.**
- `SUM`, `AVG`, `MIN`, `MAX` **all ignore NULLs**. In particular `AVG` divides by the count of **non-NULL** values.
- ⭐ **NULL comparisons yield UNKNOWN**, not TRUE/FALSE — so `WHERE col = NULL` never matches. Use **`IS NULL`** / **`IS NOT NULL`**.
- `NULL + 5` = NULL; `NULL = NULL` is UNKNOWN.
- ⭐ **`GROUP BY` treats all NULLs as one group**; `DISTINCT` treats them as one value.

🔢 Table with 10 rows, `marks` has 3 NULLs:
`COUNT(*)` = **10** · `COUNT(marks)` = **7** · `AVG(marks)` = sum of the 7 non-NULL values ÷ **7**.

**Three-valued logic:** TRUE, FALSE, UNKNOWN. `NOT UNKNOWN` = UNKNOWN. Only rows evaluating to TRUE are returned.

### 4.4 ⭐ Joins

| Join | Returns |
|---|---|
| ⭐ **INNER JOIN** | Only matching rows |
| ⭐ **LEFT OUTER JOIN** | All left rows + matches; NULLs for unmatched right |
| **RIGHT OUTER JOIN** | All right rows + matches |
| **FULL OUTER JOIN** | All rows from both sides |
| **CROSS JOIN** | Cartesian product |
| **SELF JOIN** | A table joined with itself (needs aliases) |
| **NATURAL JOIN** | Auto-joins on all same-named columns |

### 4.5 Subqueries
- **Non-correlated:** inner query runs once, independent of the outer.
- ⭐ **Correlated:** inner query references the outer query's columns and re-executes per outer row (typically with `EXISTS`).
- Operators: `IN`, `NOT IN`, `ANY`/`SOME`, `ALL`, `EXISTS`, `NOT EXISTS`.
- ⚠ **`NOT IN` with a NULL in the subquery result returns no rows** (because `x <> NULL` is UNKNOWN). `NOT EXISTS` is safe. A classic trap.

### 4.6 Views
A stored query presented as a virtual table.
- Advantages: security (hide columns), simplification, logical independence.
- ⭐ **Updatability:** a view is generally **not updatable** if it contains `DISTINCT`, `GROUP BY`, aggregates, `UNION`, or a join of multiple tables.
- **Materialised view:** physically stored and refreshed — faster reads, potential staleness.

### 4.7 Other objects
**Index** (`CREATE INDEX`) · **Trigger** (procedural code fired automatically on INSERT/UPDATE/DELETE, `BEFORE`/`AFTER`, row- or statement-level) · **Stored procedure** · **Assertion** · **Cursor** · **Sequence**.

**Set operations:** `UNION` (removes duplicates) vs `UNION ALL` (keeps them) · `INTERSECT` · `EXCEPT`/`MINUS`.

---

## 5. ⭐⭐ Functional dependencies & normalization

### 5.1 Functional dependency

📌 **X → Y** means: any two tuples agreeing on X must agree on Y. ("X functionally determines Y.")

| Type | Description |
|---|---|
| **Trivial** | Y ⊆ X (e.g. AB → A) — always holds |
| **Non-trivial** | Y ⊄ X |
| ⭐ **Full** | X → Y and no proper subset of X determines Y |
| ⭐ **Partial** | A proper subset of X already determines Y |
| ⭐ **Transitive** | X → Y and Y → Z imply X → Z |

### 5.2 ⭐ Armstrong's axioms

📌 **Reflexivity:** if Y ⊆ X then X → Y
📌 **Augmentation:** if X → Y then XZ → YZ
📌 **Transitivity:** if X → Y and Y → Z then X → Z

⭐ These three are **sound and complete** — they derive exactly the closure F⁺.

**Derived rules:** Union (X→Y, X→Z ⇒ X→YZ) · Decomposition (X→YZ ⇒ X→Y, X→Z) · Pseudo-transitivity (X→Y, WY→Z ⇒ WX→Z).

### 5.3 ⭐⭐ Attribute closure & finding candidate keys

**Attribute closure X⁺:** all attributes functionally determined by X.
**Algorithm:** start with X⁺ = X; repeatedly, if some FD A → B has A ⊆ X⁺, add B; stop when nothing changes.

⭐ **X is a candidate key ⟺ X⁺ = all attributes, and no proper subset of X has that property.**

⭐ **Shortcut for finding candidate keys:**
1. Attributes that appear **only on the left** of all FDs (never on the right) **must be in every candidate key**.
2. Attributes appearing **only on the right** are never in any candidate key.
3. Attributes on **both sides or neither** may or may not be.
4. Start with the must-have set; compute its closure; if incomplete, add "maybe" attributes one at a time.

🔢 **R(A,B,C,D), FDs: A→B, B→C, C→D.**
A appears only on the left ⇒ A must be in every key. A⁺ = {A,B,C,D} = all ⇒ **A is the only candidate key.**

🔢 **R(A,B,C), FDs: AB→C, C→A.**
(AB)⁺ = ABC ⇒ AB is a key. (BC)⁺: C→A gives A, so BC → ABC ⇒ **BC is also a key**. C⁺ = CA (no B) ⇒ not a key.
⭐ **Candidate keys: AB and BC.** Prime attributes: A, B, C (all of them).

**Canonical / minimal cover:** an equivalent FD set with (a) a single attribute on each right side, (b) no redundant FD, (c) no redundant attribute on any left side.

### 5.4 ⭐⭐ Normal forms

| NF | ⭐ Condition | Removes |
|---|---|---|
| **1NF** | All attributes **atomic** (no multivalued or composite attributes) | Repeating groups |
| ⭐ **2NF** | In 1NF **and** no **partial dependency** — no non-prime attribute depends on part of a candidate key | Partial dependencies |
| ⭐ **3NF** | In 2NF **and** no **transitive dependency** — for every non-trivial X→Y, either **X is a super key** OR **Y is a prime attribute** | Transitive dependencies |
| ⭐ **BCNF** | For every non-trivial X→Y, ⭐ **X must be a super key** | All FD-based redundancy |
| **4NF** | In BCNF and no non-trivial **multivalued dependency (MVD)** unless the determinant is a super key | MVDs |
| **5NF / PJNF** | No non-trivial **join dependency** | Join dependencies |

⭐ **Key insight — 3NF vs BCNF:** 3NF has an escape clause. It allows X→Y with a non-super-key X **provided Y is a prime attribute**. BCNF removes that allowance. Every BCNF relation is in 3NF, but not vice versa.

⭐ **A relation whose every candidate key is a single attribute is automatically in 2NF** (there is no partial key to depend on).
⭐ **A relation with only two attributes is always in BCNF.**

🔢 **R(A,B,C,D) with A→B, B→C, C→D.** Candidate key = A.
- 1NF ✅ · 2NF ✅ (single-attribute key ⇒ no partial dependency)
- 3NF ❌ — B→C where B is not a super key and C is non-prime (only A is prime)
- ⭐ **Highest normal form = 2NF**

🔢 **R(A,B,C) with AB→C, C→A.** Candidate keys AB, BC. Prime = {A,B,C}.
- 2NF: check AB→C (full, fine); C→A — C is part of candidate key BC, and A is prime. No non-prime attribute at all (all three are prime) ⇒ **3NF ✅**
- BCNF ❌ — C→A but C is **not** a super key
- ⭐ **Highest normal form = 3NF**

### 5.5 ⭐ Decomposition

📌 ⭐ **Lossless join:** decomposing R into R1 and R2 is lossless ⟺ **R1 ∩ R2 → R1** or **R1 ∩ R2 → R2**, i.e. the common attributes form a **super key of at least one fragment**.

⚠ If not lossless, the natural join produces **spurious tuples**.

**Dependency preservation:** the union of the FDs projected onto the fragments must be equivalent to the original F.

⭐ **The crucial trade-off:**

| Target | Lossless join | Dependency preserving |
|---|---|---|
| **3NF** | ⭐ **Always achievable** | ⭐ **Always achievable** |
| **BCNF** | ⭐ **Always achievable** | ⭐ **NOT always achievable** |

⭐ **A lossless, dependency-preserving decomposition into BCNF may not exist** — this is the reason 3NF is often the practical stopping point.

---

## 6. ⭐ File organization & indexing

### 6.1 File organisation

| Organisation | Description |
|---|---|
| **Heap (unordered)** | Records appended anywhere; insert O(1), search O(n) |
| **Sequential (ordered)** | Sorted on a key; binary search possible; insertion costly |
| **Hash** | Direct access by hash of the key; poor for range queries |
| **Clustered** | Related records physically together |
| **ISAM / B+ tree** | Indexed sequential |

### 6.2 ⭐ Index types

| Classification | Types |
|---|---|
| By density | ⭐ **Dense** (an entry for **every** search-key value) vs **Sparse** (entries for some values; requires the file to be ordered) |
| By level | Single-level vs **multi-level** |
| By key | ⭐ **Primary** (on the ordering key — at most one) vs **Secondary** (on a non-ordering field — many possible; ⭐ **must be dense**) |
| By clustering | ⭐ **Clustered** (physical order matches index order — at most **one** per table) vs **Non-clustered** |

⚠ A **sparse index can only be primary/clustered** — you cannot skip entries on an unordered field.

📌 **Blocking factor** = ⌊block size / record size⌋
📌 **Number of blocks** = ⌈number of records / blocking factor⌉

### 6.3 ⭐⭐ B-trees and B+ trees

**B-tree of order m (max m children):**
- Every node has at most m children and at most m − 1 keys.
- Non-root internal nodes have at least ⌈m/2⌉ children.
- All leaves at the **same level** (perfectly height-balanced).
- ⭐ **Keys AND data pointers appear in every node.**

**B+ tree of order m:**
- ⭐ **All data pointers are in the leaves only**; internal nodes hold keys purely for routing (and keys may be duplicated in leaves).
- ⭐ **Leaves are linked in a sorted doubly linked list.**

⭐ **Why B+ trees for database indexing:**

| | B-tree | ⭐ **B+ tree** |
|---|---|---|
| Data pointers | In all nodes | ⭐ **Leaves only** |
| Leaves linked | ❌ | ⭐ **✅ → efficient range queries** |
| Internal node fan-out | Lower (nodes carry data) | ⭐ **Higher → shallower tree → fewer disk I/Os** |
| Search path length | Varies (may end early) | Always to a leaf (predictable) |
| Redundant keys | ❌ | ✅ (keys repeat in leaves) |

📌 For a B+ tree of order p with key size K, pointer size P and block size B:
**p × P + (p − 1) × K ≤ B** (internal node)
**Leaf order p_leaf:** p_leaf × (K + record pointer) + P_next ≤ B

🔢 Block = 1024 B, key = 9 B, block pointer = 6 B:
Internal: p×6 + (p−1)×9 ≤ 1024 → 15p ≤ 1033 → p = **68**.

📌 Height of a B+ tree with n keys and order p ≈ **log_⌈p/2⌉(n)** — logarithmic in n, which is why lookups cost only a few disk reads.

**Operations:** insertion may cause a **split** propagating upward (height grows only at the root); deletion may cause **merge/borrow** from siblings.

---

## 7. ⭐⭐ Transactions and concurrency control

### 7.1 ⭐ ACID properties

| Property | Meaning | Ensured by |
|---|---|---|
| ⭐ **Atomicity** | All operations complete, or none do ("all or nothing") | Recovery manager / logging |
| ⭐ **Consistency** | Takes the DB from one valid state to another | Integrity constraints + application logic |
| ⭐ **Isolation** | Concurrent execution appears serial | Concurrency-control manager |
| ⭐ **Durability** | Committed changes survive failures | Logging + stable storage |

⚠ Do not confuse with the OS critical-section requirements (mutual exclusion, progress, bounded waiting).

**Transaction states:** Active → Partially Committed → **Committed**, or Active → Failed → **Aborted** (rolled back).
**Operations:** `read(X)`, `write(X)`, `commit`, `abort`.

### 7.2 ⭐ Concurrency problems

| Problem | Description |
|---|---|
| ⭐ **Lost update** (write–write) | Two transactions write X; one update is overwritten and lost |
| ⭐ **Dirty read** (write–read) | T2 reads an **uncommitted** value written by T1, which then aborts |
| ⭐ **Unrepeatable read** (read–write) | T1 reads X twice and gets different values because T2 wrote in between |
| **Phantom read** | T1 re-runs a range query and sees new rows inserted by T2 |
| **Incorrect summary** | An aggregate reads some values before and some after another transaction's updates |

### 7.3 ⭐⭐ Serializability

**Schedule:** an interleaving of operations from multiple transactions.
**Serial schedule:** transactions run one after another — always correct, but no concurrency.

⭐ **Two operations conflict** iff they belong to **different** transactions, access the **same** data item, and **at least one is a write**. (read–read never conflicts.)

⭐ **Conflict serializability test — the precedence (serialization) graph:**
1. One node per transaction.
2. For each pair of conflicting operations where Tᵢ's comes first, draw an edge **Tᵢ → Tⱼ**.
3. ⭐ **The schedule is conflict serializable ⟺ the graph is ACYCLIC.**
4. A **topological sort** of the graph gives the equivalent serial order.

⭐ **View serializability** is weaker (more permissive) than conflict serializability:
📌 **Conflict serializable ⊂ View serializable ⊂ All schedules**
Every conflict-serializable schedule is view serializable, but not conversely. (View serializability is NP-hard to test, so practical systems use conflict serializability.)

### 7.4 ⭐ Recoverability

| Schedule class | Condition |
|---|---|
| ⭐ **Recoverable** | If Tⱼ reads a value written by Tᵢ, then Tⱼ commits **after** Tᵢ commits |
| ⭐ **Cascadeless (ACA)** | A transaction reads only **committed** values → no cascading rollback |
| **Strict** | No transaction reads **or writes** an uncommitted value |

📌 **Strict ⊂ Cascadeless ⊂ Recoverable ⊂ All schedules**
⭐ **Irrecoverable schedules must be avoided at all costs**; cascading rollback is merely expensive.

### 7.5 ⭐⭐ Locking protocols

**Lock modes:** **shared (S)** for reading, **exclusive (X)** for writing.

⭐ **Lock compatibility matrix:**

| Held ↓ / Requested → | S | X |
|---|---|---|
| **S** | ✅ | ❌ |
| **X** | ❌ | ❌ |

⭐ **Two-Phase Locking (2PL):** every transaction has a **growing phase** (acquires locks, releases none) then a **shrinking phase** (releases locks, acquires none).

📌 ⭐ **2PL guarantees conflict serializability but NOT freedom from deadlock.**

| Variant | Releases locks |
|---|---|
| **Basic 2PL** | Any time in the shrinking phase |
| **Conservative 2PL** | Acquires **all** locks before starting → ⭐ **deadlock-free**, but not strict |
| ⭐ **Strict 2PL** | Holds all **exclusive** locks until commit/abort → cascadeless |
| **Rigorous 2PL** | Holds **all** locks (S and X) until commit/abort → strict |

⚠ **Conservative 2PL is the deadlock-free one; strict 2PL is the recoverable one.** Both are commonly asked.

⭐ **Timestamp ordering (non-locking):** each transaction gets a timestamp TS(T); each item keeps `read_TS` and `write_TS`. Operations violating timestamp order are rejected and the transaction is restarted. **Deadlock-free** (no waiting) but can cause **starvation** through repeated restarts.
- **Thomas's write rule:** an obsolete write can simply be ignored, allowing more schedules.

**Multiversion concurrency control (MVCC):** keep multiple versions so readers never block writers. Used by PostgreSQL and Oracle.
**Optimistic concurrency control:** three phases — read, validate, write.

**Deadlock in DBMS:** detected with a **wait-for graph** (a cycle ⇒ deadlock). Prevention via **wait-die** (older waits, younger dies) and **wound-wait** (older wounds/preempts younger, younger waits) — both use timestamps and are deadlock-free.

### 7.6 ⭐ Isolation levels (SQL standard)

| Level | Dirty read | Unrepeatable read | Phantom read |
|---|---|---|---|
| **Read Uncommitted** | ✅ possible | ✅ | ✅ |
| **Read Committed** | ❌ | ✅ | ✅ |
| **Repeatable Read** | ❌ | ❌ | ✅ |
| ⭐ **Serializable** | ❌ | ❌ | ❌ |

### 7.7 Recovery

**Log record:** `<Tᵢ, X, old_value, new_value>`

| Technique | Behaviour |
|---|---|
| **Deferred update (NO-UNDO/REDO)** | Writes applied to the DB only after commit → only **redo** needed |
| ⭐ **Immediate update (UNDO/REDO)** | Writes applied as they occur → both **undo** and **redo** needed |

⭐ **Write-Ahead Logging (WAL):** the log record must reach stable storage **before** the corresponding data page. This is what makes recovery possible.

**Checkpoint:** flush logs and dirty buffers, write a checkpoint record → limits how far back recovery must scan.
**ARIES recovery:** three passes — **Analysis → Redo → Undo**.

**Shadow paging:** a no-log alternative using a shadow page table; simple but poor for concurrency.

---

## 8. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| Degree / cardinality | Columns / rows |
| Primitive relational algebra ops | σ, π, ×, ∪, −, ρ |
| Natural join | Derived, not primitive |
| Projection | Removes duplicates |
| M:N relationship tables | 3 |
| 1:N relationship FK goes on | The N side |
| Weak entity PK | Owner PK + partial key |
| PK cannot be | NULL |
| FK enforces | Referential integrity |
| COUNT(*) vs COUNT(col) | Includes / ignores NULLs |
| `WHERE col = NULL` | Never matches — use `IS NULL` |
| Filters groups | HAVING |
| Removes table structure | DROP |
| TRUNCATE type | DDL |
| Armstrong's axioms | Reflexivity, augmentation, transitivity |
| 2NF removes | Partial dependencies |
| 3NF removes | Transitive dependencies |
| BCNF requires | Every determinant is a super key |
| 3NF allows X→Y if | Y is a prime attribute |
| Single-attribute candidate key ⇒ | Automatically 2NF |
| Two-attribute relation ⇒ | Always BCNF |
| Lossless join condition | R1∩R2 is a super key of R1 or R2 |
| BCNF may sacrifice | Dependency preservation |
| Conflict serializable ⟺ | Precedence graph acyclic |
| Conflict ⊂ View | Conflict serializable ⊂ view serializable |
| 2PL guarantees | Conflict serializability (not deadlock freedom) |
| Deadlock-free 2PL variant | Conservative 2PL |
| Cascadeless 2PL variant | Strict 2PL |
| B+ tree data pointers | Leaves only |
| B+ tree leaves | Linked (range queries) |
| Clustered indexes per table | At most 1 |
| Secondary index must be | Dense |
| WAL rule | Log before data |
| Highest isolation level | Serializable |

---

## 9. Common traps ⚠

1. **Degree = columns, cardinality = rows.**
2. **Natural join is not a primitive** relational algebra operation.
3. **`COUNT(*)` includes NULL rows; `COUNT(col)` does not.**
4. **`= NULL` never matches** — and `NOT IN` with NULLs returns nothing.
5. **3NF vs BCNF** — 3NF's prime-attribute escape clause is the entire difference.
6. **A single-attribute candidate key means 2NF is automatic.**
7. **BCNF cannot always be dependency preserving**; 3NF always can.
8. **2PL does not prevent deadlock.**
9. **Conservative 2PL (deadlock-free) vs strict 2PL (cascadeless)** — do not swap.
10. **Read–read is never a conflict.**
11. **B-tree stores data in all nodes; B+ tree only in leaves.**
12. **DELETE is DML and rollback-able; TRUNCATE and DROP are DDL.**
13. **Aggregates cannot go in `WHERE`.**
14. **Unsafe to assume a cycle-free wait-for graph means serializable** — the *precedence* graph tests serializability; the *wait-for* graph tests deadlock. Different graphs.

---

## 10. Practice

- GATE: [`Paper2_S09_Databases/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S09_Databases/) — **302 questions**
- State-PSC level: [`Paper2_S09_Databases/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S09_Databases/) — **390 questions** (includes data mining & warehousing)
- Test: [`Week_07_Test.md`](../04_Mock_Tests/Week_07_Test.md)

**Priority order if short on time:** finding candidate keys via attribute closure → normal forms (especially 3NF vs BCNF) → conflict serializability via precedence graphs → SQL NULL/aggregate semantics → B+ tree properties and order calculation → 2PL variants → ER-to-relational mapping.
