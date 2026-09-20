# Week 4 Question Bank — Data Structures

**Syllabus §5 (part)** · 200 questions · Practice set · +1 / −0.33 marking

> Covers arrays, stacks, queues, linked lists, trees, BST, AVL/balanced trees, heaps, graphs and hashing, plus a Paper-I block. Answer key and fully worked solutions follow the questions.

---

## Part A — Arrays & Address Calculation, Sparse Matrices

**Q1.** Array access by index is O(1) mainly because
(A) elements are stored in sorted order  (B) a binary search is performed  (C) the address is computed arithmetically  (D) a hash function maps the index

**Q2.** An `int` array (4 bytes/element) has base address 1000 and 0-based indexing. The address of `A[6]` is
(A) 1006  (B) 1024  (C) 1020  (D) 1026

**Q3.** For `int A[10][20]`, base 1000, 4 bytes, row-major, 0-based, the address of `A[3][5]` is
(A) 1240  (B) 1280  (C) 1300  (D) 1260

**Q4.** For the same `int A[10][20]`, base 1000, 4 bytes, 0-based, but **column-major**, the address of `A[3][5]` is
(A) 1212  (B) 1260  (C) 1112  (D) 1204

**Q5.** Inserting an element at an arbitrary interior position of an array of `n` elements takes
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n²)

**Q6.** The triplet representation of a sparse matrix stores
(A) only the non-zero values without positions  (B) (row, column, value) triplets  (C) all elements row-wise  (D) a row-pointer array

**Q7.** A 1000×1000 matrix has only 50 non-zero entries. Its triplet representation stores about how many value-bearing triplets?
(A) 1,000,000  (B) 2,050  (C) 50  (D) 3,000

**Q8.** Searching an **unsorted** array of `n` elements takes
(A) O(n)  (B) O(log n)  (C) O(1)  (D) O(n log n)

**Q9.** In **row-major** order a 2-D array is stored
(A) column by column  (B) diagonally  (C) randomly  (D) row by row

**Q10.** A `char` array (1 byte/element) has base 2000, 0-based. The address of `A[15]` is
(A) 2015  (B) 2030  (C) 2060  (D) 2016

**Q11.** A 1-based array `A[1..n]` has base 500 and element size 2 bytes. The address of `A[10]` is
(A) 520  (B) 516  (C) 518  (D) 500

---

## Part B — Stacks (LIFO, applications, expression conversion & evaluation)

**Q12.** A stack follows the discipline
(A) FIFO  (B) LIFO  (C) priority order  (D) random access

**Q13.** The postfix form of `A + B * C` is
(A) AB+C*  (B) ABC+*  (C) ABC*+  (D) A+BC*

**Q14.** The postfix form of `(A + B) * C` is
(A) AB+C*  (B) ABC*+  (C) ABC+*  (D) AB*C+

**Q15.** The prefix (Polish) form of `A + B * C` is
(A) *+ABC  (B) ABC*+  (C) +*ABC  (D) +A*BC

**Q16.** The value of the postfix expression `5 6 2 + * 12 4 / −` is
(A) 34  (B) 37  (C) 40  (D) 43

**Q17.** The value of the postfix expression `2 3 4 * +` is
(A) 9  (B) 20  (C) 14  (D) 24

**Q18.** While evaluating the postfix fragment `a b −`, the **left** operand of the subtraction is
(A) the first value popped  (B) the second value popped  (C) either value  (D) the top of stack before popping

**Q19.** Function calls and recursion are implemented by the compiler using a
(A) queue  (B) heap  (C) graph  (D) stack

**Q20.** Pushing onto a completely full stack causes
(A) overflow  (B) underflow  (C) collision  (D) rehash

**Q21.** Popping from an empty stack causes
(A) overflow  (B) segmentation fault  (C) underflow  (D) nothing

**Q22.** Which of the following is **NOT** a typical stack application?
(A) recursion handling  (B) balanced-parentheses checking  (C) undo/redo  (D) BFS traversal

**Q23.** The bracket string `{[(])}` is
(A) balanced  (B) not balanced  (C) balanced only if reversed  (D) undefined

**Q24.** In the stack-based infix-to-postfix algorithm, when a `)` is read you
(A) push it on the stack  (B) discard it immediately  (C) pop to output until `(` is found, then discard both  (D) pop the entire stack

**Q25.** Each of `push`, `pop` and `peek` on a stack takes
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q26.** The prefix form of `(A + B) * C` is
(A) *+ABC  (B) +AB*C  (C) AB+C*  (D) +A*BC

**Q27.** The postfix form of `A + B * C − D / E` is
(A) ABC*+DE/-  (B) AB+C*DE/-  (C) ABC+*DE-/  (D) ABCDE*+/-

**Q28.** The postfix form of `A * B + C * D` is
(A) ABCD**+  (B) AB*C+D*  (C) ABCD+**  (D) AB*CD*+

**Q29.** The value of the postfix expression `8 2 / 3 −` is
(A) 1  (B) 4  (C) 7  (D) −1

**Q30.** When two stacks share a single array by growing from opposite ends,
(A) each stack gets exactly n/2 slots  (B) overflow occurs only when the two tops meet  (C) it is impossible  (D) it needs two arrays

**Q31.** Excessively deep recursion typically causes
(A) heap overflow  (B) a memory leak  (C) stack overflow  (D) queue overflow

**Q32.** Which notation requires **no** parentheses and **no** precedence rules to evaluate?
(A) infix  (B) postfix  (C) infix with brackets  (D) none of these

---

## Part C — Queues (FIFO, circular, deque, priority queue)

**Q33.** A queue follows the discipline
(A) FIFO  (B) LIFO  (C) priority order  (D) random access

**Q34.** In a circular queue on an array of size `n` (keeping one slot empty), the "full" condition is
(A) `rear == front`  (B) `rear == n − 1`  (C) `front == 0`  (D) `(rear + 1) % n == front`

**Q35.** In the same circular queue, the "empty" condition is
(A) `front == rear`  (B) `(rear + 1) % n == front`  (C) `rear == n − 1`  (D) `front == 0`

**Q36.** A circular queue on an array of size `n` (one-slot-empty method) holds at most
(A) n elements  (B) n − 1 elements  (C) n + 1 elements  (D) n/2 elements

**Q37.** A circular queue on an array of size 5 holds at most
(A) 6  (B) 3  (C) 4  (D) 5

**Q38.** In a circular queue, `rear` advances according to
(A) `rear + 1`  (B) `(rear + 1) % n`  (C) `rear − 1`  (D) `rear × 2`

**Q39.** If a circular queue keeps a **separate element counter**, its usable capacity is
(A) n  (B) n − 1  (C) n + 1  (D) n/2

**Q40.** A deque (double-ended queue) allows
(A) insertion at both ends only  (B) deletion at the front only  (C) insertion and deletion at both ends  (D) insertion at the rear only

