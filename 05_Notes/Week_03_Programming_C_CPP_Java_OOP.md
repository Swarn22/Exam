# Week 3 — Programming in C, C++, Java & OOP

**Syllabus §5 (part):** Programming in C, C++, Java. Recursion.
**Estimated marks: ~7** (of the ~14 for Data Structures & Programming)

> ⭐ **Strategy note.** State-PSC papers ask far more **Java and OOP definitional** questions than GATE does, and far fewer pointer-tracing puzzles. Sections 5–7 of this file deserve as much time as sections 1–4.

---

## 💡 What this week is about

Two different things, sharing a syllabus section:

1. **How programming languages actually behave** — storage, pointers, memory layout, recursion. This is the "C" half, and it is tested with *trace-the-output* questions.
2. **Object-oriented concepts** — encapsulation, inheritance, polymorphism, and the specific rules of C++ and Java. This is tested with *definitional* questions and comparison tables.

The second half is easier to score on and is more heavily represented in the papers this exam resembles.

---

# 1. C fundamentals

## 1.1 Data types and sizes

### 💡 The idea

A **type** tells the compiler two things: how many **bytes** to reserve, and how to **interpret** those bytes. The same 32 bits could be the integer 1,078,530,011 or the float 3.14159 — only the type decides.

| Type | Typical bytes | Range |
|---|---|---|
| `char` | 1 | −128 to 127 (signed) / 0–255 (unsigned) |
| `short` | 2 | −32,768 to 32,767 |
| `int` | 4 | −2³¹ to 2³¹ − 1 |
| `long` | 4 (Windows) / 8 (Linux) | |
| `long long` | 8 | |
| `float` | 4 | ~6–7 significant digits |
| `double` | 8 | ~15–16 significant digits |
| `void` | — | No value / generic |

⚠ ⭐ **These sizes are implementation-defined.** The C standard guarantees only:
- `sizeof(char) == 1` **by definition** (a "byte" in C *is* a char)
- `char ≤ short ≤ int ≤ long ≤ long long`
- `int` is at least 16 bits, `long` at least 32

⚠ **Java is different** — its sizes are **fixed on every platform** (`int` is always 4 bytes, `char` always 2). That portability guarantee is one of Java's design goals.

## 1.2 ⭐⭐ Storage classes

### 💡 The idea

Every variable has three independent properties, and a storage class sets all three:

- **Scope** — *where in the code* the name is visible
- **Lifetime** — *how long* the memory exists
- **Linkage** — whether other files can see it

| Class | Stored in | Scope | ⭐ Lifetime | Default value |
|---|---|---|---|---|
| ⭐ **`auto`** | Stack | Block | Until the block exits | **Garbage** |
| **`register`** | CPU register (a *hint*) | Block | Until the block exits | Garbage |
| ⭐ **`static`** (local) | Data segment | ⭐ **Block** | ⭐ **The WHOLE program** | ⭐ **0** |
| **`static`** (global/function) | Data segment | ⭐ **This file only** | Whole program | 0 |
| ⭐ **`extern`** | Data segment | Global, across files | Whole program | 0 |

⭐ **`auto` is the default for local variables** — the keyword is essentially never written.

### 💡 Understanding `static` — the one that gets asked

⭐ **`static` means two completely different things depending on where you write it.** This is the source of most confusion.

**(a) `static` on a LOCAL variable** — gives it *program lifetime* while keeping *block scope*. The variable is initialised **once** and **retains its value between calls**:

```c
void counter() {
    static int c = 0;    // initialised ONCE, ever
    c++;
    printf("%d ", c);
}
int main() { counter(); counter(); counter(); }
```
🔢 Output: **`1 2 3`**

Compare with a plain local:
```c
void counter() {
    int c = 0;           // re-initialised on EVERY call
    c++;
    printf("%d ", c);
}
```
🔢 Output: **`1 1 1`**

**(b) `static` on a GLOBAL variable or function** — restricts **linkage**, hiding it from other source files. It has nothing to do with lifetime (globals already live forever). This is C's way of making something "private to this file".

⚠ ⭐ So `static` means *"remember between calls"* for locals and *"hide from other files"* for globals. Both meanings appear in exams.

### 💡 Memory layout of a running C program

Knowing this makes several questions obvious:

```
High address
   ┌─────────────────┐
   │      STACK      │  ← local variables, function parameters,
   │        ↓        │    return addresses. Grows DOWNWARD.
   │                 │
   │                 │
   │        ↑        │
   │       HEAP      │  ← malloc/calloc. Grows UPWARD.
   ├─────────────────┤
   │   BSS segment   │  ← uninitialised globals & statics (zeroed)
   ├─────────────────┤
   │  DATA segment   │  ← initialised globals & statics
   ├─────────────────┤
   │  TEXT (code)    │  ← the machine instructions (read-only)
   └─────────────────┘
Low address
```

⭐ This explains:
- why deep recursion causes **stack overflow** (the stack grows into the heap)
- why globals default to 0 (the BSS is zeroed at load time) but locals contain garbage (the stack is just whatever was there before)
- why string literals cannot be modified (they live in read-only memory)

## 1.3 ⭐ Operator precedence and associativity

### 💡 The idea

**Precedence** answers *"which operator binds tighter?"* — `a + b * c` is `a + (b*c)` because `*` has higher precedence.
**Associativity** answers *"same precedence — which way do we group?"* — `a / b * c` is `(a/b)*c` because `/` and `*` are left-associative.

| Level | Operators | Associativity |
|---|---|---|
| 1 (highest) | `()` `[]` `->` `.` `++`/`--` (**postfix**) | Left → Right |
| 2 | `!` `~` `++`/`--` (**prefix**) unary `+`/`−` `*` `&` `sizeof` `(type)` | ⭐ **Right → Left** |
| 3 | `*` `/` `%` | Left → Right |
| 4 | `+` `−` | Left → Right |
| 5 | `<<` `>>` | Left → Right |
| 6 | `<` `<=` `>` `>=` | Left → Right |
| 7 | `==` `!=` | Left → Right |
| 8–12 | `&` then `^` then `|` then `&&` then `||` | Left → Right |
| 13 | `?:` (ternary) | ⭐ **Right → Left** |
| 14 | `=` `+=` `−=` … | ⭐ **Right → Left** |
| 15 (lowest) | `,` | Left → Right |

⭐ Memory hooks: **unary operators, the ternary, and assignment are right-associative**; almost everything else is left-associative. Note that **bitwise `&` has LOWER precedence than `==`**, which is why `if (x & MASK == 0)` is a classic bug — it parses as `x & (MASK == 0)`.

### 🔢 Worked example

```c
int a = 10, b = 3;
printf("%d", a/b*b + a%b);
```
- `/` and `*` are equal precedence, **left**-associative → `(a/b)*b`
- `a/b` is **integer** division: 10/3 = **3** (truncated, remainder discarded)
- `3 * 3` = 9
- `a%b` = 10 % 3 = **1**
- `9 + 1` = **10**

