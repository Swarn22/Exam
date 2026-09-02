# Week 5 — Algorithms

**Syllabus §6:** Searching, sorting, hashing. Asymptotic worst-case time and space complexity. Algorithm design techniques: greedy, dynamic programming and divide and conquer. Graph traversals, minimum spanning trees, shortest paths.
**Estimated marks: ~11 — the highest-density technical week**

---

## 1. ⭐ Asymptotic notation

| Notation | Meaning | Bound |
|---|---|---|
| **O(g(n))** | f grows **no faster** than g | Upper bound (≤) |
| **Ω(g(n))** | f grows **at least as fast** as g | Lower bound (≥) |
| ⭐ **Θ(g(n))** | f grows **at the same rate** as g | Tight bound (=) |
| **o(g(n))** | f grows **strictly slower** | Strict upper (<) |
| **ω(g(n))** | f grows **strictly faster** | Strict lower (>) |

📌 f(n) = O(g(n)) ⟺ ∃ c, n₀ such that 0 ≤ f(n) ≤ c·g(n) for all n ≥ n₀
📌 Θ(g) = O(g) ∩ Ω(g)

### 1.1 ⭐ Growth-rate ordering (memorise)

📌 **1 < log log n < log n < √n < n < n log n < n² < n³ < 2ⁿ < 3ⁿ < n! < nⁿ**

⚠ Common confusions:
- **√n grows faster than log n** (n^0.5 vs log n).
- **n log n is between n and n².**
- **2ⁿ ≪ n!** for large n.
- log(n!) = Θ(n log n) — by Stirling's approximation.
- Any polynomial beats any polylogarithm; any exponential beats any polynomial.

### 1.2 Cases
- **Best case:** minimum running time over inputs of size n
- **Average case:** expected time over the input distribution
- ⭐ **Worst case:** maximum — the usual guarantee, and what the syllabus names explicitly

**Amortised analysis:** average cost per operation over a worst-case *sequence* (e.g. dynamic array doubling → O(1) amortised insertion).

---

## 2. ⭐ Recurrence relations

### 2.1 ⭐⭐ Master theorem

For **T(n) = a·T(n/b) + f(n)** with a ≥ 1, b > 1, compare f(n) with **n^(log_b a)**:

| Case | Condition | Result |
|---|---|---|
| **1** | f(n) = O(n^(log_b a − ε)) — f is polynomially **smaller** | **T(n) = Θ(n^(log_b a))** |
| **2** | f(n) = Θ(n^(log_b a)) — they **match** | **T(n) = Θ(n^(log_b a) · log n)** |
| **3** | f(n) = Ω(n^(log_b a + ε)) — f is polynomially **larger** (+ regularity condition) | **T(n) = Θ(f(n))** |

⚠ The Master theorem does **not** apply when f(n) is not polynomially comparable (e.g. T(n) = 2T(n/2) + n/log n), or when a or b is not constant.

🔢 **Worked examples:**

| Recurrence | log_b a | f(n) | Case | Result |
|---|---|---|---|---|
| T(n) = 2T(n/2) + n | 1 | n | 2 | ⭐ **Θ(n log n)** — merge sort |
| T(n) = 2T(n/2) + 1 | 1 | 1 | 1 | ⭐ **Θ(n)** |
| T(n) = T(n/2) + 1 | 0 | 1 | 2 | ⭐ **Θ(log n)** — binary search |
| T(n) = 2T(n/2) + n² | 1 | n² | 3 | **Θ(n²)** |
| T(n) = 4T(n/2) + n | 2 | n | 1 | **Θ(n²)** |
| T(n) = 8T(n/2) + n² | 3 | n² | 1 | **Θ(n³)** |
| T(n) = 7T(n/2) + n² | log₂7 ≈ 2.81 | n² | 1 | **Θ(n^log₂7)** — Strassen |
| T(n) = 3T(n/4) + n log n | log₄3 ≈ 0.79 | n log n | 3 | **Θ(n log n)** |

### 2.2 Other methods
- **Substitution:** guess the answer, prove by induction.
- **Recursion tree:** sum the work at each level.
- **Subtract-and-conquer** T(n) = aT(n−b) + f(n): if a = 1 → O(n·f(n)); if a > 1 → O(aⁿ/ᵇ · f(n)).

🔢 T(n) = T(n−1) + 1 → **O(n)** · T(n) = T(n−1) + n → **O(n²)** · T(n) = 2T(n−1) + 1 → **O(2ⁿ)** (Towers of Hanoi)

---

## 3. ⭐ Searching