**Q41.** In a priority queue, the element removed first is
(A) the first inserted  (B) the highest- (or lowest-) priority element  (C) the last inserted  (D) a random element

**Q42.** A priority queue is best implemented using
(A) a stack  (B) a plain unsorted array  (C) a hash table  (D) a binary heap

**Q43.** Is a priority queue a FIFO structure?
(A) yes, always  (B) no  (C) only when empty  (D) only with equal priorities

**Q44.** Which graph traversal uses a queue?
(A) DFS  (B) inorder  (C) BFS / level order  (D) preorder

**Q45.** Which is a classic queue application?
(A) print / job spooling  (B) function-call management  (C) undo operation  (D) expression evaluation

**Q46.** A plain (non-circular) array queue wastes space because
(A) `rear` cannot advance  (B) the queue is too small  (C) elements overwrite each other  (D) dequeued front slots cannot be reused

**Q47.** Enqueue and dequeue on a well-implemented queue each take
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

---

## Part D — Linked Lists

**Q48.** Given only a pointer to a node, which operation is O(1) in a doubly linked list but O(n) in a singly linked list?
(A) searching for a value  (B) traversing the list  (C) deleting that node  (D) finding the length

**Q49.** Accessing the k-th element of a linked list is
(A) O(1)  (B) O(n)  (C) O(log n)  (D) O(n log n)

**Q50.** In a singly linked list the last node's `next` pointer is
(A) points to head  (B) points to itself  (C) undefined  (D) NULL

**Q51.** In a circular singly linked list the last node's `next` pointer
(A) points to head  (B) is NULL  (C) points to the previous node  (D) is undefined

**Q52.** A doubly linked list node contains
(A) data, next  (B) prev, data, next  (C) data only  (D) two data fields

**Q53.** When reversing a singly linked list iteratively, what must be saved **before** overwriting `curr->next`?
(A) prev  (B) head  (C) next  (D) tail

**Q54.** Cycle detection in a linked list using O(1) extra space uses
(A) a hash set of nodes  (B) Floyd's tortoise-and-hare  (C) recursion  (D) sorting the list

**Q55.** In Floyd's cycle-detection algorithm, the two pointers move
(A) 1 and 1 steps  (B) 2 and 3 steps  (C) 1 and 2 steps  (D) 1 and 3 steps

**Q56.** Insertion or deletion at the **head** of a singly linked list is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q57.** Deletion at the **tail** of a singly linked list with no tail pointer is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n²)

**Q58.** Which generally has better cache performance?
(A) array  (B) linked list  (C) they are equal  (D) depends on the compiler

**Q59.** Compared with an array, a linked list needs
(A) no extra memory  (B) one extra pointer per node  (C) double the data  (D) a hash table

**Q60.** Merging two sorted linked lists of sizes m and n takes
(A) O(mn)  (B) O(m + n)  (C) O(m log n)  (D) O((m+n) log(m+n))

**Q61.** Binary search can be applied efficiently to
(A) a singly linked list  (B) a circular list  (C) a sorted array  (D) a doubly linked list

**Q62.** Finding the middle node of a linked list in a single pass uses
(A) length then divide  (B) slow/fast two pointers  (C) recursion only  (D) a stack

**Q63.** To delete a node given only a pointer to it in a **singly** linked list, the cost is
(A) O(1) using `prev`  (B) O(n) to find the predecessor  (C) impossible  (D) O(log n)

---

## Part E — Trees (terminology, types, formulas, array representation)

**Q64.** The maximum number of nodes in a binary tree of height `h` (root at height 0) is
(A) 2ʰ  (B) 2ʰ − 1  (C) 2ʰ⁺¹ − 1  (D) 2h + 1

**Q65.** With the root at height 0, the maximum number of nodes at height 3 is
(A) 7  (B) 8  (C) 15  (D) 16

**Q66.** The maximum number of nodes at level `i` of a binary tree is
(A) 2ⁱ  (B) 2ⁱ⁻¹  (C) i²  (D) 2i

**Q67.** A binary tree with `n` nodes has how many NULL child pointers?
(A) n − 1  (B) n  (C) n + 1  (D) 2n

**Q68.** A binary tree with 5 nodes has how many NULL child pointers?
(A) 4  (B) 5  (C) 10  (D) 6

**Q69.** In a full binary tree with 10 internal nodes, the number of leaves is
(A) 9  (B) 10  (C) 11  (D) 20

**Q70.** A tree (or binary tree) with `n` nodes has how many edges?
(A) n  (B) n − 1  (C) n + 1  (D) 2n

**Q71.** The number of distinct binary-tree **shapes** with 3 nodes is
(A) 3  (B) 5  (C) 6  (D) 8

**Q72.** The Catalan number C(4) equals
(A) 5  (B) 14  (C) 42  (D) 9

**Q73.** The number of distinct BSTs on 4 distinct keys is
(A) 4  (B) 24  (C) 14  (D) 8

**Q74.** In a full (strictly binary) tree every node has
(A) exactly 1 child  (B) 0 or 2 children  (C) at most 1 child  (D) any number of children

**Q75.** In a complete binary tree the last level is filled
(A) right to left  (B) randomly  (C) center outward  (D) left to right

**Q76.** A skewed (degenerate) binary tree behaves like
(A) a linked list  (B) a heap  (C) a complete tree  (D) an array

**Q77.** In 0-based array representation, the children of node `i` are at indices
(A) 2i and 2i+1  (B) 2i+1 and 2i+2  (C) i/2 and i/2+1  (D) i+1 and i+2

**Q78.** In 0-based array representation, the parent of node `i` is at index
(A) i/2  (B) ⌊(i−1)/2⌋  (C) 2i+1  (D) i−1

**Q79.** In 1-based array representation, the children of node `i` are at indices
(A) 2i and 2i+1  (B) 2i+1 and 2i+2  (C) i/2  (D) i−1

**Q80.** The maximum possible height of a binary tree with `n` nodes (root at height 0) is
(A) log n  (B) n − 1  (C) n  (D) 2n

**Q81.** A perfect binary tree of height 3 (root at height 0) has how many leaf nodes?
(A) 4  (B) 7  (C) 8  (D) 15

**Q82.** The degree of a node in a tree is
(A) its number of children  (B) its number of ancestors  (C) its level  (D) its height

**Q83.** A threaded binary tree replaces NULL pointers with
(A) child pointers  (B) threads to the inorder predecessor/successor  (C) parent pointers  (D) sibling pointers

---

## Part F — Traversals & Reconstruction

**Q84.** Preorder traversal visits nodes in the order
(A) Left, Root, Right  (B) Root, Left, Right  (C) Left, Right, Root  (D) level by level

