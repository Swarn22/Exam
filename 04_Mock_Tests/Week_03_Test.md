# Week 3 Question Bank — Programming (C, C++, Java) & OOP

**Syllabus §5 (part)** · 190 questions · Practice set · +1 / −0.33 marking

> Grounded in `05_Notes/Week_03_Programming_C_CPP_Java_OOP.md`. Standard C/C++/Java semantics; undefined-behaviour items are flagged and their answer is "undefined". Use this as a drill bank, not a timed paper.

---

## Part A — C data types, sizes & storage classes

**Q1.** The default storage class for a variable declared inside a function in C is
(A) `static`  (B) `extern`  (C) `auto`  (D) `register`

**Q2.** A `static` local variable inside a C function
(A) is destroyed when the function returns
(B) retains its value between successive calls
(C) is visible to all other files in the program
(D) must be initialised on every call

**Q3.** Which of the following is guaranteed by the C standard to be exactly 1?
(A) `sizeof(char)`  (B) `sizeof(int)`  (C) `sizeof(short)`  (D) `sizeof(void)`

**Q4.** Which relationship does the C standard actually guarantee?
(A) `int` is always 4 bytes
(B) `sizeof(char)==1` and `char ≤ short ≤ int ≤ long ≤ long long`
(C) `long` is always 8 bytes
(D) `sizeof(int) == sizeof(long)` always

**Q5.** The C standard requires `int` to be at least
(A) 8 bits  (B) 16 bits  (C) 32 bits  (D) 64 bits

**Q6.** Declaring a **global** variable or function `static` in C
(A) makes it visible to all files
(B) restricts its visibility (linkage) to the file it is declared in
(C) gives it block scope
(D) allocates it on the stack

**Q7.** A `static` local variable that is not explicitly initialised defaults to
(A) garbage  (B) 0  (C) 1  (D) `NULL`

**Q8.** An `auto` (ordinary local) variable that is not initialised contains
(A) 0  (B) garbage / an indeterminate value  (C) `NULL`  (D) 1

**Q9.** The `register` storage class in C
(A) forces the variable into a CPU register
(B) is only a hint/request to store the variable in a CPU register
(C) stores the variable on the heap
(D) makes the variable global

**Q10.** Which storage class allows a variable defined in one file to be used in another?
(A) `static`  (B) `auto`  (C) `extern`  (D) `register`

**Q11.** In a running C program, uninitialised global variables are stored in the
(A) stack  (B) heap  (C) BSS segment  (D) text segment

**Q12.** The machine instructions (executable code) of a C program reside in the
(A) data segment  (B) BSS segment  (C) text (code) segment  (D) stack

**Q13.** In Java, the size of an `int`
(A) is implementation-defined
(B) is always 4 bytes on every platform
(C) is 2 bytes
(D) is 8 bytes

**Q14.** Which statement about a program's stack is correct?
(A) The heap stores local variables
(B) The stack stores local variables/parameters and typically grows toward lower addresses
(C) Global variables live on the stack
(D) The stack always grows upward toward higher addresses

**Q15.** What is the output?
```c
void counter() { static int c = 0; c++; printf("%d ", c); }
int main() { counter(); counter(); counter(); }
```
(A) `0 1 2`  (B) `1 1 1`  (C) `1 2 3`  (D) `3 3 3`

---

## Part B — Operators, precedence & type conversion

**Q16.** In C, the expression `a + b * c` is evaluated as
(A) `(a+b)*c`  (B) `a+(b*c)`  (C) left to right regardless  (D) undefined

**Q17.** The associativity of the assignment operator `=` is
(A) left to right  (B) right to left  (C) none  (D) depends on the compiler

**Q18.** Which group of operators is **right**-associative?
(A) `+` and `−`  (B) `*` and `/`  (C) unary, ternary `?:`, and assignment  (D) relational operators

**Q19.** The expression `x & MASK == 0` is parsed as
(A) `(x & MASK) == 0`  (B) `x & (MASK == 0)`  (C) a compile error  (D) `((x & MASK) == 0)` with a warning

**Q20.** What is the output?
```c
int a = 10, b = 3;
printf("%d", a/b*b + a%b);
```
(A) 9  (B) 10  (C) 11  (D) 13

**Q21.** In C, the value of `10 / 3` (both `int`) is
(A) 3  (B) 3.33  (C) 4  (D) 0

**Q22.** In C, the value of `-7 / 2` (integer division) is
(A) −4  (B) −3  (C) −3.5  (D) 3

**Q23.** The condition `if (-1 < 1U)` evaluates to
(A) true  (B) false  (C) a compile error  (D) undefined

**Q24.** The value of `17 % 5` is
(A) 2  (B) 3  (C) 3.4  (D) 0

**Q25.** The ternary conditional operator `?:` is
(A) left-associative  (B) right-associative  (C) non-associative  (D) not an operator

**Q26.** Which operator has the **lowest** precedence in C?
(A) `=`  (B) `?:`  (C) `,` (comma)  (D) `||`

**Q27.** In an arithmetic expression, a `char` operand is first promoted to
(A) `short`  (B) `int`  (C) `unsigned char`  (D) `float`

**Q28.** In C, a character constant such as `'A'` has type
(A) `char`  (B) `int`  (C) `unsigned char`  (D) `short`

**Q29.** Which statement about C operator precedence is correct?
(A) `==` has higher precedence than `&`
(B) `&` has higher precedence than `==`
(C) they have equal precedence
(D) `&&` has higher precedence than `==`

**Q30.** What is the value of `x` after `int x = 5; x = x++ + ++x;`?
(A) 11  (B) 12  (C) 10  (D) Undefined behaviour

---

## Part C — Pointers & pointer arithmetic

**Q31.** The `&` operator applied to a variable yields
(A) its value  (B) its address  (C) its size  (D) its type

**Q32.** If `int *p = &x;`, then `*p` gives
(A) the address of `x`  (B) the value of `x`  (C) the address of `p`  (D) the size of `x`

**Q33.** An `int *p` (with `sizeof(int)==4`) currently holds address 1000. `p + 3` is
(A) 1003  (B) 1012  (C) 1006  (D) 1024

**Q34.** A `char *c` holds address 1000. `c + 3` is
(A) 1003  (B) 1012  (C) 1006  (D) 1004

**Q35.** A `double *d` (with `sizeof(double)==8`) holds address 2000. `d + 2` is
(A) 2002  (B) 2008  (C) 2016  (D) 2004

**Q36.** For `int *p1, *p2` with `p1 = 1000` and `p2 = 1020`, the value of `p2 - p1` is
(A) 20  (B) 5  (C) 4  (D) 10

**Q37.** On a 64-bit machine, which statement about pointer sizes is correct?
(A) `int*` is smaller than `double*`
(B) all pointer types have the same size (8 bytes)
(C) `char*` is 1 byte
(D) `double*` is 8 bytes but `int*` is 4 bytes

**Q38.** Which pointer operation is **illegal** in C?
(A) `pointer + integer`  (B) `pointer − pointer`  (C) `pointer + pointer`  (D) comparing two pointers

