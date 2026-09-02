# Week 3 — Programming in C, C++, Java & OOP

**Syllabus §5 (part):** Programming in C, C++, Java. Recursion.
**Estimated marks: ~7** (of the ~14 for Data Structures & Programming)

> ⭐ **Strategy note.** State-PSC papers ask far more **Java and OOP definitional** questions than GATE does, and far fewer pointer-tracing puzzles. Give Sections 5–7 of this file real weight.

---

## 1. C fundamentals

### 1.1 Data types and sizes (typical 64-bit Linux/Windows)

| Type | Bytes | Range |
|---|---|---|
| `char` | 1 | −128 to 127 (signed) / 0–255 (unsigned) |
| `short` | 2 | −32,768 to 32,767 |
| `int` | 4 | −2³¹ to 2³¹ − 1 |
| `long` | 4 (Win) / 8 (Linux) | |
| `long long` | 8 | |
| `float` | 4 | ~6–7 significant digits |
| `double` | 8 | ~15–16 significant digits |
| `void` | — | No value |

⚠ Sizes are **implementation-defined**. The guarantees are: `char` ≤ `short` ≤ `int` ≤ `long` ≤ `long long`, and `sizeof(char)` = 1 **by definition**.

### 1.2 ⭐ Storage classes

| Class | Storage | Scope | Lifetime | Default value |
|---|---|---|---|---|
| ⭐ **`auto`** | Stack | Block | Block (until it exits) | Garbage |
| **`register`** | Register (hint) | Block | Block | Garbage |
| ⭐ **`static`** (local) | Data segment | **Block** | ⭐ **Whole program** | **0** |
| **`static`** (global/function) | Data segment | **File only** (internal linkage) | Whole program | 0 |
| ⭐ **`extern`** | Data segment | Global (across files) | Whole program | 0 |

⭐ **`auto` is the default for local variables.**
⭐ **A `static` local variable retains its value between calls** and is initialised only once.
⚠ `static` means two different things: *lifetime* for locals, *linkage restriction* for globals and functions.

```c
void f() { static int c = 0; c++; printf("%d ", c); }
// f(); f(); f();  →  1 2 3
```

### 1.3 ⭐ Operator precedence (high → low)

| Level | Operators | Associativity |
|---|---|---|
| 1 | `()` `[]` `->` `.` `++`/`--` (postfix) | Left → Right |
| 2 | `!` `~` `++`/`--` (prefix) `+`/`−` (unary) `*` `&` `sizeof` `(type)` | **Right → Left** |
| 3 | `*` `/` `%` | Left → Right |
| 4 | `+` `−` | Left → Right |
| 5 | `<<` `>>` | Left → Right |
| 6 | `<` `<=` `>` `>=` | Left → Right |
| 7 | `==` `!=` | Left → Right |
| 8–12 | `&` then `^` then `|` then `&&` then `||` | Left → Right |
| 13 | `?:` | **Right → Left** |
| 14 | `=` `+=` `−=` … | **Right → Left** |
| 15 | `,` | Left → Right |

🔢 `int a=10, b=3; a/b*b + a%b` → `/` and `*` are equal precedence, left-associative: (10/3)×3 = 3×3 = 9; 10%3 = 1 → **10**.
⚠ Integer division truncates toward zero — this is why the answer is 10 and not simply `a`.

⚠ **Undefined behaviour:** expressions like `i++ + ++i` or `a[i] = i++` modify a variable twice without an intervening sequence point. Well-written exams avoid these; if you see one, the intended answer is usually "undefined".

### 1.4 Type conversion
**Implicit promotion order:** `char`/`short` → `int` → `unsigned int` → `long` → `unsigned long` → `float` → `double` → `long double`.
⚠ Mixing signed and unsigned promotes to **unsigned** — `if (-1 < 1U)` is **false**.

---

## 2. ⭐ Pointers

### 2.1 Basics
```c
int x = 10;
int *p = &x;    // p holds the address of x
*p = 20;        // x is now 20
int **pp = &p;  // pointer to pointer
```

- `&` = address-of; `*` = dereference.
- A pointer's **size is the same for all types** (8 bytes on 64-bit) — it stores an address.