**Q85.** Inorder traversal visits nodes in the order
(A) Root, Left, Right  (B) Left, Root, Right  (C) Left, Right, Root  (D) Right, Root, Left

**Q86.** Postorder traversal visits nodes in the order
(A) Left, Right, Root  (B) Root, Left, Right  (C) Left, Root, Right  (D) Right, Left, Root

For Q87–Q90, use the tree:
```
            1
          /   \
         2     3
        / \   /
       4   5 6
```

**Q87.** The preorder traversal is
(A) 1 2 4 5 3 6  (B) 4 2 5 1 6 3  (C) 4 5 2 6 3 1  (D) 1 2 3 4 5 6

**Q88.** The inorder traversal is
(A) 1 2 4 5 3 6  (B) 4 2 5 1 6 3  (C) 4 5 2 6 3 1  (D) 1 2 3 4 5 6

**Q89.** The postorder traversal is
(A) 1 2 4 5 3 6  (B) 4 2 5 1 6 3  (C) 4 5 2 6 3 1  (D) 1 2 3 4 5 6

**Q90.** The level-order traversal is
(A) 1 2 4 5 3 6  (B) 4 2 5 1 6 3  (C) 4 5 2 6 3 1  (D) 1 2 3 4 5 6

**Q91.** Which pair of traversals uniquely determines a binary tree?
(A) preorder + postorder  (B) inorder + preorder  (C) preorder + level order  (D) any single traversal

**Q92.** For a **general** binary tree, preorder + postorder together
(A) are always unique  (B) are unique only for a BST  (C) do NOT uniquely determine the tree  (D) are unique always

**Q93.** Which traversal is essential for reconstruction because it separates left-subtree nodes from right-subtree nodes?
(A) preorder  (B) inorder  (C) postorder  (D) level order

**Q94.** Which single traversal of a BST yields keys in sorted order?
(A) preorder  (B) postorder  (C) inorder  (D) level order

**Q95.** The three depth-first traversals run in
(A) O(n log n) time, O(1) space  (B) O(n) time, O(h) space  (C) O(n²) time  (D) O(log n) time

**Q96.** Level-order traversal is implemented with
(A) a stack  (B) a queue  (C) a heap  (D) recursion only

**Q97.** Given Preorder = `A B D E C F` and Inorder = `D B E A C F`, the root of the tree is
(A) A  (B) B  (C) D  (D) F

**Q98.** Preorder + postorder DO suffice to reconstruct which special tree?
(A) a skewed tree  (B) a BST  (C) a full binary tree (every node has 0 or 2 children)  (D) a complete tree

**Q99.** The last node visited in a postorder traversal is always
(A) the leftmost leaf  (B) the root  (C) the rightmost leaf  (D) the middle node

---

## Part G — Binary Search Trees

**Q100.** The BST ordering property states that for every node
(A) left > node > right  (B) left keys < node < right keys  (C) all keys are equal  (D) parent ≤ children

**Q101.** The worst-case time to search a BST of `n` nodes is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q102.** The BST worst case arises when keys are inserted
(A) in balanced fashion  (B) at random  (C) reverse then random  (D) in sorted order (producing a skewed tree)

**Q103.** The average-case time to search a BST is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q104.** To delete a node with two children in a BST, replace its key with
(A) the left child  (B) the root  (C) its inorder successor (or predecessor)  (D) any leaf

**Q105.** The inorder successor of a node with a right subtree is
(A) the largest key in the left subtree  (B) the leftmost node of the right subtree  (C) the parent  (D) the root

**Q106.** The minimum key of a BST is at
(A) the root  (B) the leftmost node  (C) the rightmost node  (D) any leaf

**Q107.** Deleting a **leaf** node from a BST requires you to
(A) replace it with its successor  (B) replace it with the root  (C) it is impossible  (D) simply remove it

**Q108.** Inserting 10, 20, 30, 40, 50 (in that order) into an empty BST produces a tree that is
(A) right-skewed, like a linked list  (B) perfectly balanced  (C) left-skewed  (D) complete

**Q109.** To test whether a binary tree is a valid BST you can check that
(A) its preorder is sorted  (B) its inorder traversal is sorted  (C) its level order is sorted  (D) it has the right node count

**Q110.** The number of distinct BSTs on 3 distinct keys is
(A) 3  (B) 5  (C) 6  (D) 8

**Q111.** At each step of a search in a balanced BST you discard
(A) one node  (B) the right subtree always  (C) about half the remaining tree  (D) nothing

---

## Part H — AVL & Balanced Trees

**Q112.** In an AVL tree the balance factor of every node must lie in
(A) {0}  (B) {−1, 0, +1}  (C) {−2, …, +2}  (D) {0, 1}

**Q113.** The height of an AVL tree with `n` nodes is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q114.** An LL imbalance is fixed by a
(A) single left rotation  (B) left-then-right rotation  (C) single right rotation  (D) right-then-left rotation

**Q115.** An RR imbalance is fixed by a
(A) single left rotation  (B) single right rotation  (C) left-then-right rotation  (D) right-then-left rotation

**Q116.** An LR imbalance is fixed by a
(A) single right rotation  (B) single left rotation  (C) left-then-right rotation  (D) right-then-left rotation

**Q117.** An RL imbalance is fixed by a
(A) single left rotation  (B) right-then-left rotation  (C) left-then-right rotation  (D) single right rotation

**Q118.** A single insertion into an AVL tree needs at most
(A) O(log n) rotations  (B) exactly two rotations  (C) at most one (single or double) rotation  (D) n rotations

**Q119.** A deletion from an AVL tree may need up to
(A) exactly 1 rotation  (B) exactly 2 rotations  (C) O(log n) rotations  (D) O(n) rotations

**Q120.** The minimum number of nodes in an AVL tree of height 4 is
(A) 7  (B) 12  (C) 15  (D) 20

**Q121.** The minimum number of nodes in an AVL tree of height 3 is
(A) 7  (B) 12  (C) 8  (D) 4

**Q122.** Compared with an AVL tree, a red-black tree is
(A) more strictly balanced  (B) unbalanced  (C) identical to AVL  (D) less strictly balanced, so it uses fewer rotations

**Q123.** Which tree keeps all data in the leaves, with the leaves linked, and is the standard database index structure?
(A) B-tree  (B) B+ tree  (C) AVL tree  (D) red-black tree

**Q124.** A B-tree is primarily designed for
(A) the cache  (B) disk storage (a node = one disk block)  (C) CPU registers  (D) the call stack

**Q125.** Inserting 30, 20, 10 (in that order) into an AVL tree triggers
(A) an RR case, single left rotation  (B) an LR case, double rotation  (C) an LL case, single right rotation  (D) an RL case, double rotation

---

## Part I — Binary Heaps

**Q126.** A binary heap is
(A) a full BST  (B) a skewed tree  (C) a sorted array  (D) a complete binary tree satisfying the heap property

