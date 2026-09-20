# Week 7 Question Bank — Databases

**Syllabus §9** · 180 questions · Practice set · +1 / −0.33 marking

> Grounded entirely in `05_Notes/Week_07_Databases.md`. Attempt a part, then verify against the answer key and read the worked reasoning for every closure, normal-form, precedence-graph and numerical question.

---

## Part A — DBMS fundamentals, architecture & data independence

**Q1.** Which of the following is **NOT** an advantage of a DBMS over a file-processing system?
(A) Controlled redundancy  (B) Constraint-based consistency enforcement  (C) A separate program must be written for every new query  (D) Built-in concurrency control

**Q2.** In the three-level architecture, the level describing the **entire logical structure** of the database (all entities, relationships and constraints) is the
(A) conceptual level  (B) external level  (C) internal level  (D) physical level

**Q3.** Adding an index to speed up a query, with no change to the conceptual schema or any application, is an instance of
(A) logical data independence  (B) physical data independence  (C) view integration  (D) schema abstraction

**Q4.** Logical data independence is best defined as the ability to
(A) change storage structures without affecting applications  (B) achieve faster access than physical independence  (C) change the conceptual schema without altering the external views  (D) avoid all schema changes

**Q5.** Which form of data independence is **harder** to achieve in practice?
(A) physical data independence  (B) both are equally hard  (C) neither is difficult  (D) logical data independence

**Q6.** The actual data stored in a database at a particular moment is called the
(A) instance  (B) schema  (C) intension  (D) metadata

**Q7.** The overall design/structure of a database, which changes only rarely, is the
(A) instance  (B) schema  (C) tuple  (D) domain

**Q8.** How many conceptual (logical) schemas does a single database have?
(A) one per user  (B) one per table  (C) exactly one  (D) one per view

**Q9.** Which data model represents data as tables of tuples and is the dominant model today?
(A) hierarchical  (B) network  (C) object-oriented  (D) relational

**Q10.** Which role is responsible for administration, security, performance tuning and backup of a database?
(A) DBA  (B) end user  (C) application programmer  (D) database designer

---

## Part B — ER model

**Q11.** A **weak entity** is represented in an ER diagram by a
(A) single rectangle  (B) double rectangle  (C) diamond  (D) double ellipse

**Q12.** A **multivalued attribute** (e.g. PhoneNumbers) is drawn as a
(A) dashed ellipse  (B) double rectangle  (C) double ellipse  (D) underlined ellipse

**Q13.** A **derived attribute** such as Age (computed from DateOfBirth) is drawn as a
(A) dashed ellipse  (B) double ellipse  (C) double rectangle  (D) diamond

**Q14.** The relationship connecting a weak entity to its owner (identifying) entity is drawn as a
(A) single diamond  (B) double rectangle  (C) dashed diamond  (D) double diamond

**Q15.** The **partial key** of a weak entity is shown with
(A) a solid underline  (B) a dashed underline  (C) a double underline  (D) no underline

**Q16.** The primary key of a weak entity is
(A) its partial key alone  (B) the owner's primary key alone  (C) the owner's primary key **plus** its own partial key  (D) a system-generated surrogate only

**Q17.** A weak entity's participation in its identifying relationship is always
(A) total  (B) partial  (C) optional  (D) zero

**Q18.** **Total participation** is represented in an ER diagram by
(A) a single line  (B) a dashed line  (C) a diamond  (D) a double line

**Q19.** Which of the following is an example of an **M:N** cardinality ratio?
(A) One person has one passport  (B) Many students take many courses  (C) One department has many employees  (D) Many employees belong to one department

**Q20.** A **key attribute** of a strong entity is shown by
(A) a double ellipse  (B) a dashed ellipse  (C) an ellipse with the name underlined  (D) a diamond

**Q21.** An Employee *manages* another Employee. The degree of this relationship is
(A) unary / recursive  (B) binary  (C) ternary  (D) quaternary

**Q22.** The Entity-Relationship model (1976) was proposed by
(A) Codd  (B) Chen  (C) Boyce  (D) Armstrong

**Q23.** An IS-A hierarchy (a Vehicle specialising into Car and Truck) is modelled using
(A) aggregation  (B) a weak entity  (C) a ternary relationship  (D) specialisation / generalisation

---

## Part C — ER → relational mapping

**Q24.** When a **1:N** relationship is mapped to tables, the foreign key is placed
(A) on the "1" side  (B) in a new separate table  (C) on the "N" (many) side  (D) on either side

**Q25.** A binary **M:N** relationship between two entities requires a **minimum** of how many tables?
(A) 1  (B) 2  (C) 4  (D) 3

**Q26.** Two entities related by a **1:N** relationship require a minimum of how many tables?
(A) 1  (B) 2  (C) 3  (D) 4

**Q27.** A **multivalued attribute** is mapped to
(A) a separate table containing the entity's primary key plus the attribute  (B) an extra column in the entity's table  (C) a derived column  (D) the owner entity's table

**Q28.** The foreign-key-placement rule generalises to: the foreign key goes on the side that has
(A) many partners  (B) the weak entity  (C) at most **one** partner  (D) the most queries

**Q29.** `Student` and `Course` with an M:N "Enrols" relationship storing a `Grade` map to which relations?
(A) Student, Course only  (B) Student, Course, Enrols(RollNo, CourseID, Grade)  (C) one combined table  (D) Student, Enrols only

**Q30.** A **composite attribute** (e.g. Name → First, Last) is mapped to relations by
(A) a separate table  (B) a multivalued table  (C) leaving it unstored  (D) flattening it into its component columns

**Q31.** A **derived attribute** is normally
(A) not stored (computed when needed)  (B) stored as an ordinary column  (C) made the primary key  (D) stored in a separate table

---

## Part D — Relational model & keys

**Q32.** The number of **attributes (columns)** in a relation is its
(A) cardinality  (B) degree  (C) domain  (D) tuple count

**Q33.** The number of **tuples (rows)** in a relation is its
(A) degree  (B) arity  (C) cardinality  (D) domain

**Q34.** R has degree 3 and 5 tuples; S has degree 2 and 3 tuples. The **degree** of R × S is
(A) 5  (B) 6  (C) 15  (D) 8

**Q35.** For the same R and S, the **cardinality** of R × S is
(A) 5  (B) 6  (C) 15  (D) 8

**Q36.** A **minimal** super key is called a
(A) primary key  (B) candidate key  (C) foreign key  (D) composite key

**Q37.** Which statement about a **primary key** is TRUE?
(A) it may be NULL  (B) it must be a single attribute  (C) it may contain duplicate values  (D) it cannot be NULL

**Q38.** Which key **may** legitimately take a NULL value?
(A) primary key  (B) candidate key  (C) foreign key  (D) super key

**Q39.** A **prime attribute** is one that is
(A) part of no candidate key  (B) part of **some** candidate key  (C) a foreign key  (D) a derived attribute

**Q40.** If `{RollNo}` alone uniquely identifies a row, then `{RollNo, Name}` is
(A) a candidate key  (B) a super key but **not** a candidate key  (C) a foreign key  (D) a primary key

**Q41.** In R(A, B, C, D) with A→B, B→C, C→D, the only candidate key is
(A) A  (B) D  (C) AD  (D) AB

**Q42.** In R(A, B, C) with AB→C and C→A, the candidate keys are
(A) AB only  (B) AB and BC  (C) C only  (D) A and B

