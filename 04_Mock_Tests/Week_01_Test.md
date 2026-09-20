# Week 1 Question Bank — Digital Logic & Number Systems

**Syllabus §2** · 170 questions · Practice set · +1 / −0.33 marking · No calculator

> These are expanded practice questions covering every subtopic of §2; attempt in timed batches of 25–30.

---

## Part A — Number Systems, Bases & Conversions

**Q1.** The decimal equivalent of the binary number `(110110)₂` is
(A) 54  (B) 46  (C) 108  (D) 27

**Q2.** The decimal number 45 converted to binary is
(A) `101101`  (B) `101100`  (C) `110101`  (D) `101011`

**Q3.** The hexadecimal equivalent of `(10110110)₂` is
(A) `A6`  (B) `B6`  (C) `C6`  (D) `D6`

**Q4.** The octal equivalent of `(10110110)₂` is
(A) `266`  (B) `256`  (C) `366`  (D) `276`

**Q5.** The decimal value of `(2F)₁₆` is
(A) 31  (B) 47  (C) 45  (D) 62

**Q6.** The decimal value of `(17)₈` is
(A) 17  (B) 23  (C) 15  (D) 11

**Q7.** The decimal value of `(11001)₂` is
(A) 25  (B) 27  (C) 19  (D) 11

**Q8.** The binary representation of decimal `0.625` is
(A) `0.101`  (B) `0.011`  (C) `0.110`  (D) `0.111`

**Q9.** The decimal value of `(1AB)₁₆` is
(A) 427  (B) 417  (C) 683  (D) 171

**Q10.** The binary equivalent of the octal number `(725)₈` is
(A) `111010101`  (B) `111001101`  (C) `110010101`  (D) `111010111`

**Q11.** The minimum number of bits needed to represent the unsigned decimal number 1000 is
(A) 9  (B) 10  (C) 11  (D) 8

**Q12.** Which number system uses only the digits 0 to 7?
(A) Binary  (B) Octal  (C) Decimal  (D) Hexadecimal

**Q13.** The decimal value of `(110.1)₂` is
(A) 6.5  (B) 6.25  (C) 12.5  (D) 3.5

**Q14.** The hexadecimal representation of decimal 255 is
(A) `EF`  (B) `FE`  (C) `FF`  (D) `F0`

**Q15.** Which of the following decimal fractions is NON-terminating (recurring) when written in binary?
(A) 0.5  (B) 0.25  (C) 0.1  (D) 0.75

---

## Part B — Signed Representation, 2's Complement & Overflow

**Q16.** In 8-bit 2's complement representation, the range of integers is
(A) −127 to +127  (B) −128 to +127  (C) −128 to +128  (D) 0 to 255

**Q17.** The 2's complement of the 8-bit number `01011010` is
(A) `10100101`  (B) `10100110`  (C) `10100111`  (D) `01011011`

**Q18.** The 1's complement of the 8-bit number `01011010` is
(A) `10100101`  (B) `10100110`  (C) `10100100`  (D) `01011011`

**Q19.** In 4-bit 2's complement, the representation of −5 is
(A) `1010`  (B) `1011`  (C) `1101`  (D) `0101`

**Q20.** In 4-bit 2's complement, the pattern `1111` represents
(A) −1  (B) −15  (C) 15  (D) −7

**Q21.** In 4-bit 2's complement, the pattern `1000` represents
(A) −8  (B) 8  (C) 0  (D) −0

**Q22.** Computing 7 − 5 in 4-bit 2's complement arithmetic gives the result bits
(A) `0010`  (B) `0011`  (C) `1110`  (D) `0001`

**Q23.** Which representation(s) have TWO distinct patterns for zero?
(A) 2's complement only  (B) Unsigned  (C) Signed-magnitude and 1's complement  (D) 2's complement and unsigned

