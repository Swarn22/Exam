# Week 1 — Digital Logic & Number Systems

**Syllabus §2:** Boolean algebra. Combinational and sequential circuits. Minimization. Number representations and computer arithmetic (fixed and floating point).
**Estimated marks: ~9**

---

## 1. Number systems

### 1.1 Bases and conversion

| Base | Name | Digits |
|---|---|---|
| 2 | Binary | 0–1 |
| 8 | Octal | 0–7 |
| 10 | Decimal | 0–9 |
| 16 | Hexadecimal | 0–9, A–F |

**Binary → Octal:** group in **3** bits from the radix point outwards.
**Binary → Hex:** group in **4** bits from the radix point outwards.

🔢 `10110110₂` → `1011|0110` → **B6₁₆**; → `010|110|110` → **266₈**

**Decimal → any base:** repeatedly divide the integer part (read remainders bottom-up); repeatedly multiply the fraction part (read the integer parts top-down).

🔢 0.625 → 0.625×2 = **1**.25 → 0.25×2 = **0**.5 → 0.5×2 = **1**.0 → `0.101₂`

📌 Number of digits needed to represent decimal N in base b = ⌊log_b N⌋ + 1

### 1.2 Signed number representations (n bits)

| Representation | Range | Zero | Notes |
|---|---|---|---|
| Unsigned | 0 to 2ⁿ − 1 | one | |
| Signed magnitude | −(2ⁿ⁻¹ − 1) to +(2ⁿ⁻¹ − 1) | **two** (+0, −0) | MSB = sign |
| 1's complement | −(2ⁿ⁻¹ − 1) to +(2ⁿ⁻¹ − 1) | **two** | complement every bit |
| ⭐ **2's complement** | **−2ⁿ⁻¹ to +2ⁿ⁻¹ − 1** | **one** | 1's complement + 1 |

⭐ **For 8 bits, 2's complement range is −128 to +127.** The asymmetry (one extra negative) is because there is only one zero.

**Taking the 2's complement — two methods:**
1. Invert all bits, add 1.
2. Faster: copy bits from the right up to and including the first `1`, then invert everything to the left.

🔢 2's complement of `01011010`: invert → `10100101`, +1 → **`10100110`**
⚠ `10100101` is the **1's** complement. This is the single most common slip in this topic.

**Why 2's complement wins:** subtraction becomes addition (A − B = A + 2's_comp(B)), there is one zero, and the sign bit participates in arithmetic normally.

### 1.3 Overflow detection ⭐

For **2's complement addition**, overflow occurs when:
- Both operands are **positive** and the result is **negative**, or
- Both operands are **negative** and the result is **positive**.

📌 Equivalently: **overflow = C_in(MSB) ⊕ C_out(MSB)** — the carry into the sign bit differs from the carry out of it.

⚠ Adding numbers of **opposite** signs can never overflow.
⚠ For **unsigned** addition, overflow is simply the final carry-out = 1. Signed and unsigned overflow are different conditions.

### 1.4 Other codes

| Code | Description |
|---|---|
| **BCD** (8421) | Each decimal digit → 4 bits. Only 0000–1001 valid; 1010–1111 illegal. 6 wasted codes/digit. |
| **Excess-3** | BCD + 0011. Self-complementing. |
| **Gray code** | Successive values differ in exactly **one** bit. Used in shaft encoders and K-maps. |
| **ASCII** | 7 bits (128 chars); extended ASCII 8 bits |
| **Unicode** | 16-bit+ (UTF-8 is variable length, 1–4 bytes) |

⭐ **Binary → Gray:** MSB stays; then Gᵢ = Bᵢ₊₁ ⊕ Bᵢ.
🔢 `1011` → G₃ = 1; G₂ = 1⊕0 = 1; G₁ = 0⊕1 = 1; G₀ = 1⊕1 = 0 → **`1110`**

**Gray → Binary:** MSB stays; then Bᵢ = Bᵢ₊₁ ⊕ Gᵢ (cumulative XOR from the left).

---

## 2. Computer arithmetic

### 2.1 Fixed point
The radix point is at a fixed position. Integers are the special case with the point at the far right. Simple and fast, but limited range.

