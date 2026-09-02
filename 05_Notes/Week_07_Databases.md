# Week 7 — Databases

**Syllabus §9:** ER-model. Relational model: relational algebra, tuple calculus, SQL. Integrity constraints, normal forms. File organization, indexing (e.g. B and B+ trees). Transactions and concurrency control.
**Estimated marks: ~11**

---

## 💡 What this subject is about

Suppose you store student records in a text file. Problems appear immediately:
- The same student's address is written in three places, and two are out of date (**redundancy and inconsistency**)
- Two clerks edit the file simultaneously and one change vanishes (**no concurrency control**)
- The power fails mid-update, leaving half a record (**no atomicity**)
- Every new query needs a new program written (**no query capability**)
- Anyone who can read the file sees the salaries (**no fine-grained security**)

A **DBMS** solves all of these. This file follows the solutions:
1. **ER model** → how to *design* the data structure
2. **Relational model & SQL** → how to *store and query* it
3. **Normalization** → how to eliminate redundancy
4. **Indexing** → how to make queries fast
5. **Transactions & concurrency control** → how to stay correct under concurrent access and failure

---

# 1. Fundamentals

## 1.1 DBMS vs file system

| | File system | ⭐ DBMS |
|---|---|---|
| Redundancy | High | Controlled |
| Consistency | Programmer's responsibility | Enforced by **constraints** |
| Concurrency | Manual/none | Built-in control |
| Recovery | Manual | **Log-based**, automatic |
| Query capability | Write a program per query | **Declarative** (SQL) |
| Security | File-level only | Row/column-level |
| Data independence | None | Physical and logical |

## 1.2 ⭐ The three-level architecture

### 💡 The idea

A DBMS deliberately separates *what the user sees*, *what the data logically is*, and *how it is physically stored* — so each can change without disturbing the others.

```
┌──────────────────────────────────────────┐
│  EXTERNAL LEVEL (views)                  │  What each user group sees.
│  Student view │ Accounts view │ ...      │  Many views per database.
└──────────────────────────────────────────┘
                    ↕  logical data independence
┌──────────────────────────────────────────┐
│  CONCEPTUAL / LOGICAL LEVEL              │  All entities, relationships,
│  The whole database's logical structure  │  constraints. One per database.
└──────────────────────────────────────────┘
                    ↕  physical data independence
┌──────────────────────────────────────────┐
│  INTERNAL / PHYSICAL LEVEL               │  Files, indexes, storage
│  How bytes are actually stored           │  structures.
└──────────────────────────────────────────┘
```

⭐⭐ **Data independence — the payoff:**

📌 ⭐ **Physical data independence** — you can change the **internal** schema (add an index, switch storage engine, reorganise files) **without altering the conceptual schema** or any application. ⭐ *Easier to achieve, and routinely used.*

📌 ⭐ **Logical data independence** — you can change the **conceptual** schema (add a column, split a table) **without altering the external views**. ⭐ *Harder, because views are defined in terms of the conceptual schema.*

🔢 Creating an index to speed up a query changes nothing about your SQL → **physical** data independence at work.

**Schema vs instance:** the **schema** is the structure (changes rarely — like a class definition). The **instance** is the actual data at a given moment (changes constantly — like an object).

**Roles:** DBA (administration, security, tuning, backup) · database designer · application programmer · end user.

**Data models:** hierarchical (tree) · network (graph) · ⭐ **relational** (tables — the dominant model) · object-oriented · object-relational · NoSQL (document, key-value, column, graph).

---

# 2. ⭐⭐ ER model

## 💡 The idea

Before you create any tables, you must decide **what things exist** and **how they relate**. The **Entity-Relationship model** (Chen, 1976) is a diagramming notation for exactly that — a design tool, not a storage format.

Three basic building blocks:
- **Entity** — a real-world thing you store data about (a Student, a Course)
- **Attribute** — a property of an entity (name, roll number)
- **Relationship** — an association between entities (a Student *enrols in* a Course)

## 2.1 ⭐ The notation

| Component | Symbol | 💡 Note |
|---|---|---|
| **Strong entity** | Rectangle | Has its own key |
| ⭐ **Weak entity** | ⭐ **DOUBLE rectangle** | ⭐ Cannot be identified by its own attributes alone |
| **Attribute** | Ellipse | |
| **Key attribute** | Ellipse with the name **underlined** | |
| **Composite attribute** | Ellipse with sub-ellipses | e.g. `Name` → `First`, `Last` |
| ⭐ **Multivalued attribute** | ⭐ **DOUBLE ellipse** | e.g. `PhoneNumbers` — a person may have several |
| ⭐ **Derived attribute** | ⭐ **DASHED ellipse** | e.g. `Age`, computed from `DateOfBirth` — usually not stored |
| **Relationship** | Diamond | |
| ⭐ **Identifying relationship** | ⭐ **DOUBLE diamond** | Connects a weak entity to its owner |

## 2.2 ⭐ Weak entities

### 💡 The idea

Consider `Dependent` (the family members of an employee, for insurance purposes). Two different employees may each have a son called "Rahul, aged 10". So `(name, age)` does not uniquely identify a dependent.

⭐ A **weak entity** has only a **partial key** (shown with a **dashed** underline) and needs its **owner/identifying entity's** key to be uniquely identified.

📌 ⭐ **A weak entity's primary key = (owner's primary key + its own partial key).**

🔢 `Dependent(EmployeeID, DependentName, Relationship)` with primary key **(EmployeeID, DependentName)**, where `EmployeeID` is also a **foreign key** to `Employee`.

⭐ A weak entity always has **total participation** in its identifying relationship — it cannot exist without its owner.

## 2.3 ⭐ Cardinality and participation

**Cardinality ratio** — how many of each side may participate:

| Ratio | 🔢 Example |
|---|---|
| **1:1** | One person has one passport |
| **1:N** | One department has many employees |
| **N:1** | Many employees belong to one department |
| ⭐ **M:N** | Many students take many courses |

**Participation constraint:**
- ⭐ **Total** (drawn as a **double line**) — **every** entity of that type must participate. This is an **existence dependency**.
- **Partial** (single line) — participation is optional.

🔢 "Every employee must be assigned to a department" → Employee has **total** participation. "A department may have no employees" → Department has **partial** participation.

**Degree of a relationship:** unary/recursive (an Employee *manages* another Employee) · **binary** (most common) · ternary · n-ary.

## 2.4 ⭐⭐ ER → relational mapping

### 💡 The idea

ER diagrams must eventually become tables. The mapping rules are mechanical — and one of them is asked constantly.