**Q43.** In R(A, B, C) with AB→C and C→A, attribute **B** is
(A) non-prime  (B) part of no key  (C) a foreign key  (D) prime and present in every candidate key

**Q44.** A **super key** is
(A) always minimal  (B) **any** attribute set that uniquely identifies a tuple  (C) always a single attribute  (D) identical to a foreign key

---

## Part E — Integrity constraints

**Q45.** The rule that a **primary key cannot be NULL** (and must be unique) is
(A) entity integrity  (B) referential integrity  (C) domain integrity  (D) key constraint

**Q46.** The rule that a **foreign key must match an existing primary key value, or be NULL**, is
(A) entity integrity  (B) referential integrity  (C) domain integrity  (D) key constraint

**Q47.** When a referenced (parent) row is deleted, the option that deletes the referencing child rows too is
(A) SET NULL  (B) RESTRICT  (C) CASCADE  (D) NO ACTION

**Q48.** The referential action that sets the foreign key to NULL when the parent is deleted is
(A) CASCADE  (B) RESTRICT  (C) SET DEFAULT  (D) SET NULL

**Q49.** Requiring column values to be drawn from the declared type/domain is
(A) entity integrity  (B) referential integrity  (C) domain integrity  (D) key constraint

**Q50.** A child-table row referring to a parent row that does not exist is called
(A) an orphan row  (B) a phantom  (C) a spurious tuple  (D) a dangling index

---

## Part F — Relational algebra & calculus

**Q51.** Which of the following is **NOT** a fundamental (primitive) operation of relational algebra?
(A) Selection σ  (B) Projection π  (C) Natural join ⋈  (D) Set difference −

**Q52.** The six primitive operations of relational algebra are
(A) σ, π, ×, ∪, −, ρ  (B) σ, π, ⋈, ∪, ∩, ÷  (C) σ, π, ×, ∩, −, ÷  (D) σ, π, ⋈, ∪, −, ρ

**Q53.** Which operation selects **columns** and removes duplicate rows?
(A) selection σ  (B) projection π  (C) Cartesian product ×  (D) rename ρ

**Q54.** Which operation selects **rows** satisfying a condition?
(A) selection σ  (B) projection π  (C) rename ρ  (D) division ÷

**Q55.** Intersection R ∩ S can be expressed using only primitives as
(A) R − S  (B) R × S  (C) R ∪ S  (D) R − (R − S)

**Q56.** The division operator R ÷ S answers which kind of query?
(A) "there exists"  (B) "for all"  (C) aggregation  (D) sorting

**Q57.** Union, intersection and set difference require the two relations to be
(A) of equal cardinality  (B) sorted  (C) union-compatible (same degree, matching domains)  (D) key-related

**Q58.** Relational algebra results are ___ whereas SQL query results are ___.
(A) bag-based / set-based  (B) set-based / bag-based  (C) both set-based  (D) both bag-based

**Q59.** If the join attribute is a **key of S** and a **foreign key in R** (no NULLs), then |R ⋈ S| equals
(A) 0  (B) |R|  (C) |S|  (D) |R| × |S|

**Q60.** The general bound on natural-join cardinality is
(A) 0 ≤ |R⋈S| ≤ |R| + |S|  (B) |R| ≤ |R⋈S| ≤ |S|  (C) 0 ≤ |R⋈S| ≤ |R| × |S|  (D) |R⋈S| = |R| × |S| always

**Q61.** Tuple relational calculus (TRC) and domain relational calculus (DRC) are
(A) procedural languages  (B) declarative languages  (C) storage formats  (D) indexing methods

**Q62.** The property that relational algebra, safe TRC and safe DRC are equivalent in expressive power is called
(A) relational completeness  (B) referential integrity  (C) normalization  (D) closure

---

## Part G — SQL

**Q63.** Which of the following is a **DDL** command?
(A) SELECT  (B) UPDATE  (C) TRUNCATE  (D) COMMIT

**Q64.** `GRANT` and `REVOKE` belong to which category?
(A) DDL  (B) DML  (C) DCL  (D) TCL

**Q65.** `COMMIT`, `ROLLBACK` and `SAVEPOINT` belong to
(A) DDL  (B) DML  (C) DCL  (D) TCL

**Q66.** Which statement about DELETE vs TRUNCATE is correct?
(A) both are DML  (B) DELETE can have a WHERE clause; TRUNCATE cannot  (C) TRUNCATE can always be rolled back  (D) DELETE removes the table structure

**Q67.** Which command removes both the **rows and the table structure**?
(A) DELETE  (B) TRUNCATE  (C) DROP  (D) UPDATE

**Q68.** `TRUNCATE` is classified as
(A) DML  (B) DDL  (C) DCL  (D) TCL

**Q69.** The correct **logical order** of clause evaluation in a SELECT statement is
(A) FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY  (B) SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY  (C) FROM → GROUP BY → WHERE → SELECT → HAVING → ORDER BY  (D) WHERE → FROM → SELECT → GROUP BY → HAVING → ORDER BY

**Q70.** Aggregate functions such as `AVG()` **cannot** appear in which clause?
(A) HAVING  (B) SELECT  (C) WHERE  (D) ORDER BY

**Q71.** The clause used to filter **groups** produced by GROUP BY is
(A) WHERE  (B) HAVING  (C) ORDER BY  (D) DISTINCT

**Q72.** `WHERE` filters ___ while `HAVING` filters ___.
(A) groups / rows  (B) rows / groups  (C) columns / rows  (D) rows / columns

**Q73.** A column alias defined in `SELECT` can be used in
(A) WHERE  (B) GROUP BY  (C) ORDER BY  (D) HAVING before grouping

**Q74.** For a table with 10 rows where the `marks` column has 3 NULLs, `COUNT(*)` and `COUNT(marks)` return respectively
(A) 10 and 10  (B) 10 and 7  (C) 7 and 7  (D) 7 and 10

**Q75.** A `marks` column has 7 non-NULL values summing to 560 and 3 NULLs (10 rows total). `AVG(marks)` returns
(A) 56  (B) 80  (C) 560  (D) 8

**Q76.** Which aggregate counts **all rows**, including rows containing NULLs?
(A) COUNT(*)  (B) COUNT(column)  (C) SUM(column)  (D) AVG(column)

**Q77.** The predicate `WHERE marks = NULL`
(A) matches all rows where marks is NULL  (B) matches nothing (evaluates to UNKNOWN)  (C) is a syntax error  (D) matches every row

**Q78.** The correct way to test for a NULL value is
(A) = NULL  (B) == NULL  (C) IS NULL  (D) EQUALS NULL

**Q79.** `SELECT * FROM A WHERE x NOT IN (SELECT y FROM B)` where column `y` contains a NULL returns
(A) all rows of A  (B) no rows at all  (C) only the matching rows  (D) a syntax error

**Q80.** Which construct is **safe** against the NULL trap and preferred over `NOT IN`?
(A) IN  (B) = ANY  (C) IS NOT NULL  (D) NOT EXISTS

**Q81.** Which join returns **all rows from the left table** plus matching rows, with NULLs where no match exists?
(A) INNER JOIN  (B) LEFT OUTER JOIN  (C) RIGHT OUTER JOIN  (D) CROSS JOIN

**Q82.** A subquery that references the **outer** query's columns and re-executes for every outer row is
(A) non-correlated  (B) a view  (C) correlated  (D) a common table expression

