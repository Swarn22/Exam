# Week 4 Mock Test — Data Structures

**Syllabus §5 (part)** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — Data Structures (Q1–Q20)

**Q1.** The postfix form of the infix expression `A + B * C` is
(A) `AB+C*`  (B) `ABC*+`  (C) `ABC+*`  (D) `A+BC*`

**Q2.** The value of the postfix expression `5 6 2 + * 12 4 / −` is
(A) 34  (B) 37  (C) 40  (D) 43

**Q3.** Which data structure is used by the compiler to implement function calls and recursion?
(A) Queue  (B) Stack  (C) Heap  (D) Graph

**Q4.** In a circular queue implemented on an array of size `n`, the "queue is full" condition is
(A) `rear == front`
(B) `(rear + 1) % n == front`
(C) `rear == n − 1`
(D) `front == 0`

**Q5.** A circular queue implemented on an array of size `n`, keeping one slot empty to distinguish full from empty, can hold at most
(A) n elements  (B) n − 1 elements  (C) n + 1 elements  (D) n/2 elements

**Q6.** The maximum number of nodes in a binary tree of height `h` (with the root at height 0) is
(A) 2ʰ  (B) 2ʰ − 1  (C) 2ʰ⁺¹ − 1  (D) 2h + 1

**Q7.** A binary tree with `n` nodes has how many NULL child pointers?
(A) n − 1  (B) n  (C) n + 1  (D) 2n

**Q8.** In a full binary tree in which every internal node has exactly two children, if there are `n` internal nodes then the number of leaf nodes is
(A) n − 1  (B) n  (C) n + 1  (D) 2n

**Q9.** Which traversal of a Binary Search Tree visits the keys in non-decreasing sorted order?
(A) Preorder  (B) Inorder  (C) Postorder  (D) Level order

**Q10.** A unique binary tree can be reconstructed from which pair of traversals?
(A) Preorder and postorder
(B) Inorder and preorder
(C) Level order and preorder only
(D) Any single traversal

**Q11.** The worst-case time complexity of searching in a Binary Search Tree containing `n` nodes is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q12.** The height of an AVL tree with `n` nodes is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q13.** In a min-heap stored as an array with the root at index 0, the children of the node at index `i` are at indices
(A) 2i and 2i + 1  (B) 2i + 1 and 2i + 2  (C) i/2 and i/2 + 1  (D) i + 1 and i + 2

**Q14.** The time complexity of building a binary heap from an unsorted array of `n` elements using `build-heap` is
(A) O(n)  (B) O(n log n)  (C) O(log n)  (D) O(n²)

**Q15.** Inserting an element into a binary heap of `n` elements takes
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q16.** For a graph with V vertices and E edges, the space required by an adjacency **matrix** and an adjacency **list** are respectively
(A) O(V + E) and O(V²)  (B) O(V²) and O(V + E)  (C) O(V²) and O(E)  (D) O(E) and O(V)

**Q17.** Breadth-First Search and Depth-First Search use, respectively,
(A) a stack and a queue
(B) a queue and a stack
(C) both a queue
(D) both a stack

**Q18.** Topological sorting is possible only for
(A) any graph
(B) a directed acyclic graph (DAG)
(C) an undirected connected graph
(D) a complete graph

**Q19.** In open addressing with **linear probing**, the phenomenon in which occupied slots form long contiguous runs is called
(A) secondary clustering  (B) primary clustering  (C) chaining  (D) rehashing

**Q20.** Which operation is O(1) in a **doubly** linked list but O(n) in a singly linked list, given only a pointer to the node to be deleted?
(A) Searching for a value
(B) Deleting that node
(C) Traversing the list
(D) Finding the length

---

## Part B — Paper-I (Q21–Q25)

**Q21.** Choose the word most nearly **opposite** in meaning to **SCARCE**.
(A) Rare  (B) Abundant  (C) Limited  (D) Insufficient

**Q22.** Fill in the blank with the correct article: *"He is ___ honest officer."*
(A) a  (B) an  (C) the  (D) no article

**Q23.** In a certain code, `TEACHER` is written as `VGCEJGT`. In the same code, `STUDENT` will be written as
(A) `UVWFGPV`  (B) `UVWEGPV`  (C) `TUVFGPV`  (D) `UWVFGPV`

**Q24.** A can complete a piece of work in 12 days and B in 18 days. Working together, they will complete it in
(A) 6 days  (B) 7.2 days  (C) 7.5 days  (D) 15 days

**Q25.** How many districts are there in Tripura at present?
(A) 4  (B) 6  (C) 8  (D) 10

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 6 | C | 11 | C | 16 | B | 21 | B |
| 2 | B | 7 | C | 12 | B | 17 | B | 22 | B |
| 3 | B | 8 | C | 13 | B | 18 | B | 23 | A |
| 4 | B | 9 | B | 14 | A | 19 | B | 24 | B |
| 5 | B | 10 | B | 15 | B | 20 | B | 25 | C |

