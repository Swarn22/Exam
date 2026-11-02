# 10 · General Ability — Quant, Reasoning & English — Precise Notes
> **TPSC ATO (IT) Paper-I §1–2** · 30 marks (fixed by the advertisement: English 15 + Mental Ability & Reasoning 15) · Syllabus: *"§1 English Composition — synonyms, antonyms, use of common phrase & idioms, use of appropriate prepositions and articles, comprehension, ordering of words in a sentence, ordering of sentences, spotting of errors, use of appropriate and qualifying words · §2 General Mental Ability & Logical reasoning — logical reasoning, analytical reasoning capabilities, quantitative and qualitative abilities, general aptitude"*
> Drawn from: R. S. Aggarwal *Quantitative Aptitude*, Made Easy reasoning & aptitude notes, the verbal-ability class notes, the English notes, the numerical-ability workbook. Refs like **[Src: RSA p.571]** point into `_source_pdfs/10_General_Ability/`.
> Paper-I §3 **GK & current affairs (20 marks)** is not covered by these sources — it is in `05_Notes/Paper1_English_Reasoning_GK.md` Part C. Paper-I needs **27.5 / 50 on its own** to qualify.

## Which notes are worth your time
| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 1.Quantitative_Aptitude…R_S_Aggarwal.pdf | R. S. Aggarwal | Typed textbook | 961 | 4.5 | **The standard quant book** — a formula block at the start of every chapter, then graded exercises · huge; one wrong clock fact (corrected below). Formula pages: number system 13–16, HCF/LCM 60, averages 215, % 317, P&L 383, ratio 435, partnership 485, pipes 519, work 535, TSD 571, boats 609, trains 621, alligation 642, SI 650, CI 672, area 697, volume 775, calendar 828, clocks 832, P&C 850, probability 859, series 877, DI 887 |
| 2.NA_Notes.pdf | Unlabelled ("Day N" workbook) | Handwritten CamScanner | 122 | 2.5 | Worked solutions only (questions mostly missing): TSD, P&L, mixtures, cube nets, coding, series · no formula sheets |
| 3.Reasoning_and_Aptitude_Made_Easy…pdf | Made Easy (GATE GA course) | Handwritten | 133 | 3.5 | Tricky aptitude: beam-balance weighings, pigeonhole socks, factor counting, 3-set Venn, clocks, P&C, painted cube, mean/SD shift · one arithmetic slip (corrected) |
| 4.VerbalAbility_Classnotes.pdf | Verbal-ability class notes | Handwritten | 100 | 3 | 58 grammar rules (nouns, SVA, tenses, speech, comparison), idioms, confused words · **several wrong entries** (corrected below); pp. 64–100 are engineering mechanics — off-topic |
| 5.English.pdf | Unlabelled | Handwritten scan | 41 | 3.5 | Compact grammar: tenses, speech, parallelism, dangling modifiers, sense verbs, much/very, some/any, each/every, SVA with "as well as" |

**If you open only one PDF besides these notes:** open **RS Aggarwal** at the formula page of the chapter you're practising, then do its first 20 exercise questions. For English use `05_Notes/Paper1_English_Reasoning_GK.md` Part A alongside Part C below.

## Topic map
| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1–4 | Numbers, %, P&L, interest | ⭐⭐⭐ | 1-step word problems |
| 5–7 | Ratio, averages, mixtures, ages | ⭐⭐ | Find the missing value |
| 8–10 | Work, pipes, speed/trains/boats | ⭐⭐⭐ | Time to finish / meet / cross |
| 11–13 | P&C, clocks & calendars, mensuration | ⭐⭐ | Count ways; angle; day of week; area/volume |
| 14 | Data interpretation | ⭐⭐ | % change, ratio from a table/chart |
| 15–21 | Reasoning (series → puzzles → syllogism → Venn) | ⭐⭐⭐ | 1-mark puzzles; series; coding; blood relation; direction |
| 22–24 | Grammar for error spotting | ⭐⭐⭐ | Spot the erroneous part / fill the blank |
| 25–26 | Articles & prepositions | ⭐⭐⭐ | Fill in the blank |
| 27–29 | Vocabulary: idioms, confused words, one-word, synonyms | ⭐⭐⭐ | Meaning of the idiom / closest word |
| 30 | Ordering words & sentences, comprehension | ⭐⭐ | Para-jumble; RC questions |

---

# PART A — QUANTITATIVE APTITUDE

