# Week 4 — Data Structures

**Syllabus §5 (part):** Arrays, stacks, queues, linked lists, trees, binary search trees, binary heaps, graphs.
**Estimated marks: ~7** (of the ~14 for Data Structures & Programming)

---

## 💡 What this subject is about

A **data structure** is a way of organising data in memory so that the operations you care about are fast.

There is no "best" structure — only trade-offs. An array gives instant access by index but slow insertion in the middle. A linked list gives instant insertion but slow access by index. Choosing correctly is most of what makes a program fast.

**The one question to ask of every structure in this file:** *what does it make fast, and what does it make slow?* If you can answer that for each, the complexity table (§9) writes itself.

---

# 1. Arrays

## 💡 The idea

An array is a **contiguous block of memory** holding elements of the same type.

```
Index:      0     1     2     3     4
          ┌─────┬─────┬─────┬─────┬─────┐
          │ 10  │ 20  │ 30  │ 40  │ 50  │
          └─────┴─────┴─────┴─────┴─────┘
Address:  1000  1004  1008  1012  1016
```

⭐ **Why access is O(1):** the computer does not search for `A[3]`. It **calculates** the address arithmetically:
```
address of A[3] = 1000 + 3 × 4 = 1012
```
One multiply and one add — constant time, regardless of array size.

⭐ **Why insertion in the middle is O(n):** to insert at position 1, every later element must physically **shift right** to make room. With a million elements, that is a million moves.

| Operation | Complexity | Why |
|---|---|---|
| Access by index | ⭐ **O(1)** | Direct address calculation |
| Search (unsorted) | O(n) | Must check every element |
| Search (sorted) | O(log n) | Binary search |
| Insert/delete at end | O(1) | No shifting |
| ⭐ **Insert/delete at position** | ⭐ **O(n)** | Shifting |

📌 **Address of A[i] = Base + (i − lower_bound) × size**
📌 ⭐ **Row-major A[i][j] = Base + [(i − L₁) × N_cols + (j − L₂)] × size**
📌 ⭐ **Column-major A[i][j] = Base + [(j − L₂) × N_rows + (i − L₁)] × size**

🔢 `int A[10][20]`, base 1000, 4 bytes, row-major, 0-based. Address of `A[3][5]`:
1000 + (3 × 20 + 5) × 4 = 1000 + 65 × 4 = **1260**

**Sparse matrix:** if a matrix is mostly zeros (say 1000×1000 with only 50 non-zeros), storing all million entries wastes memory. Store instead a list of **(row, column, value)** triplets — 50 entries. This is the *triplet representation*.

---

# 2. ⭐⭐ Stack (LIFO)

## 💡 The idea

A **stack** is a container where you can only add and remove at **one end**, called the top.

💡 **Analogy: a stack of plates.** You put a clean plate on top; you take the top plate off. You cannot pull one out of the middle. The **last** plate put on is the **first** taken off — hence **LIFO: Last In, First Out**.

```
     push ↓   ↑ pop
        ┌─────┐
        │  30 │ ← top
        ├─────┤
        │  20 │
        ├─────┤
        │  10 │
        └─────┘
```

**Operations, all O(1):**
- `push(x)` — add x on top
- `pop()` — remove and return the top
- `peek()` / `top()` — look at the top without removing
- `isEmpty()`, `isFull()`

⚠ **Overflow** = pushing onto a full stack. **Underflow** = popping an empty stack.

## 2.1 ⭐ Why stacks matter — the applications

⭐ **1. Function calls and recursion.** When `f()` calls `g()`, the computer must remember where to return. It **pushes** an activation record. When `g()` returns, it **pops**. Since calls nest perfectly (the most recent call always returns first), LIFO is exactly right.
🔢 This is why deep recursion causes **stack overflow** — too many un-popped frames.

⭐ **2. Expression conversion and evaluation.** See below.

⭐ **3. Balanced parentheses checking.** Push every opening bracket; on a closing bracket, pop and check it matches.
🔢 `{[()]}` → push `{`, `[`, `(`; then `)` pops `(` ✅, `]` pops `[` ✅, `}` pops `{` ✅, stack empty → **balanced**.
🔢 `{[(])}` → `]` tries to pop but finds `(` → **not balanced**.

**4. Undo/redo** and the browser back button — the most recent action is undone first.
⭐ **5. DFS** graph traversal (§7.3).
**6. Backtracking** algorithms (maze solving, N-queens).

## 2.2 ⭐⭐ Expression notations

### 💡 The idea

`A + B * C` is **infix** — the operator sits *between* its operands. Humans like it, but it is ambiguous without precedence rules and parentheses. Machines prefer notations that need neither.

| Notation | Form | Example for A+B*C |
|---|---|---|
| **Infix** | operand **operator** operand | `A + B * C` |
| **Prefix** (Polish) | **operator** operand operand | `+A*BC` |
| ⭐ **Postfix** (Reverse Polish) | operand operand **operator** | ⭐ `ABC*+` |

⭐ **Why postfix is useful:** it needs **no parentheses and no precedence rules** — the order is completely determined. And it can be evaluated with a single left-to-right scan using one stack. That is why compilers generate it (Week 11) and why stack machines exist (Week 2).

### ⭐ Infix → postfix, by hand

**The reliable manual method:** fully parenthesise the expression according to precedence, then move each operator to just after its right operand.

🔢 `A + B * C`
→ `A + (B * C)` → `A (B C *) +` → ⭐ **`ABC*+`**

🔢 `(A + B) * C`
→ already grouped → `(A B +) C *` → ⭐ **`AB+C*`**

🔢 `A + B * C − D / E`
→ `(A + (B*C)) − (D/E)` → `((A (BC*) +) (DE/) −)` → ⭐ **`ABC*+DE/-`**

🔢 `A * B + C * D`
→ `(A*B) + (C*D)` → **`AB*CD*+`**

### The stack algorithm (for completeness)

Scan left to right:
- **Operand** → send straight to output
- **Operator** → while the stack top has **greater or equal** precedence, pop it to output; then push this operator
- **`(`** → push
- **`)`** → pop to output until `(` is found; discard both parentheses
- At the end, pop everything remaining

⚠ For **right-associative** operators (like `^`), the rule is "strictly greater" rather than "greater or equal".

### ⭐⭐ Postfix evaluation

**Algorithm:** scan left to right. Push operands. On an operator, **pop two**, apply, push the result.

⚠ ⭐ **Order matters:** the **second value popped is the LEFT operand.**
For `a b −`, you pop `b` first, then `a`, and compute **a − b**.

🔢 **Evaluate `5 6 2 + * 12 4 / −`**

