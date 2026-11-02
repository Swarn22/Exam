# 03 · Programming (C, C++, Java) & Data Structures — Precise Notes
> **TPSC ATO (IT) Paper-II §5** · ~14 marks (estimate) · Syllabus: *"Data Structures and Programming — arrays, stacks, queues, linked lists, trees, binary search trees, binary heaps, graphs; programming in C, C++, Java; recursion"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson GATE guide (C), GATE Applied Course, Ace Academy 2020, Made Easy 2011 & handwritten sets. Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/03_C_and_Data_Structures/` — open them for diagrams (PDF-viewer page numbers). Short names: Pearson = 1, Sanchit = 2, ME-Toppers = 3, Ace-2012 = 4, ME-2011 = 5, ME-CS = 6, GAC = 7, ME-HW = 8, Ace-2020 = 9, Shared = 10.
> Cross-refs: complexity analysis, sorting (incl. heapsort), searching, hashing, MST/shortest paths → `04_Algorithms.md` · B/B+ trees → DBMS notes.

## Which notes are worth your time
| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 1.CandDS.pdf | Pearson (GATE guide, Unit 3) | Typed 2-column text | 76 | 3.5 | The only real **C** coverage (operators, storage classes, pointers, structs, malloc) plus PYQs with keys · garbled text; treats UB code as having answers; says 2-byte int and "#define allocates memory" |
| 2.DS_Sanchit_Sir_Notes.pdf | Sanchit Jain (Knowledge Gate) | Typed slides | 131 | 4 | **Backbone**: clean flow from arrays to BFS/DFS, ~200 GATE PYQs tagged by year · no C language, thin on expression trees/deque; a few code bugs and 2 wrong keys |
| 3.DS_made_Easy_Class_Toppers_Latest_Notes.pdf | Made Easy class topper | Handwritten scan (119 MB) | 201 | 2 | Pointer-arithmetic drills, tail-recursion remarks · messy, crossed-out, some wrong C claims |
| 4.Ace_Academy_Data_Structure_Class_Notes.pdf | Ace Academy (2012) | Handwritten scan | 97 | 2 | Clear basic array/BST/AVL intros · thin, few PYQs, slips in examples |
| 5.data_structure_new.pdf | Made Easy (2011) | Handwritten scan | 144 | 3 | **Best generic AVL rotation diagrams**, DLL pointer steps · grainy, no PYQ tags |
| 6.Data_Structure-CS.pdf | Made Easy (2011) | Faint handwritten scan | 352 | 2.5 | Long worked examples (stack-life, ToH call count, AVL delete) · steps unexplained; last ~100 pp are TOC/compiler |
| 7.DATA_STRUCTURE-GATEAppliedcourse_NOTES.pdf | GATE Applied Course | Neat colour handwriting with index | 182 | 4.5 | **Best-organised scan**: special matrices, expression trees, build-heap O(n), AVL height recurrence, chapter-wise solved GATE PYQs · no C, no graphs |
| 8.DataStructures_Hand_Written_Notes_Made_Easy.pdf | Made Easy (phone photos) | Watermarked photos | 136 | 3 | Struct/pointer output tracing, static vs dynamic scoping, Fibonacci call counts · glare; one GATE code mis-copied |
| 9.DS_Notes.pdf | Ace Academy (2020) | CamScanner handwritten | 156 | 4 | Syllabus map + **GATE weightage**, traversal-rebuild drills, BST/AVL deletion, band/Toeplitz formulas · some bounds not tight |
| 10.DS_Shared_notes.pdf | Unknown | Handwritten scan | 146 | 1.5 | Linked-list merge sort · hard to read, several wrong complexities |

**If you open only one PDF besides these notes:** open **GAC (file 7)** for DS diagrams and solved GATE PYQs. For C, read **Pearson (file 1) pp. 3–45**, but where it disagrees with these notes, trust these notes.

## Topic map
| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | C basics: types, operators, UB, storage classes | ⭐⭐⭐ | "Output of this code?", precedence, static variable |
| 2 | Pointers, arrays, strings, structs, malloc | ⭐⭐⭐ | Pointer-arithmetic output, declaration meaning, sizeof(struct) |
| 3 | Arrays as DS (addressing, special matrices) | ⭐⭐ | Row/column-major numerical; triangular/tridiagonal storage |
| 4 | Stacks | ⭐⭐⭐ | Infix→postfix/prefix, evaluate postfix, valid pop sequence |
| 5 | Queues | ⭐⭐ | Circular-queue full/empty, queue via stacks, deque/PQ |
| 6 | Linked lists | ⭐⭐ | "What does this function do?", O() of an operation |
| 7 | Recursion | ⭐⭐⭐ | Trace return value, count calls, tail recursion |
| 8 | Binary trees | ⭐⭐⭐ | n₀ = n₂ + 1, max/min nodes, rebuild from traversals, Catalan |
| 9 | BST | ⭐⭐⭐ | Insert order → traversal/height, delete, successor |
| 10 | AVL | ⭐⭐ | Rotation result, min nodes for height h |
| 11 | Binary heaps | ⭐⭐⭐ | Valid heap array, insert/delete result, build-heap O(n) |
| 12 | Graphs: representation, BFS/DFS | ⭐⭐ | Matrix vs list, valid BFS/DFS order, O(V+E) |
| 13 | C++, Java & OOP | ⭐⭐⭐ (PSC favourite) | Definitions: virtual, abstract, final/finally, JVM |

Trend: across GATE DS questions from 1987–2020, Ace-2020 counts trees (BT/BST/AVL/heap) ≈ 65 %, stack & queue ≈ 15 %, and arrays, linked lists, graphs and hashing ≈ 5 % each **[Src: Ace-2020 p.3]**.

---

## 1. C Fundamentals
### 1.1 Types, sizes, conversions
| Type | GCC 32/64-bit | Turbo C 16-bit |
|---|---|---|
| char / short / int | 1 / 2 / **4** | 1 / 2 / **2** |
| long / long long | 4 or 8 / 8 | 4 / — |
| float / double | 4 / 8 | 4 / 8 |
| pointer | 4 / 8 | 2 |
- 📌 The standard guarantees only 1 = char ≤ short ≤ int ≤ long ≤ long long. Signed char is −128…127; unsigned 0…255; whether plain char is signed is implementation-defined. ⚠ Pearson assumes 2-byte int; use what the question states, otherwise 4.
- Promotion: char/short → int → unsigned → long → float → double. ⭐ **Signed meets unsigned → the signed value becomes unsigned**: `-1 < 1u` is false; `sizeof(int) > -1` is false.
- Integer division truncates toward 0: `-7/2 = -3`, `-7 % 2 = -1` (the sign follows the dividend). `(float)a/b` is real division; `(float)(a/b)` is not.
- `010` = 8 (octal), `0x10` = 16, `'A'` = 65. **`sizeof('a')` = sizeof(int) in C** (1 in C++). `float f = 0.1; f == 0.1` → false.

### 1.2 Operator precedence (high → low)
| Level | Operators | Assoc. |
|---|---|---|
| 1 | `()` `[]` `->` `.` postfix `++` `--` | L→R |
| 2 | unary `!` `~` prefix `++` `--` `+` `-` `*` `&` `(type)` `sizeof` | **R→L** |
| 3–5 | `* / %` → `+ -` → `<< >>` | L→R |
| 6–7 | `< <= > >=` → `== !=` | L→R |
| 8–10 | `&` → `^` → `\|` | L→R |
| 11–12 | `&&` → `\|\|` | L→R |
| 13–14 | `?:` → `= += -=` … | **R→L** |
| 15 | `,` | L→R |
- ⚠ `x & 1 == 0` means `x & (1 == 0)` = 0. `a < b < c` means `(a<b) < c`. `x = 1, 2;` gives x = 1, but `x = (1, 2)` gives 2.
- ⚠ `*p++` = `*(p++)`. ME-Toppers p.80 says "`*` and `++` are at the same level"; that is true only for **prefix** `++`.
- `&&` and `||` short-circuit and are sequence points: in `if (0 && ++j)`, j stays the same. Right-shifting a negative value is implementation-defined; shifting by ≥ the bit width is UB. `x & (x−1)` == 0 ⇔ x is a power of 2.

### 1.3 ⭐ Undefined / unspecified behaviour (the #1 tracing trap)
- **UB** (no correct output exists): `i = i++;` `i = i++ + ++i;` `a[i] = i++;` `printf("%d %d", i, i++);` signed overflow; dereferencing NULL or a dangling pointer; out-of-bounds access; modifying a string literal; reading an uninitialised auto; double `free`.
- **Unspecified**: the order in which function arguments are evaluated. It is **not** "right to left".
- ⚠ Pearson p.5 "evaluates" `printf("%d%d%d%d%d", i++, ++i, ++i, i++, ++i)` right to left as 14 14 13 11 11. Correct: **undefined behaviour**. Its `x = i+++++i…` does not even compile: maximal munch reads `i++ ++ + i`, and `i++` is not an lvalue.
- 🎯 **How it's asked:** "Output of `i = i++ + ++i`?" → pick "undefined/compiler dependent" (NET/PSC). GATE avoids such code.

### 1.4 Control flow, functions, preprocessor
- `if (x = 5)` is always true. `for(…);` with a stray semicolon has an empty body. do-while runs **at least once** (exit-controlled).
- `switch`: integral expression only (no float, no string). Case labels must be **distinct** integer constants, so `case 10:` plus `case 8+2:` is a compile error. Missing `break` falls through; `default` may appear anywhere.
- `printf` returns the number of characters printed: `printf("%d", printf("hello"))` → `hello5`. `scanf` returns the number of items assigned.
- ⚠ Pearson p.14 says empty parentheses in a declaration mean "no parameters". In C before C23, `int f();` means *unspecified* parameters; `int f(void)` means none. In C++ both mean none. "Default return type int" holds only in C89.
- `#define` is **text substitution before compilation**: no type check, **no memory**. ⚠ Pearson p.4 says memory is allocated. 🔢 `#define SQ(x) x*x` → `SQ(2+3)` = 2+3*2+3 = **11**. The safe form is `((x)*(x))`, but `SQ(i++)` is still UB.
- 🎯 GATE-2015: j = 2*3/4 + 2.0/5 + 8/5 = 2.4, so int j = 2; `k -= --j` gives k = −1; the switch falls through and printf runs **10** times. GATE-2012: switch on 'A' with no breaks → prints "Choice A", then "Choice B No choice".

