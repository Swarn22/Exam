# Week 5 Question Bank — Algorithms

**Syllabus §6** · 161 questions · Practice set · +1 / −0.33 marking

> Attempt in timed batches (e.g. 20 questions in 20 minutes) to simulate exam pressure; mark the ones you guess and review them against the solutions.

---

## Part A — Asymptotic notation

**Q1.** Which of the following orders the functions in **increasing** order of asymptotic growth?
(A) log n, √n, n log n, n², 2ⁿ  (B) √n, log n, n log n, n², 2ⁿ  (C) log n, √n, n², n log n, 2ⁿ  (D) log n, n log n, √n, n², 2ⁿ

**Q2.** Which function grows faster for large n?
(A) log n  (B) √n  (C) they grow at the same rate  (D) it depends on the logarithm base

**Q3.** Which asymptotic notation gives a **tight** bound (both an upper and a lower bound)?
(A) O  (B) Ω  (C) Θ  (D) o

**Q4.** The notation denoting a **strict** upper bound (f grows strictly slower than g) is
(A) o(g)  (B) O(g)  (C) ω(g)  (D) Θ(g)

**Q5.** Which statement about big-O is TRUE?
(A) n = O(n²) is false  (B) O gives a lower bound  (C) n = O(n²) is true but not a tight bound  (D) O ignores constants only for exponentials

**Q6.** By Stirling's approximation, log(n!) is
(A) Θ(n)  (B) Θ(log n)  (C) Θ(n²)  (D) Θ(n log n)

**Q7.** The function 3n² + 100n + 500 is
(A) Θ(n²)  (B) Θ(n)  (C) Θ(n log n)  (D) Θ(n³)

**Q8.** In asymptotic analysis, the base of a logarithm
(A) changes the complexity class  (B) does not matter — it differs only by a constant factor  (C) matters only for Ω  (D) matters only for large n

**Q9.** Which case does the syllabus name explicitly and exams usually mean by "the complexity"?
(A) best case  (B) average case  (C) worst case  (D) amortised

**Q10.** Amortised analysis measures
(A) the average cost per operation over a worst-case sequence  (B) the probabilistic average over random inputs  (C) the best-case cost  (D) the cost of a single operation

**Q11.** A dynamic array that doubles its capacity when full has an amortised insertion cost of
(A) O(n)  (B) O(log n)  (C) O(1)  (D) O(n log n)

**Q12.** Which statement is TRUE?
(A) amortised equals average case  (B) average case is always worse than amortised  (C) amortised is a worst-case guarantee over a sequence, whereas average case is probabilistic  (D) amortised applies only to sorting

**Q13.** Θ(g) is equal to
(A) O(g) ∪ Ω(g)  (B) O(g) ∩ Ω(g)  (C) o(g) ∩ ω(g)  (D) O(g) only

**Q14.** For large n, which relationship holds?
(A) 2ⁿ > n!  (B) n! > nⁿ  (C) 2ⁿ < n!  (D) n! = 2ⁿ

**Q15.** Comparing any polynomial with any polylogarithmic function:
(A) the polylogarithm beats the polynomial  (B) they are equal  (C) it depends on constants  (D) any polynomial beats any polylogarithm

**Q16.** The notation ω(g) denotes
(A) a strict lower bound — f grows strictly faster than g  (B) a strict upper bound  (C) a tight bound  (D) a non-strict upper bound

---

## Part B — Recurrences & the Master theorem

**Q17.** By the Master theorem, T(n) = 2T(n/2) + n solves to
(A) Θ(n)  (B) Θ(n log n)  (C) Θ(n²)  (D) Θ(log n)

**Q18.** T(n) = 2T(n/2) + 1, with T(1) = 1, solves to
(A) Θ(n)  (B) Θ(n log n)  (C) Θ(log n)  (D) Θ(n²)

**Q19.** T(n) = T(n/2) + 1 (binary search) solves to
(A) Θ(1)  (B) Θ(log n)  (C) Θ(n)  (D) Θ(n log n)

**Q20.** T(n) = 2T(n/2) + n² solves to
(A) Θ(n)  (B) Θ(n²)  (C) Θ(n² log n)  (D) Θ(n³)

**Q21.** T(n) = 4T(n/2) + n solves to
(A) Θ(n)  (B) Θ(n log n)  (C) Θ(n²)  (D) Θ(n² log n)

**Q22.** T(n) = 8T(n/2) + n² solves to
(A) Θ(n²)  (B) Θ(n² log n)  (C) Θ(n³)  (D) Θ(n³ log n)

**Q23.** T(n) = 7T(n/2) + n² (Strassen) solves to
(A) Θ(n²)  (B) Θ(n^2.81)  (C) Θ(n³)  (D) Θ(n² log n)

**Q24.** T(n) = 9T(n/3) + n solves to
(A) Θ(n)  (B) Θ(n log n)  (C) Θ(n²)  (D) Θ(n² log n)

**Q25.** T(n) = 3T(n/4) + n log n solves to
(A) Θ(n^0.79)  (B) Θ(n log n)  (C) Θ(n²)  (D) Θ(n log² n)

**Q26.** In Master theorem Case 2 (f(n) equals n^(log_b a)), the result is
(A) Θ(n^(log_b a))  (B) Θ(f(n))  (C) Θ(n^(log_b a) · log n)  (D) Θ(n log n) always

**Q27.** The Master theorem does **not** apply to which recurrence?
(A) T(n) = 2T(n/2) + n  (B) T(n) = 2T(n/2) + n/log n  (C) T(n) = 4T(n/2) + n  (D) T(n) = T(n/2) + 1

**Q28.** T(n) = T(n−1) + 1 (linear search / factorial) solves to
(A) O(log n)  (B) O(n)  (C) O(n²)  (D) O(2ⁿ)

**Q29.** T(n) = T(n−1) + n (insertion / selection sort) solves to
(A) O(n)  (B) O(n log n)  (C) O(n²)  (D) O(2ⁿ)

**Q30.** T(n) = 2T(n−1) + 1 (Towers of Hanoi) solves to
(A) O(n²)  (B) O(n log n)  (C) O(2ⁿ)  (D) O(n!)

**Q31.** T(n) = T(n−1) + T(n−2) (naïve Fibonacci) solves to
(A) O(n)  (B) O(n²)  (C) O(log n)  (D) O(2ⁿ)

**Q32.** In T(n) = aT(n/b) + f(n), the term n^(log_b a) represents
(A) work at the root (combine step)  (B) work at the leaves (recursive calls at the bottom)  (C) the number of levels  (D) the combining function