| Algorithm | Best | Average | Worst | Requires |
|---|---|---|---|---|
| **Linear search** | O(1) | O(n) | **O(n)** | Nothing |
| ⭐ **Binary search** | O(1) | O(log n) | ⭐ **O(log n)** | ⭐ **Sorted array** |
| Jump search | — | — | O(√n) | Sorted |
| Interpolation search | O(1) | O(log log n) | O(n) | Sorted, uniform |
| Hashing | O(1) | **O(1)** | O(n) | Hash table |

📌 Binary search worst-case comparisons = **⌈log₂(n+1)⌉**
📌 Recurrence: T(n) = T(n/2) + 1 → Θ(log n)

⚠ Binary search on a **linked list** is not O(log n) — random access is unavailable, so it degrades to O(n).

---

## 4. ⭐⭐ Sorting — the master table

**Memorise this table completely. Direct lookups from it are near-guaranteed marks.**

| Algorithm | Best | Average | ⭐ Worst | ⭐ Space | ⭐ Stable | In-place | Method |
|---|---|---|---|---|---|---|---|
| **Bubble sort** | O(n)* | O(n²) | O(n²) | O(1) | ✅ | ✅ | Exchange |
| **Selection sort** | O(n²) | O(n²) | O(n²) | O(1) | ❌ | ✅ | Selection |
| ⭐ **Insertion sort** | ⭐ **O(n)** | O(n²) | O(n²) | O(1) | ✅ | ✅ | Insertion |
| ⭐ **Merge sort** | O(n log n) | O(n log n) | ⭐ **O(n log n)** | ⭐ **O(n)** | ✅ | ❌ | Divide & conquer |
| ⭐ **Quick sort** | O(n log n) | ⭐ **O(n log n)** | ⭐ **O(n²)** | O(log n) | ❌ | ✅ | Divide & conquer |
| ⭐ **Heap sort** | O(n log n) | O(n log n) | ⭐ **O(n log n)** | ⭐ **O(1)** | ❌ | ✅ | Selection (heap) |
| **Counting sort** | O(n+k) | O(n+k) | O(n+k) | O(k) | ✅ | ❌ | Non-comparison |
| **Radix sort** | O(d(n+k)) | O(d(n+k)) | O(d(n+k)) | O(n+k) | ✅ | ❌ | Non-comparison |
| **Bucket sort** | O(n+k) | O(n+k) | O(n²) | O(n) | ✅ | ❌ | Distribution |
| **Shell sort** | O(n log n) | depends on gap | O(n²) | O(1) | ❌ | ✅ | Insertion variant |

\* with an early-exit swap flag

### 4.1 Key facts ⭐

📌 ⭐ **Lower bound for any comparison-based sort = Ω(n log n)** — from the decision tree: n! leaves ⇒ height ≥ log₂(n!) = Ω(n log n).

⭐ **Non-comparison sorts (counting, radix, bucket) beat this bound** because they use key structure, not comparisons. Counting sort needs a small integer range k.

⭐ **Stable sorts:** insertion, bubble, merge, counting, radix, bucket.
⭐ **Unstable sorts:** **quick, heap, selection**, shell.
*Stability* = equal keys retain their relative input order. It matters when sorting by multiple fields (radix sort **requires** a stable subroutine).

⭐ **In-place (O(1) extra space):** bubble, selection, insertion, heap, shell. Quick sort uses O(log n) stack. **Merge sort is not in-place** (O(n) auxiliary).

⭐ **Quick sort's worst case O(n²)** arises when the pivot is always the smallest or largest element — e.g. an **already-sorted** array with a first- or last-element pivot. Fixes: randomised pivot, median-of-three, or median-of-medians (guarantees O(n log n) but with a large constant).

⭐ **Insertion sort is O(n) on a sorted or nearly-sorted array** — it is *adaptive*, which is why it is used for small subarrays inside hybrid sorts (Timsort, introsort).

⭐ **Selection sort always does exactly n(n−1)/2 comparisons** regardless of input, but only O(n) swaps — useful when writes are expensive.

📌 Number of swaps: bubble worst = n(n−1)/2 · selection = n−1 (or fewer).
📌 Number of inversions determines insertion sort's running time: O(n + inversions).

**Merge operation:** merging two sorted arrays of sizes m and n takes **m + n − 1** comparisons in the worst case, O(m+n) time.

**External sorting** (data larger than memory): k-way merge sort using multiple passes over disk.

---

## 5. ⭐ Divide and conquer

**Three steps:** Divide → Conquer (solve subproblems recursively) → Combine.