⭐ Answer: **10**. Note it is not simply `a` (which would be 10 by coincidence here) — the point is that `(a/b)*b` loses the remainder, and `a%b` gives it back. In general `(a/b)*b + a%b == a` for positive integers, which is exactly the division algorithm.

### ⚠ Undefined behaviour

```c
int i = 5;
printf("%d %d", i++, ++i);     // UNDEFINED
int x = i++ + ++i;             // UNDEFINED
a[i] = i++;                    // UNDEFINED
```
These modify a variable more than once without an intervening **sequence point**, so the C standard imposes no requirement at all — different compilers give different answers. ⚠ Well-constructed exams avoid these; if you meet one, the intended answer is usually **"undefined"** or **"compiler dependent"**.

### ⚠ Type promotion trap

```c
if (-1 < 1U) { ... }     // FALSE!
```
Mixing signed and unsigned promotes **both** to unsigned. `−1` becomes 4294967295, which is not less than 1. ⭐ **Signed/unsigned mixing promotes to unsigned.**

📌 **Implicit promotion order:** `char`/`short` → `int` → `unsigned int` → `long` → `unsigned long` → `float` → `double` → `long double`

---

# 2. ⭐⭐ Pointers

## 2.1 💡 The idea

Every byte of memory has an **address** — a number identifying its location, like a house number on a street.

A **pointer** is just a variable that stores an address instead of a value.

```
Memory:
  address 1000:  [  10  ]   ← int x = 10
  address 2000:  [ 1000 ]   ← int *p = &x;  (p stores x's ADDRESS)
```

Two operators do all the work:
- **`&x`** — "address of x" → gives 1000
- **`*p`** — "the value at the address in p" (**dereference**) → gives 10

```c
int x = 10;
int *p = &x;     // p now holds x's address
printf("%d", *p); // prints 10
*p = 20;         // writes THROUGH p → x is now 20
printf("%d", x);  // prints 20
```

⭐ **Why pointers exist at all** — four genuine reasons:
1. To let a function **modify** the caller's variables (C has no other way — see §3.1)
2. To handle **dynamically sized** data (arrays whose size is unknown at compile time)
3. To build **linked structures** (lists, trees — Week 4)
4. To pass large structures **cheaply** (pass an 8-byte address instead of copying 1000 bytes)

⚠ A pointer's own **size is the same for every type** (8 bytes on a 64-bit machine) — it always just holds an address. `sizeof(int*) == sizeof(double*) == sizeof(char*)`.

**Pointer to pointer:**
```c
int x = 10;
int *p = &x;
int **pp = &p;    // pp holds p's address
// **pp is 10
```

## 2.2 ⭐⭐ Pointer arithmetic

### 💡 The idea

When you write `p + 1`, C does **not** add 1 to the address. It adds **one element's worth** of bytes — because that is almost always what you mean.

📌 ⭐ **`p + n` advances the address by `n × sizeof(*p)` bytes.**

*Why:* if `p` points to `A[0]`, you want `p+1` to point to `A[1]`, not to the middle of A[0].

🔢 `int *p` with `sizeof(int) == 4`, currently holding address 1000:
- `p + 1` → **1004**
- `p + 3` → **1012** (the address increased by **12 bytes**, not 3)

🔢 `char *c` holding 1000: `c + 3` → **1003** (char is 1 byte)
🔢 `double *d` holding 1000: `d + 3` → **1024** (double is 8 bytes)

📌 **Pointer subtraction** `p2 − p1` (within the same array) gives the number of **elements** between them, not bytes.

🔢 If `p1` = 1000 and `p2` = 1012 for `int*`, then `p2 − p1` = **3**, not 12.

**Legal pointer operations:** `pointer + integer`, `pointer − integer`, `pointer − pointer`, comparison (`<`, `==`).
**Illegal:** `pointer + pointer`, `pointer * pointer`, `pointer / pointer`.

## 2.3 ⭐⭐ Arrays and pointers — related but not the same

### 💡 The idea

An **array** is a contiguous block of memory. A **pointer** is a variable holding one address. They feel similar because of one rule:

⭐ **Array decay:** when an array name is used in an expression, it **decays into a pointer to its first element** — with **two exceptions**: `sizeof` and `&`.

```c
int a[5];
int *p = a;        // legal — a decays to &a[0]
```

| | Array `int a[5]` | Pointer `int *p` |
|---|---|---|
| `sizeof` | ⭐ **20** (whole array) | ⭐ **8** (just the pointer) |
| Reassignable | ❌ No (`a = ...` is an error) | ✅ Yes |
| Memory | 20 bytes allocated for data | 8 bytes holding an address |

**Equivalent notations** — all four are legal and identical:
```c
a[i]  ==  *(a + i)  ==  *(i + a)  ==  i[a]
```
(The last one looks absurd but is legal, precisely because `a[i]` is *defined* as `*(a+i)` and addition commutes.)

### 🔢 The `sizeof` idiom — and its trap

```c
int arr[5];
int n = sizeof(arr) / sizeof(arr[0]);   // 20/4 = 5  ✅
```
This is the standard way to get an array's length.

⚠ ⭐ **But it BREAKS inside a function:**
```c
void f(int a[]) {                        // 'a' is really int*
    printf("%d", sizeof(a)/sizeof(a[0])); // 8/4 = 2  ❌  WRONG
}
int main() { int arr[5]; f(arr); }
```
Because the array **decayed** at the call, the function only received a pointer. It has no way to know the length — which is why C functions must always take the length as a separate parameter.

⭐ This is a very common exam question. `sizeof(arr)/sizeof(arr[0])` gives the element count **only in the scope where the array was declared**.

## 2.4 ⭐⭐ 2-D array address calculation

### 💡 The idea

Memory is **one-dimensional** — a flat sequence of addresses. A 2-D array is an illusion the compiler maintains by laying the rows out one after another. There are two possible layouts:

**Row-major** (C, C++, Java, Python) — store row 0 entirely, then row 1, then row 2:
```
A[0][0] A[0][1] A[0][2] | A[1][0] A[1][1] A[1][2] | A[2][0] ...
```

**Column-major** (FORTRAN, MATLAB, R) — store column 0 entirely, then column 1:
```
A[0][0] A[1][0] A[2][0] | A[0][1] A[1][1] A[2][1] | ...
```

📌 ⭐ **Row-major:** `Address of A[i][j] = Base + [ (i − L₁) × N_cols + (j − L₂) ] × size`
📌 ⭐ **Column-major:** `Address of A[i][j] = Base + [ (j − L₂) × N_rows + (i − L₁) ] × size`

*(L₁, L₂ are the lower bounds of the two dimensions — usually 0 in C, but a question may use 1.)*

**How to remember which:** in **row**-major you skip whole **rows** first, so you multiply by the number of **columns** in a row. In **column**-major you skip whole columns, so you multiply by the number of **rows**.

### 🔢 Worked example

`int A[10][20]`, base address 1000, 4 bytes per element, **row-major**, 0-based. Find the address of `A[3][5]`.