**Q33.** Karatsuba multiplication has recurrence T(n) = 3T(n/2) + n, giving
(A) O(n²)  (B) O(n^1.585)  (C) O(n log n)  (D) O(n^2.81)

**Q34.** For a subtract-and-conquer recurrence T(n) = aT(n−b) + f(n) with a = 1, the result is
(A) O(f(n))  (B) O(n·f(n))  (C) O(a^(n/b)·f(n))  (D) O(n²)

---

## Part C — Searching

**Q35.** The worst-case number of comparisons for binary search on n sorted elements is
(A) O(n)  (B) O(log n)  (C) O(n log n)  (D) O(1)

**Q36.** Binary search requires
(A) a linked list  (B) a hash table  (C) a sorted array with random access  (D) unsorted data

**Q37.** Binary search performed on a linked list runs in
(A) O(log n)  (B) O(1)  (C) O(n log n)  (D) O(n) because there is no random access

**Q38.** The exact worst-case comparison count of binary search on n elements is
(A) ⌊log₂ n⌋  (B) ⌈log₂(n+1)⌉  (C) n/2  (D) log₂ n − 1

**Q39.** For n = 1000, the worst-case number of binary-search comparisons is about
(A) 10  (B) 20  (C) 100  (D) 500

**Q40.** Linear search has worst-case time complexity
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n²)

**Q41.** Which search needs data that is sorted **and** uniformly distributed for its best average performance?
(A) linear search  (B) binary search  (C) interpolation search  (D) hashing

**Q42.** The average-case lookup time of a well-designed hash table is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q43.** Jump search has worst-case time complexity
(A) O(log n)  (B) O(√n)  (C) O(n)  (D) O(1)

**Q44.** Each step of binary search reduces the search space by
(A) one element  (B) half  (C) a quarter  (D) √n

---

## Part D — Sorting

**Q45.** The worst-case and average-case time complexities of quick sort are, respectively,
(A) O(n log n), O(n log n)  (B) O(n²), O(n log n)  (C) O(n²), O(n²)  (D) O(n log n), O(n²)

**Q46.** Which sorting algorithm is **not** stable in its standard implementation?
(A) insertion sort  (B) merge sort  (C) bubble sort  (D) quick sort

**Q47.** Heap sort's worst-case time and auxiliary space are, respectively,
(A) O(n log n) and O(1)  (B) O(n log n) and O(n)  (C) O(n²) and O(1)  (D) O(n) and O(n)

**Q48.** The auxiliary space of standard array-based merge sort is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q49.** The lower bound on comparisons for any comparison-based sort is
(A) Ω(n)  (B) Ω(n log n)  (C) Ω(log n)  (D) Ω(n²)

**Q50.** Counting sort runs in O(n + k) because it
(A) uses a better pivot  (B) is not comparison-based  (C) uses divide and conquer  (D) sorts in place

**Q51.** Which sort achieves O(n) best case on already-sorted input because it is adaptive?
(A) selection sort  (B) insertion sort  (C) merge sort  (D) heap sort

**Q52.** Quick sort's O(n²) worst case occurs on
(A) random input  (B) sorted input with a naïve first-element pivot  (C) reverse-sorted input only  (D) all inputs

**Q53.** Selection sort always performs exactly how many comparisons?
(A) n  (B) n log n  (C) n(n−1)/2  (D) n²

**Q54.** Which comparison sort is both O(n log n) worst case **and** in-place (O(1) space)?
(A) merge sort  (B) quick sort  (C) heap sort  (D) insertion sort

**Q55.** Which of these sorts is **not** in-place?
(A) heap sort  (B) insertion sort  (C) merge sort  (D) selection sort

**Q56.** Radix sort requires its per-digit subroutine to be
(A) fast  (B) comparison-based  (C) in-place  (D) stable

**Q57.** Which set contains only **unstable** sorts?
(A) insertion, merge, bubble  (B) quick, heap, selection  (C) counting, radix, bucket  (D) merge, counting, insertion

**Q58.** With an early-exit swap flag, bubble sort's best case on sorted input is
(A) O(n)  (B) O(n log n)  (C) O(n²)  (D) O(1)

**Q59.** Merging two sorted arrays of sizes m and n takes at most
(A) m + n comparisons  (B) m + n − 1 comparisons  (C) mn comparisons  (D) 2(m + n) comparisons

**Q60.** Merge sort's worst-case time complexity is
(A) O(n)  (B) O(n log n)  (C) O(n²)  (D) O(log n)

**Q61.** Which non-comparison sort runs in O(d(n + k)), where d is the number of digits?
(A) counting sort  (B) radix sort  (C) bucket sort  (D) shell sort

**Q62.** The number of swaps performed by selection sort is
(A) O(n)  (B) O(n log n)  (C) O(n²)  (D) n(n−1)/2

**Q63.** Insertion sort runs in O(n + inversions), which means it is
(A) non-adaptive  (B) adaptive to nearly-sorted input  (C) always O(n²)  (D) comparison-free

**Q64.** Counting, radix and bucket sort can beat the Ω(n log n) bound because they
(A) use better pivots  (B) are not comparison-based  (C) use recursion  (D) are in-place

**Q65.** The decision-tree argument for the Ω(n log n) lower bound uses a binary tree with how many leaves?
(A) n  (B) n²  (C) n!  (D) 2ⁿ

**Q66.** Bucket sort's worst-case time complexity is
(A) O(n)  (B) O(n log n)  (C) O(n²)  (D) O(n + k)

**Q67.** Which sort is used for small subarrays inside hybrid sorts (Timsort, introsort)?
(A) heap sort  (B) insertion sort  (C) merge sort  (D) counting sort

**Q68.** Selection sort is useful when writes are expensive because it performs
(A) O(n²) swaps  (B) O(n) swaps  (C) O(log n) swaps  (D) no swaps

**Q69.** Which sort uses O(k) extra space, where k is the key range?
(A) counting sort  (B) merge sort  (C) heap sort  (D) quick sort

**Q70.** Bubble sort's worst-case number of comparisons and swaps is
(A) n  (B) n log n  (C) n(n−1)/2  (D) 2ⁿ

---

## Part E — Divide and conquer

**Q71.** Strassen's algorithm multiplies two n×n matrices using how many multiplications of (n/2)×(n/2) blocks?
(A) 8  (B) 7  (C) 4  (D) 3