### 2.2 ⭐ Pointer arithmetic
📌 **`p + n` advances by `n × sizeof(*p)` bytes.**

🔢 `int *p` with `sizeof(int)` = 4: after `p = p + 3`, the address increases by **12 bytes**.
📌 `p2 − p1` (same array) = number of **elements** between them, not bytes.

Valid operations: `+ int`, `− int`, `−` between pointers, comparison. Invalid: `+` between two pointers, `*`, `/`.

### 2.3 ⭐ Arrays vs pointers

| | Array `int a[5]` | Pointer `int *p` |
|---|---|---|
| `sizeof` | 20 (whole array) | 8 (the pointer) |
| Reassignable | ❌ No | ✅ Yes |
| Memory | Contiguous block allocated | Just an address |

⭐ **Array decay:** an array name used in an expression decays to a pointer to its first element — **except** with `sizeof` and `&`.

🔢 `int arr[5]; sizeof(arr)/sizeof(arr[0])` = 20/4 = **5**.
⚠ **This idiom breaks inside a function**, because the parameter is a pointer: `void f(int a[])` → `sizeof(a)` = 8, giving 2, not 5. A classic trap.

**Equivalences:** `a[i]` ≡ `*(a+i)` ≡ `*(i+a)` ≡ `i[a]` (yes, the last one is legal C).

### 2.4 ⭐ 2-D array address calculation

📌 **Row-major** (C, C++, Java): elements of a row are contiguous.
**Address of A[i][j] = Base + [ (i − L₁) × N_cols + (j − L₂) ] × size**

📌 **Column-major** (FORTRAN, MATLAB): elements of a column are contiguous.
**Address of A[i][j] = Base + [ (j − L₂) × N_rows + (i − L₁) ] × size**

🔢 `int A[10][20]`, base = 1000, 4 bytes/element, row-major, 0-based:
Address of `A[3][5]` = 1000 + (3 × 20 + 5) × 4 = 1000 + 65 × 4 = **1260**.

⚠ Watch for **1-based lower bounds** — subtract them, as in the formula.

### 2.5 Special pointers

| Pointer | Meaning |
|---|---|
| **NULL pointer** | Points to nothing, by design. Dereferencing → crash. |
| ⭐ **Dangling pointer** | Points to memory that has been **freed** or gone out of scope |
| **Wild pointer** | **Uninitialised** — contains garbage |
| **Void pointer** | Generic; must be cast before dereferencing. `malloc` returns `void*`. |
| **Function pointer** | Holds a function's address: `int (*fp)(int, int) = &add;` |

### 2.6 ⭐ Dynamic memory (`<stdlib.h>`)

| Function | Behaviour |
|---|---|
| `malloc(size)` | Allocates `size` bytes; ⭐ **uninitialised** (garbage) |
| ⭐ `calloc(n, size)` | Allocates n × size bytes; ⭐ **zero-initialised** |
| `realloc(p, newsize)` | Resizes an existing block; may move it |
| `free(p)` | Releases the block |

All allocate on the **heap**; all return `void*`; all return **`NULL` on failure**.

⚠ **Memory leak:** allocated but never freed. **Double free** and **use-after-free** are undefined behaviour. Set `p = NULL` after `free(p)` to avoid dangling pointers.

**Stack vs heap:**

| | Stack | Heap |
|---|---|---|
| Allocation | Automatic (compiler) | Manual (`malloc`/`new`) |
| Speed | Fast | Slower |
| Size | Limited (overflow on deep recursion) | Large |
| Lifetime | Until the block exits | Until explicitly freed |

---

## 3. Functions and recursion

### 3.1 ⭐ Parameter passing

| Mechanism | Semantics | In C? |
|---|---|---|
| ⭐ **Call by value** | A **copy** is passed; caller's variable unchanged | ✅ The only mechanism in C |
| **Call by reference** | The variable itself is passed; changes are visible | ❌ Not in C; ✅ C++ (`int &x`), Java (for objects, references passed by value) |
| Call by address/pointer | Pass `&x`, function dereferences | ✅ C's way of simulating reference semantics |
| Call by name | Argument expression re-evaluated at each use | Algol; theoretical |
| Call by value-result (copy-restore) | Copy in, copy back on return | Ada |