| Algorithm | Recurrence | Complexity |
|---|---|---|
| Binary search | T(n) = T(n/2) + 1 | O(log n) |
| Merge sort | T(n) = 2T(n/2) + n | O(n log n) |
| Quick sort (avg) | T(n) = 2T(n/2) + n | O(n log n) |
| **Strassen's matrix multiplication** | T(n) = 7T(n/2) + n² | ⭐ **O(n^2.81)** vs naïve O(n³) |
| Karatsuba multiplication | T(n) = 3T(n/2) + n | O(n^1.585) |
| Closest pair of points | T(n) = 2T(n/2) + n | O(n log n) |
| Max-min finding | T(n) = 2T(n/2) + 2 | ⭐ **3n/2 − 2** comparisons |

⭐ Strassen uses **7** multiplications instead of 8 for 2×2 blocks — that is the whole trick.

---

## 6. ⭐ Greedy algorithms

**Idea:** make the locally optimal choice at each step and never reconsider.
**Requires:** the **greedy-choice property** and **optimal substructure**.

| Problem | Greedy works? | Strategy |
|---|---|---|
| ⭐ **Fractional knapsack** | ✅ **Yes** | Sort by value/weight ratio |
| ⭐ **0/1 knapsack** | ❌ **No** — needs DP | — |
| **Activity selection** | ✅ Yes | Pick the earliest **finishing** time |
| ⭐ **Huffman coding** | ✅ Yes | Merge the two lowest-frequency nodes |
| **Job sequencing with deadlines** | ✅ Yes | Sort by profit, schedule as late as possible |
| ⭐ **Prim's MST** | ✅ Yes | Cheapest edge leaving the tree |
| ⭐ **Kruskal's MST** | ✅ Yes | Cheapest edge that makes no cycle |
| ⭐ **Dijkstra's shortest path** | ✅ Yes (non-negative weights) | Closest unvisited vertex |
| Coin change (arbitrary denominations) | ❌ No | — |
| Coin change (canonical systems, e.g. INR) | ✅ Yes | Largest coin first |

### 6.1 ⭐ Huffman coding
Build a binary tree by repeatedly merging the two lowest-frequency nodes; assign 0/1 along edges.
- Produces an **optimal prefix-free code** (no codeword is a prefix of another).
- Complexity **O(n log n)** using a min-heap.
- 📌 More frequent symbols get **shorter** codes.
- 📌 Average code length = Σ (frequency × depth) / Σ frequency.

🔢 Frequencies a:5, b:9, c:12, d:13, e:16, f:45 → total weighted path length = 224, average = 224/100 = 2.24 bits/symbol.

---

## 7. ⭐⭐ Dynamic programming

⭐ **Two required properties:**
1. ⭐ **Optimal substructure** — an optimal solution is built from optimal solutions to subproblems.
2. ⭐ **Overlapping subproblems** — the same subproblem recurs many times (so memoisation pays off).

⚠ **Divide and conquer also has optimal substructure but NOT overlapping subproblems** — that is the distinguishing property.

**Two implementations:** **top-down with memoisation** (recursive + cache) and **bottom-up tabulation** (iterative).

### 7.1 ⭐ Standard DP problems

| Problem | Time | Space | Note |
|---|---|---|---|
| Fibonacci | O(n) | O(1) optimised | vs O(2ⁿ) naïve |
| ⭐ **0/1 knapsack** | ⭐ **O(nW)** | O(nW) → O(W) | **Pseudo-polynomial** |
| ⭐ **Longest Common Subsequence (LCS)** | ⭐ **O(mn)** | O(mn) | |
| Longest Increasing Subsequence | O(n²) or **O(n log n)** | O(n) | |
| Edit distance (Levenshtein) | O(mn) | O(mn) | |
| ⭐ **Matrix chain multiplication** | ⭐ **O(n³)** | O(n²) | Minimise scalar multiplications |
| ⭐ **Floyd–Warshall** (all-pairs SP) | ⭐ **O(V³)** | O(V²) | Handles negative edges |
| ⭐ **Bellman–Ford** (single-source SP) | ⭐ **O(VE)** | O(V) | Detects negative cycles |
| Coin change (min coins / count ways) | O(n × amount) | O(amount) | |
| Subset sum | O(n × sum) | O(sum) | Pseudo-polynomial |
| Travelling Salesman (Held–Karp) | O(n²·2ⁿ) | O(n·2ⁿ) | Still exponential |
| Optimal BST | O(n³) | O(n²) | |
| Rod cutting | O(n²) | O(n) | |