| ER construct | ⭐ Relational result |
|---|---|
| **Strong entity** | Its own table; its key becomes the primary key |
| ⭐ **Weak entity** | Own table with **(owner's PK + partial key)** as a composite primary key; owner's PK is also a foreign key |
| **Multivalued attribute** | ⭐ **A SEPARATE table** (entity's PK + the attribute) |
| **Composite attribute** | Flattened into its component columns |
| **Derived attribute** | Usually **not stored** |
| **1:1 relationship** | ⭐ **No separate table** — add a foreign key to either side (prefer the side with **total** participation) |
| ⭐ **1:N relationship** | ⭐ **No separate table** — put the foreign key on the ⭐ **"N" (many) side** |
| ⭐ **M:N relationship** | ⭐ **A SEPARATE table** with both PKs forming a composite key |
| n-ary relationship (n ≥ 3) | A separate table with all participating PKs |

### 💡 Why the FK goes on the "N" side of a 1:N

One department has many employees. If you put a "list of employees" in the Department table, you would need a multivalued attribute (not allowed in 1NF). But each employee has exactly **one** department, so a single `DeptID` column in the Employee table works perfectly.

⭐ **The rule generalises: the foreign key always goes on the side that has at most ONE partner.**

### 🔢 The minimum-tables question

📌 ⭐ **Two entities with a 1:1 or 1:N relationship need only 2 tables. An M:N relationship needs 3.**

🔢 `Student` and `Course` with an M:N "enrols" relationship →
`Student(RollNo, Name)`, `Course(CourseID, Title)`, `Enrols(RollNo, CourseID, Grade)` = ⭐ **3 tables**

🔢 `Department` and `Employee` with a 1:N relationship →
`Department(DeptID, Name)`, `Employee(EmpID, Name, DeptID)` = ⭐ **2 tables**

## 2.5 Extended ER features

**Specialisation/generalisation** — IS-A hierarchies (a `Vehicle` specialises into `Car` and `Truck`), with **disjoint vs overlapping** and **total vs partial** constraints.
**Aggregation** — treating a whole relationship as a higher-level entity, so another relationship can refer to it.

---

# 3. ⭐⭐ Relational model

## 3.1 ⭐ Terminology

### 💡 The idea

The relational model (Codd, 1970) represents everything as **tables** — mathematically, **relations**, which are sets of tuples.

```
              ← attributes / columns →
          ┌─────────┬──────────┬────────┐
          │ RollNo  │  Name    │ Marks  │
          ├─────────┼──────────┼────────┤
  tuples  │  101    │  Amit    │   80   │
   rows   │  102    │  Beena   │   75   │
     ↓    │  103    │  Chetan  │   90   │
          └─────────┴──────────┴────────┘
```

| Term | Formal name |
|---|---|
| Table | **Relation** |
| Row | **Tuple** |
| Column | **Attribute** |
| ⭐ **Number of COLUMNS** | ⭐ **DEGREE (or arity)** |
| ⭐ **Number of ROWS** | ⭐ **CARDINALITY** |
| Set of allowed values | **Domain** |

⚠⚠ ⭐ **Degree = COLUMNS. Cardinality = ROWS.** Reversing them is the single most common error in this topic.

**Memory hook:** a **card**inality counts the **card**s (rows) in the deck. Degree, like a polynomial's degree, counts the *dimensions* (columns).

🔢 R has 5 tuples and degree 3; S has 3 tuples and degree 2.
**R × S** (Cartesian product) has:
- ⭐ **Cardinality = 5 × 3 = 15** (every pair)
- ⭐ **Degree = 3 + 2 = 5** (all columns side by side)

## 3.2 ⭐⭐ Keys

### 💡 Building up the definitions

Start with the goal: **uniquely identify a row.**

- **Super key** — *any* set of attributes that uniquely identifies a tuple. `{RollNo}` works; so does `{RollNo, Name}`; so does `{RollNo, Name, Marks}`. Super keys can be wastefully large.
- ⭐ **Candidate key** — a **MINIMAL** super key: remove any attribute and it stops being unique. `{RollNo}` is a candidate key; `{RollNo, Name}` is not (it contains a smaller super key).
- **Primary key** — the candidate key the designer **chooses** as the official identifier. ⭐ **Cannot be NULL.**
- **Alternate key** — the candidate keys that were not chosen.
- ⭐ **Foreign key** — an attribute referencing another relation's primary key. ⭐ **MAY be NULL** (meaning "no relationship yet").
- **Composite key** — a key made of more than one attribute.
- ⭐ **Prime attribute** — an attribute that is part of **some** candidate key.
- ⭐ **Non-prime attribute** — part of **no** candidate key.

⚠ ⭐ **Prime/non-prime matters enormously for normalization (§5)** — the difference between 3NF and BCNF hinges on it.

## 3.3 ⭐ Integrity constraints

### 💡 The idea

Constraints are rules the DBMS **enforces automatically**, so bad data can never enter — regardless of which application inserts it.

| Constraint | ⭐ Rule |
|---|---|
| **Domain integrity** | Values must come from the declared domain/type |
| ⭐ **Entity integrity** | ⭐ **The primary key cannot be NULL** (and must be unique) |
| ⭐ **Referential integrity** | ⭐ **A foreign key value must MATCH an existing primary key value, or be NULL** |
| **Key constraint** | Candidate key values are unique |

💡 **Why entity integrity forbids NULL:** NULL means "unknown". If a primary key could be unknown, the row could not be identified — defeating the key's whole purpose.

💡 **Why referential integrity matters:** without it you get **orphan rows** — an Enrolment referring to a Student who does not exist.

⭐ **When a referenced row is deleted or updated, options are:**
- `CASCADE` — delete/update the referencing rows too
- `SET NULL` — set the foreign key to NULL
- `SET DEFAULT`
- `RESTRICT` / `NO ACTION` — refuse the operation

## 3.4 ⭐⭐ Relational algebra

### 💡 The idea

**Relational algebra** is a formal, **procedural** language: a set of operators that take relations and produce relations. SQL is its practical descendant, and query optimisers work in relational algebra internally.

⭐⭐ **The SIX fundamental (primitive) operations:**

📌 ⭐ **σ (selection) · π (projection) · × (Cartesian product) · ∪ (union) · − (set difference) · ρ (rename)**

⚠⚠ ⭐ **Natural join (⋈), intersection (∩) and division (÷) are DERIVED, not primitive.** This is a very common question.

💡 **Why they are derived:**
- `R ∩ S = R − (R − S)` — expressible with difference alone
- `R ⋈ S = π(σ(R × S))` — a join is a product followed by a selection and a projection

### ⭐ The operators

| Operation | Notation | 💡 What it does |
|---|---|---|
| **Selection** | σ_condition(R) | Picks **ROWS** satisfying the condition. Degree unchanged, cardinality shrinks |
| **Projection** | π_attributes(R) | Picks **COLUMNS**. ⭐ **Removes duplicate rows** (a relation is a set) |
| **Cartesian product** | R × S | Every row of R paired with every row of S |
| **Theta join** | R ⋈_θ S | σ_θ(R × S) — a product filtered by any condition |
| **Equi join** | R ⋈ S with `=` | Theta join using only equality |
| ⭐ **Natural join** | R ⋈ S | Equi-join on **all common attributes**, keeping **one copy** of each |
| **Left/right/full outer join** | ⟕ ⟖ ⟗ | Preserves unmatched tuples, padding with NULL |
| **Division** | R ÷ S | Tuples of R associated with **ALL** tuples of S — answers **"for all"** queries |

🔢 **Division example:** "Find students who have taken **every** course." `Enrolled(student, course) ÷ Course(course)`.

⚠ ⭐ **Union, intersection and difference require UNION-COMPATIBLE relations** — same degree, and corresponding attributes drawn from the same domains.

⚠⚠ ⭐ **Relational algebra is SET-based (duplicates automatically removed); SQL is BAG-based (duplicates kept unless you write `DISTINCT`).** This is why `π_Name(Student)` in algebra removes duplicate names but `SELECT Name FROM Student` does not.

### ⭐ Join cardinality bounds

📌 **0 ≤ |R ⋈ S| ≤ |R| × |S|**
- **0** if no rows match at all
- **|R| × |S|** if the join attribute has the same single value in every row of both
- ⭐ **Exactly |R|** if the join attribute is a **key of S** and a **foreign key in R** (with no NULLs) — because each R-row matches exactly one S-row. *This is the most commonly asked case.*

## 3.5 Relational calculus

**Declarative** (says *what* you want, not *how*) rather than procedural:
- **Tuple relational calculus (TRC)** — variables range over **tuples**: `{t | Student(t) ∧ t.Marks > 80}`
- **Domain relational calculus (DRC)** — variables range over **domain values**

📌 ⭐ **Relational algebra, TRC and DRC (restricted to safe expressions) are EQUIVALENT in expressive power.** This is called **relational completeness**, and any language achieving it is "relationally complete".

⭐ **Algebra is PROCEDURAL; calculus is DECLARATIVE. SQL is closer to calculus in style but is implemented via algebra.**

---

# 4. ⭐⭐⭐ SQL

## 4.1 ⭐ The four command categories

| Category | Commands | 💡 Note |
|---|---|---|
| ⭐ **DDL** — Data Definition | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` | Defines **structure**. ⭐ **Auto-commits** |
| ⭐ **DML** — Data Manipulation | `SELECT`, `INSERT`, `UPDATE`, `DELETE` | Manipulates **data** |
| **DCL** — Data Control | `GRANT`, `REVOKE` | Privileges |
| **TCL** — Transaction Control | `COMMIT`, `ROLLBACK`, `SAVEPOINT` | Transactions |

*(Some texts classify `SELECT` separately as DQL — Data Query Language.)*

## 4.2 ⭐⭐ DELETE vs TRUNCATE vs DROP

### 💡 The idea — three different amounts of destruction

- **`DELETE`** removes **rows you choose**, logs each one, and can be rolled back. The table remains.
- **`TRUNCATE`** removes **all rows** in one fast operation by deallocating pages. The table structure remains.
- **`DROP`** removes the **rows AND the table itself**.

| | `DELETE` | `TRUNCATE` | `DROP` |
|---|---|---|---|
| Type | **DML** | ⭐ **DDL** | ⭐ **DDL** |
| Removes | Selected rows | **All rows** | ⭐ **Rows + STRUCTURE** |
| `WHERE` clause | ✅ | ❌ | ❌ |
| Rollback-able | ✅ | ❌ (generally) | ❌ |
| Speed | Slow (row by row, logged) | ⭐ **Fast** | Fast |
| Table survives | ✅ | ✅ | ⭐ **❌** |
| Resets identity/auto-increment | ❌ | ✅ | n/a |

## 4.3 ⭐⭐ The logical order of clause evaluation

📌 ⭐ **FROM → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT**

⭐ **This order explains two exam favourites:**

⚠ ⭐ **1. Aggregate functions cannot appear in `WHERE`.** `WHERE` runs *before* grouping, so at that point no groups (and therefore no aggregates) exist yet. Use `HAVING`.
```sql
-- ❌ WRONG
SELECT dept, AVG(sal) FROM emp WHERE AVG(sal) > 50000 GROUP BY dept;
-- ✅ RIGHT
SELECT dept, AVG(sal) FROM emp GROUP BY dept HAVING AVG(sal) > 50000;
```

⚠ ⭐ **2. Column aliases defined in `SELECT` cannot be used in `WHERE`** (SELECT runs later) — but **can** be used in `ORDER BY` (which runs after SELECT).

📌 ⭐ **`WHERE` filters ROWS (before grouping); `HAVING` filters GROUPS (after aggregation).**

## 4.4 ⭐⭐⭐ NULL and aggregate semantics

### 💡 What NULL means

⭐ **NULL is not zero and not an empty string — it means "UNKNOWN" or "not applicable".** This gives SQL a **three-valued logic**: TRUE, FALSE, **UNKNOWN**.

⭐ **Consequences, all of which get asked:**

📌 ⭐ **Any comparison with NULL yields UNKNOWN**, not TRUE or FALSE.
```sql
WHERE marks = NULL     -- ⭐ NEVER matches anything, even NULL rows!
WHERE marks IS NULL    -- ⭐ THE CORRECT WAY
```
💡 **Why:** "is this unknown value equal to that unknown value?" is itself unknown. Only rows evaluating to **TRUE** are returned, so UNKNOWN rows are dropped.

📌 Arithmetic with NULL gives NULL: `NULL + 5 = NULL`.
📌 `NOT UNKNOWN = UNKNOWN`.

### ⭐⭐ Aggregate functions and NULL

| Function | ⭐ NULL behaviour |
|---|---|
| ⭐ **`COUNT(*)`** | ⭐ **Counts ALL ROWS**, including rows containing NULLs |
| ⭐ **`COUNT(column)`** | ⭐ **IGNORES NULLs** in that column |
| `SUM`, `AVG`, `MIN`, `MAX` | ⭐ **All IGNORE NULLs** |

⚠ ⭐ **`AVG` divides by the count of NON-NULL values**, not by the number of rows. This is a classic trap.

### 🔢 Worked example

A table with **10 rows**, where the `marks` column contains **3 NULLs** and 7 values summing to 560:

| Query | ⭐ Result |
|---|---|
| `COUNT(*)` | ⭐ **10** |
| `COUNT(marks)` | ⭐ **7** |
| `SUM(marks)` | 560 |
| ⭐ `AVG(marks)` | ⭐ **560 / 7 = 80** (not 560/10 = 56) |
| `COUNT(DISTINCT marks)` | Number of distinct non-NULL values |

📌 ⭐ **`GROUP BY` treats all NULLs as ONE group**; `DISTINCT` treats them as one value. (Inconsistent with `=` semantics, but that is the standard.)

## 4.5 ⭐ Joins

| Join | 💡 Returns |
|---|---|
| ⭐ **INNER JOIN** | Only **matching** rows from both sides |
| ⭐ **LEFT OUTER JOIN** | ⭐ **ALL left rows** + matches; **NULLs** where the right has no match |
| **RIGHT OUTER JOIN** | All right rows + matches |
| **FULL OUTER JOIN** | All rows from both sides |
| **CROSS JOIN** | Cartesian product (no condition) |
| **SELF JOIN** | A table joined to itself — needs aliases |
| **NATURAL JOIN** | Auto-joins on all same-named columns |

🔢 `Employee LEFT JOIN Department` returns every employee, including those with no department (their department columns are NULL). An INNER JOIN would silently drop them — which is why "find employees without a department" needs `LEFT JOIN ... WHERE dept IS NULL`.

🔢 **Self join example:** "find each employee's manager's name" — join `Employee E1` to `Employee E2` on `E1.MgrID = E2.EmpID`.

## 4.6 ⭐ Subqueries

- **Non-correlated** — the inner query runs **once**, independently.
  ```sql
  SELECT * FROM emp WHERE sal > (SELECT AVG(sal) FROM emp);
  ```
- ⭐ **Correlated** — the inner query references the **outer** query's columns, so it **re-executes for every outer row**. Typically used with `EXISTS`.
  ```sql
  SELECT * FROM emp e WHERE EXISTS
      (SELECT 1 FROM dept d WHERE d.id = e.deptid AND d.loc = 'Agartala');
  ```

**Operators:** `IN`, `NOT IN`, `ANY`/`SOME`, `ALL`, `EXISTS`, `NOT EXISTS`.

### ⚠⭐ The `NOT IN` + NULL trap

```sql
SELECT * FROM A WHERE x NOT IN (SELECT y FROM B);
```
⭐ **If ANY value of `y` is NULL, this returns NO ROWS at all.**

💡 **Why:** `x NOT IN (1, 2, NULL)` expands to `x <> 1 AND x <> 2 AND x <> NULL`. The last comparison is **UNKNOWN**, and `TRUE AND UNKNOWN = UNKNOWN`, so no row is ever TRUE.

⭐ **`NOT EXISTS` is safe** — use it instead.

## 4.7 Views

📌 A **view** is a stored query presented as a virtual table. It stores no data itself.

✅ **Uses:** security (expose only some columns — hide salaries) · simplify complex joins for users · provide logical data independence.

⭐ **Updatability — a view is generally NOT updatable if it contains:**
📌 `DISTINCT` · `GROUP BY` · aggregate functions · `UNION` · a **join of multiple tables** · a subquery in the SELECT list

💡 **Why:** the DBMS must be able to translate your update on the view into an unambiguous update on exactly one base-table row. An aggregate or a join makes that impossible (which of the 50 rows behind `AVG(sal)` should change?).

⭐ **Materialised view** — physically stored and periodically refreshed. Faster reads, but the data can be stale.

## 4.8 Other objects and set operations

**Index** (`CREATE INDEX`) · ⭐ **Trigger** (procedural code fired **automatically** on INSERT/UPDATE/DELETE; `BEFORE`/`AFTER`, row-level or statement-level) · **Stored procedure** · **Assertion** · **Cursor** (row-by-row processing) · **Sequence**.

**Set operations:**
- ⭐ **`UNION`** — combines and ⭐ **removes duplicates** (requires a sort/hash, so slower)
- ⭐ **`UNION ALL`** — combines and ⭐ **keeps duplicates** (faster)
- `INTERSECT` · `EXCEPT` / `MINUS`

---

# 5. ⭐⭐⭐ Functional dependencies and normalization

## 5.1 💡 The problem being solved

Consider this single table:

| StudentID | StudentName | CourseID | CourseName | InstructorName |
|---|---|---|---|---|
| 101 | Amit | CS01 | Databases | Dr. Rao |
| 102 | Beena | CS01 | Databases | Dr. Rao |
| 103 | Chetan | CS02 | Networks | Dr. Sen |

⭐ **Three kinds of problem, called anomalies:**

1. ⭐ **Update anomaly** — to rename "Databases" you must update **every** row mentioning it. Miss one and the data is **inconsistent**.
2. ⭐ **Insertion anomaly** — you cannot record a new course with no students yet, because `StudentID` is part of the key and cannot be NULL.
3. ⭐ **Deletion anomaly** — deleting the last student on CS02 destroys all information about the CS02 course and Dr. Sen.

⭐ **Normalization** is the systematic decomposition of tables to eliminate these anomalies. The tool for reasoning about it is the **functional dependency**.

## 5.2 ⭐ Functional dependency

📌 ⭐ **X → Y means: any two tuples that agree on X MUST agree on Y.** Read as *"X functionally determines Y"* or *"Y depends on X"*.

🔢 `StudentID → StudentName` — if two rows have the same StudentID, they must have the same name. ✅ (A student has one name.)
🔢 `StudentName → StudentID` — ❌ **not** a valid FD, because two different students could share a name.

⭐ An FD is a **statement about the real world**, not something you can read off a sample table. A sample can only *disprove* an FD.

| Type | 💡 Description |
|---|---|
| **Trivial** | Y ⊆ X (e.g. `AB → A`) — always holds, tells you nothing |
| **Non-trivial** | Y ⊄ X |
| ⭐ **Full** | X → Y and **no proper subset** of X determines Y |
| ⭐ **Partial** | A **proper subset** of X already determines Y — the villain of 2NF |
| ⭐ **Transitive** | X → Y and Y → Z, hence X → Z — the villain of 3NF |

## 5.3 ⭐ Armstrong's axioms

📌 ⭐ **Three inference rules that are SOUND and COMPLETE** (they derive exactly the FDs implied by a given set — no more, no less):

| Axiom | Rule |
|---|---|
| ⭐ **Reflexivity** | If Y ⊆ X then **X → Y** |
| ⭐ **Augmentation** | If X → Y then **XZ → YZ** |
| ⭐ **Transitivity** | If X → Y and Y → Z then **X → Z** |

**Derived rules** (provable from the three above, but useful shortcuts):
- **Union:** X→Y and X→Z ⇒ X→YZ
- **Decomposition:** X→YZ ⇒ X→Y and X→Z
- **Pseudo-transitivity:** X→Y and WY→Z ⇒ WX→Z

⚠ ⭐ **Note the asymmetry:** you may always **split the right side** (decomposition) but you may **never split the left side**. `AB → C` does **not** imply `A → C`.

## 5.4 ⭐⭐⭐ Attribute closure and finding candidate keys

### 💡 The idea

The **closure X⁺** is the set of **all** attributes determined by X, directly or through a chain.

📌 ⭐ **X is a candidate key ⟺ X⁺ = ALL attributes, and no proper subset of X has that property.**

**Algorithm:**
1. Start with X⁺ = X
2. Look for any FD `A → B` where A ⊆ X⁺; add B to X⁺
3. Repeat until nothing changes

### ⭐⭐ The shortcut for finding candidate keys

⭐ **This trick turns a slow trial-and-error search into a 30-second procedure:**

| Where an attribute appears in the FD set | ⭐ Conclusion |
|---|---|
| ⭐ **Only on the LEFT** (never on any right side) | ⭐ **Must be in EVERY candidate key** |
| ⭐ **Only on the RIGHT** | ⭐ **Is in NO candidate key** |
| **On both sides, or neither** | **May or may not** be — test it |

⭐ **Procedure:** collect the must-have attributes → compute their closure → if it is everything, that set is the only candidate key → otherwise add "maybe" attributes one (then two) at a time and test.

### 🔢 Worked example 1

**R(A, B, C, D)** with FDs **A→B, B→C, C→D**

- **A** appears only on the left → **A must be in every candidate key**
- **A⁺:** start {A} → A→B gives {A,B} → B→C gives {A,B,C} → C→D gives {A,B,C,D} = all ✅
- Since A alone is sufficient and minimal, ⭐ **A is the ONLY candidate key.**
- **Prime attributes:** {A}. **Non-prime:** {B, C, D}.

### 🔢 Worked example 2

**R(A, B, C)** with FDs **AB→C, C→A**

- Attributes on the left: A, B, C. On the right: C, A. So **B appears only on the left → B is in every candidate key.**
- **B⁺** = {B} — not enough. Try adding attributes:
- **(AB)⁺:** {A,B} → AB→C gives {A,B,C} = all ✅ → **AB is a candidate key**
- **(BC)⁺:** {B,C} → C→A gives {A,B,C} = all ✅ → ⭐ **BC is ALSO a candidate key**
- **(AC)⁺:** {A,C} — no FD applies to add B → not a key
- ⭐ **Candidate keys: AB and BC.**
- **Prime attributes:** A, B, C — ⭐ **all three are prime.** (A from BC... no: A is in AB; B is in both; C is in BC. So all three.)

⭐ **Canonical / minimal cover** — an equivalent FD set with (a) a single attribute on each right-hand side, (b) no redundant FD, and (c) no redundant attribute on any left-hand side.

## 5.5 ⭐⭐⭐ The normal forms

### 💡 The progression

Each normal form removes one specific kind of redundancy. They are **nested**: BCNF ⊂ 3NF ⊂ 2NF ⊂ 1NF.

### ⭐ 1NF — atomic values

📌 **Every attribute holds a single, indivisible value.** No repeating groups, no lists inside a cell.

🔢 ❌ Not 1NF: `Phone = "9812345678, 9823456789"`
✅ 1NF: a separate `Phone` table with one number per row.

### ⭐⭐ 2NF — no partial dependency

📌 ⭐ **In 1NF, AND no NON-PRIME attribute depends on only PART of a candidate key.**

💡 **The problem it fixes:** with a composite key, an attribute depending on only half the key gets repeated for every value of the other half.

🔢 `Enrolment(StudentID, CourseID, Grade, CourseName)`, key = (StudentID, CourseID)
- `CourseName` depends on **CourseID alone** — a **partial** dependency ❌
- So `CourseName` is repeated for every student in that course → update anomaly
- **Fix:** split into `Enrolment(StudentID, CourseID, Grade)` and `Course(CourseID, CourseName)`

📌 ⭐ **A relation whose every candidate key is a SINGLE attribute is automatically in 2NF** — there is no "part of a key" to depend on.

### ⭐⭐ 3NF — no transitive dependency

📌 ⭐ **In 2NF, AND for every non-trivial FD X → Y: either X is a SUPER KEY, OR Y is a PRIME attribute.**

💡 **Equivalently:** no non-prime attribute depends on another non-prime attribute (a *transitive* dependency through a non-key attribute).

🔢 `Student(RollNo, Name, DeptID, DeptName)`, key = RollNo
- `RollNo → DeptID` and `DeptID → DeptName`, so `RollNo → DeptName` **transitively**
- `DeptID` is not a super key, and `DeptName` is not prime ❌
- `DeptName` is repeated for every student in the department → anomalies
- **Fix:** split into `Student(RollNo, Name, DeptID)` and `Dept(DeptID, DeptName)`

### ⭐⭐ BCNF — every determinant is a super key

📌 ⭐ **For EVERY non-trivial FD X → Y, X must be a SUPER KEY.** Full stop, no exceptions.

### ⭐⭐⭐ 3NF vs BCNF — the entire difference

⭐ **3NF has an escape clause that BCNF removes.**

3NF permits `X → Y` with a **non-super-key X**, *provided* **Y is a prime attribute**. BCNF does not allow this.

📌 ⭐ **Every BCNF relation is in 3NF, but not every 3NF relation is in BCNF.**

🔢 **A relation in 3NF but not BCNF:** `R(A, B, C)` with `AB → C` and `C → B`
- Candidate keys: **AB** and **AC**. Prime attributes: A, B, C (all).
- Check 3NF: for `C → B`, C is not a super key — but **B is prime** ✅ → **3NF holds**
- Check BCNF: `C → B` where C is **not** a super key ❌ → **BCNF fails**
- ⭐ **Highest normal form = 3NF**

### ⭐ Higher forms
- **4NF** — in BCNF and no non-trivial **multivalued dependency (MVD)** unless the determinant is a super key. MVDs cause a *cross-product* style redundancy.
- **5NF / PJNF** — no non-trivial **join dependency**.

### ⭐ Summary table

| NF | ⭐ Condition | Removes |
|---|---|---|
| **1NF** | All attributes **atomic** | Repeating groups |
| ⭐ **2NF** | 1NF + no **partial** dependency | Partial dependencies |
| ⭐ **3NF** | 2NF + for every X→Y: **X is a super key OR Y is prime** | Transitive dependencies |
| ⭐ **BCNF** | For every X→Y: ⭐ **X MUST be a super key** | All FD-based redundancy |
| **4NF** | BCNF + no non-trivial MVD | MVDs |
| **5NF** | No non-trivial join dependency | Join dependencies |

📌 ⭐ **A relation with only TWO attributes is always in BCNF.** (Any non-trivial FD between two attributes must have a single attribute as determinant, and if `A → B` in R(A,B), then A is a key.)

### 🔢⭐ The classic "highest normal form" questions

🔢 **R(A,B,C,D) with A→B, B→C, C→D.** Candidate key = **A** (from §5.4).
- Prime = {A}; non-prime = {B, C, D}
- **1NF** ✅
- **2NF** ✅ — the key is a **single attribute**, so no partial dependency is possible
- **3NF** ❌ — `B→C`: B is not a super key, and C is **not prime**
- ⭐ **Answer: highest normal form = 2NF**

🔢 **R(A,B,C) with AB→C, C→A.** Candidate keys **AB, BC**; all attributes prime.
- **2NF** ✅ — check `C→A`: does a non-prime attribute depend on part of a key? There **are no non-prime attributes**, so no partial dependency ✅
- **3NF** ✅ — `C→A`: C is not a super key, but **A is prime** ✅
- **BCNF** ❌ — `C→A` and C is **not** a super key
- ⭐ **Answer: highest normal form = 3NF**

## 5.6 ⭐⭐ Decomposition

### 💡 Lossless join

If you split R into R1 and R2, you must be able to **rejoin them and get exactly R back** — no more rows, no fewer.

📌 ⭐ **A decomposition of R into R1 and R2 is LOSSLESS ⟺ (R1 ∩ R2) → R1 or (R1 ∩ R2) → R2**
*i.e. the common attributes must form a **SUPER KEY of at least one fragment**.*

⚠ If not lossless, the natural join produces **SPURIOUS TUPLES** — rows that were never in the original.

🔢 **A lossy decomposition.** `R(Student, Course, Instructor)`:

| Student | Course | Instructor |
|---|---|---|
| Amit | DB | Rao |
| Beena | Net | Sen |

Split into `R1(Student, Course)` and `R2(Course, Instructor)`? Common attribute = `Course`, which is a key of neither fragment here if a course can have several instructors. If we instead split into `R1(Student, Instructor)` and `R2(Course, Instructor)` with `Instructor` not a key of either, the rejoin can invent combinations like (Amit, Net) that never existed. ⭐ **Those are spurious tuples.**

### 💡 Dependency preservation

📌 The union of the FDs that can be **checked within individual fragments** must be **equivalent to the original FD set**.

💡 **Why it matters:** if an FD spans two fragments, the DBMS cannot enforce it without an expensive join on every insert. You would lose an integrity guarantee.

### ⭐⭐ The crucial trade-off

| Target | ⭐ Lossless join | ⭐ Dependency preserving |
|---|---|---|
| ⭐ **3NF** | ⭐ **✅ ALWAYS achievable** | ⭐ **✅ ALWAYS achievable** |
| ⭐ **BCNF** | ⭐ **✅ Always achievable** | ⭐ **❌ NOT always achievable** |

📌 ⭐⭐ **A lossless, dependency-preserving decomposition into BCNF may not exist.**

⭐ **This is why 3NF is often the practical stopping point in real database design** — you get both guarantees. Pushing to BCNF may force you to give up dependency preservation, which means giving up automatic enforcement of a real business rule.

---

# 6. ⭐⭐ File organization and indexing

## 6.1 File organisation

| Organisation | 💡 Description |
|---|---|
| **Heap (unordered)** | Records appended anywhere. Insert O(1), search O(n) |
| **Sequential (ordered)** | Sorted on a key → binary search possible, but insertion is costly (must maintain order) |
| **Hash** | Direct access by hash of the key. ⚠ **Poor for range queries** (hashing destroys ordering) |
| **Clustered** | Related records stored physically together |
| **ISAM / B+ tree** | Indexed sequential — the standard |

📌 **Blocking factor = ⌊block size ÷ record size⌋** (records per block)
📌 **Number of blocks = ⌈number of records ÷ blocking factor⌉**

🔢 4000 records of 100 bytes, block size 1024 bytes:
Blocking factor = ⌊1024/100⌋ = **10**; blocks = ⌈4000/10⌉ = **400**.

## 6.2 ⭐ Index types

### 💡 The idea

An **index** is a smaller, sorted auxiliary structure that lets you find a record without scanning the whole file — exactly like a book's index.

| Classification | ⭐ Types |
|---|---|
| **By density** | ⭐ **Dense** — an entry for **EVERY** search-key value. **Sparse** — entries for only **some** values (typically one per block) |
| **By levels** | Single-level vs **multi-level** (an index on the index — which is what a B+ tree is) |
| **By key** | ⭐ **Primary** — on the file's **ordering key**; at most **one** per file. **Secondary** — on a non-ordering field; many possible |
| **By clustering** | ⭐ **Clustered** — the **physical row order matches** the index order; ⭐ **at most ONE per table**. **Non-clustered** — separate structure with pointers |

⚠ ⭐ **A sparse index requires the file to be SORTED on that field**, so a sparse index can only be a primary/clustered index. ⭐ **A SECONDARY index must therefore be DENSE** — you cannot skip entries on an unordered field.

⚠ ⭐ **Only one clustered index per table** — because a table can be physically sorted only one way.

**Trade-off:** indexes speed up `SELECT` but **slow down** `INSERT`, `UPDATE` and `DELETE` (every index must be maintained), and consume space.

## 6.3 ⭐⭐⭐ B-trees and B+ trees

### 💡 Why disk-based trees are different

A binary search tree on 1,000,000 records has height ~20. Each level is a **separate disk access** (~10 ms). That is 200 ms per lookup — far too slow.

⭐ **The fix: make each node HUGE — one full disk block — so it holds hundreds of keys and has hundreds of children.** Height collapses from 20 to 3.

💡 **This is the entire motivation for B-trees.** In-memory trees minimise *comparisons*; disk-based trees minimise *disk accesses*, and the way to do that is to maximise the **fan-out** per node.

### ⭐ B-tree of order m

- Each node has at most **m** children and at most **m − 1** keys
- Non-root internal nodes have at least **⌈m/2⌉** children (so the tree stays at least half full)
- ⭐ **All leaves are at the SAME level** — perfectly height-balanced
- ⭐ **Keys AND data pointers appear in EVERY node** (internal and leaf)

### ⭐⭐ B+ tree of order m

Same balancing rules, but two crucial changes:
- ⭐ **ALL data pointers are in the LEAVES only.** Internal nodes hold keys purely for **routing** (keys may be duplicated in the leaves).
- ⭐ **The leaves are LINKED together** in a sorted linked list.

```
B+ tree:
                    [ 30 | 60 ]                    ← internal: keys only
                   /     |     \
        [10|20]      [40|50]      [70|80]          ← internal
        /  |  \      /  |  \      /  |  \
      ┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
      │ leaves with ALL data pointers      │
      └─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┘
        └───┴───┴───┴───┴───┴───┴───┴───┘        ← LINKED
```

### ⭐⭐ Why B+ trees won for database indexing

| | B-tree | ⭐ **B+ tree** |
|---|---|---|
| Data pointers | In **all** nodes | ⭐ **Leaves only** |
| ⭐ **Leaves linked** | ❌ | ⭐ **✅ → efficient RANGE queries** |
| ⭐ **Internal fan-out** | Lower (nodes also carry data pointers) | ⭐ **HIGHER → shallower tree → fewer disk I/Os** |
| Search path | Varies (may terminate early at an internal node) | Always goes to a leaf (**predictable**) |
| Redundant keys | ❌ | ✅ (keys repeat in leaves) |
| Sequential scan | Needs a full traversal | ⭐ **Just walk the leaf list** |

🔢 ⭐ **The range-query advantage in action.** `WHERE marks BETWEEN 60 AND 80`:
- **B+ tree:** descend **once** to the leaf containing 60, then **walk sideways** along the linked leaves until you pass 80. Almost all the work is sequential disk reads.
- **B-tree:** you must traverse the tree repeatedly, jumping around the disk.

⭐ **Range queries are extremely common in SQL (`BETWEEN`, `>`, `<`, `ORDER BY`), which is why every real DBMS uses B+ trees.**

### ⭐⭐ Order calculation

📌 ⭐ **For an INTERNAL node of a B+ tree of order p:** with block size **B**, key size **K** and block-pointer size **P**:
**p × P + (p − 1) × K ≤ B**

💡 **Reading it:** p children means p pointers, and p children need p−1 separating keys. All of it must fit in one block.

📌 **For a LEAF node** of order p_leaf, with record-pointer size P_r and one next-leaf pointer P:
**p_leaf × (K + P_r) + P ≤ B**

### 🔢 Worked example

**Block size 1024 bytes, key 9 bytes, block pointer 6 bytes. Find the order of an internal node.**
```
p × 6 + (p − 1) × 9 ≤ 1024
6p + 9p − 9 ≤ 1024
15p ≤ 1033
p ≤ 68.87
```
⭐ **p = 68**

🔢 **Same block, leaf node with record pointer 7 bytes:**
```
p_leaf × (9 + 7) + 6 ≤ 1024
16 × p_leaf ≤ 1018
p_leaf ≤ 63.6  →  p_leaf = 63
```

📌 ⭐ **Height of a B+ tree with n keys and order p ≈ log_⌈p/2⌉(n)**

🔢 With p = 68 and 1,000,000 keys: log₃₄(10⁶) ≈ **4 levels.** ⭐ **Four disk accesses to find any record among a million.** That is the payoff.

**Operations:** insertion may cause a **node SPLIT**, propagating upward; ⭐ **the tree's height grows only when the ROOT splits** (which is why all leaves stay at the same level). Deletion may cause a **merge** or a **borrow** from a sibling.

---

# 7. ⭐⭐⭐ Transactions and concurrency control

## 7.1 💡 What a transaction is

📌 A **transaction** is a **logical unit of work** — a sequence of operations that must be treated as a single indivisible action.

🔢 **The canonical example: a bank transfer of ₹1000 from A to B.**
```
read(A); A = A − 1000; write(A);
read(B); B = B + 1000; write(B);
```
If the system crashes after `write(A)` but before `write(B)`, ₹1000 has **vanished**. The two writes must either both happen or neither.

## 7.2 ⭐⭐ ACID properties

📌 ⭐ **The four guarantees a DBMS makes about transactions:**

| Property | 💡 Meaning | Guaranteed by |
|---|---|---|
| ⭐ **Atomicity** | ⭐ **All operations complete, or NONE do** — "all or nothing" | Recovery manager, **logging** |
| ⭐ **Consistency** | Takes the database from one **valid state** to another (all constraints satisfied) | Integrity constraints + correct application logic |
| ⭐ **Isolation** | Concurrent transactions appear to execute **serially** — each behaves as if it were alone | **Concurrency-control manager** |
| ⭐ **Durability** | Once **committed**, changes **survive any failure** | Logging + stable storage |

⚠⚠ ⭐ **Do not confuse ACID with the OS critical-section requirements** (mutual exclusion, progress, bounded waiting — Week 6). Exam options mix the two lists.

**Transaction states:**
```
Active ──► Partially Committed ──► COMMITTED
   │
   └────► Failed ──► ABORTED (rolled back)
```
**Operations:** `read(X)`, `write(X)`, `commit`, `abort`.

## 7.3 ⭐⭐ The four concurrency problems

### 💡 What goes wrong without control

⭐ **1. Lost update (write–write)**
```
T1: read(A)   A=100
T2: read(A)   A=100
T1: A=A+50; write(A)   → A=150
T2: A=A+30; write(A)   → A=130     ⭐ T1's update is LOST
```
Identical to the OS race condition of Week 6 — the same problem at a different level.

⭐ **2. Dirty read (write–read)**
```
T1: A=A−50; write(A)      (uncommitted)
T2: read(A)               ⭐ reads the UNCOMMITTED value
T1: ABORT (rollback)      → T2 acted on data that never officially existed
```

⭐ **3. Unrepeatable read (read–write)**
```
T1: read(A)   → 100
T2: A=200; write(A); commit
T1: read(A)   → 200      ⭐ T1 read the SAME item twice and got DIFFERENT values
```

⭐ **4. Phantom read**
```
T1: SELECT COUNT(*) FROM emp WHERE sal>50000   → 10
T2: INSERT a new employee with sal=60000; commit
T1: SELECT COUNT(*) FROM emp WHERE sal>50000   → 11   ⭐ a "phantom" row appeared
```
⚠ **Unrepeatable read concerns an existing row changing; phantom read concerns new rows appearing.**

**5. Incorrect summary** — an aggregate reads some values before and some after another transaction's updates.

## 7.4 ⭐⭐⭐ Serializability

### 💡 The idea

A **serial** schedule (T1 fully, then T2 fully) is always correct — but allows no concurrency, so it is slow.

⭐ **We want an interleaved schedule that is nevertheless EQUIVALENT to some serial schedule.** Such a schedule is **serializable**, and it gives us concurrency *and* correctness.

### ⭐ Conflicting operations

📌 ⭐ **Two operations CONFLICT if and only if:**
1. They belong to **different** transactions, **and**
2. They access the **same** data item, **and**
3. **At least one** of them is a **WRITE**

⭐ **So read–read NEVER conflicts** (two readers do not interfere).

| Pair | Conflict? |
|---|---|
| read(A) / read(A) | ❌ No |
| read(A) / write(A) | ✅ Yes |
| write(A) / read(A) | ✅ Yes |
| write(A) / write(A) | ✅ Yes |
| read(A) / write(B) | ❌ No (different items) |

### ⭐⭐⭐ Testing conflict serializability — the precedence graph

📌 **Algorithm:**
1. Draw one **node per transaction**
2. For every pair of **conflicting** operations where Tᵢ's operation comes **first** in the schedule, draw an edge **Tᵢ → Tⱼ**
3. ⭐ **The schedule is conflict serializable ⟺ the graph is ACYCLIC**
4. A **topological sort** of the graph gives the equivalent serial order

💡 **Why the cycle test works:** an edge Tᵢ → Tⱼ means "Tᵢ must come before Tⱼ in any equivalent serial order". A cycle means Tᵢ must precede Tⱼ *and* Tⱼ must precede Tᵢ — impossible.

### 🔢 Worked example 1 — serializable

```
S: r1(A)  w1(A)  r2(A)  w2(A)  r1(B)  w1(B)  r2(B)  w2(B)
```
Conflicts on A: w1(A) before r2(A) → **T1 → T2**; w1(A) before w2(A) → T1 → T2.
Conflicts on B: w1(B) before r2(B) → **T1 → T2**.

Graph: `T1 → T2` only. ⭐ **Acyclic → conflict serializable**, equivalent to the serial order **T1, T2** ✅

### 🔢 Worked example 2 — NOT serializable

```
S: r1(A)  w2(A)  w1(A)
```
- r1(A) before w2(A) → **T1 → T2**
- w2(A) before w1(A) → **T2 → T1**

Graph has a **cycle** T1 → T2 → T1. ⭐ **NOT conflict serializable** ❌

### 🔢 Worked example 3 — three transactions

```
S: r1(X)  r2(X)  w1(X)  r3(X)  w2(X)
```
- r2(X) then w1(X) → **T2 → T1**
- r1(X) then w2(X) → **T1 → T2**
Already a cycle T1 ⇄ T2. ⭐ **Not conflict serializable** ❌

### ⭐ View serializability

📌 A weaker (**more permissive**) notion: a schedule is **view serializable** if it produces the same *reads-from* relationships and final writes as some serial schedule.

📌 ⭐ **Conflict serializable ⊂ View serializable ⊂ All schedules**

⭐ Every conflict-serializable schedule is view serializable, but **not** vice versa.
⚠ ⭐ **View serializability is NP-hard to test**, which is why practical systems only enforce **conflict** serializability (testable in polynomial time via the precedence graph).

## 7.5 ⭐⭐ Recoverability

### 💡 The idea

Serializability guarantees the *result* is correct if everything commits. But what if a transaction **aborts**? A schedule can be serializable yet impossible to recover from.

🔢 **An IRRECOVERABLE schedule:**
```
T1: w(A)
T2: r(A)          ← reads T1's uncommitted value
T2: COMMIT        ← T2 commits
T1: ABORT         ⭐ T1 rolls back — but T2 already committed based on T1's bad data!
```
⭐ You cannot undo T2 (it has committed) and you cannot keep it (its data is invalid). **The database is unrecoverable.**

| Class | ⭐ Condition | 💡 Guarantee |
|---|---|---|
| ⭐ **Recoverable** | If Tⱼ reads a value written by Tᵢ, then **Tⱼ commits AFTER Tᵢ commits** | Rollback is always possible |
| ⭐ **Cascadeless (ACA)** | A transaction reads **only COMMITTED** values | ⭐ **No cascading rollback** |
| **Strict** | No transaction reads **or writes** an uncommitted value | Simplest recovery (before-images suffice) |

📌 ⭐ **Strict ⊂ Cascadeless ⊂ Recoverable ⊂ All schedules**

⭐ **Cascading rollback** — aborting T1 forces aborting T2, which forces T3… An expensive chain reaction, avoided by cascadeless schedules.
⭐ **Irrecoverable schedules must be prevented absolutely; cascading rollback is merely expensive.**

## 7.6 ⭐⭐⭐ Locking protocols

### 💡 The idea

The practical way to enforce serializability: before touching a data item, a transaction must acquire a **lock** on it.

**Two lock modes:**
- ⭐ **Shared (S)** — for **reading**. Several transactions may hold an S lock simultaneously (readers do not conflict).
- ⭐ **Exclusive (X)** — for **writing**. Only one transaction may hold it, and no S locks may coexist.

⭐ **Lock compatibility matrix:**

| Held ↓ / Requested → | **S** | **X** |
|---|---|---|
| **S** | ⭐ **✅ Granted** | ❌ Wait |
| **X** | ❌ Wait | ❌ Wait |

💡 The single ✅ in the corner is exactly the "read–read does not conflict" rule, expressed in hardware terms.

### ⭐⭐ Two-Phase Locking (2PL)

📌 ⭐ **Every transaction has exactly two phases:**
1. ⭐ **GROWING (expanding) phase** — acquires locks, **releases none**
2. ⭐ **SHRINKING phase** — releases locks, **acquires none**

The moment of the first release is the **lock point**. Once you release anything, you may never lock again.

```
locks
held │      ╱‾‾‾‾╲
     │    ╱        ╲
     │  ╱            ╲
     └────────────────────► time
      growing  ↑ shrinking
            lock point
```

📌 ⭐⭐ **2PL GUARANTEES conflict serializability — but does NOT guarantee freedom from deadlock.**

💡 **Why it guarantees serializability:** the lock points can be ordered, and that order is a valid serial order.
💡 **Why deadlock is still possible:** T1 locks A and wants B; T2 locks B and wants A. Both are perfectly 2PL-compliant, and both wait forever. ⭐ Exactly the deadlock of Week 6, in a database.

### ⭐⭐ The four 2PL variants

| Variant | ⭐ Releases locks | ⭐ Special property |
|---|---|---|
| **Basic 2PL** | Any time during the shrinking phase | Serializable only |
| ⭐ **Conservative (static) 2PL** | Acquires **ALL** locks **before starting**; blocks until it can get them all | ⭐ **DEADLOCK-FREE** (no hold-and-wait) — but not strict, and hard to implement (needs to know all items in advance) |
| ⭐ **Strict 2PL** | Holds all **EXCLUSIVE** locks until commit/abort | ⭐ **CASCADELESS** (nobody can read uncommitted data) |
| **Rigorous 2PL** | Holds **ALL** locks (S and X) until commit/abort | Strict; simplest to reason about |

⚠⚠ ⭐ **CONSERVATIVE 2PL is the deadlock-free one; STRICT 2PL is the cascadeless/recoverable one.** These two are constantly swapped in exam options — learn them as a pair.

⭐ Most real systems use **strict 2PL** (recoverability matters more than deadlock avoidance, and deadlocks can be detected and resolved).

### ⭐ Timestamp ordering (a non-locking alternative)

💡 Every transaction gets a **timestamp** when it starts, and every data item keeps a `read_TS` and `write_TS`. An operation that would violate timestamp order is **rejected**, and the transaction is **restarted**.

- ✅ ⭐ **Deadlock-free** — nobody ever waits
- ❌ ⭐ **But starvation is possible** — a transaction can be restarted repeatedly
- ⭐ **Thomas's write rule:** an *obsolete* write (one that a later transaction has already overwritten) can simply be **ignored** rather than causing a rollback — this permits more schedules.

### ⭐ Other approaches

**MVCC (Multiversion Concurrency Control)** — keep multiple versions of each item, so ⭐ **readers never block writers and writers never block readers**. Each transaction reads the version consistent with its start time. Used by **PostgreSQL and Oracle**.

**Optimistic concurrency control** — three phases: **read** (work on a private copy) → **validate** (check for conflicts) → **write**. Good when conflicts are rare.

### ⭐ Deadlock in a DBMS

- ⭐ **Detection:** build a **wait-for graph** (Tᵢ → Tⱼ if Tᵢ waits for a lock Tⱼ holds). ⭐ **A cycle means deadlock.** Abort a victim.
- ⭐ **Prevention** via timestamps:
  - ⭐ **Wait-die:** if an **OLDER** transaction wants a lock held by a younger one, it **WAITS**. If a **younger** one wants an older one's lock, it **DIES** (rolls back and restarts).
  - ⭐ **Wound-wait:** if an **OLDER** transaction wants a younger one's lock, it **WOUNDS** (preempts/aborts) the younger. If a **younger** one wants an older one's lock, it **WAITS**.
  - ⭐ Both are deadlock-free because waiting always goes in one direction of the timestamp order, so no cycle can form.

⚠⚠ ⭐ **Two different graphs, do not confuse them:**
- **PRECEDENCE (serialization) graph** → tests **serializability**
- **WAIT-FOR graph** → tests **deadlock**

## 7.7 ⭐ Isolation levels

### 💡 The idea

Full serializability is expensive. SQL therefore lets you **trade isolation for performance**, accepting specific anomalies in exchange for speed.

| Level | Dirty read | Unrepeatable read | Phantom read |
|---|---|---|---|
| **Read Uncommitted** | ✅ possible | ✅ possible | ✅ possible |
| **Read Committed** | ❌ | ✅ possible | ✅ possible |
| **Repeatable Read** | ❌ | ❌ | ✅ possible |
| ⭐ **Serializable** | ❌ | ❌ | ❌ |

⭐ Increasing isolation = increasing locking = decreasing concurrency. **Serializable** is the strictest and slowest.

## 7.8 ⭐ Recovery

### 💡 The idea

Durability requires that committed data survive a crash. But writes sit in memory buffers before reaching disk. The solution is a **log** — a sequential record of every change, written to stable storage.

📌 **Log record format:** `<Tᵢ, X, old_value, new_value>`

| Technique | 💡 Behaviour |
|---|---|
| **Deferred update (NO-UNDO/REDO)** | Changes are written to the database **only after commit**. So an aborted transaction needs no undo → ⭐ **only REDO is needed** |
| ⭐ **Immediate update (UNDO/REDO)** | Changes go to the database as they occur → ⭐ **both UNDO and REDO are needed** |

📌 ⭐⭐ **Write-Ahead Logging (WAL): the LOG RECORD must reach stable storage BEFORE the corresponding data page.**

💡 **Why WAL is essential:** if the data page reached disk first and the system crashed before the log, you would have a changed database with no record of what changed — impossible to undo. WAL guarantees that anything on disk in the database is also described in the log.

⭐ **Checkpoint** — periodically flush all logs and dirty buffers, and write a checkpoint record. On recovery you need only scan back to the last checkpoint, not to the beginning of time.

⭐ **ARIES recovery — three passes:** **Analysis** (find the state at the crash) → **Redo** (repeat history) → **Undo** (roll back the losers).

**Shadow paging** — a no-log alternative using a shadow page table (atomically switch pointers on commit). Simple, but poor for concurrency and causes fragmentation.

---

# 8. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| **Degree / cardinality** | ⭐ **Columns / rows** |
| R × S degree / cardinality | Sum / product |
| Physical data independence | Change **internal** schema, conceptual unaffected |
| Candidate key | **Minimal** super key |
| PK cannot be | **NULL** (entity integrity) |
| FK may be | NULL (referential integrity) |
| Prime attribute | Part of **some** candidate key |
| Weak entity symbol / PK | Double rectangle / owner PK + partial key |
| Multivalued attribute symbol | **Double** ellipse |
| Derived attribute symbol | **Dashed** ellipse |
| 1:N relationship — FK goes on | ⭐ **The N side** |
| M:N relationship needs | ⭐ **3 tables** |
| 1:N relationship needs | 2 tables |
| **Primitive relational algebra ops** | ⭐ **σ, π, ×, ∪, −, ρ** |
| Natural join, ∩, ÷ are | ⭐ **Derived** |
| Projection | ⭐ **Removes duplicates** |
| Algebra vs SQL | Set-based / **bag-based** |
| Algebra vs calculus | Procedural / **declarative** |
| Relationally complete | Algebra ≡ TRC ≡ DRC |
| Clause evaluation order | FROM→WHERE→GROUP BY→HAVING→SELECT→ORDER BY |
| Filters rows / filters groups | **WHERE / HAVING** |
| Aggregates cannot appear in | ⭐ **WHERE** |
| **COUNT(*) vs COUNT(col)** | ⭐ **Includes / IGNORES NULLs** |
| AVG divides by | Count of **non-NULL** values |
| `= NULL` | ⭐ **Never matches — use `IS NULL`** |
| `NOT IN` with a NULL | ⭐ **Returns no rows** |
| GROUP BY treats NULLs as | **One** group |
| Removes structure | ⭐ **DROP** |
| TRUNCATE type | ⭐ **DDL**, not rollback-able |
| UNION vs UNION ALL | Removes / keeps duplicates |
| View not updatable if it has | GROUP BY, aggregates, DISTINCT, UNION, joins |
| **Armstrong's axioms** | ⭐ **Reflexivity, augmentation, transitivity** |
| Can split right side / left side | ✅ / ⭐ **❌** |
| Candidate key test | X⁺ = all attributes, minimal |
| Attribute only on the left | ⭐ **In every candidate key** |
| 2NF removes | ⭐ **Partial** dependencies |
| 3NF removes | ⭐ **Transitive** dependencies |
| **BCNF requires** | ⭐ **Every determinant is a super key** |
| 3NF allows X→Y when | ⭐ **Y is a PRIME attribute** |
| Single-attribute candidate key ⇒ | ⭐ **Automatically 2NF** |
| Two-attribute relation ⇒ | ⭐ **Always BCNF** |
| **Lossless join condition** | ⭐ **R1∩R2 is a super key of R1 or R2** |
| Not lossless produces | **Spurious tuples** |
| 3NF: lossless + dep-preserving | ⭐ **Always possible** |
| BCNF: dep-preserving | ⭐ **NOT always possible** |
| Secondary index must be | ⭐ **Dense** |
| Clustered indexes per table | ⭐ **At most 1** |
| **B+ tree data pointers** | ⭐ **Leaves only** |
| **B+ tree leaves are** | ⭐ **Linked → range queries** |
| B+ tree internal node order | p·P + (p−1)·K ≤ B |
| B+ tree height grows when | The **root** splits |
| **ACID** | Atomicity, Consistency, Isolation, Durability |
| Atomicity ensured by | Logging / recovery manager |
| **Conflict requires** | Different txns, same item, ⭐ **≥1 write** |
| Read–read | ⭐ **Never conflicts** |
| **Conflict serializable ⟺** | ⭐ **Precedence graph is ACYCLIC** |
| View serializability | Weaker; ⭐ **NP-hard to test** |
| Recoverability nesting | Strict ⊂ Cascadeless ⊂ Recoverable |
| S lock compatible with | Another **S** lock only |
| **2PL guarantees** | ⭐ **Conflict serializability, NOT deadlock freedom** |
| **Deadlock-free 2PL variant** | ⭐ **Conservative 2PL** |
| **Cascadeless 2PL variant** | ⭐ **Strict 2PL** |
| Timestamp ordering | Deadlock-free, but starvation possible |
| MVCC | Readers never block writers |
| Deadlock test graph | ⭐ **Wait-for** graph |
| Serializability test graph | ⭐ **Precedence** graph |
| Wait-die / wound-wait | Older waits / older preempts |
| **WAL rule** | ⭐ **Log before data** |
| Highest isolation level | **Serializable** |
| Checkpoint purpose | Limit recovery scan |

---

# 9. ⚠ Common traps

1. ⭐⭐ **Degree = columns, cardinality = rows.**
2. ⭐ **Natural join, intersection and division are NOT primitive** relational algebra operations.
3. ⭐⭐ **`COUNT(*)` includes rows with NULLs; `COUNT(col)` does not. `AVG` divides by non-NULL count.**
4. ⭐⭐ **`= NULL` never matches** — and `NOT IN` with a NULL in the subquery returns nothing.
5. ⭐⭐ **3NF vs BCNF:** 3NF's "Y is prime" escape clause is the **entire** difference.
6. ⭐ **A single-attribute candidate key means 2NF is automatic.**
7. ⭐⭐ **BCNF cannot always be dependency preserving; 3NF always can.**
8. ⭐⭐ **2PL does NOT prevent deadlock.**
9. ⭐⭐ **Conservative 2PL = deadlock-free; Strict 2PL = cascadeless.** Do not swap.
10. ⭐ **Read–read is never a conflict.**
11. ⭐ **B-tree stores data in all nodes; B+ tree only in leaves (and links them).**
12. ⭐ **DELETE is DML and rollback-able; TRUNCATE and DROP are DDL.**
13. ⭐ **Aggregates cannot appear in `WHERE`.**
14. ⭐⭐ **Precedence graph tests SERIALIZABILITY; wait-for graph tests DEADLOCK.** Different graphs, different purposes.
15. **ACID ≠ the OS critical-section requirements.**
16. **The FK goes on the "N" side of a 1:N relationship.**
17. **A secondary index must be dense.**
18. **Unrepeatable read (existing row changes) ≠ phantom read (new rows appear).**

---

# 10. Practice

- GATE: [`Paper2_S09_Databases/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S09_Databases/) — **302 questions**
- State-PSC level: [`Paper2_S09_Databases/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S09_Databases/) — **390 questions** (includes data mining & warehousing)
- Test: [`Week_07_Test.md`](../04_Mock_Tests/Week_07_Test.md)

**Priority order if short on time:** ⭐ **finding candidate keys via attribute closure** → normal forms (especially 3NF vs BCNF) → conflict serializability via precedence graphs → SQL NULL and aggregate semantics → B+ tree properties and order calculation → 2PL variants → lossless decomposition → ER-to-relational mapping.