**Q72.** Strassen's matrix multiplication runs in
(A) O(n³)  (B) O(n^2.81)  (C) O(n²)  (D) O(n log n)

**Q73.** Finding both the maximum and minimum of n elements using the pairing method takes
(A) 2n − 2 comparisons  (B) 3n/2 − 2 comparisons  (C) n − 1 comparisons  (D) n log n comparisons

**Q74.** Naïve matrix multiplication has recurrence T(n) = 8T(n/2) + n², giving
(A) O(n²)  (B) O(n^2.81)  (C) O(n³)  (D) O(n² log n)

**Q75.** The three steps of divide and conquer, in order, are
(A) combine, divide, conquer  (B) divide, conquer, combine  (C) conquer, combine, divide  (D) divide, combine, conquer

**Q76.** The closest-pair-of-points divide-and-conquer algorithm runs in
(A) O(n²)  (B) O(n log n)  (C) O(n)  (D) O(n³)

**Q77.** Karatsuba multiplication has time complexity
(A) O(n²)  (B) O(n^1.585)  (C) O(n log n)  (D) O(n^2.81)

**Q78.** Which of the following is a divide-and-conquer sorting algorithm?
(A) insertion sort  (B) selection sort  (C) merge sort  (D) counting sort

**Q79.** Finding both max and min naïvely (without pairing) takes
(A) 2n − 2 comparisons  (B) 3n/2 − 2 comparisons  (C) n comparisons  (D) n log n comparisons

**Q80.** Divide and conquer differs from dynamic programming because it lacks
(A) optimal substructure  (B) overlapping subproblems  (C) recursion  (D) a combine step

---

## Part F — Greedy algorithms

**Q81.** Huffman coding uses which algorithm-design paradigm?
(A) divide and conquer  (B) dynamic programming  (C) greedy  (D) backtracking

**Q82.** The 0/1 knapsack problem is solved optimally by
(A) a greedy approach on value/weight ratio  (B) dynamic programming  (C) binary search  (D) breadth-first search

**Q83.** The fractional knapsack problem is solved optimally by
(A) greedy selection on the value/weight ratio  (B) dynamic programming  (C) backtracking  (D) breadth-first search

**Q84.** The greedy strategy for activity selection is to always pick the activity with the
(A) shortest duration  (B) earliest start time  (C) earliest finish time  (D) highest value

**Q85.** Huffman coding with a min-heap runs in
(A) O(n)  (B) O(n²)  (C) O(n³)  (D) O(n log n)

**Q86.** Frequencies a:5, b:9, c:12, d:13, e:16, f:45 (total 100) give a Huffman encoding using how many total bits?
(A) 200  (B) 100  (C) 224  (D) 300

**Q87.** For that Huffman encoding, the average code length per character is
(A) 2.24 bits  (B) 3.00 bits  (C) 2.00 bits  (D) 1.45 bits

**Q88.** A Huffman code is
(A) fixed-length  (B) not decodable  (C) lossy  (D) prefix-free

**Q89.** Huffman coding assigns to frequently occurring characters
(A) longer codes  (B) equal-length codes  (C) shorter codes  (D) no codes

**Q90.** With denominations {1, 3, 4} and target 6, greedy uses 4 + 1 + 1 = 3 coins; the optimal is
(A) 2 coins (3 + 3)  (B) 3 coins  (C) 4 coins  (D) 1 coin

**Q91.** Which paradigm requires both the greedy-choice property and optimal substructure?
(A) dynamic programming  (B) greedy algorithms  (C) divide and conquer  (D) backtracking

**Q92.** The greedy strategy for job sequencing with deadlines is to
(A) sort by deadline ascending  (B) sort by duration  (C) sort by arrival time  (D) sort by profit descending and schedule each job as late as possible

**Q93.** Greedy fails for 0/1 knapsack primarily because of
(A) indivisibility — a committed choice can block a better combination  (B) items having no value  (C) items having negative weight  (D) unlimited capacity

**Q94.** The standard exam pairing is
(A) fractional = DP, 0/1 = greedy  (B) fractional = greedy, 0/1 = DP  (C) both greedy  (D) both DP

---

## Part G — Dynamic programming

**Q95.** The standard DP for the Longest Common Subsequence of strings of lengths m and n runs in
(A) O(mn)  (B) O(m + n)  (C) O(m log n)  (D) O(2ⁿ)

**Q96.** Which two properties must a problem have for DP to apply?
(A) optimal substructure and overlapping subproblems  (B) optimal substructure and the greedy-choice property  (C) overlapping subproblems and the greedy-choice property  (D) divisibility and recursion

**Q97.** Which property distinguishes dynamic programming from divide and conquer?
(A) optimal substructure  (B) recursion  (C) a base case  (D) overlapping subproblems

**Q98.** The 0/1 knapsack DP has time complexity
(A) O(n)  (B) O(n²)  (C) O(nW)  (D) O(2ⁿ)

**Q99.** O(nW) is called pseudo-polynomial because
(A) W is a value — writing it needs only log W bits, so O(nW) is exponential in the input size  (B) it is truly polynomial  (C) it uses floating point  (D) it depends on n only

**Q100.** Matrix chain multiplication is solved by DP in
(A) O(n²)  (B) O(2ⁿ)  (C) O(n log n)  (D) O(n³)

**Q101.** Multiplying a p×q matrix by a q×r matrix costs how many scalar multiplications?
(A) p + q + r  (B) pq + qr  (C) pqr  (D) p²r

**Q102.** Edit distance (Levenshtein) between strings of lengths m and n is computed by DP in
(A) O(mn)  (B) O(m + n)  (C) O(2ⁿ)  (D) O(m log n)

**Q103.** Floyd–Warshall belongs to which paradigm?
(A) greedy  (B) dynamic programming  (C) divide and conquer  (D) backtracking

**Q104.** Regarding overlapping subproblems:
(A) DP has them, divide and conquer does not  (B) DP does not, divide and conquer does  (C) both have them  (D) neither has them

**Q105.** Bottom-up DP (tabulation), compared with top-down memoisation,
(A) uses recursion with a cache  (B) computes only the needed subproblems  (C) fills a table iteratively from the smallest subproblem upward  (D) always uses more space

**Q106.** Fibonacci computed bottom-up keeping only the last two values uses space
(A) O(n)  (B) O(log n)  (C) O(2ⁿ)  (D) O(1)

**Q107.** For A(10×30) × B(30×5) × C(5×60), (AB)C costs 4500; A(BC) costs
(A) 4500  (B) 27000  (C) 9000  (D) 18000