**Q127.** In a min-heap the minimum element is at
(A) a leaf  (B) the root  (C) the rightmost node  (D) the leftmost leaf

**Q128.** Building a heap from an unsorted array of `n` elements (bottom-up build-heap) takes
(A) O(n)  (B) O(n log n)  (C) O(log n)  (D) O(n²)

**Q129.** Inserting one element into a heap of `n` elements takes
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q130.** Extract-min from a heap takes
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q131.** Finding the minimum in a min-heap takes
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q132.** Searching for an arbitrary element in a heap takes
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q133.** The inorder traversal of a heap is
(A) sorted ascending  (B) not sorted  (C) sorted descending  (D) the same as level order

**Q134.** Inserting `n` elements one at a time into an initially empty heap costs
(A) O(n)  (B) O(n log n)  (C) O(log n)  (D) O(n²)

**Q135.** A heap insertion places the new element
(A) at the root  (B) at a random leaf  (C) at the end (next free leaf), then sifts it up  (D) at its sorted position

**Q136.** The number of leaves in an `n`-element heap is
(A) ⌊n/2⌋  (B) ⌈n/2⌉  (C) n − 1  (D) log n

**Q137.** A heap is stored as
(A) linked nodes  (B) a plain array with no pointers  (C) a hash table  (D) a BST

**Q138.** The canonical application of a heap is
(A) recursion  (B) a priority queue  (C) BFS  (D) hashing

**Q139.** Inserting 5 into the min-heap array `[10, 20, 15, 30, 25, 18]` makes the new root
(A) 10  (B) 5  (C) 15  (D) 20

---

## Part J — Graphs

**Q140.** The space required by an adjacency **matrix** is
(A) O(V + E)  (B) O(V²)  (C) O(E)  (D) O(V)

**Q141.** The space required by an adjacency **list** is
(A) O(V²)  (B) O(V + E)  (C) O(E)  (D) O(V)

**Q142.** The space for an adjacency matrix and an adjacency list are, respectively,
(A) O(V+E) and O(V²)  (B) O(V²) and O(V+E)  (C) O(V²) and O(E)  (D) O(E) and O(V)

**Q143.** The maximum number of edges in a simple **undirected** graph on `n` vertices is
(A) n²  (B) n(n−1)/2  (C) n(n−1)  (D) n − 1

**Q144.** The maximum number of edges in a simple **directed** graph on `n` vertices is
(A) n(n−1)/2  (B) n²  (C) n(n−1)  (D) 2n

**Q145.** A complete graph on 6 vertices has
(A) 12 edges  (B) 15 edges  (C) 30 edges  (D) 36 edges

**Q146.** The handshaking lemma states that the sum of all vertex degrees equals
(A) |E|  (B) 2|E|  (C) |V|  (D) |V| − 1

**Q147.** A graph with 5 vertices whose degree sum is 12 has how many edges?
(A) 5  (B) 6  (C) 12  (D) 24

**Q148.** A tree with `n` vertices has exactly
(A) n edges  (B) n − 1 edges  (C) n + 1 edges  (D) 2n edges

**Q149.** Checking whether an edge (u, v) exists is O(1) in
(A) an adjacency list  (B) an adjacency matrix  (C) both  (D) neither

**Q150.** Listing all neighbours of a vertex in O(degree) is possible with
(A) an adjacency matrix  (B) an adjacency list  (C) both, in O(1)  (D) neither

**Q151.** BFS uses which auxiliary structure?
(A) a stack  (B) a queue  (C) a heap  (D) a plain array

**Q152.** DFS uses which auxiliary structure?
(A) a queue  (B) a stack (or recursion)  (C) a heap  (D) a priority queue

**Q153.** BFS finds shortest paths in
(A) weighted graphs  (B) any graph  (C) unweighted graphs  (D) DAGs only

**Q154.** On an adjacency list, BFS and DFS each run in
(A) O(V²)  (B) O(V + E)  (C) O(V log V)  (D) O(E log V)

**Q155.** A topological sort is possible only for
(A) any graph  (B) a DAG  (C) an undirected connected graph  (D) a complete graph

**Q156.** The topological ordering of a DAG is
(A) always unique  (B) not unique in general  (C) unique for every DAG  (D) never existent

**Q157.** In DFS on a directed graph, a cycle is indicated by a
(A) forward edge  (B) back edge (to a vertex on the recursion stack)  (C) cross edge  (D) tree edge

**Q158.** Kahn's algorithm repeatedly removes a vertex with
(A) out-degree 0  (B) in-degree 0  (C) maximum degree  (D) minimum weight

**Q159.** A DAG is a
(A) directed acyclic graph  (B) disjoint acyclic graph  (C) any directed graph  (D) an undirected tree

**Q160.** For an adjacency matrix A, the (i, j) entry of Aᵏ gives
(A) the shortest path length  (B) the number of walks of length k from i to j  (C) the degree of i  (D) the number of cycles

**Q161.** Testing whether a graph is bipartite (2-colouring) is a typical application of
(A) BFS  (B) hashing  (C) a heap  (D) topological sort

---

## Part K — Hashing

**Q162.** The load factor α of a hash table is
(A) m/n  (B) n/m  (C) n × m  (D) n − m

**Q163.** In the division method `h(k) = k mod m`, the value of `m` should ideally be
(A) a power of 2  (B) prime  (C) even  (D) 1

**Q164.** Separate chaining stores colliding keys in
(A) the next free slot  (B) a linked list per slot  (C) a second table  (D) tombstones

**Q165.** The load factor can exceed 1 in
(A) linear probing  (B) separate chaining  (C) quadratic probing  (D) double hashing

**Q166.** Linear probing suffers from
(A) primary clustering  (B) secondary clustering  (C) no clustering  (D) chaining

**Q167.** Quadratic probing suffers from
(A) primary clustering  (B) secondary clustering  (C) no clustering  (D) tombstones

**Q168.** Which open-addressing scheme avoids both primary and secondary clustering?
(A) linear probing  (B) quadratic probing  (C) double hashing  (D) separate chaining

**Q169.** The probe sequence for linear probing is
(A) (h(k) + i) mod m  (B) (h(k) + i²) mod m  (C) (h₁ + i·h₂) mod m  (D) h(k)

**Q170.** The probe sequence for double hashing is
(A) (h(k) + i) mod m  (B) (h(k) + i²) mod m  (C) i mod m  (D) (h₁(k) + i·h₂(k)) mod m

**Q171.** Deletion in an open-addressing hash table requires
(A) blanking the slot  (B) tombstones  (C) rehashing on every delete  (D) chaining

**Q172.** In open addressing the load factor α is
(A) able to exceed 1  (B) always ≤ 1  (C) always exactly 1  (D) always 0