```
Elements skipped = 3 complete rows × 20 columns  = 60
                 + 5 elements into row 3          =  5
                 total                            = 65
Address = 1000 + 65 × 4 = 1000 + 260 = 1260
```
⭐ Answer: **1260**

🔢 **Same array, column-major:**
```
Elements skipped = 5 complete columns × 10 rows  = 50
                 + 3 into column 5                =  3
                 total                            = 53
Address = 1000 + 53 × 4 = 1212
```

🔢 **With 1-based bounds.** `A[1..10][1..20]`, base 1000, 4 bytes, row-major. Address of `A[3][5]`:
```
= 1000 + [(3−1) × 20 + (5−1)] × 4
= 1000 + [40 + 4] × 4
= 1000 + 176 = 1176
```
⚠ ⭐ **Always check the lower bound.** Missing the `−1` is the most common error here.

## 2.5 ⭐ The four kinds of problem pointer

### 💡 The ideas — these four terms get asked as definitions

| Pointer | Meaning | Example |
|---|---|---|
| **NULL pointer** | Points to nothing, **deliberately**. Dereferencing crashes | `int *p = NULL;` |
| ⭐ **Dangling pointer** | Points to memory that **has been freed** or has gone out of scope | `free(p);` then using `*p` |
| ⭐ **Wild pointer** | **Uninitialised** — contains whatever garbage was in that memory | `int *p; *p = 5;` |
| **Void pointer** | Generic pointer; must be **cast before dereferencing**. `malloc` returns one | `void *p = malloc(10);` |

⚠ ⭐ **Dangling ≠ wild ≠ null.** Dangling *was* valid and no longer is; wild was *never* initialised; null is intentionally nothing.

**Function pointer** — holds the address of a function, enabling callbacks:
```c
int add(int a, int b) { return a+b; }
int (*fp)(int, int) = add;
printf("%d", fp(2,3));   // 5
```

## 2.6 ⭐ Dynamic memory allocation

### 💡 The idea

`int a[100];` fixes the size at compile time. But what if you do not know the size until the program runs (reading a file, asking the user)? You need memory allocated **at run time**, from the **heap**.

| Function | Behaviour |
|---|---|
| `malloc(size)` | Allocates `size` bytes. ⭐ **Contents are UNINITIALISED (garbage)** |
| ⭐ `calloc(n, size)` | Allocates `n × size` bytes. ⭐ **Contents are ZERO-INITIALISED** |
| `realloc(p, newsize)` | Resizes an existing block; **may move it**, so always use the returned pointer |
| `free(p)` | Returns the block to the heap |

⭐ All are in `<stdlib.h>`, all allocate on the **heap**, all return `void*`, and all return **`NULL` on failure** (which you should always check).

```c
int *arr = malloc(n * sizeof(int));
if (arr == NULL) { /* handle failure */ }
...
free(arr);
arr = NULL;      // ⭐ prevents a dangling pointer
```

⭐ Memory hook: **c**alloc **c**lears; **m**alloc does not.

⚠ **Three classic bugs:**
- **Memory leak** — allocated but never freed. The program's memory use grows forever.
- **Double free** — calling `free(p)` twice. Undefined behaviour, often a crash.
- **Use after free** — dereferencing a dangling pointer.

### ⭐ Stack vs heap

| | **Stack** | **Heap** |
|---|---|---|
| Allocation | ⭐ **Automatic** (the compiler) | ⭐ **Manual** (`malloc`/`new`) |
| Deallocation | Automatic on block exit | Manual (`free`/`delete`) or by a garbage collector |
| Speed | ⭐ **Fast** (just move a pointer) | Slower (must search for a free block) |
| Size | Limited (a few MB) — ⭐ **stack overflow** on deep recursion | Large (most of available RAM) |
| Lifetime | Until the enclosing block exits | Until explicitly freed |
| Fragmentation | None | Possible |

---

# 3. Functions and recursion

## 3.1 ⭐⭐ Parameter passing

### 💡 The idea

When you call `f(x)`, what exactly does `f` receive — a **copy** of x, or **x itself**? The answer determines whether `f` can change the caller's variable, and languages differ.

| Mechanism | What is passed | Can the caller's variable change? | Used by |
|---|---|---|---|
| ⭐ **Call by value** | A **copy** of the value | ❌ **No** | ⭐ **C (always)**, Java (primitives) |
| ⭐ **Call by reference** | The variable **itself** (an alias) | ✅ Yes | C++ (`int &x`), Pascal (`var`), Fortran |
| **Call by address / pointer** | A copy of the **address** | ✅ Yes, via dereferencing | C's workaround |
| **Call by value-result** (copy-restore) | Copy in, **copy back on return** | ✅ Yes, but only at return | Ada (`in out`) |
| **Call by name** | The argument **expression**, textually substituted and **re-evaluated at every use** | ✅ Yes | Algol 60 (mostly theoretical) |
| **Call by sharing** | A copy of the **reference** | Object can be **mutated**, not **reassigned** | Java (objects), Python |

### 🔢 The classic swap demonstration

⭐ **This fails:**
```c
void swap(int a, int b) {       // CALL BY VALUE
    int t = a; a = b; b = t;
}
int main() {
    int x = 1, y = 2;
    swap(x, y);
    printf("%d %d", x, y);      // prints "1 2" — UNCHANGED
}
```
`swap` received *copies*. It faithfully swapped its own two local variables, then they were destroyed.

⭐ **This works:**
```c
void swap(int *a, int *b) {     // pass ADDRESSES
    int t = *a; *a = *b; *b = t;
}
int main() {
    int x = 1, y = 2;
    swap(&x, &y);
    printf("%d %d", x, y);      // prints "2 1" ✅
}
```

⭐ **Exam statement: C has only call by value.** Passing a pointer is still call by value — you are copying an *address*. The effect resembles call by reference, but the mechanism is different.

⚠ ⭐ **Java is also always call by value** — but for objects, the *reference value* is copied. So:
```java
void modify(int[] a) { a[0] = 99; }   // ✅ visible to caller (mutation)
void replace(int[] a) { a = new int[5]; }  // ❌ NOT visible (reassignment)
```
The method can change what the object *contains*, but cannot make the caller's variable point somewhere else.

## 3.2 ⭐⭐ Recursion

### 💡 The idea

A **recursive** function calls itself on a smaller version of the same problem. It needs exactly two things:

1. ⭐ A **base case** — a version of the problem small enough to answer directly, with no further call. *Without this, infinite recursion → stack overflow.*
2. ⭐ A **recursive case** that makes **progress** toward the base case.

```c
int fact(int n) {
    if (n == 0) return 1;          // base case
    return n * fact(n - 1);        // recursive case, smaller n
}
```

**Trace `fact(4)`:**
```
fact(4) = 4 × fact(3)
              fact(3) = 3 × fact(2)
                            fact(2) = 2 × fact(1)
                                          fact(1) = 1 × fact(0)
                                                        fact(0) = 1     ← base case
                                          fact(1) = 1
                            fact(2) = 2
              fact(3) = 6
fact(4) = 24
```

