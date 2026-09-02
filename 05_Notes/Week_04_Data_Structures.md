# Week 4 — Data Structures

**Syllabus §5 (part):** Arrays, stacks, queues, linked lists, trees, binary search trees, binary heaps, graphs.
**Estimated marks: ~7** (of the ~14 for Data Structures & Programming)

---

## 1. Arrays

Contiguous, fixed-size, homogeneous collection with O(1) random access.

| Operation | Complexity |
|---|---|
| Access by index | **O(1)** |
| Search (unsorted) | O(n) |
| Search (sorted) | O(log n) with binary search |
| Insert / delete at end | O(1) |
| Insert / delete at position | **O(n)** (shifting) |

📌 **Address of A[i] = Base + (i − lower_bound) × size**
📌 **Row-major A[i][j] = Base + [(i − L₁) × N_cols + (j − L₂)] × size**
📌 **Column-major A[i][j] = Base + [(j − L₂) × N_rows + (i − L₁)] × size**

**Sparse matrix** representations: triplet form (row, col, value) or linked list — used when most entries are zero.

---

## 2. ⭐ Stack (LIFO)

Operations: `push`, `pop`, `peek/top`, `isEmpty`, `isFull` — all **O(1)**.
Conditions: **overflow** (push on full), **underflow** (pop on empty).

### 2.1 Applications ⭐
- ⭐ **Function calls and recursion** (the call stack holds activation records)
- Expression conversion (infix ↔ postfix/prefix) and **evaluation**
- **Balanced parentheses** checking
- Undo/redo, browser back button
- **DFS** graph traversal
- Backtracking

### 2.2 ⭐ Expression notations

| Notation | Form | Example for A+B*C |
|---|---|---|
| **Infix** | operand operator operand | `A + B * C` |
| **Prefix** (Polish) | operator operands | `+A*BC` |
| **Postfix** (Reverse Polish) | operands operator | ⭐ `ABC*+` |

⭐ **Infix → Postfix algorithm:** scan left to right; operands go straight to output; for an operator, pop from the stack while the top has **greater or equal precedence**, then push; `(` is pushed, `)` pops until `(`.

🔢 `A + B * C` → `*` binds tighter → `A + (B*C)` → **`ABC*+`**
🔢 `(A + B) * C` → **`AB+C*`**
🔢 `A + B * C - D / E` → **`ABC*+DE/-`**

⭐ **Postfix evaluation:** scan left to right; push operands; on an operator pop two operands (**second popped is the left operand**), compute, push the result.

🔢 `5 6 2 + * 12 4 / -`
`6 2 +` → 8 · `5 8 *` → 40 · `12 4 /` → 3 · `40 3 -` → **37**

⚠ Order matters for `-` and `/`: for `a b -`, the result is `a − b` where `b` was popped first.

### 2.3 Implementation notes
- Array-based: fixed capacity, O(1) ops.
- Linked-list based: dynamic, push/pop at the head.
- **Two stacks in one array:** grow from opposite ends; overflow when the tops meet.

---

## 3. ⭐ Queue (FIFO)

Operations: `enqueue` (at rear), `dequeue` (from front), both **O(1)**.

### 3.1 ⭐ Circular queue

A linear array queue wastes space after dequeues; a circular queue reuses it with modular arithmetic.

📌 `rear = (rear + 1) % n` · `front = (front + 1) % n`

⭐ Keeping one slot empty to distinguish full from empty:

| Condition | Test |
|---|---|
| **Empty** | `front == rear` |
| ⭐ **Full** | ⭐ **`(rear + 1) % n == front`** |
| ⭐ **Capacity** | ⭐ **n − 1 elements** |

⚠ The one sacrificed slot is exactly what makes full and empty distinguishable. If a question says "using a counter", capacity becomes n.

### 3.2 Variants