⚠ **0/1 knapsack is O(nW), which is pseudo-polynomial**, not polynomial — W is a *value*, so its size in bits is log W. The problem is NP-hard.

**LCS recurrence:**
```
L[i][j] = L[i-1][j-1] + 1                   if X[i] == Y[j]
        = max(L[i-1][j], L[i][j-1])         otherwise
```

**Matrix chain:** multiplying an (p×q) by a (q×r) matrix costs **p·q·r** scalar multiplications. DP finds the optimal parenthesisation.

### 7.2 Greedy vs DP vs D&C ⭐

| | **Divide & Conquer** | **Greedy** | **Dynamic Programming** |
|---|---|---|---|
| Subproblems overlap | ❌ No | — | ⭐ **Yes** |
| Choice made | Split | Locally optimal, **never revisited** | Considers **all** choices, keeps the best |
| Optimality guaranteed | Yes (for its problems) | Only when greedy-choice property holds | **Yes** |
| Typical direction | Top-down | Top-down | Bottom-up (or memoised) |
| Example | Merge sort | Fractional knapsack | 0/1 knapsack |

---

## 8. ⭐⭐ Graph algorithms

### 8.1 ⭐ Minimum spanning tree (MST)

A spanning tree with minimum total edge weight. Has exactly **V − 1** edges. Applies to **connected, undirected, weighted** graphs.

| | ⭐ **Prim's** | ⭐ **Kruskal's** |
|---|---|---|
| Approach | Grow **one tree** from a start vertex | Add globally cheapest **safe edges** |
| Picks | Cheapest edge leaving the current tree | Cheapest edge not forming a cycle |
| ⭐ **Data structure** | Priority queue (min-heap) | ⭐ **Disjoint-set (union–find)** |
| Complexity | ⭐ **O(E log V)** with binary heap; O(V²) with array; O(E + V log V) with Fibonacci heap | ⭐ **O(E log E)** = O(E log V) |
| Better for | ⭐ **Dense** graphs (using the O(V²) array version) | ⭐ **Sparse** graphs |
| Works on disconnected graphs | ❌ (gives one component) | ✅ (produces a spanning forest) |

⭐ **MST is unique if all edge weights are distinct.**
⭐ The MST always contains the **minimum-weight edge** of the graph.
⭐ **Cut property:** for any cut, the minimum-weight crossing edge belongs to some MST.
⭐ **Cycle property:** the maximum-weight edge of any cycle is not in the MST (if unique).
⚠ An MST minimises **total** weight, **not** the path between any particular pair — that is a shortest-path problem, and MST paths need not be shortest paths.

**Union–find (disjoint set):** operations `find` and `union`; with union by rank + path compression, nearly O(1) amortised (inverse Ackermann α(n)).

### 8.2 ⭐⭐ Shortest paths

| Algorithm | Solves | ⭐ Complexity | Negative edges? | Negative cycle detection | Technique |
|---|---|---|---|---|---|
| **BFS** | Single-source, **unweighted** | O(V + E) | — | — | Traversal |
| ⭐ **Dijkstra** | Single-source | ⭐ **O(E log V)** (heap); O(V²) (array) | ⭐ **❌ NO** | ❌ | **Greedy** |
| ⭐ **Bellman–Ford** | Single-source | ⭐ **O(VE)** | ⭐ **✅ Yes** | ⭐ **✅ Yes** | **DP** |
| ⭐ **Floyd–Warshall** | **All-pairs** | ⭐ **O(V³)** | ✅ Yes | ✅ Yes (negative diagonal) | **DP** |
| Johnson's | All-pairs (sparse) | O(V² log V + VE) | ✅ Yes | ✅ Yes | Reweighting |
| DAG shortest path | Single-source on a DAG | **O(V + E)** | ✅ Yes | N/A | Topological order + relax |

⭐ **Why Dijkstra fails with negative edges:** it finalises a vertex once, assuming no shorter path can later appear. A negative edge can invalidate that assumption after finalisation.

⭐ **Bellman–Ford** relaxes all E edges **V − 1** times. If any edge can still be relaxed on the **V-th** pass, a **negative cycle** exists.

⭐ **Floyd–Warshall** core loop — know the loop order (k outermost):
```
for k in V: for i in V: for j in V:
    d[i][j] = min(d[i][j], d[i][k] + d[k][j])
```

### 8.3 Traversal-based algorithms