| Token | Action | Stack (bottom→top) |
|---|---|---|
| `5` | push | 5 |
| `6` | push | 5, 6 |
| `2` | push | 5, 6, 2 |
| `+` | pop 2, pop 6 → 6+2 = 8, push | 5, 8 |
| `*` | pop 8, pop 5 → 5×8 = 40, push | 40 |
| `12` | push | 40, 12 |
| `4` | push | 40, 12, 4 |
| `/` | pop 4, pop 12 → 12/4 = 3, push | 40, 3 |
| `−` | pop 3, pop 40 → 40−3 = **37**, push | **37** |

⭐ Answer: **37**

🔢 **Evaluate `2 3 4 * +`** → `3*4 = 12`, then `2+12` = **14**

## 2.3 Implementation notes

- **Array-based:** fixed capacity, O(1) ops, `top` is just an index.
- **Linked-list based:** dynamic size, push/pop at the head.
- **Two stacks in one array:** grow from opposite ends toward the middle; overflow only when the two tops meet — better space utilisation than splitting the array in half.

---

# 3. ⭐⭐ Queue (FIFO)

## 💡 The idea

A **queue** allows insertion at one end (the **rear**) and removal at the other (the **front**).

💡 **Analogy: a queue at a ticket counter.** The first person to arrive is the first served — **FIFO: First In, First Out**. Nobody jumps the line.

```
   dequeue ←  ┌─────┬─────┬─────┬─────┐  ← enqueue
   (front)    │ 10  │ 20  │ 30  │ 40  │    (rear)
              └─────┴─────┴─────┴─────┘
```

Both operations are **O(1)**.

## 3.1 ⭐⭐ The circular queue — and why it exists

### 💡 The problem with a plain array queue

```
Start:      [ 10 | 20 | 30 |    |    ]   front=0, rear=2
Dequeue ×2: [    |    | 30 |    |    ]   front=2, rear=2
Enqueue ×2: [    |    | 30 | 40 | 50 ]   front=2, rear=4
Enqueue?    rear is at the end — "full"!
```
⚠ The queue reports **full** while two slots sit empty at the front. That wasted space is unacceptable.

### ⭐ The fix

Treat the array as a **circle** — after the last index, wrap back to 0.

📌 `rear = (rear + 1) % n` and `front = (front + 1) % n`

```
        ┌───┐
    ┌───┤ 0 ├───┐
    │ 4 │   │ 1 │      after index 4, wrap to 0
    └───┤ 3 ├───┘
        │ 2 │
        └───┘
```

### ⚠ The full-vs-empty problem

Now a new difficulty: with front and rear wrapping, `front == rear` occurs **both** when the queue is empty **and** when it is completely full. The two states are indistinguishable.

⭐ **The standard solution: deliberately keep one slot empty.**

| Condition | ⭐ Test |
|---|---|
| **Empty** | `front == rear` |
| ⭐ **Full** | ⭐ **`(rear + 1) % n == front`** |
| ⭐ **Maximum elements** | ⭐ **n − 1** |

⭐ The sacrificed slot is precisely what makes full and empty distinguishable.

⚠ If a question says the implementation uses a **separate counter** of elements, then full and empty are distinguishable without sacrifice and the capacity is **n**. Read carefully.

🔢 A circular queue on an array of size 5 holds at most **4** elements (one-empty-slot method).

## 3.2 Variants

| Variant | 💡 Description |
|---|---|
| **Deque** (double-ended queue) | Insert **and** delete at **both** ends. Input-restricted (insert at one end only) and output-restricted variants exist. A deque can behave as either a stack or a queue |
| ⭐ **Priority queue** | Elements have priorities; ⭐ **the highest (or lowest) priority is dequeued first, regardless of arrival order**. Best implemented as a **binary heap** (§6) |
| **Circular queue** | As above |

⚠ ⭐ A priority queue is **not FIFO** — that is its whole point.

## 3.3 Applications

⭐ **BFS** graph traversal (§7.3) · CPU scheduling and disk scheduling (Week 6) · print/job spooling · I/O and keyboard **buffers** · call-centre and ticketing systems · any producer–consumer buffer.

💡 **Why buffers are queues:** data arrives at one rate and is consumed at another; the queue absorbs the mismatch while preserving order.

---

# 4. ⭐⭐ Linked lists

## 💡 The idea

An array's weakness is that it is **contiguous** — inserting means shifting, and the size is fixed.

A **linked list** abandons contiguity. Each element (**node**) stores its data **plus a pointer to the next node**. Nodes can live anywhere in memory; the pointers hold the sequence together.

```
head
 │
 ▼
┌────┬───┐   ┌────┬───┐   ┌────┬───┐
│ 10 │ ●─┼──►│ 20 │ ●─┼──►│ 30 │ ✕ │  (✕ = NULL)
└────┴───┘   └────┴───┘   └────┴───┘
```

```c
struct Node { int data; struct Node *next; };
```

⭐ **The trade-off in one line:** you gain O(1) insertion/deletion anywhere (just rewire two pointers), and you lose O(1) random access (you must walk from the head).

### 💡 Insertion is O(1) — see why

To insert 15 between 10 and 20, no data moves at all:
```
Before:  [10|●]──►[20|●]──►[30|✕]

         [10|●]──┐   ┌─►[20|●]──►[30|✕]
                 │   │
                 ▼   │
               [15|●]┘

After:   [10|●]──►[15|●]──►[20|●]──►[30|✕]
```
Two pointer assignments. In an array, everything after position 1 would shift.

## 4.1 Types

| Type | Structure |
|---|---|
| **Singly linked** | `data` + `next`; the last node's `next` is NULL |
| ⭐ **Doubly linked** | `prev` + `data` + `next` — can traverse **both ways** |
| **Circular singly** | The last node's `next` points back to the head (no NULL) |
| **Circular doubly** | Both ends joined |

## 4.2 ⭐ Complexities — and the one that gets asked

| Operation | Singly | ⭐ Doubly |
|---|---|---|
| Access the k-th element | O(n) | O(n) |
| Search | O(n) | O(n) |
| Insert/delete at **head** | O(1) | O(1) |
| Insert/delete at **tail** | O(n) (O(1) with a tail pointer) | O(1) with a tail pointer |
| ⭐ **Delete a node, given a pointer TO it** | ⭐ **O(n)** | ⭐ **O(1)** |

### 💡 Why that last row differs — the classic question

To delete a node, you must make its **predecessor** point past it.
- In a **doubly** linked list the node has a `prev` pointer, so the predecessor is immediately available → **O(1)**.
- In a **singly** linked list there is no way back, so you must **walk from the head** to find the predecessor → **O(n)**.

⭐ *"Which operation is O(1) in a DLL but O(n) in an SLL, given only a pointer to the node?"* → **deletion of that node**.

## 4.3 ⭐ Array vs linked list