⭐ **A C `swap(int a, int b)` cannot swap the caller's variables** — it swaps its own copies. You must write `swap(int *a, int *b)`.

⚠ **Java is always call by value** — but for objects the *reference value* is copied, so the method can mutate the object while being unable to reassign the caller's variable.

### 3.2 ⭐ Recursion

A function that calls itself. Requires a **base case** and progress toward it.

```c
int fib(int n) {
    if (n <= 1) return n;          // base case
    return fib(n-1) + fib(n-2);    // recursive case
}
```
🔢 fib: 0, 1, 1, 2, 3, 5, 8, 13 → **fib(5) = 5**.

| Recursion type | Description |
|---|---|
| **Direct** | f calls f |
| **Indirect** | f calls g, g calls f |
| ⭐ **Tail recursion** | The recursive call is the **last** operation; compilers can optimise it into a loop |
| **Tree recursion** | More than one recursive call per invocation (e.g. naïve fib) |

**Costs:** each call pushes an **activation record** (stack frame) with parameters, locals, return address. Deep recursion → **stack overflow**.

📌 Naïve `fib(n)` makes **exponential** O(2ⁿ) calls; with memoisation it becomes O(n).
📌 Number of calls in naïve fib(n) = 2·F(n+1) − 1.

**Classic recursions to know:**
- Factorial: `n! = n × (n−1)!`, base 0! = 1
- ⭐ **Towers of Hanoi:** 📌 minimum moves = **2ⁿ − 1**; recurrence T(n) = 2T(n−1) + 1
- GCD (Euclid): `gcd(a,b) = gcd(b, a%b)`
- Ackermann function (deeply recursive, not primitive recursive)

---

## 4. Structures, unions, files

### 4.1 Structure vs union ⭐

| | **`struct`** | **`union`** |
|---|---|---|
| Memory | Sum of all members (+ padding) | ⭐ **Size of the largest member** |
| Members active | All simultaneously | ⭐ **One at a time** (they share memory) |
| Use | Records | Memory-saving, type punning |

🔢 `struct {char c; int i;}` on a 4-byte-aligned machine → 8 bytes (1 + 3 padding + 4).
🔢 `union {char c; int i;}` → **4 bytes**.

**Structure padding/alignment:** compilers insert padding so each member sits at an address that is a multiple of its size. This is why `sizeof(struct)` may exceed the sum of member sizes.

**Bit-fields:** `struct { unsigned a : 3; unsigned b : 5; };` packs members into specified bit widths.

**Access:** `s.member` for a struct variable; `p->member` (≡ `(*p).member`) via a pointer.

### 4.2 File handling
`fopen` (modes `r`, `w`, `a`, `r+`, `w+`, `a+`, add `b` for binary) · `fclose` · `fscanf`/`fprintf` · `fgets`/`fputs` · `fread`/`fwrite` · `fseek`/`ftell`/`rewind` · `feof`.
⚠ `"w"` **truncates** an existing file; `"a"` appends.

### 4.3 Preprocessor
`#include` · `#define` (macros — textual substitution, no type checking; always parenthesise arguments) · `#ifdef`/`#ifndef`/`#endif` (include guards) · `#pragma`.
⚠ Macro vs function: macros are expanded inline with no type checking and can double-evaluate arguments — `#define SQ(x) ((x)*(x))` with `SQ(i++)` increments twice.

---

## 5. ⭐ Object-Oriented Programming concepts

### 5.1 The four pillars ⭐

| Pillar | Definition | Key point |
|---|---|---|
| ⭐ **Encapsulation** | Bundling data with the methods that operate on it, and restricting direct access | The *mechanism*: `private` members + `public` getters/setters |
| ⭐ **Abstraction** | Exposing only essential features, hiding implementation detail | The *goal*: abstract classes, interfaces |
| ⭐ **Inheritance** | A class acquires the properties and behaviour of another | Enables **reuse**; "is-a" relationship |
| ⭐ **Polymorphism** | One interface, many implementations | "Many forms" |

⚠ **Encapsulation vs abstraction** is a favourite distinction: encapsulation *hides data*, abstraction *hides complexity/implementation*.

