# Week 5 Mock Test — Algorithms

**Syllabus §6** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — Algorithms (Q1–Q20)

**Q1.** Using the Master theorem, the solution to `T(n) = 2T(n/2) + n` is
(A) Θ(n)  (B) Θ(n log n)  (C) Θ(n²)  (D) Θ(log n)

**Q2.** The solution to `T(n) = 2T(n/2) + 1`, with T(1) = 1, is
(A) Θ(n)  (B) Θ(n log n)  (C) Θ(log n)  (D) Θ(n²)

**Q3.** The worst-case and average-case time complexities of quick sort are respectively
(A) O(n log n) and O(n log n)
(B) O(n²) and O(n log n)
(C) O(n²) and O(n²)
(D) O(n log n) and O(n²)

**Q4.** Which of the following sorting algorithms is **not** stable in its standard implementation?
(A) Insertion sort  (B) Merge sort  (C) Bubble sort  (D) Quick sort

**Q5.** Heap sort has worst-case time complexity and auxiliary space complexity respectively
(A) O(n log n) and O(1)
(B) O(n log n) and O(n)
(C) O(n²) and O(1)
(D) O(n) and O(n)

**Q6.** The auxiliary space required by the standard array-based merge sort is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q7.** The lower bound on the number of comparisons required by any comparison-based sorting algorithm is
(A) Ω(n)  (B) Ω(n log n)  (C) Ω(log n)  (D) Ω(n²)

**Q8.** Counting sort achieves O(n + k) time because it
(A) uses a better pivot
(B) is not comparison-based
(C) uses divide and conquer
(D) sorts in place

**Q9.** The number of comparisons required by binary search on a sorted array of n elements in the worst case is
(A) O(n)  (B) O(log n)  (C) O(n log n)  (D) O(1)

**Q10.** Which algorithm design paradigm does Huffman coding use?
(A) Divide and conquer  (B) Dynamic programming  (C) Greedy  (D) Backtracking

**Q11.** The 0/1 knapsack problem is solved optimally by
(A) a greedy approach on value/weight ratio
(B) dynamic programming
(C) binary search
(D) breadth-first search

**Q12.** Dijkstra's algorithm fails to give correct shortest paths when the graph contains
(A) cycles  (B) negative edge weights  (C) more than 100 vertices  (D) undirected edges

**Q13.** The time complexity of the Bellman–Ford algorithm on a graph with V vertices and E edges is
(A) O(V log V)  (B) O(E log V)  (C) O(VE)  (D) O(V³)

**Q14.** The Floyd–Warshall all-pairs shortest path algorithm has time complexity
(A) O(V²)  (B) O(V³)  (C) O(VE)  (D) O(E log V)

**Q15.** Which data structure makes Kruskal's algorithm efficient for cycle detection?
(A) Priority queue only  (B) Disjoint-set (union–find)  (C) Hash table  (D) Stack

**Q16.** The time complexity of the standard dynamic-programming solution for the Longest Common Subsequence of two strings of lengths m and n is
(A) O(m + n)  (B) O(mn)  (C) O(m log n)  (D) O(2ⁿ)

**Q17.** Which two properties must a problem have for dynamic programming to apply?
(A) Optimal substructure and overlapping subproblems
(B) Optimal substructure and the greedy-choice property
(C) Overlapping subproblems and the greedy-choice property
(D) Divisibility and recursion

**Q18.** Arrange in increasing order of asymptotic growth: `n log n`, `2ⁿ`, `n²`, `log n`, `√n`
(A) log n, √n, n log n, n², 2ⁿ
(B) √n, log n, n log n, n², 2ⁿ
(C) log n, √n, n², n log n, 2ⁿ
(D) log n, n log n, √n, n², 2ⁿ

**Q19.** Prim's algorithm using a binary min-heap runs in
(A) O(V²)  (B) O(E log V)  (C) O(VE)  (D) O(E + V)

**Q20.** A problem is **NP-complete** if it is
(A) in NP and every problem in NP reduces to it in polynomial time
(B) solvable in polynomial time
(C) not in NP but NP-hard
(D) unsolvable

---

## Part B — Paper-I (Q21–Q25)

**Q21.** Identify the part containing the error: *"The list of participants (A)/ were displayed (B)/ on the notice board (C)/ yesterday morning. (D)"*
(A) A  (B) B  (C) C  (D) D

**Q22.** The idiom *"to burn the midnight oil"* means
(A) to waste resources  (B) to work or study late into the night  (C) to start a quarrel  (D) to celebrate

**Q23.** Find the missing term: 2, 6, 12, 20, 30, ___
(A) 40  (B) 42  (C) 44  (D) 46

**Q24.** A sum of ₹8,000 amounts to ₹9,680 in 2 years at simple interest. The rate of interest per annum is
(A) 9%  (B) 10.5%  (C) 12%  (D) 15%