| | ⭐ **Array** | ⭐ **Linked list** |
|---|---|---|
| Memory layout | ⭐ **Contiguous** | Scattered |
| ⭐ Random access | ⭐ **O(1)** | ⭐ **O(n)** |
| Insert/delete in middle | O(n) (shifting) | O(1) *given the position* |
| Size | Fixed at allocation | ⭐ **Grows dynamically** |
| Extra memory | None | ⭐ **One pointer per node** |
| ⭐ **Cache performance** | ⭐ **Better** (spatial locality — Week 2) | Worse (nodes scattered) |
| Binary search | ✅ Possible | ❌ Not practical (no random access) |

⭐ **The cache point is worth remembering:** in practice, arrays often beat linked lists even for insertion-heavy workloads, because array elements sit together and get pulled into the cache in blocks. Linked-list traversal causes a cache miss per node.

## 4.4 ⭐ Standard algorithms

### Reverse a singly linked list — O(n) time, O(1) space

```c
prev = NULL; curr = head;
while (curr != NULL) {
    next = curr->next;    // ⚠ save it FIRST
    curr->next = prev;    // reverse the link
    prev = curr;          // advance
    curr = next;
}
head = prev;
```
⚠ ⭐ **Saving `next` before overwriting `curr->next` is essential** — otherwise you lose the rest of the list. This is the standard bug in exam code snippets.

### ⭐ Cycle detection — Floyd's tortoise and hare

💡 **The idea:** run two pointers, one moving **1 step**, the other **2 steps**, per iteration. If there is no cycle, the fast one reaches NULL. If there **is** a cycle, the fast pointer laps the slow one and they **meet**.

💡 **Why they must meet:** once both are inside the loop, the gap between them closes by exactly 1 each iteration, so it eventually reaches 0.

📌 **O(n) time, O(1) space** — better than storing visited nodes in a hash set (which is O(n) space).

### Find the middle node
Same two-pointer trick: when the fast pointer reaches the end, the slow pointer is at the middle. One pass, no length calculation.

### Merge two sorted lists
Walk both, always taking the smaller head. **O(m + n)**.

---

# 5. ⭐⭐⭐ Trees

## 💡 The idea

Arrays and lists are **linear** — one element after another. But much real data is **hierarchical**: a file system, an organisation chart, a family tree, an expression's structure.

A **tree** is a hierarchical structure: one **root** at the top, each node having zero or more **children**, and no cycles.

```
              A          ← root (level 0)
            /   \
           B     C       ← level 1
          / \     \
         D   E     F     ← level 2 (D, E, F are leaves)
```

⭐ **The payoff:** a *balanced* tree of n nodes has height **O(log n)**, so searching it takes O(log n) steps instead of O(n). That is the entire reason trees exist as a search structure.

## 5.1 ⭐ Terminology

| Term | Meaning |
|---|---|
| **Root** | The single node with no parent (A above) |
| **Leaf / external node** | A node with no children (D, E, F) |
| **Internal node** | A node with at least one child |
| **Degree of a node** | Its number of children |
| **Degree of the tree** | The maximum degree of any node |
| **Level** | Distance from the root — ⚠ root at level **0** or **1** by convention |
| ⭐ **Height / depth of the tree** | The number of **edges** on the longest root-to-leaf path. ⚠ Root alone → height **0** in the edge convention |
| **Sibling** | Nodes sharing a parent |
| **Ancestor / descendant** | On the path to the root / in the subtree |
| **Subtree** | A node together with all its descendants |
| **Forest** | A collection of disjoint trees |

⚠ ⭐ **The height convention is the single biggest source of wrong answers in this topic.**
- "Root at height 0" (counting **edges**): a tree of height h has at most 2^(h+1) − 1 nodes
- "Root at height 1" (counting **nodes/levels**): the same tree has at most 2^h − 1 nodes

**Always check which the question uses.** If it says "a tree with only a root has height 0", it is the edge convention. This file uses **root at height 0** throughout.

## 5.2 ⭐ Binary tree types

A **binary tree** allows each node at most **two** children (left and right).

| Type | Definition | Picture |
|---|---|---|
| ⭐ **Full / strictly binary** | Every node has ⭐ **0 or 2** children (never exactly 1) | No node with a lone child |
| ⭐ **Complete** | All levels filled except possibly the last, which is filled ⭐ **left to right** | The shape a **heap** has |
| **Perfect** | All internal nodes have 2 children **and** all leaves are at the same level | A perfect triangle |
| ⭐ **Degenerate / skewed** | Every node has exactly one child | ⭐ Behaves like a **linked list** |
| **Balanced** | Height is O(log n) | AVL, red-black |

```
Full (0 or 2 children):     Complete (fills left→right):   Skewed:
        A                            A                        A
       / \                          / \                        \
      B   C                        B   C                        B
     / \                          / \                            \
    D   E                        D   E                            C
```

## 5.3 ⭐⭐ The formulas (root at height 0)

📌 **Maximum nodes at level i = 2ⁱ**
*Why:* level 0 has 1 node; each level can at most double.

📌 ⭐ **Maximum nodes in a tree of height h = 2^(h+1) − 1**
*Why:* sum the geometric series 2⁰ + 2¹ + … + 2ʰ = 2^(h+1) − 1.
🔢 h = 3 → 1 + 2 + 4 + 8 = **15** nodes.

📌 **Minimum height for n nodes = ⌈log₂(n+1)⌉ − 1** (a perfectly packed tree)
📌 ⭐ **Maximum height for n nodes = n − 1** (a skewed tree)

📌 ⭐ **In a FULL binary tree: leaves = internal nodes + 1** (L = I + 1)

📌 ⭐⭐ **A binary tree with n nodes has exactly (n + 1) NULL pointers.**

### 💡 Why (n+1) NULL pointers — worth understanding, not memorising

Every node has 2 child pointer slots, so there are **2n** slots in total.
Every node **except the root** is pointed to by exactly one of those slots, so **n − 1** slots hold real pointers.
Therefore NULL slots = 2n − (n − 1) = ⭐ **n + 1** ✅

🔢 A tree with 5 nodes has 10 pointer slots, 4 used, **6 NULL**.

📌 A binary tree with n nodes has **n − 1 edges** (each non-root node contributes one edge upward).

📌 ⭐ **Number of distinct binary tree SHAPES with n nodes = the Catalan number**
**C(n) = (2n)! / (n! × (n+1)!)**

🔢 C(0)=1, C(1)=1, C(2)=2, **C(3)=5**, C(4)=14, C(5)=42
🔢 For n = 3: C(3) = 6!/(3!·4!) = 720/(6·24) = **5** distinct shapes.