Other core terms: **class** (blueprint) · **object** (instance) · **message passing** · **composition** ("has-a", generally preferred over inheritance).

### 5.2 ⭐ Types of inheritance

| Type | Structure |
|---|---|
| **Single** | B ← A |
| **Multiple** | C ← A **and** B (⚠ not for classes in Java) |
| **Multilevel** | C ← B ← A |
| **Hierarchical** | B and C both ← A |
| **Hybrid** | Combination of the above |

⭐ **The diamond problem:** with multiple inheritance, if B and C both inherit from A and D inherits from both, an A-member reached via B or C is ambiguous.
- **C++ solution:** *virtual* inheritance (`class B : virtual public A`).
- ⭐ **Java solution:** forbid multiple inheritance of **classes**; allow multiple **interfaces**.

### 5.3 ⭐⭐ Polymorphism

| | **Compile-time (static)** | **Run-time (dynamic)** |
|---|---|---|
| Achieved by | ⭐ **Function/method overloading**, operator overloading | ⭐ **Function overriding**, virtual functions |
| Bound at | Compile time (early binding) | Run time (late binding) |
| Mechanism | Signature matching | **vtable / vptr** lookup |

⭐ **Overloading vs overriding:**

| | **Overloading** | **Overriding** |
|---|---|---|
| Where | Same class (or across classes) | Base class and derived class |
| Signature | **Must differ** (parameter list) | **Must be identical** |
| Return type alone can differ? | ❌ No — not sufficient | Covariant return allowed |
| Binding | Compile time | Run time |
| Java keyword | — | `@Override` |

**Virtual functions (C++):** declared `virtual` in the base class; the call is resolved through the object's **vtable** at run time.
- A **pure virtual function** (`virtual void f() = 0;`) makes the class **abstract** — it cannot be instantiated.
- ⭐ A **virtual destructor** is required when deleting a derived object through a base pointer, otherwise the derived destructor is not called.
- ⚠ **Constructors can never be virtual**; destructors can and often should be.

### 5.4 Constructors and destructors

⭐ **Constructor:** same name as the class, **no return type at all** (not even `void`), called automatically on object creation. Can be **overloaded**. Cannot be `static` or `virtual`.

| Type | Purpose |
|---|---|
| Default | No parameters |
| Parameterised | Takes arguments |
| ⭐ **Copy constructor** | `Class(const Class &obj)` — initialises from another object |

**Destructor (C++):** `~Class()`, no parameters, no return type, cannot be overloaded; called when the object is destroyed.

**Shallow vs deep copy:** a shallow copy duplicates pointer values (two objects share memory → double free); a deep copy duplicates the pointed-to data.

### 5.5 C++ specifics

⭐ **Operators that CANNOT be overloaded:**
📌 **`::` (scope resolution) · `.` (member access) · `.*` (pointer-to-member) · `?:` (ternary) · `sizeof`**
(also `typeid` and the cast operators). Everything else — including `+`, `[]`, `()`, `<<`, `new`, `delete` — can be.

**Access specifiers:** `private` (class only) · `protected` (class + derived) · `public` (anywhere).
Default access: `class` → **private**; `struct` → **public**.

**Other C++ features:** `friend` functions/classes (granted access to private members, breaking encapsulation deliberately) · templates (generic programming) · `new`/`delete` (type-aware, call constructors/destructors — unlike `malloc`/`free`) · references (`int &r = x;` — must be initialised, cannot be reseated) · STL (vector, list, map, set, stack, queue) · exception handling (`try`/`catch`/`throw`) · namespaces.

⚠ `new`/`delete` vs `malloc`/`free`: `new` calls the constructor and returns a typed pointer; `malloc` does neither.

---

## 6. ⭐ Java

### 6.1 Platform architecture

⭐ **Source (.java) → `javac` → bytecode (.class) → JVM interprets/JIT-compiles → machine code**

| Term | Meaning |
|---|---|
| ⭐ **JVM** | Java Virtual Machine — **executes bytecode**; platform-specific |
| **JRE** | JVM + standard libraries — enough to *run* Java |
| **JDK** | JRE + compiler and dev tools — needed to *develop* |
| **JIT** | Just-In-Time compiler inside the JVM; compiles hot bytecode to native code |