### 2.2 ⭐ IEEE-754 floating point

📌 **Value = (−1)^S × 1.M × 2^(E − bias)** (for normalised numbers)

| Format | Total | Sign | Exponent | Mantissa | Bias |
|---|---|---|---|---|---|
| **Single precision** (float) | 32 | 1 | **8** | 23 | **127** |
| **Double precision** (double) | 64 | 1 | **11** | 52 | **1023** |

⚠ Option "8 and 128" is the classic distractor — the bias is **127**, not 128 (bias = 2^(k−1) − 1 for a k-bit exponent).

**The implicit/hidden bit:** normalised mantissas are `1.xxxxx`, and the leading 1 is not stored. So single precision gives **24 bits of effective precision** from 23 stored bits.

**Special values (single precision):**

| E (8 bits) | M | Meaning |
|---|---|---|
| 00000000 | 0 | ± Zero |
| 00000000 | ≠ 0 | **Denormalised** (no hidden bit; value = 0.M × 2^−126) |
| 11111111 | 0 | ± Infinity |
| 11111111 | ≠ 0 | **NaN** (Not a Number) |
| 1–254 | any | Normalised number |

So the usable normalised exponent range is E = 1…254 → actual exponent −126 to +127.

🔢 **Represent −6.5 in single precision.**
6.5₁₀ = `110.1₂` = 1.101 × 2². S = 1. E = 2 + 127 = 129 = `10000001`. M = `101` then zeros.
→ `1 10000001 10100000000000000000000` = **`C1D00000`₁₆**

---

## 3. Boolean algebra

### 3.1 Basic laws