**Q83.** `UNION` differs from `UNION ALL` in that `UNION`
(A) keeps duplicates  (B) removes duplicates  (C) requires a join  (D) is faster than UNION ALL

**Q84.** A view is generally **NOT updatable** if it contains
(A) a WHERE clause  (B) an ORDER BY only  (C) a GROUP BY, aggregate function, or a join of multiple tables  (D) a projection of a single column

**Q85.** Procedural code that fires **automatically** on INSERT/UPDATE/DELETE is a
(A) view  (B) cursor  (C) sequence  (D) trigger

---

## Part H — Functional dependencies & normalization

**Q86.** The functional dependency X → Y means
(A) X and Y are equal  (B) any two tuples that agree on X must agree on Y  (C) Y is a key  (D) X is a foreign key referencing Y

**Q87.** Which set of rules is **sound and complete** for inferring all functional dependencies implied by a given set?
(A) Codd's rules  (B) Armstrong's axioms  (C) De Morgan's laws  (D) ACID rules

**Q88.** Armstrong's three primary axioms are
(A) reflexivity, augmentation, transitivity  (B) union, decomposition, pseudo-transitivity  (C) closure, minimality, superkey  (D) selection, projection, join

**Q89.** The **augmentation** axiom states
(A) if Y ⊆ X then X → Y  (B) if X → Y then XZ → YZ  (C) if X → Y and Y → Z then X → Z  (D) if X → YZ then X → Y

**Q90.** Regarding splitting the sides of an FD, you may split
(A) both sides freely  (B) the left side but not the right  (C) the right side but **not** the left  (D) neither side

**Q91.** `AB → C` does **NOT** necessarily imply which of the following?
(A) A → C  (B) ABD → C  (C) AB → C  (D) AB → CC

**Q92.** The attribute closure X⁺ is
(A) the minimal super key  (B) the set of candidate keys  (C) the set of **all** attributes functionally determined by X  (D) the set of all FDs in F

**Q93.** An attribute that appears **only on the left** side across the whole FD set must be
(A) in no candidate key  (B) in **every** candidate key  (C) a foreign key  (D) non-prime

**Q94.** An attribute that appears **only on the right** side of every FD is
(A) in no candidate key  (B) in every candidate key  (C) always prime  (D) a super key

**Q95.** A **trivial** functional dependency X → Y is one where
(A) Y ⊆ X  (B) X ⊆ Y  (C) X is empty  (D) Y is prime

**Q96.** A **partial dependency** (the villain of 2NF) occurs when
(A) X → Y and Y → Z  (B) a **non-prime** attribute depends on **part** of a candidate key  (C) Y ⊆ X  (D) a prime attribute depends on a non-prime attribute

**Q97.** 1NF requires that
(A) there are no transitive dependencies  (B) every attribute holds a single, atomic value  (C) every determinant is a super key  (D) there are no partial dependencies

**Q98.** 2NF is defined as
(A) 1NF with no transitive dependency  (B) every determinant a super key  (C) 1NF with **no partial dependency** of a non-prime attribute on a candidate key  (D) no multivalued dependency

**Q99.** A relation whose every candidate key is a **single attribute** is automatically in
(A) BCNF  (B) 2NF  (C) 4NF  (D) 5NF

**Q100.** A relation is in **3NF** if, for every non-trivial FD X → Y,
(A) X is a super key  (B) X is a super key **OR** Y is a prime attribute  (C) Y is non-prime  (D) X is prime

**Q101.** A relation is in **BCNF** if, for every non-trivial FD X → Y,
(A) X is a super key  (B) Y is prime  (C) X is prime  (D) Y is a candidate key

**Q102.** A relation is in **3NF but not BCNF** when there is an FD X → Y with X not a super key and
(A) Y non-prime  (B) Y prime  (C) Y empty  (D) X empty

**Q103.** Every relation in BCNF is
(A) not necessarily in 3NF  (B) always in 3NF  (C) never in 3NF  (D) only in 2NF

**Q104.** R(A, B, C, D) with A→B, B→C, C→D. The **highest** normal form R satisfies is
(A) 1NF  (B) 2NF  (C) 3NF  (D) BCNF

**Q105.** R(A, B, C) with AB→C and C→A. The **highest** normal form R satisfies is
(A) 1NF  (B) 2NF  (C) 3NF  (D) BCNF

**Q106.** A relation with only **two attributes** is always in
(A) only 1NF  (B) BCNF  (C) only 2NF  (D) not even 1NF

**Q107.** A **transitive dependency** (the villain of 3NF) is
(A) X → Y and Y → Z giving X → Z through a non-key attribute  (B) a non-prime attribute depending on part of a key  (C) Y ⊆ X  (D) the existence of two candidate keys

**Q108.** A **canonical / minimal cover** of an FD set has
(A) a single attribute on each right-hand side, no redundant FD, and no redundant left-hand attribute  (B) multiple attributes on each right-hand side  (C) all attributes on the left-hand side  (D) no transitive dependencies

---

## Part I — Decomposition

**Q109.** A decomposition of R into R1 and R2 is **lossless** if R1 ∩ R2 is
(A) empty  (B) a super key of at least one of R1 or R2  (C) a non-prime attribute  (D) equal to R

**Q110.** A non-lossless (lossy) decomposition, when rejoined, produces
(A) fewer rows  (B) only NULLs  (C) spurious tuples  (D) exactly the original relation

**Q111.** Which pair of guarantees can a decomposition into **3NF** always provide?
(A) lossless join only  (B) dependency preservation only  (C) neither  (D) both lossless join and dependency preservation

**Q112.** A decomposition into **BCNF**
(A) always preserves dependencies  (B) is always lossless but may not preserve dependencies  (C) is never lossless  (D) always loses information

**Q113.** **Dependency preservation** means
(A) all data is recovered on rejoin  (B) no NULLs appear  (C) the FDs checkable within individual fragments together imply the original FD set  (D) no spurious tuples appear

**Q114.** 3NF is often the practical stopping point in design because
(A) BCNF is impossible to reach  (B) 3NF guarantees **both** lossless join and dependency preservation, while BCNF may sacrifice dependency preservation  (C) 3NF removes all redundancy  (D) BCNF is not lossless

---

## Part J — File organization & indexing

**Q115.** An index with an entry for **every** search-key value in the data file is
(A) sparse  (B) dense  (C) clustered  (D) secondary

**Q116.** A **sparse** index typically has
(A) one entry per record  (B) no entries  (C) one entry per block  (D) an entry for every value

**Q117.** A **secondary** index must be
(A) sparse  (B) dense  (C) clustered  (D) primary

**Q118.** How many **clustered** indexes can a table have?
(A) unlimited  (B) at most one  (C) exactly two  (D) one per column

**Q119.** The blocking factor for records of 100 bytes in a block of 1024 bytes is
(A) 8  (B) 10  (C) 100  (D) 1024

**Q120.** With 4000 records and a blocking factor of 10, the number of blocks required is
(A) 40  (B) 4000  (C) 400  (D) 100

**Q121.** Which file organization is **poor** for range queries because it destroys ordering?
(A) sequential  (B) B+ tree  (C) hash  (D) clustered

**Q122.** Compared to a heap file, adding indexes
(A) also speeds up INSERT  (B) has no downside  (C) reduces storage  (D) speeds up SELECT but slows down INSERT/UPDATE/DELETE and consumes space

---

## Part K — B-trees and B+ trees