**Q39.** Given `int x = 10; int *p = &x; int **pp = &p;`, the value of `**pp` is
(A) the address of `x`  (B) the address of `p`  (C) 10  (D) the address of `pp`

**Q40.** A `void` pointer
(A) cannot store an address
(B) must be cast to a concrete type before it can be dereferenced
(C) is the same thing as a null pointer
(D) always points to a function

**Q41.** The return type of `malloc()` is
(A) `int*`  (B) `char*`  (C) `void*`  (D) `NULL`

**Q42.** Dereferencing a `NULL` pointer results in
(A) it returns 0  (B) undefined behaviour, usually a crash  (C) it returns `NULL`  (D) a compile error

**Q43.** Which correctly declares a pointer to a function taking two `int`s and returning `int`?
(A) `int *fp(int, int);`  (B) `int (*fp)(int, int);`  (C) `int fp*(int, int);`  (D) `(int*)fp(int, int);`

**Q44.** Which expression is **NOT** equivalent to `a[i]`?
(A) `*(a+i)`  (B) `*(i+a)`  (C) `i[a]`  (D) `*a + i`

**Q45.** A pointer that has never been initialised and holds garbage is a
(A) pointer to freed memory  (B) wild pointer  (C) null pointer  (D) void pointer

---

## Part D — Arrays, decay & 2-D address calculation

**Q46.** For `int arr[5];` with `sizeof(int)==4`, the value of `sizeof(arr)/sizeof(arr[0])` is
(A) 4  (B) 5  (C) 20  (D) 1

**Q47.** An array name does **not** decay to a pointer when used with
(A) `+`  (B) `sizeof` or `&`  (C) `[]`  (D) assignment

**Q48.** Inside `void f(int a[])`, on a 64-bit machine, `sizeof(a)` is
(A) 20  (B) 8  (C) 5  (D) 4

**Q49.** `int A[10][20]`, row-major, base 1000, 4 bytes/element, 0-based. Address of `A[3][5]`?
(A) 1140  (B) 1260  (C) 1220  (D) 1300

**Q50.** Same array `int A[10][20]`, but **column-major**, base 1000, 4 bytes. Address of `A[3][5]`?
(A) 1260  (B) 1212  (C) 1200  (D) 1224

**Q51.** `int A[1..10][1..20]` (1-based), row-major, base 1000, 4 bytes. Address of `A[3][5]`?
(A) 1260  (B) 1176  (C) 1180  (D) 1200

**Q52.** Which statement about arrays and pointers is correct?
(A) An array name can be reassigned
(B) A pointer can be reassigned but an array name cannot
(C) Both can be reassigned
(D) Neither can be reassigned

**Q53.** In `int a[5]; int *p = a;` the assignment is legal because
(A) it is illegal
(B) `a` decays to a pointer to its first element `&a[0]`
(C) it copies the whole array
(D) `p` points to the last element

**Q54.** For a 2-D array in row-major order, the address of `A[i][j]` (0-based) is
(A) Base + (i×Nrows + j)×size
(B) Base + (i×Ncols + j)×size
(C) Base + (j×Ncols + i)×size
(D) Base + (j×Nrows + i)×size

**Q55.** In column-major order the column index is multiplied by the number of
(A) columns  (B) rows  (C) elements  (D) bytes

**Q56.** The number of elements in `int a[3][4]` is
(A) 7  (B) 12  (C) 3  (D) 4

**Q57.** Which language stores 2-D arrays in **column-major** order?
(A) C  (B) Java  (C) FORTRAN  (D) Python

**Q58.** `sizeof(arr)/sizeof(arr[0])` yields the correct element count
(A) always  (B) only in the scope where the array was declared  (C) only inside functions  (D) never

---

## Part E — Dynamic memory & stack vs heap

**Q59.** Which statement about `malloc()` and `calloc()` is correct?
(A) `malloc()` zeroes the memory, `calloc()` does not
(B) `calloc()` zero-initialises the memory, `malloc()` does not
(C) both zero-initialise
(D) neither can return `NULL`

**Q60.** `calloc(5, sizeof(int))` (with `sizeof(int)==4`)
(A) allocates 5 bytes
(B) allocates 20 bytes and zero-initialises them
(C) allocates 20 bytes but leaves them uninitialised
(D) frees memory

**Q61.** `realloc(p, newsize)`
(A) always keeps the same address
(B) may move the block, so you must use the returned pointer
(C) frees the block
(D) zeroes the memory

**Q62.** Memory returned by `malloc()` is allocated from the
(A) stack  (B) heap  (C) data segment  (D) text segment

**Q63.** Calling `free(p)` and then dereferencing `*p` is
(A) safe  (B) undefined behaviour (use-after-free)  (C) guaranteed to return 0  (D) automatic reallocation

**Q64.** A memory leak occurs when
(A) memory is freed twice
(B) memory is allocated but never freed
(C) a `NULL` pointer is dereferenced
(D) the stack overflows

**Q65.** Stack allocation, compared with heap allocation, is
(A) manual and slow
(B) automatic and fast
(C) always via `malloc`
(D) performed by the programmer

**Q66.** Very deep (unbounded) recursion typically causes a
(A) heap overflow  (B) stack overflow  (C) memory leak  (D) segmentation of the heap

**Q67.** Calling `free(p)` twice on the same pointer
(A) does nothing  (B) is undefined behaviour, often a crash  (C) causes a memory leak  (D) zeroes the memory

**Q68.** After `free(p)`, the recommended practice is to
(A) call `free(p)` again  (B) set `p = NULL` to avoid a dangling pointer  (C) reallocate immediately  (D) do nothing

---

## Part F — Parameter passing

**Q69.** The parameter-passing mechanism of C is
(A) call by reference  (B) call by value only  (C) call by name  (D) call by value-result

**Q70.** A C function that attempts to swap two integers using **call by value**
(A) swaps them successfully
(B) does not affect the caller's variables
(C) causes a compilation error
(D) swaps them only if they are global

**Q71.** To make a swap in C visible to the caller, you must
(A) use call by value  (B) pass the variables' addresses (pointers)  (C) make them global  (D) return `void`

**Q72.** Passing a pointer to a C function is
(A) call by reference
(B) call by value of the address
(C) call by name
(D) call by result