📌 Number of distinct **BSTs** with n distinct keys = **C(n)** (the keys' placement is forced once the shape is chosen).
📌 Number of distinct **labelled** binary trees with n nodes = C(n) × n!

## 5.4 ⭐ Array representation of a binary tree

### 💡 The idea

A **complete** binary tree can be stored in a plain array with **no pointers at all** — the parent/child relationships are computed arithmetically.

```
Tree:          10
              /  \
            20    30
           /  \
         40    50

Array:  [10, 20, 30, 40, 50]
Index:    0   1   2   3   4
```

📌 ⭐ **0-based indexing:** children of node `i` are at ⭐ **2i+1 and 2i+2**; parent is `⌊(i−1)/2⌋`
📌 **1-based indexing:** children of node `i` are at **2i and 2i+1**; parent is `⌊i/2⌋`

🔢 0-based, node at index 1 (value 20): children at 2(1)+1 = **3** (40) and 2(1)+2 = **4** (50) ✅

⚠ ⭐ **Always check which indexing convention the question uses** — options include both.

⭐ This representation is exactly what **heaps** use (§6), and it is why heaps must be *complete* trees: any gaps would waste array slots and break the arithmetic.

## 5.5 ⭐⭐⭐ Traversals

## 💡 The idea

To "visit every node" in a linear structure is obvious — walk from start to end. In a tree there are several sensible orders, distinguished by **when you visit the root relative to its subtrees**.

```
              A
            /   \
           B     C
          / \     \
         D   E     F
```

| Traversal | Order | Mnemonic | Result above |
|---|---|---|---|
| ⭐ **Preorder** | **Root** → Left → Right | **N**LR | **A B D E C F** |
| ⭐⭐ **Inorder** | Left → **Root** → Right | L**N**R | **D B E A C F** |
| ⭐ **Postorder** | Left → Right → **Root** | LR**N** | **D E B F C A** |
| **Level order** | Level by level, left to right | BFS | **A B C D E F** |

⭐ **Memory hook:** the position of "**N**" (node/root) in the mnemonic tells you when the root is visited. **Pre** = root **first**, **In** = root in the **middle**, **Post** = root **last**.

All three depth-first traversals are **O(n)** time and use **O(h)** stack space. Level order is O(n) time, O(width) space, and uses a **queue**.

### ⭐ How to trace them quickly by hand

**Preorder** — start at the root and "hug the left wall", writing each node the **first** time you meet it.
**Inorder** — project every node straight **down** onto a horizontal line and read left to right.
**Postorder** — write each node the **last** time you leave it.

🔢 **Practice on this tree:**
```
            1
          /   \
         2     3
        / \   /
       4   5 6
```
- **Preorder:** 1, 2, 4, 5, 3, 6
- **Inorder:** 4, 2, 5, 1, 6, 3
- **Postorder:** 4, 5, 2, 6, 3, 1
- **Level order:** 1, 2, 3, 4, 5, 6

## 5.6 ⭐⭐ Reconstructing a tree from traversals

### 💡 The idea

Given two traversals, can you rebuild the unique original tree?

⭐ **Inorder is the essential one**, because it is the only traversal that tells you **which nodes are on the LEFT of the root and which are on the RIGHT**. Preorder and postorder only tell you which node *is* the root.

| Pair | Unique tree? |
|---|---|
| ⭐ **Inorder + Preorder** | ⭐ **✅ Yes** |
| ⭐ **Inorder + Postorder** | ⭐ **✅ Yes** |
| **Inorder + Level order** | ✅ Yes |
| ⭐ **Preorder + Postorder** | ⭐ **❌ NO** (for general binary trees) |
| Any single traversal | ❌ No |

### ⚠ Why preorder + postorder fails

```
Tree 1:   A          Tree 2:   A
         /                      \
        B                        B

Preorder:  A B                   A B
Postorder: B A                   B A
```
⭐ **Identical traversals, different trees.** Neither traversal reveals whether B is a left or a right child — only inorder would (`B A` vs `A B`).

⚠ **Exception:** for a **full** binary tree (every node has 0 or 2 children), preorder + postorder *is* sufficient, because a lone child cannot occur.

### 🔢 Worked reconstruction

**Preorder = `A B D E C F`, Inorder = `D B E A C F`.**

1. **Preorder's first element is the root** → **A**
2. Find A in the inorder: `D B E | A | C F`
   → left subtree = {D, B, E}, right subtree = {C, F}
3. **Left subtree.** Its preorder (next 3 elements) = `B D E`; its inorder = `D B E`.
   Root = **B**. In inorder, `D | B | E` → D is left child, E is right child.
4. **Right subtree.** Its preorder = `C F`; its inorder = `C F`.
   Root = **C**. In inorder, `C | F` — nothing left of C, F is to the right → F is C's **right** child.

```
            A
          /   \
         B     C
        / \     \
       D   E     F
```
✅ Reconstructed.

## 5.7 ⭐ Threaded binary tree

💡 **The idea:** §5.3 showed that an n-node binary tree wastes **n+1** NULL pointers. A **threaded** tree puts them to work: each NULL is replaced by a "thread" pointing to the node's **inorder predecessor or successor**.

⭐ **Payoff:** inorder traversal becomes possible **without recursion and without a stack** — O(1) extra space.

---

# 6. ⭐⭐⭐ Binary Search Tree (BST)

## 💡 The idea

A plain binary tree gives you no search advantage — you might have to look at every node. A **BST** adds one ordering rule that makes search fast:

📌 ⭐ **For every node: all keys in its LEFT subtree < node's key < all keys in its RIGHT subtree.**

```
             50
           /    \
         30      70
        /  \    /  \
      20   40  60   80
```

💡 **Why this makes search O(log n):** at each node you compare once and **discard half the remaining tree**. Looking for 40: 40 < 50 → go left; 40 > 30 → go right; found. Three comparisons for seven nodes. It is binary search, made into a data structure.

## 6.1 ⭐ Operations

| Operation | Average | ⭐ Worst |
|---|---|---|
| Search | O(log n) | ⭐ **O(n)** |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

### ⚠⚠ Why the worst case is O(n) — the crucial point

Insert 10, 20, 30, 40, 50 **in sorted order**:
```
   10
     \
      20
        \
         30
           \
            40
              \
               50
```
⭐ Every insertion goes right. The tree **degenerates into a linked list**, and search becomes O(n).

⭐ **This is exactly why balanced trees (AVL, red-black) exist**, and it is the most common mistake in this topic — candidates answer O(log n) reflexively.

## 6.2 ⭐⭐ The defining property: inorder gives sorted order

⭐ **An inorder traversal of a BST visits the keys in non-decreasing sorted order.**

🔢 The tree above: inorder = **20, 30, 40, 50, 60, 70, 80** ✅

💡 **Why:** inorder is "everything left of me, then me, then everything right of me" — and the BST property says everything left is smaller and everything right is larger. So the definition matches exactly.

⭐ This is the basis of "is this a valid BST?" questions: do an inorder traversal and check it is sorted.

## 6.3 ⭐ Deletion — the three cases

**Case 1: the node is a LEAF.** Just remove it.

**Case 2: the node has ONE child.** Replace the node with its child.
```
   30              30
     \      →        \
      40              50
        \
         50
```

**Case 3: ⭐ the node has TWO children.** You cannot simply remove it — which child takes its place?
⭐ **Replace the key with its INORDER SUCCESSOR** (the smallest key in the right subtree) — or equivalently the inorder predecessor (the largest in the left subtree) — then delete *that* node (which has at most one child, so it reduces to case 1 or 2).

🔢 Delete 50 from:
```
             50                        60
           /    \                    /    \
         30      70    →           30      70
        /  \    /  \              /  \       \
      20   40  60   80          20   40      80
```
The inorder successor of 50 is **60** (leftmost node of the right subtree). Copy 60 into the root's place and delete the original 60 node.

💡 **Why the successor works:** it is the smallest key larger than everything on the left and smaller than everything else on the right — precisely the BST property the root must satisfy.

📌 **Minimum = leftmost node** (keep going left). **Maximum = rightmost node.**

---

# 7. ⭐ Balanced trees

## 7.1 ⭐⭐ AVL tree

### 💡 The idea

A BST is only fast if it stays **bushy**. An **AVL tree** (Adelson-Velsky and Landis, 1962 — the first self-balancing BST) enforces bushiness with one rule, checked after every insert and delete:

📌 ⭐ **Balance factor = height(left subtree) − height(right subtree), and it must be in {−1, 0, +1} for EVERY node.**

If an insertion pushes some node's balance factor to ±2, the tree is repaired with a **rotation** — a local rearrangement that reduces height while preserving the BST ordering.

📌 ⭐ **Height of an AVL tree with n nodes = O(log n)** (precisely, ≤ 1.44 log₂(n+2))

### ⭐ The four rotation cases

The case is named by the **path from the unbalanced node down to the newly inserted node**:

| Imbalance | Path | ⭐ Fix |
|---|---|---|
| **LL** | Left child's Left subtree | ⭐ Single **RIGHT** rotation |
| **RR** | Right child's Right subtree | ⭐ Single **LEFT** rotation |
| **LR** | Left child's Right subtree | ⭐ **Left** then **right** (double) |
| **RL** | Right child's Left subtree | ⭐ **Right** then **left** (double) |

🔢 **LL case — insert 10, 20, 30 in decreasing order... actually insert 30, 20, 10:**
```
     30                     20
    /        LL →          /  \
   20      right          10   30
  /        rotation
 10
```
Node 30 has balance factor +2, and the insertion went left-then-left → **LL → single right rotation** ✅

🔢 **LR case — insert 30, 10, 20:**
```
     30              30              20
    /       →       /       →       /  \
   10             20               10   30
     \           /
      20        10
              (left rotate      (then right rotate
               on 10)             on 30)
```

⭐ **Straight-line imbalance (LL, RR) → ONE rotation. Zig-zag imbalance (LR, RL) → TWO rotations.**

📌 **Insertion** needs at most **one** (single or double) rotation. **Deletion** may need up to **O(log n)** rotations, propagating up to the root.

📌 **Minimum nodes in an AVL tree of height h:** N(h) = N(h−1) + N(h−2) + 1, with N(0)=1, N(1)=2.
🔢 N(2)=4, N(3)=7, N(4)=12, N(5)=20, N(6)=33
*(This gives the "sparsest legal AVL tree" — asked as "minimum nodes in an AVL tree of height 4?" → **12**.)*

## 7.2 Other balanced trees (awareness)

| Tree | 💡 Note |
|---|---|
| **Red-black tree** | Balances by colouring nodes red/black with rules; height ≤ 2log₂(n+1). ⭐ **Less strictly balanced than AVL → fewer rotations on insert/delete, slightly slower lookup.** AVL is better for read-heavy loads, red-black for write-heavy. Used in C++ `std::map` and Java `TreeMap` |
| **B-tree** | An m-way balanced search tree; keys **and** data in all nodes. Designed for **disk** — a node is one disk block |
| ⭐ **B+ tree** | Like B-tree, but **all data pointers are in the leaves**, and the **leaves are linked**. ⭐ **The database index structure** — see Week 7 |

---

# 8. ⭐⭐ Binary heaps

## 💡 The idea

Sometimes you do not need full sorting — you only ever need **the smallest (or largest) item**, repeatedly. Examples: a task scheduler always running the highest-priority job; Dijkstra's algorithm always expanding the nearest vertex.

A **heap** is optimised for exactly that:

📌 ⭐ A heap is a **COMPLETE binary tree** satisfying the **heap property**:
- **Min-heap:** every parent ≤ its children → ⭐ **the minimum is at the ROOT**
- **Max-heap:** every parent ≥ its children → the maximum is at the root

```
Min-heap:        10
                /  \
              20    15
             /  \   /
           30   25 18

Array: [10, 20, 15, 30, 25, 18]
```

⚠ ⭐ **A heap is only PARTIALLY ordered.** There is **no ordering between siblings** (20 and 15 above), and **inorder traversal is NOT sorted**. Only the root is guaranteed extremal. This is the difference from a BST, and it is why a heap can be built faster than a sorted structure.

⭐ Because it is **complete**, a heap is stored in a **plain array with no pointers** (§5.4) — extremely cache-friendly.

## 8.1 ⭐ Operations

### Insert — "sift up" / "bubble up"
Place the new element at the **end** of the array (the next free leaf position, preserving completeness), then repeatedly swap it with its parent while it is smaller.

🔢 Insert 5 into the min-heap above:
```
Append:  [10, 20, 15, 30, 25, 18, 5]     5 is a child of 15
5 < 15 → swap:  [10, 20, 5, 30, 25, 18, 15]
5 < 10 → swap:  [5, 20, 10, 30, 25, 18, 15]
```
📌 At most **height** swaps → ⭐ **O(log n)**

### Extract-min — "sift down" / "heapify"
Take the root (the answer), move the **last** element to the root (keeping completeness), then repeatedly swap it with its **smaller child** until the heap property is restored.
📌 ⭐ **O(log n)**

### ⭐⭐ Build-heap from an unsorted array — the O(n) surprise

📌 ⭐ **Building a heap from n arbitrary elements takes O(n), NOT O(n log n).**

💡 **Why — this is worth understanding, because it is a favourite question.**

The bottom-up `build-heap` starts at the **last internal node** and sifts down, working backwards to the root.

Now count the work. In a heap of n nodes:
- About **n/2** nodes are **leaves** — they sift down **0** levels
- About **n/4** nodes are one level up — they sift down at most **1** level
- About **n/8** nodes sift down at most **2** levels
- … and only **1** node (the root) sifts down **log n** levels

Total work ≈ n(0/2 + 1/4 + 2/8 + 3/16 + …) = n × (a convergent series summing to ~1) = ⭐ **O(n)**

⚠ ⭐ **Contrast:** inserting n elements **one at a time** *would* cost O(n log n), because each insertion is O(log n). The bottom-up build is cheaper because **most nodes are near the bottom and barely move.**

### ⭐ Complexity summary

| Operation | ⭐ Complexity |
|---|---|
| Find min (in a min-heap) | ⭐ **O(1)** — it is the root |
| Insert | O(log n) |
| Extract min / delete root | O(log n) |
| Decrease key | O(log n) |
| ⭐ **Build heap from an array** | ⭐ **O(n)** |
| Heap sort | O(n log n) |
| ⭐ **Search for an arbitrary element** | ⭐ **O(n)** — no ordering to guide you |

📌 Number of **leaves** in an n-element heap = ⌈n/2⌉
📌 The **last internal node** is at index ⌊n/2⌋ − 1 (0-based) — where build-heap starts
📌 **Height** of a heap with n nodes = ⌊log₂ n⌋

## 8.2 Applications

⭐ **Priority queues** (the canonical use) · ⭐ **Heap sort** (Week 5) · ⭐ **Dijkstra's and Prim's algorithms** (Week 5) · finding the k-th largest/smallest element · **median maintenance** (a max-heap for the lower half, a min-heap for the upper half) · job scheduling.

---

# 9. ⭐⭐ Graphs

## 💡 The idea

A tree can express hierarchy, but not arbitrary relationships — a tree has no cycles and every node has one parent. Road networks, social networks, web links and dependency graphs all need something more general.

📌 A **graph G = (V, E)** is a set of **vertices** and a set of **edges** connecting them. That is all — no root, no hierarchy, cycles allowed.

```
Undirected:            Directed (digraph):
   A───B                  A──►B
   │  /│                  │   │
   │ / │                  ▼   ▼
   C───D                  C──►D
```

## 9.1 Terminology

| Term | Meaning |
|---|---|
| **Directed vs undirected** | Edges have a direction, or not |
| **Weighted** | Edges carry a cost/distance |
| **Path** | A sequence of vertices connected by edges |
| **Cycle** | A path that returns to its start |
| **Connected** (undirected) | A path exists between every pair |
| **Strongly connected** (directed) | A **directed** path exists both ways between every pair |
| **Degree** | Number of incident edges (directed: **in-degree** and **out-degree**) |
| **Simple graph** | No self-loops, no multiple edges |
| **Complete graph Kₙ** | Every pair connected |
| **Bipartite** | Vertices split into two sets with no edge inside a set |
| ⭐ **Tree** | A connected **acyclic** undirected graph |
| ⭐ **DAG** | Directed Acyclic Graph — models dependencies/prerequisites |

## 9.2 ⭐ Counting formulas

📌 ⭐ **Maximum edges in a simple UNDIRECTED graph = n(n−1)/2**
*Why:* choose any 2 of n vertices = C(n,2).
📌 **Maximum edges in a simple DIRECTED graph = n(n−1)** (each pair can have an edge each way)
📌 ⭐ **Handshaking lemma: sum of all degrees = 2|E|** (each edge contributes 1 to two vertices)
📌 ⭐ **A tree with n vertices has exactly n − 1 edges**
📌 Minimum edges to keep a graph connected = **n − 1**
📌 Minimum edges to guarantee a cycle = **n**

🔢 A complete graph on 6 vertices has 6×5/2 = **15** edges.
🔢 A graph with 5 vertices and degree sum 12 has 12/2 = **6** edges.

## 9.3 ⭐⭐ Representations

### 💡 Adjacency matrix

An n×n grid where `M[i][j] = 1` if there is an edge from i to j.

```
   A B C D
A [0 1 1 0]
B [1 0 1 1]
C [1 1 0 1]
D [0 1 1 0]
```
- ✅ Checking "is there an edge A–D?" is **O(1)** — one array lookup
- ❌ ⭐ **Always uses O(V²) space, even for a graph with 3 edges**
- ❌ Listing a vertex's neighbours takes O(V) (scan the whole row)

**Facts:** symmetric for undirected graphs · diagonal all 0 for a simple graph · the (i,j) entry of **Aᵏ** gives the number of walks of length k from i to j.

### 💡 Adjacency list

An array of lists — for each vertex, a list of its neighbours.
```
A → B, C
B → A, C, D
C → A, B, D
D → B, C
```
- ✅ ⭐ **Space is O(V + E)** — proportional to what actually exists
- ✅ Listing neighbours is O(degree)
- ❌ Checking a specific edge takes O(degree)

| | ⭐ **Adjacency matrix** | ⭐ **Adjacency list** |
|---|---|---|
| ⭐ **Space** | ⭐ **O(V²)** | ⭐ **O(V + E)** |
| Check edge (u,v) | ⭐ **O(1)** | O(degree(u)) |
| List neighbours of u | O(V) | ⭐ **O(degree(u))** |
| Add an edge | O(1) | O(1) |
| ⭐ **Best for** | ⭐ **DENSE** graphs (E ≈ V²) | ⭐ **SPARSE** graphs (E ≪ V²) |

⭐ Real-world graphs (roads, social networks) are almost always **sparse**, which is why adjacency lists dominate in practice.

## 9.4 ⭐⭐ Traversals: BFS and DFS

### 💡 BFS — Breadth-First Search

Explore **level by level**: all vertices at distance 1, then all at distance 2, and so on. Like ripples spreading from a stone dropped in water.

⭐ **Uses a QUEUE** — because a queue preserves the order of discovery, so nearer vertices come out first.

```
start A → visit A
        → visit all of A's neighbours (B, C)
        → visit all of their unvisited neighbours (D)
```

⭐ **Key property: BFS finds the SHORTEST PATH in an UNWEIGHTED graph**, because it reaches every vertex by the fewest possible edges.

### 💡 DFS — Depth-First Search

Go as **deep as possible** along one path, then **backtrack** and try another. Like exploring a maze by always taking the first unexplored corridor and retreating at dead ends.

⭐ **Uses a STACK** (explicitly, or implicitly via recursion) — because a stack returns you to the most recent branch point.

### ⭐ Comparison

| | ⭐ **BFS** | ⭐ **DFS** |
|---|---|---|
| ⭐ **Data structure** | ⭐ **Queue** | ⭐ **Stack** (or recursion) |
| Order | Level by level | Deep first, then backtrack |
| Time (adjacency list) | **O(V + E)** | **O(V + E)** |
| Time (adjacency matrix) | O(V²) | O(V²) |
| Space | O(V) — the queue can hold a whole level | O(V) — recursion depth |
| ⭐ **Shortest path (unweighted)?** | ⭐ **✅ YES** | ❌ No |

⭐ **BFS applications:** shortest path in unweighted graphs · minimum-hop routing · connected components · **testing bipartiteness** (2-colouring) · web crawlers · peer-to-peer search.

⭐ **DFS applications:** ⭐ **cycle detection** · ⭐ **topological sorting** · **strongly connected components** (Kosaraju, Tarjan) · **articulation points and bridges** · path finding · maze solving · puzzle backtracking.

**DFS edge classification** (on directed graphs): tree, ⭐ **back** (points to an ancestor → indicates a **CYCLE**), forward, and cross edges.

## 9.5 ⭐⭐ Topological sort

### 💡 The idea

Given tasks with prerequisites, in what order can you do them?

```
   Foundation ──► Walls ──► Roof
        │                    ▲
        └────► Plumbing ─────┘
```
A **topological sort** is a linear ordering of vertices such that for every directed edge u→v, **u comes before v**.

📌 ⭐ **A topological sort exists ONLY for a DAG (Directed Acyclic Graph).**

💡 **Why:** if there is a cycle A→B→C→A, then A must come before B, B before C, and C before A — impossible. ⭐ Therefore **"topological sort fails" ⟺ "the graph has a cycle"**, and this is a standard way to detect cycles in a directed graph.

**Two algorithms, both O(V + E):**
- ⭐ **Kahn's algorithm:** repeatedly output any vertex with **in-degree 0** and remove it (which decrements its neighbours' in-degrees). Uses a queue.
- ⭐ **DFS-based:** run DFS and push each vertex onto a stack **when it finishes** (post-order); then pop the stack.