---

**Q1 — (B).** `*` binds tighter than `+`, so the expression is A + (B*C). Postfix: operands first, then the deeper operator — `BC*` then `A BC* +` = **ABC*+**.

**Q2 — (B).** Left to right: `6 2 +` → 8; `5 8 *` → 40; `12 4 /` → 3; `40 3 −` → **37**.

**Q3 — (B).** The call stack holds activation records (return address, parameters, locals). Recursion is just nested pushes — which is why deep recursion causes stack overflow.

**Q4 — (B).** Leaving one slot empty, `(rear + 1) % n == front` means the next write would collide with the front, i.e. full. `rear == front` is then unambiguously *empty*.

**Q5 — (B).** The sacrificed slot is what makes full and empty distinguishable, so capacity is **n − 1**.

**Q6 — (C).** Level i holds at most 2ⁱ nodes; summing i = 0…h gives 2ʰ⁺¹ − 1. *(If a question defines height with the root at level 1, the answer becomes 2ʰ − 1 — always check the convention.)*

**Q7 — (C).** There are 2n child pointer slots and n − 1 of them point to real nodes (every node except the root has exactly one parent). So NULL pointers = 2n − (n − 1) = **n + 1**.

**Q8 — (C).** In a full binary tree, leaves = internal nodes + 1. It follows directly from Q7's counting argument.

**Q9 — (B).** Inorder on a BST yields sorted order — the defining property, and the basis of BST-validity questions.

**Q10 — (B).** Inorder + preorder (or inorder + postorder) uniquely determines a binary tree. **Preorder + postorder does not** for general binary trees — it cannot distinguish a single left child from a single right child.

**Q11 — (C).** A BST degenerates to a linked list when keys are inserted in sorted order, giving **O(n)**. This is exactly why AVL/red-black trees exist.

**Q12 — (B).** AVL rebalancing keeps the height at O(log n) — height ≤ ~1.44 log₂(n+2).

**Q13 — (B).** With 0-based indexing: children of `i` are `2i+1` and `2i+2`, parent is `⌊(i−1)/2⌋`. With 1-based indexing it is 2i and 2i+1 — option A is the 1-based trap.

**Q14 — (A).** Bottom-up `build-heap` is **O(n)**, not O(n log n): most nodes are near the leaves and sift down only a short distance. Inserting n elements one at a time *would* be O(n log n).

**Q15 — (B).** Insert at the end, then sift up at most the height of the heap = **O(log n)**.

**Q16 — (B).** Matrix: V² entries regardless of edge count — good for dense graphs and O(1) edge lookup. List: O(V + E) — good for sparse graphs.

**Q17 — (B).** BFS explores level by level using a **queue**; DFS goes deep using a **stack** (explicit, or the call stack via recursion).

**Q18 — (B).** A cycle makes a linear ordering impossible, so topological sort requires a **DAG**. Detecting that no valid ordering exists is equivalent to detecting a cycle.

**Q19 — (B).** Linear probing causes **primary clustering** — long runs that lengthen every subsequent probe. Quadratic probing removes primary but introduces *secondary* clustering; double hashing avoids both.

**Q20 — (B).** With a pointer to the node, a doubly linked list can splice it out in O(1) using its `prev` pointer. A singly linked list must first find the predecessor — O(n).

**Q21 — (B).** *Scarce* = insufficient, in short supply; its opposite is **abundant**. A, C and D are all synonyms.

**Q22 — (B).** *Honest* begins with a silent *h*, so it starts with a **vowel sound** — the article is **an**. The rule follows sound, not spelling.

**Q23 — (A).** Each letter shifts +2: T→V, E→G, A→C, C→E, H→J, E→G, R→T. Applying +2 to STUDENT: S→U, T→V, U→W, D→F, E→G, N→P, T→V = **UVWFGPV**.

**Q24 — (B).** In one day A does 1/12 and B does 1/18; together 1/12 + 1/18 = 3/36 + 2/36 = 5/36. Time = 36/5 = **7.2 days**.

**Q25 — (C).** Tripura has **8 districts** — West Tripura, Sepahijala, Khowai, Gomati, South Tripura, Dhalai, Unakoti and North Tripura. It was reorganised from 4 to 8 districts in January 2012.

---

## Score

| | |
|---|---|
| Part A (Data Structures) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** missed Q6–Q12 → redo tree properties and traversals (the highest-frequency DS sub-topic); missed Q13–Q15 → redo heaps; missed Q16–Q18 → redo graph representations; missed Q19 → redo hashing. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/` (370 questions).
