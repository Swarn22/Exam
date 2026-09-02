# Week 3 Mock Test — Programming in C, C++, Java & OOP

**Syllabus §5 (part)** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — Programming & OOP (Q1–Q20)

**Q1.** The default storage class for a variable declared inside a function in C is
(A) `static`  (B) `extern`  (C) `auto`  (D) `register`

**Q2.** A `static` local variable inside a C function
(A) is destroyed when the function returns
(B) retains its value between successive calls to the function
(C) is visible to all other files in the program
(D) must be initialised on every call

**Q3.** Consider `int arr[5];` on a machine where `sizeof(int)` is 4. The value of `sizeof(arr)/sizeof(arr[0])` is
(A) 4  (B) 5  (C) 20  (D) 1

**Q4.** An integer array is declared as `int A[10][20];` and stored in **row-major** order. The base address of `A[0][0]` is 1000 and each element occupies 4 bytes. The address of `A[3][5]` is
(A) 1140  (B) 1260  (C) 1220  (D) 1300

**Q5.** What does the following function return for `f(5)`?
```c
int f(int n) {
    if (n <= 1) return n;
    return f(n-1) + f(n-2);
}
```
(A) 3  (B) 5  (C) 8  (D) 120

**Q6.** What is the output of the following?
```c
int a = 10, b = 3;
printf("%d", a/b*b + a%b);
```
(A) 9  (B) 10  (C) 11  (D) 13

**Q7.** A function in C that attempts to swap two integers using **call by value**
(A) swaps them successfully
(B) does not affect the caller's variables
(C) causes a compilation error
(D) swaps them only if they are global

**Q8.** Which statement about `malloc()` and `calloc()` is correct?
(A) `malloc()` initialises the allocated memory to zero, `calloc()` does not
(B) `calloc()` initialises the allocated memory to zero, `malloc()` does not
(C) Both initialise memory to zero
(D) Neither can return `NULL`

**Q9.** A pointer that refers to a memory location which has already been freed is called a
(A) null pointer  (B) wild pointer  (C) dangling pointer  (D) void pointer

**Q10.** Which of the following operators **cannot** be overloaded in C++?
(A) `+`  (B) `[]`  (C) `::`  (D) `<<`

**Q11.** Run-time (dynamic) polymorphism in C++ is achieved through
(A) function overloading
(B) operator overloading
(C) virtual functions and function overriding
(D) templates

**Q12.** Function overloading is an example of
(A) compile-time polymorphism  (B) run-time polymorphism  (C) inheritance  (D) encapsulation

**Q13.** Wrapping data and the methods that operate on it into a single unit, while restricting direct access to some components, is called
(A) inheritance  (B) polymorphism  (C) encapsulation  (D) recursion

**Q14.** Which of the following is **not** supported in Java?
(A) Explicit pointer arithmetic
(B) Multithreading
(C) Interfaces
(D) Garbage collection

**Q15.** In Java, which class of `String` objects is correct?
(A) `String` objects are mutable
(B) `String` objects are immutable; `StringBuffer` is mutable
(C) Both `String` and `StringBuffer` are immutable
(D) `StringBuffer` is immutable; `String` is mutable

**Q16.** In Java, the block that executes whether or not an exception is thrown is
(A) `final`  (B) `finalize`  (C) `finally`  (D) `catch`

**Q17.** The Java Virtual Machine executes
(A) source code directly  (B) machine code  (C) bytecode  (D) assembly code

**Q18.** A member declared `private` in a Java class is accessible
(A) only within the same class
(B) within the same package
(C) within the same package and subclasses
(D) from anywhere

**Q19.** Which statement about a constructor is correct?
(A) It has the same name as the class and no return type
(B) It must return `void`
(C) It can be declared `static`
(D) It cannot be overloaded

**Q20.** Java does **not** support multiple inheritance of classes primarily to avoid
(A) the diamond (ambiguity) problem
(B) memory leaks
(C) stack overflow
(D) type casting errors

---

## Part B — Paper-I (Q21–Q25)

**Q21.** The idiom *"to let the cat out of the bag"* means
(A) to release an animal  (B) to reveal a secret  (C) to create confusion  (D) to escape danger

**Q22.** Choose the word most nearly similar in meaning to **METICULOUS**.
(A) Careless  (B) Extremely careful and precise  (C) Hasty  (D) Doubtful

**Q23.** A man walks 5 km towards the north, then turns right and walks 3 km, then turns right again and walks 5 km. How far is he from his starting point?
(A) 3 km  (B) 5 km  (C) 8 km  (D) 13 km

**Q24.** The average of 5 consecutive odd numbers is 27. The largest of these numbers is
(A) 29  (B) 31  (C) 33  (D) 35