**Q108.** The LCS of X = "ABCBDAB" and Y = "BDCABA" has length
(A) 3  (B) 4  (C) 5  (D) 6

**Q109.** Given its two required properties, which paradigm always guarantees an optimal solution?
(A) dynamic programming  (B) greedy  (C) divide and conquer  (D) none

**Q110.** The Held–Karp DP for the Travelling Salesman Problem runs in
(A) O(n!)  (B) O(2ⁿ)  (C) O(n³)  (D) O(n²·2ⁿ)

---

## Part H — Minimum spanning trees

**Q111.** Which data structure makes Kruskal's cycle test efficient?
(A) priority queue only  (B) hash table  (C) disjoint-set (union–find)  (D) stack

**Q112.** Prim's algorithm with a binary min-heap runs in
(A) O(V²)  (B) O(VE)  (C) O(E log V)  (D) O(E + V)

**Q113.** An MST of a connected graph on V vertices has exactly
(A) V edges  (B) V − 1 edges  (C) E − V edges  (D) V + 1 edges

**Q114.** An MST is unique when
(A) all edge weights are distinct  (B) the graph is complete  (C) the graph is already a tree  (D) V is even

**Q115.** Kruskal's algorithm has time complexity
(A) O(V²)  (B) O(VE)  (C) O(E log E)  (D) O(V³)

**Q116.** Prim's O(V²) array implementation is best for
(A) sparse graphs  (B) trees  (C) disconnected graphs  (D) dense graphs

**Q117.** Kruskal's algorithm is generally better for
(A) dense graphs  (B) sparse graphs  (C) complete graphs  (D) directed graphs

**Q118.** The cut property states that
(A) the minimum-weight edge crossing any partition belongs to some MST  (B) the maximum-weight edge of a cycle is in the MST  (C) the MST has V edges  (D) the MST equals the shortest-path tree

**Q119.** The cycle property states that the ___ edge of any cycle is not in the MST.
(A) minimum-weight  (B) middle  (C) maximum-weight  (D) first

**Q120.** Which statement about MSTs versus shortest paths is TRUE?
(A) the u–v path in an MST is always the shortest u–v path  (B) an MST equals the shortest-path tree always  (C) an MST maximises total weight  (D) an MST minimises total weight, not any individual pair's path

**Q121.** Union–find with union by rank and path compression gives operations that are
(A) O(n)  (B) O(log n)  (C) nearly O(1) amortised (inverse Ackermann)  (D) O(n log n)

**Q122.** Prim's algorithm uses which data structure to find the cheapest edge leaving the tree?
(A) a priority queue / min-heap  (B) a disjoint-set  (C) a hash table  (D) a stack

---

## Part I — Shortest paths

**Q123.** Dijkstra's algorithm gives incorrect results when the graph contains
(A) cycles  (B) negative edge weights  (C) more than 100 vertices  (D) undirected edges

**Q124.** Bellman–Ford's time complexity on V vertices and E edges is
(A) O(V log V)  (B) O(E log V)  (C) O(VE)  (D) O(V³)

**Q125.** Floyd–Warshall's time complexity is
(A) O(V²)  (B) O(V³)  (C) O(VE)  (D) O(E log V)

**Q126.** Dijkstra's algorithm follows which paradigm?
(A) greedy  (B) dynamic programming  (C) divide and conquer  (D) backtracking

**Q127.** Bellman–Ford follows which paradigm?
(A) greedy  (B) dynamic programming  (C) divide and conquer  (D) brute force

**Q128.** For single-source shortest paths on an **unweighted** graph, the best choice is
(A) BFS in O(V + E)  (B) Dijkstra  (C) Bellman–Ford  (D) Floyd–Warshall

**Q129.** Bellman–Ford needs how many relaxation passes to guarantee correctness?
(A) V  (B) V − 1  (C) E  (D) log V

**Q130.** Bellman–Ford detects a negative cycle by
(A) running BFS  (B) sorting edges  (C) running one more (V-th) pass and checking whether any edge can still be relaxed  (D) using union–find

**Q131.** Dijkstra fails with negative edges because
(A) a finalised vertex may later be improved via a negative edge  (B) it cannot handle cycles  (C) it needs sorted edges  (D) it uses too much memory

**Q132.** With a negative edge but **no** negative cycle, Dijkstra
(A) always works  (B) detects the negative edge  (C) becomes O(VE)  (D) can still give wrong answers

**Q133.** In Floyd–Warshall, which loop **must** be outermost?
(A) i  (B) j  (C) k (the intermediate vertex)  (D) any order works

**Q134.** Dijkstra's algorithm with a binary heap runs in
(A) O(V²)  (B) O(E log V)  (C) O(VE)  (D) O(V³)

**Q135.** In Floyd–Warshall, a negative value on the diagonal d[i][i] indicates
(A) an error  (B) a zero self-loop  (C) disconnection  (D) a negative cycle

**Q136.** Which algorithm solves **all-pairs** shortest paths and handles negative edges?
(A) Dijkstra  (B) BFS  (C) Floyd–Warshall  (D) Prim

---

## Part J — Complexity classes (NP theory)

**Q137.** A problem is NP-complete if it is
(A) in NP and every problem in NP reduces to it in polynomial time  (B) solvable in polynomial time  (C) not in NP but NP-hard  (D) unsolvable

**Q138.** The class NP consists of problems that are
(A) unsolvable  (B) verifiable in polynomial time  (C) solvable only exponentially  (D) solvable in constant time

**Q139.** By the Cook–Levin theorem, the first problem proved NP-complete was
(A) Travelling Salesman  (B) Hamiltonian cycle  (C) SAT (boolean satisfiability)  (D) vertex cover

**Q140.** Which statement about NP-hard is TRUE?
(A) NP-hard implies NP-complete  (B) all NP-hard problems are in P  (C) NP-hard problems are always verifiable  (D) NP-hard problems need not be in NP and need not be decidable

**Q141.** Which statement correctly contrasts these two problems?
(A) Euler circuit is in P; Hamiltonian circuit is NP-complete  (B) Euler circuit is NP-complete; Hamiltonian is in P  (C) both are in P  (D) both are NP-complete

**Q142.** P ⊆ NP because
(A) all NP problems are in P  (B) P = NP is proven  (C) verification is harder than solving  (D) if you can solve a problem fast, you can verify it fast

**Q143.** Which of the following is in P?
(A) Travelling Salesman  (B) Hamiltonian cycle  (C) minimum spanning tree  (D) SAT