## 1. Number System
- 📌 **Divisibility:** 2 (last digit even) · 3 / 9 (digit sum divisible by 3 / 9) · 4 (last two digits) · 8 (last three) · 5 (ends 0/5) · 6 (by 2 and 3) · 11 (**alternating digit sum** divisible by 11) **[Src: RSA p.13–16]**.
- 📌 If N = pᵃ·qᵇ·rᶜ (primes): **number of factors = (a + 1)(b + 1)(c + 1)**; number of odd factors = same product without the power of 2 **[Src: ME-Reasoning p.3–4]**. 🔢 360 = 2³·3²·5 → 4·3·2 = **24** factors, 6 odd.
- 📌 **Unit digits** cycle: 2 → 2, 4, 8, 6 · 3 → 3, 9, 7, 1 · 7 → 7, 9, 3, 1 · 8 → 8, 4, 2, 6 · 4 → 4, 6 · 9 → 9, 1 · 0, 1, 5, 6 never change. 🔢 Unit digit of 7⁹⁵: 95 mod 4 = 3 → **3**.
- 📌 Sums: 1 + … + n = n(n + 1)/2 · squares n(n + 1)(2n + 1)/6 · cubes [n(n + 1)/2]² · first n odd numbers = n².
- 📌 **Trailing zeros of n!** = ⌊n/5⌋ + ⌊n/25⌋ + ⌊n/125⌋ + … → 100! has **24**.
- AP: tₙ = a + (n − 1)d, Sₙ = n/2·(2a + (n − 1)d) · GP: tₙ = arⁿ⁻¹, Sₙ = a(rⁿ − 1)/(r − 1).
- Remainders: (a·b) mod n = [(a mod n)(b mod n)] mod n.

## 2. HCF & LCM
- 📌 **HCF × LCM = product** (for two numbers only) **[Src: RSA p.60]**.
- 📌 HCF of fractions = HCF(numerators)/LCM(denominators); LCM of fractions = LCM(numerators)/HCF(denominators).
- Largest number dividing x, y, z leaving the **same remainder** = HCF(\|x − y\|, \|y − z\|, \|z − x\|).
- Smallest number that leaves remainder r when divided by a, b, c = LCM(a, b, c) + r.
- Bells/lights tolling at intervals a, b, c next coincide after **LCM(a, b, c)**; "how many times in T" → ⌊T/LCM⌋ + 1 if counting the start **[Src: ME-Reasoning p.12]**.

## 3. Percentages, Profit & Loss
- 📌 x % of y = y % of x. Fraction table: ½ = 50 %, ⅓ = 33.33 %, ¼ = 25 %, ⅕ = 20 %, ⅙ = 16.67 %, ⅛ = 12.5 %, 1/9 = 11.11 %, 1/11 = 9.09 %, 1/12 = 8.33 % **[Src: RSA p.317]**.
- 📌 ⭐ **Successive change** a % then b %: net = **a + b + ab/100** (use negative signs for decreases). Up r % then down r % → net **−r²/100 %** (always a loss).
- 📌 Price rises r % → cut consumption by **r/(100 + r) × 100 %** to keep spending unchanged.
- 📌 Profit % = (SP − CP)/CP × 100 (on **cost** price unless told otherwise) · SP = CP × (100 + P %)/100 **[Src: RSA p.383]**.
- 📌 Discount is on **marked price**: SP = MP × (1 − d/100). Successive discounts a %, b % = single **a + b − ab/100** % **[Src: ME-Reasoning p.48]**.
- 📌 ⭐ **False weight:** gain % = error/(true value − error) × 100. 🔢 Uses 800 g for 1 kg → 200/800 × 100 = **25 %** **[Src: NA p.18]**.
- 📌 Two items sold at the same SP, one at x % gain and one at x % loss → overall **loss of x²/100 %**.

## 4. Simple & Compound Interest
- 📌 **SI = P·R·T/100** · **CI amount A = P(1 + R/100)ᵀ** **[Src: RSA p.650, 672]**.
- Half-yearly: rate R/2, periods 2T. Quarterly: R/4, 4T.
- 📌 ⭐ **CI − SI** on the same P: 2 years = **P(R/100)²** · 3 years = P(R/100)²·(3 + R/100).
- SI: money doubles in 100/R years; if it doubles in n years it **triples in 2n** (interest grows linearly) **[Src: NA p.25]**. CI: if it doubles in n years it becomes **4× in 2n**.
- 🔢 P = 10,000, R = 10 %, 2 years: SI = 2,000, CI = 2,100, difference = 10,000 × 0.01 = **100**.

## 5. Ratio, Proportion & Partnership
- a : b = c : d ⇒ ad = bc. Mean proportional of a and b = √(ab); third proportional = b²/a; fourth proportional to a, b, c = bc/a.
- 📌 **Partnership:** profit shares ∝ **capital × time** **[Src: RSA p.485]**.
- 🔢 Incomes 9 : 7, expenses 4 : 3, each saves 2,000 → 9x − 4y = 7x − 3y = 2000 → x = 2000, y = 4000 → incomes **18,000 and 14,000** **[Src: NA p.55]**.

