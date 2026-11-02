# 01 · Digital Logic — Precise Notes
> **TPSC ATO (IT) Paper-II §2** · ~9 marks (estimate) · Syllabus: *"Digital Logic — Boolean algebra; combinational and sequential circuits; minimization; number representations and computer arithmetic (fixed and floating point)"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson GATE guide, 11-DLD notebook, Study247, 3-DLD notebook, Made Easy, Ace, 9-DL, 8-ekxam, 10-DLD. Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/01_Digital_Logic/` (PDF page numbers) — open them for diagrams. IEEE-754 lives here; COA cross-references §2.4.

## Which notes are worth your time
| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 1.Digital_Logic.pdf | Pearson GATE guide | Typeset, 2-column | 81 | 4 | Complements, codes, comparator, parity, gate counts; year-tagged GATE PYQs with keys · no IEEE-754/Booth/FSM |
| 2.Digital_Sanchit_Sir_Notes.pdf | Sanchit Jain (Knowledge Gate) | Typeset slides | 172 | 4 | Backbone: Boolean algebra, K-maps, MUX/decoder, FFs, counters; biggest NET+GATE PYQ bank · no signed numbers, codes, IEEE, Booth; a few slips (⚠) |
| 3.DLD.pdf | Aditya Jain notebook | Handwritten photos, very neat | 185 | 3.5 | Cleanest diagrams: comparators, MUX implementation, counter analysis · no number systems |
| 4.digital_electronics…Made_Easy….pdf | Made Easy class notes | Handwritten scan | 134 | 3 | 16 two-variable functions, JK excitation shortcut · ~25 % logic families/DAC/ADC |
| 5.Ace_Academy_DL_Class_Notes.pdf | Ace Academy class notes | Faint handwritten scan | 94 | 2.5 | Hazards, state diagram → JK · promised floating-point chapter missing |
| 6.Digital_Electronics_Handwriting_Notes.pdf | CSE Study247 | Neat colour handwriting | 136 | 3.5 | PI/EPI drills, race-around timing, sync vs async reset · arithmetic thin; 64 MB |
| 7.Digital_Logic-CS.pdf | Wiki Engineering | Faint handwritten scan | 172 | 2 | NAND/NOR universality · ECE-oriented (ADC/DAC, transmission gates) |
| 8.Digital_Logic.pdf | ekxam.com lecture notes | Colour handwriting, dim photos | 103 | 3 | "Functions of functions", adder–subtractor tricks · dim, blank pages |
| 9.DL.pdf | Personal notebook (YOUVA) | Handwritten photos | 190 | 3 | Signed and fixed-point worked examples · 189 MB; floating point and Booth missing |
| 10.DLD_Notes.pdf | Personal notebook | CamScanner | 109 | 2.5 | Repeated-state counter trick · thin, average legibility |
| 11.DLD.pdf | Personal notebook (same course as 8) | CamScanner, legible | 246 | 4 | Only scan with IEEE-754, Booth, Hamming · 83 MB; IEEE bias written as 2^(k−1) |

**If you open only one PDF besides these notes:** open **Pearson (1.Digital_Logic.pdf)**. It is searchable, it covers the number-representation and codes half that Sanchit skips, and its chapter-end GATE PYQs are the best drill. With one more hour, read **11.DLD.pdf pp. 228–246** (IEEE-754, Booth).

## Topic map
| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1.1 | Base conversion | ⭐⭐⭐ | hex↔octal; find unknown base |
| 1.3 | Signed numbers, ranges | ⭐⭐⭐ | n-bit range; value of a pattern |
| 1.4 | BCD/XS-3/Gray codes | ⭐⭐ | Gray↔binary; self-complementing? |
| 2.1 | Overflow | ⭐⭐⭐ | correct overflow expression |
| 2.2 | Booth | ⭐ | recode multiplier; count ops |
| 2.3 | Fixed point | ⭐ | range/resolution |
| 2.4 | IEEE-754 | ⭐⭐⭐ | decode/encode pattern; special values |
| 3.1–3.2 | Laws, duality, XOR | ⭐⭐ | name law; dual; XOR identity |
| 3.4 | Function counting | ⭐⭐ | number of (self-dual) functions |
| 3.5 | Universal gates | ⭐⭐⭐ | minimum NAND/NOR count |
| 4 | K-map, PI/EPI | ⭐⭐⭐ | minimal SOP/POS; count PIs/EPIs |
| 5.2 | RCA vs CLA | ⭐⭐⭐ | delay; CLA gate count |
| 5.5 | MUX implementation | ⭐⭐⭐ | output of MUX circuit; min MUX size |
| 5.6–5.7 | Decoder/encoder | ⭐⭐ | decoders for expansion; priority encoder |
| 6.2 | FF tables | ⭐⭐⭐ | characteristic equation; conversion |
| 6.3 | Race-around | ⭐⭐ | cause/cure |
| 6.4 | Counters | ⭐⭐⭐ | min FFs; state sequence; f_max |
| 6.5–6.6 | Ring/Johnson, shift registers | ⭐⭐ | states; clocks needed |
| 6.7 | Mealy vs Moore | ⭐ | difference; detector states |

## 1. Number Systems & Codes

### 1.1 Bases and conversions
- Base r uses digits 0 … r−1, and (10)ᵣ = r. Value = Σ dᵢrⁱ.
- Decimal → base r: integer part by repeated ÷ r (remainders read bottom-up); fraction by repeated × r (integer parts read top-down).
- Binary ↔ octal: groups of 3; binary ↔ hex: groups of 4, counted outward from the radix point. Octal ↔ hex: go through binary.
- 📌 Bits for N = ⌊log₂N⌋ + 1. Decimal digits for n bits = ⌊n·log₁₀2⌋ + 1 (123 bits → 38).
- 0.1₁₀ is recurring in binary. A fraction terminates in base r only if its denominator's prime factors divide r.
- 🔢 (BCA9)₁₆ = 1 011 110 010 101 001 = (136251)₈ (GATE-2017). (1217)₈ = (28F)₁₆ (GATE-2009).
- 🔢 x² − 13x + 36 has roots 5 and 6 in base b → sum (13)_b = b + 3 = 11 → **b = 8** (GATE-2017). (123)₅ = (x8)_y → xy = 30, y > 8 → 3 solutions (GATE-2014). (43)ₓ = (y3)₈ → x = 2y → 5 solutions (GATE-2015).
- 🎯 "Number of 1s in 3×512 + 7×64 + 5×8 + 3": write it as (3753)₈ → 9 ones (NET-Dec-2009).

### 1.2 Complements
- 📌 r's complement = rⁿ − N; (r−1)'s = (rⁿ − 1) − N; r's = (r−1)'s + 1. Example: 9's of 843 = 156, 10's = 157.
- 2's complement shortcut: copy bits from the LSB up to and including the first 1, then invert the rest.
- M − N by r's complement: compute M + r's(N). An end carry means a positive result (drop the carry). No carry means the result is −[r's complement of the sum].
- With (r−1)'s complement, add the end carry back to the LSB (**end-around carry**) [Src: 9-DL p.24; Pearson p.6].

### 1.3 Signed-number representations
| Representation | −5 (4-bit) | Range (n bits) | Zeros | Negate by |
|---|---|---|---|---|
| Sign-magnitude | 1101 | ±(2ⁿ⁻¹−1) | two | flip MSB |
| 1's complement | 1010 | ±(2ⁿ⁻¹−1) | two | invert |
| 2's complement | 1011 | −2ⁿ⁻¹ … 2ⁿ⁻¹−1 | one | invert + 1 |
- ⭐ 8-bit 2's complement: **−128 … +127** (GATE-2013). Positive numbers look the same in all three.
- 📌 2's-complement value = −bₙ₋₁2ⁿ⁻¹ + Σ bᵢ2ⁱ. Example: 1111 1111 1111 0101 = −11 (GATE-2016). 10111011 = −59 (SM), −68 (1's), −69 (2's).
- Sign extension copies the MSB. Left shift by k multiplies by 2ᵏ: (F87B)₁₆ × 8 = (C3D8)₁₆ (GATE-2010).
- 🎯 GATE-2016: (number of 16-bit 2's-complement integers) − (number of 16-bit SM integers) = **1** [Src: 11-DLD p.240].

### 1.4 Codes
- Excess-3 = BCD + 0011. Gray codes of 0–9: 0000 0001 0011 0010 0110 0111 0101 0100 1100 1101.

| Code | Weighted | Self-complementing | Unit distance |
|---|---|---|---|
| 8421 BCD (1010–1111 invalid) | yes | **no** | no |
| 2421, 5211, 3321, 84−2−1 | yes | yes | no |
| Excess-3 | no | yes | no |
| Gray (cyclic, reflected) | no | no | yes |
- 📌 A code is self-complementing if code(9−N) is the bitwise complement of code(N). A weighted 4-bit code needs weights summing to 9.
- ⚠ Pearson p.8 says "all weighted BCD codes are self-complementing". That is wrong: 8421 is weighted but not self-complementing.
- 📌 Binary → Gray: g_MSB = b_MSB, gᵢ = bᵢ₊₁ ⊕ bᵢ. Gray → binary: bᵢ = bᵢ₊₁ ⊕ gᵢ. Each needs n−1 XOR gates. 🔢 1001 → 1101; Gray 1010 → 1100.
- BCD addition: if a digit sum is > 9 or carries, add 0110 (8 + 5 = 1101 + 0110 = 1 0011).
- Even parity bit = XOR of the data bits; it detects only an odd number of errors. 📌 Hamming: 2ᵖ ≥ m + p + 1 (m = 4 → p = 3; m = 8 → p = 4) [Src: 11-DLD p.212, 224].
- ASCII is 7-bit: 'A' = 65, 'a' = 97, '0' = 48. EBCDIC is 8-bit.

## 2. Computer Arithmetic (fixed and floating point)

### 2.1 Addition, subtraction, overflow
- In 2's complement, add all bits and drop the carry out of the MSB. A − B = A + B′ + 1.
- 📌 **Signed overflow** happens only when both operands have the same sign and the result's sign differs: V = Aₙ₋₁Bₙ₋₁S′ₙ₋₁ + A′ₙ₋₁B′ₙ₋₁Sₙ₋₁ = **Cₙ ⊕ Cₙ₋₁**. Operands of opposite sign never overflow (GATE-2017).
- 📌 **Unsigned overflow** = carry out Cₙ (GATE-2006). In unsigned A − B, Cₙ = 1 means A ≥ B.
- 🔢 4-bit: 0101 + 0100 = 1001 → −7, overflow (C₄ = 0, C₃ = 1) [Src: MadeEasy p.100].

### 2.2 Booth's multiplication (signed 2's complement)
| Qᵢ Qᵢ₋₁ | Action, then arithmetic right shift of A, Q, Q₋₁ | Digit |
|---|---|---|
| 00 / 11 | shift only | 0 |
| 01 | A ← A + M | +1 |
| 10 | A ← A − M | −1 |
- Start with Q₋₁ = 0 and A = 0, and run n iterations. The product is in A:Q.
- A run of 1s from bit i to bit j equals 2ʲ⁺¹ − 2ⁱ. So 01110 → +1 0 0 −1 0 = 16 − 2, i.e. 1 add + 1 subtract [Src: 11-DLD p.243].
- Best case: long runs of 1s. **Worst case: alternating 0101…**, which needs one operation per bit [Src: 11-DLD p.246].

### 2.3 Fixed point
- The radix point is at a fixed position. 📌 With 1 sign + i integer + f fraction bits: step = 2⁻ᶠ; 2's-complement range is −2ⁱ … 2ⁱ − 2⁻ᶠ; sign-magnitude range is ±(2ⁱ − 2⁻ᶠ).
- 🔢 8-bit SM with 1+4+3 bits: −12.25 → 1 1100 010; range ±15.875 [Src: 9-DL p.37].
- Fixed point is simple, fast and has a uniform step but a small range (DSP, money). Floating point has a huge range and uniform *relative* precision but needs an FPU.

### 2.4 IEEE-754
- Normalised value = (−1)ˢ × **1.M** × 2^(E − bias). The leading 1 is hidden. A biased exponent lets floats compare like unsigned integers.

| | Single (32) | Double (64) |
|---|---|---|
| S / E / M bits | 1 / 8 / 23 | 1 / 11 / 52 |
| Bias | **127** | **1023** |
| Precision | 24 bits ≈ 7 digits | 53 bits ≈ 15–16 digits |
| Normal stored E → actual | 1–254 → −126…+127 | 1–2046 → −1022…+1023 |
| Largest | (2−2⁻²³)×2¹²⁷ ≈ 3.4×10³⁸ | ≈ 1.8×10³⁰⁸ |
| Smallest normal | 2⁻¹²⁶ ≈ 1.18×10⁻³⁸ | 2⁻¹⁰²² ≈ 2.2×10⁻³⁰⁸ |
| Smallest denormal | 2⁻¹⁴⁹ ≈ 1.4×10⁻⁴⁵ | 2⁻¹⁰⁷⁴ ≈ 4.9×10⁻³²⁴ |

| Stored E | M | Meaning |
|---|---|---|
| 0 | 0 | ±0 |
| 0 | ≠0 | denormal (−1)ˢ × **0.M** × 2⁻¹²⁶ |
| 1–254 | any | normalised |
| 255 | 0 | ±∞ |
| 255 | ≠0 | NaN |
- ⚠ The denormal exponent is 1 − bias = −126, not −127.
- ⚠ 11-DLD p.230/236 says bias = 2^(k−1). That is a generic excess-code convention; IEEE uses **2^(k−1) − 1**. If a question defines its own format, use the bias it states.
- 0x00000000 is the **special value +0** (GATE-2008). Half precision is 1/5/10 with bias 15 [Src: 11-DLD p.236].
- 🔢 **Encode −13.625:** 1101.101 = 1.101101×2³ → S = 1, E = 130 = 10000010, M = 1011010… → **C15A0000₁₆**.
- 🔢 **Decode 0x41C80000:** E = 131 − 127 = 4, 1.1001×2⁴ = **25** [Src: 11-DLD p.238].
- 🎯 Decode a 32-bit pattern and pick the nearest decimal (GATE-2017); identify +0/∞/NaN patterns; field widths, bias, range.

### 2.5 Floating-point arithmetic
- **Add:** align (shift the smaller-exponent mantissa right) → add → normalise → round.
- **Multiply:** S = S₁ ⊕ S₂; E = E₁ + E₂ − bias; multiply mantissas → normalise → round.
- ⚠ FP addition is not associative.

## 3. Boolean Algebra & Logic Gates

### 3.1 Laws
| Law | AND form | OR form |
|---|---|---|
| Idempotent | A·A = A | A + A = A |
| Absorption | A(A + B) = A | A + AB = A |
| Redundant literal | A(A′ + B) = AB | A + A′B = A + B |
| Distributive | A(B + C) = AB + AC | A + BC = (A + B)(A + C) |
| De Morgan | (AB)′ = A′ + B′ | (A + B)′ = A′B′ |
| Consensus | (A+B)(A′+C)(B+C) = (A+B)(A′+C) | AB + A′C + BC = AB + A′C |
- **Dual:** swap + ↔ · and 0 ↔ 1, keeping the literals; f^d(x) = [f(x′)]′. **Complement:** also complement the literals. The dual of x + yz is x(y + z) (NET-Dec-2007) [Src: Sanchit p.26–27].
- Shannon expansion f = x·f(1) + x′·f(0) underlies MUX implementation.
- 🎯 x + x = x is idempotent (NET-Jun-2008); x + xy = x is absorption (NET-Jun-2011).

### 3.2 Gates and XOR
| Gate | Output 1 when | Associative | Universal |
|---|---|---|---|
| NAND | any input 0 | **no** | yes |
| NOR | all inputs 0 | **no** | yes |
| XOR | odd number of 1s | yes | no |
| XNOR | 2-input: inputs equal | yes | no |
- 📌 A⊕1 = A′; A⊕A = 0; A′⊕B′ = A⊕B; (A⊕B)′ = A′⊕B = A⊙B; A⊕B⊕AB = A + B. If A⊕B = C, then A⊕C = B and A⊕B⊕C = 0.
- Chained 2-input XNORs over an odd number of variables equal their XOR [Src: Sanchit p.19].
- ⚠ Sanchit p.15 says XNOR is high when the inputs "are different". It is high when they are **equal**.
- ⚠ Sanchit p.18 keys a = a⊕b, b = a⊕b, a = b⊕a (NET-Dec-2005) as "retains". It actually **swaps** a and b.
- 🎯 An operator with truth table 0110 is XOR: commutative and associative (GATE-2015). The non-associative connective is NAND (NET-Dec-2004).

### 3.3 Canonical forms
- Minterm mᵢ is 1 on exactly one row; maxterm Mᵢ = mᵢ′. 📌 Σm(S) = ΠM(rows not in S); f′ = Σm(rows not in S).
- A term with k missing literals covers 2ᵏ minterms: AB in 4 variables → m12–15 [Src: 9-DL p.50]. 🔢 PQ + QR′ + PR′ = Σm(2,4,6,7) (GATE-2010).
- f₁·f₂ = intersection of minterm sets; f₁ + f₂ = union. With don't-cares: d·1 = d, d + 0 = d [Src: Sanchit p.47–49].

### 3.4 Counting functions (n variables)
| Quantity | Count |
|---|---|
| Boolean functions | ⭐ **2^(2ⁿ)** (n = 4 → 2¹⁶) |
| Self-dual functions | ⭐ **2^(2ⁿ⁻¹)** (GATE-2014) |
| Neutral (#minterms = #maxterms) | C(2ⁿ, 2ⁿ⁻¹) |
| Realisations with k don't-cares | 2ᵏ |
- Self-dual test: the function is neutral and contains exactly one minterm of each pair (mᵢ, m₂ⁿ₋₁₋ᵢ). For n = 3 the pairs are (0,7), (1,6), (2,5), (3,4). The majority function Σm(3,5,6,7) is self-dual [Src: 3-DLD p.30].
- The 16 two-variable functions include the inhibitions AB′, A′B and the implications A′ + B, A + B′ [Src: MadeEasy p.1–2].

### 3.5 Functional completeness and gate counts
- **Complete:** {NAND}, {NOR}, {AND, NOT}, {OR, NOT}, {2:1 MUX + constants}, {XOR, AND, 1}, {→, 0}. **Not complete:** {AND, OR}, {XOR, NOT}.
- Post's criterion: a set is complete iff it contains a function outside each of these classes: 0-preserving, 1-preserving, self-dual, monotone, linear.
- Sanchit's "partially complete" means complete only with constants allowed, e.g. a′ + b [Src: Sanchit p.55, 62].

| Target | Min 2-input NAND | Min 2-input NOR |
|---|---|---|
| AND / OR | 2 / 3 | 3 / 2 |
| XOR / XNOR | **4** / 5 | **5** / 4 |
| Half adder | 5 | 5 |
| Full adder / full subtractor | 9 | 9 |
- SOP → NAND-NAND; POS → NOR-NOR [Src: Sanchit p.57–60].
- 🎯 XOR needs 4 NANDs (GATE-2004). AB + C with 2-input NOR = (A + C)(B + C) needs 3 (GATE-2009).

## 4. Minimisation

### 4.1 K-map rules
- Cells follow Gray order and the edges wrap (the four corners are adjacent). A group of 2ᵏ cells removes k literals.
- Groups are rectangles with power-of-2 sizes, as large and as few as possible. Overlaps are allowed. Use a don't-care only if it enlarges a group.
- POS: group the 0s and write complemented sum terms.
- 5-variable map: two 4-variable maps (A = 0 and A = 1); cells in the same position are adjacent. K-maps are practical up to 5–6 variables [Src: Sanchit p.31–33].

### 4.2 Implicants
- **PI:** a group not contained in any larger group. **EPI:** a PI covering some minterm no other PI covers; it is in every minimal SOP.
- Minimal SOP = EPIs + the fewest other PIs covering the rest. A function may have several minimal forms.
- Every minimal expression is irredundant, but not the reverse [Src: Sanchit p.52].
- ⚠ Don't-cares never need covering, and they never make a PI essential.
- 🔢 Σ(0,2,4,5,6,10): the PIs are w′z′, w′xy′ and x′yz′ → **3** (GATE-2015). Σ(1,3,4,6,9,11,12,14) = x⊕z, so it is independent of 2 variables (GATE-2007).
- 🎯 Count EPIs with don't-cares (GATE-2018, answer 3); minimal POS (GATE-2017); minimum literal count (GATE-2003) [Src: Study247 p.40; Sanchit p.34–43].

### 4.3 Quine–McCluskey (sources only name it; steps added)
1. Group the minterms (and don't-cares) by their number of 1s.
2. Combine terms in adjacent groups that differ in one bit; tick them and repeat.
3. The unticked terms are the PIs.
4. In the PI chart, use minterm columns only; a column with a single × marks an EPI.
- QM works for any number of variables and is the method suited to computers.

### 4.4 Algebraic shortcuts
- a + a′b + a′b′c + a′b′c′d′ = a + b + c + d′ [Src: Sanchit p.54]. (P + Q′)(PQ′ + PR)(P′R′ + Q′) = PQ′ (GATE-2008).
- MCQ trick: substitute 0/1 values to eliminate options.

## 5. Combinational Circuits
The output depends only on the present inputs: no memory and no clock.

### 5.1 Adders and subtractors
| Circuit | Expressions | Build |
|---|---|---|
| Half adder | S = A⊕B; C = AB | XOR + AND |
| Full adder | S = A⊕B⊕Cin = Σm(1,2,4,7); Cout = AB + Cin(A⊕B) = Σm(3,5,6,7) | 2 HA + OR |
| Half subtractor | D = A⊕B; Bout = A′B | XOR + AND + NOT |
| Full subtractor | D = A⊕B⊕Bin; Bout = A′B + Bin(A⊕B)′ | 2 HS + OR |
- ⭐ Sum = odd function; carry = majority (self-dual). FA = 3:8 decoder + two ORs [Src: Sanchit p.97].

### 5.2 Ripple carry vs carry look-ahead
- **RCA:** n full adders; the carry passes 2 gate levels per stage, so the delay is 2n levels: O(n).
- 📌 **CLA:** Gᵢ = AᵢBᵢ, Pᵢ = Aᵢ⊕Bᵢ, Cᵢ₊₁ = Gᵢ + PᵢCᵢ, Sᵢ = Pᵢ⊕Cᵢ. For example C₂ = G₁ + P₁G₀ + P₁P₀C₀ and C₄ = G₃ + P₃G₂ + P₃P₂G₁ + P₃P₂P₁G₀ + P₃P₂P₁P₀C₀ (maximum fan-in n + 1) [Src: Sanchit p.72–73].
- 📌 CLA delay = 1 (P,G) + 2 (carries) + 1 (sum) = **4 gate delays**. A carry generator for C₁…Cₙ needs **n(n+1)/2 AND + n OR** gates: 4-bit → 10, 4 (GATE-2007).
- With fan-in 2, CLA delay is **Θ(log n)** (GATE-2016).
- 🎯 4-bit CLA without XOR gates: P (2) + carry (2) + sum (2) = **6** (GATE-2004). In an 8-bit RCA with A = 1, the longest latency comes from **B = −1** (GATE-2016).
- 🎯 GATE-2015: XOR = 2.4 µs, AND/OR = 1.2 µs, FA = 2 HA + OR, 4-bit RCA → key **19.2 µs** (4 × 4.8). ⚠ A strict critical path gives 12.0 µs; pick 19.2 if it is offered [Src: Pearson p.54 key].

### 5.3 Adder–subtractor and BCD adder
- Each B input passes through an XOR with mode M, and Cin = M: M = 0 adds, M = 1 subtracts. V = Cₙ ⊕ Cₙ₋₁ [Src: Sanchit p.70].
- With constant inputs the same circuit becomes BCD↔XS-3 (±0011), 9's complement (1001 − B) or 10's complement (1010 − B) [Src: 8-ekxam p.60].
- 📌 BCD adder correction: C = K + Z₈Z₄ + Z₈Z₂; if C = 1, add 0110.

### 5.4 Comparator
- 1-bit: A > B = AB′; A < B = A′B; A = B = (A⊕B)′.
- n-bit, with xᵢ = (Aᵢ⊕Bᵢ)′: A > B = A₃B′₃ + x₃A₂B′₂ + x₃x₂A₁B′₁ + x₃x₂x₁A₀B′₀. The truth table has 2²ⁿ rows [Src: 3-DLD p.130; Pearson p.38].

### 5.5 Multiplexer
- A 2ⁿ:1 MUX has n select lines: Y = Σ mᵢ(S)·Iᵢ.
- 📌 An n-variable function fits a **2ⁿ⁻¹:1 MUX** + 1 inverter, with data inputs from {0, 1, x, x′} (GATE-2007).
- 🔢 Σm(1,2,4,6,7) with A,B on the selects: I₀ = C, I₁ = C′, I₂ = C′, I₃ = 1 [Src: 3-DLD p.80].
- A 2:1 MUX is universal: (S = A, I₀ = 0, I₁ = B) gives AB; (I₀ = 1, I₁ = 0) gives A′.
- 📌 An N:1 MUX from m:1 MUXes needs Σ⌈N/mᵏ⌉ = (N−1)/(m−1) when N = mᵏ: 16:1 from 4:1 → 5; 128:1 from 4:1 → 43 [Src: Sanchit p.89–90].
- 🎯 Read a MUX circuit (GATE-2014/2016); make AND/NOR from 2:1 MUXes (GATE-2007/2005).

### 5.6 Decoder, demultiplexer, ROM
- An n:2ⁿ decoder outputs every minterm. A DEMUX with its data input used as an enable is a decoder.
- 📌 Any function = decoder + one OR gate per output. Active-low outputs need a NAND instead [Src: Pearson p.40–41].
- 📌 6:64 from 3:8 decoders = 8 + 1 = **9** (GATE-2007). 4:16 from 2:4 = 5 [Src: Sanchit p.100].
- ROM = fixed AND (decoder) + programmable OR. PLA: both arrays programmable. PAL: programmable AND, fixed OR.
- 🎯 Decoder n→2ⁿ, MUX 2ⁿ→1, DEMUX 1→2ⁿ (NET-Jul-2018).

### 5.7 Encoder and priority encoder
- A 4:2 encoder assumes one active input: Y₁ = I₂ + I₃, Y₀ = I₁ + I₃.
- 📌 Priority encoder with I₃ highest: **Y₁ = I₃ + I₂, Y₀ = I₃ + I₁I′₂**, valid bit V = ΣIᵢ (GATE-2013).
- ⚠ Sanchit p.105 swaps the output equations relative to his own table. Correct: MSB = I₂ + I₃, LSB = I₃ + I₁I′₂.

### 5.8 Hazards
- **Static-1 hazard:** a 0-glitch when an input change crosses between groups that share no term. Example: AB + A′C with B = C = 1 while A changes. Fix it by adding the consensus term BC; the hazard-free circuit is not minimal.
- Static-0 is the POS counterpart. A dynamic hazard gives 3+ transitions.
- ⚠ Ace p.55 lists stuck-at faults as hazards. Stuck-at faults are permanent defects, not glitches.

## 6. Sequential Circuits
The output depends on the present input and the stored state.

### 6.1 Latch vs flip-flop
| | Latch | Flip-flop |
|---|---|---|
| Triggering | level (transparent) | edge |
| Built from | cross-coupled NAND/NOR | master–slave latches |
- NOR SR latch: S = R = 1 is forbidden (Q = Q′ = 0). NAND latch: S = R = 0 is forbidden (Q = Q′ = 1; GATE-2004 key: "indeterminate"). The NAND-latch sequence 00 → 11 can oscillate (GATE-2007) [Src: Sanchit p.108–114].
- Synchronous circuits avoid hazards more easily (NET-Jun-2010).

### 6.2 Flip-flop tables
| FF | Characteristic equation | Excitation 0→0, 0→1, 1→0, 1→1 |
|---|---|---|
| SR | Q⁺ = S + R′Q (SR = 0) | 0X, 10, 01, X0 |
| JK | Q⁺ = JQ′ + K′Q | 0X, 1X, X1, X0 |
| D | Q⁺ = D | 0, 1, 0, 1 |
| T | Q⁺ = T⊕Q | 0, 1, 1, 0 |
- 📌 JK excitation shortcut: for Q = 0, J = Q⁺ and K = X; for Q = 1, K = (Q⁺)′ and J = X [Src: MadeEasy p.45].
- Conversions: T from JK: J = K = T. D from SR: S = D, R = D′ (NET-Dec-2005). JK from D: D = JQ′ + K′Q. JK from T: T = JQ′ + KQ. T from D: D = T⊕Q [Src: Sanchit p.125–128].

### 6.3 Race-around and timing
- **Race-around:** a level-triggered JK with J = K = 1 toggles repeatedly while t_pw > t_pd. Cures: t_pw < t_pd < T, edge triggering, or a **master–slave** FF [Src: Study247 p.90; Pearson p.59].
- A master–slave FF changes on the falling edge. Its drawback is **1s-catching**: the inputs must stay stable while CLK = 1. It is the FF "free from race" (NET-Jun-2014).
- 📌 Synchronous f_max = 1/(t_pd + t_comb + t_setup). Ripple: T ≥ n·t_pd, so 4 bits × 25 ns → 10 MHz (NET-Jun-2007).

### 6.4 Counters
- 📌 Minimum FFs for mod-N = **⌈log₂N⌉**: mod-258 → 9 (GATE-2011); mod-18 → 5.

| | Asynchronous (ripple) | Synchronous |
|---|---|---|
| Clock | each FF clocked by the previous output | common clock |
| Delay | n·t_pd | t_pd + t_comb |
| Also called | **serial** | **parallel** |
| Glitches | yes | no |
- ⚠ Sanchit p.146 calls synchronous counters "serial" and asynchronous ones "parallel". That is reversed.
- 📌 Ripple direction: a −ve-edge FF clocked from Q counts up (from Q′, down). A +ve-edge FF clocked from Q′ counts up.
- Mod-M followed by mod-N = mod-MN (NET-Jul-2019). An **async clear** at N gives mod-N, and state N is a glitch. A **sync clear** decoding N gives mod-(N+1) [Src: Study247 p.122].
- Design: state table → excitations (unused states = don't-cares) → K-maps. Analysis: input equations → next-state table → trace (GATE-2011/2014/2017) [Src: Sanchit p.137–142; 3-DLD p.170].
- **Self-starting:** unused states eventually return to the main cycle; otherwise the counter can lock out. **Free-running** means all 2ⁿ states are in the cycle, so a free-running counter is also self-starting [Src: Sanchit p.150].
- 🔢 Repeated values need extra FFs: 0,1,0,2,0,3 → **4** (GATE-2016); 0,0,1,1,2,2,3,3 → **3** (GATE-2015) [Src: 10-DLD p.85].

### 6.5 Ring and Johnson
| | Ring | Johnson (twisted) |
|---|---|---|
| Feedback | Q_last → D_first | Q′_last → D_first |
| States (n FFs) | **n** | **2n** |
| Unused | 2ⁿ − n | 2ⁿ − 2n |
| Duty cycle | 1/n | 50 % |
- 🔢 4-bit Johnson from 0000: 0, 8, 12, 14, 15, 7, 3, 1 (GATE-2015) [Src: Sanchit p.158–160; 9-DL p.188].

### 6.6 Shift registers
| Mode | Load + read clocks | Use |
|---|---|---|
| SISO | n + (n−1) = **2n−1** | delay line |
| SIPO | n + 0 | serial → parallel |
| PISO | 1 + (n−1) | parallel → serial |
| PIPO | 1 + 0 | storage |
- 🔢 A 32-bit SISO at 1 GHz takes 63 ns. D FFs are the usual choice. Shift left = ×2, shift right = ÷2. A universal shift register uses one 4:1 MUX per bit (hold, shift-left, shift-right, load) [Src: Sanchit p.152–157].
- 🎯 A shift register with XOR feedback is fed a bit stream; give its contents after k clocks (GATE-2006) [Src: Sanchit p.157; 3-DLD p.178].

### 6.7 Mealy vs Moore (added — not in sources)
| | Moore | Mealy |
|---|---|---|
| Output depends on | state only | state + input |
| Timing | after the clock edge; glitch-free | immediate |
| n-bit sequence detector | n + 1 states | n states |
- Each machine type can be converted into the other. FFs needed = ⌈log₂(number of states)⌉.

## Last-day revision sheet
| Item | Value |
|---|---|
| Functions / self-dual / neutral | 2^(2ⁿ) / 2^(2ⁿ⁻¹) / C(2ⁿ, 2ⁿ⁻¹) |
| r's / (r−1)'s complement | rⁿ − N / rⁿ − 1 − N |
| SM and 1's range | ±(2ⁿ⁻¹ − 1), two zeros |
| 2's complement range | −2ⁿ⁻¹ … 2ⁿ⁻¹−1 |
| Signed / unsigned overflow | Cₙ ⊕ Cₙ₋₁ / Cₙ |
| Gray | gᵢ = bᵢ₊₁ ⊕ bᵢ; bᵢ = bᵢ₊₁ ⊕ gᵢ |
| Hamming | 2ᵖ ≥ m + p + 1 |
| IEEE single | 1/8/23, bias 127, max ≈ 3.4×10³⁸, min normal 2⁻¹²⁶ |
| IEEE double | 1/11/52, bias 1023, max ≈ 1.8×10³⁰⁸, min normal 2⁻¹⁰²² |
| IEEE specials | E = 0: ±0 / denormal 0.M×2⁻¹²⁶; E = all 1s: ±∞ / NaN |
| Fixed point (2's) | −2ⁱ … 2ⁱ − 2⁻ᶠ, step 2⁻ᶠ |
| Full adder | S = A⊕B⊕C; Cout = AB + C(A⊕B) |
| CLA | Cᵢ₊₁ = Gᵢ + PᵢCᵢ; 4 delays; n(n+1)/2 AND + n OR |
| RCA | 2n gate levels, O(n) |
| MUX for n vars | 2ⁿ⁻¹:1 + inverter |
| MUX tree | (N−1)/(m−1) |
| XOR gates | 4 NAND / 5 NOR |
| HA / FA gates | 5 / 9 |
| FF equations | SR: S + R′Q; JK: JQ′ + K′Q; D: D; T: T⊕Q |
| Mod-N | ⌈log₂N⌉ FFs |
| Ring / Johnson | n / 2n states; unused 2ⁿ−n / 2ⁿ−2n |
| f_max | ripple 1/(n·t_pd); sync 1/(t_pd + t_comb + t_setup) |
| SISO | 2n − 1 clocks |

1. ⭐ NAND and NOR are universal but not associative.
2. Dual keeps the literals; complement inverts them.
3. Don't-cares never make a PI essential.
4. ⭐ 8-bit 2's complement: −128 … +127.
5. Opposite-sign operands never overflow.
6. 8421 is not self-complementing; Excess-3 is.
7. ⭐ IEEE bias = 2^(k−1) − 1.
8. The denormal exponent is −126.
9. 0x00000000 = +0.
10. Booth's worst case is an alternating multiplier.
11. FA carry = majority.
12. ⭐ CLA with fan-in 2: Θ(log n).
13. RCA worst case: A = 1, B = −1.
14. 6:64 decoder needs 9 3:8 decoders.
15. ⭐ A 2:1 MUX is universal.
16. Priority encoder: Y₀ = I₃ + I₁I′₂.
17. A hazard is fixed by the consensus term.
18. NOR latch forbids 11; NAND latch forbids 00.
19. ⭐ Cure race-around with master–slave.
20. Ripple counter = serial.
21. A −ve-edge FF clocked from Q counts up.
22. Async clear: the state is not counted.
23. Johnson duty cycle = 50 %.
24. Moore needs one more state than Mealy.
25. FP addition is not associative.
26. Gray code is unit-distance and non-weighted.
27. BCD correction: add 0110 when the sum > 9 or carries.
28. Latches are level-triggered; FFs are edge-triggered.
29. A master–slave FF changes on the falling edge and suffers 1s-catching.
30. Unsigned A − B: carry out = 1 means A ≥ B.

## Dropped as outside TPSC syllabus
- Analog vs digital, history, the design narrative (Sanchit p.1–4).
- Logic families, V_IH/V_IL, fan-out, MOS circuits, transmission gates (MadeEasy p.106–122; 7-WikiEngg p.165).
- ADC/DAC (MadeEasy p.122–134; 7-WikiEngg p.130).
- Memory address decoding (Ace p.75); this belongs to COA.
- Probability PYQs (Pearson GATE-2015; Sanchit GATE-2019).
- Orthogonal-function counting (Sanchit p.30).