**Q144.** The halting problem is NP-hard but not NP-complete because it is
(A) in P  (B) verifiable quickly  (C) undecidable, hence not in NP  (D) solvable in polynomial time

**Q145.** Whether P = NP is
(A) proven true  (B) proven false  (C) the most famous open problem in computer science  (D) irrelevant

**Q146.** Which of the following is NP-complete?
(A) 0/1 knapsack (decision version)  (B) sorting  (C) shortest path with non-negative weights  (D) minimum spanning tree

---

## Part K — Paper-I (English, Reasoning, GK)

**Q147.** Identify the part containing the error: *"The list of participants (A)/ were displayed (B)/ on the notice board (C)/ yesterday morning. (D)"*
(A) A  (B) B  (C) C  (D) D

**Q148.** The idiom *"to burn the midnight oil"* means
(A) to waste resources  (B) to work or study late into the night  (C) to start a quarrel  (D) to celebrate

**Q149.** Find the missing term: 2, 6, 12, 20, 30, ___
(A) 40  (B) 42  (C) 44  (D) 46

**Q150.** A sum of ₹8,000 amounts to ₹9,680 in 2 years at simple interest. The annual rate is
(A) 9%  (B) 10.5%  (C) 12%  (D) 15%

**Q151.** Neermahal, the lake palace of Tripura, stands in the middle of which lake?
(A) Dumboor Lake  (B) Rudrasagar Lake  (C) Amarpur Lake  (D) Jampui Lake

**Q152.** Choose the synonym of *"ephemeral"*.
(A) permanent  (B) enormous  (C) short-lived  (D) colourful

**Q153.** Choose the antonym of *"benevolent"*.
(A) kind  (B) generous  (C) malevolent  (D) gentle

**Q154.** Find the odd one out: 3, 5, 7, 9, 11
(A) 3  (B) 5  (C) 9  (D) 11

**Q155.** If FRIEND is coded as HTKGPF, then CANDLE is coded as
(A) ECPFNG  (B) DBOEMF  (C) ECQFNG  (D) EDPFNG

**Q156.** A 150 m long train running at 90 km/h crosses a pole in
(A) 6 s  (B) 5 s  (C) 10 s  (D) 15 s

**Q157.** The average of the first 10 natural numbers is
(A) 5  (B) 5.5  (C) 6  (D) 10

**Q158.** *Doctor* is to *Patient* as *Teacher* is to
(A) school  (B) book  (C) class  (D) student

**Q159.** The capital of Tripura is
(A) Agartala  (B) Aizawl  (C) Imphal  (D) Shillong

**Q160.** The Ujjayanta Palace is located in
(A) Agartala  (B) Udaipur  (C) Dharmanagar  (D) Kailashahar

**Q161.** If 5 pens cost ₹75, then 8 pens cost
(A) ₹100  (B) ₹125  (C) ₹150  (D) ₹120

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | A | 2 | B | 3 | C | 4 | A | 5 | C | 6 | D | 7 | A | 8 | B |
| 9 | C | 10 | A | 11 | C | 12 | C | 13 | B | 14 | C | 15 | D | 16 | A |
| 17 | B | 18 | A | 19 | B | 20 | B | 21 | C | 22 | C | 23 | B | 24 | C |
| 25 | B | 26 | C | 27 | B | 28 | B | 29 | C | 30 | C | 31 | D | 32 | B |
| 33 | B | 34 | B | 35 | B | 36 | C | 37 | D | 38 | B | 39 | A | 40 | C |
| 41 | C | 42 | A | 43 | B | 44 | B | 45 | B | 46 | D | 47 | A | 48 | C |
| 49 | B | 50 | B | 51 | B | 52 | B | 53 | C | 54 | C | 55 | C | 56 | D |
| 57 | B | 58 | A | 59 | B | 60 | B | 61 | B | 62 | A | 63 | B | 64 | B |
| 65 | C | 66 | C | 67 | B | 68 | B | 69 | A | 70 | C | 71 | B | 72 | B |
| 73 | B | 74 | C | 75 | B | 76 | B | 77 | B | 78 | C | 79 | A | 80 | B |
| 81 | C | 82 | B | 83 | A | 84 | C | 85 | D | 86 | C | 87 | A | 88 | D |
| 89 | C | 90 | A | 91 | B | 92 | D | 93 | A | 94 | B | 95 | A | 96 | A |
| 97 | D | 98 | C | 99 | A | 100 | D | 101 | C | 102 | A | 103 | B | 104 | A |
| 105 | C | 106 | D | 107 | B | 108 | B | 109 | A | 110 | D | 111 | C | 112 | C |
| 113 | B | 114 | A | 115 | C | 116 | D | 117 | B | 118 | A | 119 | C | 120 | D |
| 121 | C | 122 | A | 123 | B | 124 | C | 125 | B | 126 | A | 127 | B | 128 | A |
| 129 | B | 130 | C | 131 | A | 132 | D | 133 | C | 134 | B | 135 | D | 136 | C |
| 137 | A | 138 | B | 139 | C | 140 | D | 141 | A | 142 | D | 143 | C | 144 | C |
| 145 | C | 146 | A | 147 | B | 148 | B | 149 | B | 150 | B | 151 | B | 152 | C |
| 153 | C | 154 | C | 155 | A | 156 | A | 157 | B | 158 | D | 159 | A | 160 | A |
| 161 | D | | | | | | | | | | | | | | |

---

# 📝 Detailed Solutions

**Q1. (A)** The standard growth ordering is 1 < log n < √n < n < n log n < n² < 2ⁿ. Note √n = n^0.5 (polynomial) grows faster than log n, and n log n sits between n and n².

**Q2. (B)** √n = n^0.5 is polynomial, whereas log n is polylogarithmic; any polynomial eventually dominates any polylog, so √n grows faster.

**Q3. (C)** Θ gives a tight bound: Θ(g) = O(g) ∩ Ω(g), an upper and a lower bound simultaneously.

**Q4. (A)** Little-o, o(g), is the strict upper bound — f grows strictly slower than g. O(g) is the non-strict upper bound.

**Q5. (C)** O is an upper bound, so n = O(n²) is a true statement; it is simply not tight. Exams asking for "the complexity" want the tightest bound (Θ).

**Q6. (D)** By Stirling's approximation, log(n!) = Θ(n log n). This is the source of the comparison-sort lower bound.

**Q7. (A)** Drop constants and lower-order terms: the n² term dominates, so 3n² + 100n + 500 = Θ(n²).