⚠ ⭐ **The topological order is generally NOT unique** — above, `Foundation, Walls, Plumbing, Roof` and `Foundation, Plumbing, Walls, Roof` are both valid.

**Real uses:** build systems (make), course prerequisites, spreadsheet formula evaluation, package dependency resolution, instruction scheduling.

## 9.6 Cycle detection

- **Undirected graph:** run DFS; if you find an edge to an already-visited vertex that is **not the parent**, there is a cycle. (Or use union–find.)
- ⭐ **Directed graph:** run DFS; a **back edge** — an edge to a vertex currently **on the recursion stack** — indicates a cycle.
⚠ In a directed graph, merely reaching a visited vertex is **not** enough (it could be a cross edge to a finished branch). It must still be *on the stack*.

---

# 10. ⭐⭐ Hashing

## 💡 The idea

Arrays give O(1) access **by index**. But what if your key is a **name** or a **string**, not an index?

⭐ **Hashing** applies a **hash function** that converts a key into an array index:
```
h("Rahul") = 7   →  store the record at slot 7
```
Now lookup is a single computation plus one array access — ⭐ **O(1) on average**, independent of how many items are stored. That is dramatically better than a tree's O(log n).

```
     Key         h(key)      Table
   "Rahul"  ───►   7    ───► [7] = Rahul's record
   "Priya"  ───►   3    ───► [3] = Priya's record
```