| Variant | Description |
|---|---|
| **Deque** (double-ended queue) | Insert/delete at **both** ends. Input-restricted and output-restricted variants exist. |
| ⭐ **Priority queue** | Each element has a priority; the highest (or lowest) priority is dequeued first. Best implemented as a **binary heap**. |
| **Circular queue** | As above |

### 3.3 Applications
⭐ **BFS** graph traversal · CPU/disk scheduling · print/job spooling · buffers (I/O, keyboard) · call-centre systems.

---

## 4. ⭐ Linked lists

| Type | Structure |
|---|---|
| **Singly** | Each node has `data` + `next`; last node's `next` = NULL |
| **Doubly** | Each node has `prev` + `data` + `next` |
| **Circular singly** | Last node's `next` points to the head |
| **Circular doubly** | Both ends linked around |

### 4.1 Complexities

| Operation | Singly | Doubly |
|---|---|---|
| Access k-th element | O(n) | O(n) |
| Search | O(n) | O(n) |
| Insert/delete at **head** | O(1) | O(1) |
| Insert/delete at **tail** | O(n) (O(1) with tail pointer) | O(1) with tail pointer |
| ⭐ **Delete a given node** (pointer to it supplied) | ⭐ **O(n)** — must find the predecessor | ⭐ **O(1)** — `prev` is available |

⭐ This last row is the classic "what is O(1) in a DLL but O(n) in an SLL" question.

### 4.2 Array vs linked list ⭐

| | **Array** | **Linked list** |
|---|---|---|
| Memory | Contiguous | Scattered (dynamic) |
| Random access | ⭐ **O(1)** | ⭐ **O(n)** |
| Insertion/deletion in middle | O(n) shifting | O(1) *given the node position* |
| Size | Fixed (static) | Grows dynamically |
| Extra memory | None | Pointer per node |
| Cache performance | ⭐ Better (spatial locality) | Worse |
| Binary search | Possible | Not practical |

### 4.3 Standard algorithms
- **Reverse a list:** iterative with three pointers (`prev`, `curr`, `next`) — O(n) time, O(1) space.
- ⭐ **Cycle detection — Floyd's tortoise and hare:** slow moves 1 step, fast moves 2; they meet iff a cycle exists. O(n) time, O(1) space.
- **Find the middle:** slow/fast pointers; when fast reaches the end, slow is at the middle.
- **Merge two sorted lists:** O(m+n).
- ⚠ Losing the `next` pointer before reassigning is the standard bug in reversal questions.

---

## 5. ⭐⭐ Trees

### 5.1 Terminology

| Term | Meaning |
|---|---|
| **Root** | Node with no parent |
| **Leaf / external** | Node with no children |
| **Internal** | Node with at least one child |
| **Degree of a node** | Number of children |
| **Level** | Root at level 0 (or 1 — ⚠ check convention) |
| **Height / depth of tree** | Number of **edges** on the longest root-to-leaf path (root alone → height 0) |
| **Sibling** | Nodes with the same parent |
| **Ancestor / descendant** | Nodes on the path to root / in a subtree |

⚠ **Height convention is the single biggest source of wrong answers here.** "Root at height 0" (edge counting) vs "root at height 1" (node counting) shift every formula by one. Read the question.

### 5.2 ⭐ Binary tree types

| Type | Definition |
|---|---|
| **Full / strictly binary** | Every node has **0 or 2** children |
| **Complete** | All levels filled except possibly the last, which fills **left to right** |
| **Perfect** | All internal nodes have 2 children and all leaves are at the same level |
| **Degenerate / skewed** | Every node has one child (behaves like a linked list) |
| **Balanced** | Height is O(log n) |

### 5.3 ⭐ Key formulas (root at height 0)