⭐ **"Write once, run anywhere"** comes from bytecode being platform-independent while the JVM is platform-specific.

### 6.2 ⭐ Features Java does NOT have

📌 **No explicit pointers/pointer arithmetic · No `goto` (reserved but unused) · No operator overloading · No multiple inheritance of classes · No destructors · No `struct`/`union` · No global variables**

⭐ Java **does** have: automatic **garbage collection**, multithreading, interfaces, exception handling, packages, platform independence, security (bytecode verifier, sandbox).

### 6.3 ⭐ Access modifiers

| Modifier | Same class | Same package | Subclass (other package) | Anywhere |
|---|---|---|---|---|
| ⭐ **`private`** | ✅ | ❌ | ❌ | ❌ |
| **default** (no modifier) | ✅ | ✅ | ❌ | ❌ |
| **`protected`** | ✅ | ✅ | ✅ | ❌ |
| **`public`** | ✅ | ✅ | ✅ | ✅ |

### 6.4 ⭐⭐ `final` vs `finally` vs `finalize`

| Keyword | What it is | Meaning |
|---|---|---|
| ⭐ **`final`** | **Modifier** | `final` variable = constant; `final` method = cannot be overridden; `final` class = cannot be extended |
| ⭐ **`finally`** | **Block** | ⭐ **Always executes**, whether or not an exception is thrown (used for cleanup) |
| ⭐ **`finalize()`** | **Method** | Called by the garbage collector before reclaiming an object; **deprecated**, unreliable |

⚠ This three-way distinction is one of the most frequently asked Java questions in state-PSC papers.

### 6.5 ⭐ Strings

| Class | Mutable? | Thread-safe? |
|---|---|---|
| ⭐ **`String`** | ❌ **Immutable** | Yes (by immutability) |
| **`StringBuffer`** | ✅ Mutable | ✅ **Synchronised** |
| **`StringBuilder`** | ✅ Mutable | ❌ Not synchronised (**faster**) |

⭐ Every "modification" of a `String` creates a **new object**. The **string constant pool** interns literals, so `"abc" == "abc"` is true for literals but `new String("abc") == "abc"` is **false**.
⚠ Use `.equals()` to compare string **contents**; `==` compares **references**.

### 6.6 ⭐ Abstract class vs interface

| | **Abstract class** | **Interface** |
|---|---|---|
| Instantiable | ❌ | ❌ |
| Methods | Abstract **and** concrete | Abstract (plus `default`/`static` since Java 8) |
| Variables | Any | Implicitly `public static final` (constants) |
| Constructor | ✅ Yes | ❌ No |
| Multiple inheritance | ❌ One superclass only | ⭐ **✅ A class can implement many** |
| Keyword | `extends` | `implements` |
| Use when | Classes share code and an "is-a" relation | Unrelated classes share a **contract** |

### 6.7 ⭐ Exception handling

```
Throwable
├── Error            (JVM problems — OutOfMemoryError, StackOverflowError; do not catch)
└── Exception
    ├── RuntimeException  → ⭐ UNCHECKED (NullPointerException,
    │                        ArrayIndexOutOfBoundsException, ArithmeticException,
    │                        ClassCastException, NumberFormatException)
    └── others            → ⭐ CHECKED (IOException, SQLException,
                             ClassNotFoundException, FileNotFoundException)
```

⭐ **Checked** exceptions must be caught or declared with `throws` — **compiler enforced**.
⭐ **Unchecked** (RuntimeException and Error) need not be declared.

Keywords: `try` · `catch` · `finally` · `throw` (throws one instance) · `throws` (declares in the signature).
⚠ `throw` vs `throws` — singular statement vs method declaration clause.

### 6.8 Other Java essentials
- **`static`:** belongs to the class, not an instance. `static` methods cannot use `this` or access instance members directly. `static` blocks run once at class loading.
- **`this`** (current object) and **`super`** (parent class).
- **Garbage collection:** automatic; `System.gc()` is only a *request*. Objects become eligible when unreachable. Mark-and-sweep, generational collection.
- **Wrapper classes:** `int`→`Integer`, `char`→`Character`, etc. **Autoboxing/unboxing** converts automatically.
- **8 primitive types:** `byte`(1), `short`(2), `int`(4), `long`(8), `float`(4), `double`(8), `char`(2, **Unicode**), `boolean`.
  ⚠ Java's `char` is **2 bytes** (Unicode), unlike C's 1 byte.