### 1.5 Storage classes, scope, lifetime
| Class | Stored in | Default | Scope | Lifetime |
|---|---|---|---|---|
| auto (default for locals) | stack | garbage | block | block |
| register | CPU register (a hint); `&` not allowed | garbage | block | block |
| static local | data/BSS | **0** | block | **whole program**; initialised once |
| static global/function | data/BSS | 0 | **this file only** (internal linkage) | program |
| extern | data/BSS | 0 | global | program; declares only, so no definition anywhere → **linker error** |
- Memory layout: text · data · BSS (zero-filled) · heap (malloc) · stack (activation records). ⚠ Pearson p.35 says "static allocation uses the stack". Statics live in data/BSS; only autos live on the stack.
- An inner declaration hides the outer one. Pearson ex.: global/extern i = 33, block i = 22, innermost i = 11 → prints `11 22 33`.
- 🔢 GATE-2007: `static int r` in f(5) (n > 3: r = n, return f(n−2)+2; else return f(n−1)+r) → **18**, since every call shares r = 5.
- **Static (lexical) vs dynamic scoping**: C binds a free variable to its definition in the enclosing *text*; dynamic scoping binds to the most recent definition on the *call stack*. Global x = 1; `show()` prints x; `f()` declares a local x = 2 and calls `show()` → static scoping prints 1, dynamic prints 2 **[Src: ME-HW p.2]**.

---

## 2. Pointers, Arrays, Strings, Structures, Memory
### 2.1 Declarations (spiral rule: start at the name, go right, then left)
| Declaration | Meaning |
|---|---|
| `int *p[10]` / `int (*p)[10]` | array of 10 int pointers / pointer to an array of 10 ints |
| `int *f(int)` / `int (*f)(int)` | function returning int* / pointer to a function |
| `const int *p` | pointer to const: `*p=` illegal, `p++` OK |
| `int *const p` | const pointer: `*p=` OK, `p++` illegal |
- `void *` must be cast before dereferencing (no arithmetic in standard C). **Dangling** = points to freed memory or a dead local (`return &local;`). **Wild** = uninitialised. **Leak** = allocated block no longer reachable.