| Task | Algorithm | Complexity |
|---|---|---|
| Connected components | BFS/DFS | O(V + E) |
| Cycle detection | DFS (back edge) or union–find | O(V + E) |
| ⭐ **Topological sort** | Kahn's (in-degree) or DFS post-order | O(V + E) — **DAG only** |
| Strongly connected components | Kosaraju (2 DFS) / Tarjan (1 DFS) | O(V + E) |
| Articulation points & bridges | DFS with discovery/low values | O(V + E) |
| Bipartiteness | BFS 2-colouring | O(V + E) |

---

## 9. Complexity classes (definitional only)

| Class | Meaning |
|---|---|
| **P** | Solvable in polynomial time by a deterministic machine |
| **NP** | ⭐ **Verifiable** in polynomial time (solvable in poly time non-deterministically) |
| ⭐ **NP-hard** | At least as hard as every problem in NP; **need not be in NP**, need not even be decidable |
| ⭐ **NP-complete** | ⭐ **In NP AND NP-hard** |

⭐ **P ⊆ NP.** Whether **P = NP** is unresolved.
⭐ **Cook–Levin theorem:** **SAT** was the first problem proved NP-complete.

**Known NP-complete:** SAT, 3-SAT, Travelling Salesman (decision), Hamiltonian cycle/path, vertex cover, clique, independent set, graph colouring, subset sum, 0/1 knapsack (decision), bin packing, set cover.
**In P:** shortest path (non-negative), MST, sorting, matching in bipartite graphs, linear programming, primality testing (AKS), Euler circuit.

⚠ **Euler circuit is in P; Hamiltonian circuit is NP-complete** — a favourite contrast.
⚠ **NP-hard does not imply NP-complete** (the halting problem is NP-hard but not in NP).

---

## 10. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| T(n) = 2T(n/2) + n | Θ(n log n) |
| T(n) = 2T(n/2) + 1 | Θ(n) |
| T(n) = T(n/2) + 1 | Θ(log n) |
| Comparison sort lower bound | Ω(n log n) |
| Quick sort worst / average | O(n²) / O(n log n) |
| Merge sort space | O(n) |
| Heap sort space | O(1) |
| Unstable sorts | Quick, heap, selection, shell |
| Insertion sort on sorted input | O(n) |
| Selection sort comparisons | n(n−1)/2 always |
| Counting sort | O(n+k), non-comparison |
| Strassen | O(n^2.81), 7 multiplications |
| Max-min comparisons | 3n/2 − 2 |
| Huffman | Greedy, O(n log n), prefix-free |
| Fractional / 0-1 knapsack | Greedy / DP |
| 0/1 knapsack complexity | O(nW), pseudo-polynomial |
| LCS | O(mn) |
| Matrix chain | O(n³) |
| DP requires | Optimal substructure + overlapping subproblems |
| Prim / Kruskal | O(E log V) / O(E log E) |
| Kruskal uses | Union–find |
| MST edges | V − 1 |
| MST unique when | All weights distinct |
| Dijkstra | O(E log V), no negative edges |
| Bellman–Ford | O(VE), detects negative cycles |
| Floyd–Warshall | O(V³), DP, all-pairs |
| Topological sort | DAG only, O(V+E) |
| NP-complete | In NP and NP-hard |
| First NP-complete problem | SAT (Cook–Levin) |

---

## 11. Common traps ⚠

1. **Build-heap O(n)** — carried over from Week 4, still asked here.
2. **Quick sort's worst case is on sorted input** with a naïve pivot, not random input.
3. **Merge sort is not in-place**; heap sort is.
4. **Quick sort is unstable; merge sort is stable.**
5. **√n > log n.**
6. **Dijkstra cannot handle negative edges** — even without a negative cycle.
7. **Bellman–Ford is O(VE), not O(V²).**
8. **Fractional knapsack = greedy; 0/1 knapsack = DP.** Reversing this is the most common error in this section.
9. **O(nW) is pseudo-polynomial**, not polynomial.
10. **NP-hard ⊅ NP** — NP-complete requires membership in NP too.
11. **Prim's is better for dense graphs, Kruskal's for sparse** — with the appropriate implementations.
12. **MST ≠ shortest path tree.**

---

## 12. Practice

- GATE: [`Paper2_S06_Algorithms/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S06_Algorithms/) — **358 questions**
- State-PSC level: [`Paper2_S06_Algorithms/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S06_Algorithms/) — **256 questions**
- Test: [`Week_05_Test.md`](../04_Mock_Tests/Week_05_Test.md)

**Priority order if short on time:** the sorting master table (§4) → Master theorem cases → Dijkstra/Bellman–Ford/Floyd–Warshall comparison → Prim vs Kruskal → greedy vs DP problem classification → asymptotic ordering → NP definitions.