**Q123.** In a **B+ tree**, data (record) pointers are stored
(A) in all nodes  (B) in the leaves only  (C) in the root only  (D) in internal nodes only

**Q124.** Which property gives B+ trees efficient **range queries**?
(A) higher fan-out  (B) shorter height  (C) leaves linked in a sorted list  (D) data stored in internal nodes

**Q125.** The main reason B+ trees are preferred to B-trees for database indexing is
(A) smaller height for the same order only  (B) data pointers in linked leaves (efficient range queries) plus higher internal fan-out (shallower tree)  (C) they store no keys in internal nodes  (D) they allow only duplicate keys

**Q126.** In a **B-tree**, keys and data pointers appear
(A) in the leaves only  (B) in the root only  (C) in internal nodes only  (D) in every node (internal and leaf)

**Q127.** For a B+ tree **internal** node with block size B = 1024, key size K = 9, block-pointer P = 6, using p·P + (p−1)·K ≤ B, the order p is
(A) 34  (B) 63  (C) 68  (D) 128

**Q128.** For a B+ tree **leaf** with block 1024, key 9, record-pointer 7 and next-leaf pointer 6, using p·(K + Pr) + P ≤ B, the order is
(A) 63  (B) 68  (C) 60  (D) 64

**Q129.** In a B+ tree of order m, all leaves are
(A) at different levels  (B) at the same level  (C) unlinked  (D) stored in the root

**Q130.** The height of a B+ tree grows only when
(A) any node splits  (B) a leaf splits  (C) the root splits  (D) a leaf merges

---

## Part L — Transactions & ACID

**Q131.** The **ACID** properties of a transaction are
(A) Atomicity, Consistency, Isolation, Durability  (B) Atomicity, Concurrency, Integrity, Durability  (C) Accuracy, Consistency, Isolation, Dependability  (D) Atomicity, Consistency, Indexing, Durability

**Q132.** "All operations of a transaction complete, or none do" defines
(A) atomicity  (B) consistency  (C) isolation  (D) durability

**Q133.** The guarantee that **committed** changes survive any subsequent failure is
(A) atomicity  (B) consistency  (C) isolation  (D) durability

**Q134.** Isolation is enforced by the
(A) recovery manager  (B) concurrency-control manager  (C) query optimizer  (D) buffer manager

**Q135.** A transaction that has executed its final statement but has not yet committed is in which state?
(A) active  (B) partially committed  (C) aborted  (D) failed

**Q136.** A **transaction** is best defined as
(A) a single query  (B) a schedule  (C) a logical unit of work treated as a single indivisible action  (D) a checkpoint

---

## Part M — Concurrency control, serializability, recoverability & locking

**Q137.** Two operations **conflict** if and only if they
(A) are both reads  (B) belong to different transactions, access the same item, and at least one is a write  (C) belong to the same transaction  (D) access different items

**Q138.** Which pair of operations **never** conflicts?
(A) read(A) / write(A)  (B) write(A) / read(A)  (C) read(A) / read(A)  (D) write(A) / write(A)

**Q139.** A schedule is **conflict serializable** if and only if its precedence (serialization) graph
(A) is connected  (B) is acyclic  (C) contains a cycle  (D) is complete

**Q140.** In a precedence graph, an edge Tᵢ → Tⱼ is drawn when
(A) Tᵢ and Tⱼ read the same item  (B) Tᵢ commits before Tⱼ  (C) a conflicting pair exists with Tᵢ's operation occurring first  (D) Tᵢ waits for Tⱼ

**Q141.** The schedule **S: r1(A) w2(A) w1(A)** is
(A) conflict serializable, order T1, T2  (B) conflict serializable, order T2, T1  (C) not conflict serializable (its precedence graph has a cycle)  (D) a serial schedule

**Q142.** The schedule **S: r1(A) w1(A) r2(A) w2(A) r1(B) w1(B) r2(B) w2(B)** is
(A) conflict serializable, equivalent to the serial order T1, T2  (B) not serializable  (C) conflict serializable, equivalent to T2, T1  (D) view but not conflict serializable

**Q143.** View serializability, compared to conflict serializability, is
(A) stronger (admits fewer schedules)  (B) identical  (C) weaker (more permissive) but NP-hard to test  (D) tested by the wait-for graph

**Q144.** The correct class containment is
(A) conflict serializable ⊂ view serializable ⊂ all schedules  (B) view ⊂ conflict ⊂ all  (C) all ⊂ conflict ⊂ view  (D) they are disjoint

**Q145.** An **irrecoverable** schedule is one in which
(A) a transaction reads only committed data  (B) Tⱼ reads Tᵢ's uncommitted value, Tⱼ commits, then Tᵢ aborts  (C) no transaction reads uncommitted data  (D) all transactions commit in order

**Q146.** A **cascadeless** schedule is guaranteed by requiring that a transaction
(A) never deadlocks  (B) is serializable  (C) reads only **committed** values (so no cascading rollback)  (D) is durable

**Q147.** The nesting of recoverability classes is
(A) Strict ⊂ Cascadeless ⊂ Recoverable  (B) Recoverable ⊂ Cascadeless ⊂ Strict  (C) Strict ⊂ Recoverable ⊂ Cascadeless  (D) all three are equal

**Q148.** In the lock compatibility matrix, which lock request can be **granted** while a lock is already held?
(A) X requested while S is held  (B) S requested while S is held  (C) X requested while X is held  (D) S requested while X is held

**Q149.** The Two-Phase Locking (2PL) protocol guarantees
(A) conflict serializability  (B) freedom from deadlock  (C) freedom from starvation  (D) recoverability in all cases

**Q150.** Under 2PL, once a transaction **releases** its first lock it
(A) may acquire more locks  (B) may not acquire any more locks  (C) must commit immediately  (D) re-enters the growing phase

**Q151.** Which 2PL variant is **deadlock-free** because it acquires all locks before it begins?
(A) basic 2PL  (B) strict 2PL  (C) conservative (static) 2PL  (D) rigorous 2PL

**Q152.** Which 2PL variant holds all **exclusive** locks until commit/abort, guaranteeing **cascadeless** schedules?
(A) conservative 2PL  (B) strict 2PL  (C) basic 2PL  (D) timestamp ordering

**Q153.** Which statement is TRUE?
(A) 2PL prevents deadlock  (B) conservative 2PL = deadlock-free; strict 2PL = cascadeless  (C) strict 2PL = deadlock-free  (D) basic 2PL = cascadeless

**Q154.** Deadlock in a DBMS is detected using a
(A) precedence graph  (B) wait-for graph (a cycle means deadlock)  (C) B+ tree  (D) lock table alone

**Q155.** The **precedence** graph tests ___ while the **wait-for** graph tests ___.
(A) deadlock / serializability  (B) serializability / deadlock  (C) recovery / isolation  (D) both test deadlock

**Q156.** In the **wait-die** scheme, when an **older** transaction requests a lock held by a younger one, it
(A) waits  (B) dies (rolls back)  (C) wounds the younger  (D) commits

**Q157.** In the **wound-wait** scheme, when an **older** transaction requests a lock held by a younger one, it
(A) waits  (B) dies  (C) wounds (preempts/aborts) the younger  (D) commits

**Q158.** Timestamp-ordering concurrency control is
(A) prone to deadlock  (B) deadlock-free but starvation is possible  (C) always cascadeless  (D) NP-hard to test