⭐ **How it works in memory:** each call pushes an **activation record (stack frame)** onto the stack, holding that call's own parameters, locals and return address. Four nested calls = four frames, each with its **own** `n`. That is why recursion works at all — and why it consumes stack space proportional to its depth.

### 🔢 Fibonacci — the standard trace question

```c
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```
The sequence: fib(0)=0, fib(1)=1, fib(2)=1, fib(3)=2, fib(4)=3, ⭐ **fib(5)=5**, fib(6)=8, fib(7)=13.

⚠ Some textbooks start Fibonacci at 1,1,2,3,5. **Read the base case in the code given.** Here `fib(0)` returns 0, so the sequence starts 0,1,1,2,3,5.

⭐ **Why naïve Fibonacci is terrible:** the call tree recomputes the same values over and over.
```
                fib(5)
           /            \
       fib(4)          fib(3)
      /     \          /    \
  fib(3)   fib(2)  fib(2)  fib(1)
   /  \     /  \    /  \
fib(2) f(1) f(1) f(0) f(1) f(0)
 / \
f(1) f(0)
```
`fib(2)` is computed **three** times. For fib(40) the redundancy is astronomical.

📌 ⭐ **Naïve fib(n) is O(2ⁿ)**. With **memoisation** (caching results) it becomes **O(n)** — which is exactly the *overlapping subproblems* property that makes it a dynamic-programming problem (Week 5).
📌 Number of calls made by naïve fib(n) = **2·F(n+1) − 1**.

### ⭐ Types of recursion

| Type | Description |
|---|---|
| **Direct** | f calls f |
| **Indirect / mutual** | f calls g, and g calls f |
| ⭐ **Tail recursion** | The recursive call is the ⭐ **very last operation** — nothing is done with its result. Compilers can convert it into a loop, using **O(1)** stack |
| **Tree recursion** | More than one recursive call per invocation (naïve fib) |

🔢 **Tail vs non-tail:**
```c
int fact(int n) { return n * fact(n-1); }              // NOT tail — the multiply
                                                        // happens after the call returns
int fact_t(int n, int acc) { return fact_t(n-1, n*acc); } // TAIL — nothing after the call
```

### ⭐ Classic recursions to know

| Problem | Recurrence | 📌 Result |
|---|---|---|
| Factorial | T(n) = T(n−1) + 1 | O(n) |
| ⭐ **Towers of Hanoi** | T(n) = 2T(n−1) + 1 | ⭐ **Minimum moves = 2ⁿ − 1** |
| Naïve Fibonacci | T(n) = T(n−1) + T(n−2) + 1 | O(2ⁿ) |
| GCD (Euclid) | gcd(a,b) = gcd(b, a % b) | O(log min(a,b)) |
| Binary search | T(n) = T(n/2) + 1 | O(log n) |
| Ackermann | — | Grows faster than any primitive recursive function |

🔢 **Towers of Hanoi with 4 discs:** 2⁴ − 1 = **15 moves**. With 64 discs (the legend): 2⁶⁴ − 1 ≈ 1.8 × 10¹⁹ moves.

### ⭐ Recursion vs iteration

| | Recursion | Iteration |
|---|---|---|
| Code clarity | ⭐ Often clearer for tree/divide-and-conquer problems | Clearer for simple loops |
| Memory | ⭐ **O(depth) stack space** | O(1) |
| Speed | Slower (call overhead) | Faster |
| Risk | ⭐ **Stack overflow** | Infinite loop |

⭐ Every recursion can be rewritten iteratively (using an explicit stack if necessary), and vice versa.

---

# 4. Structures, unions and files

## 4.1 ⭐ Structure vs union

### 💡 The idea

A **structure** groups several variables that exist **at the same time** — a student's name, roll number and marks. Members sit side by side in memory, so the size is the sum.

A **union** groups several variables that share **the same memory**, of which only **one is meaningful at a time**. Used when a value could be one of several types, and you know which.

```c
struct S { char c; int i; };   // c AND i both exist
union  U { char c; int i; };   // c OR i — they overlap
```

| | ⭐ **`struct`** | ⭐ **`union`** |
|---|---|---|
| Memory | ⭐ **Sum of all members** (+ padding) | ⭐ **Size of the LARGEST member** |
| Members valid | All simultaneously | ⭐ **One at a time** |
| Use | Records | Memory saving, type reinterpretation |

🔢 On a machine with 4-byte ints and 4-byte alignment:
- `sizeof(struct S)` = 1 (char) + **3 (padding)** + 4 (int) = **8 bytes**
- `sizeof(union U)` = max(1, 4) = ⭐ **4 bytes**

### 💡 Structure padding — why the size is bigger than you expect

CPUs read memory fastest when a 4-byte value sits at an address divisible by 4. So the compiler inserts invisible **padding** bytes to keep each member aligned.

🔢 ```c
struct A { char c; int i; char d; };
```
Layout: `c` at 0, padding at 1–3, `i` at 4–7, `d` at 8, padding at 9–11 (so the whole struct is a multiple of 4) → **12 bytes**, not 6.

🔢 Reordering helps:
```c
struct B { char c; char d; int i; };   // c at 0, d at 1, pad 2-3, i at 4-7 → 8 bytes
```
⭐ Same members, different order, **8 bytes instead of 12**. This is why "order struct members largest-first" is a real optimisation.

**Bit-fields** pack members into a specified number of bits:
```c
struct Flags { unsigned a : 3; unsigned b : 5; };   // 3+5 = 8 bits in one byte
```

**Access:** `s.member` for a struct variable, ⭐ `p->member` (identical to `(*p).member`) via a pointer.

**Self-referential structures** are the basis of all linked data structures (Week 4):
```c
struct Node { int data; struct Node *next; };
```

## 4.2 File handling

| Task | Function |
|---|---|
| Open / close | `fopen`, `fclose` |
| Formatted I/O | `fscanf`, `fprintf` |
| Line/string I/O | `fgets`, `fputs` |
| Binary I/O | `fread`, `fwrite` |
| Positioning | `fseek`, `ftell`, `rewind` |
| End of file | `feof` |

**Modes:** `"r"` read · ⚠ ⭐ **`"w"` write — TRUNCATES an existing file to zero length** · `"a"` append · `"r+"`, `"w+"`, `"a+"` for read+write · add `b` (`"rb"`) for binary.

## 4.3 Preprocessor

### 💡 The idea

Before the compiler proper sees your code, the **preprocessor** performs pure **text substitution**. It understands nothing about types or syntax.

| Directive | Purpose |
|---|---|
| `#include` | Paste in another file's contents |
| `#define` | Textual macro substitution |
| `#ifdef` / `#ifndef` / `#endif` | Conditional compilation; ⭐ **include guards** |
| `#pragma` | Compiler-specific instruction |

⚠ ⭐ **Macros are not functions.** They are text, so:
```c
#define SQ(x) x*x
SQ(2+3)   →  2+3*2+3  =  11    ❌  not 25
```
Fix by parenthesising **everything**:
```c
#define SQ(x) ((x)*(x))
SQ(2+3)   →  ((2+3)*(2+3))  =  25   ✅
```
⚠ And macros can **double-evaluate**: `SQ(i++)` increments `i` twice.