## 6. Averages
- Average = sum/count. Consecutive numbers: average = (first + last)/2.
- New member replaces one and the average rises by d over n people → new value = old value + n·d.
- 📌 ⭐ **Average speed** over **equal distances** at x and y = **2xy/(x + y)** (not (x + y)/2) **[Src: RSA p.215]**.

## 7. Mixtures, Alligation & Ages
- 📌 **Alligation:** cheaper : dearer = **(d − m) : (m − c)**, where c, d are the two prices and m the mean price **[Src: RSA p.642]**.
- 📌 ⭐ **Repeated replacement:** from x litres, take out y and replace with water n times → pure liquid left = **x(1 − y/x)ⁿ**. 🔢 200 l, 20 l replaced 3 times → 200 × 0.9³ = **145.8 l** **[Src: NA p.40]**.
- Ages: write one equation per statement ("n years ago", "after n years") and solve; the difference between two people's ages never changes.

## 8. Time & Work, Pipes & Cisterns
- 📌 A alone a days, B alone b days → together **ab/(a + b)** days. Work per day = 1/a (efficiency) **[Src: RSA p.535]**.
- 📌 **M₁D₁H₁/W₁ = M₂D₂H₂/W₂** (men × days × hours ÷ work).
- Wages are shared in the ratio of **work done** (= efficiency × days).
- 🔢 A 12 days, B 16 days, working on **alternate days** starting with A: in 2 days 7/48 done; after 12 days 42/48; day 13 (A) adds 4/48 → 46/48; the remaining 2/48 takes B 2/3 of a day → **13⅔ days** **[Src: ME-Reasoning p.30]**.
- 📌 **Pipes:** filling pipe a hours, emptying pipe b hours → net rate 1/a − 1/b **[Src: RSA p.519]**.

## 9. Time, Speed & Distance
- 📌 **km/h → m/s: × 5/18**; m/s → km/h: × 18/5.
- 📌 Same distance: time ∝ 1/speed. Speed becomes (5/4)× → time becomes 4/5 → saves ⅕ of the usual time. 🔢 Reaches 6 min early at 5/4 the speed → usual time **30 min** **[Src: NA p.2]**.
- 📌 **Relative speed:** opposite directions S₁ + S₂, same direction \|S₁ − S₂\|.
- Two people start together from opposite ends and meet → distances ∝ speeds. 🔢 Meet at 600 km of a 1600 km route → speed ratio **3 : 5** **[Src: NA p.3]**.
- Average speed for equal distances: 2xy/(x + y) (§6).

## 10. Trains, Boats & Streams
- 📌 **Trains** **[Src: RSA p.621]**:
  - Pass a pole or a person: time = train length / speed.
  - Pass a platform or bridge: (train length + platform length) / speed.
  - Two trains, opposite directions: (L₁ + L₂)/(S₁ + S₂); same direction: (L₁ + L₂)/(S₁ − S₂).
  - ⭐ After meeting, the trains take a and b hours to reach their destinations → **speed ratio = √b : √a**. 🔢 9 h and 16 h → **4 : 3**.
- 📌 **Boats** **[Src: RSA p.609]:** downstream u + v, upstream u − v. **Boat speed u = (D + U)/2**, **stream speed v = (D − U)/2**.

## 11. Permutations & Combinations
- 📌 ⁿPᵣ = n!/(n − r)! · ⁿCᵣ = n!/(r!(n − r)!) · arrangements with repeats n!/(p!q!…) · circular (n − 1)! · necklace (n − 1)!/2 **[Src: RSA p.850]**.
- 📌 Diagonals of an n-gon = **n(n − 3)/2** · handshakes among n = ⁿC₂ · lines through n points (no 3 collinear) = ⁿC₂ · triangles = ⁿC₃.
- 🔢 Triangles from 21 points, of which 10 lie on one line and 11 on another (no other collinear sets): ²¹C₃ − ¹⁰C₃ − ¹¹C₃ = 1330 − 120 − 165 = **1045**. ⚠ ME-Reasoning p.78 gets the answer but writes a side step as "¹⁰C₂ × 11 = 445"; it is 45 × 11 = **495**.
- 🔢 Letters of LEVEL: 5!/(2!·2!) = **30**.
- Probability problems: see `09_Probability_and_Statistics.md` §1–3.

