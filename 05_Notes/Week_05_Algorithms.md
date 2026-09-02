# Week 5 — Algorithms

**Syllabus §6:** Searching, sorting, hashing. Asymptotic worst-case time and space complexity. Algorithm design techniques: greedy, dynamic programming and divide and conquer. Graph traversals, minimum spanning trees, shortest paths.
**Estimated marks: ~11 — the highest-density technical week**

---

## 💡 What this subject is about

Week 4 asked *"how do I store data?"*. This week asks *"how do I process it efficiently, and how do I prove one method is better than another?"*

Three themes:
1. **Measuring efficiency** — asymptotic notation and recurrences, so "faster" becomes a precise claim
2. **Standard algorithms** — searching, sorting, graph algorithms, with their complexities
3. **Design techniques** — divide & conquer, greedy, dynamic programming: three general strategies for inventing algorithms

⭐ For this exam, **the complexity tables are worth more marks than the algorithm details.** Direct lookups ("what is the worst case of quick sort?") are extremely common. Learn the tables cold, then understand the reasoning behind them.

---

# 1. ⭐⭐ Asymptotic notation

## 💡 The idea

You want to compare two algorithms. Timing them on your laptop is useless — a faster machine, a different compiler or a different input size changes the answer.

So instead we ask: **how does the running time GROW as the input grows?**

An algorithm taking `3n² + 100n + 500` steps and one taking `n²` steps are considered **equally good**, because for large n the `n²` term dominates everything else:

| n | 3n² | 100n | 500 | 3n² share |
|---|---|---|---|---|
| 10 | 300 | 1000 | 500 | 17% |
| 100 | 30,000 | 10,000 | 500 | 74% |
| 10,000 | 300,000,000 | 1,000,000 | 500 | 99.7% |

⭐ **So we throw away constants and lower-order terms and keep only the dominant growth rate.** `3n² + 100n + 500` becomes **O(n²)**.

⭐ **Why this is the right thing to measure:** constants depend on the machine; growth rate is a property of the *algorithm*. An O(n log n) algorithm on a slow machine will always beat an O(n²) algorithm on a fast machine, for large enough n.

## 1.1 ⭐ The five notations

| Notation | Meaning | Bound | Analogy |
|---|---|---|---|
| **O(g)** | f grows **no faster** than g | Upper (≤) | "at most" |
| **Ω(g)** | f grows **at least as fast** as g | Lower (≥) | "at least" |
| ⭐ **Θ(g)** | f grows at **the same rate** as g | Tight (=) | "exactly" |
| **o(g)** | f grows **strictly slower** | Strict upper (<) | "less than" |
| **ω(g)** | f grows **strictly faster** | Strict lower (>) | "greater than" |

📌 **Formal definition of O:** f(n) = O(g(n)) if there exist constants **c > 0** and **n₀** such that `0 ≤ f(n) ≤ c·g(n)` for all `n ≥ n₀`.

💡 In words: *beyond some point n₀, f never exceeds a constant multiple of g.*

📌 **Θ(g) = O(g) ∩ Ω(g)** — both an upper and a lower bound.

⚠ ⭐ **O is an upper bound, so technically n = O(n²) is TRUE** (n does grow no faster than n²) — it is just not *tight*. When an exam asks for "the complexity", it usually wants the tightest bound.

## 1.2 ⭐⭐ The growth-rate ordering — memorise this

📌 ⭐ **1 < log log n < log n < √n < n < n log n < n² < n³ < 2ⁿ < 3ⁿ < n! < nⁿ**

**Concrete feel for the difference** (approximate operations for n = 1,000,000):

| Complexity | Operations | Feels like |
|---|---|---|
| O(log n) | 20 | Instant |
| O(√n) | 1,000 | Instant |
| O(n) | 1,000,000 | Instant |
| O(n log n) | 20,000,000 | Fraction of a second |
| O(n²) | 10¹² | ~15 minutes |
| O(2ⁿ) | 10³⁰¹⁰³⁰ | Longer than the universe has existed |

⭐ **This is why the O(n log n) vs O(n²) sorting distinction matters so much in practice.**