| | Macro | Function |
|---|---|---|
| Expanded at | Preprocessing (text) | Called at run time |
| Type checking | ❌ None | ✅ Yes |
| Speed | Faster (no call overhead) | Call overhead |
| Debugging | Hard | Easy |
| Code size | Grows with each use | One copy |

---

# 5. ⭐⭐ Object-Oriented Programming concepts

## 5.1 💡 Why OOP exists

In **procedural** programming (plain C) you have data on one side and functions on the other. Nothing stops any function from modifying any data, so in a large program it becomes impossible to know who changed what. Related things also drift apart — a `Student` struct here, its functions scattered across ten files.

**Object-Oriented Programming** binds data and the functions that operate on it into a single unit (a **class**), and controls who may touch the data.

- **Class** — the blueprint/template (e.g. "Car": has colour, speed; can accelerate, brake)
- **Object** — an actual instance built from the blueprint (a specific red car doing 60 km/h)

One class, many objects — like one architectural drawing and many houses.

## 5.2 ⭐⭐ The four pillars

### ⭐ 1. Encapsulation

📌 **Bundling data with the methods that operate on it, and restricting direct access to the data.**

```java
class BankAccount {
    private double balance;            // nobody outside can touch this directly

    public void deposit(double amt) {
        if (amt > 0) balance += amt;   // the class enforces its own rules
    }
    public double getBalance() { return balance; }
}
```
💡 **Why it matters:** without encapsulation any code could write `account.balance = -5000;`. With it, the only way in is `deposit()`, which validates. The class **protects its own invariants**.

⭐ Mechanism: `private` fields + `public` getters/setters.

### ⭐ 2. Abstraction

📌 **Exposing only what is essential, hiding the implementation detail.**

💡 **Everyday analogy:** you drive a car by turning a wheel and pressing pedals. You do not need to know about fuel injection or differential gears. The steering wheel is the *interface*; the mechanism is *hidden*.

⭐ Mechanism: abstract classes and interfaces — they declare *what* can be done without saying *how*.

⚠ ⭐ **Encapsulation vs abstraction** — a favourite exam distinction:
- **Encapsulation** hides **DATA**, and is the *mechanism* (access modifiers).
- **Abstraction** hides **COMPLEXITY/IMPLEMENTATION**, and is the *design goal* (interfaces).

They are related — encapsulation is one way to achieve abstraction — but they are not the same.

### ⭐ 3. Inheritance

📌 **A class acquires the properties and behaviour of another class.**

```java
class Vehicle {                        // base / parent / super class
    int wheels;
    void start() { ... }
}
class Car extends Vehicle {            // derived / child / sub class
    int doors;                         // Car automatically HAS wheels and start()
}
```
💡 **Why:** code **reuse**, and it models the real-world "**is-a**" relationship (a Car *is a* Vehicle).

⚠ Contrast with **composition**, the "**has-a**" relationship (a Car *has an* Engine). ⭐ Modern design advice is *"prefer composition over inheritance"*, because inheritance couples classes tightly.

### ⭐ 4. Polymorphism

📌 **"Many forms" — one interface, many implementations.**

```java
Shape s;
s = new Circle();    s.draw();   // draws a circle
s = new Square();    s.draw();   // draws a square
```
The **same call** `s.draw()` does different things depending on the actual object. This lets you write code that works with `Shape` without knowing or caring which shape it is.

💡 **Why it matters:** you can add a `Triangle` class later and existing code that loops over shapes calling `draw()` works unchanged. That is the whole payoff of OOP.

## 5.3 ⭐⭐ Types of polymorphism

| | ⭐ **Compile-time (static)** | ⭐ **Run-time (dynamic)** |
|---|---|---|
| Achieved by | ⭐ **Method/function OVERLOADING**, operator overloading | ⭐ **Method OVERRIDING** (with virtual functions) |
| Resolved at | ⭐ **Compile time** (early binding) | ⭐ **Run time** (late binding) |
| Mechanism | Signature matching by the compiler | ⭐ **vtable / vptr lookup** |
| Cost | Free | A small indirection |

### ⭐⭐ Overloading vs overriding — memorise this

```java
// OVERLOADING — same name, DIFFERENT parameters, same class
class Calc {
    int add(int a, int b)          { return a+b; }
    double add(double a, double b) { return a+b; }
    int add(int a, int b, int c)   { return a+b+c; }
}
```
The compiler picks one by looking at the argument types at the call site. Nothing happens at run time.

```java
// OVERRIDING — same name, SAME parameters, base and derived class
class Animal { void speak() { System.out.println("..."); } }
class Dog extends Animal { void speak() { System.out.println("Woof"); } }

Animal a = new Dog();
a.speak();     // prints "Woof" — decided at RUN TIME by the object's actual type
```

| | ⭐ **Overloading** | ⭐ **Overriding** |
|---|---|---|
| Where | Same class | Base class **and** derived class |
| Parameter list | ⭐ **MUST DIFFER** | ⭐ **MUST BE IDENTICAL** |
| Return type alone can differ? | ⭐ **❌ No — compile error** | Covariant return allowed |
| Binding | Compile time | Run time |
| Also called | Static / early binding | Dynamic / late binding |
| Java annotation | — | `@Override` |

⚠ ⭐ **Two methods differing only in return type is a compile error, not overloading.** The compiler cannot choose based on return type, since a return value may be ignored.

### 💡 How run-time dispatch actually works — the vtable

Each class with virtual functions gets a hidden table (**vtable**) of function pointers, and each object carries a hidden pointer (**vptr**) to its class's vtable.

```
Dog object:  [vptr] ──► Dog's vtable: [ speak → Dog::speak ]
Cat object:  [vptr] ──► Cat's vtable: [ speak → Cat::speak ]
```
Calling `a.speak()` compiles to *"follow the vptr, look up slot 0, call it"* — so the **object itself** determines which code runs. That is dynamic dispatch, and it costs one extra memory indirection.

## 5.4 ⭐ Types of inheritance

| Type | Structure | Diagram |
|---|---|---|
| **Single** | B inherits from A | A → B |
| ⭐ **Multiple** | C inherits from A **and** B | A,B → C ⚠ **not for classes in Java** |
| **Multilevel** | C ← B ← A (a chain) | A → B → C |
| **Hierarchical** | B and C both inherit from A | A → B, A → C |
| **Hybrid** | Any combination | |

### ⭐⭐ The diamond problem

```
        A
       / \
      B   C        Both B and C inherit from A
       \ /
        D          D inherits from both B and C
```
💡 **The problem:** if A has a method `f()`, and D calls `f()`, which copy does it get — the one inherited via B, or via C? If B and C each *overrode* `f()` differently, the call is genuinely **ambiguous**. Worse, D may end up with **two copies of A's data**.