📌 **Maximum nodes at level i = 2ⁱ**
📌 ⭐ **Maximum nodes in a tree of height h = 2^(h+1) − 1**
📌 **Minimum height for n nodes = ⌈log₂(n+1)⌉ − 1**
📌 **Maximum height for n nodes = n − 1** (skewed)
📌 ⭐ **In a full binary tree: leaves = internal nodes + 1**, i.e. **L = I + 1**
📌 ⭐ **A binary tree with n nodes has exactly (n + 1) NULL pointers**
📌 **Total links = 2n; used links = n − 1**
📌 A binary tree with n nodes has **n − 1 edges**
📌 Number of distinct binary trees with n nodes = **Catalan number C(n) = (2n)! / (n!(n+1)!)**
📌 Number of distinct **BSTs** with n distinct keys = also C(n); number of distinct **binary trees with labels** = C(n) × n!

🔢 n = 3 → C(3) = 6!/(3!·4!) = 720/144 = **5** distinct binary tree shapes.

⭐ **Array representation of a binary tree:**

| Indexing | Children of i | Parent of i |
|---|---|---|
| **0-based** | ⭐ **2i+1, 2i+2** | ⌊(i−1)/2⌋ |
| **1-based** | 2i, 2i+1 | ⌊i/2⌋ |

⚠ Always check which indexing the question uses.

### 5.4 ⭐⭐ Traversals

| Traversal | Order | Mnemonic |
|---|---|---|
| **Preorder** | **Root** → Left → Right | NLR |
| ⭐ **Inorder** | Left → **Root** → Right | LNR |
| **Postorder** | Left → Right → **Root** | LRN |
| **Level order** | Level by level (uses a **queue**) | BFS |

All are **O(n)** time. Recursive versions use O(h) stack space.

⭐ **Inorder traversal of a BST yields keys in sorted order.** This is the defining property and the basis of "is this a valid BST" questions.

⭐ **Reconstructing a tree from traversals:**

| Pair | Unique tree? |
|---|---|
| ⭐ **Inorder + Preorder** | ✅ **Yes** |
| ⭐ **Inorder + Postorder** | ✅ **Yes** |
| ⭐ **Inorder + Level order** | ✅ Yes |
| ⭐ **Preorder + Postorder** | ⭐ **❌ NO** (for general binary trees) |
| Any single traversal | ❌ No |

⚠ **Inorder is essential** — it is what splits the tree into left and right subtrees. Preorder + postorder cannot distinguish a lone left child from a lone right child. *(Exception: for a **full** binary tree, preorder + postorder is sufficient.)*

🔢 Preorder = `A B D E C F`, Inorder = `D B E A C F`
Root = A (first in preorder). Inorder left of A = `D B E`, right = `C F`.
In `D B E`, preorder order is `B D E` → B is root, D left, E right. In `C F`, preorder is `C F` → C root, F right child.

**Threaded binary tree:** NULL pointers are replaced by "threads" to the inorder predecessor/successor, allowing traversal without a stack or recursion.

### 5.5 ⭐ Binary Search Tree (BST)

**Property:** for every node, all keys in the left subtree < node key < all keys in the right subtree.

| Operation | Average | ⭐ Worst |
|---|---|---|
| Search | O(log n) | ⭐ **O(n)** |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

⭐ The worst case is a **skewed** tree, produced by inserting keys in sorted order — it degenerates into a linked list. This is precisely why balanced trees exist.

**Deletion — three cases:**
1. **Leaf:** remove it.
2. **One child:** replace the node with its child.
3. ⭐ **Two children:** replace with the **inorder successor** (minimum of the right subtree) or inorder predecessor (maximum of the left subtree), then delete that node recursively.

**Minimum** = leftmost node; **maximum** = rightmost node.

### 5.6 ⭐ AVL tree (self-balancing BST)

📌 **Balance factor = height(left subtree) − height(right subtree) ∈ {−1, 0, +1}**

📌 ⭐ **Height of an AVL tree with n nodes = O(log n)** (precisely, ≤ 1.44 log₂(n+2) − 0.328)