**Q159.** MVCC (multiversion concurrency control) ensures that
(A) readers block writers  (B) readers never block writers and writers never block readers  (C) only one version of each item exists  (D) there is no isolation

**Q160.** Which isolation level prevents **dirty reads** but still allows unrepeatable reads and phantoms?
(A) Read Uncommitted  (B) Read Committed  (C) Repeatable Read  (D) Serializable

**Q161.** The **Write-Ahead Logging (WAL)** rule states that
(A) the data page must be written before the log  (B) the log record must reach stable storage **before** the corresponding data page  (C) logging is optional  (D) commit must precede logging

**Q162.** In the **lost update** problem
(A) a transaction reads uncommitted data  (B) a phantom row appears  (C) two transactions read then write the same item and one update is overwritten and lost  (D) the same item is read twice with different values

**Q163.** A **dirty read** occurs when a transaction
(A) reads committed data  (B) reads a value written by an uncommitted transaction that later aborts  (C) reads the same item twice  (D) sees a phantom row

**Q164.** The difference between an unrepeatable read and a phantom read is
(A) there is none  (B) unrepeatable read = an existing row's value changes; phantom = new rows appear/disappear  (C) phantom = value changes; unrepeatable = new rows  (D) both concern only new rows

**Q165.** The schedule **S: r1(X) r2(X) w1(X) r3(X) w2(X)** is
(A) conflict serializable  (B) not conflict serializable (its precedence graph has a cycle T1 ⇄ T2)  (C) a serial schedule  (D) equivalent to T3, T1, T2

---

## Part N — Paper-I (English, Reasoning, GK)

**Q166.** Choose the grammatically correct sentence.
(A) Each of the students have submitted their assignment.  (B) Each of the students has submitted his assignment.  (C) Each of the student have submitted their assignment.  (D) Each of the student has submit his assignment.

**Q167.** The idiom *"a blessing in disguise"* means
(A) an obvious advantage  (B) something that seems bad at first but turns out to be good  (C) a hidden threat  (D) a religious ceremony

**Q168.** If A is the brother of B, B is the sister of C, and C is the father of D, then A is D's
(A) father  (B) uncle  (C) brother  (D) grandfather

**Q169.** A train 150 m long crosses a pole in 15 seconds. Its speed is
(A) 10 km/h  (B) 24 km/h  (C) 36 km/h  (D) 45 km/h

**Q170.** The Tripura Sundari Temple, one of the 51 Shakti Peethas, is located at
(A) Agartala  (B) Udaipur  (C) Dharmanagar  (D) Kailashahar

**Q171.** Choose the synonym of **"ephemeral"**.
(A) everlasting  (B) frequent  (C) short-lived  (D) important

**Q172.** Choose the antonym of **"benevolent"**.
(A) kind  (B) generous  (C) cheerful  (D) malevolent

**Q173.** A person who knows and can use many languages is a
(A) linguist  (B) polyglot  (C) bilingual  (D) orator

**Q174.** Find the next term: 2, 6, 12, 20, 30, ?
(A) 40  (B) 42  (C) 44  (D) 36

**Q175.** Which is the odd one out?
(A) Square  (B) Triangle  (C) Circle  (D) Rectangle

**Q176.** Find the next term: 3, 5, 9, 17, 33, ?
(A) 65  (B) 49  (C) 63  (D) 66

**Q177.** A man walks 5 km North, turns right and walks 3 km, then turns right and walks 5 km. How far is he from the start?
(A) 3 km  (B) 5 km  (C) 8 km  (D) 13 km

**Q178.** The capital of Tripura is
(A) Agartala  (B) Udaipur  (C) Aizawl  (D) Kohima

**Q179.** Tripura became a full-fledged state of the Indian Union in
(A) 1949  (B) 1956  (C) 1972  (D) 1963

**Q180.** The length of an IPv4 address is
(A) 32 bits  (B) 64 bits  (C) 128 bits  (D) 16 bits

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | C | 31 | A | 61 | B | 91 | A | 121 | C | 151 | C |
| 2 | A | 32 | B | 62 | A | 92 | C | 122 | D | 152 | B |
| 3 | B | 33 | C | 63 | C | 93 | B | 123 | B | 153 | B |
| 4 | C | 34 | A | 64 | C | 94 | A | 124 | C | 154 | B |
| 5 | D | 35 | C | 65 | D | 95 | A | 125 | B | 155 | B |
| 6 | A | 36 | B | 66 | B | 96 | B | 126 | D | 156 | A |
| 7 | B | 37 | D | 67 | C | 97 | B | 127 | C | 157 | C |
| 8 | C | 38 | C | 68 | B | 98 | C | 128 | A | 158 | B |
| 9 | D | 39 | B | 69 | A | 99 | B | 129 | B | 159 | B |
| 10 | A | 40 | B | 70 | C | 100 | B | 130 | C | 160 | B |
| 11 | B | 41 | A | 71 | B | 101 | A | 131 | A | 161 | B |
| 12 | C | 42 | B | 72 | B | 102 | B | 132 | A | 162 | C |
| 13 | A | 43 | D | 73 | C | 103 | B | 133 | D | 163 | B |
| 14 | D | 44 | B | 74 | B | 104 | B | 134 | B | 164 | B |
| 15 | B | 45 | A | 75 | B | 105 | C | 135 | B | 165 | B |
| 16 | C | 46 | B | 76 | A | 106 | B | 136 | C | 166 | B |
| 17 | A | 47 | C | 77 | B | 107 | A | 137 | B | 167 | B |
| 18 | D | 48 | D | 78 | C | 108 | A | 138 | C | 168 | B |
| 19 | B | 49 | C | 79 | B | 109 | B | 139 | B | 169 | C |
| 20 | C | 50 | A | 80 | D | 110 | C | 140 | C | 170 | B |
| 21 | A | 51 | C | 81 | B | 111 | D | 141 | C | 171 | C |
| 22 | B | 52 | A | 82 | C | 112 | B | 142 | A | 172 | D |
| 23 | D | 53 | B | 83 | B | 113 | C | 143 | C | 173 | B |
| 24 | C | 54 | A | 84 | C | 114 | B | 144 | A | 174 | B |
| 25 | D | 55 | D | 85 | D | 115 | B | 145 | B | 175 | C |
| 26 | B | 56 | B | 86 | B | 116 | C | 146 | C | 176 | A |
| 27 | A | 57 | C | 87 | B | 117 | B | 147 | A | 177 | A |
| 28 | C | 58 | B | 88 | A | 118 | B | 148 | B | 178 | A |
| 29 | B | 59 | B | 89 | B | 119 | B | 149 | A | 179 | C |
| 30 | D | 60 | C | 90 | C | 120 | C | 150 | B | 180 | A |

---

# 📝 Detailed Solutions

**Q1. (C)** In a file system every new query needs a program written for it; a DBMS provides declarative querying (SQL). Controlled redundancy, constraint-based consistency and concurrency control are all DBMS advantages.

**Q2. (A)** The conceptual (logical) level holds the whole database's logical structure — all entities, relationships and constraints — and there is exactly one per database. The external level is user views; the internal level is physical storage.

**Q3. (B)** Changing the internal schema (adding an index) without touching the conceptual schema or applications is physical data independence — the easier, routinely used form.

**Q4. (C)** Logical data independence is changing the conceptual schema (add a column, split a table) without altering external views. It is harder because views are defined on the conceptual schema.