### 2.2 Pointer arithmetic
- 📌 `p + i` = address + i·sizeof(*p). `q − p` = number of **elements** (same array only). Allowed: ptr ± int, ptr − ptr, compare, assign. **Not allowed**: ptr + ptr, ×, ÷.
- `*p++` → value, then p advances · `(*p)++` → pointee incremented · `++*p` → pointee pre-incremented · `*++p` → advance, then dereference.
- ⚠ Pearson p.33 says "all pointers are the size of int". Pointer size is implementation-defined (8 on 64-bit, where int is 4).

### 2.3 Arrays vs pointers
- ⭐ `a[i] ≡ *(a+i) ≡ i[a]`. An array name **decays** to `&a[0]` in expressions but is not a pointer: `a++` is illegal, and `sizeof a` gives the whole array. A function parameter `int a[]` *is* `int *a`, so sizeof inside the function gives the pointer size. A 2-D parameter needs its column count: `f(int m[][4])`.
- `&a + 1` skips the **whole** array:
```c
int a[5] = {1,2,3,4,5};
int *p = (int *)(&a + 1);
printf("%d %d", *(a + 1), *(p - 1));   /* 2 5 */
```
- 🔢 GATE-2015 `unsigned x[4][3]`, base 2000, 4-byte int: `x+3` = 2000 + 3·12, `*(x+3)` = &x[3][0], `*(x+2)+3` = 2000 + 24 + 12 → **2036, 2036, 2036**.
- 🔢 GATE-2015: `static int *p[] = {a, a+3, a+4, a+1, a+2}; int **ptr = p; ptr++;` → `ptr−p, **ptr` prints **140**.

### 2.4 Strings
- `char s[] = "abc"` → sizeof **4**, strlen 3, modifiable. `char *p = "abc"` → literal; **writing is UB**. `char s[3] = "abc"` is legal C (no '\0'), an error in C++.
- `s1 == s2` compares addresses. `strcmp` → <0 / 0 / >0, so `if (strcmp(a,b))` is true when the strings **differ**. `scanf("%s")` stops at whitespace; `gets` is unsafe (removed in C11).
- 🔢 GATE-2015: `char s1[7]="1234", *p = s1+2; *p='0';` → **1204**. Recursive `foo(a+1); putchar(*a);` stopping at a blank, on "ABCD EFGH" → **DCBA**.

### 2.5 Structures, unions, padding
```c
struct A { char c; int i; char d; };   /* 1+3pad+4+1+3pad = 12 */
struct B { int i; char c; char d; };   /* 4+1+1+2pad      = 8  */
struct C { char c; double d; };        /* 1+7pad+8         = 16 */
union  U { int i; char s[5]; };        /* largest 5, padded to 8 */
```
- Each member is aligned to its size; the total is padded to the largest alignment. A union's members share storage, so size = largest member, rounded up.
- Structs can be assigned, passed and returned by value, but **not compared with `==`**. `p->m` ≡ `(*p).m`. A self-referential struct needs a **pointer** member. A bit-field has no address. `enum {A, B=5, C}` → A = 0, C = 6.

### 2.6 Parameter passing & dynamic memory
| Mechanism | Effect | Where |
|---|---|---|
| Call by value (copy) | caller unchanged | **C's only mechanism**; Java (copies of primitives and of references) |
| Call by address | change via `*p` | C idiom. ⚠ Pearson calls it call-by-reference |
| Call by reference (alias) | direct | C++ `int &x` |
| Value-result / name | copy back at return / re-evaluate at each use | Ada / Algol-60 |
- 🎯 GATE-2015: `f1(a,b)` swaps by value (no effect); `f2(&b,&c)` swaps b and c. With a=4, b=5, c=6, `c−a−b` = **−5**. Pearson ex.: `f(int *p, int *q){ p = q; *p = 12; }` called as `f(&i,&j)` → prints **0 12**.
- `malloc(n)` leaves memory **uninitialised** (returns NULL on failure). `calloc(k,size)` **zero-fills**. `realloc(p,n)` may move the block and keeps the contents; `realloc(NULL,n)` ≡ malloc; on failure it returns NULL and the old block is still valid. `free(NULL)` is a no-op; a double free is UB. C++ `new`/`delete` run constructors/destructors and throw `bad_alloc`; pair `new[]` with `delete[]`.
- **Tracing checklist:** UB? → integer division/promotion → `*p++`, `&` vs `==` → pre vs post ++ → switch fall-through → static locals persist → array decay and sizeof → '\0' and sizeof vs strlen.

---

## 3. Arrays as a Data Structure
- 📌 1-D: `B + W·(i − L)`; number of elements = U − L + 1.
- 📌 ⭐ Row-major `A[L1..U1][L2..U2]`: `B + W·[(i−L1)·(U2−L2+1) + (j−L2)]`. Column-major: `B + W·[(j−L2)·(U1−L1+1) + (i−L1)]`.
- 3-D row-major: `B + W·[(i−L1)·n2·n3 + (j−L2)·n3 + (k−L3)]`. C is row-major; FORTRAN is column-major.
- 🔢 VAL[1..15][1..10], W = 4, B = 1500, VAL[12][9]. Row-major: 1500 + 4·(11·10 + 8) = **1972**. Column-major: 1500 + 4·(8·15 + 11) = **2024** **[Src: Sanchit p.7]**. A[−6..6], W = 4, B = 3500 → A[0] = **3524**.
- ⚠ GATE-2004: the time to multiply matrices is **independent** of row- or column-major storage.

**Special matrices (store only the non-zeros)** **[Src: GAC p.70–72; Ace-2020 p.125]**
| n×n matrix | Elements stored | Index of A[i][j] (1-based, row-major) |
|---|---|---|
| Lower triangular / symmetric | n(n+1)/2 | i(i−1)/2 + (j−1) |
| Upper triangular | n(n+1)/2 | (i−1)n − (i−1)(i−2)/2 + (j−i) |
| Lower triangular, column-major | n(n+1)/2 | (j−1)n − (j−1)(j−2)/2 + (i−j) |
| Tridiagonal (\|i−j\| ≤ 1) | 3n − 2 | 2i + j − 3 |
| Diagonal | n | i − 1 |
| Toeplitz (constant diagonals) | 2n − 1 | i ≤ j: j − i; i > j: n + i − j − 1 |
| Z-matrix | 3n − 2 | — |
| Band D(n,a) (main diagonal ± (a−1)) | (2a−1)n − a(a−1) | — |
- ⚠ Sanchit p.12 gives lower-triangular storage as "n(n−1)/2"; **correct is n(n+1)/2**. ⚠ GAC p.72 writes "diagonal → 4·n"; it is n elements (4n bytes only for 4-byte elements).
- **Sparse matrix (added)**: triplet form = header (rows, cols, t) plus t rows of (row, col, value) = 3(t+1) words. Worth it when 3(t+1) < m·n.
- 🎯 GATE-2005: frequencies of scores above 50 out of [0..100] → **an array of 50**. GATE-2000: Σ(i − j) over an n×n matrix = **0**.