**Q173.** With table size 10, `h(k) = k mod 10`, and linear probing, inserting 12, 22, 32, 42 places 42 in slot
(A) 2  (B) 3  (C) 4  (D) 5

**Q174.** Rehashing is typically triggered when the load factor exceeds about
(A) 0.1  (B) 0.5  (C) 0.7  (D) 1.0

**Q175.** The average search cost in separate chaining is
(A) O(1)  (B) O(1 + α)  (C) O(n) always  (D) O(log n)

**Q176.** Collisions in hashing are unavoidable because of
(A) bad hash functions only  (B) the pigeonhole principle  (C) a small load factor  (D) prime table sizes

**Q177.** The worst-case search time in a hash table (all keys collide) is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

---

## Part L — Complexity Lookup (mixed)

**Q178.** Access by index in an unsorted array is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q179.** Search in a **sorted** array is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q180.** Average-case search/insert/delete in a hash table is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q181.** Search/insert/delete in an AVL tree is
(A) O(1)  (B) O(log n)  (C) O(n)  (D) O(n log n)

**Q182.** Heap sort runs in
(A) O(n)  (B) O(log n)  (C) O(n log n)  (D) O(n²)

**Q183.** The height of a heap with `n` nodes is
(A) n − 1  (B) ⌊log₂ n⌋  (C) √n  (D) n

**Q184.** Recursion is implemented using
(A) a queue  (B) a stack  (C) a heap  (D) a graph

**Q185.** Which structure gives O(1) access by index but O(n) insertion in the middle?
(A) an array  (B) a linked list  (C) a BST  (D) a heap

---

## Part M — Paper-I (English, Reasoning, GK)

**Q186.** Choose the word most nearly **opposite** in meaning to **SCARCE**.
(A) Rare  (B) Limited  (C) Abundant  (D) Insufficient

**Q187.** Fill in the blank with the correct article: *"He is ___ honest officer."*
(A) a  (B) an  (C) the  (D) no article

**Q188.** In a code, `TEACHER` is written as `VGCEJGT`. Then `STUDENT` is written as
(A) UVWFGPV  (B) UVWEGPV  (C) TUVFGPV  (D) UWVFGPV

**Q189.** A can finish a job in 12 days and B in 18 days. Working together they finish it in
(A) 6 days  (B) 7.2 days  (C) 7.5 days  (D) 15 days

**Q190.** How many districts does Tripura currently have?
(A) 4  (B) 6  (C) 8  (D) 10

**Q191.** Choose the synonym of **DILIGENT**.
(A) lazy  (B) hardworking  (C) careless  (D) slow

**Q192.** Find the next term: 2, 6, 12, 20, 30, ?
(A) 40  (B) 36  (C) 44  (D) 42

**Q193.** Find the odd one out: 3, 5, 9, 11.
(A) 3  (B) 5  (C) 9  (D) 11

**Q194.** Find the next term: 5, 10, 20, 40, ?
(A) 60  (B) 80  (C) 100  (D) 50

**Q195.** The plural of "criterion" is
(A) criterions  (B) criteria  (C) criterion  (D) criterias

**Q196.** The capital of Tripura is
(A) Aizawl  (B) Agartala  (C) Imphal  (D) Shillong

**Q197.** 15% of 200 equals
(A) 30  (B) 15  (C) 20  (D) 45

**Q198.** Choose the correctly spelled word.
(A) Accommodate  (B) Acommodate  (C) Accomodate  (D) Acomodate

**Q199.** If A : B = 2 : 3 and B : C = 4 : 5, then A : C =
(A) 2 : 5  (B) 8 : 5  (C) 8 : 15  (D) 3 : 5

**Q200.** A man walks 3 km north, then 4 km east. His straight-line distance from the start is
(A) 7 km  (B) 5 km  (C) 1 km  (D) 25 km

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|
| 1 | C | 2 | B | 3 | D | 4 | A | 5 | C |
| 6 | B | 7 | C | 8 | A | 9 | D | 10 | A |
| 11 | C | 12 | B | 13 | C | 14 | A | 15 | D |
| 16 | B | 17 | C | 18 | B | 19 | D | 20 | A |
| 21 | C | 22 | D | 23 | B | 24 | C | 25 | A |
| 26 | A | 27 | A | 28 | D | 29 | A | 30 | B |
| 31 | C | 32 | B | 33 | A | 34 | D | 35 | A |
| 36 | B | 37 | C | 38 | B | 39 | A | 40 | C |
| 41 | B | 42 | D | 43 | B | 44 | C | 45 | A |
| 46 | D | 47 | A | 48 | C | 49 | B | 50 | D |
| 51 | A | 52 | B | 53 | C | 54 | B | 55 | C |
| 56 | A | 57 | C | 58 | A | 59 | B | 60 | B |
| 61 | C | 62 | B | 63 | B | 64 | C | 65 | C |
| 66 | A | 67 | C | 68 | D | 69 | C | 70 | B |
| 71 | B | 72 | B | 73 | C | 74 | B | 75 | D |
| 76 | A | 77 | B | 78 | B | 79 | A | 80 | B |
| 81 | C | 82 | A | 83 | B | 84 | B | 85 | B |
| 86 | A | 87 | A | 88 | B | 89 | C | 90 | D |
| 91 | B | 92 | C | 93 | B | 94 | C | 95 | B |
| 96 | B | 97 | A | 98 | C | 99 | B | 100 | B |
| 101 | C | 102 | D | 103 | B | 104 | C | 105 | B |
| 106 | B | 107 | D | 108 | A | 109 | B | 110 | B |
| 111 | C | 112 | B | 113 | B | 114 | C | 115 | A |
| 116 | C | 117 | B | 118 | C | 119 | C | 120 | B |
| 121 | A | 122 | D | 123 | B | 124 | B | 125 | C |
| 126 | D | 127 | B | 128 | A | 129 | B | 130 | B |
| 131 | A | 132 | C | 133 | B | 134 | B | 135 | C |
| 136 | B | 137 | B | 138 | B | 139 | B | 140 | B |
| 141 | B | 142 | B | 143 | B | 144 | C | 145 | B |
| 146 | B | 147 | B | 148 | B | 149 | B | 150 | B |
| 151 | B | 152 | B | 153 | C | 154 | B | 155 | B |
| 156 | B | 157 | B | 158 | B | 159 | A | 160 | B |
| 161 | A | 162 | B | 163 | B | 164 | B | 165 | B |
| 166 | A | 167 | B | 168 | C | 169 | A | 170 | D |
| 171 | B | 172 | B | 173 | D | 174 | C | 175 | B |
| 176 | B | 177 | C | 178 | A | 179 | B | 180 | A |
| 181 | B | 182 | C | 183 | B | 184 | B | 185 | A |
| 186 | C | 187 | B | 188 | A | 189 | B | 190 | C |
| 191 | B | 192 | D | 193 | C | 194 | B | 195 | B |
| 196 | B | 197 | A | 198 | A | 199 | C | 200 | B |