⭐ **Two solutions:**
- **C++:** allows multiple inheritance and offers **virtual inheritance** (`class B : virtual public A`) to ensure only one shared copy of A.
- ⭐ **Java:** sidesteps it entirely — **forbids multiple inheritance of CLASSES**, but allows a class to implement **many INTERFACES** (which traditionally carried no state or implementation, so there was nothing to be ambiguous about).

⭐ **Exam answer: Java does not support multiple inheritance of classes in order to avoid the diamond/ambiguity problem.**

## 5.5 ⭐ Constructors and destructors

### 💡 The idea

A **constructor** is a special method that runs **automatically** when an object is created. Its job is to put the object into a valid initial state — you can never accidentally use an uninitialised object.

⭐ **Rules for a constructor:**
- Has the ⭐ **same name as the class**
- Has ⭐ **NO return type at all** — not even `void`
- Is called automatically on object creation
- ✅ **Can be overloaded**
- ❌ ⭐ **Cannot be `static`** and ❌ ⭐ **cannot be `virtual`**

⚠ Writing `void MyClass()` makes it an **ordinary method** that happens to share the class's name, not a constructor.

| Constructor type | Purpose |
|---|---|
| **Default** | No parameters. The compiler supplies one **only if you write none at all** |
| **Parameterised** | Takes arguments |
| ⭐ **Copy constructor** | `MyClass(const MyClass &other)` — creates a new object from an existing one |

**Destructor (C++):** `~MyClass()` — runs when the object is destroyed, to release resources. No parameters, no return type, ⭐ **cannot be overloaded** (there is only one way to die).

⭐ **Why a destructor should often be `virtual`:**
```cpp
Base *p = new Derived();
delete p;     // without a virtual destructor, only Base::~Base runs
              // → Derived's resources leak
```

### ⭐ Shallow vs deep copy

```cpp
class S { char *name; };
```
- **Shallow copy** (the default) copies the **pointer**. Now two objects point at the *same* buffer. When both destructors run, the buffer is freed twice → **crash**. Modifying one object silently changes the other.
- ⭐ **Deep copy** allocates a new buffer and copies the **contents**. This is what a properly written copy constructor does.

⭐ **This is precisely why you write a copy constructor.**

---

# 6. ⭐⭐ C++ specifics

## 6.1 ⭐ Operators that cannot be overloaded

📌 ⭐ **`::` (scope resolution) · `.` (member access) · `.*` (pointer-to-member) · `?:` (ternary) · `sizeof`**
*(also `typeid` and the named cast operators)*

💡 **Why these five?** They are part of the language's *structural* grammar rather than operations on values. Allowing `::` to be redefined would make it impossible to parse C++ at all.

⭐ **Everything else CAN be overloaded** — including `+`, `-`, `*`, `/`, `[]`, `()`, `->`, `<<`, `>>`, `=`, `==`, `++`, `new`, `delete`.

🔢 Overloading `<<` is how `cout << x` works for user-defined types.

## 6.2 Access specifiers and defaults

| Specifier | Accessible from |
|---|---|
| `private` | The class itself (and its friends) only |
| `protected` | The class **and derived classes** |
| `public` | Anywhere |

📌 ⭐ **Default access: `class` → private; `struct` → public.** (That is essentially the *only* difference between `class` and `struct` in C++.)

## 6.3 ⭐ Other C++ features

| Feature | 💡 What it is |
|---|---|
| ⭐ **`friend`** | A function or class granted access to private members. Deliberately breaks encapsulation — used for operator overloading and tightly-coupled helpers |
| **Templates** | Generic programming: write `template<class T> T max(T a, T b)` once and it works for `int`, `double`, `string` |
| ⭐ **`new` / `delete`** | Type-aware allocation. ⭐ **`new` calls the CONSTRUCTOR and returns a typed pointer; `malloc` does neither** |
| ⭐ **References** | `int &r = x;` — an alias. ⭐ **Must be initialised at declaration and can never be reseated.** This is what makes true call-by-reference possible |
| **STL** | Standard Template Library: `vector`, `list`, `map`, `set`, `stack`, `queue`, plus algorithms |
| **Exception handling** | `try` / `catch` / `throw` |
| **Namespaces** | Prevent name collisions (`std::cout`) |
| **Pure virtual function** | `virtual void f() = 0;` — makes the class ⭐ **abstract** (cannot be instantiated); derived classes must implement it |

⚠ ⭐ **`new`/`delete` vs `malloc`/`free`:** `new` calls constructors and is type-safe; `malloc` just returns raw bytes as `void*`. Never mix them (`new` then `free` is undefined behaviour).

---

# 7. ⭐⭐ Java

## 7.1 💡 How Java achieves portability

```
   Hello.java   ──javac──►   Hello.class   ──JVM──►   machine code
  (source code)             (BYTECODE —              (specific to
                             platform independent)     this CPU)
```

⭐ **The trick:** `javac` compiles to **bytecode**, an instruction set for an imaginary machine. Every real platform ships a **JVM** that executes that bytecode. So the *program* is portable and the *JVM* is platform-specific.

⭐ **"Write once, run anywhere."**

| Term | 💡 Meaning |
|---|---|
| ⭐ **JVM** | Java Virtual Machine — ⭐ **executes bytecode**. Platform-specific |
| ⭐ **JRE** | JVM + standard class libraries — enough to **RUN** Java programs |
| ⭐ **JDK** | JRE + compiler (`javac`) + tools — needed to **DEVELOP** |
| **JIT** | Just-In-Time compiler inside the JVM; compiles frequently-executed ("hot") bytecode to native code for speed |

📌 Nesting: **JDK ⊃ JRE ⊃ JVM**

## 7.2 ⭐⭐ What Java deliberately omits

📌 ⭐ **No explicit pointers or pointer arithmetic · No `goto` (reserved but unused) · No operator overloading · No multiple inheritance of classes · No destructors · No `struct`/`union` · No global variables · No `sizeof` operator**

💡 **Why:** each omission removes a class of bugs. No pointer arithmetic means no buffer overruns; no manual `delete` means no dangling pointers or double frees. Java trades expressive power for safety.

⭐ **What Java adds:** automatic **garbage collection**, built-in multithreading, interfaces, exception handling, packages, security (bytecode verifier, sandbox), reflection.

## 7.3 ⭐⭐ Access modifiers

| Modifier | Same class | Same package | Subclass (other package) | Anywhere |
|---|---|---|---|---|
| ⭐ **`private`** | ✅ | ❌ | ❌ | ❌ |
| **default** (no keyword) | ✅ | ✅ | ❌ | ❌ |
| **`protected`** | ✅ | ✅ | ✅ | ❌ |
| **`public`** | ✅ | ✅ | ✅ | ✅ |

⭐ Increasing openness: `private` < default (package-private) < `protected` < `public`.
⚠ ⭐ **`private` means "same class only"** — not "same package".

## 7.4 ⭐⭐ `final` vs `finally` vs `finalize`

### 💡 Three unrelated things with confusingly similar names — and one of the most-asked Java questions.