📌 ⭐ **Load factor α = n / m** (n = elements stored, m = table slots)

**Good hash function properties:** deterministic · fast to compute · **uniform** (spreads keys evenly over all slots).

**Common hash functions:**
- **Division method:** `h(k) = k mod m`. ⭐ Choose m **prime** and avoid powers of 2 (a power of 2 uses only the low-order bits, which are often patterned).
- **Multiplication method**, **mid-square**, **folding**.

## 10.1 ⭐⭐ Collisions

### 💡 The problem

Two different keys can hash to the same slot — `h("Rahul") = h("Amit") = 7`. This is a **collision**, and it is unavoidable: you are mapping a huge key space into a small table (pigeonhole principle).

The whole art of hashing is what to do next.

### ⭐ Method 1 — Separate chaining

Each slot holds a **linked list** of all keys that hashed there.

```
[0] → NULL
[1] → "Amit" → "Zara" → NULL
[2] → NULL
[3] → "Priya" → NULL
```

- ✅ Simple; deletion is easy
- ✅ ⭐ The load factor **can exceed 1** (lists grow indefinitely)
- Average search = **O(1 + α)**
- ❌ ⭐ Worst case **O(n)** if every key collides (all in one list)
- ❌ Extra memory for pointers; poor cache behaviour

### ⭐ Method 2 — Open addressing