**Q5. (D)** Logical data independence is harder to achieve because external views depend directly on the conceptual schema; physical independence is easier and routine.

**Q6. (A)** The instance is the actual data at a given moment (like an object); the schema is the structure (like a class definition).

**Q7. (B)** The schema is the structure of the database and changes rarely; the instance changes constantly.

**Q8. (C)** There is exactly one conceptual schema per database (the whole logical structure). Many external views can sit above it.

**Q9. (D)** The relational model (Codd, 1970) stores data as tables/relations and is the dominant model.

**Q10. (A)** The DBA handles administration, security, tuning and backup.

**Q11. (B)** A weak entity is drawn with a double rectangle; it cannot be identified by its own attributes alone.

**Q12. (C)** A multivalued attribute uses a double ellipse; a derived attribute uses a dashed ellipse.

**Q13. (A)** A derived attribute (e.g. Age from DateOfBirth), usually not stored, is drawn as a dashed ellipse.

**Q14. (D)** The identifying relationship linking a weak entity to its owner is a double diamond.

**Q15. (B)** The partial key of a weak entity is shown with a dashed underline (a full key uses a solid underline).

**Q16. (C)** A weak entity's primary key = owner's primary key + its own partial key; the owner's PK is also a foreign key.

**Q17. (A)** A weak entity always has total participation in its identifying relationship — it cannot exist without its owner (an existence dependency).

**Q18. (D)** Total participation is drawn as a double line; partial participation is a single line.

**Q19. (B)** "Many students take many courses" is M:N. One passport is 1:1; one department–many employees is 1:N/N:1.

**Q20. (C)** A key attribute is an ellipse with its name underlined.

**Q21. (A)** An Employee managing another Employee is a unary/recursive relationship (one entity set participates in two roles).

**Q22. (B)** Peter Chen proposed the ER model in 1976.

**Q23. (D)** IS-A hierarchies (Vehicle → Car, Truck) are specialisation/generalisation, with disjoint/overlapping and total/partial constraints.

**Q24. (C)** For a 1:N relationship, no separate table is created; the foreign key goes on the "N" (many) side, since each N-side row has exactly one partner.

**Q25. (D)** An M:N relationship needs a separate junction table, so two entities plus that table = 3 tables minimum.

**Q26. (B)** A 1:N relationship needs no separate table — the FK sits on the N side — so only 2 tables are required.

**Q27. (A)** A multivalued attribute maps to a separate table containing the entity's PK plus the attribute value (one row per value).

**Q28. (C)** The FK-placement rule generalises: the foreign key always goes on the side that has at most one partner.

**Q29. (B)** Student(RollNo,Name), Course(CourseID,Title) and the junction Enrols(RollNo,CourseID,Grade) = 3 relations for the M:N with an attribute on the relationship.

**Q30. (D)** A composite attribute is flattened into its component columns; a multivalued attribute (not composite) would need a separate table.

**Q31. (A)** A derived attribute is normally not stored; it is computed from other attributes when needed.

**Q32. (B)** Degree = number of columns (attributes). Cardinality = number of rows.

**Q33. (C)** Cardinality = number of tuples (rows). Memory hook: cardinality counts the cards (rows).

**Q34. (A)** Degree of R × S = degree(R) + degree(S) = 3 + 2 = 5 (all columns side by side).

**Q35. (C)** Cardinality of R × S = |R| × |S| = 5 × 3 = 15 (every pair).

**Q36. (B)** A candidate key is a minimal super key: removing any attribute breaks uniqueness.

**Q37. (D)** A primary key cannot be NULL (entity integrity) and must be unique; it may be composite.

**Q38. (C)** A foreign key may be NULL (meaning "no relationship yet"); primary/candidate/super keys identify rows and cannot be NULL.

**Q39. (B)** A prime attribute is part of some candidate key; a non-prime attribute is part of none.

**Q40. (B)** {RollNo,Name} uniquely identifies rows so it is a super key, but it is not minimal (it contains the smaller super key {RollNo}), so it is not a candidate key.

**Q41. (A)** A appears only on the left, so it must be in every key. A⁺ = {A}→{A,B}→{A,B,C}→{A,B,C,D} = all attributes; A alone suffices, so A is the only candidate key.

**Q42. (B)** B appears only on the left, so B is in every key. (AB)⁺ = ABC = all ✓; (BC)⁺: C→A gives A, so BC → ABC = all ✓; (AC)⁺ cannot reach B. Keys = AB and BC.

**Q43. (D)** Since B never appears on any right-hand side, B is in every candidate key (AB and BC both contain B); therefore B is prime.

**Q44. (B)** A super key is any attribute set that uniquely identifies a tuple; it need not be minimal.

**Q45. (A)** Entity integrity: the primary key cannot be NULL and must be unique.

**Q46. (B)** Referential integrity: a foreign key value must match an existing primary key value or be NULL.

**Q47. (C)** CASCADE deletes/updates the referencing child rows when the parent is deleted/updated.

**Q48. (D)** SET NULL sets the foreign key to NULL when the parent row is deleted.

**Q49. (C)** Domain integrity requires values to come from the declared domain/type.

**Q50. (A)** A child row referencing a non-existent parent is an orphan row — exactly what referential integrity prevents.

**Q51. (C)** The six primitives are σ, π, ×, ∪, −, ρ. Natural join, intersection and division are derived (e.g. R ⋈ S = π(σ(R × S))).

**Q52. (A)** The fundamental set is σ (selection), π (projection), × (product), ∪ (union), − (difference), ρ (rename).

**Q53. (B)** Projection picks columns and, because a relation is a set, removes duplicate rows.

**Q54. (A)** Selection σ picks the rows satisfying a condition; degree is unchanged.

**Q55. (D)** R ∩ S = R − (R − S), expressible with difference alone, which is why intersection is derived.

**Q56. (B)** Division answers universal ("for all") queries, e.g. students who have taken every course.

**Q57. (C)** Union, intersection and difference require union-compatible relations: same degree with corresponding attributes over the same domains.

**Q58. (B)** Relational algebra is set-based (duplicates auto-removed); SQL is bag-based (duplicates kept unless DISTINCT is used).

**Q59. (B)** When the join attribute is a key of S and a foreign key in R (no NULLs), each R-row matches exactly one S-row, so |R ⋈ S| = |R|.

**Q60. (C)** The bound is 0 ≤ |R ⋈ S| ≤ |R| × |S|: 0 if nothing matches, |R|×|S| if every row matches every row.

**Q61. (B)** TRC and DRC are declarative (they state what is wanted, not how); algebra is procedural.

**Q62. (A)** Algebra ≡ safe TRC ≡ safe DRC in expressive power — relational completeness.

**Q63. (C)** TRUNCATE is DDL. SELECT/UPDATE are DML; COMMIT is TCL.

**Q64. (C)** GRANT and REVOKE are DCL (data control language) — they manage privileges.

**Q65. (D)** COMMIT, ROLLBACK and SAVEPOINT are TCL (transaction control).

**Q66. (B)** DELETE (DML) allows a WHERE clause and is rollback-able; TRUNCATE (DDL) removes all rows, has no WHERE and is generally not rollback-able. Neither removes the table structure.

**Q67. (C)** DROP removes the rows and the table structure itself; DELETE/TRUNCATE keep the structure.

**Q68. (B)** TRUNCATE is DDL, auto-commits and is not (generally) rollback-able.

