# Week 1 — Digital Logic & Number Systems

**Syllabus §2:** Boolean algebra. Combinational and sequential circuits. Minimization. Number representations and computer arithmetic (fixed and floating point).
**Estimated marks: ~9**

---

## 💡 What this whole subject is about

A computer is, physically, millions of tiny electrical switches. A switch has only two states: **on** or **off**. That is all the hardware can do.

Digital Logic is the study of how you get from "millions of on/off switches" to "a machine that can add numbers, remember things and make decisions". It has three parts, and this file follows them in order:

1. **Number systems** — how do you represent a number like −27.5 using only on/off?
2. **Combinational circuits** — how do you wire switches together so they *compute* something (add, compare, select)?
3. **Sequential circuits** — how do you make a circuit *remember* a value, so the computer has memory?

Everything else (Week 2's processor design, and ultimately all software) is built on top of this.

---

# 1. Number systems

## 1.1 Why binary, and how positional notation works

### 💡 The idea

You already use a **positional number system** every day. When you write 4,072 you mean:

```
4 × 1000  +  0 × 100  +  7 × 10  +  2 × 1
4 × 10³   +  0 × 10²  +  7 × 10¹ +  2 × 10⁰
```

The **position** of each digit tells you what power of 10 to multiply it by. We use powers of 10 because we have 10 fingers — there is nothing mathematically special about it.

A computer has "two fingers" (on and off), so it uses powers of **2**. The rules are identical; only the base changes.

**Binary `1101` means:**
```
1 × 2³  +  1 × 2²  +  0 × 2¹  +  1 × 2⁰
1 × 8   +  1 × 4   +  0 × 2   +  1 × 1   =  13
```

Two other bases appear constantly, purely as **shorthand for humans**:
- **Octal** (base 8) — one octal digit = exactly 3 binary digits
- **Hexadecimal** (base 16) — one hex digit = exactly 4 binary digits

Nobody wants to read `10110110`. Writing it as `B6` in hex is the same information, four times shorter. Computers do not "use hex" — hex is just how we write binary down.

### Reference

| Base | Name | Digits |
|---|---|---|
| 2 | Binary | 0–1 |
| 8 | Octal | 0–7 |
| 10 | Decimal | 0–9 |
| 16 | Hexadecimal | 0–9, A–F (A=10, B=11, C=12, D=13, E=14, F=15) |

**Memorise this small table — it makes hex conversion instant:**

| Binary | Hex | Binary | Hex |
|---|---|---|---|
| 0000 | 0 | 1000 | 8 |
| 0001 | 1 | 1001 | 9 |
| 0010 | 2 | 1010 | A |
| 0011 | 3 | 1011 | B |
| 0100 | 4 | 1100 | C |
| 0101 | 5 | 1101 | D |
| 0110 | 6 | 1110 | E |
| 0111 | 7 | 1111 | F |

## 1.2 Conversions

### How it works

**Binary → Octal:** group the bits in **3s**, starting from the radix point and moving outwards. Pad with zeros if needed.
**Binary → Hex:** group the bits in **4s**, same rule.

*Why does this work?* Because 8 = 2³ and 16 = 2⁴. Three binary digits can express exactly 8 values, which is exactly one octal digit's worth of information.

🔢 **Convert `10110110₂` to hex and octal.**

Hex — group in 4s from the right:
```
1011 | 0110
  B  |   6      →  B6₁₆
```
Octal — group in 3s from the right (pad the left with a zero):
```
010 | 110 | 110
 2  |  6  |  6   →  266₈
```

**Decimal → any base (integer part):** repeatedly **divide** by the base, and read the remainders **bottom-up**.

🔢 **Convert 45 to binary.**
```
45 ÷ 2 = 22 remainder 1   ↑
22 ÷ 2 = 11 remainder 0   │
11 ÷ 2 =  5 remainder 1   │  read
 5 ÷ 2 =  2 remainder 1   │  upwards
 2 ÷ 2 =  1 remainder 0   │
 1 ÷ 2 =  0 remainder 1   ↑
```
Reading bottom to top: **`101101₂`**. Check: 32+8+4+1 = 45 ✅

**Decimal → any base (fraction part):** repeatedly **multiply** by the base, and read the integer parts **top-down**.

🔢 **Convert 0.625 to binary.**
```
0.625 × 2 = 1.25  → integer part 1  ↓
0.25  × 2 = 0.50  → integer part 0  │  read
0.5   × 2 = 1.00  → integer part 1  ↓  downwards
```
Result: **`0.101₂`**. Check: 0.5 + 0 + 0.125 = 0.625 ✅

⚠ Some decimal fractions **never terminate** in binary. 0.1 in binary is `0.0001100110011…` recurring — which is exactly why `0.1 + 0.2 != 0.3` in most programming languages.

📌 Number of digits needed to represent decimal N in base b = **⌊log_b N⌋ + 1**

## 1.3 Representing negative numbers

### 💡 The idea

Binary as described so far can only express 0 and positive numbers. But we need negatives. The problem: we cannot store a minus sign — we only have 0s and 1s.

The solution is to **sacrifice one bit** (the leftmost, called the **MSB** — Most Significant Bit) to indicate sign. There are three historical ways to do this, and understanding *why* the third one won is the point of this section.

**Attempt 1 — Signed magnitude.** MSB = 0 means positive, MSB = 1 means negative; the rest is the plain magnitude.
```
+5 = 0000 0101
−5 = 1000 0101      (same bits, sign flipped)
```
*Problem:* there are **two zeros** (`0000 0000` = +0 and `1000 0000` = −0), which wastes a value and breaks equality checks. Worse, addition needs special-case hardware: to compute 5 + (−3) the circuit must notice the signs differ, compare magnitudes, subtract the smaller from the larger, and work out the result's sign. That is a lot of logic.

**Attempt 2 — 1's complement.** To negate a number, **flip every bit**.
```
+5 = 0000 0101
−5 = 1111 1010      (every bit inverted)
```
*Better,* but still two zeros (`0000 0000` and `1111 1111`), and addition needs an awkward "end-around carry" fix.

**Attempt 3 — 2's complement.** To negate a number, **flip every bit, then add 1**.
```
+5 = 0000 0101
     1111 1010      (flip)
   + 1
−5 = 1111 1011      (add 1)
```

⭐ **Why 2's complement won, and why every real computer uses it:**

1. **There is exactly one zero.** Negating `0000 0000` gives `1111 1111 + 1` = `0000 0000` (the carry falls off the end). No −0.
2. ⭐ **Subtraction becomes addition.** A − B is computed as A + (2's complement of B). The processor therefore needs only an **adder** — no separate subtractor circuit. This is an enormous hardware saving and is the real reason for the choice.
3. **The sign bit participates in arithmetic normally.** No special-casing.

🔢 **Check point 2:** compute 7 − 5 in 4-bit 2's complement.
```
 7 = 0111
 5 = 0101  →  2's comp:  1010 + 1 = 1011  (= −5)

   0111   (7)
 + 1011   (−5)
 ------
  10010   → discard the carry out of the 4-bit width → 0010 = 2 ✅
```
The adder did a subtraction without knowing it.

### How to take a 2's complement — two methods

**Method 1 (definition):** invert all bits, add 1.
**Method 2 (faster, do this in the exam):** scan from the right; **copy bits up to and including the first `1`, then invert everything to the left of it.**

🔢 **2's complement of `01011010`:**
- Method 1: invert → `10100101`; add 1 → **`10100110`**
- Method 2: from the right, the first `1` is in position 1 (the `10` at the end). Copy `10`, invert the rest (`010110` → `101001`) → **`10100110`** ✅

⚠ ⭐ **`10100101` is the 1's complement, not the 2's complement.** Forgetting the "+1" is the single most common error in this entire topic, and exam options are always written to include it.

### ⭐ Reference — ranges

| Representation | Range (n bits) | Zeros | Negation rule |
|---|---|---|---|
| Unsigned | 0 to 2ⁿ − 1 | one | n/a |
| Signed magnitude | −(2ⁿ⁻¹ − 1) to +(2ⁿ⁻¹ − 1) | **two** | Flip MSB |
| 1's complement | −(2ⁿ⁻¹ − 1) to +(2ⁿ⁻¹ − 1) | **two** | Flip all bits |
| ⭐ **2's complement** | ⭐ **−2ⁿ⁻¹ to +2ⁿ⁻¹ − 1** | **one** | Flip all bits, **add 1** |

⭐ **For 8 bits, 2's complement range is −128 to +127.**

*Why the asymmetry?* With 8 bits you have 256 patterns. One is used for zero, leaving 255 for non-zero values. Since there is no −0 to waste, you get 127 positives and **128** negatives. The extra pattern `1000 0000` is −128.

🔢 Quick sanity table (4-bit 2's complement):

| Bits | Value | Bits | Value |
|---|---|---|---|
| 0000 | 0 | 1000 | **−8** |
| 0001 | 1 | 1001 | −7 |
| 0010 | 2 | 1010 | −6 |
| 0011 | 3 | 1011 | −5 |
| 0100 | 4 | 1100 | −4 |
| 0101 | 5 | 1101 | −3 |
| 0110 | 6 | 1110 | −2 |
| 0111 | **7** | 1111 | −1 |

Notice: `1111` is −1, not −15. To read a negative 2's complement number, either (a) take its 2's complement to get the magnitude, or (b) treat the MSB as having weight **−2ⁿ⁻¹**: `1011` = −8 + 0 + 2 + 1 = −5 ✅

## 1.4 Overflow

### 💡 The idea

**Overflow** means the true answer does not fit in the number of bits you have. The circuit still produces *an* answer — just a wrong one, silently. Detecting this is important.

🔢 In 4-bit 2's complement (range −8 to +7), compute 5 + 4:
```
  0101   (+5)
+ 0100   (+4)
------
  1001   which reads as −7, not +9
```
Two positives produced a negative. The true answer (9) is outside the range, so the sign bit got corrupted.

### ⭐ How to detect it

⭐ For **2's complement (signed) addition**, overflow occurs when:
- Both operands are **positive** and the result is **negative**, or
- Both operands are **negative** and the result is **positive**.

📌 ⭐ Equivalently, in hardware: **overflow = C_in(MSB) ⊕ C_out(MSB)** — the carry *into* the sign bit differs from the carry *out of* it.

🔢 Check the example above: carry into the MSB column was 1, carry out was 0. 1 ⊕ 0 = 1 → **overflow** ✅

⚠ ⭐ **Adding numbers of opposite signs can NEVER overflow.** (Adding a positive and a negative gives a result between them in magnitude, so it must fit.)

⚠ ⭐ **Signed and unsigned overflow are different tests.** For **unsigned** addition, overflow is simply "the final carry-out is 1". A question that gives you a carry-out and asks about signed overflow is testing exactly this distinction.

## 1.5 Other codes

### 💡 Why extra codes exist

Plain binary is efficient, but sometimes you want a different property:
- You want to display digits on a 7-segment display without doing division → **BCD**
- You want a code where negating is easy for arithmetic circuits → **Excess-3**
- You want consecutive values to differ in only one bit, so a sensor never misreads during a transition → **Gray code**

**Gray code's motivation is worth understanding.** Imagine a rotating shaft with a position sensor reading 3 bits. Going from 3 (`011`) to 4 (`100`) in plain binary changes all three bits at once. If the three sensors do not switch at exactly the same instant, you might momentarily read `111` (= 7) or `000` (= 0) — a wildly wrong position. Gray code guarantees only **one** bit changes per step, so the worst-case misread is off by one.

### Reference

| Code | Description |
|---|---|
| **BCD** (8421) | Each **decimal digit** separately encoded in 4 bits. Only `0000`–`1001` valid; ⭐ `1010`–`1111` are **invalid** (6 wasted patterns per digit) |
| **Excess-3** | BCD + 0011. **Self-complementing** (the 9's complement of a digit is the 1's complement of its code) |
| ⭐ **Gray code** | ⭐ Successive values differ in **exactly one bit**. Used in shaft encoders and in K-map row/column ordering |
| **ASCII** | 7 bits (128 characters); extended ASCII uses 8 |
| **Unicode** | 16-bit+ (UTF-8 is variable length, 1–4 bytes) |

🔢 **BCD vs binary for 25:**
- Plain binary: `11001` (5 bits)
- BCD: `0010 0101` (digit 2, then digit 5 — 8 bits)

BCD wastes space but makes decimal display trivial.

### ⭐ Binary ↔ Gray conversion

📌 **Binary → Gray:** the MSB stays the same; then each Gray bit = **XOR of the two adjacent binary bits**, i.e. Gᵢ = Bᵢ₊₁ ⊕ Bᵢ.

🔢 **Convert `1011` to Gray:**
```
Binary:   1   0   1   1
           \ / \ / \ /
Gray:     1   1   1   0
```
- G₃ = B₃ = **1** (MSB copied)
- G₂ = B₃ ⊕ B₂ = 1 ⊕ 0 = **1**
- G₁ = B₂ ⊕ B₁ = 0 ⊕ 1 = **1**
- G₀ = B₁ ⊕ B₀ = 1 ⊕ 1 = **0**

Answer: **`1110`**

📌 **Gray → Binary:** the MSB stays; then each binary bit = **previous binary bit XOR current Gray bit** (a running/cumulative XOR from the left), i.e. Bᵢ = Bᵢ₊₁ ⊕ Gᵢ.

🔢 **Convert Gray `1110` back to binary:**
- B₃ = G₃ = **1**
- B₂ = B₃ ⊕ G₂ = 1 ⊕ 1 = **0**
- B₁ = B₂ ⊕ G₁ = 0 ⊕ 1 = **1**
- B₀ = B₁ ⊕ G₀ = 1 ⊕ 0 = **1**

Answer: **`1011`** ✅ (matches the original)

---

# 2. Computer arithmetic

## 2.1 Fixed point

### 💡 The idea

If you want to store 12.75, one option is to just **agree in advance** where the decimal point sits — say, 6 bits for the integer part and 2 for the fraction. Then `001100.11` means 12.75.

This is **fixed point**. It is simple and fast (the hardware treats it as an ordinary integer), but the range is rigid: with the point fixed at that position you can never store 1,000,000 or 0.001.

Integers are just fixed point with the point at the far right.

## 2.2 ⭐⭐ IEEE-754 floating point

### 💡 The idea

Scientists solved this range problem centuries ago with **scientific notation**:

```
0.000000045  →  4.5 × 10⁻⁸
45,000,000   →  4.5 × 10⁷
```

Same two-part shape (**a number between 1 and 10, times a power of 10**) covers a colossal range. Floating point is exactly this idea in binary:

```
value = ± (a number between 1 and 2) × 2^(some exponent)
```

The word "floating" means the binary point *moves* depending on the exponent — the opposite of fixed point.

So to store a float you need three pieces of information, and IEEE-754 packs them into one word:

```
┌─┬──────────┬───────────────────────┐
│S│ Exponent │       Mantissa        │
└─┴──────────┴───────────────────────┘
 1     8                23             = 32 bits (single precision)
```

- **S** — sign bit (0 = positive, 1 = negative)
- **Exponent** — the power of 2
- **Mantissa** (also called significand or fraction) — the digits of the number itself

### How it works — the two clever tricks

📌 ⭐ **value = (−1)^S × 1.M × 2^(E − bias)**

**Trick 1 — the biased exponent.** The exponent needs to be negative sometimes (for small numbers). Rather than making the exponent field itself a signed 2's complement number, IEEE-754 stores **actual exponent + bias**, so the stored value is always non-negative.

For single precision the bias is **127**. So:
- actual exponent −5 → stored as 122
- actual exponent 0 → stored as 127
- actual exponent +10 → stored as 137

*Why bother?* Because it makes floating-point numbers **comparable as if they were plain integers**. Two positive floats can be compared bit-by-bit from the left, which makes sorting and comparison hardware trivial.

📌 **bias = 2^(k−1) − 1** for a k-bit exponent field. For k = 8: 2⁷ − 1 = **127**.
⚠ ⭐ Exam options always include **128**. The bias is **127**.

**Trick 2 — the hidden (implicit) bit.** A normalised binary mantissa always looks like `1.something` — because if it started with 0 you would shift it and adjust the exponent. Since that leading 1 is *always* there, there is no point storing it.

⭐ So single precision stores 23 mantissa bits but gives you **24 bits of effective precision**. This is a free 1-bit accuracy gain.

### 🔢 Worked example — encode −6.5

**Step 1: convert 6.5 to binary.**
6 = `110`, 0.5 = `.1` → 6.5 = `110.1₂`

**Step 2: normalise** (shift so there is exactly one 1 before the point).
`110.1` = `1.101 × 2²` (we moved the point 2 places left, so the exponent is +2)

**Step 3: fill the three fields.**
- **S** = 1 (negative)
- **E** = actual exponent + bias = 2 + 127 = 129 = `10000001`
- **M** = the digits after the point: `101`, then pad with zeros to 23 bits

**Step 4: assemble.**
```
S    E          M
1  10000001  10100000000000000000000
```
Grouped in 4s for hex: `1100 0001 1101 0000 0000 0000 0000 0000` = **`C1D00000`₁₆**

### 🔢 Worked example — decode `41400000`₁₆

```
0100 0001 0100 0000 0000 0000 0000 0000
S = 0
E = 1000 0010 = 130  →  actual exponent = 130 − 127 = 3
M = 100 0000...      →  mantissa = 1.100₂ = 1.5
value = +1.5 × 2³ = 12.0
```

### ⭐ Reference

| Format | Total | Sign | Exponent | Mantissa | ⭐ Bias |
|---|---|---|---|---|---|
| ⭐ **Single precision** (`float`) | 32 | 1 | ⭐ **8** | 23 | ⭐ **127** |
| ⭐ **Double precision** (`double`) | 64 | 1 | ⭐ **11** | 52 | ⭐ **1023** |

⚠ Option "8 and 128" is the standard distractor; option "11 and 1023" is the double-precision trap.

### ⭐ Special values

Two exponent patterns are reserved to encode special cases:

| E (8 bits) | M | Meaning |
|---|---|---|
| `00000000` | 0 | ± **Zero** (there is a +0 and a −0) |
| `00000000` | ≠ 0 | ⭐ **Denormalised** — no hidden bit; value = 0.M × 2⁻¹²⁶ (lets you represent numbers even smaller than the normal minimum, at reduced precision) |
| `11111111` | 0 | ± **Infinity** (result of 1.0/0.0) |
| `11111111` | ≠ 0 | ⭐ **NaN** — Not a Number (result of 0.0/0.0 or √−1) |
| 1 to 254 | any | Normal number |

⭐ So the usable normalised exponent field is E = 1…254, giving actual exponents **−126 to +127**.

⚠ **Floating point is not exact.** Only numbers expressible as a finite sum of powers of 2 are exact. This is why you compare floats with `|a − b| < ε` rather than `a == b`.

---

# 3. Boolean algebra

## 💡 The idea

In ordinary algebra your variables hold numbers and your operators are + and ×. In **Boolean algebra** (George Boole, 1854) your variables hold only **0 or 1** — false or true, off or on — and the operators are **AND, OR, NOT**.

Boolean algebra is the mathematics of switching circuits. Claude Shannon's 1937 master's thesis pointed out that a network of relays behaves exactly like a Boolean expression — and that insight is the foundation of all digital design.

Its practical purpose in this exam is **simplification**. If a circuit implements `A·B + A·B'`, you want to notice that this is just `A`, because that means one wire instead of three gates. Fewer gates = cheaper, faster, less power.

### The three basic operations

| Operation | Written | Meaning | Truth |
|---|---|---|---|
| **AND** | A·B or AB | Output 1 only if **both** inputs are 1 | Like multiplication |
| **OR** | A + B | Output 1 if **at least one** input is 1 | Like addition (but 1+1 = 1) |
| **NOT** | A' or Ā | Inverts | |

⚠ Note `1 + 1 = 1` in Boolean algebra, not 2. There is no "2" — the only values are 0 and 1.

## 3.1 ⭐ The laws

Most of these look exactly like ordinary algebra, which is why they are easy. Focus your memorisation on the ones that **do not** have an ordinary-algebra counterpart.

| Law | AND form | OR form |
|---|---|---|
| Identity | A·1 = A | A + 0 = A |
| Null / dominance | A·0 = 0 | ⭐ **A + 1 = 1** |
| Idempotent | ⭐ **A·A = A** | ⭐ **A + A = A** |
| Complement | A·A' = 0 | A + A' = 1 |
| Involution | (A')' = A | |
| Commutative | AB = BA | A+B = B+A |
| Associative | A(BC) = (AB)C | A+(B+C) = (A+B)+C |
| Distributive | A(B+C) = AB + AC | ⭐ **A + BC = (A+B)(A+C)** |
| **Absorption** | A(A+B) = A | ⭐ **A + AB = A** |
| ⭐ **Absorption-2** | A(A'+B) = AB | ⭐ **A + A'B = A + B** |
| ⭐ **Consensus** | AB + A'C + BC = AB + A'C | (A+B)(A'+C)(B+C) = (A+B)(A'+C) |

The four to actually memorise, because they have no decimal analogue:
- ⭐ **A + 1 = 1** (once something is true, ORing anything keeps it true)
- ⭐ **A + A = A** (no "2A")
- ⭐ **A + AB = A** (absorption)
- ⭐ **A + A'B = A + B**

🔢 **Prove A + A'B = A + B** two ways.

*Algebraically:* A + A'B = (A + A')(A + B) [distributive] = 1·(A + B) = **A + B** ✅

*By truth table:*

| A | B | A' | A'B | A + A'B | A + B |
|---|---|---|---|---|---|
| 0 | 0 | 1 | 0 | 0 | 0 |
| 0 | 1 | 1 | 1 | **1** | **1** |
| 1 | 0 | 0 | 0 | **1** | **1** |
| 1 | 1 | 0 | 0 | **1** | **1** |

Columns match → identity holds ✅

*Intuitively:* "A is true, OR (A is false AND B is true)" — the second branch only matters when A is false, in which case it reduces to "B is true". So overall: A or B.

## 3.2 ⭐⭐ De Morgan's theorems

### 💡 The idea

These tell you how to push a NOT **through** an AND or an OR. They are the most-used identities in the whole subject and are asked directly almost every exam.

📌 ⭐ **(A + B)' = A' · B'**
📌 ⭐ **(A · B)' = A' + B'**

**In words:** the complement of a **sum** is the **product** of the complements, and vice versa. **Break the bar, change the sign.**

**Intuition with an everyday sentence:**
- "It is NOT (raining OR cold)" means "it is NOT raining AND NOT cold." → (A+B)' = A'B' ✅
- "It is NOT (sunny AND warm)" means "it is either not sunny OR not warm." (It does not mean both fail.) → (AB)' = A' + B' ✅

**Generalised rule:** to complement any expression — complement every variable **and** swap every AND ↔ OR.

🔢 **Simplify `(A + B + C)'`** → **A'·B'·C'**

🔢 **Simplify `(AB' + C)'`**
```
(AB' + C)' = (AB')' · C'          [De Morgan on the OR]
           = (A' + B'') · C'      [De Morgan on the AND]
           = (A' + B) · C'        [involution: B'' = B]
```

⚠ ⭐ **Duality is NOT the same as De Morgan.**
- **Duality principle:** swap AND ↔ OR and 0 ↔ 1. The identity stays valid, but you do **not** complement the variables. (Dual of `A + 1 = 1` is `A · 0 = 0`.)
- **De Morgan:** swap AND ↔ OR **and** complement all the variables — and this produces the *complement* of the expression, not an equivalent one.

## 3.3 ⭐ Canonical forms — minterms and maxterms

### 💡 The idea

Given a truth table, how do you write down the Boolean expression? There are two systematic ways, and both amount to "read the table off, row by row".

Suppose you have this function:

| Row | A | B | C | F |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 | **1** |
| 2 | 0 | 1 | 0 | 0 |
| 3 | 0 | 1 | 1 | **1** |
| 4 | 1 | 0 | 0 | 0 |
| 5 | 1 | 0 | 1 | **1** |
| 6 | 1 | 1 | 0 | 0 |
| 7 | 1 | 1 | 1 | **1** |

**Approach 1 — describe the rows where F = 1 (SOP).**
Row 1 is A=0, B=0, C=1. An AND term that is 1 *only* for that row is `A'B'C`. Such a term is called a **minterm**, written m₁.
Do this for every 1-row and OR them together:
```
F = A'B'C + A'BC + AB'C + ABC  =  Σm(1, 3, 5, 7)
```
This is the **Sum Of Products (SOP)** or **disjunctive normal form**.

**Approach 2 — describe the rows where F = 0 (POS).**
Row 0 is A=0, B=0, C=0. An OR term that is 0 *only* for that row is `(A + B + C)`. Such a term is a **maxterm**, M₀.
AND all the 0-row maxterms together:
```
F = (A+B+C)(A+B'+C)(A'+B+C)(A'+B'+C)  =  ΠM(0, 2, 4, 6)
```
This is the **Product Of Sums (POS)** or **conjunctive normal form**.

Both describe the same function. SOP is usually shorter when there are few 1s; POS when there are few 0s.

### ⚠ The convention trap

⭐ **Minterms and maxterms use OPPOSITE conventions**, and this catches people constantly:

| | Minterm (for SOP) | Maxterm (for POS) |
|---|---|---|
| Term type | Product (AND) | Sum (OR) |
| A variable appears **uncomplemented** when its bit is | **1** | **0** |
| A variable appears **complemented** when its bit is | **0** | **1** |

🔢 For the row A=1, B=0, C=1 (row 5): minterm m₅ = `AB'C`; maxterm M₅ = `A' + B + C'`. Note every literal is inverted between them.

📌 ⭐ **mᵢ' = Mᵢ** — a maxterm is the complement of the corresponding minterm.
📌 The minterm indices of F and the maxterm indices of F together cover all of 0…2ⁿ−1 with no overlap. (In our example: Σm(1,3,5,7) and ΠM(0,2,4,6).)
📌 The minterms of F' are exactly the indices missing from F's minterm list.

🔢 **Simplify F(A,B,C) = Σm(1,3,5,7).**
Look at the indices in binary: 001, 011, 101, 111. In every one, **C = 1**, and A and B take all possible combinations. So F is 1 exactly when C is 1, regardless of A and B:
⭐ **F = C**

That is a four-term expression collapsing to a single wire — which is the whole point of minimisation (§4).

### ⭐ Counting formulas

📌 With n variables there are **2ⁿ rows** in the truth table, hence **2ⁿ minterms** and 2ⁿ maxterms.
📌 ⭐ **Number of distinct Boolean functions of n variables = 2^(2ⁿ)**

*Why?* The truth table has 2ⁿ rows, and each row's output can independently be 0 or 1. So the number of possible output columns is 2 raised to the number of rows.

🔢 n = 2 → 2^4 = **16** functions of two variables (AND, OR, XOR, NAND, NOR, XNOR, A, B, A', B', 0, 1, and 4 more).
🔢 n = 3 → 2^8 = **256**.
🔢 n = 4 → 2^16 = **65,536**.

## 3.4 ⭐ Gates and universality

### 💡 The idea

A **gate** is the physical circuit that performs one Boolean operation. Seven matter:

| Gate | Expression | Behaviour in words |
|---|---|---|
| **AND** | A·B | 1 only if **all** inputs are 1 |
| **OR** | A+B | 1 if **any** input is 1 |
| **NOT** (inverter) | A' | Flips the input |
| ⭐ **NAND** | (A·B)' | AND then invert — 0 only if all inputs are 1 |
| ⭐ **NOR** | (A+B)' | OR then invert — 1 only if all inputs are 0 |
| ⭐ **XOR** | A⊕B = A'B + AB' | 1 when the inputs **differ** |
| **XNOR** | (A⊕B)' | 1 when the inputs are **equal** |

### ⭐ Universal gates

📌 ⭐ **NAND and NOR are universal** — you can build **any** Boolean function using only NAND gates, or only NOR gates.

**Why does that matter?** A chip factory would rather manufacture one kind of gate than seven. Since NAND alone is sufficient, entire processors can be (and historically were) built from nothing but NAND gates.

**Proof sketch — building everything from NAND:**
```
NOT A     = A NAND A                       (1 gate)
A AND B   = NOT(A NAND B) = (A NAND B) NAND (A NAND B)   (2 gates)
A OR B    = (NOT A) NAND (NOT B)           (3 gates)
```
Since {AND, OR, NOT} is enough to express any function (via SOP), and all three can be built from NAND, NAND is universal. ✅

⚠ ⭐ **AND, OR and XOR are NOT universal.** With only AND and OR you can never produce a complement, so you can never build NOT.

📌 **Gate counts when building from NAND:** NOT = 1, AND = 2, OR = 3, XOR = 4, XNOR = 5.

### ⭐ XOR properties (worth knowing separately)

📌 A⊕0 = A · A⊕1 = A' · **A⊕A = 0** · **A⊕A' = 1**
📌 XOR is **commutative and associative**, so a chain of XORs can be evaluated in any order.
📌 ⭐ An n-input XOR outputs **1 when an odd number of inputs are 1** — so XOR is a **parity detector**. This is why error-detection circuits (§Week 8's CRC and parity) are XOR trees.
📌 XOR is its own inverse: (A⊕B)⊕B = A. This is the basis of simple encryption and of swapping two variables without a temporary.

---

# 4. Minimization

## 💡 The idea

The SOP expression you read off a truth table is correct but **wasteful**. `Σm(1,3,5,7)` has four 3-input AND gates and a 4-input OR gate — but the function is just `C`, a bare wire.

**Minimisation** is the systematic process of finding the smallest equivalent expression. You could do it with the algebraic laws, but that requires spotting the right move. The **K-map** turns it into a visual, mechanical procedure.

## 4.1 ⭐⭐ K-maps (Karnaugh maps)

### How it works

A K-map is the truth table redrawn as a grid, with the rows and columns labelled in **Gray-code order** (00, 01, **11**, 10 — *not* 00, 01, 10, 11).

⭐ **The Gray-code ordering is the entire trick.** It guarantees that **physically adjacent cells differ in exactly one variable**. And when two minterms differ in exactly one variable, that variable cancels:
```
AB'C + ABC = AC(B' + B) = AC·1 = AC
```
So "circle two adjacent 1s" *is* "apply the simplification law". The map makes the algebra visible.

**A 3-variable map (A along the side, BC along the top):**
```
        BC
A     00   01   11   10
    ┌────┬────┬────┬────┐
 0  │ m0 │ m1 │ m3 │ m2 │
    ├────┼────┼────┼────┤
 1  │ m4 │ m5 │ m7 │ m6 │
    └────┴────┴────┴────┘
```
Note the column order `00 01 11 10`. Cell m1 (001) and m3 (011) are neighbours and differ only in B ✅

**A 4-variable map (AB down the side, CD along the top):**
```
         CD
AB    00   01   11   10
    ┌────┬────┬────┬────┐
 00 │ m0 │ m1 │ m3 │ m2 │
    ├────┼────┼────┼────┤
 01 │ m4 │ m5 │ m7 │ m6 │
    ├────┼────┼────┼────┤
 11 │m12 │m13 │m15 │m14 │
    ├────┼────┼────┼────┤
 10 │ m8 │ m9 │m11 │m10 │
    └────┴────┴────┴────┘
```

### ⭐ The rules

1. Plot a **1** in every cell whose minterm is in the function.
2. **Group the 1s** into rectangles whose size is a **power of 2** (1, 2, 4, 8, 16).
3. ⭐ Groups may **wrap around** the edges — the left column is adjacent to the right column, and the top row to the bottom row. (The map is really a torus.) ⭐ **The four corners of a 4-variable map form a valid group of 4.**
4. Make groups **as LARGE as possible**, and use **as FEW groups as possible**.
5. Groups may **overlap** — that is fine and often necessary.
6. Every 1 must be covered by at least one group.
7. Read each group as a product term: include only the variables that are **constant** across the whole group.

📌 ⭐ **A group of 2ᵏ cells eliminates k variables.** So:
- group of 2 → one variable drops out
- group of 4 → two variables drop out
- group of 8 → three variables drop out

**Bigger groups mean simpler terms — which is why rule 4 says "as large as possible".**

### 🔢 Worked example 1

**Minimise F(A,B,C) = Σm(1, 3, 5, 7).**
```
        BC
A     00   01   11   10
    ┌────┬────┬────┬────┐
 0  │ 0  │ 1  │ 1  │ 0  │
    ├────┼────┼────┼────┤
 1  │ 0  │ 1  │ 1  │ 0  │
    └────┴────┴────┴────┘
```
All four 1s form a single 2×2 block (the two middle columns). Across that block:
- A varies (0 and 1) → drops out
- B varies (0 and 1) → drops out
- C is **always 1** → keep as `C`

⭐ **F = C** ✅ (matching the algebraic answer from §3.3)

### 🔢 Worked example 2

**Minimise F(A,B,C,D) = Σm(0, 1, 2, 3, 8, 9, 10, 11).**
```
         CD
AB    00   01   11   10
    ┌────┬────┬────┬────┐
 00 │ 1  │ 1  │ 1  │ 1  │   ← m0,m1,m3,m2
    ├────┼────┼────┼────┤
 01 │ 0  │ 0  │ 0  │ 0  │
    ├────┼────┼────┼────┤
 11 │ 0  │ 0  │ 0  │ 0  │
    ├────┼────┼────┼────┤
 10 │ 1  │ 1  │ 1  │ 1  │   ← m8,m9,m11,m10
    └────┴────┴────┴────┘
```
The top row and bottom row are **adjacent by wrap-around**, so all eight 1s form one group of 8.
Across the group: C varies, D varies, A varies (00 and 10) — but **B is always 0**.

⭐ **F = B'** ✅ — eight minterms collapse to one inverter.

### 🔢 Worked example 3 (four corners)

**Minimise F(A,B,C,D) = Σm(0, 2, 8, 10).**
```
         CD
AB    00   01   11   10
    ┌────┬────┬────┬────┐
 00 │ 1  │ 0  │ 0  │ 1  │
    ├────┼────┼────┼────┤
 01 │ 0  │ 0  │ 0  │ 0  │
    ├────┼────┼────┼────┤
 11 │ 0  │ 0  │ 0  │ 0  │
    ├────┼────┼────┼────┤
 10 │ 1  │ 0  │ 0  │ 1  │
    └────┴────┴────┴────┘
```
The **four corners** are mutually adjacent by double wrap-around → one group of 4.
Across it: A varies, C varies; **B = 0 always**, **D = 0 always**.

⭐ **F = B'D'**

### ⭐ Implicant terminology

These four terms get asked as definitions:

| Term | Meaning |
|---|---|
| **Implicant** | Any valid group of 1s (i.e. any product term that implies F) |
| ⭐ **Prime implicant (PI)** | An implicant that **cannot be enlarged** into a bigger valid group |
| ⭐ **Essential prime implicant (EPI)** | A prime implicant that covers **at least one 1 that NO other prime implicant covers**. ⭐ **Every EPI must appear in the final answer** — there is no alternative way to cover that 1 |
| **Redundant PI** | A prime implicant all of whose 1s are already covered by other chosen groups — can be omitted |

⭐ **Minimisation procedure:** find all prime implicants → select all **essential** ones → cover any remaining 1s with the fewest additional PIs.

### ⭐ Don't-care conditions

### 💡 The idea

Sometimes an input combination **can never occur**, or you genuinely do not care what the output is. Example: a BCD digit is 0–9, so the input patterns 1010–1111 never happen. If someone feeds them in, any output is acceptable.

These are marked **X** (or d) on the map, and they are a **gift**: you may treat each X as **0 or 1, whichever makes your groups larger**.

⚠ Two rules:
1. You may include an X in a group if it helps enlarge it.
2. ⭐ **Never make a group consisting only of don't-cares** — that adds a term that covers no real 1.

🔢 **F(A,B,C,D) = Σm(1,3,7,11,15) with don't-cares d(0,2,5).**
Without the don't-cares you would need several small groups. Using X at m0 and m2 lets you form a group of 4 with m0,m1,m2,m3 → `A'B'`, and m3,m7,m11,m15 group to `CD`. Result: **F = A'B' + CD** — much simpler than the don't-care-free minimisation.

### ⭐ POS minimisation

To get the minimal **POS** form: group the **0s** instead of the 1s (this minimises F'), then complement the result using De Morgan.

🔢 F = Σm(1,3,5,7) → the 0s are m0,m2,m4,m6 → grouping them gives F' = C' → so **F = (C')' = C**, and in POS form the single sum term is just `C`.

## 4.2 Quine–McCluskey (tabular method)

### 💡 The idea

K-maps are visual, which means they stop being usable beyond about 5–6 variables (you cannot draw a 7-dimensional grid). **Quine–McCluskey** does the same job as a table, so a computer can run it.

**Steps:** group minterms by the number of 1s in their binary form → compare adjacent groups and combine any pair differing in exactly one bit (marking the differing position with a dash) → repeat until no more combining is possible; anything left uncombined is a **prime implicant** → build a **prime implicant chart** → pick the essential PIs → cover the rest minimally.

*Awareness level is sufficient for this exam* — expect at most a definitional question ("which method is suitable for computer implementation?" → Quine–McCluskey).

---

# 5. Combinational circuits

## 💡 The idea

📌 **A combinational circuit's output depends ONLY on its present inputs.** No memory, no feedback, no clock. Give it the same inputs and it gives the same output, every time, immediately.

Think of it as a **function** implemented in hardware: inputs go in the left, the answer comes out the right. Everything in §3 and §4 was about specifying and simplifying such functions; this section is about the standard, reusable building blocks.

## 5.1 ⭐ Multiplexer (MUX) — the data selector

### 💡 The idea

A multiplexer is an **electronically controlled selector switch**. It has several data inputs, one output, and some **select** lines that decide which input gets through.

Think of a TV with 4 input sources and a remote. The remote's 2 buttons (2 bits = 4 combinations) choose which source reaches the screen. That is a 4:1 MUX.

```
        ┌───────────┐
 I0 ───►│           │
 I1 ───►│   4 : 1   │───► Y
 I2 ───►│    MUX    │
 I3 ───►│           │
        └─────┬─────┘
              │
           S1   S0        (select lines)
```
If S1S0 = 10 (binary 2), then Y = I2.

📌 ⭐ **A 2ⁿ : 1 MUX has n select lines and 2ⁿ data inputs.**

| Size | Select lines | Data inputs |
|---|---|---|
| 2:1 | 1 | 2 |
| 4:1 | 2 | 4 |
| 8:1 | 3 | 8 |
| 16:1 | 4 | 16 |

**Boolean expression of a 4:1 MUX:**
`Y = S1'S0'I0 + S1'S0·I1 + S1S0'·I2 + S1S0·I3`

Notice: this is exactly a sum of minterms of the select variables, each gated by a data input.

### ⭐ Using a MUX to implement any function

That observation is the key exam skill. Since a 2ⁿ:1 MUX generates all 2ⁿ minterms of its select inputs, you can implement **any** n-variable function by:
- connecting the n variables to the **select** lines, and
- connecting each **data input** to the function's output value (0 or 1) for that row of the truth table.

🔢 **Implement F(A,B) = Σm(0,2) with a 4:1 MUX.**
Truth table gives F = 1 for AB = 00 and 10. So connect A,B to S1,S0 and set I0 = 1, I1 = 0, I2 = 1, I3 = 0. Done — no gates at all.

⭐ **The smaller trick — using a 2ⁿ⁻¹ : 1 MUX for an n-variable function.**

You can do better. Put **n − 1** variables on the select lines, and feed each data input with one of just four things: **0, 1, X, or X'** (where X is the leftover n-th variable).

🔢 **Implement F(A,B,C) = Σm(1,2,4,7) with a 4:1 MUX.**

Put A,B on the selects; C is the leftover variable. Examine the truth table two rows at a time:

| A B | C=0 | C=1 | F as a function of C | Data input |
|---|---|---|---|---|
| 0 0 | m0 = 0 | m1 = 1 | equals C | **I0 = C** |
| 0 1 | m2 = 1 | m3 = 0 | equals C' | **I1 = C'** |
| 1 0 | m4 = 1 | m5 = 0 | equals C' | **I2 = C'** |
| 1 1 | m6 = 0 | m7 = 1 | equals C | **I3 = C** |

So a 4:1 MUX plus one inverter implements a 3-variable function.

📌 ⭐ **Therefore an n-variable function needs a MUX of minimum size 2ⁿ⁻¹ : 1.**
🔢 A **4-variable** function needs a minimum **8:1** MUX.
🔢 A **3-variable** function needs a minimum **4:1** MUX.

⚠ A MUX is itself a **universal logic element** — any Boolean function can be built from MUXes alone.

## 5.2 ⭐ Demultiplexer, decoder, encoder

### 💡 The ideas

**Demultiplexer (DEMUX)** — the reverse of a MUX. One input, 2ⁿ outputs, n select lines route the input to the chosen output. Like one post office sorting a letter into one of many pigeonholes.

**Decoder** — n inputs, 2ⁿ outputs; **exactly one output is active** for each input combination. It "decodes" a binary number into a one-hot signal.

🔢 A **2-to-4 decoder**:

| A1 A0 | Y3 Y2 Y1 Y0 |
|---|---|
| 0 0 | 0 0 0 **1** |
| 0 1 | 0 0 **1** 0 |
| 1 0 | 0 **1** 0 0 |
| 1 1 | **1** 0 0 0 |

📌 ⭐ **An n-to-2ⁿ decoder generates all 2ⁿ minterms.** Therefore ⭐ **decoder + OR gates implements any function**: just OR together the outputs corresponding to the function's minterms.

🔢 To implement F(A,B,C) = Σm(1,3,5,7): use a 3-to-8 decoder and OR outputs Y1, Y3, Y5, Y7.

**Real-world use:** memory address decoding. A 10-bit address goes into a decoder to select exactly one of 1024 memory rows.

**Encoder** — the inverse of a decoder: 2ⁿ inputs, n outputs. It reports *which* input is active as a binary number.
⚠ Problem: if **two** inputs are active at once, a plain encoder's output is garbage.
⭐ **Priority encoder** solves this: if several inputs are active, the **highest-priority** one determines the output. Used in interrupt controllers (Week 2) to pick which device to service first.

## 5.3 ⭐ Adders

### 💡 The idea

The most important combinational circuit is the one that adds. Everything numeric a computer does reduces to addition (subtraction via 2's complement, multiplication via repeated shift-add).

**Half adder** — adds two bits, producing a sum and a carry:

| A | B | Sum | Carry |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | **0** | **1** |

📌 **Sum = A ⊕ B** and **Carry = A · B**

*Why is it "half"?* Because it cannot accept a carry **in** from a previous column. Real multi-bit addition needs that.

**Full adder** — adds three bits (A, B, and a carry-in):

📌 **Sum = A ⊕ B ⊕ C_in**
📌 **Carry_out = AB + C_in(A ⊕ B)** *(equivalently AB + BC_in + AC_in — "carry out if at least two inputs are 1")*

📌 ⭐ **A full adder = 2 half adders + 1 OR gate.**

*How:* the first half adder computes A⊕B and AB. The second adds C_in to that partial sum, producing the final Sum and a second carry. The two carries are ORed. (They can never both be 1, so OR is safe.)

```
A ──┐
    ├─HA1─── (A⊕B) ──┐
B ──┘   └── AB ──┐   ├─HA2─── Sum
                 │   │   └── (A⊕B)·Cin ──┐
      C_in ──────┼───┘                   ├─OR─── Carry_out
                 └───────────────────────┘
```

### ⭐ Ripple-carry adder — and why it is slow

Chain n full adders, feeding each carry-out into the next carry-in:

```
  A3B3      A2B2      A1B1      A0B0
   ││        ││        ││        ││
  ┌▼▼┐ C3  ┌▼▼┐ C2  ┌▼▼┐ C1  ┌▼▼┐
  │FA│◄────│FA│◄────│FA│◄────│FA│◄── C0
  └┬─┘     └┬─┘     └┬─┘     └┬─┘
   S3       S2       S1       S0
```

**The problem:** FA3 cannot compute its sum until C3 arrives, which needs C2, which needs C1, which needs C0. The carry **ripples** through every stage in turn.

📌 ⭐ **Delay ≈ n × (delay per full adder)** — linear in the word size.

🔢 A 32-bit ripple-carry adder with 2 ns per stage takes **64 ns**. For a processor running at 1 GHz (1 ns per cycle), that is hopeless.

### ⭐⭐ Carry Look-Ahead Adder (CLA) — the fix

### 💡 The idea

The insight: you do not have to *wait* for the carry — you can **predict** it directly from the inputs.

Think about when column i produces a carry into column i+1. Exactly two situations:

1. ⭐ **The column GENERATES a carry by itself** — both input bits are 1. `1 + 1 = 10`, carry out regardless of what came in.
   📌 **Gᵢ = Aᵢ · Bᵢ** (AND)
2. ⭐ **The column PROPAGATES an incoming carry** — exactly one input bit is 1. Then `1 + 0 + carry_in` produces a carry out only if carry_in was 1; the column passes it along.
   📌 **Pᵢ = Aᵢ ⊕ Bᵢ** (XOR)

📌 ⭐ **Cᵢ₊₁ = Gᵢ + Pᵢ · Cᵢ**

⚠ ⭐ **G uses AND; P uses XOR.** Do not swap them. Exam options always offer the reverse.

**Now expand the recursion:**
```
C1 = G0 + P0·C0
C2 = G1 + P1·C1 = G1 + P1·G0 + P1·P0·C0
C3 = G2 + P2·G1 + P2·P1·G0 + P2·P1·P0·C0
```
Every carry is now a **two-level (AND-OR) function of the original inputs and C0** — computable in **two gate delays**, no matter how far along the word it is.

📌 ⭐ **CLA carry delay is O(1)** (independent of n), at the cost of much more hardware (the expressions grow wide). Real designs compromise with block/hierarchical carry look-ahead.

## 5.4 Other combinational blocks

| Block | Function |
|---|---|
| **Subtractor** | Usually built as A + (2's complement of B) using the same adder |
| **Magnitude comparator** | Outputs A>B, A=B, A<B. Equality uses **XNOR** per bit |
| **BCD adder** | A binary adder plus correction logic: **add 6 when the sum exceeds 9** or generates a carry |
| **Parity generator/checker** | An **XOR tree**, since XOR detects odd parity |
| **Code converter** | Binary↔Gray, binary↔BCD, etc. |

🔢 **BCD adder:** 7 + 5 = 12. In binary, `0111 + 0101 = 1100` = 12, which is **not** a valid BCD digit. Add 6: `1100 + 0110 = 10010` → carry 1, digit `0010` = 2 → reads as "12" in BCD ✅

---

# 6. Sequential circuits

## 💡 The idea

Everything so far has been memoryless. But a computer must **remember** — it needs registers, counters, and state.

📌 **A sequential circuit's output depends on its present inputs AND on its stored state.** It achieves this with **feedback**: an output is wired back to an input, so the circuit's own past influences its present.

Think of a light switch versus a calculator. A switch is combinational — its state depends only on where you last pushed it *right now*. A calculator's display depends on the whole sequence of buttons you pressed — that requires memory.

| | **Combinational** | **Sequential** |
|---|---|---|
| Memory | ❌ No | ✅ Yes |
| Feedback | ❌ No | ✅ Yes |
| Clock | Not needed | Usually needed |
| Output depends on | Present inputs only | Present inputs **+ state** |
| Examples | Adder, MUX, decoder | Register, counter, FSM |

## 6.1 Latches vs flip-flops, and the clock

### 💡 The idea

If millions of memory elements each updated whenever their inputs happened to change, the machine would be chaos — races, glitches, unpredictable timing. The solution is a **clock**: a square wave that says "everybody update *now*". This is **synchronous** design, and it is why processors are described as "3 GHz" (3 billion update instants per second).

Two kinds of storage element:

| | **Latch** | ⭐ **Flip-flop** |
|---|---|---|
| Triggered by | **Level** — transparent for as long as the enable is high | ⭐ **Edge** — changes only on the clock's rising or falling edge |
| Behaviour | Follows the input while enabled | Samples the input once per clock edge |
| Used for | Simple storage, some ASIC designs | ⭐ Almost all synchronous logic |

**Flip-flops are preferred** because the update instant is unambiguous, which makes timing analysis possible.

## 6.2 ⭐⭐ The four flip-flops

### 💡 SR flip-flop — the starting point

Two inputs: **S** (Set → make output 1) and **R** (Reset → make output 0).

| S | R | Q(next) | Meaning |
|---|---|---|---|
| 0 | 0 | **Q** | Hold (remember) |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| 1 | 1 | ⭐ **Invalid** | "Set and reset at once" is contradictory |

📌 **Characteristic equation: Q(n+1) = S + R'Q**

⚠ ⭐ **S = R = 1 is forbidden** — the circuit's two outputs would both be forced to the same value, breaking the Q/Q' relationship, and on release the settled state is unpredictable (a race).

### 💡 JK flip-flop — the fix

JK is SR with the forbidden combination given a **useful** meaning: **toggle**.

| J | K | Q(next) | Meaning |
|---|---|---|---|
| 0 | 0 | **Q** | Hold |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| ⭐ **1** | ⭐ **1** | ⭐ **Q' (toggle)** | Flip to the opposite |

📌 **Q(n+1) = JQ' + K'Q**

⭐ Because it has no invalid state, JK is the most general flip-flop, and the others can be derived from it.

### 💡 D flip-flop — the simplest and most used

One input. Whatever D is at the clock edge becomes Q.

📌 ⭐ **Q(n+1) = D**

*"D" stands for Data or Delay* — it delays its input by one clock cycle. ⭐ **This is the flip-flop used to build registers and memory**, because "store this value" is by far the most common requirement.

Built from JK by setting J = D and K = D'.

### 💡 T flip-flop — the toggler

One input. T = 1 toggles, T = 0 holds.

📌 **Q(n+1) = T ⊕ Q**

⭐ Used in **counters**, since counting in binary is exactly a pattern of toggling.

Built from JK by tying J = K = T.

## 6.3 ⭐⭐ Excitation tables — the design tool

### 💡 The idea

The characteristic tables above answer: *"given the inputs, what happens to Q?"* — useful for **analysis**.

But when you **design** a circuit you have the opposite question: *"I need Q to go from 0 to 1 — what inputs must I apply?"* That is what an **excitation table** answers. It is the characteristic table read backwards.

⭐ **Memorise this table. Every sequential-design question is solved with it.**

| Q → Q(n+1) | S R | J K | D | T |
|---|---|---|---|---|
| **0 → 0** | 0 X | 0 X | 0 | 0 |
| **0 → 1** | 1 0 | 1 X | 1 | 1 |
| **1 → 0** | 0 1 | X 1 | 0 | 1 |
| **1 → 1** | X 0 | X 0 | 1 | 0 |

**X means "don't care"** — either value works, which is a bonus, because don't-cares make the K-map simplification much better.

**Reading a row:** to make Q go from 1 to 0 using a JK flip-flop, you need K = 1 and J can be anything (`X 1`).

**Sanity check the T column:** T must be 1 exactly when Q *changes* (0→1 and 1→0) and 0 when it stays. ✅ That is why T = Q ⊕ Q(next).

⭐ **Standard design procedure for a sequential circuit:**
1. Draw the **state diagram** from the problem statement.
2. Write the **state table** (present state, input → next state, output).
3. Assign binary codes to states (**state assignment**).
4. Use the excitation table to fill in the required **flip-flop inputs** for each transition.
5. **K-map** each flip-flop input as a function of present state and inputs.
6. Draw the circuit.

## 6.4 ⭐ The race-around condition

### 💡 The idea — a real bug and its fix

Take a **level-triggered** JK flip-flop and set J = K = 1 (toggle). While the clock is high, the circuit is transparent, so:
- Q toggles 0 → 1
- that new Q feeds back to the inputs
- the toggle condition is still active, so Q toggles 1 → 0
- …and so on, for as long as the clock stays high

📌 ⭐ **Race-around:** the output oscillates multiple times in one clock pulse, so the final state is unpredictable. It happens when the **clock pulse width > flip-flop propagation delay**.

⭐ **Fixes:**
1. ⭐ **Master–slave configuration** — the standard solution. Two latches in series driven by **opposite clock phases**:
   - While the clock is HIGH: the **master** follows the inputs; the **slave** is isolated (output frozen).
   - When the clock goes LOW: the master freezes; the **slave** copies the master.

   Since the slave (whose output feeds back) only changes when the master is frozen, ⭐ **exactly one toggle can occur per clock period.**
2. **Edge-triggering** (a narrow effective sampling window).
3. Making the clock pulse narrower than the propagation delay — theoretically valid, practically unusable.

⭐ **Exam answer: the race-around condition is eliminated by the master–slave configuration.**

## 6.5 ⭐ Counters

### 💡 The idea

A counter is a set of flip-flops that steps through a fixed sequence of states — 000, 001, 010, 011, … Used for counting events, generating addresses, dividing frequency, and timing.

### ⭐ Asynchronous (ripple) vs synchronous

**Asynchronous / ripple counter:** only the first flip-flop gets the real clock; each subsequent flip-flop is clocked by the **previous flip-flop's output**.

```
CLK ──►FF0──►FF1──►FF2──►FF3
        Q0    Q1    Q2    Q3
```
- ✅ Very simple, minimal hardware.
- ❌ ⭐ **Delays ADD UP: total delay = n × t_pd.** The change ripples through the chain, so during the settling time the counter shows **transient invalid states** (glitches). Feeding those to decoding logic causes spurious outputs.

**Synchronous counter:** all flip-flops share the **same clock**; combinational logic decides which ones should toggle.

```
      ┌──────┬──────┬──────┐
CLK ──┼──►FF0┼──►FF1┼──►FF2 ...   (all clocked together)
```
- ✅ ⭐ **Total delay = one flip-flop delay** (+ the combinational logic) — fast, and no glitch states.
- ❌ More gates.

🔢 A 4-bit **ripple** counter with 10 ns per flip-flop settles in 4 × 10 = **40 ns**. A 4-bit **synchronous** counter settles in **10 ns**. That factor-of-n difference is the whole reason synchronous design dominates.

### ⭐ Sizing formulas

📌 ⭐ **Flip-flops needed for a MOD-N counter = ⌈log₂ N⌉**
📌 ⭐ **Maximum modulus with n flip-flops = 2ⁿ**

*Why:* n flip-flops give 2ⁿ distinct patterns, and you need at least N of them.

🔢 **MOD-12 counter:** ⌈log₂12⌉ = ⌈3.58⌉ = **4** flip-flops. (3 would give only 8 states — not enough.) With 4 flip-flops you must add logic to reset after state 11, skipping the 4 unused states.
🔢 **MOD-16:** exactly 4 flip-flops, no skipping needed.
🔢 **MOD-100:** ⌈log₂100⌉ = **7** flip-flops.

⚠ "MOD-N" means **N distinct states**, not N flip-flops.

### ⭐ Ring and Johnson counters

### 💡 The idea

These are shift registers wired into a loop, and they are asked about specifically because their state counts are counter-intuitive.

**Ring counter:** a shift register whose last output feeds back into the first input. Load a single 1 and it circulates:
```
1000 → 0100 → 0010 → 0001 → 1000 → ...
```
📌 ⭐ **n flip-flops give n states.**
✅ Advantage: the state is already one-hot, so **no decoder is needed**. ❌ Very inefficient use of flip-flops.

**Johnson (twisted-ring / switch-tail) counter:** same, but the last output is **complemented** before feeding back:
```
0000 → 1000 → 1100 → 1110 → 1111 → 0111 → 0011 → 0001 → 0000 → ...
```
📌 ⭐ **n flip-flops give 2n states** — double the ring counter, for the same hardware.

⚠ ⭐ **Ring = n states, Johnson = 2n states.** Do not swap them.

🔢 A 4-bit ring counter has **4** states; a 4-bit Johnson counter has **8**; a 4-bit binary counter has **16**.

## 6.6 Shift registers

### 💡 The idea

A chain of D flip-flops where each one's output feeds the next one's input. On every clock, the whole contents shift one position.

**Four types**, by how data enters and leaves:

| Type | Meaning |
|---|---|
| **SISO** | Serial In, Serial Out |
| **SIPO** | Serial In, Parallel Out — ⭐ **serial-to-parallel conversion** |
| **PISO** | Parallel In, Serial Out — ⭐ **parallel-to-serial conversion** |
| **PIPO** | Parallel In, Parallel Out — a plain register |

**Uses:** serial↔parallel conversion (UART/network interfaces) · delay lines · ⭐ **multiplication/division by 2** (left shift = ×2, right shift = ÷2) · sequence generation · ring/Johnson counters.

🔢 `0011` (3) shifted left → `0110` (6) ✅ · shifted right → `0001` (1, integer division) ✅

## 6.7 ⭐⭐ Finite state machines: Mealy vs Moore

### 💡 The idea

A **finite state machine (FSM)** is the general model of any sequential circuit: a finite set of states, transitions between them driven by inputs, and outputs. Traffic-light controllers, vending machines, protocol handlers and processor control units are all FSMs.

There are exactly two ways to decide the output, and the distinction is one of the most reliably asked comparisons in Digital Logic.

⭐ **Moore machine — output depends on the STATE only.**
Each state has an output written *inside* the circle. The output changes only when the state changes, i.e. only on a clock edge.

```
      ┌────────┐   1    ┌────────┐
 ────►│ S0 / 0 │───────►│ S1 / 1 │
      └────────┘◄───────└────────┘
                    0
```
(Output 0 in S0, output 1 in S1 — written with the state.)

⭐ **Mealy machine — output depends on the STATE AND the current INPUT.**
Outputs are written *on the transition arrows* as `input / output`.

```
      ┌────┐   1 / 1    ┌────┐
 ────►│ S0 │───────────►│ S1 │
      └────┘◄───────────└────┘
              0 / 0
```

### ⭐ Comparison

| | ⭐ **Moore** | ⭐ **Mealy** |
|---|---|---|
| Output is a function of | ⭐ **Present state ONLY** | ⭐ **Present state + present input** |
| Output shown | In the state (circle) | On the transition (arrow) |
| Number of states | Usually **more** | Usually **fewer** |
| Output timing | Changes only on a clock edge — ⭐ **synchronous, glitch-free** | Reacts **immediately** to input; ⭐ can glitch |
| Response speed | One clock cycle later | Same cycle |

⭐ **Both models are equally powerful** — any Mealy machine has an equivalent Moore machine and vice versa. The choice is an engineering trade-off: **Mealy is faster and smaller; Moore is safer and easier to time.**

🔢 **Practical intuition:** for a circuit that detects the input sequence `101`, a Mealy machine needs 3 states and asserts the output the instant the final 1 arrives. A Moore machine needs 4 states (an extra "detected" state) and asserts the output one clock later.

---

# 7. Logic families (awareness only)

### 💡 The idea

The same Boolean function can be built with different transistor technologies, trading speed against power. You only need the comparison.

| Family | Speed | Power | Note |
|---|---|---|---|
| **TTL** (Transistor-Transistor Logic) | Moderate | Moderate | Bipolar, totem-pole output; the 74xx series |
| ⭐ **CMOS** | Moderate–fast | ⭐ **Very low static power** | Dominant technology; high noise immunity, high fan-out. Draws power mainly when **switching** |
| **ECL** (Emitter-Coupled Logic) | ⭐ **Fastest** | Highest | Non-saturating transistors |

**Key terms:**

| Term | Meaning |
|---|---|
| **Fan-out** | How many gate inputs one output can reliably drive |
| **Fan-in** | Number of inputs a gate has |
| **Noise margin** | How much voltage noise can be tolerated before a 0 is misread as a 1 |
| **Propagation delay** | Time from input change to output change |
| **Power–delay product** | The standard figure of merit (lower is better) |
| ⭐ **Tri-state buffer** | Outputs 0, 1, or **high-impedance (Z)** — effectively disconnecting itself. ⭐ This is what lets many devices **share one bus**: all but one go to Z |

---

# 8. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| 8-bit 2's complement range | −128 to +127 |
| 2's complement | 1's complement + 1 |
| Signed overflow | C_in(MSB) ⊕ C_out(MSB) |
| Opposite-sign addition | Can never overflow |
| Boolean functions of n variables | 2^(2ⁿ) |
| Minterms of n variables | 2ⁿ |
| IEEE-754 single precision | 1 + 8 + 23, bias **127** |
| IEEE-754 double precision | 1 + 11 + 52, bias 1023 |
| Hidden bit gives | 24 bits of precision from 23 stored |
| E = all 1s, M = 0 / M ≠ 0 | Infinity / NaN |
| Universal gates | **NAND, NOR** |
| XOR detects | Odd parity |
| A + A'B | A + B |
| (A+B+C)' | A'B'C' |
| Group of 2ᵏ cells in a K-map | Eliminates k variables |
| Essential prime implicant | Covers a 1 no other PI covers |
| Don't-care rule | Never group only don't-cares |
| Method for many variables | Quine–McCluskey |
| 2ⁿ:1 MUX select lines | n |
| Min MUX for n-variable function | **2ⁿ⁻¹ : 1** |
| Decoder outputs for n inputs | 2ⁿ |
| Decoder generates | All minterms |
| Full adder from half adders | **2 HA + 1 OR** |
| CLA generate / propagate | **Gᵢ = AᵢBᵢ (AND) / Pᵢ = Aᵢ⊕Bᵢ (XOR)** |
| CLA carry equation | Cᵢ₊₁ = Gᵢ + PᵢCᵢ |
| SR forbidden input | S = R = 1 |
| JK with J = K = 1 | **Toggle** |
| D flip-flop | Q(n+1) = D |
| T flip-flop | Q(n+1) = T ⊕ Q |
| Race-around fix | **Master–slave** |
| MOD-N counter flip-flops | ⌈log₂N⌉ |
| Ring / Johnson counter states | **n / 2n** |
| Ripple counter delay | n × t_pd |
| Synchronous counter delay | t_pd |
| Left / right shift | ×2 / ÷2 |
| Moore output | Present **state only** |
| Mealy output | State **+ input** |
| Fewer states | Mealy |
| Glitch-free output | Moore |
| Lets devices share a bus | Tri-state buffer |
| Gray code property | Adjacent codes differ in 1 bit |
| BCD invalid codes | 1010–1111 (6 per digit) |
| BCD adder correction | Add 6 when sum > 9 |

---

# 9. ⚠ Common traps

1. ⭐ **1's vs 2's complement** — invert, *then add 1*. The 1's complement is always an option.
2. ⭐ **IEEE single-precision bias is 127, not 128.**
3. ⭐ **CLA: Generate uses AND; Propagate uses XOR** — never the reverse.
4. **Ripple counter delays add; synchronous counter delays do not.**
5. ⭐ **Ring = n states; Johnson = 2n states.**
6. ⭐ **Moore = state only; Mealy = state + input.**
7. ⭐ **Maxterm convention is inverted** relative to minterms (a variable is complemented when its bit is **1**).
8. ⭐ **Duality ≠ De Morgan.** Duality swaps AND/OR and 0/1 only; De Morgan also complements the variables.
9. **"MOD-N" means N states**, not N flip-flops.
10. ⭐ **Signed and unsigned overflow are different tests** — a carry-out alone detects only unsigned overflow.
11. **Height/level conventions:** if a K-map question numbers cells differently, re-derive rather than assume.
12. **K-map groups wrap around edges** — and the four corners of a 4-variable map are one valid group.
13. **A group of only don't-cares is invalid.**
14. **The minimum MUX for an n-variable function is 2ⁿ⁻¹:1, not 2ⁿ:1.**

---

# 10. Practice

- GATE: [`Paper2_S02_Digital_Logic/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S02_Digital_Logic/) — **313 questions**
- State-PSC level: [`Paper2_S02_Digital_Logic/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S02_Digital_Logic/) — **309 questions**
- Test: [`Week_01_Test.md`](../04_Mock_Tests/Week_01_Test.md)

**Priority order if short on time:** number representation & 2's complement → IEEE-754 → K-map minimisation → MUX/decoder implementation → flip-flop excitation table → counters (MOD-N, ring, Johnson) → Mealy vs Moore → De Morgan.