## 12. Clocks & Calendars
- 📌 ⭐ **Angle between the hands** at H:M = **\|30H − 5.5M\|** (take 360 − θ if > 180). 🔢 9:25 → \|270 − 137.5\| = **132.5°** **[Src: ME-Reasoning p.70]**.
- 📌 Hands **coincide 11 times in 12 hours (22 in a day)**, every 65 5⁄11 minutes. They are at right angles 22 times in 12 h (44/day) and opposite 11 times in 12 h (22/day).
  - ⚠ RS Aggarwal (p.832) states "in every hour both hands coincide once" — wrong: there is no coincidence between 11 and 1 except at 12, giving **11, not 12**, in 12 hours.
- Mirror image of a clock time = 11:60 − time (e.g. 3:20 → 8:40).
- 📌 **Calendars** **[Src: RSA p.828]:** odd days — ordinary year 1, leap year 2; 100 years → 5, 200 → 3, 300 → 1, 400 → 0. Leap year: divisible by 4, but a century year only if divisible by 400 (1900 no, 2000 yes). Day codes 0 = Sun … 6 = Sat.
- 🔢 1 Jan 2027 is a **Friday**, so 17 Jan 2027 (exam day) is a **Sunday**.

## 13. Mensuration (basic)
| Shape | Area / surface | Perimeter / volume |
|---|---|---|
| Rectangle l × b | lb | 2(l + b) |
| Triangle | ½·base·height; Heron √(s(s − a)(s − b)(s − c)) | a + b + c |
| Equilateral triangle a | (√3/4)a² | 3a |
| Circle r | πr² | 2πr |
| Sector angle θ | (θ/360)·πr² | arc (θ/360)·2πr |
| Cube a | 6a² | a³ |
| Cuboid | 2(lb + bh + hl) | lbh |
| Cylinder | curved 2πrh, total 2πr(r + h) | πr²h |
| Cone (slant l) | curved πrl, total πr(r + l) | ⅓πr²h |
| Sphere | 4πr² | (4/3)πr³ |
| Hemisphere | total 3πr² | (2/3)πr³ |

- Each side changes by x % → area changes by **2x + x²/100 %** (volume: 3x + 3x²/100 + x³/10⁴ %) **[Src: RSA p.697, 775]**.
- ⭐ **Painted cube** cut into n³ small cubes: 3 faces painted = 8 · 2 faces = 12(n − 2) · 1 face = 6(n − 2)² · none = (n − 2)³ **[Src: ME-Reasoning p.108]**.

## 14. Data Interpretation tactics
- Approximate first, compute last; read the units and the base year.
- % change = (new − old)/old × 100. Change in a **ratio** x/y when x rises a % and y rises b %: (a − b)/(100 + b) × 100 % **[Src: NA p.48]**.
- "Which year saw the highest % growth" ≠ "highest absolute growth" — check which one is asked.

---

# PART B — REASONING

## 15. Series, Analogy & Classification
- **Number series:** check differences (and differences of differences), ×/÷ patterns, squares/cubes ± k, primes, two interleaved series, ×n + n patterns.
- **Wrong-number series:** find the rule from most terms; if two numbers seem wrong, your rule is wrong. 🔢 10, 12, 28, 90, 368, **1840** — rule ×1+2, ×2+4, ×3+6, ×4+8, ×5+10 → the last term should be 368 × 5 + 10 = **1850**, so 1840 is the wrong number **[Src: NA p.108]**.
- 📌 **Letter positions:** A = 1 … Z = 26; reverse position = 27 − n; memory word **EJOTY** = 5, 10, 15, 20, 25.
- **Analogy:** find the relation in the first pair (n² − n, n³ + n, …). 🔢 42 : 56 :: 110 : 132 (6·7 : 7·8 :: 10·11 : 11·12) **[Src: NA p.115]**.
- **Odd one out:** classify by type, prime/composite, vowels, positions.

## 16. Coding–Decoding
- Letter shift (+k / −k), reverse alphabet (A ↔ Z, sum of positions 27), positional (−1, −2, −3, …), number coding (A = 1 …), symbol substitution, coded sentences (find common words).
- 🔢 DELHI → CCIDD: D − 1 = C, E − 2 = C, L − 3 = I, H − 4 = D, I − 5 = D **[Src: NA p.100]**.

## 17. Blood Relations
- Draw a family tree: + / − for gender, horizontal line for siblings/spouses, vertical for generations.
- Fixed phrases: "only son of my grandfather" (paternal) = **father** · "my mother's only daughter" = **me** (if female) · "brother's son" = nephew · "father's sister" = aunt.
- Coded relations (A + B = A is the father of B, …): decode one symbol at a time, write gender as you go **[Src: NA p.121]**.