Store everything **inside the table**. On a collision, **probe** for another free slot by a fixed rule.

| Scheme | ⭐ Probe sequence | ⭐ Problem |
|---|---|---|
| ⭐ **Linear probing** | `(h(k) + i) mod m` — try the next slot, then the next | ⭐ **PRIMARY clustering** |
| ⭐ **Quadratic probing** | `(h(k) + c₁i + c₂i²) mod m` | ⭐ **SECONDARY clustering** (no primary) |
| ⭐ **Double hashing** | `(h₁(k) + i·h₂(k)) mod m` | ⭐ **Best** — avoids both |

### 💡 Understanding clustering — why linear probing degrades

⭐ **Primary clustering (linear probing):** occupied slots form long **contiguous runs**. Any new key hashing anywhere into a run must probe past the whole run. Worse, runs **grow and merge**, so the problem accelerates.
```
[.][X][X][X][X][.][.]     a cluster of 4
                          any key hashing to slots 1–4 must probe to slot 5,
                          extending the cluster to 5
```

⭐ **Secondary clustering (quadratic probing):** keys hashing to the **same initial slot** follow the **same probe sequence**, so they still pile up — but keys hashing to *different* slots no longer interfere. Much milder than primary clustering.

⭐ **Double hashing:** the probe *step size* depends on the key, so even two keys with the same initial slot take different routes. This is why it is the best of the three.

### 🔢 Worked example — linear probing

Table size 10, `h(k) = k mod 10`. Insert 12, 22, 32, 42:
```
12 → slot 2                        [.][.][12][.][.][.][.][.][.][.]
22 → slot 2 taken → slot 3         [.][.][12][22][.][.][.][.][.][.]
32 → slots 2,3 taken → slot 4      [.][.][12][22][32][.][.][.][.][.]
42 → slots 2,3,4 taken → slot 5    [.][.][12][22][32][42][.][.][.][.]
```
⭐ A cluster of 4 has formed — searching for 42 now needs 4 probes. **Primary clustering** in action.

### ⚠ Two open-addressing gotchas