**Q24.** For signed (2's complement) addition, overflow is detected by
(A) C_in(MSB) ⊕ C_out(MSB)  (B) carry-out = 1  (C) MSB of result = 1  (D) C_in(MSB) · C_out(MSB)

**Q25.** In 4-bit 2's complement, adding (+5) + (+4) gives
(A) `1001`, with overflow  (B) `1001`, no overflow  (C) `0110`, no overflow  (D) `1000`, with overflow

**Q26.** Which addition can NEVER produce a signed overflow?
(A) Two positive numbers  (B) Two negative numbers  (C) Numbers of opposite signs  (D) Any addition

**Q27.** The decimal value of the 8-bit 2's complement number `10100110` is
(A) −90  (B) −86  (C) 166  (D) −38

**Q28.** The 8-bit 2's complement representation of −20 is
(A) `11101100`  (B) `11101011`  (C) `00010100`  (D) `11101101`

**Q29.** How many negative numbers can be represented in 8-bit 2's complement?
(A) 127  (B) 128  (C) 255  (D) 256

**Q30.** For UNSIGNED addition, overflow occurs when
(A) MSB of result = 1  (B) the final carry-out is 1  (C) C_in ⊕ C_out = 1  (D) result = 0

**Q31.** In a processor, the subtraction A − B is performed as
(A) A + (2's complement of B)  (B) A + (1's complement of B)  (C) A − B directly by a subtractor  (D) B − A

---

## Part C — Binary Codes (BCD, Gray, Excess-3, ASCII)

**Q32.** The Gray code equivalent of the binary number `1011` is
(A) `1110`  (B) `1101`  (C) `1010`  (D) `1111`

**Q33.** The binary equivalent of the Gray code `1110` is
(A) `1011`  (B) `1001`  (C) `1100`  (D) `1111`

**Q34.** The BCD (8421) representation of decimal 25 is
(A) `00100101`  (B) `11001`  (C) `00110111`  (D) `01000101`

**Q35.** In BCD (8421), which group of 4-bit codes is INVALID?
(A) `0000`–`0101`  (B) `1010`–`1111`  (C) `0110`–`1001`  (D) None

**Q36.** The Excess-3 code is
(A) weighted  (B) self-complementing  (C) a cyclic code  (D) unweighted and non-self-complementing

**Q37.** The defining property of Gray code is that
(A) successive values differ in exactly one bit  (B) it is weighted  (C) two bits change per step  (D) it is self-complementing

**Q38.** Standard (non-extended) ASCII uses how many bits per character?
(A) 7  (B) 8  (C) 16  (D) 6

**Q39.** The Gray code equivalent of the binary number `0111` is
(A) `0100`  (B) `0101`  (C) `1000`  (D) `0111`

**Q40.** The Excess-3 code for decimal 5 is
(A) `0101`  (B) `1000`  (C) `0010`  (D) `1001`

**Q41.** In a BCD adder, a correction value is added to the sum whenever it exceeds 9. That correction is
(A) `0110`  (B) `0011`  (C) `1010`  (D) `1001`

**Q42.** Gray code is most commonly used in
(A) arithmetic logic units  (B) shaft/position encoders  (C) floating-point units  (D) cache memory

---

## Part D — Fixed & Floating Point (IEEE-754)

**Q43.** In IEEE-754 single precision, the number of exponent bits and the bias are, respectively,
(A) 8 and 128  (B) 8 and 127  (C) 11 and 1023  (D) 23 and 127

**Q44.** In IEEE-754 double precision, the number of exponent bits and the bias are, respectively,
(A) 8 and 127  (B) 11 and 1023  (C) 11 and 1024  (D) 8 and 128

**Q45.** For a k-bit exponent field, the IEEE-754 bias is
(A) 2ᵏ − 1  (B) 2^(k−1) − 1  (C) 2^(k−1)  (D) 2ᵏ

**Q46.** Because of the hidden (implicit) leading bit, single precision provides how many bits of effective precision?
(A) 23  (B) 24  (C) 32  (D) 8

**Q47.** The IEEE-754 single-precision number `41400000₁₆` represents the value
(A) 12.0  (B) 6.5  (C) 1.5  (D) 24.0

**Q48.** The value −6.5 encoded in IEEE-754 single precision (in hex) is
(A) `C1D00000`  (B) `41D00000`  (C) `C1500000`  (D) `C1C80000`

**Q49.** In IEEE-754, an exponent field of all 1s with mantissa = 0 represents
(A) zero  (B) infinity  (C) NaN  (D) a denormalised number

**Q50.** In IEEE-754, an exponent field of all 1s with mantissa ≠ 0 represents
(A) infinity  (B) NaN  (C) zero  (D) a denormalised number

**Q51.** In IEEE-754, an exponent field of all 0s with mantissa ≠ 0 represents
(A) a normal number  (B) a denormalised number  (C) infinity  (D) NaN

**Q52.** The total width of an IEEE-754 double-precision number is
(A) 32 bits  (B) 64 bits  (C) 80 bits  (D) 128 bits

**Q53.** The word "floating" in floating point refers to the fact that
(A) the binary point is fixed  (B) the binary point moves depending on the exponent  (C) the sign floats  (D) the mantissa is fixed

**Q54.** The value of a normalised IEEE-754 number is given by
(A) (−1)^S × 1.M × 2^(E − bias)  (B) (−1)^S × 0.M × 2^E  (C) (−1)^S × M × 2^bias  (D) (−1)^S × 1.M × 2^E

---

## Part E — Boolean Algebra & De Morgan's Theorems

**Q55.** The Boolean expression `A + A'B` simplifies to
(A) A  (B) B  (C) A + B  (D) A'B

**Q56.** In Boolean algebra, `A + 1` equals
(A) A  (B) 1  (C) 0  (D) A'

**Q57.** In Boolean algebra, `A + A` equals
(A) 2A  (B) A  (C) 1  (D) 0

**Q58.** By the absorption law, `A + AB` equals
(A) A  (B) B  (C) AB  (D) A + B

**Q59.** The expression `A · A'` equals
(A) A  (B) 1  (C) 0  (D) A'

**Q60.** By involution, `(A')'` equals
(A) A'  (B) A  (C) 1  (D) 0

**Q61.** By De Morgan's theorem, `(A · B)'` equals
(A) A' · B'  (B) A' + B'  (C) A + B  (D) AB

**Q62.** Applying De Morgan's theorem, `(A + B + C)'` equals
(A) A' + B' + C'  (B) A' · B' · C'  (C) A'·B' + C'  (D) (A·B·C)'

**Q63.** By the consensus theorem, `AB + A'C + BC` equals
(A) AB + A'C  (B) AB + BC  (C) A'C + BC  (D) AB + A'C + BC

**Q64.** The DUAL of the identity `A + 1 = 1` is
(A) A · 0 = 0  (B) A + 0 = A  (C) A · 1 = A  (D) A' = 1

**Q65.** The number of distinct Boolean functions of 2 variables is
(A) 4  (B) 8  (C) 16  (D) 2

**Q66.** The number of distinct Boolean functions of n variables is
(A) 2ⁿ  (B) 2^(2ⁿ)  (C) n²  (D) 2n

**Q67.** The expression `A ⊕ A` equals
(A) A  (B) 0  (C) 1  (D) A'

**Q68.** The expression `A ⊕ A'` equals
(A) 0  (B) 1  (C) A  (D) A'

**Q69.** The expression `A ⊕ 1` equals
(A) A  (B) A'  (C) 1  (D) 0

**Q70.** The simplified complement `(AB' + C)'` equals
(A) (A' + B)·C'  (B) A'B·C'  (C) A'B + C'  (D) (A + B')·C'

**Q71.** By the distributive law (OR form), `A + BC` equals
(A) (A + B)(A + C)  (B) AB + AC  (C) (A + B)C  (D) A(B + C)

**Q72.** An XOR gate outputs 1 when
(A) both inputs are equal  (B) the inputs differ  (C) both inputs are 1  (D) both inputs are 0

**Q73.** An n-input XOR gate acts as a detector of
(A) even parity  (B) an odd number of 1s  (C) all-ones  (D) majority

**Q74.** The duality principle differs from De Morgan's theorem because duality
(A) also complements the variables  (B) does NOT complement the variables  (C) changes nothing  (D) only inverts the output

---

## Part F — Minterms, Maxterms, Canonical Forms & K-Maps

**Q75.** The minimal SOP for `F(A,B,C) = Σm(1, 3, 5, 7)` is
(A) A  (B) B  (C) C  (D) A'C

**Q76.** The maximum number of minterms in a Boolean function of 5 variables is
(A) 5  (B) 10  (C) 25  (D) 32

**Q77.** In a minterm, a variable appears in COMPLEMENTED form when its bit value is
(A) 0  (B) 1  (C) X  (D) either

**Q78.** The relationship between the minterm mᵢ and maxterm Mᵢ of the same index is
(A) mᵢ = Mᵢ  (B) mᵢ' = Mᵢ  (C) mᵢ + Mᵢ = 1  (D) mᵢ · Mᵢ = 1

**Q79.** A group of 2ᵏ cells in a K-map eliminates
(A) k variables  (B) 2k variables  (C) k − 1 variables  (D) 2ᵏ variables

**Q80.** In a 4-variable K-map, the four corner cells
(A) cannot be grouped  (B) form a valid group of 4  (C) form a group of 2  (D) form an invalid group

**Q81.** An ESSENTIAL prime implicant is one that
(A) is any valid group  (B) covers at least one 1 that no other prime implicant covers  (C) is the largest group  (D) is redundant

**Q82.** A prime implicant is an implicant that
(A) cannot be enlarged into a bigger valid group  (B) is a single cell  (C) contains only don't-cares  (D) is a maxterm

**Q83.** The minimal expression for `F(A,B,C,D) = Σm(0,1,2,3,8,9,10,11)` is
(A) B'  (B) A'  (C) C'  (D) D'

**Q84.** The minimal expression for `F(A,B,C,D) = Σm(0,2,8,10)` is
(A) B'D'  (B) BD  (C) A'C'  (D) B'C'

**Q85.** The rule for don't-care conditions in K-maps is
(A) treat all as 1  (B) never form a group consisting only of don't-cares  (C) always ignore them  (D) always treat as 0

**Q86.** Which minimisation method is best suited for computer implementation with many variables?
(A) Karnaugh map  (B) Quine–McCluskey  (C) truth table inspection  (D) Venn diagram

**Q87.** The canonical Sum-of-Products form of a function is a
(A) sum of minterms  (B) product of maxterms  (C) sum of maxterms  (D) product of minterms

**Q88.** The number of cells in a 4-variable K-map is
(A) 8  (B) 16  (C) 4  (D) 32

**Q89.** For variables A, B, C, the minterm m₅ is
(A) AB'C  (B) A'BC  (C) ABC'  (D) AB'C'

**Q90.** To obtain the minimal POS form from a K-map, you group the
(A) 1s  (B) 0s  (C) don't-cares  (D) corners

**Q91.** The number of rows in the truth table of an n-variable function is
(A) n  (B) 2n  (C) 2ⁿ  (D) n²

---

## Part G — Logic Gates & Universality

**Q92.** Which of the following is a universal gate?
(A) AND  (B) OR  (C) NAND  (D) XOR

**Q93.** Which PAIR of gates are BOTH universal?
(A) AND, OR  (B) NAND, NOR  (C) XOR, XNOR  (D) NOT, AND

**Q94.** The number of NAND gates required to build a NOT gate is
(A) 1  (B) 2  (C) 3  (D) 4

**Q95.** The number of NAND gates required to build an AND gate is
(A) 1  (B) 2  (C) 3  (D) 4

**Q96.** An XNOR gate outputs 1 when
(A) the inputs differ  (B) the inputs are equal  (C) both are 0  (D) both are 1

**Q97.** A NAND gate outputs 0 ONLY when
(A) all inputs are 0  (B) all inputs are 1  (C) the inputs differ  (D) any input is 1

**Q98.** A NOR gate outputs 1 ONLY when
(A) all inputs are 0  (B) all inputs are 1  (C) any input is 1  (D) the inputs differ

**Q99.** Which of the following gates is NOT universal?
(A) NAND  (B) NOR  (C) XOR  (D) both NAND and NOR

**Q100.** The number of NAND gates required to build an OR gate is
(A) 1  (B) 2  (C) 3  (D) 4

**Q101.** Besides NAND and NOR gates, which of the following can by itself implement any Boolean function?
(A) a multiplexer  (B) a half adder  (C) a decoder alone  (D) an encoder

---

## Part H — Multiplexer, Demultiplexer, Decoder & Encoder

**Q102.** A Boolean function of 4 variables can be implemented using a single multiplexer of minimum size
(A) 4 : 1  (B) 8 : 1  (C) 16 : 1  (D) 2 : 1

**Q103.** A decoder with n input lines has a maximum of how many output lines?
(A) n  (B) 2n  (C) 2ⁿ  (D) n²

**Q104.** A 2ⁿ : 1 multiplexer has how many select lines?
(A) n  (B) 2ⁿ  (C) 2n  (D) n²

**Q105.** The number of select lines in an 8 : 1 multiplexer is
(A) 2  (B) 3  (C) 4  (D) 8

**Q106.** The minimum multiplexer needed to implement a 3-variable function is
(A) 2 : 1  (B) 4 : 1  (C) 8 : 1  (D) 16 : 1

**Q107.** An n-to-2ⁿ decoder generates
(A) all maxterms  (B) all minterms  (C) exactly one output always  (D) parity

**Q108.** A priority encoder is used to
(A) add numbers  (B) resolve the case when several inputs are active at once  (C) store data  (D) select one of many inputs

**Q109.** A demultiplexer is functionally the
(A) same as a multiplexer  (B) reverse of a multiplexer  (C) same as an encoder  (D) same as a comparator

**Q110.** The number of data inputs in a 4 : 1 multiplexer is
(A) 2  (B) 4  (C) 8  (D) 1

**Q111.** An encoder with 2ⁿ input lines has how many output lines?
(A) 2ⁿ  (B) n  (C) 2n  (D) 1

**Q112.** A decoder can implement any Boolean function when combined with
(A) OR gates  (B) flip-flops  (C) a counter  (D) nothing else

**Q113.** On a 4 : 1 multiplexer, the select combination S₁S₀ = 10 routes which input to the output?
(A) I0  (B) I1  (C) I2  (D) I3

---

## Part I — Adders & Arithmetic Circuits

**Q114.** A full adder can be realised using
(A) two half adders and one OR gate  (B) two half adders and one AND gate  (C) one half adder and one OR gate  (D) three half adders

**Q115.** In a carry look-ahead adder, the generate Gᵢ and propagate Pᵢ functions are
(A) Gᵢ = Aᵢ ⊕ Bᵢ, Pᵢ = Aᵢ·Bᵢ  (B) Gᵢ = Aᵢ·Bᵢ, Pᵢ = Aᵢ ⊕ Bᵢ  (C) Gᵢ = Aᵢ + Bᵢ, Pᵢ = Aᵢ·Bᵢ  (D) Gᵢ = Aᵢ·Bᵢ, Pᵢ = Aᵢ + Bᵢ

**Q116.** In a half adder, the SUM output is
(A) A·B  (B) A ⊕ B  (C) A + B  (D) A'B

**Q117.** In a half adder, the CARRY output is
(A) A ⊕ B  (B) A + B  (C) A · B  (D) A'B

**Q118.** In a full adder, the SUM output is
(A) A ⊕ B  (B) A ⊕ B ⊕ C_in  (C) AB + C_in  (D) A·B·C_in

**Q119.** In a full adder, the CARRY-OUT is
(A) AB + C_in(A ⊕ B)  (B) A ⊕ B ⊕ C_in  (C) A·B·C_in  (D) A + B + C_in

**Q120.** The propagation delay of an n-bit ripple-carry adder is approximately
(A) constant  (B) n × (delay per full adder)  (C) log n  (D) n²

**Q121.** The carry-generation delay of a carry look-ahead adder is
(A) O(n)  (B) O(1) / constant  (C) O(log n)  (D) O(n²)

**Q122.** The carry recurrence in a CLA is
(A) Cᵢ₊₁ = Gᵢ + Pᵢ·Cᵢ  (B) Cᵢ₊₁ = Pᵢ + Gᵢ·Cᵢ  (C) Cᵢ₊₁ = Gᵢ·Pᵢ  (D) Cᵢ₊₁ = Gᵢ ⊕ Cᵢ

**Q123.** In a magnitude comparator, the bit-wise EQUALITY (A = B) is checked using
(A) XOR gates  (B) XNOR gates  (C) NAND gates  (D) OR gates

**Q124.** A 32-bit ripple-carry adder with 2 ns delay per stage settles in
(A) 32 ns  (B) 64 ns  (C) 2 ns  (D) 16 ns

**Q125.** Subtraction A − B is normally implemented using
(A) a dedicated subtractor  (B) an adder fed with the 2's complement of B  (C) a comparator  (D) a decoder

---

## Part J — Flip-Flops & Excitation Tables

**Q126.** In a JK flip-flop, when J = K = 1, the output on the next clock edge
(A) is set to 1  (B) is reset to 0  (C) toggles  (D) is unchanged

**Q127.** The master–slave configuration of a flip-flop is primarily used to eliminate
(A) propagation delay  (B) the race-around condition  (C) power dissipation  (D) fan-out limitation

**Q128.** The forbidden input combination of an SR flip-flop is
(A) S = R = 0  (B) S = 0, R = 1  (C) S = 1, R = 0  (D) S = R = 1

**Q129.** The characteristic equation of a D flip-flop is
(A) Q(n+1) = D  (B) Q(n+1) = D ⊕ Q  (C) Q(n+1) = DQ'  (D) Q(n+1) = D + Q

**Q130.** The characteristic equation of a T flip-flop is
(A) Q(n+1) = T  (B) Q(n+1) = T ⊕ Q  (C) Q(n+1) = TQ  (D) Q(n+1) = T + Q

**Q131.** The characteristic equation of a JK flip-flop is
(A) Q(n+1) = JQ' + K'Q  (B) Q(n+1) = J + K'Q  (C) Q(n+1) = JQ + K'Q'  (D) Q(n+1) = J'Q + KQ'

**Q132.** In the excitation table of a JK flip-flop, the transition Q: 0 → 1 requires
(A) J = 1, K = X  (B) J = 0, K = X  (C) J = X, K = 1  (D) J = X, K = 0

**Q133.** In the excitation table of a JK flip-flop, the transition Q: 1 → 0 requires
(A) J = 1, K = X  (B) J = X, K = 1  (C) J = 0, K = X  (D) J = X, K = 0

**Q134.** The essential difference between a latch and a flip-flop is that
(A) a latch is edge-triggered  (B) a flip-flop is level-triggered  (C) a latch is level-triggered while a flip-flop is edge-triggered  (D) there is no difference

**Q135.** The race-around condition occurs when
(A) the clock pulse width is greater than the flip-flop propagation delay  (B) the clock width is less than the delay  (C) J = K = 0  (D) the clock is stopped

**Q136.** A D flip-flop is obtained from a JK flip-flop by setting
(A) J = K = D  (B) J = D, K = D'  (C) J = D', K = D  (D) J = 1, K = 0

**Q137.** In the excitation table of a T flip-flop, the transition Q: 1 → 1 requires
(A) T = 0  (B) T = 1  (C) T = X  (D) T = Q

---

## Part K — Counters, Shift Registers, FSMs & Logic Families

**Q138.** The minimum number of flip-flops required to build a MOD-12 counter is
(A) 3  (B) 4  (C) 6  (D) 12

**Q139.** An n-bit ring counter and an n-bit Johnson (twisted-ring) counter have, respectively, how many distinct states?
(A) n and n  (B) n and 2n  (C) 2n and n  (D) 2ⁿ and n

**Q140.** A 4-bit ripple (asynchronous) counter uses flip-flops each with 10 ns propagation delay. The maximum settling time is
(A) 10 ns  (B) 20 ns  (C) 40 ns  (D) 4 ns

**Q141.** In a Moore machine, the output depends on
(A) the present state only  (B) the present state and the present input  (C) the present input only  (D) the next state only

**Q142.** The minimum number of flip-flops required for a MOD-100 counter is
(A) 6  (B) 7  (C) 10  (D) 100

**Q143.** The maximum modulus achievable with n flip-flops is
(A) n  (B) 2n  (C) 2ⁿ  (D) n²

**Q144.** The number of distinct states in a 4-bit Johnson counter is
(A) 4  (B) 8  (C) 15  (D) 16

**Q145.** The total propagation delay of a synchronous counter is approximately
(A) n × t_pd  (B) one flip-flop delay  (C) n² · t_pd  (D) log n

**Q146.** A SIPO shift register performs
(A) parallel-to-serial conversion  (B) serial-to-parallel conversion  (C) serial-to-serial conversion  (D) parallel-to-parallel conversion

**Q147.** Left-shifting a binary number by one position is equivalent to
(A) division by 2  (B) multiplication by 2  (C) adding 1  (D) multiplication by 4

**Q148.** Compared with a Moore machine, a Mealy machine for the same task usually needs
(A) more states  (B) fewer states  (C) the same number of states  (D) no states

**Q149.** In a Mealy machine, outputs are associated with the
(A) states (circles)  (B) transitions (arrows)  (C) clock  (D) inputs only

**Q150.** Which logic family has the lowest static power consumption?
(A) TTL  (B) CMOS  (C) ECL  (D) RTL

**Q151.** The fastest logic family is
(A) TTL  (B) CMOS  (C) ECL  (D) PMOS

**Q152.** A tri-state buffer is used to
(A) provide three logic levels for computation  (B) allow many devices to share a single bus  (C) speed up adders  (D) count events

**Q153.** The fan-out of a gate refers to
(A) the number of its inputs  (B) the number of gate inputs its output can reliably drive  (C) its propagation delay  (D) its power dissipation

**Q154.** Regarding computational power, Mealy and Moore machines are
(A) Moore is more powerful  (B) Mealy is more powerful  (C) equally powerful  (D) incomparable

**Q155.** A drawback of an asynchronous (ripple) counter is that
(A) it needs a shared clock  (B) it shows transient invalid (glitch) states while the carry ripples  (C) it has too few states  (D) it has no drawback

---

## Part L — Paper-I (English, Reasoning & GK)

**Q156.** Choose the word most nearly OPPOSITE in meaning to BENEVOLENT.
(A) Generous  (B) Malevolent  (C) Charitable  (D) Kind

**Q157.** Fill in the blank: *"She has been living in Agartala ___ 2015."*
(A) for  (B) from  (C) since  (D) by

**Q158.** If `MONDAY` is coded as `NPOEBZ`, then `FRIDAY` is coded as
(A) `GSJEBZ`  (B) `GSJFBZ`  (C) `ESHCZX`  (D) `GTJEBZ`

**Q159.** Find the next term: 3, 7, 15, 31, 63, ___
(A) 95  (B) 121  (C) 127  (D) 128

**Q160.** Tripura attained full-fledged statehood in the Indian Union on
(A) 15 October 1949  (B) 1 November 1956  (C) 21 January 1972  (D) 20 February 1987

**Q161.** Choose the word most nearly SIMILAR in meaning to DILIGENT.
(A) Lazy  (B) Hardworking  (C) Careless  (D) Slow

**Q162.** One word for "a person who cannot read or write":
(A) Illiterate  (B) Ignorant  (C) Novice  (D) Amateur

**Q163.** Find the next term: 2, 6, 12, 20, 30, ___
(A) 36  (B) 40  (C) 42  (D) 44

**Q164.** Doctor : Hospital :: Teacher : ?
(A) Student  (B) School  (C) Book  (D) Class

**Q165.** Find the next term: 1, 4, 9, 16, 25, ___
(A) 30  (B) 36  (C) 49  (D) 35

**Q166.** The idiom "to bury the hatchet" means
(A) to dig a hole  (B) to make peace  (C) to hide something  (D) to start a fight

**Q167.** The capital of Tripura is
(A) Aizawl  (B) Agartala  (C) Imphal  (D) Shillong

**Q168.** If A > B and B > C, then
(A) A < C  (B) A = C  (C) A > C  (D) cannot be determined

**Q169.** Which of the following rivers flows through Tripura?
(A) Gomati (Gumti)  (B) Kaveri  (C) Godavari  (D) Sutlej

**Q170.** Choose the CORRECTLY spelled word.
(A) Occurence  (B) Occurrence  (C) Occurance  (D) Ocurrence

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | A | 2 | A | 3 | B | 4 | A | 5 | B | 6 | C | 7 | A | 8 | A | 9 | A | 10 | A |
| 11 | B | 12 | B | 13 | A | 14 | C | 15 | C | 16 | B | 17 | B | 18 | A | 19 | B | 20 | A |
| 21 | A | 22 | A | 23 | C | 24 | A | 25 | A | 26 | C | 27 | A | 28 | A | 29 | B | 30 | B |
| 31 | A | 32 | A | 33 | A | 34 | A | 35 | B | 36 | B | 37 | A | 38 | A | 39 | A | 40 | B |
| 41 | A | 42 | B | 43 | B | 44 | B | 45 | B | 46 | B | 47 | A | 48 | A | 49 | B | 50 | B |
| 51 | B | 52 | B | 53 | B | 54 | A | 55 | C | 56 | B | 57 | B | 58 | A | 59 | C | 60 | B |
| 61 | B | 62 | B | 63 | A | 64 | A | 65 | C | 66 | B | 67 | B | 68 | B | 69 | B | 70 | A |
| 71 | A | 72 | B | 73 | B | 74 | B | 75 | C | 76 | D | 77 | A | 78 | B | 79 | A | 80 | B |
| 81 | B | 82 | A | 83 | A | 84 | A | 85 | B | 86 | B | 87 | A | 88 | B | 89 | A | 90 | B |
| 91 | C | 92 | C | 93 | B | 94 | A | 95 | B | 96 | B | 97 | B | 98 | A | 99 | C | 100 | C |
| 101 | A | 102 | B | 103 | C | 104 | A | 105 | B | 106 | B | 107 | B | 108 | B | 109 | B | 110 | B |
| 111 | B | 112 | A | 113 | C | 114 | A | 115 | B | 116 | B | 117 | C | 118 | B | 119 | A | 120 | B |
| 121 | B | 122 | A | 123 | B | 124 | B | 125 | B | 126 | C | 127 | B | 128 | D | 129 | A | 130 | B |
| 131 | A | 132 | A | 133 | B | 134 | C | 135 | A | 136 | B | 137 | A | 138 | B | 139 | B | 140 | C |
| 141 | A | 142 | B | 143 | C | 144 | B | 145 | B | 146 | B | 147 | B | 148 | B | 149 | B | 150 | B |
| 151 | C | 152 | B | 153 | B | 154 | C | 155 | B | 156 | B | 157 | C | 158 | A | 159 | C | 160 | C |
| 161 | B | 162 | A | 163 | C | 164 | B | 165 | B | 166 | B | 167 | B | 168 | C | 169 | A | 170 | B |

---

# 📝 Detailed Solutions

**Q1. (A)** `110110` = 32 + 16 + 0 + 4 + 2 + 0 = **54**. Reading the weights 2⁵…2⁰ for the set bits gives the value directly.

**Q2. (A)** Repeated division of 45 by 2 gives remainders 1,0,1,1,0,1 read bottom-up = `101101`. Check: 32+8+4+1 = 45.

**Q3. (B)** Group in 4s from the right: `1011|0110` = B|6 = **B6**. (`1011` = 11 = B, `0110` = 6.)

**Q4. (A)** Group in 3s from the right with a leading zero pad: `010|110|110` = 2|6|6 = **266**.

**Q5. (B)** `2F₁₆` = 2×16 + 15 = 32 + 15 = **47**. (F = 15.)

**Q6. (C)** `17₈` = 1×8 + 7 = **15**. Option A treats it as decimal, which is the trap.

**Q7. (A)** `11001` = 16 + 8 + 0 + 0 + 1 = **25**.

**Q8. (A)** 0.625×2 = 1.25 (1); 0.25×2 = 0.5 (0); 0.5×2 = 1.0 (1) → **0.101**. Check: 0.5 + 0.125 = 0.625.

**Q9. (A)** `1AB₁₆` = 1×256 + 10×16 + 11 = 256 + 160 + 11 = **427**.

**Q10. (A)** Each octal digit → 3 bits: 7=`111`, 2=`010`, 5=`101` → **111010101**.

**Q11. (B)** 2⁹ = 512 < 1000 ≤ 1024 = 2¹⁰, so **10** bits are needed. (⌊log₂1000⌋ + 1 = 9 + 1 = 10.)

**Q12. (B)** Octal (base 8) uses digits 0–7. Binary uses 0–1, decimal 0–9, hex 0–F.

**Q13. (A)** `110.1` = 4 + 2 + 0 + 0.5 = **6.5**. The `.1` after the point is 2⁻¹ = 0.5.

**Q14. (C)** 255 = 2⁸ − 1 = `11111111` = `FF₁₆`. Two hex digits of all 1s.

**Q15. (C)** 0.1 has no finite binary expansion (it is `0.0001100110011…` recurring); 0.5, 0.25 and 0.75 are exact sums of negative powers of 2.

**Q16. (B)** n-bit 2's complement spans −2ⁿ⁻¹ to +2ⁿ⁻¹ − 1 = **−128 to +127**; the asymmetry arises because there is only one zero.

**Q17. (B)** Invert `01011010` → `10100101`; add 1 → **`10100110`**. Option A is the 1's complement (the classic trap).

**Q18. (A)** 1's complement = invert every bit only: `01011010` → **`10100101`** (no +1).

**Q19. (B)** 5 = `0101`; invert → `1010`; add 1 → **`1011`**. Check: −8 + 2 + 1 = −5.

**Q20. (A)** In 4-bit 2's complement `1111` = −8 + 4 + 2 + 1 = **−1**, not −15 (that would be sign-magnitude thinking).

**Q21. (A)** `1000` uses the MSB weight only: −2³ = **−8**. This is the extra negative value with no positive counterpart.

**Q22. (A)** 7 = `0111`; −5 = `1011`; `0111 + 1011 = 10010`; discard the carry-out → `0010` = **2**.

**Q23. (C)** Signed-magnitude has +0/−0 and 1's complement has `0000`/`1111`; 2's complement and unsigned each have exactly one zero.

**Q24. (A)** Overflow = carry into the sign bit XOR carry out of the sign bit = **C_in(MSB) ⊕ C_out(MSB)**.

**Q25. (A)** `0101 + 0100 = 1001` = −7 in 4-bit 2's complement; two positives gave a negative, so **overflow occurs**. The true 9 is out of the −8..+7 range.

**Q26. (C)** Adding a positive and a negative yields a magnitude between the two operands, which always fits — **opposite signs never overflow**.

**Q27. (A)** Using MSB weight −128: `10100110` = −128 + 32 + 4 + 2 = **−90**.

**Q28. (A)** 20 = `00010100`; invert → `11101011`; add 1 → **`11101100`**. Check: −128 + 64 + 32 + 8 + 4 = −20.

**Q29. (B)** With 256 patterns and one zero, there are 127 positives and **128** negatives (patterns `10000000`…`11111111`).

**Q30. (B)** Unsigned overflow is simply a **final carry-out of 1**; the C_in⊕C_out test is only for signed overflow.

**Q31. (A)** The ALU computes A − B as **A + (2's complement of B)**, so only an adder is needed — the key advantage of 2's complement.

**Q32. (A)** Binary→Gray: keep MSB, then XOR adjacent bits. 1011 → G=1, 1⊕0=1... using Gᵢ=Bᵢ₊₁⊕Bᵢ gives 1,1,1,0 = **`1110`**.

**Q33. (A)** Gray→Binary: MSB copied, then running XOR. 1110 → B=1, 1⊕1=0, 0⊕1=1, 1⊕0=1 = **`1011`**.

**Q34. (A)** BCD encodes each decimal digit in 4 bits: 2 = `0010`, 5 = `0101` → **`00100101`**. Option B is plain binary (25 = `11001`).

**Q35. (B)** Valid BCD digits are `0000`–`1001`; codes **`1010`–`1111`** are the 6 invalid patterns per digit.

**Q36. (B)** Excess-3 (BCD + 0011) is **self-complementing** — the 9's complement of a digit equals the 1's complement of its code.

**Q37. (A)** Gray code is defined by **successive values differing in exactly one bit**, avoiding multi-bit transition glitches.

**Q38. (A)** Standard ASCII is a **7-bit** code (128 characters); extended ASCII uses 8 bits.

**Q39. (A)** Binary 0111 → Gray: G₃=0, G₂=0⊕1=1, G₁=1⊕1=0, G₀=1⊕1=0 = **`0100`**.

**Q40. (B)** Excess-3 of 5 = 5 + 3 = 8 = **`1000`**.

**Q41. (A)** When a BCD sum exceeds 9 (or generates a carry), add **`0110`** (6) to correct it into valid BCD.

**Q42. (B)** Gray code's single-bit-change property makes it ideal for **shaft/position encoders** (and K-map ordering).

**Q43. (B)** Single precision = 1 sign + **8 exponent** + 23 mantissa, bias **127**. Option A ("8 and 128") is the standard trap; C is the double-precision values.

**Q44. (B)** Double precision = 1 + **11** exponent + 52 mantissa, bias **1023**.

**Q45. (B)** Bias = **2^(k−1) − 1**; for k = 8 that is 127, for k = 11 it is 1023.

**Q46. (B)** The always-present leading 1 is not stored, so 23 stored bits give **24 bits** of effective precision.

**Q47. (A)** `41400000` = 0 | 10000010 | 100…; S=0, E=130 → exp 3, M = 1.1₂ = 1.5; value = 1.5 × 2³ = **12.0**.

**Q48. (A)** 6.5 = `110.1` = 1.101 × 2²; S=1, E = 2+127 = 129 = `10000001`, M = `101` padded → bits assemble to **`C1D00000`**.

**Q49. (B)** E = all 1s with M = 0 encodes ±**infinity**.

**Q50. (B)** E = all 1s with M ≠ 0 encodes **NaN** (Not a Number).

**Q51. (B)** E = all 0s with M ≠ 0 encodes a **denormalised** number (no hidden bit, value = 0.M × 2⁻¹²⁶).

**Q52. (B)** Double precision is **64 bits** total (1 + 11 + 52).

**Q53. (B)** "Floating" means the **binary point moves** with the exponent — the opposite of fixed point.

**Q54. (A)** The normalised value is **(−1)^S × 1.M × 2^(E − bias)**, combining sign, hidden-bit mantissa and biased exponent.

**Q55. (C)** A + A'B = (A + A')(A + B) = 1·(A + B) = **A + B** (absorption-2).

**Q56. (B)** Null/dominance law: once ORed with 1 the result is always **1**.

**Q57. (B)** Idempotent law: **A + A = A** (there is no "2A" in Boolean algebra).

**Q58. (A)** Absorption: A + AB = A(1 + B) = A·1 = **A**.

**Q59. (C)** Complement law: A·A' = **0** (a variable and its complement cannot both be 1).

**Q60. (B)** Involution: **(A')' = A** — double negation cancels.

**Q61. (B)** De Morgan: the complement of a product is the sum of complements → **A' + B'**.

**Q62. (B)** Complement of a sum = product of complements → **A'·B'·C'**.

**Q63. (A)** Consensus theorem: the BC term is redundant, so AB + A'C + BC = **AB + A'C**.

**Q64. (A)** Duality swaps AND↔OR and 0↔1 (no complementing of variables), so the dual of A + 1 = 1 is **A · 0 = 0**.

**Q65. (C)** Number of functions of n variables = 2^(2ⁿ); for n = 2 this is 2⁴ = **16**.

**Q66. (B)** With 2ⁿ truth-table rows each independently 0 or 1, the count is **2^(2ⁿ)**.

**Q67. (B)** A ⊕ A = **0** (identical inputs never differ).

**Q68. (B)** A ⊕ A' = **1** (a value and its complement always differ).

**Q69. (B)** XOR with 1 inverts: A ⊕ 1 = **A'**.

**Q70. (A)** (AB' + C)' = (AB')'·C' = (A' + B)·C' after De Morgan and involution → **(A' + B)·C'**.

**Q71. (A)** OR-form distributive law: **A + BC = (A + B)(A + C)** (no ordinary-algebra analogue).

**Q72. (B)** XOR outputs 1 exactly when the **inputs differ**.

**Q73. (B)** An n-input XOR outputs 1 for an **odd number of 1s** — it is a parity detector.

**Q74. (B)** Duality does **NOT complement the variables** (it only swaps AND/OR and 0/1); De Morgan does complement them.

**Q75. (C)** Minterms 1,3,5,7 in binary all have C = 1 with A,B varying, so F = **C**.

**Q76. (D)** n variables give 2ⁿ minterms; 2⁵ = **32**.

**Q77. (A)** In a minterm, a variable is **complemented when its bit is 0** (uncomplemented when 1).

**Q78. (B)** A maxterm is the complement of the same-index minterm: **mᵢ' = Mᵢ**.

**Q79. (A)** A group of 2ᵏ cells removes **k variables** (a group of 4 removes 2, etc.).

**Q80. (B)** By double wrap-around the four corners are mutually adjacent and **form a valid group of 4**.

**Q81. (B)** An essential prime implicant **covers at least one 1 that no other prime implicant covers**, so it must be in the final answer.

**Q82. (A)** A prime implicant is a group that **cannot be enlarged** into a bigger valid (power-of-2) group.

**Q83. (A)** These eight minterms are the whole top and bottom rows (AB = 00 and 10) where B = 0 throughout → **B'**.

**Q84. (A)** m0,m2,m8,m10 are the four corners; B = 0 and D = 0 across the group → **B'D'**.

**Q85. (B)** Don't-cares may be used to enlarge groups, but you must **never form a group of only don't-cares**.

**Q86. (B)** **Quine–McCluskey** is the tabular method suited to computer implementation for many variables.

**Q87. (A)** The canonical SOP (disjunctive normal form) is a **sum of minterms**.

**Q88. (B)** A 4-variable map has 2⁴ = **16** cells.

**Q89. (A)** m₅ → 101 → A=1, B=0, C=1 → **AB'C**.

**Q90. (B)** Minimal POS is obtained by grouping the **0s** (minimising F') and complementing.

**Q91. (C)** An n-variable truth table has **2ⁿ** rows.

**Q92. (C)** **NAND** is universal; AND, OR and XOR are not.

**Q93. (B)** **NAND and NOR** are the two universal gates.

**Q94. (A)** NOT A = A NAND A — a single NAND gate → **1**.

**Q95. (B)** A AND B = NOT(A NAND B), needing the NAND plus a NAND-inverter = **2** gates.

**Q96. (B)** XNOR outputs 1 when the **inputs are equal**.

**Q97. (B)** A NAND outputs 0 only when **all inputs are 1** (AND then invert).

**Q98. (A)** A NOR outputs 1 only when **all inputs are 0** (OR then invert).

**Q99. (C)** **XOR is not universal** (you cannot build NOT from XOR alone in general); both NAND and NOR are.

**Q100. (C)** A OR B = (NOT A) NAND (NOT B), needing two inverters plus one NAND = **3** gates.

**Q101. (A)** A **multiplexer** is itself a universal logic element — any function can be built from MUXes.

**Q102. (B)** An n-variable function needs a minimum 2ⁿ⁻¹ : 1 MUX; for n = 4 that is an **8 : 1** MUX.

**Q103. (C)** An n-input decoder produces at most **2ⁿ** outputs (one per input combination).

**Q104. (A)** A 2ⁿ : 1 MUX has **n** select lines.

**Q105. (B)** 8 = 2³, so an 8 : 1 MUX has **3** select lines.

**Q106. (B)** A 3-variable function needs a minimum 2³⁻¹ = 4 → **4 : 1** MUX (with the third variable/its complement on data lines).

**Q107. (B)** An n-to-2ⁿ decoder generates **all 2ⁿ minterms**, so decoder + OR gates realises any function.

**Q108. (B)** A **priority encoder** resolves the ambiguity when several inputs are active by choosing the highest-priority one.

**Q109. (B)** A DEMUX is the **reverse of a MUX** — one input routed to one of many outputs.

**Q110. (B)** A 4 : 1 MUX has **4** data inputs (and 2 select lines).

**Q111. (B)** An encoder maps 2ⁿ inputs to **n** outputs (inverse of a decoder).

**Q112. (A)** A decoder realises any function when its minterm outputs are combined with **OR gates**.

**Q113. (C)** S₁S₀ = 10 is binary 2, so the MUX passes **I2** to the output.

**Q114. (A)** A full adder = **two half adders + one OR gate**; the OR merges the two half-adder carries.

**Q115. (B)** **Gᵢ = Aᵢ·Bᵢ (AND)** and **Pᵢ = Aᵢ ⊕ Bᵢ (XOR)**; the reversed pairing in other options is the trap.

**Q116. (B)** Half-adder sum = **A ⊕ B**.

**Q117. (C)** Half-adder carry = **A · B**.

**Q118. (B)** Full-adder sum = **A ⊕ B ⊕ C_in**.

**Q119. (A)** Full-adder carry-out = **AB + C_in(A ⊕ B)** (equivalently AB + BC_in + AC_in).

**Q120. (B)** In a ripple-carry adder the carry propagates stage by stage, so delay ≈ **n × (per-stage delay)**.

**Q121. (B)** A CLA computes every carry as a two-level function of the inputs, giving **O(1)** carry delay.

**Q122. (A)** The CLA carry recurrence is **Cᵢ₊₁ = Gᵢ + Pᵢ·Cᵢ**.

**Q123. (B)** Bit-wise equality is detected by **XNOR** (output 1 when the two bits match).

**Q124. (B)** 32 stages × 2 ns = **64 ns** for a ripple-carry adder.

**Q125. (B)** Subtraction uses **an adder fed with the 2's complement of B**, so no dedicated subtractor is needed.

**Q126. (C)** With J = K = 1 the JK flip-flop **toggles** — the useful behaviour that replaces SR's forbidden state.

**Q127. (B)** The master–slave configuration eliminates the **race-around condition** by allowing only one toggle per clock.

**Q128. (D)** **S = R = 1** is forbidden in an SR flip-flop (contradictory set/reset, unpredictable settled state).

**Q129. (A)** D flip-flop: **Q(n+1) = D** (it stores whatever D is at the clock edge).

**Q130. (B)** T flip-flop: **Q(n+1) = T ⊕ Q** (T = 1 toggles, T = 0 holds).

**Q131. (A)** JK characteristic equation: **Q(n+1) = JQ' + K'Q**.

**Q132. (A)** For Q: 0 → 1 a JK needs **J = 1, K = X** (set, K don't-care).

**Q133. (B)** For Q: 1 → 0 a JK needs **J = X, K = 1** (reset, J don't-care).

**Q134. (C)** A **latch is level-triggered** (transparent while enabled) while a **flip-flop is edge-triggered** (samples on a clock edge).

**Q135. (A)** Race-around occurs when the **clock pulse width exceeds the flip-flop's propagation delay**, letting a level-triggered JK toggle repeatedly.

**Q136. (B)** A D flip-flop is made from a JK by setting **J = D, K = D'**.

**Q137. (A)** For a T flip-flop, Q holding at 1 (1 → 1) means no change, so **T = 0**.

**Q138. (B)** MOD-12 needs 12 states; ⌈log₂12⌉ = **4** flip-flops (3 give only 8).

**Q139. (B)** A ring counter gives **n** states (a single circulating 1); a Johnson counter gives **2n** states (complemented feedback).

**Q140. (C)** Ripple counter delays add: 4 × 10 = **40 ns**.

**Q141. (A)** In a Moore machine the output is a function of the **present state only**.

**Q142. (B)** ⌈log₂100⌉ = 7 (2⁶ = 64 < 100 ≤ 128 = 2⁷) → **7** flip-flops.

**Q143. (C)** n flip-flops give 2ⁿ distinct states, so the maximum modulus is **2ⁿ**.

**Q144. (B)** A 4-bit Johnson counter has 2n = 2×4 = **8** states.

**Q145. (B)** A synchronous counter clocks all flip-flops together, so total delay ≈ **one flip-flop delay** (plus combinational logic).

**Q146. (B)** SIPO = Serial In, Parallel Out — it performs **serial-to-parallel** conversion.

**Q147. (B)** A left shift appends a 0 at the LSB, **multiplying by 2**; a right shift divides by 2.

**Q148. (B)** A Mealy machine typically needs **fewer states** than the equivalent Moore machine.

**Q149. (B)** In a Mealy machine outputs are written on the **transitions (arrows)** as input/output.

**Q150. (B)** **CMOS** has very low static power (it draws current mainly while switching).

**Q151. (C)** **ECL** is the fastest logic family (non-saturating transistors), at the cost of high power.

**Q152. (B)** A tri-state buffer's high-impedance state lets **many devices share one bus** (all but one go to Z).

**Q153. (B)** Fan-out is the **number of gate inputs one output can reliably drive**.

**Q154. (C)** Mealy and Moore machines are **equally powerful** — each can be converted to the other.

**Q155. (B)** Because carries ripple, an asynchronous counter passes through **transient invalid (glitch) states** before settling.

**Q156. (B)** *Benevolent* (kind, well-meaning) is opposite to **malevolent** (wishing harm); generous, charitable and kind are all synonyms.

**Q157. (C)** **Since** is used with a point in time (since 2015); *for* is used with a duration.

**Q158. (A)** Each letter shifts +1: F→G, R→S, I→J, D→E, A→B, Y→Z = **GSJEBZ**.

**Q159. (C)** Each term is 2ⁿ − 1 (or double and add 1): 63 → 127 → **127**.

**Q160. (C)** Tripura became a full-fledged state on **21 January 1972** (1949 was the merger, 1956 the Union Territory status).

**Q161. (B)** *Diligent* means **hardworking**/industrious; the others are antonyms.

**Q162. (A)** A person who cannot read or write is **illiterate**.

**Q163. (C)** Differences are 4,6,8,10 → next difference 12 → 30 + 12 = **42** (pattern n(n+1)).

**Q164. (B)** A doctor works in a hospital as a teacher works in a **school** (workplace analogy).

**Q165. (B)** These are perfect squares 1²…5²; the next is 6² = **36**.

**Q166. (B)** "To bury the hatchet" means **to make peace** / end a quarrel.

**Q167. (B)** The capital of Tripura is **Agartala** (Aizawl = Mizoram, Imphal = Manipur, Shillong = Meghalaya).

**Q168. (C)** Transitivity of ">" gives **A > C**.

**Q169. (A)** The **Gomati (Gumti)** river flows through Tripura; the others are outside the state.

**Q170. (B)** The correct spelling is **Occurrence** (double c, double r).