## 18. Direction Sense
- North at the top; **right turn = 90° clockwise**, left = anticlockwise. Final distance by Pythagoras: √(Δx² + Δy²).
- Shadows: morning sun in the **east** → shadows fall **west**; evening → shadows east. At noon there is (almost) no shadow.
- 🔢 Walk 3 km N, 4 km E → **5 km** from start, towards the north-east.

## 19. Ranking, Seating & Puzzles
- 📌 **Ranking:** total = rank from top + rank from bottom − 1. Persons between A and B = total − (rankA + rankB) (when counted from opposite ends).
- **Linear seating:** if all face north, their right is your right; facing south, it flips. **Circular facing the centre:** right = anticlockwise.
- Puzzles: draw a grid (persons × attributes); place definite clues first, then the negative ones; use elimination.
- **Truth/lie puzzles:** assume each statement true in turn and check consistency **[Src: NA p.85]**.
- 📌 **Beam balance:** with w weighings you can find one heavier item among **3ʷ** → 100 balls need **5** (3⁴ = 81 < 100) **[Src: ME-Reasoning p.1]**.
- 📌 **Pigeonhole / worst case:** 10 blue + 12 grey socks → **3** to guarantee a matching pair, **14** to guarantee a blue pair (12 grey + 2 blue) **[Src: ME-Reasoning p.2]**.
- **Cubes & dice:** in a net, alternate squares in a straight row are **opposite faces**; two faces seen together on one die are never opposite **[Src: NA p.70]**.

## 20. Syllogisms
- Draw Venn circles for the **minimum** overlap the statements force; a conclusion is valid only if it holds in **every** possible diagram **[Src: ME-Reasoning p.92]**.

| Premises | Definite conclusion |
|---|---|
| All A are B + All B are C | All A are C (and Some C are A) |
| All A are B + Some C are A | Some C are B |
| All A are B + No B is C | No A is C |
| Some A are B + Some B are C | **No definite conclusion** (two particulars) |
| Two negative premises | **No definite conclusion** |

- **Possibility** questions: "Some A being C is a possibility" is true if nothing rules it out.
- **Either–or:** if neither "Some A are C" nor "No A is C" can be concluded, but one of them must be true, the answer is "either I or II follows".

## 21. Venn Diagrams, Statements & Data Sufficiency
- 📌 n(A ∪ B) = n(A) + n(B) − n(A ∩ B) · n(A ∪ B ∪ C) = Σn(A) − Σn(A ∩ B) + n(A ∩ B ∩ C).
- 📌 **Three sets:** at least two = exactly two + all three. 🔢 at least two = 50, exactly two = 40 → **all three = 10** **[Src: ME-Reasoning p.25]**.
- **Statement–assumption:** an assumption is something the author must take for granted (unstated). **Conclusion:** must follow from the statement alone. **Course of action:** practical, reduces the problem, and doesn't create a bigger one.
- **Data sufficiency** options: I alone / II alone / either alone / both together / neither — test each statement alone before combining.

---

# PART C — ENGLISH

## 22. Subject–Verb Agreement (the most-tested rule)
- Two subjects joined by **and** → plural (*Ram and Shyam are…*), unless they are one idea (*Bread and butter is…*; *The secretary and treasurer has* — one person).
- ⭐ **Each / every / either / neither / everyone / nobody** + singular verb. "**Many a** student **has**…" — singular.
- ⭐ **Either…or / neither…nor / not only…but also** → the verb agrees with the **nearer** subject.
- ⭐ **as well as, along with, together with, with, besides, in addition to, like** → the verb agrees with the **first** subject (*The captain, as well as the players, **is**…*) **[Src: English p.32]**.
- "**One of** the + plural noun" + singular verb; "one of those **who** + plural verb".
- "**The number of**… is" (singular) vs "**A number of**… are" (plural). "More than one" + singular noun + singular verb.
- ⭐ **Uncountable nouns** take singular verbs and no plural -s: information, advice, furniture, luggage, baggage, equipment, machinery, scenery, news, poetry, mischief.
- Collective nouns (team, jury, committee) — singular when acting as one unit, plural when members act separately.

## 23. Tenses, Conditionals & Fixed Pairs
- **Since** + point of time (*since 2020*), **for** + duration (*for two years*) — both with the perfect tense.
- Don't use *will* in time/condition clauses: *When he **comes**, I will tell him* (not *will come*).
- Conditionals: *If + present, will* · *If + past, would* · *If + had + V3, would have + V3*.
- ⭐ **Hardly / scarcely … when** · **no sooner … than** · (never "hardly … than"). With an inversion: *No sooner **had** he left than it rained*.
- "**It is high time** + past tense" (*It is high time we **left***). "**Wish** + past / past perfect". "**Lest** … should". "**Unless**" already means *if not* — don't add *not*.