⭐ **`final` — a MODIFIER (keyword)**
```java
final int MAX = 100;              // constant — cannot be reassigned
final void f() { }                // method cannot be OVERRIDDEN
final class C { }                 // class cannot be EXTENDED
```

⭐ **`finally` — a BLOCK**
```java
try {
    risky();
} catch (Exception e) {
    handle(e);
} finally {
    cleanup();      // ⭐ ALWAYS runs — exception or not, return or not
}
```
Used for releasing resources (closing files, connections) that must be freed whatever happens.

⭐ **`finalize()` — a METHOD**
```java
protected void finalize() { }     // called by the GC before reclaiming the object
```
⚠ **Deprecated and unreliable** — you cannot know *when* (or even *whether*) the garbage collector will call it. Modern Java uses `try-with-resources` instead.

📌 ⭐ **Summary: `final` = modifier · `finally` = block that always executes · `finalize()` = GC hook (deprecated).**

## 7.5 ⭐⭐ Strings

### 💡 The idea — why String is immutable

```java
String s = "Hello";
s = s + " World";     // does NOT modify the original
```
This creates a **brand new** String object; the original `"Hello"` is untouched (and becomes garbage). `String` objects can **never** be changed after creation.

💡 **Why design it that way?** Security (a String passed to a security check cannot be altered afterwards), thread safety for free (nothing can change, so no locks needed), and it enables the **string constant pool** — identical literals can safely share one object.

| Class | Mutable? | Thread-safe? | Speed |
|---|---|---|---|
| ⭐ **`String`** | ⭐ **❌ Immutable** | ✅ (by immutability) | — |
| **`StringBuffer`** | ✅ Mutable | ⭐ **✅ Synchronised** | Slower |
| **`StringBuilder`** | ✅ Mutable | ❌ Not synchronised | ⭐ **Fastest** |

⭐ Use `StringBuilder` when building a string in a loop — concatenating with `+` in a loop creates a new object each iteration, making it O(n²).

### ⚠ The `==` vs `.equals()` trap

```java
String a = "hello";
String b = "hello";
String c = new String("hello");

a == b        // TRUE  — both refer to the same pooled literal
a == c        // ⭐ FALSE — 'new' forces a separate object
a.equals(c)   // ⭐ TRUE  — same CONTENT
```

📌 ⭐ **`==` compares REFERENCES (identity); `.equals()` compares CONTENT.** Always use `.equals()` for strings.

## 7.6 ⭐⭐ Abstract class vs interface

### 💡 The idea

Both let you declare *what* something can do without saying *how*. They differ in what else they can carry.

**Abstract class** — a partially built class. It can hold real code and state, and it expresses an "is-a" relationship.
```java
abstract class Shape {
    String colour;                          // state ✅
    void setColour(String c) { colour = c; } // concrete method ✅
    abstract double area();                 // subclasses MUST implement
}
```

**Interface** — a pure contract. Traditionally no state, no implementation.
```java
interface Drawable {
    void draw();          // implicitly public abstract
}
```

| | ⭐ **Abstract class** | ⭐ **Interface** |
|---|---|---|
| Instantiable | ❌ | ❌ |
| Methods | Abstract **and** concrete | Abstract (plus `default`/`static` since Java 8) |
| Variables | Any kind | ⭐ Implicitly **`public static final`** (constants) |
| Constructor | ✅ Yes | ❌ No |
| ⭐ Multiple inheritance | ❌ **One superclass only** | ⭐ **✅ A class can implement MANY** |
| Keyword | `extends` | `implements` |
| ⭐ Use when | Classes share **code** and an "is-a" relationship | ⭐ **Unrelated classes share a capability/contract** |

🔢 A `Bird` and an `Aeroplane` are unrelated, but both can fly → give both an interface `Flyable`. A `Circle` and a `Square` are both genuinely Shapes with shared colour handling → abstract class `Shape`.

## 7.7 ⭐⭐ Exception handling

### 💡 The idea

An **exception** is an object representing an abnormal event. Instead of returning error codes that callers forget to check, Java *throws* the exception, unwinding the stack until someone catches it.

```
                    Throwable
                   /         \
              Error           Exception
        (JVM problems —      /          \
         do NOT catch)   RuntimeException   everything else
        OutOfMemoryError  ⭐ UNCHECKED      ⭐ CHECKED
        StackOverflowError                 IOException
                          NullPointerException     SQLException
                          ArrayIndexOutOfBounds    ClassNotFoundException
                          ArithmeticException      FileNotFoundException
                          ClassCastException
                          NumberFormatException
```

⭐⭐ **Checked vs unchecked — the key distinction:**

| | ⭐ **Checked** | ⭐ **Unchecked** |
|---|---|---|
| Which | `Exception` **except** `RuntimeException` | ⭐ **`RuntimeException` and `Error`** |
| ⭐ Compiler | ⭐ **MUST be caught or declared with `throws`** | No requirement |
| Represents | Recoverable external conditions (file missing, network down) | Programming bugs (null dereference, bad index) |
| Examples | `IOException`, `SQLException`, `ClassNotFoundException` | `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException` |

💡 **The reasoning:** a missing file is a *foreseeable* condition your code should handle, so the compiler insists. A null dereference is a *bug* — you should fix the code, not catch it everywhere.

⚠ ⭐ **`throw` vs `throws`:**
- **`throw`** — a **statement** that raises one exception instance: `throw new IOException("oops");`
- **`throws`** — a **clause in the method signature** declaring what it might raise: `void read() throws IOException`

## 7.8 ⭐ Other Java essentials

**`static`** — belongs to the **class**, not to any instance. One copy shared by all objects.
```java
class Counter {
    static int count = 0;       // shared by every Counter
    int id;                     // one per object
}
```
⚠ ⭐ **A `static` method cannot use `this`** or access instance members directly (there is no instance). `static` blocks run once, at class loading.
🔢 `main` is `static` precisely because it must run before any object exists.

**`this` and `super`** — reference to the current object / the parent class.

**⭐ Garbage collection** — the JVM automatically reclaims objects that are no longer **reachable** from any live reference.
⚠ ⭐ **`System.gc()` is only a REQUEST**, not a command; the JVM may ignore it. Algorithms: mark-and-sweep, generational (young/old), copying.

**⭐ The 8 primitive types:**

| Type | Bytes | Note |
|---|---|---|
| `byte` | 1 | |
| `short` | 2 | |
| `int` | 4 | Default integer type |
| `long` | 8 | |
| `float` | 4 | |
| `double` | 8 | Default floating type |
| ⭐ **`char`** | ⭐ **2** | ⭐ **Unicode** — unlike C's 1-byte char |
| `boolean` | JVM-dependent | `true`/`false` only — no 0/1 equivalence |

⭐ **These sizes are fixed on every platform** — a deliberate contrast with C.

**Wrapper classes** — `int`→`Integer`, `char`→`Character`, etc., so primitives can be used where objects are required (e.g. in collections). ⭐ **Autoboxing/unboxing** converts automatically.