📌 Minimum nodes in an AVL tree of height h: **N(h) = N(h−1) + N(h−2) + 1**, with N(0)=1, N(1)=2.
🔢 N(2)=4, N(3)=7, N(4)=12, N(5)=20.

⭐ **Four rotations:**

| Imbalance | Rotation | Type |
|---|---|---|
| Left-Left (LL) | Single **right** rotation | Single |
| Right-Right (RR) | Single **left** rotation | Single |
| Left-Right (LR) | Left then right | Double |
| Right-Left (RL) | Right then left | Double |

Insertion needs at most **one** (single or double) rotation; deletion may need **O(log n)** rotations.

### 5.7 Other balanced trees (awareness)

| Tree | Note |
|---|---|
| **Red-black tree** | Colour-based balancing; height ≤ 2log₂(n+1). Fewer rotations than AVL on update; AVL is more strictly balanced so faster for lookup-heavy loads. |
| **B-tree** | m-way balanced search tree; keys **and** data in all nodes. Used for disk-based indexes. |
| ⭐ **B+ tree** | All data pointers in the **leaves**, which are **linked** → efficient range scans; internal nodes hold keys only, so fan-out is higher. **The database index structure.** (See Week 7.) |

---

## 6. ⭐ Binary heaps

**Definition:** a **complete** binary tree satisfying the heap property.
- **Min-heap:** every parent ≤ its children → the **minimum is at the root**.
- **Max-heap:** every parent ≥ its children → the maximum is at the root.

⚠ A heap is **partially ordered** — there is no ordering between siblings, and inorder traversal is *not* sorted. Only the root is guaranteed extremal.

Stored as an **array** with no pointers (0-based: children of i at 2i+1, 2i+2).

### 6.1 ⭐ Complexities

| Operation | Complexity |
|---|---|
| Find min (min-heap) | **O(1)** |
| Insert (then sift up) | **O(log n)** |
| Delete/extract min (then sift down) | **O(log n)** |
| Decrease key | O(log n) |
| ⭐ **Build heap from an unsorted array** | ⭐ **O(n)** |
| Heap sort | O(n log n) |
| Search for an arbitrary element | O(n) |

⭐ ⚠ **Build-heap is O(n), not O(n log n).** The bottom-up `heapify` procedure works from the last internal node upward; most nodes are near the leaves and sift down only a short distance. Inserting n elements **one at a time** *would* cost O(n log n) — that is the distinction being tested.

📌 In a heap of n elements, the number of leaves = ⌈n/2⌉ and the last internal node is at index ⌊n/2⌋ − 1 (0-based).
📌 Height of a heap with n nodes = ⌊log₂n⌋.

### 6.2 Applications
Priority queues · **Heap sort** · Dijkstra's and Prim's algorithms · finding the k-th largest/smallest · median maintenance (two heaps) · scheduling.

---

## 7. ⭐ Graphs

### 7.1 Terminology
**G = (V, E)**. Directed vs undirected · weighted vs unweighted · path · cycle · connected (undirected) · strongly connected (directed) · degree (in-degree/out-degree) · simple graph (no self-loops or multi-edges) · complete graph · bipartite · tree (connected acyclic) · forest · DAG (directed acyclic graph).

📌 ⭐ **Maximum edges in a simple undirected graph = n(n−1)/2**
📌 **Maximum edges in a simple directed graph = n(n−1)**
📌 **Sum of degrees = 2|E|** (handshaking lemma)
📌 A tree with n vertices has exactly **n − 1** edges
📌 Minimum edges to keep a graph connected = n − 1
📌 A complete graph Kₙ has n(n−1)/2 edges

### 7.2 ⭐ Representations

| | **Adjacency matrix** | **Adjacency list** |
|---|---|---|
| ⭐ **Space** | ⭐ **O(V²)** | ⭐ **O(V + E)** |
| Check if edge (u,v) exists | **O(1)** | O(degree(u)) |
| Iterate all neighbours of u | O(V) | O(degree(u)) |
| Add an edge | O(1) | O(1) |
| Best for | **Dense** graphs | ⭐ **Sparse** graphs |