## 24. Pronouns, Modifiers, Comparison & Qualifying Words
- After prepositions use object pronouns: *between you and **me***. *Each other* (two), *one another* (more than two). *One* → *one's*.
- Reflexive verbs need a pronoun: avail **oneself** of, absent oneself, pride oneself on.
- ⭐ **Parallelism:** *not only … but also*, *either … or* must join the same grammatical forms. **Dangling modifier:** *Walking in the park, **the trees** looked lovely* ✗ → *Walking in the park, **I** saw…* **[Src: English p.20]**.
- ⭐ **Comparison:** no double comparatives (*more better* ✗). *Superior/inferior/senior/junior/prefer* + **to**, not *than*. *Elder/eldest* for family and **never with "than"** — *older than* **[Src: VerbalAbility p.32 — ⚠ the notes show "elder than" as correct; it is not]**. "Than **any other** + singular noun".
- Sense verbs (look, seem, smell, taste, feel, sound) take **adjectives**: *The rose smells **sweet***.

| Qualifier | Use with | Example |
|---|---|---|
| much / little / less / amount | uncountable | much water, less sugar |
| many / few / fewer / number | countable | many books, fewer errors |
| a few / a little | some (positive) | a few friends helped |
| few / little | hardly any (negative) | few friends helped |
| the few / the little | all of the small amount | the few books I had |
| very | adjectives, present participles | very good, very interesting |
| much | past participles, comparatives | much obliged, much better |
| some | positive sentences, offers | some tea? |
| any | negatives, questions | not any money |
| each | two or more, individually | each of the two |
| every | three or more, as a group | every student |
| too … to | excess (negative result) | too tired to walk |
| enough | **after** the adjective | good enough |

- **Only** changes meaning by position: *Only I saw him* / *I only saw him* / *I saw only him*.
- **Question tags:** positive statement → negative tag; *I am…, **aren't I**?* · *Let's go, **shall we**?* · imperative → *will you?* · *Nobody came, did **they**?*
- **Voice:** object → subject + be + past participle (*is being done*, *has been done*, *can be done*); intransitive verbs have no passive.
- **Narration:** tense moves one step back (except universal truths), *said to* → *told*, now → then, today → that day, tomorrow → the next day, yesterday → the day before.

## 25. Articles
- **a / an by sound, not spelling:** an hour, an honest man, an MBA, an FIR · a university, a European, a one-rupee coin.
- **The:** unique things (the sun), superlatives and ordinals (the best, the first), rivers, seas, oceans, mountain ranges, deserts, groups of islands (the Ganga, the Himalayas, the Andamans), newspapers and holy books (the Hindu, the Gita), musical instruments (plays the guitar), "the + adjective" = a class (the poor), names with *of* (the Bay of Bengal).
- **No article:** single mountains and lakes (Mount Everest, Dal Lake), languages, subjects, meals in general, games (play cricket), abstract nouns in a general sense (Honesty is…), *go to school/church/bed* (for the purpose).

## 26. Prepositions
- **Time:** **at** + clock time, night, noon · **on** + days and dates · **in** + months, years, seasons, *the morning* · **by** = not later than · **till/until** = up to (continuing) · **since** (point) vs **for** (duration) · **during** + a period.
- **Place:** at (point), in (enclosed area), on (surface); **into** (movement inwards) vs **in** (position); **between** (two) vs **among** (more than two); **beside** (next to) vs **besides** (in addition to).
- **Fixed prepositions** (asked as fill-in-the-blank):

| Word + prep | Word + prep | Word + prep |
|---|---|---|
| accused **of** | charged **with** | abide **by** |
| afraid **of** | aim **at** | angry **with** a person / **at** a thing |
| agree **with** a person / **to** a proposal | ashamed **of** | averse **to** |
| capable **of** | comply **with** | confident **of** |
| congratulate **on** | consist **of** | deprived **of** |
| die **of** a disease / **from** a cause | different **from** | divide **into** |
| good **at** | independent **of** | insist **on** |
| interested **in** | married **to** | prefer A **to** B |
| prevent **from** | refrain **from** | senior / junior **to** |
| superior / inferior **to** | sympathy **with** (agreement) / **for** (pity) | according **to** |