⚠ ⭐ **Common confusions:**
- **√n grows FASTER than log n.** (√n = n^0.5 is polynomial; log n is not.)
- **n log n sits between n and n².**
- **2ⁿ ≪ n!** for large n.
- **log(n!) = Θ(n log n)** (by Stirling's approximation) — this is the source of the sorting lower bound.
- Any **polynomial** beats any **polylogarithm**; any **exponential** beats any polynomial.
- The **base of a logarithm does not matter** in big-O: log₂n and log₁₀n differ by a constant factor, so both are O(log n).

## 1.3 Cases and amortised analysis

- **Best case** — the luckiest input (rarely useful)
- **Average case** — expected over the input distribution (often hard to analyse)
- ⭐ **Worst case** — the guarantee. ⭐ **This is what the syllabus names explicitly and what exams usually mean.**

⭐ **Amortised analysis** — the average cost per operation over a worst-case **sequence** of operations.
🔢 A dynamic array (`vector`, `ArrayList`) doubles its capacity when full. Most insertions are O(1); the occasional doubling is O(n). But over n insertions, the total doubling work is n + n/2 + n/4 + … ≈ 2n, so the **amortised** cost per insertion is **O(1)**.

⚠ **Amortised ≠ average case.** Amortised is a worst-case guarantee over a sequence; average case is a probabilistic statement about inputs.

---

# 2. ⭐⭐ Recurrence relations

## 💡 The idea

A recursive algorithm's running time is naturally expressed as a **recurrence** — the time for size n in terms of the time for smaller sizes.

🔢 Merge sort splits the array in two, sorts each half recursively, then merges in O(n):
```
T(n) = 2·T(n/2)  +  n
       ↑            ↑
   two recursive   merging cost
   calls on n/2
```
Solving this recurrence gives the algorithm's complexity.

## 2.1 ⭐⭐ The Master theorem

For recurrences of the form **T(n) = a·T(n/b) + f(n)** with a ≥ 1, b > 1:

💡 **The intuition:** you are comparing two costs.
- **n^(log_b a)** = the total work done at the **leaves** (all the recursive calls at the bottom)
- **f(n)** = the work done at the **root** (the combining step)

Whichever dominates determines the answer.

| Case | Condition | ⭐ Result | 💡 Meaning |
|---|---|---|---|
| **1** | f(n) is polynomially **smaller** than n^(log_b a) | **Θ(n^(log_b a))** | Leaves dominate |
| **2** | f(n) **equals** n^(log_b a) | **Θ(n^(log_b a) · log n)** | Every level costs the same; multiply by the number of levels (log n) |
| **3** | f(n) is polynomially **larger** (+ regularity condition) | **Θ(f(n))** | The root dominates |

📌 **How to apply it in the exam, in three steps:**
1. Read off **a** (number of recursive calls) and **b** (division factor)
2. Compute **n^(log_b a)**
3. Compare with f(n) → pick the case

⚠ The Master theorem does **not** apply when f(n) is not polynomially comparable to n^(log_b a) (e.g. `T(n) = 2T(n/2) + n/log n`), or when a or b is not constant.

## 2.2 🔢 Worked examples — the table to know

| Recurrence | a, b | n^(log_b a) | f(n) | Case | ⭐ Answer |
|---|---|---|---|---|---|
| **T(n) = 2T(n/2) + n** | 2, 2 | n¹ = n | n | **2** (equal) | ⭐ **Θ(n log n)** — *merge sort* |
| **T(n) = 2T(n/2) + 1** | 2, 2 | n | 1 | **1** (f smaller) | ⭐ **Θ(n)** |
| **T(n) = T(n/2) + 1** | 1, 2 | n⁰ = 1 | 1 | **2** (equal) | ⭐ **Θ(log n)** — *binary search* |
| **T(n) = 2T(n/2) + n²** | 2, 2 | n | n² | **3** (f larger) | **Θ(n²)** |
| **T(n) = 4T(n/2) + n** | 4, 2 | n² | n | **1** | **Θ(n²)** |
| **T(n) = 8T(n/2) + n²** | 8, 2 | n³ | n² | **1** | **Θ(n³)** |
| **T(n) = 7T(n/2) + n²** | 7, 2 | n^2.81 | n² | **1** | **Θ(n^log₂7) ≈ Θ(n^2.81)** — *Strassen* |
| **T(n) = 3T(n/4) + n log n** | 3, 4 | n^0.79 | n log n | **3** | **Θ(n log n)** |
| **T(n) = 9T(n/3) + n** | 9, 3 | n² | n | **1** | Θ(n²) |

### 🔢 Detailed walkthrough — T(n) = 2T(n/2) + n

1. a = 2, b = 2
2. log_b a = log₂2 = 1 → n^1 = **n**
3. f(n) = n. They are **equal** → **Case 2**
4. Answer: **Θ(n^1 · log n) = Θ(n log n)** ✅

💡 **Intuition check via the recursion tree:**
```
Level 0:   n                          work = n
Level 1:   n/2 + n/2                  work = n
Level 2:   n/4 + n/4 + n/4 + n/4      work = n
...
There are log₂n levels, each costing n  →  n log n  ✅
```

## 2.3 Other methods

**Substitution:** guess the answer, prove it by induction.
**Recursion tree:** draw the tree and sum the work per level (as above) — the most intuitive method.

**Subtract-and-conquer** `T(n) = a·T(n − b) + f(n)`:
- if a = 1 → O(n · f(n))
- if a > 1 → O(aⁿ/ᵇ · f(n))

🔢 Standard results to recognise instantly:

| Recurrence | ⭐ Answer | Example |
|---|---|---|
| T(n) = T(n−1) + 1 | **O(n)** | Linear search, factorial |
| T(n) = T(n−1) + n | **O(n²)** | Insertion/selection sort |
| T(n) = 2T(n−1) + 1 | **O(2ⁿ)** | Towers of Hanoi |
| T(n) = T(n/2) + 1 | **O(log n)** | Binary search |
| T(n) = T(n−1) + T(n−2) | **O(2ⁿ)** | Naïve Fibonacci |

---

# 3. ⭐ Searching

## 💡 The idea

**Linear search:** check every element until you find it. Works on any data. O(n).

**Binary search:** requires **sorted** data. Compare with the middle element; the answer is in one half, so **discard the other half**. Repeat.

🔢 **Search for 40 in `[10, 20, 30, 40, 50, 60, 70]`:**
```
low=0, high=6 → mid=3 → A[3]=40 = target ✅  (1 comparison!)
```
🔢 **Search for 60:**
```
low=0, high=6 → mid=3 → A[3]=40 < 60 → search right half, low=4
low=4, high=6 → mid=5 → A[5]=60 ✅
```

⭐ **Why O(log n):** each step halves the search space. Starting with n, after k steps you have n/2ᵏ. You stop when that reaches 1, so k = log₂n.

| Algorithm | Best | Average | ⭐ Worst | Requires |
|---|---|---|---|---|
| **Linear search** | O(1) | O(n) | **O(n)** | Nothing |
| ⭐ **Binary search** | O(1) | O(log n) | ⭐ **O(log n)** | ⭐ **Sorted array** |
| Jump search | — | — | O(√n) | Sorted |
| Interpolation search | O(1) | O(log log n) | O(n) | Sorted **and uniformly distributed** |
| Hashing | O(1) | **O(1)** | O(n) | A hash table |

📌 ⭐ **Binary search worst-case comparisons = ⌈log₂(n+1)⌉**
🔢 n = 1000 → ⌈log₂1001⌉ = **10** comparisons. n = 1,000,000 → **20**.

⚠ ⭐ **Binary search on a LINKED LIST is not O(log n)** — you cannot jump to the middle without walking there, so it degrades to O(n). Binary search needs **random access**.

---

# 4. ⭐⭐⭐ Sorting

> ⭐ **The master table in §4.3 is the single highest-value thing in this file.** Direct lookups from it are near-guaranteed marks. Learn it completely.

## 4.1 💡 How each algorithm actually works

### Bubble sort — repeatedly swap adjacent out-of-order pairs
Each pass "bubbles" the largest remaining element to the end.
🔢 `[5, 2, 9, 1]` → pass 1: `[2,5,1,9]` → pass 2: `[2,1,5,9]` → pass 3: `[1,2,5,9]`
⭐ With an **early-exit flag** (stop if a pass makes no swaps), the best case on already-sorted input is **O(n)**.

### Selection sort — repeatedly find the minimum and put it in place
🔢 `[5,2,9,1]` → find min (1), swap to front: `[1,2,9,5]` → find min of rest (2), already placed → `[1,2,9,5]` → find min (5), swap: `[1,2,5,9]`
⭐ **Always does exactly n(n−1)/2 comparisons**, whatever the input — it cannot detect that the array is already sorted. But it does only **O(n) swaps**, which makes it useful when *writes* are expensive (e.g. flash memory).

### ⭐ Insertion sort — insert each element into its correct place among those already sorted
💡 **Exactly how you sort a hand of playing cards.**
🔢 `[5,2,9,1]` → take 2, insert before 5: `[2,5,9,1]` → take 9, already in place: `[2,5,9,1]` → take 1, insert at front: `[1,2,5,9]`
⭐ **Best case O(n)** on sorted input, because each element's inner loop exits immediately. ⭐ This **adaptivity** is why insertion sort is used for small subarrays inside hybrid sorts (Timsort, introsort).

### ⭐ Merge sort — divide, sort each half, merge
```
        [38, 27, 43, 3, 9, 82, 10]
        /                        \
   [38,27,43]                 [3,9,82,10]
     /     \                   /        \
  [38]  [27,43]            [3,9]      [82,10]
          /   \             / \        /   \
       [27]  [43]         [3] [9]   [82]  [10]
   ── merge back up, always taking the smaller head ──
        [3, 9, 10, 27, 38, 43, 82]
```
⭐ **O(n log n) in ALL cases** — the splitting is oblivious to the data, so there is no bad input. ❌ Needs **O(n) auxiliary space** for merging.

### ⭐ Quick sort — pick a pivot, partition, recurse
```
[38, 27, 43, 3, 9, 82, 10]   pivot = 38
 → partition into [27,3,9,10] | 38 | [43,82]
 → recurse on each side
```
⭐ **Average O(n log n)** and **in-place** — in practice usually the fastest general sort, because its inner loop is very tight and cache-friendly.

⚠⚠ **Worst case O(n²)** when the pivot is always the **smallest or largest** element, so the partition is 1 : n−1 instead of roughly half and half:
```
Already-sorted input with a first-element pivot:
[1,2,3,4,5] → pivot 1 → [] | 1 | [2,3,4,5]
              → pivot 2 → [] | 2 | [3,4,5]      ... n levels, O(n) work each = O(n²)
```
⭐ **Fixes:** randomised pivot · median-of-three · median-of-medians (guarantees O(n log n) but with a large constant).

### ⭐ Heap sort — build a max-heap, then repeatedly extract the maximum
Build-heap is O(n); n extractions cost O(log n) each → **O(n log n)**.
⭐ **The only comparison sort that is both O(n log n) worst case AND in-place (O(1) space).** That is its selling point.

### Counting sort — count occurrences, then write out
🔢 Sort `[4,2,2,8,3,3,1]` with keys 0–8: build counts `[0,1,2,2,1,0,0,0,1]`, then output each value that many times → `[1,2,2,3,3,4,8]`.
⭐ **O(n + k)** where k is the key range. Not comparison-based.

### Radix sort — sort by each digit in turn, least significant first
🔢 `[170, 45, 75, 90, 802, 24, 2, 66]`
→ by units: `[170, 90, 802, 2, 24, 45, 75, 66]`
→ by tens: `[802, 2, 24, 45, 66, 170, 75, 90]`
→ by hundreds: `[2, 24, 45, 66, 75, 90, 170, 802]` ✅
⚠ ⭐ **Radix sort REQUIRES a stable subroutine** (usually counting sort) — otherwise the ordering achieved in earlier passes is destroyed.

## 4.2 ⭐⭐ Two concepts that get asked directly

### 💡 Stability

📌 ⭐ **A sort is STABLE if elements with equal keys keep their original relative order.**

🔢 Sort these records by **marks**:
```
Input:   (Amit,80)  (Beena,75)  (Chetan,80)
Stable:  (Beena,75) (Amit,80)   (Chetan,80)   ← Amit still before Chetan ✅
Unstable:(Beena,75) (Chetan,80) (Amit,80)     ← order flipped ❌
```

⭐ **Why it matters:** to sort by *"department, then by name"*, you sort by name first and then **stably** by department. Stability preserves the name ordering within each department. Without it you would need a compound comparator.

⭐ **STABLE:** insertion, bubble, merge, counting, radix, bucket
⭐ **UNSTABLE:** ⭐ **quick, heap, selection**, shell

💡 **Why quick sort is unstable:** partitioning swaps elements that are far apart, so two equal keys can be reordered.
💡 **Why heap sort is unstable:** the heap structure moves elements arbitrarily.

### 💡 In-place

📌 A sort is **in-place** if it uses **O(1)** extra space (beyond the input array).

⭐ **In-place:** bubble, selection, insertion, heap, shell. Quick sort uses O(log n) recursion stack — usually still counted as in-place.
⭐ **NOT in-place:** ⭐ **merge sort** (needs O(n) for merging), counting, radix, bucket.

## 4.3 ⭐⭐⭐ The master table

| Algorithm | Best | Average | ⭐ **Worst** | ⭐ **Space** | ⭐ **Stable** | In-place | Method |
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
| **Shell sort** | O(n log n) | Depends on gap sequence | O(n²) | O(1) | ❌ | ✅ | Insertion variant |

\* with an early-exit swap flag

### ⭐⭐ The Ω(n log n) lower bound

📌 ⭐ **Any COMPARISON-BASED sorting algorithm requires Ω(n log n) comparisons in the worst case.**

💡 **Why — the decision-tree argument:**
There are **n!** possible orderings of n elements. Each comparison has 2 outcomes, so a comparison-based algorithm is a **binary decision tree** whose leaves are the n! possible answers.
A binary tree with n! leaves has height ≥ **log₂(n!)**, and by Stirling's approximation log₂(n!) = Θ(n log n).
⭐ Since the height is the worst-case number of comparisons, no comparison sort can beat Ω(n log n). ✅

⭐ **Counting, radix and bucket sort beat this bound** — because they are **not comparison-based**. They exploit the *structure* of the keys (integers in a known small range), so the decision-tree argument does not apply. The price is that they only work for such keys, and need extra space.

📌 **Other exact counts worth knowing:**
- Selection sort: exactly **n(n−1)/2** comparisons, always; at most n−1 swaps
- Bubble sort worst case: n(n−1)/2 comparisons and swaps
- ⭐ Insertion sort runs in **O(n + inversions)** — an *inversion* is a pair out of order, so nearly-sorted arrays are nearly linear
- ⭐ Merging two sorted arrays of sizes m and n takes at most **m + n − 1** comparisons

**External sorting** — when the data does not fit in memory, use a **k-way merge sort** with multiple passes over disk, minimising I/O.

---

# 5. ⭐ Divide and conquer

## 💡 The idea

📌 **Three steps: DIVIDE the problem into smaller subproblems → CONQUER them recursively → COMBINE the results.**

💡 **Why it works:** if combining is cheap relative to the problem size, breaking the problem down repeatedly reduces total work. Merge sort's combine step is O(n) but there are only log n levels, giving O(n log n) instead of O(n²).

| Algorithm | Recurrence | ⭐ Complexity |
|---|---|---|
| Binary search | T(n) = T(n/2) + 1 | O(log n) |
| Merge sort | T(n) = 2T(n/2) + n | O(n log n) |
| Quick sort (average) | T(n) = 2T(n/2) + n | O(n log n) |
| ⭐ **Strassen's matrix multiplication** | T(n) = **7**T(n/2) + n² | ⭐ **O(n^2.81)** vs naïve O(n³) |
| Karatsuba multiplication | T(n) = 3T(n/2) + n | O(n^1.585) |
| Closest pair of points | T(n) = 2T(n/2) + n | O(n log n) |
| ⭐ **Max-min finding** | T(n) = 2T(n/2) + 2 | ⭐ **3n/2 − 2** comparisons |

### 💡 Strassen's trick

Multiplying two n×n matrices naïvely needs 8 multiplications of (n/2)×(n/2) blocks → T(n) = 8T(n/2) + n² = O(n³).
⭐ **Strassen found a way to do it with only 7 multiplications** (plus more additions, which are cheap). T(n) = 7T(n/2) + n² → **O(n^log₂7) = O(n^2.81)**.
⭐ **Exam fact: Strassen uses 7 multiplications instead of 8.**

### 💡 Max-min in 3n/2 − 2 comparisons
Naïvely, finding both the max and min takes 2n − 2 comparisons. Instead, compare elements in **pairs** first (n/2 comparisons), then feed only the larger of each pair into the max hunt and the smaller into the min hunt.
Total = n/2 + (n/2 − 1) + (n/2 − 1) = ⭐ **3n/2 − 2** ✅

---

# 6. ⭐⭐ Greedy algorithms

## 💡 The idea

📌 **At each step, make the choice that looks best RIGHT NOW, and never reconsider.**

💡 **Analogy:** giving change with the fewest coins. Facing ₹87, you take the largest coin not exceeding it (₹50), then repeat with ₹37, and so on. You never go back and rethink.

⭐ **Greedy is fast and simple — but it is only CORRECT for certain problems.** It needs:
1. ⭐ **Greedy-choice property** — a locally optimal choice is part of some globally optimal solution
2. **Optimal substructure** — the remaining problem, after that choice, is a smaller instance of the same problem

## 6.1 ⭐⭐ Where greedy works — and where it fails

| Problem | ⭐ Greedy works? | Strategy |
|---|---|---|
| ⭐ **Fractional knapsack** | ⭐ **✅ YES** | Sort by **value/weight ratio**, take greedily, split the last item |
| ⭐ **0/1 knapsack** | ⭐ **❌ NO — needs DP** | — |
| **Activity selection** | ✅ Yes | Always pick the activity with the **earliest FINISH time** |
| ⭐ **Huffman coding** | ✅ Yes | Repeatedly merge the two **lowest-frequency** nodes |
| **Job sequencing with deadlines** | ✅ Yes | Sort by profit; schedule each as **late as possible** |
| ⭐ **Prim's MST** | ✅ Yes | Cheapest edge leaving the current tree |
| ⭐ **Kruskal's MST** | ✅ Yes | Cheapest edge that creates no cycle |
| ⭐ **Dijkstra's shortest path** | ✅ Yes (non-negative weights only) | Closest unvisited vertex |
| **Coin change (arbitrary denominations)** | ❌ No | — |
| Coin change (canonical systems like INR) | ✅ Yes | Largest coin first |

### 🔢⭐ Why greedy FAILS for 0/1 knapsack — the key example

Capacity **10 kg**. Items:

| Item | Value | Weight | Ratio |
|---|---|---|---|
| A | ₹60 | 5 kg | 12 |
| B | ₹50 | 5 kg | 10 |
| C | ₹100 | 10 kg | 10 |

**Greedy by ratio:** take A (ratio 12) → 5 kg left → take B (ratio 10) → total value **₹110**.
**Optimal:** take C alone → total value **₹100**… wait, that is worse. Let us use a clearer instance.

Capacity **10 kg**:

| Item | Value | Weight | Ratio |
|---|---|---|---|
| A | ₹60 | 6 kg | 10 |
| B | ₹50 | 5 kg | 10 |
| C | ₹50 | 5 kg | 10 |

**Greedy** takes A first (6 kg), leaving 4 kg — not enough for B or C. Total = **₹60**.
**Optimal** takes B and C (10 kg exactly). Total = **₹100** ✅

⭐ **The problem is indivisibility.** Greedy commits to A and then cannot undo that choice when it turns out to block a better combination. **Fractional** knapsack has no such trap — you can always fill the remaining capacity with a fraction of the next item, so greedy is provably optimal there.

⭐ **Exam statement: fractional knapsack = greedy; 0/1 knapsack = dynamic programming.** Reversing this is the most common error in the whole Algorithms section.

### 🔢 Why coin change can fail
Denominations {1, 3, 4}, target **6**.
**Greedy:** 4 + 1 + 1 = **3 coins**.
**Optimal:** 3 + 3 = **2 coins** ✅
Greedy fails for arbitrary denominations, though it happens to work for the Indian and most real currency systems (which are designed to be "canonical").

## 6.2 ⭐ Huffman coding

### 💡 The idea

Fixed-length encoding gives every character the same number of bits — wasteful when some characters are far more common than others. **Huffman coding** gives ⭐ **frequent characters SHORT codes and rare ones LONG codes**.

⭐ It produces a **prefix-free code** — no codeword is a prefix of another — so the decoder never needs delimiters and can decode unambiguously left to right.

**Algorithm:** put every character in a min-heap keyed by frequency. Repeatedly **remove the two smallest**, merge them into a node whose frequency is their sum, and reinsert. Label left edges 0 and right edges 1.

📌 **Complexity O(n log n)** with a min-heap.

### 🔢 Worked example

Frequencies: a:5, b:9, c:12, d:13, e:16, f:45 (total 100)

```
Merge 5+9 = 14        → {12, 13, 14, 16, 45}
Merge 12+13 = 25      → {14, 16, 25, 45}
Merge 14+16 = 30      → {25, 30, 45}
Merge 25+30 = 55      → {45, 55}
Merge 45+55 = 100     → done
```
Resulting code lengths: f = 1 bit; c, d = 3 bits; a, b, e = 4 bits.

📌 **Total encoded bits = Σ (frequency × code length)**
= 45(1) + 12(3) + 13(3) + 5(4) + 9(4) + 16(4)
= 45 + 36 + 39 + 20 + 36 + 64 = **224 bits**

📌 **Average code length = 224/100 = 2.24 bits/character** — compared with 3 bits for fixed-length encoding of 6 symbols. ⭐ A 25% saving.

---

# 7. ⭐⭐⭐ Dynamic programming

## 💡 The idea

Recall naïve Fibonacci from Week 3: it recomputes `fib(3)` many times over. **Dynamic programming** is the fix — **solve each subproblem once and store the answer**.

📌 ⭐ **Two properties a problem MUST have for DP to apply:**

⭐ **1. Optimal substructure** — an optimal solution is built from optimal solutions to subproblems.
🔢 The shortest path from A to C via B contains the shortest path from A to B. ✅

⭐ **2. Overlapping subproblems** — the same subproblem is encountered **many times**, so caching pays.
🔢 fib(5) calls fib(3) twice, fib(2) three times. ✅

⚠⚠ ⭐ **Divide & conquer also has optimal substructure — but NOT overlapping subproblems.** Merge sort's two halves are completely distinct; caching would gain nothing. ⭐ **Overlapping subproblems is what distinguishes DP from divide & conquer**, and it is the standard exam question.

### ⭐ Two implementation styles

| Style | How | Note |
|---|---|---|
| **Top-down (memoisation)** | Recursive, with a cache checked at entry | Natural to write; only computes what is needed |
| **Bottom-up (tabulation)** | Iterative, filling a table from the smallest subproblem upward | No recursion overhead; often allows space optimisation |

🔢 **Fibonacci, three ways:**
```
Naïve recursion:  O(2ⁿ) time, O(n) space
Memoised:         O(n)  time, O(n) space
Bottom-up:        O(n)  time, O(1) space   (keep only the last two values)
```

## 7.1 ⭐⭐ The standard DP problems

| Problem | ⭐ Time | Space | 💡 Note |
|---|---|---|---|
| Fibonacci | O(n) | O(1) optimised | vs O(2ⁿ) naïve |
| ⭐ **0/1 knapsack** | ⭐ **O(nW)** | O(nW) → O(W) | ⭐ **Pseudo-polynomial** |
| ⭐ **Longest Common Subsequence (LCS)** | ⭐ **O(mn)** | O(mn) | |
| Longest Increasing Subsequence | O(n²) or **O(n log n)** | O(n) | |
| Edit distance (Levenshtein) | O(mn) | O(mn) | Spell checkers, diff |
| ⭐ **Matrix chain multiplication** | ⭐ **O(n³)** | O(n²) | Minimise scalar multiplications |
| ⭐ **Floyd–Warshall** | ⭐ **O(V³)** | O(V²) | All-pairs shortest paths |
| ⭐ **Bellman–Ford** | ⭐ **O(VE)** | O(V) | Single-source, handles negatives |
| Coin change (min coins / count ways) | O(n × amount) | O(amount) | |
| Subset sum | O(n × sum) | O(sum) | Pseudo-polynomial |
| Travelling Salesman (Held–Karp) | O(n²·2ⁿ) | O(n·2ⁿ) | Still exponential, but better than n! |
| Optimal BST | O(n³) | O(n²) | |
| Rod cutting | O(n²) | O(n) | |

### ⚠⭐ Why O(nW) is "pseudo-polynomial"

The 0/1 knapsack DP table is n rows (items) × W columns (capacities), so filling it is **O(nW)** — which *looks* polynomial.

But **W is a VALUE, not an input size.** Writing the number W down takes only **log W bits**. So in terms of the actual input length, O(nW) is **exponential** — doubling the number of bits in W squares the running time.

⭐ **This is why 0/1 knapsack remains NP-hard despite having an O(nW) algorithm.** The term for this is **pseudo-polynomial**.

### 🔢 LCS — the standard recurrence

Find the longest sequence appearing (not necessarily contiguously) in both strings.

```
L[i][j] = L[i-1][j-1] + 1                    if X[i] == Y[j]
        = max(L[i-1][j], L[i][j-1])          otherwise
```
💡 **Reading it:** if the current characters match, they must be part of the LCS, so extend the diagonal answer. If they do not, drop one character from either string and take the better result.

🔢 X = "ABCBDAB", Y = "BDCABA" → LCS = "BCBA", length **4**.
Table size (m+1)×(n+1), O(1) per cell → ⭐ **O(mn)**.

### 🔢 Matrix chain multiplication

📌 Multiplying a **p×q** matrix by a **q×r** matrix costs **p·q·r** scalar multiplications.

For a chain A(10×30) × B(30×5) × C(5×60):
- `(AB)C` = (10×30×5) + (10×5×60) = 1500 + 3000 = **4500**
- `A(BC)` = (30×5×60) + (10×30×60) = 9000 + 18000 = **27,000**

⭐ **Same answer, 6× the work.** DP finds the optimal parenthesisation in **O(n³)**.

## 7.2 ⭐⭐ Greedy vs DP vs Divide & Conquer

| | **Divide & Conquer** | ⭐ **Greedy** | ⭐ **Dynamic Programming** |
|---|---|---|---|
| ⭐ **Subproblems overlap** | ❌ No | — | ⭐ **✅ Yes** |
| Choice made | Split into independent parts | ⭐ Locally optimal, **never revisited** | ⭐ Considers **all** choices, keeps the best |
| Optimality | Yes (for its problems) | Only if the greedy-choice property holds | ⭐ **Always** (given the two properties) |
| Direction | Top-down | Top-down | Bottom-up (or memoised) |
| Speed | Fast | ⭐ **Fastest** | Slower (fills a table) |
| Example | Merge sort | Fractional knapsack | 0/1 knapsack |

⭐ **Decision rule for the exam:** if a locally best choice can be *proved* to be globally safe → greedy. If choices interact and you must compare alternatives → DP.

---

# 8. ⭐⭐⭐ Graph algorithms

## 8.1 ⭐⭐ Minimum Spanning Tree (MST)

### 💡 The idea

You must connect n cities with cables. Every possible link has a cost. What is the **cheapest set of links that connects everything**?

The answer is a **spanning tree** — connects all vertices, contains no cycle (a cycle would mean a redundant, removable link) — of **minimum total weight**.

📌 ⭐ **An MST has exactly V − 1 edges.**
📌 Applies to **connected, undirected, weighted** graphs.

### ⭐ Prim's algorithm — grow one tree

💡 Start at any vertex. Repeatedly add the **cheapest edge that connects a vertex already in the tree to one outside it**. The tree grows outward like a crystal.

Uses a **priority queue (min-heap)** to find that cheapest edge quickly.

### ⭐ Kruskal's algorithm — add cheapest edges globally

💡 Sort **all** edges by weight. Go through them in order, adding each edge **unless it would create a cycle**. You start with a forest of isolated vertices that gradually merge.

Uses ⭐ **union–find (disjoint set)** to test "would this create a cycle?" in nearly O(1): an edge creates a cycle exactly when both endpoints are already in the same component.

### ⭐⭐ Comparison

| | ⭐ **Prim's** | ⭐ **Kruskal's** |
|---|---|---|
| Approach | Grow **one tree** from a start vertex | Add globally cheapest safe edges |
| Picks | Cheapest edge **leaving the tree** | Cheapest edge **not forming a cycle** |
| ⭐ **Data structure** | **Priority queue (min-heap)** | ⭐ **Disjoint-set (union–find)** |
| ⭐ **Complexity** | ⭐ **O(E log V)** with a binary heap; **O(V²)** with an array; O(E + V log V) with a Fibonacci heap | ⭐ **O(E log E) = O(E log V)** (dominated by sorting) |
| ⭐ **Better for** | ⭐ **DENSE** graphs (the O(V²) array version wins when E ≈ V²) | ⭐ **SPARSE** graphs |
| Disconnected graph | Produces one component's tree | ✅ Produces a spanning **forest** |

⚠ Note `log E ≈ log V²= 2 log V = O(log V)`, so the two heap-based complexities are the same order.

### ⭐ MST properties worth knowing

📌 ⭐ **The MST is UNIQUE if all edge weights are distinct.** (Equal weights can permit several equally-cheap trees.)
📌 ⭐ The MST always contains the **minimum-weight edge** of the graph.
📌 ⭐ **Cut property:** for any partition of the vertices, the minimum-weight edge crossing the partition belongs to some MST. *(This is what makes both algorithms correct.)*
📌 ⭐ **Cycle property:** the maximum-weight edge of any cycle is **not** in the MST (if it is unique).

⚠⚠ ⭐ **An MST minimises the TOTAL weight, not the path between any particular pair.** The path from u to v inside an MST is generally **not** the shortest u–v path. MST ≠ shortest-path tree — a favourite trap.

### 💡 Union–find (disjoint set)

Maintains a collection of disjoint sets with two operations:
- **find(x)** — which set is x in?
- **union(x,y)** — merge two sets

With **union by rank** + **path compression**, both are nearly O(1) amortised (technically the inverse Ackermann function α(n), which is < 5 for any conceivable n).

## 8.2 ⭐⭐⭐ Shortest paths

### 💡 Which algorithm for which situation

| Situation | ⭐ Use |
|---|---|
| Unweighted graph, single source | ⭐ **BFS** — O(V+E) |
| Non-negative weights, single source | ⭐ **Dijkstra** |
| **Negative** weights present, single source | ⭐ **Bellman–Ford** |
| **All pairs** | ⭐ **Floyd–Warshall** |
| DAG, single source | Topological order + relax — O(V+E) |

### ⭐ Dijkstra's algorithm

💡 Maintain a tentative distance to every vertex. Repeatedly pick the **unvisited vertex with the smallest tentative distance**, mark it **finalised**, and **relax** all its outgoing edges (update neighbours if going through this vertex is shorter).

📌 **O(E log V)** with a binary heap; **O(V²)** with a simple array (better for dense graphs).

### ⚠⚠ ⭐ Why Dijkstra fails with negative edges

Dijkstra's correctness rests on one assumption: ⭐ **once a vertex is finalised, no shorter path to it can ever be found**, because every remaining path must pass through some other unvisited vertex whose distance is already ≥ this one's.

A **negative edge destroys that assumption.**

🔢 ```
        A
    5 /   \ 2
     /     \
    B       C
     \     /
   -10\   /
        D
```
Edges: A→B = 5, A→C = 2, C→D = 1, B→D = −10.
- Dijkstra picks C (distance 2) first, then D via C (distance 3), and **finalises D at 3**.
- But the true shortest path is A→B→D = 5 + (−10) = **−5**.
⭐ Dijkstra already committed to D, so it never finds this. ❌

⚠ ⭐ **Note this happens even with NO negative cycle.** The usual wrong answer is "Dijkstra fails only with negative cycles" — it fails with any negative edge.

### ⭐ Bellman–Ford

💡 Instead of being clever about the order, just **relax every edge, V−1 times**.

💡 **Why V−1 passes suffice:** any shortest path has at most V−1 edges (more would mean repeating a vertex, i.e. a cycle). After pass k, all shortest paths using at most k edges are correct. So after V−1 passes, everything is correct.

📌 ⭐ **O(VE)** — slower than Dijkstra, but it handles negative weights.

⭐ **Negative-cycle detection — the bonus feature:** run **one more** (the V-th) pass. If any edge can *still* be relaxed, a shorter path was found using ≥ V edges, which is only possible if a **negative cycle** exists (you can loop around it to reduce the cost indefinitely).

### ⭐ Floyd–Warshall

💡 A DP over "intermediate vertices allowed". Let `d[i][j]` be the shortest path from i to j using only vertices from {1..k} as intermediates. Increase k one at a time.

```
for k in 1..V:            ⭐ k MUST be the OUTERMOST loop
  for i in 1..V:
    for j in 1..V:
      d[i][j] = min( d[i][j],  d[i][k] + d[k][j] )
```
💡 **Reading the update:** *"is going from i to j directly better, or via k?"*

📌 ⭐ **O(V³)** time, O(V²) space. Handles negative edges. ⭐ **A negative value on the diagonal (d[i][i] < 0) means a negative cycle.**

⚠ ⭐ **The loop order matters — k must be outermost.** Swapping it produces wrong answers, and this is asked.

### ⭐⭐ Comparison table

| Algorithm | Solves | ⭐ Complexity | ⭐ Negative edges? | Detects −cycles? | Technique |
|---|---|---|---|---|---|
| **BFS** | Single-source, **unweighted** | O(V + E) | — | — | Traversal |
| ⭐ **Dijkstra** | Single-source | ⭐ **O(E log V)** (heap) / O(V²) (array) | ⭐ **❌ NO** | ❌ | ⭐ **Greedy** |
| ⭐ **Bellman–Ford** | Single-source | ⭐ **O(VE)** | ⭐ **✅ Yes** | ⭐ **✅ Yes** | ⭐ **DP** |
| ⭐ **Floyd–Warshall** | ⭐ **All-pairs** | ⭐ **O(V³)** | ✅ Yes | ✅ Yes (negative diagonal) | ⭐ **DP** |
| Johnson's | All-pairs (sparse) | O(V² log V + VE) | ✅ Yes | ✅ | Reweighting |
| DAG shortest path | Single-source on a DAG | **O(V + E)** | ✅ Yes | N/A | Topological order |

## 8.3 Traversal-based algorithms (from Week 4)

| Task | Algorithm | Complexity |
|---|---|---|
| Connected components | BFS/DFS | O(V + E) |
| Cycle detection | DFS (back edge) or union–find | O(V + E) |
| ⭐ **Topological sort** | Kahn's (in-degree) or DFS post-order | O(V + E) — ⭐ **DAG only** |
| Strongly connected components | Kosaraju (2 DFS) / Tarjan (1 DFS) | O(V + E) |
| Articulation points & bridges | DFS with discovery/low values | O(V + E) |
| Bipartiteness | BFS 2-colouring | O(V + E) |

---

# 9. ⭐ Complexity classes

## 💡 The idea

Some problems have fast algorithms. Some have none that anyone has found. Complexity classes formalise the difference.

| Class | 💡 Meaning |
|---|---|
| **P** | Solvable in **polynomial time** by a deterministic machine. "Efficiently solvable" |
| ⭐ **NP** | ⭐ **VERIFIABLE in polynomial time.** Given a proposed solution, you can *check* it quickly — even if *finding* it seems hard |
| ⭐ **NP-hard** | ⭐ At least as hard as **every** problem in NP. ⭐ **Need not be in NP; need not even be decidable** |
| ⭐ **NP-complete** | ⭐ **In NP AND NP-hard** — the hardest problems that are still verifiable |

🔢 **Sudoku illustrates NP perfectly:** solving a hard Sudoku is difficult, but **checking** a completed grid takes seconds. Easy to verify, seemingly hard to solve.

📌 ⭐ **P ⊆ NP** (if you can solve it fast, you can verify it fast). ⭐ **Whether P = NP is the most famous open problem in computer science.**

📌 ⭐ **Cook–Levin theorem: SAT (boolean satisfiability) was the first problem proved NP-complete.** Every other NP-completeness proof works by reduction from an already-known NP-complete problem.

⭐ **Known NP-complete:** SAT, 3-SAT, **Travelling Salesman (decision version)**, **Hamiltonian cycle/path**, vertex cover, clique, independent set, graph colouring, subset sum, **0/1 knapsack (decision)**, bin packing, set cover.

⭐ **In P:** shortest path (non-negative), MST, sorting, bipartite matching, linear programming, primality testing (AKS 2002), **Euler circuit**.

⚠⚠ ⭐ **Euler circuit is in P; Hamiltonian circuit is NP-complete.**
💡 **Why the difference?** An Euler circuit visits every **edge** once, and there is a simple local criterion (every vertex has even degree) — checkable in O(V+E). A Hamiltonian circuit visits every **vertex** once, and no such local criterion exists.

⚠ ⭐ **NP-hard does NOT imply NP-complete.** The halting problem is NP-hard but not in NP (it is undecidable), so it is not NP-complete.

---

# 10. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| Growth order | log n < √n < n < n log n < n² < 2ⁿ < n! |
| √n vs log n | **√n is larger** |
| log(n!) | Θ(n log n) |
| T(n) = 2T(n/2) + n | **Θ(n log n)** |
| T(n) = 2T(n/2) + 1 | **Θ(n)** |
| T(n) = T(n/2) + 1 | **Θ(log n)** |
| T(n) = T(n−1) + n | Θ(n²) |
| T(n) = 2T(n−1) + 1 | Θ(2ⁿ) |
| Comparison sort lower bound | **Ω(n log n)** — decision tree, log(n!) |
| Binary search comparisons | ⌈log₂(n+1)⌉ |
| Binary search on a linked list | O(n) — no random access |
| Quick sort worst / average | **O(n²) / O(n log n)** |
| Quick sort worst case occurs on | **Sorted input** with a naïve pivot |
| Merge sort space | **O(n)** — not in-place |
| Heap sort space | **O(1)** — in-place |
| Both O(n log n) worst **and** in-place | **Heap sort** |
| Unstable sorts | **Quick, heap, selection**, shell |
| Insertion sort on sorted input | **O(n)** — adaptive |
| Selection sort comparisons | n(n−1)/2 **always** |
| Selection sort swaps | O(n) — good when writes are costly |
| Counting sort | O(n+k), non-comparison |
| Radix sort requires | A **stable** subroutine |
| Merging two sorted arrays | m + n − 1 comparisons |
| Strassen | **7** multiplications, O(n^2.81) |
| Max-min comparisons | **3n/2 − 2** |
| Huffman | Greedy, O(n log n), **prefix-free** |
| Huffman gives frequent symbols | **Shorter** codes |
| Fractional / 0-1 knapsack | ⭐ **Greedy / DP** |
| 0/1 knapsack complexity | O(nW), **pseudo-polynomial** |
| LCS | O(mn) |
| Matrix chain | O(n³); p×q by q×r costs pqr |
| DP requires | **Optimal substructure + overlapping subproblems** |
| D&C lacks | **Overlapping subproblems** |
| Prim / Kruskal | O(E log V) / O(E log E) |
| Kruskal uses | **Union–find** |
| Prim uses | Priority queue |
| Prim better for / Kruskal better for | Dense / sparse |
| MST edges | **V − 1** |
| MST unique when | All weights **distinct** |
| MST vs shortest path | ⭐ **Different** — MST paths are not shortest paths |
| Dijkstra | O(E log V), **greedy**, **no negative edges** |
| Dijkstra fails because | A finalised vertex can be improved later |
| Bellman–Ford | **O(VE)**, DP, detects negative cycles |
| Bellman–Ford passes | V − 1 (V-th detects a negative cycle) |
| Floyd–Warshall | **O(V³)**, DP, all-pairs, **k outermost** |
| Topological sort | **DAG only**, O(V+E), not unique |
| NP | Verifiable in polynomial time |
| NP-complete | **In NP AND NP-hard** |
| First NP-complete problem | **SAT** (Cook–Levin) |
| Euler vs Hamiltonian circuit | **P vs NP-complete** |

---

# 11. ⚠ Common traps

1. ⭐ **Fractional knapsack = greedy; 0/1 knapsack = DP.** The most common reversal in this section.
2. ⭐ **Quick sort's worst case occurs on SORTED input**, not random input.
3. ⭐ **Merge sort is not in-place (O(n) space); heap sort is (O(1)).**
4. ⭐ **Quick sort is unstable; merge sort is stable.**
5. ⭐ **√n grows faster than log n.**
6. ⭐ **Dijkstra fails with ANY negative edge**, not only with negative cycles.
7. ⭐ **Bellman–Ford is O(VE), not O(V²).**
8. ⭐ **O(nW) is pseudo-polynomial, not polynomial.**
9. ⭐ **NP-hard ⊅ NP** — NP-complete additionally requires membership in NP.
10. ⭐ **MST ≠ shortest-path tree.**
11. **Prim is better for dense graphs, Kruskal for sparse** (with the appropriate implementations).
12. **Build-heap is O(n)** (carried over from Week 4, still asked here).
13. **Floyd–Warshall's k loop must be outermost.**
14. **Radix sort needs a stable inner sort.**
15. **Divide & conquer has optimal substructure but no overlapping subproblems** — that is what separates it from DP.
16. **Amortised ≠ average case.**

---

# 12. Practice

- GATE: [`Paper2_S06_Algorithms/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S06_Algorithms/) — **358 questions**
- State-PSC level: [`Paper2_S06_Algorithms/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S06_Algorithms/) — **256 questions**
- Test: [`Week_05_Test.md`](../04_Mock_Tests/Week_05_Test.md)

**Priority order if short on time:** ⭐ **the sorting master table (§4.3)** → Master theorem worked cases → the shortest-path comparison table → Prim vs Kruskal → greedy vs DP problem classification → asymptotic growth ordering → NP definitions.