**Adjacency matrix facts:** symmetric for undirected graphs · diagonal is 0 for a simple graph · the (i,j) entry of Aᵏ gives the number of walks of length k from i to j.

### 7.3 ⭐ Traversals

| | **BFS** | **DFS** |
|---|---|---|
| ⭐ **Data structure** | ⭐ **Queue** | ⭐ **Stack** (or recursion) |
| Order | Level by level | Deep first, then backtrack |
| Time (adj. list) | O(V + E) | O(V + E) |
| Time (adj. matrix) | O(V²) | O(V²) |
| Space | O(V) | O(V) |
| Finds shortest path? | ⭐ **Yes, in unweighted graphs** | ❌ No |

**BFS applications:** shortest path in unweighted graphs · connected components · bipartiteness testing · level/minimum-hop problems · peer-to-peer/crawlers.

**DFS applications:** ⭐ **cycle detection** · ⭐ **topological sorting** · strongly connected components (Kosaraju, Tarjan) · articulation points and bridges · path finding · maze solving.

**DFS edge classification (on directed graphs):** tree, back (⭐ indicates a **cycle**), forward, cross edges.

### 7.4 ⭐ Topological sort

A linear ordering of vertices such that for every directed edge u→v, u comes before v.

⭐ **Possible only for a DAG** — a cycle makes any ordering impossible. Therefore "topological sort fails" ⟺ "the graph has a cycle".

Two algorithms, both **O(V + E)**:
- **Kahn's algorithm:** repeatedly output a vertex of in-degree 0 and remove it (uses a queue).
- **DFS-based:** push vertices onto a stack on completion (post-order), then pop.

⚠ The topological order is **not unique** in general.

### 7.5 Cycle detection
- **Undirected:** DFS and find an edge to an already-visited vertex that is not the parent; or use union–find.
- **Directed:** DFS and find a **back edge** (an edge to a vertex currently on the recursion stack).

---

## 8. ⭐ Hashing

Maps keys to array indices via a hash function, giving **O(1) average** insert/search/delete.

📌 **Load factor α = n / m** (n = elements stored, m = table slots)

**Hash functions:** division method `h(k) = k mod m` (choose m prime, avoid powers of 2) · multiplication method · mid-square · folding. A good hash function is **uniform** and **deterministic**.

### 8.1 ⭐ Collision resolution

**(a) Separate chaining** — each slot holds a linked list.
- Load factor can exceed 1.
- Average search = O(1 + α); worst case O(n) when all keys collide.
- Simple deletion.

**(b) Open addressing** — store all elements in the table itself, probing for a free slot.

| Scheme | Probe sequence | Clustering |
|---|---|---|
| ⭐ **Linear probing** | `(h(k) + i) mod m` | ⭐ **Primary clustering** — long contiguous runs |
| **Quadratic probing** | `(h(k) + c₁i + c₂i²) mod m` | ⭐ **Secondary clustering** (no primary) |
| ⭐ **Double hashing** | `(h₁(k) + i·h₂(k)) mod m` | ⭐ **Best** — avoids both |

⚠ **Primary clustering (linear) vs secondary clustering (quadratic)** — know which belongs to which. In open addressing α ≤ 1 always, and **deletion requires tombstones** (a deleted marker), otherwise probe chains break.

🔢 Insert 12, 22, 32 into a table of size 10 with `h(k) = k mod 10` and linear probing:
12 → slot 2; 22 → slot 2 taken → slot 3; 32 → slots 2, 3 taken → slot 4.

**Rehashing:** when α exceeds a threshold (typically 0.7), allocate a bigger table (usually double, next prime) and reinsert all keys.

---