**Q8. (B)** log₂ n and log₁₀ n differ only by a constant factor (change-of-base), which big-O ignores, so the base is irrelevant.

**Q9. (C)** Worst case is the guarantee the syllabus names explicitly and that exams mean by "the complexity".

**Q10. (A)** Amortised analysis is the average cost per operation over a worst-case **sequence** of operations, not a probabilistic average over inputs.

**Q11. (C)** Total doubling work over n insertions is n + n/2 + n/4 + … ≈ 2n, so amortised cost per insertion is O(1).

**Q12. (C)** Amortised is a worst-case guarantee over a sequence; average case is a probabilistic statement about inputs — they are different concepts.

**Q13. (B)** By definition Θ(g) = O(g) ∩ Ω(g) — the function is bounded both above and below by g.

**Q14. (C)** For large n, 2ⁿ ≪ n! (which is in turn ≪ nⁿ), so 2ⁿ < n!.

**Q15. (D)** Any polynomial (e.g. n^0.001) eventually beats any polylogarithm (e.g. log^100 n); polynomials dominate polylogs.

**Q16. (A)** Little-omega, ω(g), is the strict lower bound — f grows strictly faster than g.

**Q17. (B)** a = 2, b = 2, so n^(log₂2) = n¹ = n = f(n): Master theorem Case 2 → Θ(n·log n) = Θ(n log n). This is merge sort.

**Q18. (A)** n^(log₂2) = n, and f(n) = 1 is polynomially smaller: Case 1 → Θ(n). The n leaves dominate.

**Q19. (B)** a = 1, b = 2, n^(log₂1) = n⁰ = 1 = f(n): Case 2 → Θ(1·log n) = Θ(log n). This is binary search.

**Q20. (B)** n^(log₂2) = n, f(n) = n² is polynomially larger: Case 3 → Θ(n²). The root's combine step dominates.

**Q21. (C)** n^(log₂4) = n², f(n) = n is polynomially smaller: Case 1 → Θ(n²).

**Q22. (C)** n^(log₂8) = n³, f(n) = n² is smaller: Case 1 → Θ(n³).

**Q23. (B)** n^(log₂7) ≈ n^2.81, f(n) = n² is smaller: Case 1 → Θ(n^log₂7) ≈ Θ(n^2.81). This is Strassen's algorithm.

**Q24. (C)** n^(log₃9) = n², f(n) = n is smaller: Case 1 → Θ(n²).

**Q25. (B)** n^(log₄3) ≈ n^0.79, f(n) = n log n is polynomially larger (and satisfies the regularity condition): Case 3 → Θ(n log n).

**Q26. (C)** In Case 2, f(n) equals n^(log_b a), so every level costs the same; multiply by the number of levels (log n) → Θ(n^(log_b a) · log n).

**Q27. (B)** In T(n) = 2T(n/2) + n/log n, f(n) = n/log n is not polynomially comparable to n^(log₂2) = n, so the Master theorem does not apply.

**Q28. (B)** T(n) = T(n−1) + 1 unrolls to a sum of n constant terms → O(n). Example: linear search, factorial.

**Q29. (C)** T(n) = T(n−1) + n = n + (n−1) + … + 1 = n(n+1)/2 → O(n²). Example: insertion/selection sort.

**Q30. (C)** T(n) = 2T(n−1) + 1 doubles each step → O(2ⁿ). This is Towers of Hanoi (2ⁿ − 1 moves).

**Q31. (D)** T(n) = T(n−1) + T(n−2) grows like the Fibonacci numbers → O(2ⁿ) (more precisely O(φⁿ)). This is naïve Fibonacci.

**Q32. (B)** n^(log_b a) counts the total work at the leaves (all recursive calls at the bottom); f(n) is the root/combine work.

**Q33. (B)** n^(log₂3) ≈ n^1.585, f(n) = n is smaller: Case 1 → Θ(n^log₂3) ≈ O(n^1.585). This is Karatsuba multiplication.

**Q34. (B)** For subtract-and-conquer with a = 1, T(n) = aT(n−b) + f(n) → O(n·f(n)) (the recursion has depth n/b levels, each doing f-work with no branching).

**Q35. (B)** Each step halves the search space, so the number of comparisons is O(log n).

**Q36. (C)** Binary search needs a sorted array **and** random access to reach the middle element in O(1).

**Q37. (D)** A linked list has no random access — reaching the middle costs O(n) — so binary search degrades to O(n).

**Q38. (B)** The exact worst-case comparison count is ⌈log₂(n+1)⌉.

**Q39. (A)** ⌈log₂(1001)⌉ = 10, since 2¹⁰ = 1024 ≥ 1001 > 512 = 2⁹.

**Q40. (C)** Linear search may inspect every element → O(n) worst case.

**Q41. (C)** Interpolation search achieves O(log log n) average only when data is sorted and uniformly distributed.

**Q42. (A)** With a good hash function and load factor, hash-table lookup is O(1) on average (O(n) worst case).

**Q43. (B)** Jump search steps in blocks of √n then scans within a block → O(√n).

**Q44. (B)** Binary search discards one half each step, so the space shrinks by half.

**Q45. (B)** Quick sort is O(n²) worst case (bad pivots) and O(n log n) on average.

**Q46. (D)** Quick sort's partitioning swaps distant elements, breaking the relative order of equal keys, so it is unstable. Insertion, merge and bubble are stable.

**Q47. (A)** Heap sort is O(n log n) worst case and in-place (O(1) auxiliary space) — its distinguishing feature.

**Q48. (C)** Standard merge sort merges into a temporary array of size n → O(n) auxiliary space.

**Q49. (B)** The decision tree over n! orderings has height ≥ log₂(n!) = Ω(n log n).

**Q50. (B)** Counting sort indexes into a count array instead of comparing keys, so it is not comparison-based and dodges the Ω(n log n) bound.

**Q51. (B)** Insertion sort's inner loop exits immediately on sorted input, giving O(n) best case — it is adaptive.

**Q52. (B)** With a naïve first-element pivot, sorted input produces 1 : (n−1) partitions at every level → O(n²).

**Q53. (C)** Selection sort scans the unsorted remainder every pass, always doing exactly n(n−1)/2 comparisons regardless of input.

**Q54. (C)** Heap sort is the only comparison sort that is both O(n log n) worst case and in-place (O(1) space).

**Q55. (C)** Merge sort needs O(n) auxiliary space for merging, so it is not in-place. Heap, insertion and selection are in-place.