| Law | AND form | OR form |
|---|---|---|
| Identity | A·1 = A | A + 0 = A |
| Null / dominance | A·0 = 0 | A + 1 = 1 |
| Idempotent | A·A = A | A + A = A |
| Complement | A·A' = 0 | A + A' = 1 |
| Involution | (A')' = A | |
| Commutative | AB = BA | A+B = B+A |
| Associative | A(BC) = (AB)C | A+(B+C) = (A+B)+C |
| Distributive | A(B+C) = AB + AC | **A + BC = (A+B)(A+C)** |
| **Absorption** | A(A+B) = A | A + AB = A |
| **Absorption-2** ⭐ | A(A'+B) = AB | **A + A'B = A + B** |
| Consensus ⭐ | AB + A'C + BC = AB + A'C | (A+B)(A'+C)(B+C) = (A+B)(A'+C) |

⭐ **De Morgan's theorems** — asked directly, almost every exam:
📌 **(A + B)' = A'·B'**  and  **(A·B)' = A' + B'**
Generalised: complement the whole expression by complementing each variable and swapping AND ↔ OR.

**Duality principle:** swap AND ↔ OR and 0 ↔ 1; the identity remains valid. (Duality does *not* complement the variables — De Morgan does.)

### 3.2 Canonical forms

For n variables there are **2ⁿ minterms** and **2ⁿ maxterms**.

| Form | Built from | Notation |
|---|---|---|
| **SOP** (Sum of Products) | minterms (where F = 1) | F = Σm(…) |
| **POS** (Product of Sums) | maxterms (where F = 0) | F = ΠM(…) |

- **Minterm mᵢ**: product term; variable appears **uncomplemented if its bit is 1**.
- **Maxterm Mᵢ**: sum term; variable appears **complemented if its bit is 1** (the reverse convention).
- 📌 **mᵢ' = Mᵢ**
- The minterm indices of F and the maxterm indices of F together cover all 0…2ⁿ−1.

🔢 F(A,B,C) = Σm(1,3,5,7) → these are exactly the odd indices → **F = C**. (All rows where C = 1.)

⭐ **Number of distinct Boolean functions of n variables = 2^(2ⁿ)**. For n = 3 → 2⁸ = **256**.

### 3.3 Gates and universality

| Gate | Expression | Notes |
|---|---|---|
| AND | A·B | |
| OR | A+B | |
| NOT | A' | |
| **NAND** | (A·B)' | ⭐ **Universal** |
| **NOR** | (A+B)' | ⭐ **Universal** |
| **XOR** | A⊕B = A'B + AB' | 1 when inputs **differ**; odd-parity detector |
| **XNOR** | (A⊕B)' | 1 when inputs are **equal**; equality comparator |

⭐ Only **NAND and NOR** are universal. AND, OR and XOR are not.

**Gates needed to build others from NAND:** NOT = 1, AND = 2, OR = 3, XOR = 4, XNOR = 5.

**XOR properties:** A⊕0 = A · A⊕1 = A' · A⊕A = 0 · A⊕A' = 1 · associative and commutative.
An n-input XOR outputs 1 when an **odd** number of inputs are 1.

---

## 4. Minimization

### 4.1 K-maps (Karnaugh maps)

- Cells are arranged in **Gray-code order** so adjacent cells differ in one variable.
- Group **1s** in powers of 2 (1, 2, 4, 8, …). Groups may wrap around edges and corners.
- Make groups **as large as possible** and **as few as possible**.
- A group of 2ᵏ cells eliminates k variables.

| Term | Meaning |
|---|---|
| **Implicant** | Any group of 1s (a valid product term) |
| **Prime implicant** | An implicant that cannot be combined into a larger group |
| ⭐ **Essential prime implicant** | A prime implicant covering at least one 1 that **no other prime implicant covers** |
| **Redundant PI** | A prime implicant all of whose 1s are covered by others |

**Don't-care (X / d) conditions:** may be treated as 0 or 1 — whichever makes groups larger. Never make a group of only don't-cares.

⭐ For POS minimization, group the **0s** and complement the result (or read the groups as sum terms with inverted literals).

### 4.2 Quine–McCluskey (tabular method)
Systematic, computer-implementable alternative to K-maps; works for any number of variables. Steps: group minterms by number of 1s → combine terms differing in one bit → repeat until no combination possible → prime implicant chart → select essential PIs → cover the rest minimally.
*Awareness level is enough — expect at most a definitional question.*

---

## 5. Combinational circuits

**Definition:** output depends **only on the present inputs**; no memory, no feedback.

### 5.1 Multiplexer (MUX) — data selector

| Size | Select lines | Data inputs |
|---|---|---|
| 2:1 | 1 | 2 |
| 4:1 | 2 | 4 |
| 8:1 | 3 | 8 |
| 2ⁿ:1 | n | 2ⁿ |

📌 A 2ⁿ:1 MUX needs **n select lines**.

⭐ **Implementing an n-variable function with a MUX:**
- Using a **2ⁿ:1** MUX: connect the n variables to the select lines and the minterm values (0/1) to the data inputs. Always possible, directly from the truth table.
- Using a **2ⁿ⁻¹:1** MUX: connect n−1 variables to selects; each data input gets one of **0, 1, X, X'** (the n-th variable). **This is the minimum size needed.**

🔢 A 4-variable function needs a minimum **8:1** MUX.

⚠ A MUX is itself a universal logic element — any Boolean function can be realised with one.

### 5.2 Demultiplexer / Decoder

- **DEMUX:** 1 input → 2ⁿ outputs, selected by n control lines.
- ⭐ **Decoder:** n inputs → **2ⁿ** outputs; exactly one output active per input combination. An n:2ⁿ decoder generates all 2ⁿ minterms, so **decoder + OR gates implements any function**.
- **Priority encoder:** if several inputs are active, the highest-priority one determines the output. Resolves the ambiguity a plain encoder has.
- **Encoder:** 2ⁿ inputs → n outputs (inverse of a decoder).

### 5.3 Adders

**Half adder:** Sum = A ⊕ B; Carry = A·B
**Full adder:** Sum = A ⊕ B ⊕ C_in; Carry = AB + C_in(A ⊕ B)

⭐ A full adder = **2 half adders + 1 OR gate**.

**Ripple-carry adder:** n full adders chained. The carry must propagate through all stages.
📌 Delay ≈ **n × (delay per full adder)** — slow, and grows linearly with n.

⭐ **Carry Look-Ahead Adder (CLA):**
📌 **Generate Gᵢ = Aᵢ · Bᵢ** (a carry is created here)
📌 **Propagate Pᵢ = Aᵢ ⊕ Bᵢ** (an incoming carry passes through)
📌 **Cᵢ₊₁ = Gᵢ + Pᵢ · Cᵢ**

Expanding this recursion gives every carry as a 2-level function of the inputs → carry delay becomes **O(1)** (independent of n) at the cost of much more hardware.
⚠ Do not swap G and P. G uses **AND**, P uses **XOR**.

**Other blocks:** subtractor (A + 2's comp of B), magnitude comparator, BCD adder (add 6 when the sum exceeds 9), parity generator/checker (XOR tree).

---

## 6. Sequential circuits

**Definition:** output depends on present inputs **and** the stored state. Contains memory (flip-flops) and feedback.

| | Combinational | Sequential |
|---|---|---|
| Memory | No | Yes |
| Feedback | No | Yes |
| Clock | Not needed | Usually needed |
| Output depends on | Present inputs only | Present inputs + state |

### 6.1 Latches vs flip-flops
- **Latch:** level-triggered (transparent while the enable is active).
- **Flip-flop:** edge-triggered (changes only on a clock edge). Preferred for synchronous design.

### 6.2 Flip-flop characteristic tables ⭐

**SR flip-flop** (S = Set, R = Reset)

| S | R | Q(next) |
|---|---|---|
| 0 | 0 | Q (no change) |
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | **Invalid / forbidden** |

📌 Characteristic equation: **Q(n+1) = S + R'Q**

**JK flip-flop** — fixes SR's invalid state

| J | K | Q(next) |
|---|---|---|
| 0 | 0 | Q |
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| **1** | **1** | **Q' (toggle)** ⭐ |

📌 **Q(n+1) = JQ' + K'Q**

**D flip-flop** (Data / Delay) — 📌 **Q(n+1) = D**. Used for registers and data storage.

**T flip-flop** (Toggle) — 📌 **Q(n+1) = T ⊕ Q**. T = 1 toggles, T = 0 holds. Used in counters.

### 6.3 ⭐ Excitation tables (needed for circuit design)

| Q → Q(n+1) | S R | J K | D | T |
|---|---|---|---|---|
| 0 → 0 | 0 X | 0 X | 0 | 0 |
| 0 → 1 | 1 0 | 1 X | 1 | 1 |
| 1 → 0 | 0 1 | X 1 | 0 | 1 |
| 1 → 1 | X 0 | X 0 | 1 | 0 |

**Memorise this table.** Circuit-design questions ("what is the minimum logic to implement…") are solved by writing the excitation table, then K-mapping each flip-flop input.

### 6.4 Race-around condition ⭐
In a **level-triggered** JK flip-flop with J = K = 1, the output toggles repeatedly for as long as the clock is high (if the clock pulse width > propagation delay).

**Fixes:**
1. ⭐ **Master–slave configuration** (two latches in series, on opposite clock phases) — allows exactly one toggle per clock period.
2. Edge-triggering.
3. Clock pulse width < propagation delay (impractical).

### 6.5 Counters

**Asynchronous (ripple) counter:** the output of one flip-flop clocks the next.
📌 Total delay = **n × t_pd** (delays add up) — simple but slow, with transient invalid states.

**Synchronous counter:** all flip-flops share the same clock.
📌 Total delay = **t_pd** (one flip-flop delay) plus combinational logic — faster, no glitches.

⭐ 📌 **Flip-flops needed for a MOD-N counter = ⌈log₂N⌉**
🔢 MOD-12 → ⌈log₂12⌉ = **4** flip-flops (3 would give only 8 states).

⭐ 📌 **Maximum modulus of an n-flip-flop counter = 2ⁿ**

| Counter type | States with n flip-flops |
|---|---|
| Binary (up/down) | 2ⁿ |
| ⭐ **Ring counter** | **n** |
| ⭐ **Johnson (twisted-ring) counter** | **2n** |

A ring counter circulates a single 1 through n positions. A Johnson counter feeds back the **complement** of the last stage, doubling the state count.

### 6.6 Shift registers
Types: SISO, SIPO, PISO, PIPO. Uses: serial↔parallel conversion, delay lines, multiplication/division by 2 (left/right shift), sequence generation.

### 6.7 ⭐ Finite state machines: Mealy vs Moore

| | **Moore** | **Mealy** |
|---|---|---|
| Output is a function of | **Present state only** | **Present state + present input** |
| Output shown on | States (in the circle) | Transitions (on the arrow) |
| Number of states | Usually **more** | Usually **fewer** |
| Output timing | Synchronous with the clock; **glitch-free** | Reacts immediately; can glitch |
| Response speed | One clock later | Same cycle |

⚠ This is one of the most reliably asked comparison questions in Digital Logic. Both are equally powerful — any Mealy machine has an equivalent Moore machine, and vice versa.

**Design steps for a synchronous sequential circuit:** state diagram → state table → state assignment → excitation table → K-map each flip-flop input → draw circuit.

---

## 7. Logic families (awareness)

| Family | Speed | Power | Notes |
|---|---|---|---|
| TTL | Moderate | Moderate | Totem-pole output |
| **CMOS** | Moderate–fast | **Very low static** | Dominant technology; high noise immunity, high fan-out |
| ECL | **Fastest** | Highest | Non-saturating |

**Fan-out:** the maximum number of gate inputs one output can drive.
**Noise margin:** the tolerance to voltage noise before misinterpretation.
**Propagation delay:** input change → output change.
**Tri-state buffer:** outputs 0, 1 or high-impedance (Z) — enables shared buses.

---

## 8. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| 8-bit 2's complement range | −128 to +127 |
| Boolean functions of n variables | 2^(2ⁿ) |
| Minterms of n variables | 2ⁿ |
| IEEE-754 single precision | 1 + 8 + 23, bias 127 |
| IEEE-754 double precision | 1 + 11 + 52, bias 1023 |
| Universal gates | NAND, NOR |
| MUX select lines for 2ⁿ:1 | n |
| Decoder outputs for n inputs | 2ⁿ |
| Min MUX for n-variable function | 2ⁿ⁻¹ : 1 |
| Full adder from half adders | 2 HA + 1 OR |
| CLA: generate / propagate | Gᵢ = AᵢBᵢ / Pᵢ = Aᵢ⊕Bᵢ |
| JK with J=K=1 | Toggle |
| MOD-N counter flip-flops | ⌈log₂N⌉ |
| Ring / Johnson counter states | n / 2n |
| Ripple counter delay | n × t_pd |
| Race-around fix | Master–slave |
| Moore output | Present state only |
| A + A'B | A + B |
| (A+B+C)' | A'B'C' |
| Gray code property | Adjacent codes differ in 1 bit |
| BCD invalid codes | 1010–1111 (6 per digit) |

---

## 9. Common traps ⚠

1. **1's vs 2's complement** — invert, *then add 1*.
2. **IEEE bias is 127, not 128** (single precision).
3. **Generate uses AND; propagate uses XOR** — not the reverse.
4. **Ripple counter delays add; synchronous counters do not.**
5. **Ring = n states, Johnson = 2n states** — not the reverse.
6. **Moore = state only; Mealy = state + input.**
7. **Maxterm convention is inverted** relative to minterms (variable complemented when its bit is 1).
8. **Duality ≠ De Morgan.** Duality swaps AND/OR and 0/1 only; De Morgan also complements the variables.
9. **Height/level conventions:** if a question says "MOD-N", it means N distinct states, not N flip-flops.
10. **Signed vs unsigned overflow are different tests** — carry-out alone only detects unsigned overflow.

---

## 10. Practice

- GATE: [`Paper2_S02_Digital_Logic/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S02_Digital_Logic/) — **313 questions**
- State-PSC level: [`Paper2_S02_Digital_Logic/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S02_Digital_Logic/) — **309 questions**
- Test: [`Week_01_Test.md`](../04_Mock_Tests/Week_01_Test.md)

**Priority order if short on time:** number representation & 2's complement → IEEE-754 → K-maps → MUX/decoder implementation → flip-flop excitation tables → counters → Mealy/Moore.