- **Java sizes are fixed** across all platforms — unlike C.
- **Collections:** `List` (ArrayList, LinkedList) · `Set` (HashSet, TreeSet) · `Map` (HashMap, TreeMap) · `Queue`.
  ⚠ `Map` does **not** extend `Collection`.
- **Threads:** extend `Thread` or implement `Runnable` (preferred, since Java allows only one superclass). States: New → Runnable → Running → Blocked/Waiting → Terminated. `synchronized` for mutual exclusion.
- **`main` signature:** `public static void main(String[] args)`.

---

## 7. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| Default storage class (local) | `auto` |
| `static` local | Retains value between calls; initialised once |
| `p = p + 3` for `int *p` | Address += 12 bytes |
| `sizeof(arr)/sizeof(arr[0])` | Number of elements (fails after decay) |
| Row-major A[i][j] | Base + (i×ncols + j) × size |
| `malloc` vs `calloc` | calloc zero-initialises |
| Freed-then-used pointer | Dangling |
| Uninitialised pointer | Wild |
| C parameter passing | Call by value only |
| Towers of Hanoi moves | 2ⁿ − 1 |
| Naïve fib(n) complexity | O(2ⁿ) |
| `union` size | Largest member |
| Operators not overloadable in C++ | `::` `.` `.*` `?:` `sizeof` |
| Default access in `class` / `struct` | private / public |
| Compile-time polymorphism | Overloading |
| Run-time polymorphism | Overriding + virtual functions |
| Constructor return type | None at all |
| Virtual constructor | Not allowed |
| JVM executes | Bytecode |
| Java multiple inheritance of classes | Not supported (diamond problem) |
| `finally` | Always executes |
| `finalize()` | Called by GC; deprecated |
| Java `String` | Immutable |
| `StringBuilder` vs `StringBuffer` | Not synchronised / synchronised |
| Java `private` | Same class only |
| Checked exception | Must be caught or declared |
| `NullPointerException` | Unchecked |
| Java `char` size | 2 bytes (Unicode) |
| Interface variables | `public static final` |

---

## 8. Common traps ⚠

1. **`sizeof(array)/sizeof(array[0])` fails inside a function** — the array has decayed to a pointer.
2. **`malloc` does not zero memory**; `calloc` does.
3. **1's/2's complement style confusion in C:** integer division truncates; `-7/2` is `-3`, not `-4`.
4. **Dangling ≠ wild ≠ null.**
5. **C has no call by reference** — only call by value (possibly of a pointer).
6. **`final` / `finally` / `finalize`** are three unrelated things.
7. **`String` is immutable**; `==` compares references, `.equals()` compares content.
8. **Java is call by value even for objects** — you can mutate the object, not reassign the caller's reference.
9. **Overloading needs different parameters** — differing return type alone is a compile error.
10. **`Map` is not a `Collection`.**
11. **Constructors have no return type** — writing `void` makes it an ordinary method.
12. **Java `char` is 2 bytes**, C `char` is 1.

---

## 9. Practice

- GATE: [`Paper2_S05_Data_Structures_and_Programming/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — see `GATE_PYQ_Programming_-_Programming_in_C.pdf` (131 questions)
- ⭐ State-PSC level: [`Paper2_S05_.../`](../02_State_PSC_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/) — **578 questions including dedicated Java and OOP sets.** These match the exam's style far better than GATE's C-tracing puzzles.
- Also: `02_State_PSC_PYQs/Papers/Other_State_PSCs/Arunachal_Pradesh_PSC/APPSC_2021_AssistantSystemManager_PracticalProgramming_and_WebDesign.pdf`
- Test: [`Week_03_Test.md`](../04_Mock_Tests/Week_03_Test.md)

**Priority order if short on time:** OOP four pillars & polymorphism → Java `final`/`finally`/`finalize`, String, access modifiers, exceptions → pointers & array address calculation → storage classes → recursion → structures/unions.