## 27. ⭐ Idioms & Phrases (40 most asked)
| Idiom | Meaning | Idiom | Meaning |
|---|---|---|---|
| A bolt from the blue | sudden shock | Achilles' heel | weak point |
| Add fuel to the fire | make worse | Apple of one's eye | very dear |
| At sixes and sevens | in confusion | At the eleventh hour | at the last moment |
| Beat about the bush | avoid the point | Bell the cat | take a risky lead |
| Bite the dust | be defeated / die | Blow one's own trumpet | boast |
| Break the ice | start a conversation | Burn the midnight oil | work late |
| Bury the hatchet | make peace | By hook or by crook | by any means |
| Call a spade a spade | speak frankly | Cock-and-bull story | absurd made-up story |
| Cold feet | last-minute nervousness | Cry over spilt milk | regret the past uselessly |
| Cut corners | do cheaply/carelessly | ⭐ Fair-weather friend | friend only in good times |
| Hand in glove | in close collusion | Head over heels | completely (in love) |
| Hit the nail on the head | be exactly right | In hot water | in trouble |
| In the nick of time | just in time | Kill two birds with one stone | two gains, one effort |
| Let the cat out of the bag | reveal a secret | Lion's share | largest part |
| Make both ends meet | live within income | Nip in the bud | stop at the start |
| Off the cuff | without preparation | Once in a blue moon | very rarely |
| Pull someone's leg | tease | Put the cart before the horse | reverse the order |
| Red-letter day | memorable day | Show the white feather | act cowardly |
| Smell a rat | suspect something | A storm in a teacup | fuss over nothing |
| Take with a pinch of salt | doubt | Turn a deaf ear | ignore |
| Under the weather | unwell | White elephant | costly but useless |
| Wild-goose chase | futile search | Spill the beans | reveal a secret |

- ⚠ VerbalAbility p.10 glosses *fair-weather friend* as "good friend" — it means the **opposite** (a friend who leaves in hard times).

## 28. Commonly Confused Words
| Pair | Difference |
|---|---|
| accept / except | receive / excluding |
| advice / advise | noun / verb |
| affect / effect | verb (influence) / noun (result) |
| allusion / illusion | indirect reference / false belief |
| beside / besides | next to / in addition |
| complement / compliment | completes / praise |
| council / counsel | body of people / advice |
| credible / credulous | believable / easily fooled |
| desert / dessert | dry land / sweet dish |
| discreet / discrete | tactful / separate |
| elicit / illicit | draw out / illegal |
| eminent / imminent | distinguished / about to happen |
| emigrate / immigrate | leave a country / enter one |
| ensure / insure | make certain / buy insurance |
| farther / further | physical distance / additional |
| formally / formerly | officially / previously |
| judicial / judicious | of courts / wise |
| lose / loose | misplace / not tight |
| personal / personnel | private / staff |
| principal / principle | head, main / rule |
| stationary / stationery | not moving / writing material |
| continual / continuous | repeated with breaks / unbroken |
| economic / economical | of the economy / thrifty |
| loath / loathe | unwilling / hate |
| respectful / respective | showing respect / individual |

