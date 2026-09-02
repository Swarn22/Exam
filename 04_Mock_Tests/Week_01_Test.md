# Week 1 Mock Test — Digital Logic & Number Systems

**Syllabus §2** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — Digital Logic (Q1–Q20)

**Q1.** In an 8-bit 2's complement representation, the range of integers that can be represented is
(A) −127 to +127  (B) −128 to +127  (C) −128 to +128  (D) 0 to 255

**Q2.** The decimal equivalent of the binary number `(110110)₂` is
(A) 54  (B) 46  (C) 108  (D) 27

**Q3.** In IEEE-754 single-precision floating point format, the number of bits allotted to the exponent and the value of the bias are, respectively,
(A) 8 and 128  (B) 8 and 127  (C) 11 and 1023  (D) 23 and 127

**Q4.** The 2's complement of the 8-bit number `01011010` is
(A) `10100101`  (B) `10100110`  (C) `10100111`  (D) `01011011`

**Q5.** The Boolean expression `A + A'B` simplifies to
(A) A  (B) B  (C) A + B  (D) A'B

**Q6.** A Boolean function of 4 variables can be implemented using a single multiplexer of minimum size
(A) 4 : 1  (B) 8 : 1  (C) 16 : 1  (D) 2 : 1

**Q7.** A full adder can be realised using
(A) two half adders and one OR gate
(B) two half adders and one AND gate
(C) one half adder and one OR gate
(D) three half adders

**Q8.** In a carry look-ahead adder, the *generate* function `Gᵢ` and *propagate* function `Pᵢ` for inputs `Aᵢ`, `Bᵢ` are
(A) Gᵢ = Aᵢ ⊕ Bᵢ, Pᵢ = Aᵢ·Bᵢ
(B) Gᵢ = Aᵢ·Bᵢ, Pᵢ = Aᵢ ⊕ Bᵢ
(C) Gᵢ = Aᵢ + Bᵢ, Pᵢ = Aᵢ·Bᵢ
(D) Gᵢ = Aᵢ·Bᵢ, Pᵢ = Aᵢ + Bᵢ

**Q9.** In a JK flip-flop, when J = K = 1, the output on the next clock edge
(A) is set to 1  (B) is reset to 0  (C) toggles  (D) is unchanged

**Q10.** The minimum number of flip-flops required to build a MOD-12 counter is
(A) 3  (B) 4  (C) 6  (D) 12

**Q11.** An n-bit ring counter and an n-bit Johnson (twisted-ring) counter have, respectively, how many distinct states?
(A) n and n  (B) n and 2n  (C) 2n and n  (D) 2ⁿ and n

**Q12.** The master-slave configuration of a flip-flop is primarily used to eliminate
(A) propagation delay  (B) the race-around condition  (C) power dissipation  (D) fan-out limitation

**Q13.** Which of the following is a *universal* gate?
(A) AND  (B) OR  (C) NAND  (D) XOR

**Q14.** A decoder with n input lines has a maximum of how many output lines?
(A) n  (B) 2n  (C) 2ⁿ  (D) n²

**Q15.** In a Moore machine, the output depends on
(A) the present state only
(B) the present state and the present input
(C) the present input only
(D) the next state only

**Q16.** The number of minterms in a Boolean function of 5 variables is at most
(A) 5  (B) 10  (C) 25  (D) 32

**Q17.** The Gray code equivalent of the binary number `1011` is
(A) `1110`  (B) `1101`  (C) `1010`  (D) `1111`