**Q69. (A)** Logical order: FROM → WHERE → GROUP BY → HAVING → SELECT → (DISTINCT) → ORDER BY → LIMIT.

**Q70. (C)** WHERE runs before grouping, so no aggregates exist yet; aggregates therefore cannot appear in WHERE (use HAVING).

**Q71. (B)** HAVING filters groups after aggregation; WHERE filters rows before grouping.

**Q72. (B)** WHERE filters rows (pre-grouping); HAVING filters groups (post-aggregation).

**Q73. (C)** SELECT runs after WHERE/GROUP BY/HAVING but before ORDER BY, so a SELECT alias is usable in ORDER BY, not in WHERE.

**Q74. (B)** COUNT(*) counts all rows = 10; COUNT(marks) ignores the 3 NULLs = 7.

**Q75. (B)** AVG divides SUM by the count of non-NULL values: 560 / 7 = 80 (not 560/10 = 56).

**Q76. (A)** COUNT(*) counts every row including those with NULLs; COUNT(column), SUM, AVG all ignore NULLs.

**Q77. (B)** Any comparison with NULL yields UNKNOWN; only TRUE rows are returned, so `= NULL` matches nothing. Use IS NULL.

**Q78. (C)** IS NULL is the correct test; `= NULL` always evaluates to UNKNOWN.

**Q79. (B)** `x NOT IN (…, NULL)` expands to `x <> … AND x <> NULL`; the NULL comparison is UNKNOWN, so no row is ever TRUE — zero rows returned. NOT EXISTS is safe.

**Q80. (D)** NOT EXISTS is safe against the NULL trap and is the recommended alternative to NOT IN.

**Q81. (B)** LEFT OUTER JOIN keeps all left rows, padding unmatched right columns with NULL.

**Q82. (C)** A correlated subquery references the outer query's columns, so it re-executes per outer row (often with EXISTS).

**Q83. (B)** UNION removes duplicates (needs a sort/hash); UNION ALL keeps duplicates and is faster.

**Q84. (C)** A view is generally not updatable if it uses GROUP BY, aggregates, DISTINCT, UNION or a multi-table join — the DBMS cannot map the update to one base-table row.

**Q85. (D)** A trigger is procedural code fired automatically on INSERT/UPDATE/DELETE (BEFORE/AFTER, row- or statement-level).

**Q86. (B)** X → Y means any two tuples that agree on X must agree on Y ("X determines Y").

**Q87. (B)** Armstrong's axioms are sound and complete: they derive exactly the FDs implied by a given set.

**Q88. (A)** The three axioms are reflexivity, augmentation and transitivity; union, decomposition and pseudo-transitivity are derived rules.

**Q89. (B)** Augmentation: if X → Y then XZ → YZ.

**Q90. (C)** By decomposition you may split the right side (X→YZ ⇒ X→Y, X→Z), but you may never split the left side.

**Q91. (A)** AB → C does not imply A → C (you cannot split the left side). ABD → C follows by augmentation; AB → CC is trivial.

**Q92. (C)** X⁺ (closure) is the set of all attributes functionally determined by X, directly or transitively.

**Q93. (B)** An attribute appearing only on the left of the FD set is determined by nothing else, so it must be in every candidate key.

**Q94. (A)** An attribute appearing only on the right is fully determined by others, so it is in no candidate key.

**Q95. (A)** A trivial FD is one where Y ⊆ X (e.g. AB → A); it always holds.

**Q96. (B)** A partial dependency is a non-prime attribute depending on only part of a candidate key — the violation removed by 2NF.

**Q97. (B)** 1NF requires every attribute to hold a single atomic value (no repeating groups or lists).

**Q98. (C)** 2NF = 1NF plus no partial dependency: no non-prime attribute depends on only part of a candidate key.

**Q99. (B)** With a single-attribute candidate key there is no "part of a key" to depend on, so the relation is automatically in 2NF.

**Q100. (B)** 3NF: for every non-trivial X → Y, X is a super key OR Y is a prime attribute.

**Q101. (A)** BCNF: for every non-trivial X → Y, X must be a super key (no exceptions).

**Q102. (B)** A relation is in 3NF but not BCNF when an FD X → Y has X not a super key but Y prime — 3NF's escape clause that BCNF removes.

**Q103. (B)** BCNF is strictly stronger than 3NF, so every BCNF relation is in 3NF (but not conversely).

**Q104. (B)** Candidate key = A (single attribute) ⇒ 2NF automatic. But B → C is transitive: B is not a super key and C is non-prime ⇒ not 3NF. Highest NF = 2NF.

**Q105. (C)** Keys AB and BC; all of A, B, C are prime, so there are no non-prime attributes ⇒ 2NF and 3NF hold. But C → A has C not a super key ⇒ BCNF fails. Highest NF = 3NF.

**Q106. (B)** A two-attribute relation R(A,B) is always in BCNF: any non-trivial FD (A→B or B→A) has a single-attribute determinant that is then a key.

**Q107. (A)** A transitive dependency: X → Y and Y → Z (Y not a super key) yields X → Z through a non-key attribute — removed by 3NF.

**Q108. (A)** A canonical/minimal cover has a single attribute on each RHS, no redundant FD, and no redundant LHS attribute.

**Q109. (B)** A decomposition is lossless iff R1 ∩ R2 is a super key of at least one fragment (i.e. R1∩R2 → R1 or → R2).

**Q110. (C)** A lossy decomposition creates spurious tuples on rejoin — rows never in the original relation.

**Q111. (D)** A 3NF decomposition can always be made both lossless and dependency preserving.

**Q112. (B)** A BCNF decomposition is always lossless but may fail to preserve dependencies.

**Q113. (C)** Dependency preservation: the FDs enforceable within individual fragments together imply (are equivalent to) the original FD set.

**Q114. (B)** 3NF is the practical stopping point because it guarantees both lossless join and dependency preservation, whereas BCNF may force loss of dependency preservation.

**Q115. (B)** A dense index has an entry for every search-key value; a sparse index has entries for only some (typically one per block).

**Q116. (C)** A sparse index typically holds one entry per block and requires the file to be sorted on that field.

**Q117. (B)** A secondary index is on a non-ordering field, so it cannot skip entries — it must be dense.

**Q118. (B)** A table can be physically sorted only one way, so at most one clustered index is possible.

**Q119. (B)** Blocking factor = ⌊block size ÷ record size⌋ = ⌊1024 / 100⌋ = 10.

**Q120. (C)** Number of blocks = ⌈records ÷ blocking factor⌉ = ⌈4000 / 10⌉ = 400.

**Q121. (C)** Hashing destroys ordering, so hash organization is poor for range queries (good for exact-match).

**Q122. (D)** Indexes speed up SELECT but must be maintained on every INSERT/UPDATE/DELETE and consume extra space.

**Q123. (B)** In a B+ tree all data (record) pointers are in the leaves; internal nodes hold keys only for routing.

**Q124. (C)** The leaves of a B+ tree are linked in a sorted list, so a range query descends once and then walks sideways.

**Q125. (B)** B+ trees win because data pointers sit in linked leaves (efficient range queries) and internal nodes carry only keys, giving higher fan-out and a shallower tree.

**Q126. (D)** In a B-tree, keys and data pointers appear in every node (internal and leaf); this lowers fan-out compared to a B+ tree.

**Q127. (C)** p·6 + (p−1)·9 ≤ 1024 ⇒ 15p − 9 ≤ 1024 ⇒ 15p ≤ 1033 ⇒ p ≤ 68.87 ⇒ p = 68.