---

## 4. Stacks (LIFO)
- push, pop, peek: all **O(1)**. Array stack: top = −1 means empty; **overflow** when pushing at top = N−1; **underflow** when popping at top = −1. Linked stack: push and pop at the head.
- Uses: function calls/recursion, bracket matching (GATE-2004), expression conversion and evaluation, undo, backtracking, DFS.
- ⭐ Two stacks growing toward each other in one array: full when **top1 = top2 − 1** (GATE-2004).
- ⭐ **Valid pop sequence** (pushes 1..n in order): once x is popped, every smaller value still on the stack must come out in **decreasing** order. The "3-1-2" pattern is impossible, e.g. 5, 4, 3, 1, 2 **[Src: Sanchit p.19]**. Number of valid sequences = Catalan C(n): 5 for n = 3, 14 for n = 4.
- GATE-2003 average stack-life = **n(X + Y) − X**.
- **Infix → postfix**: operands go to the output; `(` is pushed; `)` pops to the output until `(`. For an operator op, pop while the top has **higher** precedence, or **equal** precedence with op **left-associative**. Then push op. Right-associative `^` at equal precedence is just pushed. Prefix: reverse the input (swapping brackets), convert, reverse again.
- 🔢 `a + b*c/d^e^f*d − c + b` → postfix `a b c * d e f ^ ^ / d * + c − b +` · prefix `+ − + a * / * b c ^ d ^ e f d c b`. GATE-2004: `a + b×c − d^e^f` → **`a b c × + d e f ^ ^ −`**.
- **Evaluation**: postfix → scan left to right; on an operator pop **B, then A**, push A op B. Prefix → scan right to left; the first pop is the left operand. One stack suffices (GATE-2002).
- 🔢 GATE-2015: `10 5 + 60 6 / * 8 −` = **142**. GATE-2007: `8 2 3 ^ / 2 3 * + 5 1 * −` → top two after the first `*` are **6, 1**. `8 2 3 * 1 / + 4 1 * 2 / +` = **16**.

---

## 5. Queues (FIFO)
- ⭐ Circular array of size n, front = rear = 0 initially: **full when (rear+1) mod n == front; empty when rear == front**. Capacity n − 1 (GATE-2012). Count = (rear − front + n) mod n. The plain linear array wastes freed front cells.
- Linked queue with head and tail: enqueue at the tail, dequeue at the head, both O(1). If you enqueue at the head and dequeue at the tail of a singly linked list instead: **O(1), O(n)** (GATE-2018). A circular list with one pointer should point to the **rear** (GATE-2004); rear→next = front (GATE-2017).
- **Deque**: insert/delete at both ends. Input-restricted = insert at one end only; output-restricted = delete at one end only. **Priority queue**: highest priority first, FIFO among ties.

| PQ implementation | insert | delete-min | find-min |
|---|---|---|---|
| Unsorted array/list | O(1) | O(n) | O(n) |
| Sorted array/list | O(n) | O(1) | O(1) |
| **Binary heap** | O(log n) | O(log n) | O(1) |
| Balanced BST | O(log n) | O(log n) | O(log n) |
- **Queue from 2 stacks**: enqueue pushes S1; dequeue pops S2, refilling S2 from S1 when it is empty. Amortised O(1). GATE-2006, n inserts and m deletes: **n+m ≤ pushes ≤ 2n, 2m ≤ pops ≤ n+m**. Stack from 2 queues: one operation costs O(n).
- A stack from a min-PQ needs keys in **strictly decreasing** order (GATE-1997). A stack with REVERSE gives ENQUEUE = 3 instructions, DEQUEUE = 1 (GATE-2014). `i = delete(Q); f(Q); insert(Q,i)` **reverses** Q (GATE-2007).
- Uses: BFS, level order, round-robin CPU scheduling, spooling and buffers.

---

## 6. Linked Lists
| Operation | Array | SLL (head) | SLL (head+tail) | DLL (head+tail) |
|---|---|---|---|---|
| k-th element | O(1) | O(k) | O(k) | O(k) |
| insert/delete at front | O(n) | O(1) | O(1) | O(1) |
| insert at end | O(1)* | O(n) | **O(1)** | O(1) |
| **delete last** | O(1) | O(n) | **O(n)** (needs the predecessor) | O(1) |
| delete a given node X | O(n) | O(n) | O(n) | **O(1)** |

*If capacity is available.
- Arrays win on random access and **cache locality**. Lists grow dynamically and insert/delete without shifting, at the cost of pointer space and no binary search. Search stays O(n) even in a sorted list.
- DLL delete X: `X->prev->next = X->next; X->next->prev = X->prev;`. DLL insert after M takes 4 pointer updates **[Src: ME-2011 p.65]**. A header (sentinel) node removes the NULL special cases; a circular list's loop test is `while (p != head)`.
```c
struct node *reverse(struct node *head) {      /* iterative, 3 pointers */
    struct node *prev = NULL, *cur = head, *next;
    while (cur) { next = cur->next; cur->next = prev; prev = cur; cur = next; }
    return prev;                               /* i.e. *head_ref = prev */
}
```
- ⚠ Sanchit p.55 inserts at the front with `ptr->next = head->next`. **Correct: `ptr->next = head; head = ptr;`**. Sanchit p.57's reversal `r=q; q=r;` should be `r=q; q=p; p=p->next; q->next=r;`. Its recursive traversal (p.51) has no NULL base case.
- Delete X given only a pointer to X: copy next's data into X, then delete next (**impossible for the last node**). Middle node / n-th from the end → two pointers; cycle → Floyd slow/fast. All O(n) time, O(1) space. ⚠ Shared p.70 says finding the middle is O(1); it is O(n). Merge sort is the sort of choice for lists.
- 🎯 GATE codes **[Src: Sanchit p.58–62]**:
  - Pairwise value swap on 1..7 → **2 1 4 3 6 5 7**.
  - Move the last node to the front → `q->next = NULL; p->next = head; head = p;`.
  - `f(p)` returns 1 iff the list is **sorted non-decreasing**.
  - DLL prev/next swap → list **reversed**.
  - Printing after the recursive call → **reverse order**.
  - `fun(start->next->next)` with prints before and after, on 1..6 → **1 3 5 5 3 1**.
  - With head and tail pointers, only **deleting the last element** depends on n. The 8th node from the start is O(1); the 8th from the end is O(n).