**Q56. (D)** Radix sort processes digits least-significant-first and relies on a **stable** subroutine to preserve earlier orderings.

**Q57. (B)** Quick, heap and selection sort are all unstable. Counting, radix, bucket, insertion, merge and bubble are stable.

**Q58. (A)** With an early-exit flag, a single pass over sorted input makes no swaps and stops → O(n).

**Q59. (B)** Merging two sorted arrays of sizes m and n takes at most m + n − 1 comparisons (the last element needs no comparison).

**Q60. (B)** Merge sort is O(n log n) in all cases because its splitting is data-oblivious.

**Q61. (B)** Radix sort runs in O(d(n + k)), where d is the number of digits and k the digit range.

**Q62. (A)** Selection sort performs at most n − 1 swaps → O(n) swaps, useful when writes are costly.

**Q63. (B)** O(n + inversions) means nearly-sorted input (few inversions) runs nearly linearly — insertion sort is adaptive.

**Q64. (B)** These sorts exploit key structure rather than comparing keys, so the decision-tree lower bound does not apply.

**Q65. (C)** There are n! possible orderings, so the decision tree has n! leaves; its height ≥ log₂(n!) = Θ(n log n).

**Q66. (C)** Bucket sort degrades to O(n²) worst case when all elements fall into one bucket.

**Q67. (B)** Insertion sort's low overhead and adaptivity make it ideal for the small subarrays used inside Timsort/introsort.

**Q68. (B)** Selection sort does only O(n) swaps, so it is preferred when writes are expensive (e.g. flash memory).

**Q69. (A)** Counting sort uses O(k) space for its count array, where k is the key range.

**Q70. (C)** Bubble sort's worst case makes n(n−1)/2 comparisons and up to n(n−1)/2 swaps.

**Q71. (B)** Strassen multiplies (n/2)-blocks with only 7 multiplications (instead of the naïve 8), giving T(n) = 7T(n/2) + n².

**Q72. (B)** T(n) = 7T(n/2) + n² → Θ(n^log₂7) ≈ O(n^2.81), beating naïve O(n³).

**Q73. (B)** Compare elements in pairs (n/2), then find max among larger halves (n/2 − 1) and min among smaller halves (n/2 − 1): total 3n/2 − 2.

**Q74. (C)** Naïve block multiplication uses 8 sub-multiplications: T(n) = 8T(n/2) + n² → n^(log₂8) = n³, Case 1 → O(n³).

**Q75. (B)** Divide and conquer: divide into subproblems, conquer (solve) recursively, then combine the results.

**Q76. (B)** Closest pair uses T(n) = 2T(n/2) + O(n) → O(n log n).

**Q77. (B)** Karatsuba: T(n) = 3T(n/2) + n → O(n^log₂3) ≈ O(n^1.585).

**Q78. (C)** Merge sort divides the array, sorts each half recursively, and merges — a classic divide-and-conquer algorithm.

**Q79. (A)** Naïvely, finding max and min separately takes (n−1) + (n−1) = 2n − 2 comparisons.

**Q80. (B)** Divide and conquer has optimal substructure but **not** overlapping subproblems (its subproblems are disjoint); that absence is what distinguishes it from DP.

**Q81. (C)** Huffman repeatedly merges the two lowest-frequency nodes — a locally optimal, provably globally optimal choice: greedy.

**Q82. (B)** 0/1 knapsack items are indivisible, so greedy fails; DP over (item, capacity) gives O(nW).

**Q83. (A)** Fractional knapsack allows splitting the last item, so greedy by value/weight ratio is provably optimal.

**Q84. (C)** Activity selection picks the activity with the earliest finish time, leaving the most room for the rest.

**Q85. (D)** Building the heap and doing n extract-min/insert operations gives O(n log n).

**Q86. (C)** Merging 5+9=14, 12+13=25, 14+16=30, 25+30=55, 45+55=100 gives lengths f=1, c=d=3, a=b=e=4. Total = 45(1)+12(3)+13(3)+5(4)+9(4)+16(4) = 45+36+39+20+36+64 = 224 bits.

**Q87. (A)** Average code length = 224/100 = 2.24 bits/char, versus 3 bits for fixed-length coding of 6 symbols.

**Q88. (D)** Huffman produces a prefix-free code — no codeword is a prefix of another — allowing unambiguous left-to-right decoding.

**Q89. (C)** Huffman gives frequent characters shorter codes and rare characters longer codes, minimising total length.

**Q90. (A)** Greedy takes 4 + 1 + 1 = 3 coins, but 3 + 3 = 2 coins is optimal; greedy fails for arbitrary (non-canonical) denominations.

**Q91. (B)** Greedy algorithms require the greedy-choice property and optimal substructure.

**Q92. (D)** Job sequencing sorts jobs by profit (descending) and schedules each as late as its deadline allows, maximising total profit.

**Q93. (A)** Because items are indivisible, greedy can commit to a high-ratio item that then blocks a strictly better combination — the core reason greedy fails on 0/1 knapsack.

**Q94. (B)** The standard pairing: fractional knapsack = greedy; 0/1 knapsack = dynamic programming.

**Q95. (A)** The LCS DP fills an (m+1)×(n+1) table with O(1) work per cell → O(mn).

**Q96. (A)** DP requires optimal substructure and overlapping subproblems; the greedy-choice property is what characterises greedy, not DP.

**Q97. (D)** Both DP and divide and conquer have optimal substructure, but only DP has overlapping subproblems — that is the distinguishing property.

**Q98. (C)** The 0/1 knapsack DP table is n×W, filled in O(nW).

**Q99. (A)** W is a numeric value needing only log W bits to write, so O(nW) is exponential in the input length — hence "pseudo-polynomial".

**Q100. (D)** Matrix chain DP considers O(n²) subchains, each taking O(n) to split → O(n³).

**Q101. (C)** Multiplying a p×q by a q×r matrix costs p·q·r scalar multiplications.

**Q102. (A)** Edit distance fills an (m+1)×(n+1) table with O(1) per cell → O(mn).

**Q103. (B)** Floyd–Warshall is a DP over "which intermediate vertices are allowed", incrementing k.

**Q104. (A)** DP has overlapping subproblems (so caching helps); divide and conquer's subproblems are disjoint, so caching gains nothing.

**Q105. (C)** Bottom-up tabulation fills a table iteratively from the smallest subproblem upward, avoiding recursion overhead.

**Q106. (D)** Keeping only the last two Fibonacci values needs O(1) space (and O(n) time).