---

# 📝 Detailed Solutions

**Q1. (C)** The CPU does not search for `A[i]`; it computes `Base + (i − L)×size` with one multiply and one add — constant time regardless of array size.

**Q2. (B)** `1000 + (6 − 0)×4 = 1000 + 24 = 1024`.

**Q3. (D)** Row-major: `Base + (i×N_cols + j)×size = 1000 + (3×20 + 5)×4 = 1000 + 65×4 = 1000 + 260 = 1260`.

**Q4. (A)** Column-major: `Base + (j×N_rows + i)×size = 1000 + (5×10 + 3)×4 = 1000 + 53×4 = 1000 + 212 = 1212`.

**Q5. (C)** Every element after the insertion point must shift right, so the cost is proportional to `n` — O(n).

**Q6. (B)** A sparse matrix is stored as a list of (row, column, value) triplets, keeping only the non-zeros together with their positions.

**Q7. (C)** Only the non-zero entries are stored, so the triplet list holds about 50 value triplets rather than 1,000,000 cells.

**Q8. (A)** With no ordering, you may have to inspect every element — O(n).

**Q9. (D)** Row-major stores the array one full row at a time; consecutive elements of a row are adjacent in memory.

**Q10. (A)** `2000 + (15 − 0)×1 = 2015` (1-byte elements).

**Q11. (C)** 1-based: `Base + (i − 1)×size = 500 + (10 − 1)×2 = 500 + 18 = 518`.

**Q12. (B)** A stack adds and removes only at the top — Last In, First Out.

**Q13. (C)** `*` binds tighter, so `A + (B*C)`. Postfix: `BC*` then `A BC* +` = `ABC*+`.

**Q14. (A)** Grouping is forced: `(A+B)*C` → `AB+` then `AB+ C *` = `AB+C*`.

**Q15. (D)** Prefix places the operator before its operands: `A + (B*C)` → `+ A *BC` = `+A*BC`.

**Q16. (B)** `6 2 +` = 8; `5 8 *` = 40; `12 4 /` = 3; `40 3 −` = **37**.

**Q17. (C)** `3 4 *` = 12; `2 12 +` = **14**.

**Q18. (B)** For `a b −` you pop `b` first (right operand) then `a`; the **second** popped value is the left operand, giving `a − b`.

**Q19. (D)** Each call pushes an activation record and each return pops it — a stack; that is why deep recursion overflows the stack.

**Q20. (A)** Pushing onto a full stack is overflow (popping an empty stack is underflow).

**Q21. (C)** Popping an empty stack is underflow.

**Q22. (D)** Recursion, parentheses checking and undo/redo all use stacks; BFS uses a **queue**, so it is not a stack application.

**Q23. (B)** `]` tries to match but the top is `(`, a mismatch, so `{[(])}` is **not** balanced.

**Q24. (C)** On `)` you pop operators to the output until the matching `(` appears, then discard both parentheses.

**Q25. (A)** All three touch only the top and take O(1).

**Q26. (A)** `(A+B)*C`: `+AB` for the sum, then `* +AB C` = `*+ABC`.

**Q27. (A)** `(A + (B*C)) − (D/E)` → `ABC*+` and `DE/`, joined by `−` = `ABC*+DE/-`.

**Q28. (D)** `(A*B) + (C*D)` → `AB*` and `CD*`, joined by `+` = `AB*CD*+`.

**Q29. (A)** `8 2 /` = 4; `4 3 −` = **1**.

**Q30. (B)** Growing two stacks from opposite ends means overflow occurs only when the two tops meet — better space utilisation than splitting in half.

**Q31. (C)** Too many un-popped activation records exhaust the call stack — stack overflow.

**Q32. (B)** Postfix (and prefix) need neither parentheses nor precedence rules; a single left-to-right scan with one stack evaluates it.

**Q33. (A)** A queue removes from the front and adds at the rear — First In, First Out.

**Q34. (D)** Keeping one slot empty, the table is full when `(rear + 1) % n == front`.

**Q35. (A)** With the one-empty-slot method, `front == rear` unambiguously means empty.

**Q36. (B)** One slot is sacrificed to distinguish full from empty, so capacity is `n − 1`.

**Q37. (C)** `n − 1 = 5 − 1 = 4`.

**Q38. (B)** Wrapping around the array, `rear = (rear + 1) % n`.

**Q39. (A)** A separate counter distinguishes full from empty without a sacrificed slot, so all `n` slots are usable.

**Q40. (C)** A deque permits insertion and deletion at **both** ends.

**Q41. (B)** A priority queue serves the highest- (or lowest-) priority element first, regardless of arrival order.

**Q42. (D)** A binary heap gives O(log n) insert and extract with O(1) access to the extremal element — ideal for a priority queue.

**Q43. (B)** No — priority order overrides arrival order, so it is not FIFO.

**Q44. (C)** BFS / level-order traversal uses a queue to preserve discovery order.

**Q45. (A)** Print/job spooling is a producer–consumer buffer, a classic queue use.

**Q46. (D)** As the front advances, the vacated leading slots cannot be reused in a plain array queue, so it reports full with free space — the reason circular queues exist.

**Q47. (A)** Both operate on fixed ends — O(1).

**Q48. (C)** A DLL node has a `prev` pointer, so it can be spliced out in O(1); an SLL must walk from the head to find the predecessor — O(n).

**Q49. (B)** Without random access you must walk from the head — O(n).

**Q50. (D)** In an SLL the last node's `next` is NULL.

**Q51. (A)** In a circular SLL the last node points back to the head (no NULL).

**Q52. (B)** A doubly linked node stores `prev`, `data`, and `next`.

**Q53. (C)** You must save `next = curr->next` before rewriting `curr->next`, or the rest of the list is lost.

**Q54. (B)** Floyd's tortoise-and-hare detects a cycle in O(n) time and O(1) space.

**Q55. (C)** The slow pointer moves 1 step and the fast pointer 2 steps per iteration; inside a cycle the gap closes by 1 each step, so they meet.

**Q56. (A)** Head insertion/deletion just rewires the head pointer — O(1).

**Q57. (C)** Without a tail pointer you must traverse to the last node — O(n).

**Q58. (A)** Array elements are contiguous, giving spatial locality; linked-list nodes are scattered and cause a cache miss per node.

**Q59. (B)** Each node needs one extra pointer (two in a DLL) beyond the data.

**Q60. (B)** One pass through both lists taking the smaller head each time — O(m + n).

**Q61. (C)** Binary search needs O(1) random access, available in a sorted array but not a linked list.

**Q62. (B)** A slow (1×) and fast (2×) pointer: when the fast reaches the end, the slow is at the middle — one pass.