- ⚠ GATE-2017 `join(m,n)` (walks to the end of n, sets `p->next = m`). Sanchit p.62 keys it as D. **Correct is B**: it appends m to n, or dereferences NULL if n is empty. Set union/intersection on unsorted lists are the slowest operations (GATE-2004).

---

## 7. Recursion
- Types: **direct**; **indirect/mutual**; **tail** (the recursive call is the *last* action); **non-tail/head**; **tree** (several calls, e.g. Fibonacci); **nested** (Ackermann). Each call pushes an activation record (parameters, locals, return address), so space = O(maximum depth). No base case → stack overflow.
- ⭐ Tail recursion can be turned into a loop with **no stack**; non-tail recursion needs an explicit stack **[Src: ME-Toppers p.180]**. `return n*fact(n-1)` is **not** tail recursive (the multiply is pending).
- 📌 Counting calls: write `T(n) = 1 + Σ T(sub-calls)` with T(base) = 1.
  - GATE-2015 `get(n){ if(n<1) return; get(n−1); get(n−3); … }` → get(6) makes **25** calls.
  - `T(n) = 1 + 2T(n−1)`, T(0) = 1 → 2ⁿ⁺¹ − 1 calls, depth n + 1 **[Src: Ace-2020 p.135]**.
- 📌 Naive Fibonacci with F(0) = 0, F(1) = 1: **calls = 2F(n+1) − 1** (fib(5) → 15), **additions = F(n+1) − 1**, stack depth n. The first addition comes after n + 1 calls **[Src: ME-HW p.130]**.
- 📌 Tower of Hanoi: **moves = 2ⁿ − 1**. Calls = **2ⁿ⁺¹ − 1 if the base case is n = 0** (an empty call); 2ⁿ − 1 if the n = 1 base case moves directly. ⚠ Sanchit p.28 gives 2ⁿ⁺¹ − 1 next to an n = 1 base case **[cf. ME-CS p.140]**.
- Ackermann: A(0,n) = n+1; A(m,0) = A(m−1,1); A(m,n) = A(m−1, A(m,n−1)). A(1,n) = n+2, A(2,n) = 2n+3, A(3,n) = 2ⁿ⁺³ − 3.
- Excessive recursion: `pow(x,n/2)*pow(x,n/2)` recomputes the half. Saving it in a variable gives O(log n) multiplications (2³⁷ in 7) **[Src: ME-2011 p.30]**.
- 🔢 Traces **[Src: Sanchit p.29–35]**:
  - `fun(x,y){ if(x==0) return y; return fun(x−1, x+y); }` → fun(4,3) = **13**.
  - `foo(n,r) = n%r + foo(n/r,r)` (sum of base-r digits): foo(345,10) = **12**, foo(513,2) = **2**.
  - `fun(x,y) = x + fun(x,y−1)` = x·y; `fun2(a,b) = fun(a, fun2(a,b−1))` = **aᵇ**.
  - f(11) with f(n/2)+f(n/2+1) for odd n → **5**. GATE-2015 fun(5) → **51**.
  - Printing before and after the recursive call gives a palindrome: `print(1000)` → 1000 2000 4000 4000 2000 1000.
- Tower of Hanoi is **not** backtracking; N-queens, knight's tour and m-colouring are.

---

## 8. Trees & Binary Trees
- A tree with n nodes has **n − 1 edges**. ⭐ **Height convention**: GATE counts edges, so a single node has height 0 and the root is at depth 0. Some books count levels from 1, so read each question. ⚠ Sanchit p.75 says "path length = number of nodes"; the standard definition is **edges**.

| Name | Definition |
|---|---|
| Full / strict / 2-tree | every node has 0 or 2 children (CLRS, GAC). ⚠ Horowitz–Sahni and Pearson use "full binary tree of depth k" for the **perfect** tree with 2ᵏ − 1 nodes |
| Perfect | every internal node has 2 children and all leaves share one level |
| Complete | all levels full except possibly the last, filled **left to right** |
| Skewed | every node has only a left (or only a right) child |

| 📌 Quantity (height h in edges) | Value |
|---|---|
| Max nodes at level i / of height h / min of height h | 2ⁱ / 2ʰ⁺¹ − 1 / h + 1 |
| Min height with n nodes | ⌊log₂ n⌋ |
| ⭐ Leaves vs degree-2 nodes | **n₀ = n₂ + 1** |
| NULL links in a linked BT | n + 1 |
| Strict BT, I internal | L = I + 1, n = 2I + 1; min nodes of height h = 2h + 1 |
| k-ary (every internal node has k children) | **L = (k−1)I + 1** |
| Complete BT | height ⌊log₂ n⌋, leaves ⌈n/2⌉; 1-based children 2i, 2i+1, parent ⌊i/2⌋ |
| Array size for **any** BT of n nodes | **2ⁿ − 1** (right-skewed; GATE-2006) |
- 🔢 GATE-2015: height 5 → max 63, min 6. GATE-2007: L = 41, I = 10 → **n = 5**. GATE-2010: every node has an odd number of descendants → **0** nodes have exactly one child.
- **Traversals**: pre NLR · in LNR · post LRN · level order = **BFS with a queue**. Each is O(n). ⭐ Root-Right-Left ("New-order", GATE-2016) = **reverse of postorder**.
- ⭐ **Uniqueness**: inorder + (pre, post or level) → unique tree. **Pre + post → not unique** (unique only for a strict BT). A BST needs just pre or post.
- Rebuilding: the root is the first of preorder or the last of postorder; split the inorder sequence at the root; recurse. 🔢 GATE-2007: in = d b e a f c g, pre = a b d e c f g → post = **d e b f g c a**. GATE-2018 (post 8 9 6 7 4 5 2 3 1, in 8 6 9 4 7 2 5 1 3) → height **4** **[Src: Ace-2020 p.55]**.
- **Expression tree** (leaves operands, internal nodes operators): inorder → infix (needs brackets), preorder → prefix, postorder → postfix. Build from postfix with a stack: operand → push a node; operator → pop the right child, then the left, join, push **[Src: GAC p.129–130]**.
- ⭐ **Counting**: unlabelled shapes = BSTs on n distinct keys = **Catalan C(n) = (2n)!/((n+1)!·n!)** → 1, 1, 2, **5**, **14**, 42, 132. 3 unlabelled nodes → 5 (GATE-2007); 4 keys → 14 BSTs. Labelled binary trees = n!·C(n). A **given** shape fills with n keys into a BST in exactly **1** way (GATE-2011).
- **Threaded BT (added)**: the n + 1 NULL links point to the inorder predecessor/successor, so inorder traversal needs no stack.