**Q107. (B)** A(BC) = (30×5×60) + (10×30×60) = 9000 + 18000 = 27000, versus 4500 for (AB)C — six times the work.

**Q108. (B)** The LCS of "ABCBDAB" and "BDCABA" is "BCBA", of length 4.

**Q109. (A)** Given optimal substructure and overlapping subproblems, DP examines all choices and always yields an optimal solution.

**Q110. (D)** Held–Karp uses states (subset, endpoint): O(2ⁿ) subsets × O(n) endpoints × O(n) transitions → O(n²·2ⁿ).

**Q111. (C)** Kruskal uses disjoint-set (union–find) to test in near-O(1) whether adding an edge would form a cycle.

**Q112. (C)** Prim with a binary min-heap and adjacency list runs in O(E log V).

**Q113. (B)** A spanning tree of V vertices has exactly V − 1 edges.

**Q114. (A)** If all edge weights are distinct, the MST is unique; equal weights can allow several equally cheap trees.

**Q115. (C)** Kruskal is dominated by sorting the edges → O(E log E) = O(E log V).

**Q116. (D)** The O(V²) array version of Prim wins on dense graphs where E ≈ V².

**Q117. (B)** Kruskal (sorting-based) is better on sparse graphs.

**Q118. (A)** Cut property: for any partition of the vertices, the minimum-weight crossing edge belongs to some MST.

**Q119. (C)** Cycle property: the maximum-weight edge of any cycle is not in the MST (when it is unique).

**Q120. (D)** An MST minimises the total edge weight, not the path between any particular pair; the MST path is generally not the shortest u–v path.

**Q121. (C)** Union by rank plus path compression makes both find and union nearly O(1) amortised — the inverse Ackermann function α(n) < 5 for all practical n.

**Q122. (A)** Prim uses a priority queue (min-heap) to quickly find the cheapest edge leaving the current tree.

**Q123. (B)** Dijkstra assumes finalised distances never improve; a negative edge violates that, so it can give wrong answers.

**Q124. (C)** Bellman–Ford does V − 1 passes over all E edges → O(VE).

**Q125. (B)** Three nested loops over all vertices give O(V³), with O(V²) space.

**Q126. (A)** Dijkstra greedily finalises the closest unvisited vertex at each step.

**Q127. (B)** Bellman–Ford is dynamic programming: after k passes, all shortest paths using ≤ k edges are correct.

**Q128. (A)** On an unweighted graph, BFS finds single-source shortest paths in O(V + E).

**Q129. (B)** Any shortest path has at most V − 1 edges, so V − 1 relaxation passes suffice.

**Q130. (C)** Running one extra (V-th) pass: if any edge can still be relaxed, a negative cycle exists.

**Q131. (A)** Once Dijkstra finalises a vertex it never revisits it; a later negative edge could have produced a shorter path — this even happens without any negative cycle.

**Q132. (D)** Even with no negative cycle, a single negative edge can make Dijkstra commit early and return a wrong distance.

**Q133. (C)** The intermediate-vertex loop k must be outermost; otherwise the DP produces wrong results.

**Q134. (B)** Dijkstra with a binary heap runs in O(E log V) (O(V²) with a simple array).

**Q135. (D)** A negative d[i][i] means a path from i back to i has negative total weight — a negative cycle.

**Q136. (C)** Floyd–Warshall solves all-pairs shortest paths and handles negative edges (detecting negative cycles via a negative diagonal).

**Q137. (A)** NP-complete = in NP **and** NP-hard (every NP problem reduces to it in polynomial time).

**Q138. (B)** NP is the class of problems whose proposed solutions are verifiable in polynomial time.

**Q139. (C)** By the Cook–Levin theorem, SAT (boolean satisfiability) was the first problem proved NP-complete.

**Q140. (D)** NP-hard means "at least as hard as every NP problem"; such a problem need not be in NP and need not even be decidable (e.g. the halting problem).

**Q141. (A)** Euler circuit is in P (simple even-degree criterion); Hamiltonian circuit is NP-complete (no local criterion).

**Q142. (D)** If a problem is solvable in polynomial time, its solution can be verified in polynomial time, so P ⊆ NP.

**Q143. (C)** Minimum spanning tree is in P (Prim/Kruskal). TSP, Hamiltonian cycle and SAT are NP-complete.

**Q144. (C)** The halting problem is undecidable, so it is not in NP; being NP-hard but not in NP, it is not NP-complete.

**Q145. (C)** Whether P = NP is the most famous open problem in computer science.

**Q146. (A)** The decision version of 0/1 knapsack is NP-complete. Sorting, non-negative shortest path and MST are all in P.

**Q147. (B)** The subject is "the list" (singular), so it should read "was displayed"; the prepositional phrase "of participants" is a distractor.

**Q148. (B)** "Burn the midnight oil" means to work or study late into the night.

**Q149. (B)** Terms are n(n+1): 1×2, 2×3, 3×4, 4×5, 5×6, so next is 6×7 = 42 (differences 4, 6, 8, 10, 12).

**Q150. (B)** SI = 9680 − 8000 = 1680 over 2 years; rate = (1680 × 100)/(8000 × 2) = 168000/16000 = 10.5%.

**Q151. (B)** Neermahal stands in the middle of Rudrasagar Lake at Melaghar, a Ramsar-designated wetland.

**Q152. (C)** "Ephemeral" means lasting a very short time — short-lived.

**Q153. (C)** The antonym of "benevolent" (kind, well-meaning) is "malevolent" (wishing harm).

**Q154. (C)** 3, 5, 7, 11 are prime; 9 = 3×3 is composite, so 9 is the odd one out.

**Q155. (A)** Each letter shifts by +2: C→E, A→C, N→P, D→F, L→N, E→G, giving ECPFNG (as F→H, R→T, … confirm the +2 rule).

**Q156. (A)** 90 km/h = 25 m/s; time = length/speed = 150/25 = 6 seconds.

**Q157. (B)** Sum of first 10 naturals = 55; average = 55/10 = 5.5.

**Q158. (D)** A doctor treats a patient as a teacher teaches a student — the professional-to-recipient relationship.

**Q159. (A)** Agartala is the capital of Tripura (Aizawl, Imphal and Shillong are the capitals of Mizoram, Manipur and Meghalaya).

**Q160. (A)** Ujjayanta Palace, the former royal palace, is in Agartala.

**Q161. (D)** One pen costs 75/5 = ₹15; eight pens cost 15 × 8 = ₹120.