**Q128. (A)** p·(9+7) + 6 ≤ 1024 ⇒ 16p ≤ 1018 ⇒ p ≤ 63.6 ⇒ p_leaf = 63.

**Q129. (B)** All leaves of a B+ tree are at the same level (perfectly height-balanced).

**Q130. (C)** A B+ tree grows in height only when the root splits, which keeps all leaves at the same level.

**Q131. (A)** ACID = Atomicity, Consistency, Isolation, Durability.

**Q132. (A)** Atomicity = "all or nothing"; all operations complete or none do (ensured by logging/recovery).

**Q133. (D)** Durability guarantees committed changes survive any failure (logging + stable storage).

**Q134. (B)** Isolation is ensured by the concurrency-control manager; atomicity/durability by the recovery manager.

**Q135. (B)** After its final statement but before committing, a transaction is partially committed.

**Q136. (C)** A transaction is a logical unit of work treated as a single indivisible action.

**Q137. (B)** Two operations conflict iff they are from different transactions, on the same item, with at least one write. Read–read never conflicts.

**Q138. (C)** read(A)/read(A) never conflicts — two readers do not interfere; the other three pairs involve a write.

**Q139. (B)** A schedule is conflict serializable iff its precedence graph is acyclic; a topological sort gives the equivalent serial order.

**Q140. (C)** Draw Tᵢ → Tⱼ when a conflicting pair exists with Tᵢ's operation occurring first in the schedule.

**Q141. (C)** r1(A) before w2(A) gives T1→T2; w2(A) before w1(A) gives T2→T1. The cycle T1⇄T2 means not conflict serializable.

**Q142. (A)** On A: w1(A) before r2(A) and w2(A) give T1→T2; on B: w1(B) before r2(B) gives T1→T2. Only edge T1→T2 ⇒ acyclic ⇒ serializable, equivalent to serial order T1, T2.

**Q143. (C)** View serializability is weaker/more permissive than conflict serializability but is NP-hard to test, so systems enforce conflict serializability.

**Q144. (A)** Conflict serializable ⊂ view serializable ⊂ all schedules.

**Q145. (B)** Irrecoverable: Tⱼ reads Tᵢ's uncommitted value and commits, then Tᵢ aborts — Tⱼ cannot be undone (committed) nor kept (invalid data).

**Q146. (C)** A cascadeless (ACA) schedule requires transactions to read only committed values, eliminating cascading rollback.

**Q147. (A)** Strict ⊂ Cascadeless ⊂ Recoverable ⊂ all schedules.

**Q148. (B)** In the lock matrix only S/S is compatible: an S lock can be granted while another S is held. Any pairing with X waits.

**Q149. (A)** 2PL guarantees conflict serializability but NOT freedom from deadlock (or starvation).

**Q150. (B)** After the first release (lock point), 2PL enters the shrinking phase and may acquire no more locks.

**Q151. (C)** Conservative (static) 2PL acquires all locks before starting (no hold-and-wait), so it is deadlock-free.

**Q152. (B)** Strict 2PL holds all exclusive locks until commit/abort, so nobody reads uncommitted data — cascadeless.

**Q153. (B)** Conservative 2PL is the deadlock-free variant; strict 2PL is the cascadeless variant. These two are constantly swapped in exam options.

**Q154. (B)** Deadlock is detected with a wait-for graph (Tᵢ→Tⱼ if Tᵢ waits for a lock Tⱼ holds); a cycle means deadlock.

**Q155. (B)** The precedence graph tests serializability; the wait-for graph tests deadlock — two different graphs.

**Q156. (A)** Wait-die: an older transaction requesting a younger one's lock waits; a younger requesting an older's lock dies (restarts).

**Q157. (C)** Wound-wait: an older transaction wounds (preempts) the younger; a younger requesting an older's lock waits.

**Q158. (B)** Timestamp ordering never makes transactions wait, so it is deadlock-free, but repeated restarts can cause starvation.

**Q159. (B)** MVCC keeps multiple versions, so readers never block writers and writers never block readers (used by PostgreSQL, Oracle).

**Q160. (B)** Read Committed prevents dirty reads but still allows unrepeatable reads and phantoms.

**Q161. (B)** WAL: the log record must reach stable storage before the corresponding data page, so any on-disk change is always described in the log.

**Q162. (C)** Lost update: two transactions read then write the same item, and one write overwrites the other, losing an update.

**Q163. (B)** Dirty read: a transaction reads a value written by an uncommitted transaction that later aborts.

**Q164. (B)** Unrepeatable read = an existing row's value changes between two reads; phantom read = new rows appear/disappear for the same query.

**Q165. (B)** r2(X) before w1(X) gives T2→T1; r1(X) before w2(X) gives T1→T2. Cycle T1⇄T2 ⇒ not conflict serializable.

**Q166. (B)** "Each" is singular and takes a singular verb: "Each of the student**s** **has** submitted **his** assignment." Plural noun after *of*, singular verb agreeing with *each*.

**Q167. (B)** *A blessing in disguise* = something that appears unfortunate at first but proves beneficial later.

**Q168. (B)** A and B are siblings; B is C's sister, so A is also C's sibling (brother); D is C's child, so A is D's uncle.

**Q169. (C)** Crossing a pole = covering the train's own length: 150 m in 15 s = 10 m/s = 10 × 18/5 = 36 km/h.

**Q170. (B)** The Tripura Sundari Temple (Matabari) is at Udaipur in Gomati district, one of the 51 Shakti Peethas.

**Q171. (C)** *Ephemeral* means short-lived / lasting a very short time.

**Q172. (D)** *Benevolent* (kind, well-meaning) is the opposite of *malevolent* (wishing harm).

**Q173. (B)** A polyglot knows and uses many languages; a bilingual person knows two; a linguist studies language.

**Q174. (B)** Differences are 4, 6, 8, 10, then 12: 30 + 12 = 42. (Also n(n+1): 6×7 = 42.)

**Q175. (C)** A circle is the odd one out — it has no straight sides or vertices, unlike the square, triangle and rectangle.

**Q176. (A)** Differences double: 2, 4, 8, 16, then 32: 33 + 32 = 65. (Each term = previous ×2 − 1.)

**Q177. (A)** North 5 km, then East 3 km, then South 5 km. The N and S cancel, leaving a net displacement of 3 km East, so distance from start = 3 km.

**Q178. (A)** Agartala is the capital of Tripura.

**Q179. (C)** Tripura became a full-fledged state on 21 January 1972 (it was a Union Territory earlier).

**Q180. (A)** An IPv4 address is 32 bits long (IPv6 is 128 bits).

---

## Score

| | |
|---|---|
| Part A–M (Databases, Q1–Q165) | ___ / 165 |
| Part N (Paper-I, Q166–Q180) | ___ / 15 |
| Raw total | ___ / 180 |
| After −0.33 penalty per wrong answer | ___ |

**Highest-yield revisit order** (from the notes): finding candidate keys via attribute closure → normal forms (especially 3NF vs BCNF) → conflict serializability via precedence graphs → SQL NULL/aggregate semantics → B+ tree properties and order calculation → 2PL variants → lossless decomposition → ER-to-relational mapping. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S09_Databases/` (302 questions) and `02_State_PSC_PYQs/Subject_wise/Paper2_S09_Databases/` (390 questions).