---

## 9. Binary Search Trees
- Left subtree < key < right subtree. ⭐ **Inorder = sorted.** Min is the leftmost node, max the rightmost.
- Search, insert, delete, successor: **O(h)**. Average O(log n), **worst O(n)** for a skewed tree (GATE-2013, GATE-2015). h ranges from ⌊log₂ n⌋ to n − 1, so 15 nodes → **3 and 14** (GATE-2017).
- **Successor**: the minimum of the right subtree if there is one; otherwise the lowest ancestor whose left subtree contains the node.
- **Delete**: leaf → remove; one child → splice it in; two children → copy the inorder successor in, then delete that node. ⭐ This successor has **no left child**.
- The first key inserted is the root. Keys 1..n with p nodes in the root's right subtree → the first key was **n − p** **[Src: Ace-2020 p.28]**. Insertion orders that give a chain = **2ⁿ⁻¹** (64 for n = 7, GATE-2016).
- 🔢 GATE-2013: pre 30 20 10 15 25 23 39 35 42 → post **15 10 23 25 20 35 42 39 30**. GATE-2015: insert 71, 65, 84, 69, 67, 83 → deepest key **67**. Expected comparisons = Σ(depth+1)/n, e.g. 18/7 ≈ 2.57 **[Src: Sanchit p.97]**.
- A BST rebuilds from its post/pre-order in **Θ(n)** (GATE-2008). ⚠ Ace-2020 p.24 derives O(n log n) for its method; not tight. Range sum over m keys = O(log n + m) → **110** (GATE-2014). ⚠ Sanchit p.98 also prints "100".
- For O(log n) delete-min plus insert-if-absent, use a **balanced BST**, not a heap (GATE-2003).

---

## 10. AVL Trees
- An AVL tree is a BST with **BF = h(left) − h(right) ∈ {−1, 0, +1}** at every node; all operations O(log n) worst case.

| Insertion case (path from the lowest unbalanced node A) | Fix |
|---|---|
| LL | single **right** rotation at A |
| RR | single **left** rotation at A |
| LR | left rotation at the child, then right at A |
| RL | right rotation at the child, then left at A |
- ⭐ An **insertion** is fixed by one single or double rotation at the lowest unbalanced ancestor. A **deletion** may need rotations up to O(log n) ancestors. In deletion, take B = A's child on the taller side: BF(B) = 0 or the same sign as A → single rotation; opposite sign → double. Diagrams **[Src: ME-2011 p.99–102; GAC p.151–154]**; deletion examples **[Src: Ace-2020 p.45; ME-CS p.230]**.
- 📌 ⭐ Min nodes for height h: **N(h) = N(h−1) + N(h−2) + 1**, N(0) = 1, N(1) = 2 → 1, 2, 4, **7**, 12, 20, 33, 54 (= F(h+3) − 1). Max nodes = 2ʰ⁺¹ − 1. Worst-case height ≈ **1.44 log₂ n** **[Src: GAC p.149]**. Max height with 7 nodes = **3** (GATE-2009).
- 🔢 Insert 70, 60, 80, 50, 65, 68: 68 goes 70 → 60 → 65 → right, so 70 gets BF +2 via L then R, an **LR** case. Result: 65 with left child 60 (holding 50) and right child 70 (holding 68 and 80) → **3 leaves**.
- One line on others: Red-Black tree height ≤ 2·log₂(n+1); splay tree amortised O(log n).

---

## 11. Binary Heaps
- A **complete** binary tree in an array with max-heap order (parent ≥ children). Height ⌊log₂ n⌋; leaves at indices ⌊n/2⌋+1 … n.

| Operation | Time |
|---|---|
| find-max | O(1) |
| insert (sift-up) / delete-max (last element to the root, sift-down) | O(log n) |
| ⭐ **build-heap** (heapify i = ⌊n/2⌋ … 1) | **O(n)**, since Σ⌈n/2ʰ⁺¹⌉·h = O(n) **[Src: GAC p.135–136]** |
| n successive inserts | O(n log n) |
| find-min in a max-heap / search a key | O(n), scanning the ⌈n/2⌉ leaves (GATE-2006) |
| merge two n-heaps | O(n) by rebuilding (the slowest standard operation) |
- 🔢 GATE-2014: 10 8 5 3 2; insert 1, then 7 → **10 8 7 3 2 1 5**. GATE-2015: insert 35 into 40 30 20 10 15 16 17 8 4 → **40 35 20 10 30 16 17 8 4 15**. GATE-2009: two deletes on 25 14 16 13 10 8 12 → **14 13 12 8 10**. GATE-2015: 89 19 50 17 12 15 2 5 7 11 6 9 100 → **3** swaps.
- Valid heap test: A[i] ≥ A[2i] and A[i] ≥ A[2i+1] for every i.
- 📌 Number of heaps: H(n) = C(n−1, L)·H(L)·H(R), with L and R the subtree sizes → **80** for {1..7} (GATE-2018).
- Min-heap of 1..1023: key 9 sits at depth ≤ **8** (GATE-2016). The k-th smallest for a constant k takes O(1) (GATE-2008). Adding n elements to an n-heap costs Θ(n) (GATE-2008).
- Insert with binary search on the leaf-to-root path: **O(log log n) comparisons**, but still O(log n) swaps (GATE-2003) **[Src: Ace-2020 p.85]**. In a 16-element heap the root's right subtree has **7** nodes.
- d-ary heap (0-based): children d·i+1 … d·i+d. For the top 10 of 10⁶ items, keep a min-heap of size 10. Heapsort → `04_Algorithms.md`.