**Q25.** Kokborok, one of the official languages of Tripura, belongs to which language family?
(A) Indo-Aryan  (B) Dravidian  (C) Tibeto-Burman  (D) Austroasiatic

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | C | 6 | B | 11 | C | 16 | C | 21 | B |
| 2 | B | 7 | B | 12 | A | 17 | C | 22 | B |
| 3 | B | 8 | B | 13 | C | 18 | A | 23 | A |
| 4 | B | 9 | C | 14 | A | 19 | A | 24 | B |
| 5 | B | 10 | C | 15 | B | 20 | A | 25 | C |

---

**Q1 — (C).** Local variables are `auto` by default (automatic storage duration, block scope). The keyword is almost never written explicitly.

**Q2 — (B).** `static` gives the variable *static storage duration* (it lives for the whole program) while keeping its *block scope*. It is initialised only once.

**Q3 — (B).** `sizeof(arr)` = 5 × 4 = 20; `sizeof(arr[0])` = 4; 20/4 = **5**. Note this idiom fails if `arr` has decayed to a pointer inside a function — a favourite trap.

**Q4 — (B).** Row-major: address = base + (i × ncols + j) × size = 1000 + (3 × 20 + 5) × 4 = 1000 + 65 × 4 = **1260**.

**Q5 — (B).** This is Fibonacci: f(0)=0, f(1)=1, f(2)=1, f(3)=2, f(4)=3, **f(5)=5**.

**Q6 — (B).** `/` and `*` are left-associative and equal precedence: `a/b*b` = (10/3)×3 = 3×3 = 9 (integer division truncates). `a%b` = 1. Total = **10**. Note 9 ≠ 10 because integer division loses the remainder — that is the whole point of the question.

**Q7 — (B).** Call by value copies the arguments; the function swaps its own copies. C has no call by reference — you must pass pointers explicitly.

**Q8 — (B).** `calloc(n, size)` zero-initialises; `malloc(size)` leaves the memory uninitialised. Both return `NULL` on failure, and both return `void*`.

**Q9 — (C).** A **dangling** pointer points to freed or out-of-scope memory. A *wild* pointer is one that was never initialised; a *null* pointer points to nothing by design.

**Q10 — (C).** The five operators that cannot be overloaded in C++ are `::` (scope resolution), `.` (member access), `.*`, `?:` and `sizeof`.

**Q11 — (C).** Run-time polymorphism requires a virtual function resolved through the vtable at execution time. Overloading and templates are resolved at compile time.

**Q12 — (A).** Overloading is resolved by the compiler from the argument signature — compile-time (static) polymorphism. Overriding is the run-time counterpart.

**Q13 — (C).** Encapsulation = bundling data with methods + access control. Abstraction (hiding *implementation detail*) is related but distinct; encapsulation is the mechanism, abstraction the goal.

**Q14 — (A).** Java deliberately omits explicit pointer arithmetic for safety. It has references, but you cannot do address arithmetic on them.

**Q15 — (B).** `String` is immutable (every "modification" creates a new object); `StringBuffer` (thread-safe) and `StringBuilder` (faster, not synchronised) are mutable.

**Q16 — (C).** `finally` always runs. Do not confuse it with `final` (a modifier preventing inheritance/reassignment/overriding) or `finalize()` (a deprecated pre-GC hook). Distinguishing these three is a standard exam question.

**Q17 — (C).** `javac` compiles source to platform-independent **bytecode**; the JVM interprets or JIT-compiles it. This is what "write once, run anywhere" means.

**Q18 — (A).** `private` = same class only. `default` (no modifier) = same package; `protected` = same package + subclasses; `public` = anywhere.

**Q19 — (A).** A constructor shares the class name and has **no return type at all** (not even `void`). It can be overloaded, and it cannot be `static`.

**Q20 — (A).** With multiple inheritance of classes, an inherited member reachable by two paths is ambiguous — the diamond problem. Java allows multiple *interface* inheritance instead, since interfaces traditionally carried no state.

**Q21 — (B).** *Let the cat out of the bag* = disclose a secret, usually accidentally.

**Q22 — (B).** *Meticulous* = showing great attention to detail; very careful and precise.

**Q23 — (A).** North 5 km, right (east) 3 km, right again (south) 5 km. The two 5 km legs cancel, leaving him **3 km** due east of the start, facing south.

**Q24 — (B).** For an odd count of consecutive numbers the average is the middle term, so the middle number is 27. The five are 23, 25, 27, 29, **31**.

**Q25 — (C).** Kokborok (Tripuri) is a **Tibeto-Burman** language of the Sino-Tibetan family, and is an official language of Tripura alongside Bengali and English.

---

## Score

| | |
|---|---|
| Part A (Programming & OOP) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** missed Q3/Q4/Q7/Q8/Q9 → redo pointers, arrays and dynamic memory (the densest C topic); missed Q10–Q13 → redo OOP concepts; missed Q14–Q20 → redo Java fundamentals. **Java and OOP definitional questions are far more common in state-PSC papers than in GATE** — drill `02_State_PSC_PYQs/Subject_wise/Paper2_S05_Data_Structures_and_Programming/` (578 questions, including dedicated Java and OOP sets).
