# 04 · Algorithms — Precise Notes
> **TPSC ATO (IT) Paper-II §6** · ~11 marks (estimate) · Syllabus: *"Algorithms — searching, sorting, hashing; asymptotic worst-case time and space complexity; greedy, dynamic programming, divide and conquer; graph traversals, minimum spanning trees, shortest paths"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson GATE guide (graph algorithms, BFS/DFS, hashing), Unacademy GATE PYQ notes, Made Easy class notes. Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/04_Algorithms/`.
> Cross-refs: heap structure, tree/graph representations → `03_Programming_and_Data_Structures.md` §11–12.

## Which notes are worth your time
| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 1.Algorithm.pdf | Pearson GATE guide | Typed, 2-column | 76 | 4 | Widest typed coverage — asymptotics, sorting, D&C, greedy, DP, **graph algorithms, BFS/DFS, hashing, P/NP**, practice sets with keys · dry; text extraction garbled in places |
| 2.Algo_Sanchit_Sir_Notes.pdf | Sanchit Jain (Knowledge Gate) | Typed slides | 91 | 4 | **Backbone**: asymptotics, Master theorem, sorting, hashing, greedy, DP, MST, Dijkstra/Bellman–Ford, ~150 year-tagged GATE/NET PYQs · **thin on graph traversals** (no topological sort, BFS/DFS barely covered), little on searching, no Strassen |
| 3.Algo_V1_Made_Easy_Class_Latest_Notes.pdf | Made Easy class notes | Neat handwritten scan (101 MB) | 215 | 4 | Clearest handwriting; full derivations (e.g. quick-sort partition code) · very large file |
| 4.Algorithms_Notes.pdf | Unlabelled | Clean handwriting, CamScanner | 239 | 3.5 | Step-by-step traces (e.g. Kruskal on the classic 7-vertex graph) · few PYQs |
| 5.Ace_Academy_Algo_Class_Notes.pdf | Ace Academy | Faint notebook scan | 126 | 2.5 | Multistage-graph / DP examples · faint, cramped |
| 6.Design_Analysis_and_Algorithm-CS.pdf | Wiki Engineering | Handwritten scan | 398 | 2.5 | Long; heap and complexity examples · slow to use, uneven legibility |
| 7.Algorthims_Hand_Written_Notes_Made_Easy.pdf | Made Easy (phone photos) | Photos with watermark | 158 | 3 | Good greedy walk-throughs (knapsack by profit / weight / ratio) · glare |
| 8.DAA.pdf | Unlabelled | Neat scan | 112 | 3.5 | Clean definitions (spanning trees, greedy method) · basic level |
| 9.Complete_Algorithm_Notes.pdf | Unacademy | CamScanner, PYQ walk-throughs | 87 | 4 | **Best for PYQ practice**: year-tagged GATE questions solved one per box (BFS/DFS, MST, sorting) · not a theory source |

**If you open only one PDF besides these notes:** open **Unacademy (file 9)** to practise year-tagged GATE questions, and use **Pearson (file 1)** for the graph-traversal theory that Sanchit skips.

## Topic map
| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | Asymptotic notation & growth rates | ⭐⭐⭐ | "Arrange in increasing order", "which is true: f = O(g)?", loop complexity |
| 2 | Recurrences & Master theorem | ⭐⭐⭐ | Solve T(n); recurrence of a given recursive code |
| 3 | Searching | ⭐⭐ | Binary-search comparisons; min-max / second-largest comparison counts |
| 4 | Sorting | ⭐⭐⭐ | Best/avg/worst table, stable / in-place, best algorithm for a situation, pass output |
| 5 | Hashing | ⭐⭐⭐ | Final table after linear probing / chaining; expected probes; clustering type |
| 6 | Divide & conquer | ⭐⭐ | Recurrence of merge/quick/Strassen; max-min comparisons |
| 7 | Greedy | ⭐⭐⭐ | Huffman code lengths & average; fractional knapsack value; job sequencing profit |
| 8 | Dynamic programming | ⭐⭐⭐ | LCS length, matrix-chain cost & parenthesisations, 0/1 knapsack, DP vs greedy |
| 9 | Graph traversals (BFS, DFS) | ⭐⭐ | Valid BFS/DFS order, edge types, topological sort, complexity with matrix vs list |
| 10 | Minimum spanning trees | ⭐⭐⭐ | MST weight, Prim vs Kruskal complexity, edge-in-MST properties |
| 11 | Shortest paths | ⭐⭐⭐ | Dijkstra order/distances, negative edges, Bellman–Ford, Floyd–Warshall complexity |
| 12 | P / NP (awareness) | ⭐ | Definitions only |

---

## 1. Asymptotic Analysis
### 1.1 Notations
| Notation | Meaning | Formal | Limit test (lim f/g) |
|---|---|---|---|
| f = O(g) | upper bound (≤) | f(n) ≤ c·g(n) for all n ≥ n₀ | 0 or constant |
| f = Ω(g) | lower bound (≥) | f(n) ≥ c·g(n) for all n ≥ n₀ | constant or ∞ |
| f = Θ(g) | tight (=) | c₁g ≤ f ≤ c₂g | constant c, 0 < c < ∞ |
| f = o(g) | strictly smaller (<) | for **every** c > 0 | 0 |
| f = ω(g) | strictly larger (>) | for **every** c > 0 | ∞ |

- ⭐ **Properties:** all five are transitive · O, Ω, Θ are reflexive (o, ω are not) · only Θ is symmetric · transpose: f = O(g) ⇔ g = Ω(f); f = o(g) ⇔ g = ω(f) **[Src: Sanchit p.4–8]**.
- ⚠ O is an upper bound, not "worst case", and Ω is not "best case". Worst-case running time of insertion sort is Θ(n²); you can say it is O(n²) **and** Ω(n²).
- f = Θ(g) ⇔ f = O(g) and f = Ω(g). max(f, g) = Θ(f + g).

### 1.2 ⭐ Growth-rate ordering
📌 **1 < log log n < log n < (log n)ᵏ < nᵉ (any ε > 0) < n < n log n < n² < n³ < … < 2ⁿ < 3ⁿ < n! < nⁿ**

- Base of a log does not matter: log₂ n = Θ(log₁₀ n). But the base of an **exponent** does: 2ⁿ = o(3ⁿ).
- ⭐ log(n!) = Θ(n log n) (Stirling) · n! = ω(2ⁿ), n! = o(nⁿ) · 2ⁿ⁺¹ = Θ(2ⁿ) but 2²ⁿ ≠ O(2ⁿ).
- n^(log n) = 2^(log² n) lies between every polynomial and 2ⁿ. √n vs log² n: any power of n beats any power of log n.
- 📌 **Trick:** to compare f and g, compare log f and log g. If log f = o(log g) then f = o(g). ⚠ Equal-order logs do *not* imply f = Θ(g) (n and n² have logs of the same order).
- 📌 Sums: Σi = Θ(n²) · Σi² = Θ(n³) · Σ 1/i = Θ(log n) (harmonic) · Σ log i = Θ(n log n) · Σ 2ⁱ (i ≤ log n) = Θ(n).

### 1.3 Loop patterns
| Code shape | Complexity |
|---|---|
| `for i = 1..n` · `for j = 1..i` | n(n+1)/2 = Θ(n²) |
| `for (i = 1; i < n; i *= 2)` | Θ(log n) |
| `for (i = n; i > 0; i /= 2)` · `for j = 1..i` | n + n/2 + … = Θ(n) |
| `for i = 1..n` · `for (j = 1; j < n; j += i)` | n·Hₙ = Θ(n log n) |
| `for (i = 1; i·i ≤ n; i++)` | Θ(√n) |
| `for (i = 2; i < n; i = i·i)` | Θ(log log n) |
| Independent nested loops n and log n | Θ(n log n) |

- **Space complexity** = auxiliary space; for recursion count the **maximum stack depth** × frame size (recursive binary search O(log n); naive recursive Fibonacci O(n) stack, Θ(φⁿ) time).

🎯 **How it's asked:** order five functions (GATE-2017/2008 style); "which of these is true" with Θ/o statements; complexity of a 2–3-level loop; the value returned by a loop **[Src: Sanchit p.9–12]**.

---

## 2. Recurrences & the Master Theorem
📌 **Master theorem** for T(n) = a·T(n/b) + f(n), a ≥ 1, b > 1 — compare f(n) with **n^(log_b a)** **[Src: Sanchit p.13–15]**:

| Case | Condition | Result |
|---|---|---|
| 1 | f = O(n^(log_b a − ε)) | Θ(n^(log_b a)) |
| 2 | f = Θ(n^(log_b a)) | Θ(n^(log_b a) · log n) |
| 3 | f = Ω(n^(log_b a + ε)) **and** a·f(n/b) ≤ c·f(n), c < 1 | Θ(f(n)) |

- **Extended case 2:** f = Θ(n^(log_b a) · logᵏ n) → k ≥ 0: Θ(n^(log_b a) logᵏ⁺¹ n) · k = −1: Θ(n^(log_b a) log log n) · k < −1: Θ(n^(log_b a)).
- ⚠ **Master does not apply** when a is not a constant (T(n) = n·T(n/2) + …), a < 1, the problem shrinks by subtraction (T(n − 1)), or f(n) is not polynomially separated in the basic form — e.g. 2T(n/2) + n/log n (basic form fails; the extended form gives Θ(n log log n)).

### 2.1 ⭐ Results to know by heart
| Recurrence | Solution | Where it appears |
|---|---|---|
| T(n/2) + 1 | Θ(log n) | binary search |
| T(n/2) + n | Θ(n) | quickselect best case, halving work |
| 2T(n/2) + 1 | Θ(n) | tree traversal, max-min |
| 2T(n/2) + n | Θ(n log n) | merge sort, balanced quick sort |
| 2T(n/2) + n² | Θ(n²) | |
| 3T(n/2) + n | Θ(n^log₂3) ≈ n^1.585 | Karatsuba multiplication |
| 7T(n/2) + n² | Θ(n^log₂7) ≈ n^2.81 | **Strassen** |
| 8T(n/2) + n² | Θ(n³) | D&C matrix multiply |
| T(n − 1) + 1 | Θ(n) | linear recursion |
| T(n − 1) + n | Θ(n²) | **quick sort worst case** |
| 2T(n − 1) + 1 | Θ(2ⁿ) | **Tower of Hanoi** (2ⁿ − 1 moves) |
| T(n − 1) + T(n − 2) + 1 | Θ(φⁿ), φ ≈ 1.618 | naive Fibonacci |
| T(√n) + 1 | Θ(log log n) | substitute n = 2ᵐ |
| 2T(√n) + log n | Θ(log n · log log n) | m = log n → S(m) = 2S(m/2) + m |
| T(n/3) + T(2n/3) + n | Θ(n log n) | recursion tree, depth log₃/₂ n |
| T(n/2) + T(n/4) + n | Θ(n) | fractions sum to < 1 → geometric |

- 🔢 T(n) = T(2n/3) + 1: a = 1, b = 3/2, n^(log_b a) = n⁰ = 1 = f → case 2 → **Θ(log n)** **[Src: Sanchit p.15]**.
- 🔢 T(n) = 4T(n/2) + n² log n: n^(log₂4) = n², f = n² log n → extended case 2 with k = 1 → **Θ(n² log² n)**.
- **Recursion-tree method:** cost per level × number of levels; if per-level cost shrinks geometrically, the root dominates; if it grows, the leaves dominate (n^(log_b a) leaves).

🎯 **How it's asked:** solve a recurrence (almost every paper); write the recurrence for a given recursive function and solve it; "Master theorem is not applicable to …".

---

## 3. Searching
| Method | Requirement | Time | Notes |
|---|---|---|---|
| Linear search | none | worst n comparisons, avg (n + 1)/2 (successful) | works on linked lists and unsorted data |
| ⭐ Binary search | **sorted + random access** | Θ(log n); worst **⌊log₂ n⌋ + 1** comparisons | iterative O(1) space, recursive O(log n) stack |
| Interpolation search | sorted, uniformly distributed | avg O(log log n), worst O(n) | probes by value, not by middle |
| Exponential search | sorted, unbounded | O(log i) for target at i | doubling then binary search |

- ⚠ Binary search on a **linked list** is O(n) — no random access. Use `mid = low + (high − low)/2` to avoid integer overflow.
- 📌 **Comparison counts** (asked often): max and min together — naive 2n − 2, pairwise/D&C **⌈3n/2⌉ − 2** · second largest — **n + ⌈log₂ n⌉ − 2** (tournament) · minimum comparisons to sort n keys ≥ ⌈log₂ n!⌉ (3 keys: 3; 5 keys: 7).
- **Selection** (k-th smallest): quickselect expected O(n), worst O(n²); median-of-medians worst **O(n)**.

---

## 4. Sorting
### 4.1 ⭐⭐ Master table
| Algorithm | Best | Average | Worst | Extra space | Stable | In-place |
|---|---|---|---|---|---|---|
| Bubble (with swap flag) | **n** | n² | n² | O(1) | ✅ | ✅ |
| Selection | n² | n² | n² | O(1) | ❌ | ✅ |
| Insertion | **n** | n² | n² | O(1) | ✅ | ✅ |
| Merge | n log n | n log n | n log n | **O(n)** | ✅ | ❌ |
| Quick | n log n | n log n | **n²** | O(log n) stack (O(n) worst) | ❌ | ✅ |
| Heap | n log n | n log n | n log n | O(1) | ❌ | ✅ |
| Counting | n + k | n + k | n + k | O(n + k) | ✅ | ❌ |
| Radix (LSD, base b, d digits) | d(n + b) | d(n + b) | d(n + b) | O(n + b) | ✅ | ❌ |
| Bucket | n + k | n (uniform input) | n² | O(n + k) | ✅ (if inner sort stable) | ❌ |
| Shell | n log n | gap-dependent (~n^1.25–n^1.5) | n² (Shell's gaps) | O(1) | ❌ | ✅ |

**[Src: Sanchit p.23–35; Pearson ch.2]**

### 4.2 Facts each algorithm gets asked about
- **Bubble:** after pass i, the i largest are in place; without the swap flag the best case is also Θ(n²). Worst swaps n(n − 1)/2.
- **Selection:** exactly n(n − 1)/2 comparisons always; ⭐ **at most n − 1 swaps** → best when writes are expensive.
- **Insertion:** ⭐ time = Θ(n + I), I = number of inversions → best for **nearly sorted** or small inputs; online. Max inversions n(n − 1)/2. Binary insertion sort cuts comparisons to O(n log n) but shifts stay O(n²).
- **Merge:** merging lists of sizes m and n takes at most **m + n − 1** comparisons; worst comparisons for the whole sort n⌈log₂ n⌉ − 2^⌈log₂ n⌉ + 1. Best for **linked lists** and **external sorting**. Counts inversions in O(n log n).
- **Quick:** worst Θ(n²) when the pivot is always the min/max — sorted or reverse-sorted input with first/last-element pivot, or all-equal keys with Lomuto partition **[Src: ME-class p.100]**. Any constant-fraction split (even 1 : 99) is still Θ(n log n). Randomised pivot → expected Θ(n log n).
  - 🎯 GATE-2009: pivot = (n/4)-th smallest found in O(n) → worst case **Θ(n log n)**. GATE-2014: pivot = element at the **middle position** → worst case still **O(n²)**.
- **Heap:** build-heap O(n) + (n − 1) extract-max O(log n) each. Not stable. See heap mechanics in `03` §11.
- ⭐ **Lower bound:** any comparison sort needs **Ω(n log n)** comparisons in the worst case (decision tree with n! leaves has height ≥ log₂ n!). Counting/radix/bucket beat it because they don't compare.
- **Radix:** each digit pass must use a **stable** sort (usually counting sort).

### 4.3 Which sort for which situation
| Situation | Pick |
|---|---|
| Nearly sorted / very small n | Insertion |
| Fewest swaps (costly writes) | Selection |
| Guaranteed n log n with O(1) extra space | Heap |
| Guaranteed n log n **and** stable | Merge |
| Linked list | Merge |
| Data larger than RAM | External merge sort |
| Fastest in practice on arrays | Quick (randomised) |
| Integers in a small range k | Counting |
| k-sorted array (each element ≤ k away) | Min-heap of size k + 1 → O(n log k) |
| Merge k sorted lists (total n) | Min-heap → O(n log k) |

🎯 **How it's asked:** "which is stable / in-place", "worst case of quick sort and when", "array after 2 passes of bubble/selection/insertion", "best algorithm for nearly sorted input" (GATE/NET favourites) **[Src: Unacademy file 9]**.

---

## 5. Hashing
- **Hash functions:** division h(k) = k mod m (m prime, not close to a power of 2) · multiplication h(k) = ⌊m·(kA mod 1)⌋, Knuth A ≈ 0.618 · mid-square · folding.
- 📌 **Load factor α = n/m** (keys / slots).

| Scheme | Probe sequence | Problem | Distinct probe sequences |
|---|---|---|---|
| **Chaining** | linked list per slot | long chains | — (α may exceed 1) |
| **Linear probing** | (h(k) + i) mod m | ⭐ **primary clustering** | m |
| **Quadratic probing** | (h(k) + c₁i + c₂i²) mod m | **secondary clustering** | m |
| **Double hashing** | (h₁(k) + i·h₂(k)) mod m | none (best open addressing) | Θ(m²) |

- 📌 **Chaining:** unsuccessful search Θ(1 + α), successful Θ(1 + α/2); worst case Θ(n) (all keys in one chain).
- 📌 **Open addressing (uniform hashing, α < 1):** unsuccessful ≤ **1/(1 − α)** probes; successful ≤ (1/α)·ln(1/(1 − α)). Linear probing (Knuth): successful ≈ ½(1 + 1/(1 − α)), unsuccessful ≈ ½(1 + 1/(1 − α)²).
- ⚠ In open addressing a deleted slot must be marked **"deleted"** (tombstone), not empty — otherwise later searches stop early. h₂(k) must never be 0 and should be co-prime with m.
- 🔢 **GATE-2009 (linear probing):** m = 10, h(k) = k mod 10, insert 12, 18, 13, 2, 3, 23, 5, 15 → slots 2:12 · 3:13 · 4:2 · 5:3 · 6:23 · 7:5 · 8:18 · 9:15 (0 and 1 empty) **[Src: Sanchit p.40–42]**.
- 🔢 **GATE-2014 (chaining):** 9 slots, h(k) = k mod 9, keys 5, 28, 19, 15, 20, 33, 12, 17, 10 → slot 1 holds 28, 19, 10 → max chain **3**, min **0**, average **1**.
- 🔢 100 slots, chaining, uniform hashing: P(first 3 slots all empty after 3 inserts) = **(97/100)³** (GATE-2014).

🎯 **How it's asked:** final table after insertions; which clustering a scheme suffers; expected probes for a given α; chain lengths **[Src: Sanchit p.36–46]**.

---

## 6. Divide & Conquer
- Divide into sub-problems, solve recursively, combine. Works when sub-problems are **independent** (contrast DP).

| Problem | Recurrence | Complexity |
|---|---|---|
| Binary search | T(n/2) + 1 | Θ(log n) |
| Merge sort | 2T(n/2) + n | Θ(n log n) |
| Quick sort | T(k) + T(n − k − 1) + n | Θ(n log n) avg, Θ(n²) worst |
| Max-min | 2T(n/2) + 2 | 3n/2 − 2 comparisons |
| Power aⁿ (repeated squaring) | T(n/2) + 1 | Θ(log n) multiplications |
| Karatsuba (integer multiply) | 3T(n/2) + n | Θ(n^1.585) |
| Strassen (matrix multiply) | 7T(n/2) + n² | Θ(n^2.81) — 7 multiplications instead of 8 |
| Closest pair of points | 2T(n/2) + n | Θ(n log n) |

---

## 7. Greedy Algorithms
- Make the locally best choice and never revisit it. Correct only when the problem has **greedy-choice property + optimal substructure**.

| Problem | Greedy rule | Time | Optimal? |
|---|---|---|---|
| ⭐ Fractional knapsack | take items in decreasing **p/w** | O(n log n) | ✅ |
| 0/1 knapsack | any greedy rule | — | ❌ → use DP |
| Activity selection | earliest **finish** time first | O(n log n) | ✅ |
| Job sequencing with deadlines | highest profit first, into the **latest free slot ≤ deadline** | O(n²) (O(n log n) with DSU) | ✅ |
| ⭐ Huffman coding | merge the **two smallest** frequencies | O(n log n) with a min-heap | ✅ |
| Optimal merge pattern | merge the two **smallest files** | O(n log n) | ✅ |
| Prim / Kruskal / Dijkstra | see §10–11 | | ✅ |

- 🔢 **Fractional knapsack** (M = 20; (p, w) = (25, 18), (24, 15), (15, 10)): by p/w (1.6, 1.5, 1.39) → all of item 2 + ½ of item 3 = 24 + 7.5 = **31.5**. Greedy by profit gives 28.2, by weight 31 — both sub-optimal **[Src: ME-HW p.80]**.
- 🔢 **Job sequencing** (profit, deadline): (100, 2), (19, 1), (27, 2), (25, 1), (15, 3) → slot 2 ← 100, slot 1 ← 27, (25) and (19) rejected, slot 3 ← 15 → profit **142**.
- 🔢 ⭐ **Huffman (GATE-2007):** probabilities ½, ¼, ⅛, 1/16, 1/32, 1/32 → code lengths 1, 2, 3, 4, 5, 5 → average = ½ + ½ + ⅜ + ¼ + 5/32 + 5/32 = **1.9375 bits** **[Src: Sanchit p.48–50]**.
  - 📌 Average length = Σ pᵢ·lᵢ. n symbols → n − 1 merges; the tree is a full binary tree; codes are **prefix-free**. Equal frequencies → fixed-length ⌈log₂ n⌉ codes.
- 🔢 **Optimal merge** of files 20, 30, 10, 5, 30: 5+10 = 15 → 15+20 = 35 → 30+30 = 60 → 35+60 = 95 → total record moves = 15 + 35 + 60 + 95 = **205** **[Src: Sanchit p.51]**.

---

## 8. Dynamic Programming
- Use DP when the problem has **optimal substructure** and **overlapping sub-problems**. Memoisation = top-down with a cache; tabulation = bottom-up table.
- ⚠ D&C solves **independent** sub-problems; DP reuses **overlapping** ones; greedy commits to one choice without exploring others.

| Problem | Recurrence (core) | Time | Space |
|---|---|---|---|
| Fibonacci | F(n) = F(n−1) + F(n−2) | Θ(n) (vs Θ(φⁿ) naive) | O(1) possible |
| ⭐ 0/1 knapsack | K[i][w] = max(K[i−1][w], vᵢ + K[i−1][w − wᵢ]) | **Θ(nW)** — pseudo-polynomial | Θ(nW) |
| ⭐ LCS | c[i][j] = c[i−1][j−1] + 1 if xᵢ = yⱼ, else max(c[i−1][j], c[i][j−1]) | **Θ(mn)** | Θ(mn) |
| ⭐ Matrix-chain | m[i][j] = min over k of m[i][k] + m[k+1][j] + pᵢ₋₁·pₖ·pⱼ | **Θ(n³)** | Θ(n²) |
| Subset sum | S[i][s] = S[i−1][s] ∨ S[i−1][s − aᵢ] | Θ(n·S) | Θ(n·S) |
| Coin change (min coins) | C[s] = 1 + min C[s − cᵢ] | Θ(n·S) | Θ(S) |
| Edit distance | min of insert/delete/replace | Θ(mn) | Θ(mn) |
| Longest increasing subsequence | L[i] = 1 + max L[j], j < i, aⱼ < aᵢ | Θ(n²) (n log n with binary search) | Θ(n) |
| Optimal BST | e[i][j] over roots r | Θ(n³) | Θ(n²) |
| Floyd–Warshall | §11 | Θ(V³) | Θ(V²) |
| Bellman–Ford | §11 | Θ(VE) | Θ(V) |
| Travelling salesman (DP) | over subsets | Θ(n²·2ⁿ) | Θ(n·2ⁿ) |
| Multistage graph | cost(i) = min(c(i, j) + cost(j)) | Θ(V + E) | Θ(V) |

- 🔢 **LCS** of `ABCBDAB` and `BDCABA` = **4** (e.g. BCBA) **[Src: Sanchit p.57–60]**.
- 🔢 **Matrix chain:** A 10×100, B 100×5, C 5×50 → (AB)C = 5,000 + 2,500 = **7,500** vs A(BC) = 25,000 + 50,000 = 75,000 **[Src: Sanchit p.61–64]**.
  - 📌 Number of ways to parenthesise n matrices = Catalan **C(n−1)** = (2(n−1))! / (n!·(n−1)!) → 3 matrices: 2 · 4 matrices: **5** · 5 matrices: 14.
- 🔢 **0/1 knapsack:** W = 7, items (w, v) = (1, 1), (3, 4), (4, 5), (5, 7) → best = (3, 4) + (4, 5) = **9**.
- 🔢 **Multistage graph:** greedy picks the cheapest next edge and fails; DP from the sink gives the true minimum **[Src: Ace p.65]**.

🎯 **How it's asked:** fill an LCS/knapsack cell or give the final value; minimum scalar multiplications for a 4–6 matrix chain (GATE-2016/2018 style); "which uses DP" (Floyd–Warshall, Bellman–Ford) vs "which is greedy" (Dijkstra, Prim, Kruskal, Huffman).

---

## 9. Graph Traversals (BFS, DFS)
*(Representations — adjacency matrix vs list — are in `03` §12. Sanchit barely covers this section; it is built mainly from Pearson's graph chapter.)*

| | BFS | DFS |
|---|---|---|
| Data structure | **queue** | **stack** / recursion |
| Time (adjacency list) | Θ(V + E) | Θ(V + E) |
| Time (adjacency matrix) | **Θ(V²)** | **Θ(V²)** |
| Gives | shortest paths by **edge count** in unweighted graphs, levels | discovery/finish times, edge classes |
| Used for | shortest path (unweighted), bipartite check, connected components, web crawling | **topological sort**, cycle detection, SCCs, articulation points, bridges, maze solving |

- ⭐ **BFS tree property:** in an undirected graph every non-tree edge (u, v) joins vertices whose BFS levels differ by **at most 1**, so d(u) − d(v) ∈ {−1, 0, 1} — it can **never be 2** (GATE-2015) **[Src: Unacademy p.45]**. The BFS tree from w gives shortest paths from w to **every** vertex (GATE-2014).
- ⭐ **DFS edge classes** (directed): tree, back (to an ancestor), forward (to a descendant), cross (everything else). **Undirected graphs have only tree and back edges.** A graph has a **cycle ⇔ DFS finds a back edge**.
- 📌 **Topological sort** (DAG only): order vertices by **decreasing DFS finish time**, or Kahn's algorithm (repeatedly remove an in-degree-0 vertex). Θ(V + E). A DAG can have many topological orders; a graph with a cycle has none.
- **Strongly connected components:** Kosaraju (DFS, transpose, DFS in decreasing finish order) or Tarjan — Θ(V + E).
- Connected components = number of times BFS/DFS must be restarted from an unvisited vertex.
- 🎯 GATE-2014: DFS on a graph stored as an **adjacency matrix** → **Θ(n²)**, since every row must be scanned **[Src: Unacademy p.45]**. Also asked: "which sequence is a valid BFS/DFS order" — check each next vertex is a neighbour of the right predecessor.

---

## 10. Minimum Spanning Trees
- Spanning tree of a connected graph with V vertices has **V − 1 edges**. ⭐ Complete graph Kₙ has **nⁿ⁻² spanning trees** (Cayley).
- ⭐ **Cut property:** the lightest edge crossing any cut is in some MST. **Cycle property:** the strictly heaviest edge on a cycle is in no MST.
- ⭐ All edge weights **distinct ⇒ MST is unique**. With equal weights, several MSTs may exist but they all have the **same total weight**.

| | Kruskal | Prim |
|---|---|---|
| Idea | sort edges, add the next lightest that **doesn't form a cycle** | grow **one tree**, add the lightest edge leaving it |
| Structure | union–find (disjoint sets) | priority queue |
| Time | **O(E log E) = O(E log V)** | binary heap O(E log V) · Fibonacci heap O(E + V log V) · **matrix + array O(V²)** |
| Intermediate state | a forest (may be disconnected) | always one connected tree |
| Better for | sparse graphs | dense graphs (O(V²) version) |

- 🔢 Kruskal on the classic 7-vertex graph (edges 10, 12, 14, 16, 18, 22, 24, 25, 28): add 10, 12, 14, 16 · skip 18 (cycle) · add 22 · skip 24 · add 25 → stop at 6 edges, **cost 99**; 28 is never considered **[Src: Algorithms_Notes p.120]**.
- ⚠ Adding the same constant to every edge **does not change the MST** (but can change shortest paths). Squaring positive weights doesn't change it either. An MST is **not** a shortest-path tree.
- ⚠ Prim and Kruskal can produce different MSTs when weights tie — both are still minimum.

🎯 **How it's asked:** weight of the MST of a drawn graph; "which edge sequence could Kruskal/Prim pick"; complexity comparison; true/false on MST properties (GATE PYQs collected in Sanchit p.69–82).

---

## 11. Shortest Paths
| Algorithm | Problem | Negative edges? | Technique | Time |
|---|---|---|---|---|
| BFS | single source, **unweighted** | — | traversal | Θ(V + E) |
| ⭐ **Dijkstra** | single source | ❌ (may give wrong answers) | greedy | binary heap O((V + E) log V) · array O(V²) · Fibonacci O(E + V log V) |
| ⭐ **Bellman–Ford** | single source | ✅; **detects negative cycles** | DP | **Θ(VE)** |
| DAG shortest path | single source on a DAG | ✅ | topological order + relax | Θ(V + E) |
| ⭐ **Floyd–Warshall** | **all pairs** | ✅ (no negative cycles) | DP | **Θ(V³)** time, Θ(V²) space |
| Johnson | all pairs, sparse | ✅ | Bellman–Ford + Dijkstra | O(VE log V) |

- 📌 **Relaxation:** if d[v] > d[u] + w(u, v) then d[v] = d[u] + w(u, v), parent[v] = u.
- 📌 **Bellman–Ford:** relax **all edges V − 1 times**; if any edge still relaxes on a V-th pass → a negative cycle is reachable. (Basis of distance-vector routing — see `07` §8.)
- 📌 **Floyd–Warshall:** Dᵏ[i][j] = min(Dᵏ⁻¹[i][j], Dᵏ⁻¹[i][k] + Dᵏ⁻¹[k][j]); a negative value on the diagonal ⇒ negative cycle.
- 🔢 Why Dijkstra fails with a negative edge: A→B = 1, A→C = 2, C→B = −2. Dijkstra finalises B at 1, but the true distance is 0.
- ⚠ Multiplying all weights by a positive constant keeps shortest paths; **adding** a constant can change them (paths with more edges are penalised more).
- 🎯 NET: "all-pairs shortest paths is efficiently solved using" → **dynamic programming** (Floyd–Warshall) **[Src: Sanchit p.90]**. GATE: order in which Dijkstra finalises vertices, or the distance array after k iterations **[Src: Sanchit p.83–87]**.

---

## 12. P, NP (awareness only)
- **P** = solvable in polynomial time · **NP** = a proposed solution can be **verified** in polynomial time · **NP-hard** = every NP problem reduces to it · **NP-complete** = in NP **and** NP-hard.
- NP-complete examples: SAT (Cook's theorem), 3-SAT, vertex cover, clique, Hamiltonian cycle, TSP (decision), subset sum, 0/1 knapsack (decision), graph k-colouring (k ≥ 3).
- In P: sorting, shortest paths, MST, 2-SAT, Euler circuit, bipartite check. ⚠ 0/1 knapsack's Θ(nW) DP is **pseudo-polynomial**, not polynomial.
- If any NP-complete problem is solved in polynomial time, then P = NP (still open).

---

## Last-day revision sheet
| Formula / number | Value |
|---|---|
| Growth order | 1 < log log n < log n < nᵉ < n < n log n < n² < 2ⁿ < n! < nⁿ |
| log(n!) | Θ(n log n) |
| Master: compare f(n) with | n^(log_b a) |
| T(n) = 2T(n/2) + n | Θ(n log n) |
| T(n) = T(n−1) + n | Θ(n²) |
| T(n) = 2T(n−1) + 1 | Θ(2ⁿ), Hanoi 2ⁿ − 1 moves |
| T(n) = T(√n) + 1 | Θ(log log n) |
| Strassen | 7 multiplications, Θ(n^2.81) |
| Binary search worst comparisons | ⌊log₂ n⌋ + 1 |
| Max + min comparisons | ⌈3n/2⌉ − 2 |
| Second largest | n + ⌈log₂ n⌉ − 2 |
| Comparison-sort lower bound | Ω(n log n) |
| Merge two lists (m, n) | ≤ m + n − 1 comparisons |
| Insertion sort time | Θ(n + inversions) |
| Selection sort swaps | ≤ n − 1 |
| Build-heap | O(n) |
| Load factor | α = n/m |
| Chaining search | Θ(1 + α) |
| Open addressing, unsuccessful | ≤ 1/(1 − α) probes |
| Double hashing probe sequences | Θ(m²) |
| Huffman (½, ¼, ⅛, 1/16, 1/32, 1/32) | average 1.9375 bits |
| Matrix-chain parenthesisations | Catalan C(n−1): 4 matrices → 5 |
| LCS / edit distance | Θ(mn) |
| Matrix chain | Θ(n³) |
| 0/1 knapsack | Θ(nW), pseudo-polynomial |
| Spanning-tree edges | V − 1 |
| Spanning trees of Kₙ | nⁿ⁻² |
| Kruskal | O(E log V) |
| Prim (matrix) / (heap) | O(V²) / O(E log V) |
| Dijkstra (heap) / (array) | O((V + E) log V) / O(V²) |
| Bellman–Ford | Θ(VE), V − 1 passes |
| Floyd–Warshall | Θ(V³) |
| BFS / DFS (list) / (matrix) | Θ(V + E) / Θ(V²) |

**One-liners**
1. ⭐ O = upper bound, Ω = lower bound, Θ = tight; o and ω are strict.
2. Only Θ is symmetric; o and ω are not reflexive.
3. Log base doesn't change Θ; exponent base does.
4. Master theorem doesn't apply to T(n − 1) recurrences or non-constant a.
5. ⭐ Stable: bubble, insertion, merge, counting, radix. Unstable: selection, quick, heap, shell.
6. ⭐ In-place: bubble, selection, insertion, quick, heap, shell. Not in-place: merge, counting, radix.
7. Quick sort worst case Θ(n²) on sorted input with first/last pivot; any constant-ratio split stays Θ(n log n).
8. Insertion sort is best for nearly sorted data; selection for fewest swaps.
9. Merge sort is the choice for linked lists and external sorting.
10. Heap sort: Θ(n log n) in all cases with O(1) space, but not stable.
11. Counting/radix/bucket beat n log n because they don't compare keys.
12. Linear probing → primary clustering; quadratic → secondary; double hashing → neither.
13. Open-addressing deletes need a "deleted" marker.
14. Chaining tolerates α > 1; open addressing needs α < 1.
15. Greedy is optimal for fractional knapsack, not 0/1.
16. Activity selection: sort by finish time.
17. Huffman: merge the two smallest; prefix-free codes; n − 1 merges.
18. DP needs optimal substructure + overlapping sub-problems.
19. Floyd–Warshall and Bellman–Ford are DP; Dijkstra, Prim, Kruskal, Huffman are greedy.
20. BFS gives shortest paths only for unweighted graphs.
21. Undirected DFS has only tree and back edges; back edge ⇔ cycle.
22. Topological sort exists only for DAGs — decreasing finish times.
23. BFS non-tree edge levels differ by at most 1.
24. Distinct weights ⇒ unique MST.
25. Heaviest edge on a cycle is never in an MST; lightest edge across a cut always is.
26. Adding a constant to all weights keeps the MST but may change shortest paths.
27. Kruskal grows a forest; Prim grows one tree.
28. Dijkstra fails with negative edges; Bellman–Ford handles them and detects negative cycles.
29. Matrix representation makes BFS/DFS Θ(V²).
30. 0/1 knapsack DP is pseudo-polynomial; the decision version is NP-complete.

## Dropped as outside TPSC syllabus
- Amortised analysis and advanced data structures (Fibonacci heaps beyond their complexity line, splay trees) — appear in Made Easy/Wiki-Engg scans.
- Network flow (Ford–Fulkerson), string matching (KMP, Rabin–Karp), backtracking/branch-and-bound (N-queens, graph colouring search) — present in Pearson and some scans, not named in the syllabus line.
- Formal NP-completeness proofs and reductions (kept only the §12 awareness box).
- Discrete-maths graph theory (Euler/Hamilton theorems, colouring, planarity) — discrete maths is outside this exam.

> ⚠ **Note on this file:** the reviewer agent for Algorithms stalled before writing, so this file and its source ratings were completed by the main session from Sanchit's and Pearson's text plus one sampled page of each scan. Its error audit of the sources is lighter than the other files' — every formula and worked answer here was re-derived by hand.