---

## 12. Graphs: Representation, BFS, DFS
| | Adjacency matrix | Adjacency list |
|---|---|---|
| Space | **Θ(V²)** | **Θ(V + E)** |
| Edge (u,v)? / neighbours of u | O(1) / O(V) | O(deg u) / O(deg u) |
| BFS/DFS | **O(V²)** (GATE-2014) | **O(V + E)** |
| Best for | dense graphs | sparse graphs |
- The undirected matrix is symmetric with 2E ones; Σ deg = 2E. 📌 Max edges: n(n−1)/2 undirected, n(n−1) directed. Simple undirected graphs on n labelled vertices = **2^(n(n−1)/2)**.
- **BFS** (queue + visited[]): shortest edge-count paths from the source in an unweighted graph (GATE-2014). u visited before v ⇒ d(u) ≤ d(v) (GATE-2001). A non-tree edge (u,v) has |d(u) − d(v)| ≤ 1, so **never 2** (GATE-2015). In a binary tree, a vertex at distance 4 is BFS vertex number ≤ **31** (GATE-2016). BFS also tests bipartiteness.
- **DFS** (stack or recursion): edges are tree, back (signals a cycle), forward or cross. ⭐ An **undirected** DFS has **no cross edges** (GATE-2018: I true, II false). Recursion depth ≤ V. Applications: cycles, topological sort, components (Θ(V + E), GATE-2008), articulation points.
- To check a claimed DFS order: each next vertex must be an unvisited neighbour of the **most recent** vertex that still has one. BFS must finish each level first.
- ⚠ Sanchit p.122 recurses with `DFS(v)`; it should be `DFS(x)`. Twin pointers in adjacency lists take **Θ(m+n)** (GATE-2016). MST, shortest paths → `04_Algorithms.md`.

---

## 13. C++, Java & OOP Essentials (added — not in sources)
- **Pillars:** **Encapsulation** = data plus methods bound together, data hidden by access specifiers. **Abstraction** = show *what*, hide *how*. **Inheritance** = "is-a" reuse. **Polymorphism** = one interface, many forms. GATE-2005's essential features: abstraction & encapsulation plus polymorphism with inheritance.
- **Class vs object**: a blueprint vs an instance. In C++ an empty class has sizeof = **1**; a virtual function adds a vptr to each object.
- **Constructors**: class name, no return type, can be overloaded. Kinds: default, parameterised, **copy `X(const X&)`** (the parameter must be a reference, or the copy recurses forever; it runs on pass/return by value and `X b = a;`), move. The default copy is shallow.
- ⭐ **Order**: constructors run **base → members → derived**; destructors run in reverse. Constructors cannot be virtual. **Make the base destructor virtual** whenever objects are deleted through a base pointer.

| C++ inheritance → | public | protected | private |
|---|---|---|---|
| base public member becomes | public | protected | private |
| base protected member becomes | protected | protected | private |
| base private member | inaccessible | inaccessible | inaccessible |
- Default access is private for `class`, public for `struct`. Inheritance kinds: single, multilevel, hierarchical, multiple, hybrid. **Diamond problem** (two copies of the shared base) → fixed in C++ by a **virtual base class**. Java allows one class plus many interfaces.

| Overloading | Overriding |
|---|---|
| same name, different parameters (return type alone is not enough) | same signature in a subclass |
| **compile-time** (static binding), incl. operators and templates | **run-time** (dynamic binding) |
| one class | base ↔ derived; C++ needs `virtual`, Java methods are virtual unless static/final/private |
- **Virtual function**: each class has a vtable, each object a vptr; a call through a base pointer or reference runs the actual object's version. **Pure virtual** `virtual void f() = 0;` makes the class **abstract** (not instantiable; pointers/references allowed). Object slicing = copying a derived object into a base object.
- Not overloadable in C++: `::` `.` `.*` `?:` `sizeof` `typeid`. **friend**: a non-member that can read privates; friendship is not inherited, mutual or transitive. **static** member: one copy per class; a static function has **no `this`**. `this` is a pointer in C++, a reference in Java.
- **Reference vs pointer**: a reference must be initialised and cannot be null, reseated or used in arithmetic. **Templates** give compile-time generics; Java generics use type erasure and need wrapper types.

| C++ | Java |
|---|---|
| compiled to native code | **bytecode** run on the JVM ("write once, run anywhere") |
| pointers, struct/union, goto, global functions | no explicit pointers; everything sits in classes |
| multiple class inheritance, operator overloading | interfaces only; no operator overloading (only `+` for String) |
| new/delete, destructors | **garbage collection** |
| platform-dependent type sizes | fixed: int 4, long 8, **char 2 (Unicode)**, boolean; no unsigned types; `>>>` |
| by value or by reference | **always by value** (references are copied) |
- **JDK = JRE + tools** (javac, jar, javadoc). **JRE = JVM + libraries.** The JVM loads, verifies and executes bytecode by interpreting plus **JIT** compilation of hot code to native code. Bytecode is portable; the JVM is platform-specific.
- Java access: `private` (class) < default (package) < `protected` (package + subclasses) < `public`. A top-level class is public or default; one public class per file, named after the file.
- **final** = constant variable / method that cannot be overridden / class that cannot be extended. **finally** = always runs after try/catch, even after `return`, unless `System.exit()`. **finalize()** = pre-GC hook (deprecated).