**Q18.** Applying De Morgan's theorem, `(A + B + C)'` equals
(A) A' + B' + C'  (B) A'·B'·C'  (C) A'·B' + C'  (D) (A·B·C)'

**Q19.** A 4-bit ripple (asynchronous) counter uses flip-flops each with propagation delay 10 ns. The maximum total delay before the output settles is
(A) 10 ns  (B) 20 ns  (C) 40 ns  (D) 4 ns

**Q20.** Consider `F(A,B,C) = Σm(1, 3, 5, 7)`. The minimal SOP expression for F is
(A) A  (B) B  (C) C  (D) A'C

---

## Part B — Paper-I (Q21–Q25)

**Q21.** Choose the word most nearly **opposite** in meaning to **BENEVOLENT**.
(A) Generous  (B) Malevolent  (C) Charitable  (D) Kind

**Q22.** Fill in the blank with the appropriate preposition: *"She has been living in Agartala ___ 2015."*
(A) for  (B) from  (C) since  (D) by

**Q23.** If in a certain code `MONDAY` is written as `NPOEBZ`, then `FRIDAY` will be written as
(A) `GSJEBZ`  (B) `GSJFBZ`  (C) `ESHCZX`  (D) `GTJEBZ`

**Q24.** Find the next term in the series: 3, 7, 15, 31, 63, ___
(A) 95  (B) 121  (C) 127  (D) 128

**Q25.** Tripura attained the status of a full-fledged State of the Indian Union on
(A) 15 October 1949  (B) 1 November 1956  (C) 21 January 1972  (D) 20 February 1987

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 6 | B | 11 | B | 16 | D | 21 | B |
| 2 | A | 7 | A | 12 | B | 17 | A | 22 | C |
| 3 | B | 8 | B | 13 | C | 18 | B | 23 | A |
| 4 | B | 9 | C | 14 | C | 19 | C | 24 | C |
| 5 | C | 10 | B | 15 | A | 20 | C | 25 | C |

---

**Q1 — (B).** With n bits, 2's complement spans −2ⁿ⁻¹ to +2ⁿ⁻¹ − 1, i.e. −128 to +127. The asymmetry exists because there is only one representation of zero.

**Q2 — (A).** 110110 = 32 + 16 + 0 + 4 + 2 + 0 = **54**.

**Q3 — (B).** Single precision = 1 sign + **8 exponent** + 23 mantissa = 32 bits, bias **127**. (Double precision is 1 + 11 + 52 with bias 1023 — option C is the double-precision trap.)

**Q4 — (B).** Invert: `10100101`; add 1: `10100110`. (Option A is the 1's complement — the most common error.)

**Q5 — (C).** Absorption: A + A'B = (A + A')(A + B) = 1·(A + B) = **A + B**.

**Q6 — (B).** An n-variable function needs only a 2ⁿ⁻¹ : 1 multiplexer, feeding the n-th variable (or its complement, 0, or 1) into the data inputs. For n = 4 that is an **8 : 1** MUX.

**Q7 — (A).** Sum = A⊕B⊕C from two cascaded half adders; carry = the two half-adder carries **OR**-ed together.

**Q8 — (B).** A carry is *generated* when both bits are 1 (Aᵢ·Bᵢ) and *propagated* when exactly one is 1 (Aᵢ ⊕ Bᵢ). Then Cᵢ₊₁ = Gᵢ + Pᵢ·Cᵢ.

**Q9 — (C).** J = K = 1 is the toggle condition — precisely the input combination that is forbidden in an SR flip-flop, which is why JK is preferred.

**Q10 — (B).** MOD-12 needs 12 distinct states; ⌈log₂12⌉ = **4** flip-flops (3 would give only 8).

**Q11 — (B).** A ring counter circulates a single 1 through n positions → **n** states. A Johnson counter feeds back the *complement*, doubling this to **2n** states.

**Q12 — (B).** In a level-triggered JK flip-flop with J = K = 1, the output can toggle repeatedly while the clock is high (race-around). The master-slave (or edge-triggered) design allows exactly one toggle per clock.

**Q13 — (C).** NAND and NOR are universal — any Boolean function can be built from either alone. AND, OR and XOR are not.

**Q14 — (C).** An n-to-2ⁿ decoder activates one output per input combination.

**Q15 — (A).** Moore: output = f(present state). Mealy: output = f(present state, present input). Mealy typically needs fewer states; Moore's output is glitch-free.

**Q16 — (D).** n variables give 2ⁿ minterms; 2⁵ = **32**.

**Q17 — (A).** Gray: keep the MSB, then XOR adjacent binary bits. 1011 → G₃=1, G₂=1⊕0=1, G₁=0⊕1=1, G₀=1⊕1=0 → **1110**.

**Q18 — (B).** De Morgan: the complement of a sum is the product of complements → **A'·B'·C'**.

**Q19 — (C).** In a ripple counter the clock propagates serially through the stages, so delays add: 4 × 10 = **40 ns**. (A synchronous counter would settle in 10 ns — that is its whole advantage.)

**Q20 — (C).** Minterms 1, 3, 5, 7 are exactly the odd indices — every term where C = 1, regardless of A and B. So F = **C**.

**Q21 — (B).** *Benevolent* = kind, well-meaning; its opposite is **malevolent** (wishing harm). A, C and D are all synonyms — a classic distractor pattern in the "spotting the odd one" style.

**Q22 — (C).** **Since** is used with a *point* in time (since 2015, since Monday); *for* is used with a *duration* (for ten years).

**Q23 — (A).** Each letter advances by one: M→N, O→P, N→O, D→E, A→B, Y→Z. Applying +1 to FRIDAY: F→G, R→S, I→J, D→E, A→B, Y→Z = **GSJEBZ**.

**Q24 — (C).** Each term is 2ⁿ − 1: 3, 7, 15, 31, 63, **127**. (Equivalently, double and add 1.)

**Q25 — (C).** Tripura merged with the Indian Union on **15 October 1949**, became a Union Territory in 1956, and attained **full statehood on 21 January 1972** under the North-Eastern Areas (Reorganisation) Act, 1971 — the same day as Manipur and Meghalaya. Option A is the merger date, and is the intended trap.

---

## Score

| | |
|---|---|
| Part A (Digital Logic) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

Record in `01_Study_Plan/Weekly_Progress_Tracker.md` and log every wrong answer.

**Weak-area pointers:** missed Q3/Q4 → redo number representation; missed Q6/Q7/Q8 → redo combinational circuits; missed Q9–Q12 → redo sequential circuits and counters. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S02_Digital_Logic/` (313 questions).