## 29. One-word Substitutes, Synonyms & Antonyms
- One-word: *autobiography* (one's own life story) · *bibliophile* (book lover) · *omnipotent / omniscient / omnipresent* (all-powerful / all-knowing / everywhere) · *misanthrope* (hater of mankind) · *philanthropist* (lover of mankind, donor) · *polyglot* (speaks many languages) · *panacea* (cure for all ills) · *posthumous* (after death) · *infallible* (cannot err) · *inevitable* (cannot be avoided) · *ambidextrous* (uses both hands) · *atheist* (doesn't believe in God) · *anarchy* (absence of government) · *autocracy* (rule by one) · *plagiarism* (copying another's work) · *epitaph* (words on a tomb) · *euthanasia* (painless killing of the incurably ill) · *incorrigible* (cannot be corrected) · *inaudible* (cannot be heard).
- Use roots: bene- (good), mal- (bad), -phile (lover), -phobia (fear), omni- (all), poly- (many), mis- (hatred / wrong), -cide (killing), -cracy (rule).
- ⚠ VerbalAbility p.52 gives *latent* as an antonym of *hidden* — they are **synonyms** (latent = present but hidden). The same notes (p.45) list *suggest* among verbs used without *to*; correct usage is *suggest that he go* / *suggest going*, never *suggest him to go*.

## 30. Ordering Words & Sentences; Comprehension
- **Word ordering:** Subject → Verb → Object → Place → Time; adverbs of frequency before the main verb (*He **always** comes*).
- **Para-jumbles:**
  1. Find the **opening** sentence: it introduces the topic and needs no earlier context (no *he/this/however* referring back).
  2. Lock **mandatory pairs**: noun → pronoun; idea → example (*for instance*); contrast words (*however, but*); time sequence (*first … then … finally*).
  3. The **closing** sentence sums up or concludes (*thus, therefore*).
  4. Eliminate options using one locked pair instead of testing every order.
- **Reading comprehension:** read the questions first, then the passage; separate **stated** facts from **inferences**; reject options with extreme words (*always, never, only*) unless the passage uses them; "main idea" answers cover the whole passage, not one paragraph; tone questions — look at the adjectives.
- **Spotting errors — check in this order:** subject–verb agreement → tense → pronoun → preposition → article → comparison/parallelism → idiom/usage. "No error" is a legitimate answer — don't force an error that isn't there.

---

## Last-day revision sheet
| Item | Formula / rule |
|---|---|
| Number of factors | (a + 1)(b + 1)(c + 1) |
| Trailing zeros in n! | ⌊n/5⌋ + ⌊n/25⌋ + … |
| HCF × LCM | product of the two numbers |
| Successive % change | a + b + ab/100 |
| Up r % then down r % | −r²/100 % |
| Successive discounts | a + b − ab/100 % |
| False weight gain | error/(true − error) × 100 |
| Same SP, x % gain & x % loss | loss x²/100 % |
| SI / CI | PRT/100 / P(1 + R/100)ᵀ |
| CI − SI (2 years) | P(R/100)² |
| Partnership | capital × time |
| Alligation | (d − m) : (m − c) |
| Replacement | x(1 − y/x)ⁿ |
| Work together | ab/(a + b) |
| M₁D₁H₁/W₁ | = M₂D₂H₂/W₂ |
| km/h → m/s | × 5/18 |
| Average speed, equal distances | 2xy/(x + y) |
| Trains crossing | (L₁ + L₂)/(relative speed) |
| Trains after meeting (a, b h) | speed ratio √b : √a |
| Boat / stream | (D + U)/2 / (D − U)/2 |
| Diagonals of n-gon | n(n − 3)/2 |
| Circular arrangements | (n − 1)! |
| Clock angle | \|30H − 5.5M\| |
| Hands coincide | 11 times / 12 h; every 65 5⁄11 min |
| Odd days | year 1, leap 2, 100 y 5, 400 y 0 |
| Area change for x % sides | 2x + x²/100 % |
| Ranking | total = top + bottom − 1 |
| Beam balance | 3ʷ items with w weighings |
| Painted cube (n) | 8 · 12(n − 2) · 6(n − 2)² · (n − 2)³ |
| Three-set Venn | at least two = exactly two + all three |

**One-liners**
1. ⭐ Each/every/many a + singular verb.
2. ⭐ Either…or / neither…nor: verb agrees with the nearer subject.
3. ⭐ As well as / along with / together with: verb agrees with the first subject.
4. The number of + singular; a number of + plural.
5. Information, advice, furniture, luggage, equipment, news: never plural.
6. Hardly/scarcely … when; no sooner … than.
7. Superior/senior/prefer + to, never than.
8. Elder is never followed by than — use older than.
9. a/an go by sound: an hour, a university, an MBA.
10. The + rivers, oceans, mountain ranges; no article for single mountains and lakes.
11. Since + point of time; for + duration.
12. Between two, among many; beside = next to, besides = in addition.
13. Sense verbs take adjectives: smells sweet.
14. Much + past participle / comparative; very + adjective.
15. Few = hardly any; a few = some.
16. Fair-weather friend = deserts you in hard times.
17. Latent = hidden (synonym).
18. Para-jumble: opening has no back-reference; lock noun → pronoun pairs.
19. RC: avoid extreme options unless the passage is extreme.
20. ⭐ Up r % then down r % is always a loss.
21. Average speed over equal distances is the harmonic mean, not the arithmetic mean.
22. CI − SI for two years = P(R/100)².
23. SI doubling in n years ⇒ triples in 2n; CI doubling in n ⇒ quadruples in 2n.
24. Clock hands coincide 22 times a day, not 24.
25. 1900 was not a leap year; 2000 was.
26. Two particular or two negative premises → no definite conclusion.
27. Right turn = clockwise; morning shadows point west.
28. Pigeonhole: think of the worst case first.
29. 17 Jan 2027 is a Sunday.
30. Paper-I needs 27.5 / 50 on its own — don't sacrifice this hour for Paper-II.

## Dropped as outside TPSC syllabus
- VerbalAbility pp. 64–100 (engineering mechanics), Engineering-Maths topics (they belong to file 09 or are out of scope).
- Advanced quant beyond state-PSC level in RS Aggarwal (logarithms, surds and indices drills, heights and distances, stocks and shares, true discount, banker's discount) — skim only if time remains.
- GATE-specific general-aptitude tricks with no state-PSC equivalent (e.g. exponential growth curve sketching).
- GK and current affairs → `05_Notes/Paper1_English_Reasoning_GK.md` Part C.

> ⚠ **Note on this file:** the reviewer agent stalled before writing, so this file was completed by the main session from that agent's saved review notes (all five PDFs reviewed, ~105 scan pages viewed) plus standard grammar and quant references. Every worked answer was re-derived by hand.