**Q73.** True call by reference (an alias for the caller's variable) is directly available in
(A) C  (B) C++ using references (`int &x`)  (C) Java  (D) all of these

**Q74.** The mechanism that copies the argument in and copies the result back on return is
(A) call by value  (B) call by reference  (C) call by value-result (copy-restore)  (D) call by name

**Q75.** In call by name, the actual parameter is
(A) copied once  (B) an alias  (C) the textual expression, re-evaluated at each use  (D) an address

**Q76.** In Java, passing an object to a method
(A) copies the whole object
(B) lets the method reassign the caller's reference
(C) copies the reference, so the object can be mutated but the caller's variable cannot be reseated
(D) is call by reference

---

## Part G — Recursion

**Q77.** What does `f(5)` return?
```c
int f(int n) { if (n <= 1) return n; return f(n-1) + f(n-2); }
```
(A) 3  (B) 5  (C) 8  (D) 120

**Q78.** A correctly written recursive function must have
(A) a loop  (B) a base case and progress toward it  (C) global variables  (D) exactly two parameters

**Q79.** A recursive function that lacks a reachable base case will
(A) return 0  (B) recurse infinitely and overflow the stack  (C) not compile  (D) run in O(1)

**Q80.** What does `fact(4)` return, where `int fact(int n){ return n<=0 ? 1 : n*fact(n-1); }`?
(A) 12  (B) 16  (C) 24  (D) 120

**Q81.** The minimum number of moves to solve Towers of Hanoi with `n` discs is
(A) n²  (B) 2ⁿ − 1  (C) 2n − 1  (D) n!

**Q82.** The minimum number of moves for Towers of Hanoi with 4 discs is
(A) 7  (B) 15  (C) 16  (D) 8

**Q83.** The minimum number of moves for Towers of Hanoi with 5 discs is
(A) 31  (B) 32  (C) 15  (D) 63

**Q84.** A tail-recursive function is one where
(A) there are two recursive calls
(B) the recursive call is the very last operation
(C) it never terminates
(D) it uses a loop internally

**Q85.** The time complexity of naïve (unmemoised) recursive Fibonacci is
(A) O(n)  (B) O(n log n)  (C) O(2ⁿ)  (D) O(n²)

**Q86.** With memoisation, computing `fib(n)` becomes
(A) O(2ⁿ)  (B) O(n)  (C) O(log n)  (D) O(n²)

**Q87.** Each recursive call stores its parameters, locals and return address in
(A) the heap  (B) a CPU register  (C) an activation record (stack frame) on the stack  (D) the data segment

**Q88.** The function `int f(int n){ return n * f(n-1); }` is
(A) tail recursive
(B) not tail recursive, because the multiplication happens after the call returns
(C) iterative
(D) indirect recursion

**Q89.** Euclid's GCD, `gcd(a,b) = gcd(b, a % b)`, has time complexity
(A) O(n)  (B) O(log min(a,b))  (C) O(a·b)  (D) O(1)

**Q90.** The recurrence `T(n) = T(n/2) + 1` solves to
(A) O(n)  (B) O(log n)  (C) O(n log n)  (D) O(n²)

---

## Part H — Structures, unions, files & preprocessor

**Q91.** On a machine with 4-byte `int` and 4-byte alignment, `sizeof(union U { char c; int i; })` is
(A) 1  (B) 4  (C) 5  (D) 8

**Q92.** With 4-byte `int` and 4-byte alignment, `sizeof(struct S { char c; int i; })` is
(A) 5  (B) 8  (C) 4  (D) 6

**Q93.** With 4-byte `int` and 4-byte alignment, `sizeof(struct A { char c; int i; char d; })` is
(A) 6  (B) 8  (C) 12  (D) 9

**Q94.** In a `union`,
(A) all members hold valid values simultaneously
(B) only one member holds a meaningful value at a time
(C) members are stored side by side
(D) the size is the sum of the members

**Q95.** The size of a structure may exceed the sum of its members' sizes because of
(A) compiler bugs  (B) padding inserted for alignment  (C) the union rule  (D) bit-fields only

**Q96.** With 4-byte `int`, `sizeof(struct B { char c; char d; int i; })` is
(A) 12  (B) 8  (C) 6  (D) 10

**Q97.** A bit-field member such as `unsigned a : 3;` lets you
(A) increase the struct size
(B) specify the exact number of bits the member occupies
(C) create a union
(D) force 4-byte alignment

**Q98.** The expression `p->member` is identical to
(A) `*p.member`  (B) `(*p).member`  (C) `p.member`  (D) `&p.member`

**Q99.** `struct Node { int data; struct Node *next; };` is an example of a
(A) union  (B) self-referential structure (the basis of linked lists)  (C) bit-field  (D) array

**Q100.** Opening a file with mode `"w"`
(A) appends to it
(B) truncates an existing file to zero length
(C) opens it for reading only
(D) fails if the file exists

**Q101.** To add data to the end of an existing file without erasing it, use mode
(A) `"r"`  (B) `"w"`  (C) `"a"`  (D) `"r+"`

**Q102.** The C preprocessor
(A) performs type checking
(B) performs pure text substitution before compilation
(C) runs at link time
(D) executes the program

**Q103.** What does `SQ(2+3)` expand to and evaluate as, given `#define SQ(x) x*x`?
(A) 25  (B) 11  (C) 10  (D) 6

**Q104.** To prevent a header file from being included twice, you use
(A) `#pragma error`  (B) `#ifndef` / `#define` / `#endif` include guards  (C) two `#include`s  (D) `static`

**Q105.** Compared with functions, macros
(A) are type-checked
(B) have no type checking and may evaluate their arguments more than once
(C) are always slower
(D) are called at run time

---

## Part I — OOP concepts

**Q106.** Bundling data with the methods that operate on it, while restricting direct access to the data, is
(A) inheritance  (B) polymorphism  (C) encapsulation  (D) recursion

**Q107.** Exposing only the essential features while hiding implementation detail is
(A) encapsulation  (B) abstraction  (C) inheritance  (D) polymorphism

**Q108.** Which distinction between encapsulation and abstraction is correct?
(A) Encapsulation hides implementation; abstraction hides data
(B) Encapsulation hides data (the mechanism); abstraction hides complexity/implementation (the design goal)
(C) They are identical
(D) Neither hides anything

**Q109.** Inheritance models which relationship?
(A) has-a  (B) is-a  (C) uses-a  (D) part-of

**Q110.** Composition models which relationship?
(A) has-a  (B) is-a  (C) is-like-a  (D) none

**Q111.** A class is best described as
(A) an instance of an object
(B) a blueprint/template from which objects are created
(C) a function
(D) a variable

**Q112.** "One interface, many implementations" describes
(A) encapsulation  (B) abstraction  (C) polymorphism  (D) inheritance

**Q113.** Function overloading is an example of
(A) compile-time polymorphism  (B) run-time polymorphism  (C) inheritance  (D) encapsulation

**Q114.** Run-time (dynamic) polymorphism in C++ is achieved through
(A) function overloading  (B) operator overloading  (C) virtual functions and function overriding  (D) templates

**Q115.** Two overloaded methods must differ in their
(A) return type only  (B) parameter list  (C) name  (D) access modifier

**Q116.** An overriding method must have
(A) a different parameter list
(B) the same signature as the base-class method
(C) a different name
(D) a different return type only

**Q117.** Two methods with the same name and parameters but only a different return type cause
(A) overloading  (B) overriding  (C) a compile error  (D) run-time dispatch

**Q118.** Run-time method dispatch in C++ is implemented using
(A) a symbol table  (B) the vtable and vptr  (C) templates  (D) macros

**Q119.** When a class inherits from two base classes at once, it is
(A) single  (B) multiple  (C) multilevel  (D) hierarchical

**Q120.** An inheritance chain A → B → C is called
(A) multiple  (B) multilevel  (C) hierarchical  (D) hybrid

**Q121.** Java forbids multiple inheritance of classes primarily to avoid
(A) the diamond (ambiguity) problem  (B) memory leaks  (C) stack overflow  (D) type-casting errors

**Q122.** In C++, to ensure only one shared copy of a common base class in a diamond, you use
(A) `friend`  (B) virtual inheritance  (C) templates  (D) `static`

**Q123.** Which statement about a constructor is correct?
(A) It has the same name as the class and no return type
(B) It must return `void`
(C) It can be declared `static`
(D) It cannot be overloaded

**Q124.** A C++ destructor
(A) can be overloaded
(B) cannot be overloaded and takes no parameters
(C) has a return type
(D) can be declared `static`

**Q125.** A base-class destructor should be `virtual` so that
(A) constructors run in order
(B) deleting a derived object through a base pointer also calls the derived destructor
(C) it can be overloaded
(D) memory is zeroed

---

## Part J — C++ specifics

**Q126.** Which operator **cannot** be overloaded in C++?
(A) `+`  (B) `[]`  (C) `::`  (D) `<<`

**Q127.** Which operator **can** be overloaded in C++?
(A) `sizeof`  (B) `?:`  (C) `::`  (D) `[]`

**Q128.** Which set lists operators that cannot be overloaded in C++?
(A) `+ − * /`  (B) `:: . .* ?: sizeof`  (C) `[] () -> =`  (D) `<< >> == !=`

**Q129.** In C++, the default access specifier for members of a `class` is
(A) `public`  (B) `private`  (C) `protected`  (D) none

**Q130.** In C++, the default access specifier for members of a `struct` is
(A) `private`  (B) `public`  (C) `protected`  (D) hidden

**Q131.** The key difference between `new` and `malloc` is that
(A) they are identical
(B) `new` calls the constructor and returns a typed pointer; `malloc` returns raw `void*`
(C) `malloc` calls the constructor
(D) `new` returns `void*`

**Q132.** A C++ reference
(A) can be null
(B) must be initialised at declaration and cannot be reseated
(C) can be reassigned freely
(D) is exactly the same as a pointer

**Q133.** A class containing a pure virtual function (`virtual void f() = 0;`) is
(A) instantiable  (B) abstract and cannot be instantiated  (C) `final`  (D) a template

**Q134.** A `friend` function of a class
(A) is a member function
(B) can access the private members of the class
(C) cannot access private members
(D) is inherited by derived classes

**Q135.** A `protected` member is accessible from
(A) anywhere
(B) the class itself and its derived classes
(C) the same class only
(D) the same file only

**Q136.** C++ templates primarily enable
(A) manual memory management  (B) generic programming over types  (C) exception handling  (D) inheritance

**Q137.** Calling `free()` on memory obtained from `new`
(A) is required
(B) is undefined behaviour; you must use `delete`
(C) frees the constructors
(D) is perfectly safe

---

## Part K — Java

**Q138.** The Java Virtual Machine executes
(A) source code directly  (B) machine code  (C) bytecode  (D) assembly code

**Q139.** The Java compiler `javac` produces
(A) machine code  (B) platform-independent bytecode (`.class`)  (C) assembly  (D) source code

**Q140.** Which nesting relationship is correct?
(A) JVM ⊃ JRE ⊃ JDK  (B) JDK ⊃ JRE ⊃ JVM  (C) JRE ⊃ JDK ⊃ JVM  (D) JVM ⊃ JDK ⊃ JRE

**Q141.** Which of the following is **not** supported in Java?
(A) Explicit pointer arithmetic  (B) Multithreading  (C) Interfaces  (D) Garbage collection

**Q142.** Which of the following does Java support?
(A) operator overloading  (B) explicit pointer arithmetic  (C) automatic garbage collection  (D) destructors

**Q143.** In Java, `String` objects are
(A) mutable
(B) immutable; `StringBuffer`/`StringBuilder` are mutable
(C) both immutable and mutable
(D) mutable while `StringBuffer` is immutable

**Q144.** In Java, `==` applied to two `String` objects compares
(A) their contents  (B) their references (identity)  (C) their lengths  (D) their hash codes

**Q145.** Given `String a = "hello"; String c = new String("hello");`, `a == c` is
(A) true  (B) false  (C) a compile error  (D) a runtime error

**Q146.** For the same `a` and `c` above, `a.equals(c)` is
(A) false  (B) true  (C) a compile error  (D) null

**Q147.** Compared with `StringBuilder`, `StringBuffer` is
(A) faster and not thread-safe
(B) synchronised (thread-safe) but slower
(C) immutable
(D) identical

**Q148.** The block that executes whether or not an exception is thrown is
(A) `final`  (B) `finalize`  (C) `finally`  (D) `catch`

**Q149.** Which statement about `final`, `finally` and `finalize` is correct?
(A) `final` is a block, `finally` is a modifier
(B) `final` is a modifier, `finally` is a block that always runs, `finalize()` is a GC hook method
(C) all three are exception keywords
(D) `finalize` prevents overriding

**Q150.** A class declared `final` in Java
(A) cannot be instantiated  (B) cannot be extended (subclassed)  (C) has no methods  (D) is abstract

**Q151.** A member declared `private` in a Java class is accessible
(A) only within the same class
(B) within the same package
(C) within the same package and subclasses
(D) from anywhere

**Q152.** A Java member with **no** access modifier (default) is accessible
(A) within the same class only
(B) within the same package
(C) from anywhere
(D) by subclasses in other packages

**Q153.** A checked exception in Java
(A) need not be handled
(B) must be caught or declared with `throws`
(C) extends `RuntimeException`
(D) is an `Error`

**Q154.** `NullPointerException` is a(n)
(A) checked exception  (B) unchecked (runtime) exception  (C) `Error`  (D) compile error

**Q155.** Which distinction between `throw` and `throws` is correct?
(A) `throw` declares, `throws` raises
(B) `throw` raises an exception instance; `throws` declares in the method signature
(C) they are identical
(D) `throws` raises an instance

**Q156.** Variables declared in a Java interface are implicitly
(A) `private`  (B) `public static final`  (C) `protected`  (D) `transient`

**Q157.** In Java, a class can
(A) extend many classes
(B) implement many interfaces but extend only one class
(C) implement only one interface
(D) extend interfaces

**Q158.** In Java, a `char` occupies
(A) 1 byte  (B) 2 bytes  (C) 4 bytes  (D) an implementation-defined size

**Q159.** In the Java Collections Framework, which interface does **not** extend `Collection`?
(A) `List`  (B) `Set`  (C) `Queue`  (D) `Map`

**Q160.** A `static` method in Java
(A) can use `this`
(B) cannot use `this` or access instance members directly
(C) is created per object
(D) runs only after an object is created

**Q161.** The preferred way to define a thread's task in Java is to
(A) extend `Thread`
(B) implement `Runnable`
(C) implement `Callable` only
(D) override `finalize`

**Q162.** The correct signature of the Java entry point is
(A) `void main()`
(B) `public static void main(String[] args)`
(C) `static int main()`
(D) `public void main(String args)`

**Q163.** Calling `System.gc()`
(A) forces immediate garbage collection
(B) is only a request the JVM may ignore
(C) frees one specific object
(D) is illegal

**Q164.** Which of the following can have a constructor?
(A) an interface  (B) an abstract class  (C) both  (D) neither

**Q165.** `IOException` is a(n)
(A) unchecked exception  (B) checked exception  (C) `Error`  (D) `RuntimeException`

---

## Part L — Predict the output

**Q166.** What is printed?
```c
int a = 5, b = 2;
printf("%d", a << b);
```
(A) 10  (B) 20  (C) 7  (D) 25

**Q167.** What is printed?
```c
int i = 0;
while (i < 3) { printf("%d", i); i++; }
```
(A) `123`  (B) `012`  (C) `0123`  (D) `0 1 2`

**Q168.** What is printed?
```c
int arr[] = {10, 20, 30, 40};
int *p = arr;
printf("%d", *(p + 2));
```
(A) 20  (B) 30  (C) 40  (D) 10

**Q169.** What is printed?
```c
char str[] = "hello";
printf("%d", (int)sizeof(str));
```
(A) 5  (B) 6  (C) 4  (D) 8

**Q170.** What is printed?
```c
#define CUBE(x) (x)*(x)*(x)
printf("%d", CUBE(2));
```
(A) 6  (B) 8  (C) 2  (D) 18

**Q171.** What is printed in Java?
```java
System.out.println(10 + 20 + "Result");
```
(A) `Result30`  (B) `30Result`  (C) `1020Result`  (D) `Result1020`

**Q172.** What is printed in Java?
```java
System.out.println("Result" + 10 + 20);
```
(A) `Result30`  (B) `Result1020`  (C) `30Result`  (D) `1020Result`

**Q173.** What is printed in Java?
```java
String s = "abc";
s.concat("def");
System.out.println(s);
```
(A) `abcdef`  (B) `abc`  (C) `def`  (D) a compile error

**Q174.** What is printed?
```c
int n = 4, result = 1;
for (int i = 1; i <= n; i++) result *= i;
printf("%d", result);
```
(A) 10  (B) 16  (C) 24  (D) 256

**Q175.** What does `f(4)` return?
```c
int f(int n) { if (n == 0) return 0; return n + f(n-1); }
```
(A) 10  (B) 4  (C) 24  (D) 16

---

## Part M — Paper-I (English, Reasoning, GK)

**Q176.** The idiom *"to let the cat out of the bag"* means
(A) to release an animal  (B) to reveal a secret  (C) to create confusion  (D) to escape danger

**Q177.** Choose the word most nearly similar in meaning to **METICULOUS**.
(A) Careless  (B) Extremely careful and precise  (C) Hasty  (D) Doubtful

**Q178.** A man walks 5 km north, turns right and walks 3 km, then turns right again and walks 5 km. How far is he from the start?
(A) 3 km  (B) 5 km  (C) 8 km  (D) 13 km

**Q179.** The average of 5 consecutive odd numbers is 27. The largest of these numbers is
(A) 29  (B) 31  (C) 33  (D) 35

**Q180.** Kokborok, an official language of Tripura, belongs to which language family?
(A) Indo-Aryan  (B) Dravidian  (C) Tibeto-Burman  (D) Austroasiatic

**Q181.** Choose the antonym of **BENEVOLENT**.
(A) Kind  (B) Generous  (C) Cruel  (D) Helpful

**Q182.** One word for "a person who cannot read or write" is
(A) ignorant  (B) illiterate  (C) innocent  (D) illegal

**Q183.** Find the next term: 2, 6, 12, 20, 30, ?
(A) 40  (B) 42  (C) 44  (D) 36

**Q184.** A train 120 m long, running at 54 km/h, crosses a pole in
(A) 6 s  (B) 8 s  (C) 10 s  (D) 12 s

**Q185.** The simple interest on Rs 5000 at 8% per annum for 2 years is
(A) Rs 400  (B) Rs 800  (C) Rs 1000  (D) Rs 80

**Q186.** Find the odd one out.
(A) Square  (B) Circle  (C) Rectangle  (D) Triangle

**Q187.** The capital of Tripura is
(A) Aizawl  (B) Agartala  (C) Imphal  (D) Kohima

**Q188.** Tripura became a full-fledged state of India in
(A) 1947  (B) 1956  (C) 1972  (D) 1949

**Q189.** Choose the synonym of **EPHEMERAL**.
(A) Eternal  (B) Short-lived  (C) Important  (D) Hidden

**Q190.** If 5 pens cost Rs 60, the cost of 8 pens (at the same rate) is
(A) Rs 80  (B) Rs 90  (C) Rs 96  (D) Rs 100

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | C | 28 | B | 55 | B | 82 | B | 109 | B | 136 | B | 163 | B |
| 2 | B | 29 | A | 56 | B | 83 | A | 110 | A | 137 | B | 164 | B |
| 3 | A | 30 | D | 57 | C | 84 | B | 111 | B | 138 | C | 165 | B |
| 4 | B | 31 | B | 58 | B | 85 | C | 112 | C | 139 | B | 166 | B |
| 5 | B | 32 | B | 59 | B | 86 | B | 113 | A | 140 | B | 167 | B |
| 6 | B | 33 | B | 60 | B | 87 | C | 114 | C | 141 | A | 168 | B |
| 7 | B | 34 | A | 61 | B | 88 | B | 115 | B | 142 | C | 169 | B |
| 8 | B | 35 | C | 62 | B | 89 | B | 116 | B | 143 | B | 170 | B |
| 9 | B | 36 | B | 63 | B | 90 | B | 117 | C | 144 | B | 171 | B |
| 10 | C | 37 | B | 64 | B | 91 | B | 118 | B | 145 | B | 172 | B |
| 11 | C | 38 | C | 65 | B | 92 | B | 119 | B | 146 | B | 173 | B |
| 12 | C | 39 | C | 66 | B | 93 | C | 120 | B | 147 | B | 174 | C |
| 13 | B | 40 | B | 67 | B | 94 | B | 121 | A | 148 | C | 175 | A |
| 14 | B | 41 | C | 68 | B | 95 | B | 122 | B | 149 | B | 176 | B |
| 15 | C | 42 | B | 69 | B | 96 | B | 123 | A | 150 | B | 177 | B |
| 16 | B | 43 | B | 70 | B | 97 | B | 124 | B | 151 | A | 178 | A |
| 17 | B | 44 | D | 71 | B | 98 | B | 125 | B | 152 | B | 179 | B |
| 18 | C | 45 | B | 72 | B | 99 | B | 126 | C | 153 | B | 180 | C |
| 19 | B | 46 | B | 73 | B | 100 | B | 127 | D | 154 | B | 181 | C |
| 20 | B | 47 | B | 74 | C | 101 | C | 128 | B | 155 | B | 182 | B |
| 21 | A | 48 | B | 75 | C | 102 | B | 129 | B | 156 | B | 183 | B |
| 22 | B | 49 | B | 76 | C | 103 | B | 130 | B | 157 | B | 184 | B |
| 23 | B | 50 | B | 77 | B | 104 | B | 131 | B | 158 | B | 185 | B |
| 24 | A | 51 | B | 78 | B | 105 | B | 132 | B | 159 | D | 186 | B |
| 25 | B | 52 | B | 79 | B | 106 | C | 133 | B | 160 | B | 187 | B |
| 26 | C | 53 | B | 80 | C | 107 | B | 134 | B | 161 | B | 188 | C |
| 27 | B | 54 | B | 81 | B | 108 | B | 135 | B | 162 | B | 189 | B |
| | | | | | | | | | | | | 190 | C |

---

# 📝 Detailed Solutions

**Q1. (C)** Local variables have automatic storage duration by default — the `auto` storage class — giving block scope and a lifetime ending at block exit. The keyword is almost never written.

**Q2. (B)** `static` gives the local variable static storage duration (whole-program lifetime) while keeping block scope. It is initialised once and keeps its value across calls.

**Q3. (A)** By definition `sizeof(char) == 1` — a "byte" in C *is* a char. All other sizes are implementation-defined.

**Q4. (B)** The standard guarantees `sizeof(char)==1` and the ordering `char ≤ short ≤ int ≤ long ≤ long long`. Exact sizes of `int`/`long` are implementation-defined.

**Q5. (B)** The C standard requires `int` to be at least 16 bits and `long` at least 32 bits. Typical implementations use 32-bit `int`, but 16 is the guaranteed minimum.

**Q6. (B)** On a global variable or function, `static` restricts linkage to the current translation unit (file), hiding it from other files. It has nothing to do with lifetime here.

**Q7. (B)** Objects with static storage duration (including `static` locals) are zero-initialised if no initialiser is given.

**Q8. (B)** Automatic (`auto`) variables are not initialised; they hold whatever garbage was on the stack.

**Q9. (B)** `register` is only a hint asking the compiler to keep the variable in a CPU register; the compiler may ignore it. You also cannot take its address.

**Q10. (C)** `extern` declares that a variable is defined elsewhere, giving external linkage so multiple files can share it.

**Q11. (C)** Uninitialised globals and statics live in the BSS segment, which is zeroed at load time.

**Q12. (C)** Executable machine instructions live in the read-only text (code) segment.

**Q13. (B)** Java fixes primitive sizes on every platform: `int` is always 4 bytes. This portability is a deliberate design goal.

**Q14. (B)** The stack holds local variables, parameters and return addresses and typically grows downward (toward lower addresses) into the heap; deep recursion can overflow it.

**Q15. (C)** The `static int c` is initialised once and retained: the three calls print 1, then 2, then 3 → `1 2 3`.

**Q16. (B)** `*` binds tighter than `+`, so `a + b * c` is `a + (b*c)`.

**Q17. (B)** Assignment is right-associative, so `a = b = c` is `a = (b = c)`.

**Q18. (C)** Unary operators, the ternary `?:` and assignment operators are right-associative; most others are left-associative.

**Q19. (B)** `==` has higher precedence than bitwise `&`, so `x & MASK == 0` parses as `x & (MASK == 0)` — the classic masking bug.

**Q20. (B)** `/` and `*` are equal precedence, left-associative: `(10/3)*3 = 3*3 = 9` (integer division truncates), and `10%3 = 1`, so `9 + 1 = 10`.

**Q21. (A)** Integer division truncates toward zero: `10/3 = 3`.

**Q22. (B)** C integer division truncates toward zero, so `-7/2 = -3`, not −4.

**Q23. (B)** Mixing signed and unsigned promotes both to unsigned; `-1` becomes a huge unsigned value, which is not `< 1`, so the condition is false.

**Q24. (A)** `17 % 5 = 2` (17 = 3×5 + 2).

**Q25. (B)** The ternary operator is right-associative, so nested `?:` groups from the right.

**Q26. (C)** The comma operator has the lowest precedence of all C operators.

**Q27. (B)** By integer promotion, `char`/`short` operands are promoted to `int` before arithmetic.

**Q28. (B)** In C (unlike C++), a character constant has type `int`, so `sizeof('A')` equals `sizeof(int)`.

**Q29. (A)** `==` (equality) has higher precedence than bitwise `&`; that is exactly why `x & MASK == 0` misparses.

**Q30. (D)** `x` is modified twice between sequence points (via `x++` and `++x`) with no intervening sequence point, so the behaviour is undefined.

**Q31. (B)** `&x` yields the address of `x`.

**Q32. (B)** Dereferencing with `*p` yields the value stored at the address `p` holds — the value of `x`.

**Q33. (B)** `p + 3` advances by `3 × sizeof(int) = 12` bytes: `1000 + 12 = 1012`.

**Q34. (A)** `char` is 1 byte, so `c + 3 = 1000 + 3 = 1003`.

**Q35. (C)** `double` is 8 bytes, so `d + 2 = 2000 + 16 = 2016`.

**Q36. (B)** Pointer subtraction gives the number of elements: `(1020 − 1000)/sizeof(int) = 20/4 = 5`.

**Q37. (B)** A pointer just holds an address, so all pointer types are the same size (8 bytes on a 64-bit machine).

**Q38. (C)** Adding two pointers is illegal; pointer+integer, pointer−pointer and comparison are all legal.

**Q39. (C)** `pp` → `p` → `x`, so `**pp` dereferences twice to reach `x`'s value, 10.

**Q40. (B)** A `void*` has no element type, so it must be cast to a concrete pointer type before dereferencing.

**Q41. (C)** `malloc` (like `calloc`/`realloc`) returns a generic `void*`.

**Q42. (B)** Dereferencing `NULL` is undefined behaviour and usually crashes the program.

**Q43. (B)** `int (*fp)(int, int);` declares `fp` as a pointer to a function taking two ints and returning int; the parentheses around `*fp` are essential.

**Q44. (D)** `a[i]` equals `*(a+i)`, `*(i+a)` and `i[a]`. But `*a + i` is `a[0] + i`, which is different.

**Q45. (B)** An uninitialised pointer holding garbage is a wild pointer (distinct from dangling and null).

**Q46. (B)** `sizeof(arr) = 5×4 = 20`, `sizeof(arr[0]) = 4`, so `20/4 = 5`.

**Q47. (B)** Array-to-pointer decay does not happen with `sizeof` or the address-of `&` operator.

**Q48. (B)** A parameter `int a[]` is really `int*`, so `sizeof(a)` is the pointer size, 8, on a 64-bit machine.

**Q49. (B)** Row-major: `1000 + (3×20 + 5)×4 = 1000 + 65×4 = 1000 + 260 = 1260`.

**Q50. (B)** Column-major: `1000 + (5×10 + 3)×4 = 1000 + 53×4 = 1000 + 212 = 1212`.

**Q51. (B)** With 1-based bounds: `1000 + [(3−1)×20 + (5−1)]×4 = 1000 + [40+4]×4 = 1000 + 176 = 1176`.

**Q52. (B)** A pointer variable can be reassigned; an array name is not a modifiable lvalue, so `a = ...` is an error.

**Q53. (B)** In an expression the array name decays to a pointer to its first element, so `int *p = a;` is `p = &a[0]`.

**Q54. (B)** Row-major skips whole rows first, so you multiply the row index by the number of columns: `Base + (i×Ncols + j)×size`.

**Q55. (B)** Column-major skips whole columns first, so the column index is multiplied by the number of rows.

**Q56. (B)** `int a[3][4]` has `3×4 = 12` elements.

**Q57. (C)** FORTRAN (also MATLAB, R) uses column-major order; C, C++, Java and Python are row-major.

**Q58. (B)** The idiom works only where the array is declared; once it decays to a pointer (e.g. inside a function) it fails.

**Q59. (B)** `calloc` zero-initialises its memory; `malloc` leaves it uninitialised. Both return `void*` and `NULL` on failure.

**Q60. (B)** `calloc(5, sizeof(int))` allocates `5×4 = 20` bytes and zero-initialises them.

**Q61. (B)** `realloc` may relocate the block to satisfy the new size, so you must always use the returned pointer.

**Q62. (B)** `malloc`, `calloc` and `realloc` all allocate from the heap.

**Q63. (B)** Using a pointer after its memory has been freed is a use-after-free — undefined behaviour.

**Q64. (B)** A memory leak is heap memory that is allocated but never freed, so usage grows over time.

**Q65. (B)** Stack allocation is automatic (managed by the compiler) and fast — just adjusting a pointer — whereas the heap must search for a free block.

**Q66. (B)** Deep recursion pushes too many frames and overflows the stack.

**Q67. (B)** Freeing the same pointer twice is undefined behaviour and often crashes.

**Q68. (B)** Setting `p = NULL` after `free(p)` prevents a dangling pointer and makes an accidental later `free` harmless.

**Q69. (B)** C passes all arguments by value only; passing a pointer just copies an address.

**Q70. (B)** Call by value copies the arguments, so the function swaps only its own copies; the caller's variables are unchanged.

**Q71. (B)** You must pass the addresses (pointers) and swap through dereferencing for the change to be visible.

**Q72. (B)** Passing a pointer is still call by value — the *address* is copied — though the effect resembles call by reference.

**Q73. (B)** C++ references (`int &x`) provide true call by reference. C has no such mechanism.

**Q74. (C)** Call by value-result (copy-restore, e.g. Ada `in out`) copies the argument in and copies the result back on return.

**Q75. (C)** In call by name the actual argument's expression is textually substituted and re-evaluated at each use.

**Q76. (C)** Java is call by value; for objects the reference value is copied, so a method can mutate the object but cannot reseat the caller's variable.

**Q77. (B)** This is Fibonacci: f(0)=0, f(1)=1, f(2)=1, f(3)=2, f(4)=3, f(5)=5.

**Q78. (B)** Recursion needs a base case and each recursive call must make progress toward it.

**Q79. (B)** Without a reachable base case the function recurses forever and overflows the stack.

**Q80. (C)** `fact(4) = 4×3×2×1 = 24`.

**Q81. (B)** Towers of Hanoi satisfies T(n) = 2T(n−1) + 1, giving a minimum of 2ⁿ − 1 moves.

**Q82. (B)** 2⁴ − 1 = 15.

**Q83. (A)** 2⁵ − 1 = 31.

**Q84. (B)** In tail recursion the recursive call is the last operation, so nothing is done with its result and it can become a loop.

**Q85. (C)** Naïve Fibonacci recomputes subproblems, giving exponential O(2ⁿ) time.

**Q86. (B)** Memoisation caches each result, computing each of n values once → O(n).

**Q87. (C)** Each call's parameters, locals and return address form an activation record on the stack.

**Q88. (B)** The multiplication `n * f(n-1)` happens after the recursive call returns, so it is not tail recursive.

**Q89. (B)** Euclid's algorithm runs in O(log min(a,b)) because the remainder shrinks rapidly.

**Q90. (B)** T(n) = T(n/2) + 1 (binary-search style) solves to O(log n).

**Q91. (B)** A union's size is that of its largest member: max(1, 4) = 4.

**Q92. (B)** `char` at 0, 3 padding bytes, `int` at 4–7 → 8 bytes.

**Q93. (C)** `c` at 0, pad 1–3, `i` at 4–7, `d` at 8, pad 9–11 (to a multiple of 4) → 12 bytes.

**Q94. (B)** Union members overlap in the same memory, so only one holds a meaningful value at a time.

**Q95. (B)** The compiler inserts padding bytes to keep members aligned, so the size can exceed the sum of member sizes.

**Q96. (B)** `c` at 0, `d` at 1, pad 2–3, `i` at 4–7 → 8 bytes; ordering the small members together saves padding.

**Q97. (B)** Bit-fields let you specify the exact number of bits a member uses, packing several into one storage unit.

**Q98. (B)** `p->member` is defined as `(*p).member`.

**Q99. (B)** A structure containing a pointer to its own type is self-referential — the basis of linked lists and trees.

**Q100. (B)** Mode `"w"` truncates an existing file to zero length (or creates it).

**Q101. (C)** Mode `"a"` appends, writing at the end without erasing existing content.

**Q102. (B)** The preprocessor performs pure text substitution before compilation and understands no types.

**Q103. (B)** `SQ(2+3)` expands to `2+3*2+3 = 2+6+3 = 11` because the macro lacks parentheses.

**Q104. (B)** Include guards using `#ifndef`/`#define`/`#endif` prevent multiple inclusion of a header.

**Q105. (B)** Macros are textual, so they have no type checking and can evaluate arguments more than once (e.g. `SQ(i++)`).

**Q106. (C)** Bundling data with methods plus access control is encapsulation.

**Q107. (B)** Showing only essential features and hiding implementation detail is abstraction.

**Q108. (B)** Encapsulation hides data and is the mechanism (access modifiers); abstraction hides complexity/implementation and is the design goal.

**Q109. (B)** Inheritance models the "is-a" relationship (a Car is a Vehicle).

**Q110. (A)** Composition models "has-a" (a Car has an Engine).

**Q111. (B)** A class is a blueprint/template; objects are instances built from it.

**Q112. (C)** "One interface, many implementations" is polymorphism.

**Q113. (A)** Overloading is resolved by the compiler from argument types — compile-time (static) polymorphism.

**Q114. (C)** Run-time polymorphism uses virtual functions and overriding, resolved at run time via the vtable.

**Q115. (B)** Overloaded methods must differ in their parameter list; a differing return type alone is not enough.

**Q116. (B)** An overriding method must keep the same signature as the base-class method.

**Q117. (C)** The compiler cannot choose based on return type alone, so same name + same parameters + different return type is a compile error.

**Q118. (B)** Dynamic dispatch follows the object's vptr into its class's vtable to find the function.

**Q119. (B)** Inheriting from two base classes at once is multiple inheritance.

**Q120. (B)** A chain A → B → C is multilevel inheritance.

**Q121. (A)** Multiple class inheritance can make an inherited member reachable by two paths ambiguous — the diamond problem — which Java avoids by forbidding it.

**Q122. (B)** C++ virtual inheritance (`class B : virtual public A`) ensures a single shared copy of the common base.

**Q123. (A)** A constructor has the class's name and no return type (not even `void`); it can be overloaded but not `static`.

**Q124. (B)** A destructor takes no parameters, has no return type and cannot be overloaded — there is only one way to destroy an object.

**Q125. (B)** A virtual destructor ensures that deleting a derived object through a base pointer runs the derived destructor too, preventing leaks.

**Q126. (C)** `::` (scope resolution) cannot be overloaded; the non-overloadable set is `:: . .* ?: sizeof`.

**Q127. (D)** `[]` (subscript) can be overloaded; `sizeof`, `?:` and `::` cannot.

**Q128. (B)** The operators that cannot be overloaded are exactly `:: . .* ?: sizeof`.

**Q129. (B)** Members of a `class` are `private` by default.

**Q130. (B)** Members of a `struct` are `public` by default — essentially the only difference from `class`.

**Q131. (B)** `new` calls the constructor and returns a typed pointer; `malloc` returns raw `void*` and initialises nothing.

**Q132. (B)** A reference must be initialised at declaration and can never be made to refer to a different object.

**Q133. (B)** A class with a pure virtual function is abstract and cannot be instantiated; derived classes must implement it.

**Q134. (B)** A `friend` function is granted access to the class's private (and protected) members.

**Q135. (B)** `protected` members are accessible within the class and its derived classes.

**Q136. (B)** Templates provide generic programming, writing code once that works for many types.

**Q137. (B)** Memory from `new` must be released with `delete`; using `free` on it is undefined behaviour.

**Q138. (C)** The JVM executes platform-independent bytecode.

**Q139. (B)** `javac` compiles source to bytecode stored in `.class` files.

**Q140. (B)** The nesting is JDK ⊃ JRE ⊃ JVM.

**Q141. (A)** Java deliberately omits explicit pointer arithmetic for safety; it supports multithreading, interfaces and garbage collection.

**Q142. (C)** Java supports automatic garbage collection but not operator overloading, explicit pointers or destructors.

**Q143. (B)** `String` is immutable; every "modification" creates a new object. `StringBuffer`/`StringBuilder` are mutable.

**Q144. (B)** `==` compares references (identity), not content.

**Q145. (B)** `new String(...)` forces a separate object, so `a == c` is false.

**Q146. (B)** `.equals()` compares content, so `a.equals(c)` is true.

**Q147. (B)** `StringBuffer` is synchronised (thread-safe) but slower; `StringBuilder` is faster and not synchronised.

**Q148. (C)** The `finally` block always runs, whether or not an exception is thrown.

**Q149. (B)** `final` is a modifier, `finally` is a block that always executes, and `finalize()` is a (deprecated) GC hook method.

**Q150. (B)** A `final` class cannot be extended/subclassed.

**Q151. (A)** `private` restricts access to the same class only — not the package.

**Q152. (B)** Default (package-private) access allows use within the same package.

**Q153. (B)** A checked exception must be caught or declared with `throws`, enforced by the compiler.

**Q154. (B)** `NullPointerException` extends `RuntimeException`, so it is unchecked.

**Q155. (B)** `throw` is a statement that raises an exception instance; `throws` is a signature clause declaring possible exceptions.

**Q156. (B)** Interface variables are implicitly `public static final` (constants).

**Q157. (B)** A class may implement many interfaces but extend only one class.

**Q158. (B)** Java's `char` is 2 bytes (Unicode), unlike C's 1-byte char.

**Q159. (D)** `Map` stores key-value pairs and does not extend `Collection`; `List`, `Set` and `Queue` do.

**Q160. (B)** A `static` method has no instance, so it cannot use `this` or access instance members directly.

**Q161. (B)** Implementing `Runnable` is preferred because it leaves the single inheritance slot free.

**Q162. (B)** The required entry point is `public static void main(String[] args)`.

**Q163. (B)** `System.gc()` is only a request; the JVM may ignore it.

**Q164. (B)** An abstract class can have a constructor (run by subclasses); an interface cannot.

**Q165. (B)** `IOException` is a checked exception (it does not extend `RuntimeException`).

**Q166. (B)** `5 << 2` shifts 5 left by 2 bits: `5 × 4 = 20`.

**Q167. (B)** The loop prints i for i = 0, 1, 2 with no separators → `012`.

**Q168. (B)** `p` points to `arr[0]`, so `*(p+2)` is `arr[2] = 30`.

**Q169. (B)** `"hello"` needs 5 characters plus the null terminator, so the array is 6 bytes.

**Q170. (B)** `CUBE(2)` expands to `(2)*(2)*(2) = 8`; the parentheses keep it correct here.

**Q171. (B)** Evaluated left to right: `10 + 20 = 30`, then `30 + "Result"` → `"30Result"`.

**Q172. (B)** `"Result" + 10` → `"Result10"`, then `+ 20` → `"Result1020"` (string concatenation, not addition).

**Q173. (B)** `String` is immutable; `s.concat("def")` returns a new string that is discarded, so `s` stays `"abc"`.

**Q174. (C)** The loop computes `4! = 1×2×3×4 = 24`.

**Q175. (A)** `f(4) = 4 + 3 + 2 + 1 + 0 = 10`.

**Q176. (B)** *Let the cat out of the bag* means to disclose a secret, usually accidentally.

**Q177. (B)** *Meticulous* means showing great attention to detail — very careful and precise.

**Q178. (A)** North 5 km, east 3 km, south 5 km: the two 5 km legs cancel, leaving 3 km due east of the start.

**Q179. (B)** With five consecutive odd numbers the average is the middle term (27): 23, 25, 27, 29, 31 — the largest is 31.

**Q180. (C)** Kokborok (Tripuri) is a Tibeto-Burman language of the Sino-Tibetan family.

**Q181. (C)** *Benevolent* means kind/well-meaning; its antonym is cruel.

**Q182. (B)** A person who cannot read or write is *illiterate*.

**Q183. (B)** The terms are n(n+1): 2, 6, 12, 20, 30, then 6×7 = 42.

**Q184. (B)** 54 km/h = 15 m/s; crossing a pole = length/speed = 120/15 = 8 s.

**Q185. (B)** SI = P×R×T/100 = 5000×8×2/100 = 800.

**Q186. (B)** A circle has no straight sides or vertices; the square, rectangle and triangle are all straight-sided polygons.

**Q187. (B)** The capital of Tripura is Agartala.

**Q188. (C)** Tripura became a full-fledged state on 21 January 1972.

**Q189. (B)** *Ephemeral* means lasting a very short time — short-lived.

**Q190. (C)** Unit cost = 60/5 = 12; 8 pens cost 8×12 = 96.