| Interface | Abstract class |
|---|---|
| fields `public static final` only | any fields |
| abstract + `default`/`static` methods (Java 8), private methods (Java 9) | abstract + concrete methods |
| no constructors; a class `implements` many | constructors exist; a class `extends` one |
- **Exceptions**: Throwable → **Error** (OutOfMemoryError, StackOverflowError) and **Exception**. **Checked** exceptions (IOException, FileNotFoundException, SQLException, ClassNotFoundException, InterruptedException) must be caught or declared with `throws`. **Unchecked** = RuntimeException and subclasses (NullPointerException, ArithmeticException for int ÷ 0, ArrayIndexOutOfBoundsException, ClassCastException, NumberFormatException). `throw` raises; `throws` declares. A superclass catch placed before a subclass catch → compile error.
- **String** is **immutable** (enables the pool, thread safety, hash caching). **StringBuffer**: mutable, **synchronized**. **StringBuilder**: mutable, unsynchronized, fastest.
- **== vs equals()**: `==` compares references for objects; `equals()` compares content (String overrides it). `"ab" == "ab"` → true (pooled); `new String("ab") == "ab"` → false. Equal objects must have equal hashCodes.
- **GC** reclaims unreachable objects; `System.gc()` is only a request. Locals get no default (using one uninitialised is a compile error); fields default to 0 / false / null. Float ÷ 0 → Infinity or NaN.

---

## Last-day revision sheet
| Item | Value |
|---|---|
| Row- / column-major A[i][j] | B + W[(i−L1)·cols + (j−L2)] / B + W[(j−L2)·rows + (i−L1)] |
| Triangular / tridiagonal / Toeplitz / band | n(n+1)/2 / 3n−2 / 2n−1 / (2a−1)n − a(a−1) |
| Lower-triangular index (1-based, row-major) | i(i−1)/2 + (j−1) |
| Circular queue, size n | full (r+1)%n == f; empty r == f; capacity n−1 |
| Catalan C(n) | (2n)!/((n+1)!n!): 1, 1, 2, 5, 14, 42, 132 |
| BT of height h (edges) | max 2ʰ⁺¹−1, min h+1; level i ≤ 2ⁱ |
| Leaves | n₀ = n₂ + 1; k-ary L = (k−1)I + 1; NULL links n+1 |
| Complete BT | height ⌊log₂ n⌋, leaves ⌈n/2⌉, parent ⌊i/2⌋ |
| AVL min nodes | 1, 2, 4, 7, 12, 20, 33 (N(h) = N(h−1)+N(h−2)+1); height ≈ 1.44 log₂ n |
| Heap | build O(n); insert/delete O(log n); leaves ⌊n/2⌋+1..n |
| Fibonacci calls / additions | 2F(n+1)−1 / F(n+1)−1 |
| Tower of Hanoi | moves 2ⁿ−1; calls 2ⁿ⁺¹−1 (base n = 0) |
| Chain-producing BST insertion orders / simple graphs | 2ⁿ⁻¹ / 2^(n(n−1)/2) |
| BFS/DFS | O(V+E) list, O(V²) matrix |

1. ⭐ `i = i++` and `printf("%d %d", i, i++)` → undefined; argument evaluation order is unspecified.
2. `sizeof(i++)` does not increment i (sizeof does not evaluate its operand).
3. `-1 < 1u` is false; `&` and `|` bind looser than `==`; `*p++` = `*(p++)`.
4. `a[i] ≡ i[a]`; `&a + 1` skips the whole array; an array parameter is a pointer.
5. `char s[]="abc"`: sizeof 4, strlen 3. Writing to `char *p = "abc"` is UB.
6. Static locals: initialised once, default 0. Autos hold garbage. `extern` without a definition → linker error.
7. `#define SQ(x) x*x` → SQ(2+3) = 11; macros allocate no memory.
8. switch: integral expression only; duplicate case → compile error; no break → fall-through.
9. C has only call by value; pointers simulate call by reference.
10. malloc → garbage; calloc → zeros; free(NULL) is safe.
11. {char, int, char} = 12 bytes, reordered = 8; union = largest member, rounded up.
12. Postfix evaluation pops B, then A; pop sequence "3-1-2" is impossible; two stacks are full when top1 = top2 − 1.
13. Queue from two stacks: amortised O(1). Circular-list queue: keep the rear pointer.
14. SLL: deleting the last node is O(n) even with a tail pointer. Deleting a given node by copying fails for the last node.
15. Inorder + one other traversal → unique tree; pre + post → not unique; Root-Right-Left = reverse postorder.
16. BST inorder is sorted; the two-child delete uses the successor, which has no left child.
17. BST worst case O(n); 15 nodes → height 3 to 14.
18. AVL insert: one (single or double) rotation; delete: up to O(log n). 7 nodes → max height 3.
19. Build-heap O(n); find-min in a max-heap O(n); 80 min-heaps on 7 keys.
20. BFS → unweighted shortest paths; undirected DFS has no cross edges.
21. Tail recursion → loop without a stack; `n*fact(n−1)` is not tail recursive.
22. Constructors base → derived, destructors reverse; base destructor virtual.
23. Overloading = compile time; overriding = run time; copy-constructor parameter by reference.
24. Abstract class (≥ 1 pure virtual / `abstract`) cannot be instantiated; an interface's fields are public static final.
25. JDK ⊃ JRE ⊃ JVM; JIT compiles hot bytecode at run time; bytecode is portable, the JVM is not.
26. final / finally / finalize = constant-or-sealed / always-runs block / pre-GC hook.
27. String immutable; StringBuffer synchronized; StringBuilder fastest.
28. `==` compares references, `equals()` content; checked = IOException family, unchecked = RuntimeException family.
29. Java passes by value only; char is 2 bytes; no pointers, no multiple class inheritance, no operator overloading.
30. Not overloadable in C++: `::` `.` `.*` `?:` `sizeof`.

## Dropped as outside TPSC syllabus
- **Hashing** (direct-address tables, hash functions, probing, chaining): Shared p.1+, ME-Toppers p.2+, GAC ch. 55, Ace-2020 → `04_Algorithms.md`.
- **Heapsort, sorting comparisons, list merge sort analysis** (GAC ch. 46, Shared p.70); **searching and asymptotic analysis**; **graph algorithms** (MST, shortest paths, topological sort) → `04_Algorithms.md`.
- **B-trees / B+ trees** (ME-HW ~p.95–105, ME-CS) → DBMS notes.
- **Theory of Computation / compiler** pages (DPDA, LR(0), null-production removal) in ME-CS from about p.300 onward.
- Backtracking applications (Sudoku, 8-queens), DOM as a tree, randomized BST, dynamic arrays and amortised analysis (GAC ch. 31, 41, 43.5–43.7); the Young-tableau puzzle (GATE-2015, Sanchit p.11).
- Pearson's numerical-methods PYQ (secant method) and its activation-record/storage-allocation PYQ (compiler design).