**Q25.** Neermahal, the well-known lake palace of Tripura, is situated in the middle of which lake?
(A) Dumboor Lake  (B) Rudrasagar Lake  (C) Amarpur Lake  (D) Jampui Lake

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 6 | C | 11 | B | 16 | B | 21 | B |
| 2 | A | 7 | B | 12 | B | 17 | A | 22 | B |
| 3 | B | 8 | B | 13 | C | 18 | A | 23 | B |
| 4 | D | 9 | B | 14 | B | 19 | B | 24 | B |
| 5 | A | 10 | C | 15 | B | 20 | A | 25 | B |

---

**Q1 — (B).** a = 2, b = 2, so n^(log_b a) = n¹ = n, which matches f(n) = n. Master theorem **Case 2** → Θ(n log n). This is exactly merge sort.

**Q2 — (A).** a = 2, b = 2, n^(log_b a) = n, and f(n) = 1 is polynomially smaller. **Case 1** → Θ(n). Intuition: the work is dominated by the n leaves.

**Q3 — (B).** Worst case **O(n²)** occurs when the pivot is always the smallest or largest element (e.g. already-sorted input with a first-element pivot). Randomised pivots make the average **O(n log n)** overwhelmingly likely.

**Q4 — (D).** Quick sort's partitioning swaps distant elements and destroys the relative order of equal keys. Heap sort and selection sort are also unstable; insertion, merge, bubble and counting sort are stable.

**Q5 — (A).** Heap sort is **O(n log n)** in the worst case *and* sorts **in place** — O(1) auxiliary space. That combination is its selling point over merge sort and quick sort.

**Q6 — (C).** Standard merge sort merges into a temporary array of size n → **O(n)** auxiliary space. (In-place merge variants exist but are impractical.)

**Q7 — (B).** The decision tree for n! possible orderings has height ≥ log₂(n!) = **Ω(n log n)**.

**Q8 — (B).** Counting sort indexes directly into a count array instead of comparing elements, so the Ω(n log n) comparison bound does not apply. It needs a small integer key range k.

**Q9 — (B).** The search space halves each step → **O(log n)**, precisely ⌈log₂(n+1)⌉ comparisons in the worst case.

**Q10 — (C).** Huffman repeatedly merges the two lowest-frequency nodes — a locally optimal choice that is provably globally optimal. **Greedy.**

**Q11 — (B).** Items cannot be split, so the greedy ratio rule fails. DP over (item, capacity) gives O(nW) — pseudo-polynomial. **Fractional** knapsack, by contrast, *is* solved greedily.

**Q12 — (B).** Dijkstra assumes that once a vertex is finalised, no shorter path can appear. A negative edge violates this. Use **Bellman–Ford** for negative weights (it also detects negative cycles).

**Q13 — (C).** V − 1 relaxation passes over all E edges → **O(VE)**.

**Q14 — (B).** Three nested loops over all vertices → **O(V³)**, using O(V²) space. It is a dynamic-programming algorithm and handles negative edges (but not negative cycles).

**Q15 — (B).** Kruskal sorts edges, then uses **union–find** to test in near-constant time whether adding an edge would form a cycle.

**Q16 — (B).** Filling an (m+1) × (n+1) table with O(1) work per cell → **O(mn)**.

**Q17 — (A).** **Optimal substructure** (an optimal solution contains optimal solutions to subproblems) and **overlapping subproblems** (the same subproblem recurs, making memoisation worthwhile). The greedy-choice property is what distinguishes greedy from DP.

**Q18 — (A).** log n < √n < n log n < n² < 2ⁿ. Note √n = n^0.5 grows *faster* than log n but slower than n.

**Q19 — (B).** With a binary heap and adjacency list, Prim's is **O(E log V)** — the same bound as Kruskal's. With a simple array it is O(V²), which is actually better for dense graphs.

**Q20 — (A).** NP-complete = in NP **and** NP-hard. NP-hard alone drops the "in NP" requirement, so an NP-hard problem need not even be decidable.

**Q21 — (B).** The subject is *the list* (singular), not *participants*. It should read "The list of participants **was** displayed". The intervening prepositional phrase is a deliberate distraction.

**Q22 — (B).** *Burn the midnight oil* = work or study late into the night.

**Q23 — (B).** The terms are n(n+1): 1×2 = 2, 2×3 = 6, 3×4 = 12, 4×5 = 20, 5×6 = 30, 6×7 = **42**. (Equivalently, differences are 4, 6, 8, 10, **12**.)

**Q24 — (B).** SI = 9680 − 8000 = 1680 for 2 years. Rate = (1680 × 100)/(8000 × 2) = 168000/16000 = **10.5%**.

**Q25 — (B).** **Neermahal**, built in 1930 by Maharaja Bir Bikram Kishore Manikya, stands in the middle of **Rudrasagar Lake** at Melaghar in Sepahijala district. Rudrasagar is also a Ramsar-designated wetland.

---

## Score

| | |
|---|---|
| Part A (Algorithms) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** missed Q1/Q2 → redo recurrences and the Master theorem; missed Q3–Q9 → **build the complexity table** (best/average/worst/space/stability for every sort) and memorise it; missed Q10–Q17 → redo greedy vs DP; missed Q12–Q19 → redo graph algorithms. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S06_Algorithms/` (358 questions).