**Q63. (B)** With only a pointer to the node, an SLL must walk from the head to locate the predecessor — O(n).

**Q64. (C)** Summing 2⁰ + 2¹ + … + 2ʰ = 2ʰ⁺¹ − 1.

**Q65. (C)** `2³⁺¹ − 1 = 16 − 1 = 15`.

**Q66. (A)** Level 0 has 1 node and each level can at most double, so level `i` has at most 2ⁱ.

**Q67. (C)** There are 2n pointer slots; `n − 1` point to real nodes, so NULLs = `2n − (n − 1) = n + 1`.

**Q68. (D)** `n + 1 = 5 + 1 = 6` (10 slots, 4 used, 6 NULL).

**Q69. (C)** In a full binary tree leaves = internal + 1 = `10 + 1 = 11`.

**Q70. (B)** Every non-root node contributes exactly one edge upward — `n − 1` edges.

**Q71. (B)** The Catalan number C(3) = 6!/(3!·4!) = 720/144 = **5** distinct shapes.

**Q72. (B)** C(4) = 8!/(4!·5!) = 40320/2880 = **14**.

**Q73. (C)** The number of BSTs on n distinct keys is the Catalan number; C(4) = **14**.

**Q74. (B)** A full (strictly binary) tree has every node with 0 or 2 children — never exactly one.

**Q75. (D)** A complete tree fills the last level from left to right.

**Q76. (A)** A skewed tree has one child per node, degenerating into a linked list.

**Q77. (B)** 0-based: children of `i` are `2i+1` and `2i+2`.

**Q78. (B)** 0-based parent is `⌊(i−1)/2⌋`.

**Q79. (A)** 1-based: children of `i` are `2i` and `2i+1`.

**Q80. (B)** A fully skewed tree of `n` nodes has height `n − 1`.

**Q81. (C)** A perfect tree of height h has 2ʰ leaves; `2³ = 8` (total nodes 15, leaves (15+1)/2 = 8).

**Q82. (A)** A node's degree is its number of children.

**Q83. (B)** Threads replace NULLs with pointers to the inorder predecessor/successor, enabling stackless inorder traversal.

**Q84. (B)** Preorder = Root, Left, Right (NLR).

**Q85. (B)** Inorder = Left, Root, Right (LNR).

**Q86. (A)** Postorder = Left, Right, Root (LRN).

**Q87. (A)** Root first, hug the left: 1, 2, 4, 5, 3, 6.

**Q88. (B)** Project nodes down and read left to right: 4, 2, 5, 1, 6, 3.

**Q89. (C)** Write each node when last left: 4, 5, 2, 6, 3, 1.

**Q90. (D)** Level by level: 1, 2, 3, 4, 5, 6.

**Q91. (B)** Inorder + preorder (or inorder + postorder) uniquely determines a binary tree.

**Q92. (C)** For general binary trees preorder + postorder cannot distinguish a lone left child from a lone right child, so they are not unique.

**Q93. (B)** Only inorder reveals which nodes fall to the left vs right of the root, so it is essential for reconstruction.

**Q94. (C)** Inorder of a BST visits keys in non-decreasing sorted order.

**Q95. (B)** Depth-first traversals visit each node once (O(n)) using stack space proportional to height (O(h)).

**Q96. (B)** Level-order uses a queue.

**Q97. (A)** The first element of preorder is the root — **A**.

**Q98. (C)** In a full binary tree (0 or 2 children) a lone child cannot occur, so preorder + postorder suffice.

**Q99. (B)** Postorder visits the root last.

**Q100. (B)** For every node, all left-subtree keys are smaller and all right-subtree keys are larger.

**Q101. (C)** A skewed BST degenerates to a list, making search O(n).

**Q102. (D)** Inserting already-sorted keys makes every insertion go one way, producing a skewed tree.

**Q103. (B)** A reasonably balanced BST gives O(log n) search on average.

**Q104. (C)** Replace the key with its inorder successor (or predecessor), then delete that node, which has at most one child.

**Q105. (B)** The inorder successor is the smallest key in the right subtree — its leftmost node.

**Q106. (B)** Keep going left to reach the minimum.

**Q107. (D)** A leaf is simply removed (deletion case 1).

**Q108. (A)** Each new key is larger, so every insertion goes right, producing a right-skewed list-like tree.

**Q109. (B)** A binary tree is a valid BST iff its inorder traversal is strictly increasing.

**Q110. (B)** C(3) = **5** distinct BSTs.

**Q111. (C)** One comparison discards an entire subtree — about half the remaining nodes — giving O(log n).

**Q112. (B)** Every node's balance factor (height_left − height_right) must be −1, 0, or +1.

**Q113. (B)** AVL balancing keeps height O(log n) (≤ ~1.44 log₂(n+2)).

**Q114. (C)** Left-child's-left insertion (LL) is a straight line fixed by a single right rotation.