**⭐ Collections framework:**
```
Collection                          Map (⚠ NOT a Collection)
├── List  (ordered, duplicates OK)  ├── HashMap
│   ├── ArrayList  (fast random     ├── TreeMap (sorted)
│   │               access)         └── LinkedHashMap
│   └── LinkedList (fast insert)
├── Set   (no duplicates)
│   ├── HashSet
│   └── TreeSet (sorted)
└── Queue
    └── PriorityQueue
```
⚠ ⭐ **`Map` does NOT extend `Collection`** — because a Map stores key-value *pairs*, not single elements.

**Threads** — extend `Thread` or ⭐ **implement `Runnable`** (preferred, because Java allows only one superclass and you may need it for something else).
States: New → Runnable → Running → Blocked/Waiting → Terminated.
`synchronized` provides mutual exclusion (Week 6's critical-section problem, at the language level).

📌 `public static void main(String[] args)` — the exact required signature.

---

# 8. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| Default storage class (local) | `auto` |
| `static` local variable | Retains value between calls; initialised **once**; defaults to 0 |
| `static` global | Restricts visibility to that **file** |
| Locals live on / dynamic memory on | Stack / heap |
| Deep recursion causes | Stack overflow |
| `p = p + 3` for `int *p` | Address += **12 bytes** |
| `p2 − p1` gives | Number of **elements** |
| `sizeof(arr)/sizeof(arr[0])` | Element count — ⭐ **fails after array decay** |
| Array decay exceptions | `sizeof` and `&` |
| Row-major A[i][j] | Base + (i×ncols + j) × size |
| Column-major A[i][j] | Base + (j×nrows + i) × size |
| `malloc` vs `calloc` | calloc **zero-initialises** |
| Both return | `void*`, `NULL` on failure |
| Freed-then-used pointer | **Dangling** |
| Never-initialised pointer | **Wild** |
| C parameter passing | ⭐ **Call by value only** |
| Java parameter passing | Call by value (of the reference for objects) |
| Recursion needs | Base case + progress |
| Recursion stores state in | Activation records on the stack |
| Towers of Hanoi moves | **2ⁿ − 1** |
| Naïve fib(n) complexity | **O(2ⁿ)**; O(n) with memoisation |
| Tail recursion | Recursive call is the **last** operation |
| `union` size | **Largest** member |
| `struct` size | Sum + **padding** |
| `p->x` equals | `(*p).x` |
| `"w"` file mode | **Truncates** the file |
| Macro pitfalls | No type checking, double evaluation |
| Encapsulation hides | **Data** |
| Abstraction hides | **Implementation/complexity** |
| Inheritance relationship | "is-a" |
| Composition relationship | "has-a" |
| Compile-time polymorphism | **Overloading** |
| Run-time polymorphism | **Overriding** + virtual functions |
| Run-time dispatch mechanism | **vtable / vptr** |
| Overloading requires | **Different parameters** |
| Overriding requires | **Identical signature** |
| Differ only in return type | ⭐ **Compile error** |
| Diamond problem | Multiple inheritance ambiguity |
| Java's diamond solution | No multiple **class** inheritance; many **interfaces** |
| Constructor return type | ⭐ **None at all** |
| Constructor can be | Overloaded (not static, not virtual) |
| Destructor should be | Virtual, if deleting via a base pointer |
| Shallow copy copies | The **pointer** (shared buffer) |
| C++ non-overloadable operators | `::` `.` `.*` `?:` `sizeof` |
| Default access: class / struct | private / public |
| `new` vs `malloc` | `new` calls the **constructor**, is typed |
| C++ reference | Must be initialised; cannot be reseated |
| Pure virtual makes the class | **Abstract** |
| JVM executes | **Bytecode** |
| JDK ⊃ JRE ⊃ | JVM |
| Java lacks | Pointers, `goto`, operator overloading, multiple class inheritance, destructors |
| Java `private` | **Same class only** |
| `final` / `finally` / `finalize` | Modifier / always-runs block / GC hook (deprecated) |
| Java `String` | **Immutable** |
| `StringBuffer` vs `StringBuilder` | Synchronised / faster |
| `==` vs `.equals()` | Reference / content |
| Interface variables are | `public static final` |
| Multiple interfaces | ✅ Allowed |
| Checked exception | ⭐ **Must be caught or declared** |
| `NullPointerException` | **Unchecked** |
| `throw` vs `throws` | Statement / signature clause |
| Java `char` size | **2 bytes** (Unicode) |
| `Map` extends `Collection`? | ⭐ **No** |
| Preferred thread approach | Implement `Runnable` |
| `System.gc()` | Only a **request** |

---

# 9. ⚠ Common traps

1. ⭐ **`sizeof(array)/sizeof(array[0])` fails inside a function** — the array decayed to a pointer.
2. ⭐ **`malloc` does not zero memory; `calloc` does.**
3. **Pointer arithmetic scales by element size** — `p+3` is not "+3 bytes".
4. **Dangling ≠ wild ≠ null** — know all three definitions.
5. ⭐ **C has no call by reference** — only call by value, possibly of a pointer.
6. ⭐ **`final` / `finally` / `finalize` are three unrelated things.**
7. ⭐ **`String` is immutable; `==` compares references, `.equals()` compares content.**
8. ⭐ **Java is call by value even for objects** — you can mutate the object but not reassign the caller's reference.
9. ⭐ **Overloading needs different parameters** — a differing return type alone is a compile error.
10. ⭐ **`Map` is not a `Collection`.**
11. ⭐ **Constructors have no return type** — writing `void` makes it an ordinary method.
12. ⭐ **Java `char` is 2 bytes; C `char` is 1.**
13. **Constructors cannot be virtual; destructors can and often should be.**
14. **Encapsulation hides data; abstraction hides implementation.**
15. **`static` methods cannot use `this`.**
16. **Struct size ≠ sum of member sizes, because of padding.**
17. **Integer division truncates** — `10/3` is 3, and `-7/2` is −3 (toward zero).
18. **Mixing signed and unsigned promotes to unsigned** — `-1 < 1U` is false.

---

# 10. Practice

- GATE: [`Paper2_S05_Data_Structures_and_Programming/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — see `GATE_PYQ_Programming_-_Programming_in_C.pdf` (131 questions)
- ⭐ **State-PSC level:** [`Paper2_S05_.../`](../02_State_PSC_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — **578 questions including dedicated Java and OOP sets.** These match this exam's style far better than GATE's C-tracing puzzles.
- Also: `02_State_PSC_PYQs/Papers/Other_State_PSCs/Arunachal_Pradesh_PSC/APPSC_2021_AssistantSystemManager_PracticalProgramming_and_WebDesign.pdf`
- Test: [`Week_03_Test.md`](../04_Mock_Tests/Week_03_Test.md)

**Priority order if short on time:** the four OOP pillars & polymorphism types → Java `final`/`finally`/`finalize`, String, access modifiers, checked vs unchecked exceptions → abstract class vs interface → pointers & 2-D array address calculation → storage classes (`static` especially) → recursion (Hanoi, Fibonacci) → struct vs union → C++ non-overloadable operators.