## 9. ⭐ Complexity summary table

| Structure | Access | Search | Insert | Delete |
|---|---|---|---|---|
| Array (unsorted) | O(1) | O(n) | O(1)* | O(n) |
| Array (sorted) | O(1) | O(log n) | O(n) | O(n) |
| Stack / Queue | O(n) | O(n) | **O(1)** | **O(1)** |
| Singly linked list | O(n) | O(n) | O(1) at head | O(1) at head |
| Doubly linked list | O(n) | O(n) | O(1) | O(1) given the node |
| **BST (average)** | O(log n) | O(log n) | O(log n) | O(log n) |
| ⭐ **BST (worst)** | **O(n)** | **O(n)** | **O(n)** | **O(n)** |
| **AVL / Red-black** | O(log n) | O(log n) | O(log n) | O(log n) |
| **Binary heap** | O(1) for min/max | O(n) | O(log n) | O(log n) |
| ⭐ **Hash table (average)** | — | **O(1)** | **O(1)** | **O(1)** |
| Hash table (worst) | — | O(n) | O(n) | O(n) |
| B / B+ tree | O(log n) | O(log n) | O(log n) | O(log n) |

\* amortised, at the end

---

## 10. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| Postfix of A+B*C | ABC*+ |
| Circular queue full | (rear+1)%n == front |
| Circular queue capacity | n − 1 |
| Recursion uses | Stack |
| BFS / DFS use | Queue / Stack |
| Max nodes, binary tree of height h | 2^(h+1) − 1 |
| NULL pointers in an n-node binary tree | n + 1 |
| Full binary tree: leaves | internal + 1 |
| Distinct binary trees with n nodes | Catalan C(n) |
| Heap array children (0-based) | 2i+1, 2i+2 |
| Sorted traversal of a BST | Inorder |
| Unique tree from | Inorder + (pre or post)order |
| Preorder + postorder | ❌ Not unique (general binary tree) |
| BST worst-case search | O(n) — skewed |
| AVL balance factor | −1, 0, +1 |
| AVL height | O(log n) |
| Build-heap | **O(n)** |
| Heap insert | O(log n) |
| Max edges, simple undirected | n(n−1)/2 |
| Adjacency matrix / list space | O(V²) / O(V+E) |
| Topological sort requires | DAG |
| Linear probing problem | Primary clustering |
| Quadratic probing problem | Secondary clustering |
| Load factor | n/m |
| O(1) in DLL, O(n) in SLL | Delete a given node |

---

## 11. Common traps ⚠

1. **Build-heap is O(n)**, not O(n log n).
2. **Preorder + postorder does not determine a general binary tree.**
3. **Height convention** — root at 0 or 1 changes every formula.
4. **Heap array indexing** — 0-based (2i+1, 2i+2) vs 1-based (2i, 2i+1).
5. **A heap's inorder traversal is not sorted** — only the root is extremal.
6. **Circular queue capacity is n − 1**, not n (when using the one-empty-slot method).
7. **BST worst case is O(n)** — many candidates answer O(log n) reflexively.
8. **Primary vs secondary clustering** map to linear vs quadratic probing.
9. **In postfix evaluation the second value popped is the left operand.**
10. **Adjacency matrix space is O(V²) regardless of how few edges there are.**
11. **Topological order is not unique.**
12. **Deletion in open addressing needs tombstones.**

---

## 12. Practice

- GATE: [`Paper2_S05_Data_Structures_and_Programming/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — **370 questions** (DS 238)
- State-PSC level: [`Paper2_S05_.../`](../02_State_PSC_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — **578 questions**
- Test: [`Week_04_Test.md`](../04_Mock_Tests/Week_04_Test.md)

**Priority order if short on time:** tree formulas & traversals → the complexity summary table (§9) → stacks/postfix → BST and AVL → heaps (especially build-heap) → graph representations & BFS/DFS → hashing collision resolution.