**Q115. (A)** RR (right-child's-right) is fixed by a single left rotation.

**Q116. (C)** LR (left-child's-right) is a zig-zag needing a left then a right rotation.

**Q117. (B)** RL (right-child's-left) needs a right then a left rotation.

**Q118. (C)** An insertion needs at most one single or double rotation to rebalance.

**Q119. (C)** A deletion may cascade rotations up to the root — O(log n) of them.

**Q120. (B)** N(h) = N(h−1)+N(h−2)+1 with N(0)=1, N(1)=2 → N(2)=4, N(3)=7, N(4)=**12**.

**Q121. (A)** From the same recurrence, N(3) = 4 + 2 + 1 = **7**.

**Q122. (D)** Red-black trees are less strictly balanced than AVL, so they need fewer rotations (better for write-heavy loads).

**Q123. (B)** A B+ tree keeps all data pointers in linked leaves — the standard database index structure.

**Q124. (B)** A B-tree node is sized to one disk block, designed for disk storage.

**Q125. (C)** 30→20→10 goes left-then-left at node 30 (balance factor +2): an LL case fixed by a single right rotation.

**Q126. (D)** A heap is a complete binary tree obeying the heap (parent-child ordering) property.

**Q127. (B)** In a min-heap every parent ≤ its children, so the minimum sits at the root.

**Q128. (A)** Bottom-up build-heap is O(n): most nodes are near the leaves and sift down a short distance (the work series converges to ~1×n).

**Q129. (B)** Insert at the end and sift up at most the height — O(log n).

**Q130. (B)** Move the last element to the root and sift down at most the height — O(log n).

**Q131. (A)** The minimum is the root — O(1).

**Q132. (C)** A heap is only partially ordered, so an arbitrary search scans everything — O(n).

**Q133. (B)** A heap has no left/right ordering, so its inorder traversal is not sorted; only the root is extremal.

**Q134. (B)** n insertions at O(log n) each cost O(n log n) — more than the O(n) bottom-up build.

**Q135. (C)** The new element goes to the next free leaf (end of the array), then sifts up.

**Q136. (B)** An n-element heap has ⌈n/2⌉ leaves.

**Q137. (B)** Because it is complete, a heap is stored in a plain array with no pointers.

**Q138. (B)** The priority queue is the canonical heap application.

**Q139. (B)** Append 5 (child of 15): `[10,20,15,30,25,18,5]`; 5<15 swap → `[10,20,5,30,25,18,15]`; 5<10 swap → `[5,20,10,30,25,18,15]`. New root = **5**.

**Q140. (B)** An adjacency matrix has V² entries — O(V²) regardless of edge count.

**Q141. (B)** An adjacency list stores each vertex plus its edges — O(V + E).

**Q142. (B)** Matrix O(V²), list O(V + E).

**Q143. (B)** Choosing any 2 of n vertices = C(n,2) = n(n−1)/2.

**Q144. (C)** Each ordered pair can have an edge — n(n−1).

**Q145. (B)** 6×5/2 = **15** edges.

**Q146. (B)** Each edge adds 1 to two vertices' degrees, so the degree sum is 2|E|.

**Q147. (B)** |E| = degree sum / 2 = 12/2 = **6**.

**Q148. (B)** A tree on n vertices has exactly n − 1 edges.

**Q149. (B)** An adjacency matrix answers "is there an edge (u,v)?" in O(1) by direct lookup.

**Q150. (B)** An adjacency list lists a vertex's neighbours in O(degree).

**Q151. (B)** BFS uses a queue to preserve discovery order.

**Q152. (B)** DFS uses a stack (explicit or via recursion).

**Q153. (C)** BFS reaches each vertex by fewest edges, giving shortest paths in unweighted graphs.

**Q154. (B)** Both visit every vertex and edge once on an adjacency list — O(V + E).

**Q155. (B)** A linear ordering respecting all edges exists only if there is no cycle — a DAG.

**Q156. (B)** Multiple valid orderings usually exist, so the topological order is not unique.

**Q157. (B)** A back edge to a vertex still on the recursion stack indicates a cycle.

**Q158. (B)** Kahn's algorithm repeatedly outputs a vertex with in-degree 0 and decrements its neighbours.

**Q159. (A)** DAG = Directed Acyclic Graph.

**Q160. (B)** The (i,j) entry of Aᵏ counts the walks of length k from i to j.

**Q161. (A)** Bipartiteness testing is a 2-colouring done with BFS (or DFS).

**Q162. (B)** Load factor α = n/m (elements over slots).

**Q163. (B)** A prime m avoids the low-bit patterns that powers of 2 expose, spreading keys evenly.

**Q164. (B)** Separate chaining keeps a linked list of colliding keys at each slot.

**Q165. (B)** In chaining the lists can grow indefinitely, so α can exceed 1.

**Q166. (A)** Linear probing forms long contiguous runs — primary clustering.

**Q167. (B)** Quadratic probing removes primary clustering but keys with the same initial slot still collide — secondary clustering.

**Q168. (C)** Double hashing makes the step size key-dependent, avoiding both clustering types.

**Q169. (A)** Linear probing: `(h(k) + i) mod m`.

**Q170. (D)** Double hashing: `(h₁(k) + i·h₂(k)) mod m`.

**Q171. (B)** Blanking a slot breaks probe chains; a tombstone marks it deleted so probing continues past it.

**Q172. (B)** Open addressing stores items inside the table, so α ≤ 1 always.

**Q173. (D)** 12→slot 2; 22→3; 32→4; 42 finds 2,3,4 taken → slot **5**.

**Q174. (C)** Rehashing typically triggers around a load factor of 0.7.

**Q175. (B)** In chaining, average search is O(1 + α).

**Q176. (B)** Mapping a huge key space into a small table forces collisions — the pigeonhole principle.

**Q177. (C)** If every key collides, search degrades to O(n).

**Q178. (A)** Indexed access is a direct address calculation — O(1).

**Q179. (B)** Binary search on a sorted array is O(log n).

**Q180. (A)** With a good hash function, hash-table operations average O(1).

**Q181. (B)** AVL height is O(log n), so all operations are O(log n).

**Q182. (C)** Heap sort is O(n log n) (n extract-min operations of O(log n) each).

**Q183. (B)** A heap with n nodes has height ⌊log₂ n⌋.

**Q184. (B)** Nested calls return in LIFO order — recursion uses a stack.

**Q185. (A)** An array gives O(1) indexed access but O(n) middle insertion (shifting).

**Q186. (C)** *Scarce* means insufficient/in short supply; its opposite is **abundant**. Rare, limited and insufficient are synonyms.

**Q187. (B)** *Honest* has a silent `h`, so it begins with a vowel sound — the article is **an**.

**Q188. (A)** Each letter shifts +2: S→U, T→V, U→W, D→F, E→G, N→P, T→V = **UVWFGPV**.

**Q189. (B)** Combined rate = 1/12 + 1/18 = 3/36 + 2/36 = 5/36; time = 36/5 = **7.2 days**.

**Q190. (C)** Tripura currently has **8 districts** (reorganised from 4 in January 2012).

**Q191. (B)** *Diligent* means hardworking/industrious.

**Q192. (D)** Terms are n(n+1): 1·2, 2·3, 3·4, 4·5, 5·6, then 6·7 = **42** (differences 4, 6, 8, 10, 12).

**Q193. (C)** 3, 5, 11 are prime; **9** (= 3×3) is not, so it is the odd one out.

**Q194. (B)** Each term doubles: 5, 10, 20, 40, then 40×2 = **80**.

**Q195. (B)** The plural of *criterion* is **criteria**.

**Q196. (B)** The capital of Tripura is **Agartala**.

**Q197. (A)** 15% of 200 = 0.15 × 200 = **30**.

**Q198. (A)** The correct spelling is **Accommodate** (double c, double m).

**Q199. (C)** Scale B to 12: A:B = 8:12 and B:C = 12:15, so A:C = **8:15**.

**Q200. (B)** Right triangle with legs 3 and 4: √(3² + 4²) = √25 = **5 km**.

---

## Score

| | |
|---|---|
| Part A–L (Data Structures, Q1–Q185) | ___ / 185 |
| Part M (Paper-I, Q186–Q200) | ___ / 15 |
| Raw total | ___ / 200 |
| After −0.33 penalty per wrong answer | ___ |

**Weak-area pointers:** revisit the relevant section of `05_Notes/Week_04_Data_Structures.md` for any part you miss, then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/` (370 questions) and the State-PSC set (578 questions). Priority topics: tree formulas & traversals, BST worst case, build-heap = O(n), preorder+postorder non-uniqueness, circular-queue capacity, and hashing collision resolution.