⚠ ⭐ **In open addressing, α ≤ 1 always** — you cannot store more items than slots.
⚠ ⭐ **Deletion requires TOMBSTONES.** If you simply blank a slot, probe chains break:
```
Insert 12, 22 → [.][.][12][22]...
Delete 12     → [.][.][ ][22]...
Search 22     → probes slot 2, finds it EMPTY, concludes 22 is absent ❌
```
The fix is to mark the slot "deleted" (a tombstone) rather than empty, so probing continues past it.

### ⭐ Rehashing
When α exceeds a threshold (typically **0.7**), allocate a **bigger table** (usually double, rounded to the next prime) and **reinsert every key** (their hashes change with m). Expensive, but amortised O(1).

---

# 11. ⭐⭐ Complexity summary — the table to memorise

| Structure | Access | Search | Insert | Delete |
|---|---|---|---|---|
| Array (unsorted) | **O(1)** | O(n) | O(1)* | O(n) |
| Array (sorted) | **O(1)** | **O(log n)** | O(n) | O(n) |
| Stack / Queue | O(n) | O(n) | **O(1)** | **O(1)** |
| Singly linked list | O(n) | O(n) | O(1) at head | O(1) at head |
| Doubly linked list | O(n) | O(n) | O(1) | ⭐ **O(1) given the node** |
| **BST (average)** | O(log n) | O(log n) | O(log n) | O(log n) |
| ⭐ **BST (worst — skewed)** | ⭐ **O(n)** | ⭐ **O(n)** | ⭐ **O(n)** | ⭐ **O(n)** |
| **AVL / Red-black** | O(log n) | O(log n) | O(log n) | O(log n) |
| **Binary heap** | ⭐ **O(1)** for min/max | O(n) | O(log n) | O(log n) |
| ⭐ **Hash table (average)** | — | ⭐ **O(1)** | **O(1)** | **O(1)** |
| Hash table (worst) | — | O(n) | O(n) | O(n) |
| B / B+ tree | O(log n) | O(log n) | O(log n) | O(log n) |

\* amortised, appending at the end

---

# 12. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| Array access is O(1) because | Address is **calculated**, not searched |
| Row-major A[i][j] | Base + (i×ncols + j) × size |
| Stack order / Queue order | LIFO / FIFO |
| Recursion uses | **Stack** |
| BFS / DFS use | **Queue / Stack** |
| Postfix of A+B*C | **ABC*+** |
| Postfix of (A+B)*C | AB+C* |
| Postfix evaluation: `a b −` | Second popped is the **left** operand → a − b |
| Circular queue full | **(rear+1)%n == front** |
| Circular queue capacity | **n − 1** |
| Priority queue is | **Not** FIFO |
| Delete a given node: SLL / DLL | O(n) / **O(1)** |
| Reverse a list needs | prev, curr, next — save `next` first |
| Cycle detection in a list | **Floyd's tortoise and hare**, O(1) space |
| Max nodes at level i | 2ⁱ |
| Max nodes, height h (root=0) | **2^(h+1) − 1** |
| NULL pointers in an n-node binary tree | **n + 1** |
| Edges in an n-node tree | n − 1 |
| Full binary tree: leaves | **internal + 1** |
| Distinct binary tree shapes with n nodes | **Catalan C(n)**; C(3) = 5 |
| Heap array children (0-based) | **2i+1, 2i+2** |
| Heap array children (1-based) | 2i, 2i+1 |
| Sorted traversal of a BST | **Inorder** |
| Unique tree from | Inorder + (pre **or** post)order |
| Preorder + postorder | ⭐ **Not unique** (general binary tree) |
| BST worst-case search | **O(n)** — skewed, from sorted insertion |
| BST delete with 2 children | Replace with the **inorder successor** |
| AVL balance factor | −1, 0, +1 |
| AVL height | O(log n) |
| LL / RR imbalance | Single rotation |
| LR / RL imbalance | Double rotation |
| Min nodes in an AVL of height 4 | 12 |
| Heap is | A **complete** binary tree, partially ordered |
| Heap inorder traversal | **Not** sorted |
| **Build-heap** | ⭐ **O(n)** |
| Heap insert / extract | O(log n) |
| Heap search | O(n) |
| Max edges, simple undirected | **n(n−1)/2** |
| Max edges, simple directed | n(n−1) |
| Sum of degrees | 2\|E\| |
| Adjacency matrix / list space | **O(V²) / O(V+E)** |
| Matrix better for / list better for | Dense / sparse |
| BFS finds shortest path when | Graph is **unweighted** |
| Topological sort requires | **DAG** |
| Topological order is | **Not unique** |
| Back edge in DFS indicates | A **cycle** |
| Linear probing problem | **Primary** clustering |
| Quadratic probing problem | **Secondary** clustering |
| Best probing scheme | **Double hashing** |
| Load factor | n/m |
| Chaining allows α | > 1 |
| Open addressing deletion needs | **Tombstones** |

---

# 13. ⚠ Common traps

1. ⭐ **Build-heap is O(n)**, not O(n log n) — because most nodes are near the leaves.
2. ⭐ **Preorder + postorder does NOT determine a general binary tree** — inorder is the essential traversal.
3. ⭐ **Height convention** — root at 0 (edges) vs root at 1 (nodes) shifts every formula.
4. ⭐ **Heap array indexing** — 0-based (2i+1, 2i+2) vs 1-based (2i, 2i+1).
5. ⭐ **A heap's inorder traversal is not sorted** — only the root is extremal.
6. ⭐ **Circular queue capacity is n − 1** with the one-empty-slot method.
7. ⭐ **BST worst case is O(n)** — from inserting sorted data.
8. ⭐ **Primary clustering = linear probing; secondary = quadratic.**
9. ⭐ **In postfix evaluation, the second value popped is the LEFT operand.**
10. **Adjacency matrix uses O(V²) space regardless of edge count.**
11. **Topological sort order is not unique.**
12. **Deletion in open addressing needs tombstones**, not blanking.
13. **A priority queue is not a FIFO queue.**
14. **BFS only gives shortest paths in UNWEIGHTED graphs** — use Dijkstra when weighted (Week 5).

---

# 14. Practice

- GATE: [`Paper2_S05_Data_Structures_and_Programming/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — **370 questions** (238 on data structures)
- State-PSC level: [`Paper2_S05_.../`](../02_State_PSC_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — **578 questions**
- Test: [`Week_04_Test.md`](../04_Mock_Tests/Week_04_Test.md)

**Priority order if short on time:** the complexity summary table (§11) → tree formulas & traversals → tree reconstruction → BST properties & worst case → heaps (especially build-heap = O(n)) → stacks/postfix → graph representations & BFS/DFS → hashing collision resolution → AVL rotations.
