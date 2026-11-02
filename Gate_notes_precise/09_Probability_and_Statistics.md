# 09 · Probability & Statistics — Precise Notes
> **TPSC ATO (IT) Paper-II §1** · ~7 marks (estimate) · Syllabus: *"Probability and Statistics — random variables; uniform, normal, exponential, Poisson and binomial distributions; mean, median, mode and standard deviation; conditional probability and Bayes theorem"*
> Drawn from: Made Easy Engineering-Maths handwritten notes (its probability chapter only), RS Aggarwal (probability chapter), Made Easy reasoning notes. Refs like **[Src: EM p.17]** point into `_source_pdfs/09_Engineering_Maths/`; **[Src: RSA p.859]** into `_source_pdfs/10_General_Ability/`.
> This is the **only** Engineering-Mathematics section in the TPSC syllabus — linear algebra, calculus and discrete maths are out. Deeper explanations: `05_Notes/Week_09_Communication_and_Probability.md` Part B.

## Which notes are worth your time
| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 09_Engineering_Maths/1.Engineering_Maths_Hand_Written_Notes_Made_Easy.pdf | Made Easy (Wiki Engineering scan) | Handwritten scan | 132 (probability = pp. 4–37) | 2.5 | Basic probability, conditional probability, Bayes trees, random variables, E/Var rules, joint tables, binomial, hypergeometric, Poisson, skewness · **no uniform, normal, exponential or descriptive statistics** at all; several mistakes (corrected below); pp. 38–132 are discrete maths / linear algebra / calculus — out of scope |
| 10_General_Ability/1.Quantitative_Aptitude…R_S_Aggarwal.pdf | R. S. Aggarwal | Typed textbook | 961 (probability ≈ p. 859) | 4 | Coins/dice/cards probability drills at Paper-I level · no distributions |
| 10_General_Ability/3.Reasoning_and_Aptitude_Made_Easy… | Made Easy | Handwritten | 133 | 3.5 | A few probability puzzles, mean/SD shift rules (p. 108) |

**Only one weak source exists for this section, so most of this file is standard textbook material (Ross / Walpole level).** Sections built mainly from own knowledge are marked "(added — not in sources)". For a second explanation use `05_Notes/Week_09` Part B rather than any PDF.

## Topic map
| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | Basic probability & rules | ⭐⭐⭐ | Dice/cards/coins; "at least one"; mutually exclusive vs independent |
| 2 | Counting for probability | ⭐⭐ | Committees, arrangements, with/without replacement |
| 3 | Conditional probability & Bayes | ⭐⭐⭐ | Two-bag/urn, test-accuracy, defective-machine problems |
| 4 | Random variables, E & Var | ⭐⭐ | E(aX + b), Var(aX + b), find k so ΣP = 1 |
| 5 | The five named distributions | ⭐⭐⭐ | Mean/variance of each; Poisson approximation; memorylessness; normal % rule |
| 6 | Mean, median, mode, SD | ⭐⭐⭐ | Compute from data; effect of adding/multiplying; empirical relation |
| 7 | Correlation & regression | ⭐ | Range of r; meaning of sign |

---

## 1. Basic Probability
- **Sample space S** = all outcomes; **event** = subset of S. Classical probability: **P(E) = n(E)/n(S)** (finite, equally likely outcomes). Relative-frequency definition = long-run proportion **[Src: EM p.6]**.
- 📌 **Axioms:** 0 ≤ P(E) ≤ 1 · P(S) = 1 · P(A ∪ B) = P(A) + P(B) for disjoint A, B.
- 📌 **Rules:** P(A′) = 1 − P(A) · **P(A ∪ B) = P(A) + P(B) − P(A ∩ B)** · P(A ∪ B ∪ C) = ΣP(A) − ΣP(A ∩ B) + P(A ∩ B ∩ C) · De Morgan: P(A′ ∩ B′) = 1 − P(A ∪ B), P(A′ ∪ B′) = 1 − P(A ∩ B) **[Src: EM p.12]**.
- 📌 **"At least one" = 1 − P(none).** 🔢 At least one six in 4 rolls = 1 − (5/6)⁴ = 671/1296 ≈ **0.518**.

| | Mutually exclusive | Independent |
|---|---|---|
| Definition | A ∩ B = ∅ → **P(A ∩ B) = 0** | **P(A ∩ B) = P(A)·P(B)** |
| Union | P(A) + P(B) | P(A) + P(B) − P(A)P(B) |
| Can both hold? | ⚠ **No** (if P(A), P(B) > 0): disjoint events are *dependent* — knowing A happened tells you B didn't | |

- ⚠ EM p.8 writes "P(A ∩ B) = ∅" for mutually exclusive events — correct is **P(A ∩ B) = 0** (∅ is a set, not a number).
- **Exhaustive** events: A ∪ B = S. Mutually exclusive + exhaustive ⇒ P(B) = 1 − P(A).
- Pairwise independence of A, B, C does **not** imply mutual independence (also need P(A ∩ B ∩ C) = P(A)P(B)P(C)).
- Standard numbers: a deck has 52 cards, 4 suits × 13, 12 face cards (J, Q, K), 4 aces, 26 red. Two dice: 36 outcomes; P(sum = 7) = 6/36 = **1/6** (the most likely sum).

## 2. Counting for Probability
- 📌 ⁿPᵣ = n!/(n − r)! (ordered) · ⁿCᵣ = n!/(r!(n − r)!) (unordered) · ⁿCᵣ = ⁿCₙ₋ᵣ.
- Arrangements with repeats: n!/(p!·q!·…) · circular: (n − 1)! · necklace (flip allowed): (n − 1)!/2.
- With vs without replacement: 🔢 two aces from a deck — without replacement (4/52)(3/51) = 1/221; with replacement (4/52)² = 1/169 **[Src: EM p.12]**.
- 🔢 Arrange BIRD so it starts with D: 3!/4! = **1/4** **[Src: EM p.6]**.
- Committee: 🔢 2 men from 5 and 1 woman from 4 → ⁵C₂·⁴C₁ = 40 ways.
- Hypergeometric (drawing without replacement): P(X = x) = ʳCₓ·⁽ᴺ⁻ʳ⁾C₍ₙ₋ₓ₎ / ᴺCₙ; mean = n·r/N **[Src: EM p.33–34]**.

## 3. Conditional Probability & Bayes' Theorem
- 📌 **P(A \| B) = P(A ∩ B) / P(B)**, P(B) > 0 → multiplication rule **P(A ∩ B) = P(B)·P(A \| B)**.
- Independence ⇔ P(A \| B) = P(A).
- 📌 **Total probability:** if B₁ … Bₙ partition S, **P(E) = Σ P(Bᵢ)·P(E \| Bᵢ)**.
- 📌 ⭐ **Bayes:** **P(Bᵢ \| E) = P(Bᵢ)·P(E \| Bᵢ) / Σⱼ P(Bⱼ)·P(E \| Bⱼ)** — "prior × likelihood ÷ total". Posteriors sum to 1. Draw a tree: first branch = cause (bag, machine, disease), second = observed effect **[Src: EM p.15–19]**.

🔢 **Two bags** (EM p.17): Bag 1 has 5 black + 3 green, Bag 2 has 2 black + 4 green; pick a bag at random, draw one ball.
P(green) = ½·(3/8) + ½·(4/6) = 9/48 + 16/48 = **25/48**. P(Bag 1 \| green) = (3/16) ÷ (25/48) = **9/25**.

🔢 **Medical test** (classic): prevalence 1 %, sensitivity 99 %, false-positive rate 5 %.
P(+) = 0.01·0.99 + 0.99·0.05 = 0.0099 + 0.0495 = 0.0594 → P(disease \| +) = 0.0099/0.0594 = **1/6 ≈ 16.7 %** — low, because the disease is rare.

🔢 **Factories:** A makes 60 % of bulbs (2 % defective), B makes 40 % (3 % defective). P(defective) = 0.012 + 0.012 = 0.024; P(from B \| defective) = 0.012/0.024 = **½**.

🎯 **How it's asked:** urn/bag Bayes, test-reliability Bayes, "probability it came from machine X" — near-certain one question.

## 4. Random Variables, Expectation & Variance
| | Discrete | Continuous |
|---|---|---|
| Described by | PMF p(x) = P(X = x) | PDF f(x) |
| Must satisfy | p(x) ≥ 0, Σ p(x) = 1 | f(x) ≥ 0, ∫ f(x) dx = 1 |
| Probability of a single value | can be > 0 | ⚠ **P(X = a) = 0** — only intervals have probability |
| Probability of an interval | Σ over the values | area under f |
| CDF F(x) = P(X ≤ x) | step function | continuous, F′(x) = f(x) |

- CDF is non-decreasing, F(−∞) = 0, F(∞) = 1, P(a < X ≤ b) = F(b) − F(a).
- 🔢 Two-dice sum: P(sum = s) = (6 − \|s − 7\|)/36. "Find k so the PMF sums to 1": set Σ k·g(x) = 1 **[Src: EM p.20]**.
- 📌 **E(X) = Σ x·p(x)** (or ∫ x f(x) dx) · **Var(X) = E(X²) − [E(X)]²** · SD σ = √Var.
- 📌 **Linear rules:** E(aX + b) = a·E(X) + b · **Var(aX + b) = a²·Var(X)** · **σ(aX + b) = \|a\|·σ** · E(X + Y) = E(X) + E(Y) always.
  - ⚠ EM p.23 writes σ(aX + b) = aσ — correct is **\|a\|σ** (SD is never negative). Adding a constant b changes the mean, **not** the spread.
- 📌 Var(aX + bY) = a²Var(X) + b²Var(Y) + 2ab·Cov(X, Y); if X, Y independent, Cov = 0 and E(XY) = E(X)E(Y). Cov(X, Y) = E(XY) − E(X)E(Y); Cov(X, X) = Var(X).
- 🔢 E(X) = 50, Var(X) = 100 → E(3X + 5) = **155**, Var(3X + 5) = **900**, σ = **30** **[Src: EM p.23]**.
- 🔢 Fair die: E(X) = 3.5, E(X²) = 91/6, Var = 91/6 − 12.25 = **35/12**.
- 🔢 Expected number of tosses: first head = **2** (1/p); two heads (not necessarily consecutive) = **4** (2/p); two consecutive heads = **6**.
  - ⚠ EM p.21–22 concludes "on average 1.5 tosses to get 2 heads" — impossible (you need at least 2 tosses); the source summed the series wrongly.
- **Chebyshev:** P(\|X − μ\| < kσ) ≥ 1 − 1/k² for any distribution. 🔢 μ = 56, σ = 10, interval 36–76 → k = 2 → P ≥ **3/4** **[Src: EM p.21]**.

## 5. ⭐⭐⭐ The Five Named Distributions
| Distribution | PMF / PDF | Mean | Variance | Use when |
|---|---|---|---|---|
| **Binomial** B(n, p) | ⁿCₓ pˣ (1 − p)ⁿ⁻ˣ, x = 0 … n | **np** | **np(1 − p)** | fixed n independent trials, two outcomes, constant p |
| **Poisson** (λ) | e^(−λ) λˣ / x!, x = 0, 1, 2, … | **λ** | **λ** | count of rare events in a fixed interval |
| **Uniform** U(a, b) | 1/(b − a) on [a, b] | **(a + b)/2** | **(b − a)²/12** | every value in a range equally likely |
| **Exponential** (λ) | λe^(−λx), x ≥ 0 | **1/λ** | **1/λ²** | waiting time between Poisson events, lifetimes |
| **Normal** N(μ, σ²) | (1/(σ√(2π))) e^(−(x − μ)²/(2σ²)) | **μ** | **σ²** | sums/averages of many effects; measurements |

*(Uniform, exponential and normal are missing from the EM source — added — not in sources.)*

### 5.1 Binomial
- Conditions: fixed n, independent trials, two outcomes, same p each trial **[Src: EM p.29–31]**.
- 🔢 10 dice, X = number of sixes: E = 10/6 ≈ 1.67, σ = √(50/36) = 5√2/6; P(X ≥ 2) = 1 − P(0) − P(1) = 1 − (5/6)¹⁰ − 10(1/6)(5/6)⁹.
- 🔢 Mean 50, variance 25 → q = 25/50 = ½, p = ½, **n = 100** **[Src: EM p.31]**.
- **Shape:** symmetric only if p = ½; p < ½ → **positively (right) skewed**; p > ½ → negatively skewed. ⚠ EM p.31 calls "number of sixes" symmetric — wrong (p = 1/6 → right-skewed); the notes self-correct on p.32.
- Mode ≈ ⌊(n + 1)p⌋. Variance ≤ mean always (q ≤ 1).

### 5.2 Poisson
- 📌 **Mean = variance = λ** (the tell-tale property). λ = rate × time **[Src: EM p.34–36]**.
- ⭐ **Poisson approximation to binomial:** n large, p small → λ = np. 🔢 10,000 tractors, defect rate 1/2000 → λ = 5; P(X = 2) = e⁻⁵·5²/2! ≈ **0.084**.
- 🔢 40 arrivals/hour, half-hour window → λ = 20; P(at least one) = 1 − P(X = 0) = 1 − e⁻²⁰. ⚠ EM p.35 labels this "1 − P(X = 1)" — the correct complement is **P(X = 0)**.
- Sum of independent Poissons is Poisson with λ₁ + λ₂.

### 5.3 Uniform (added — not in sources)
- 🔢 U(2, 8): mean 5, variance 36/12 = **3**; P(3 < X < 5) = 2/6 = **⅓**.
- Discrete uniform on 1 … n: mean (n + 1)/2, variance (n² − 1)/12 (die: 3.5 and 35/12).

### 5.4 Exponential (added — not in sources)
- 📌 P(X > t) = **e^(−λt)**, CDF 1 − e^(−λt). Median = (ln 2)/λ < mean.
- ⭐ **Memoryless:** P(X > s + t \| X > s) = P(X > t) — the only continuous memoryless distribution (geometric is the discrete one).
- 🔢 Mean life 10 h → λ = 0.1; P(lasts > 10 h) = e⁻¹ ≈ **0.368**; P(lasts 10 more hours, given it has run 5) = e⁻¹ as well.

### 5.5 Normal (added — not in sources)
- Bell-shaped, symmetric about μ; **mean = median = mode**; total area 1; inflection points at μ ± σ.
- 📌 **Standardise:** Z = (X − μ)/σ ~ N(0, 1). P(Z ≤ 0) = 0.5.
- 📌 ⭐ **68–95–99.7 rule:** within μ ± σ ≈ 68.3 %, μ ± 2σ ≈ 95.4 %, μ ± 3σ ≈ 99.7 %.
- 🔢 μ = 60, σ = 10: P(50 < X < 70) ≈ **68 %**; P(X > 80) ≈ (1 − 0.954)/2 ≈ **2.3 %**.
- Normal approximation to binomial when np ≥ 5 and n(1 − p) ≥ 5 (μ = np, σ² = npq). ⚠ EM p.37 says "when n and p are both large" — imprecise; the condition is n large with p not too close to 0 or 1.
- Sum of independent normals is normal; Central Limit Theorem: means of large samples are ≈ normal whatever the original distribution.

🎯 **How it's asked:** "mean = variance" ⇒ Poisson; memoryless ⇒ exponential; mean/variance of U(a, b); n and p from binomial mean & variance; % of data within 1σ/2σ.

## 6. Mean, Median, Mode & Standard Deviation (added — not in sources)
### 6.1 Central tendency
| Measure | Raw data | Grouped data | Notes |
|---|---|---|---|
| **Mean** x̄ | Σx / n | Σfx / Σf (class midpoints) | uses every value; affected by outliers |
| **Median** | middle value of sorted data; even n → average of the two middle | L + ((N/2 − cf)/f)·h | robust to outliers |
| **Mode** | most frequent value | L + ((f₁ − f₀)/(2f₁ − f₀ − f₂))·h | can be multiple or none |

(L = lower boundary of the median/modal class, cf = cumulative frequency before it, f = its frequency, f₀/f₂ = frequencies of the classes before/after, h = class width.)

- 📌 ⭐ **Empirical relation** (moderately skewed data): **Mode ≈ 3·Median − 2·Mean**.
- 📌 **Skewness:** positive (right) skew → **mean > median > mode**; negative skew → mode > median > mean; symmetric → all equal **[Src: EM p.32–33]**. 🔢 Mean 60, median 50, mode 40 → positively skewed.
- 📌 Combined mean = (n₁x̄₁ + n₂x̄₂)/(n₁ + n₂). 🔢 20 students averaging 50 and 30 averaging 60 → **56**.
- AM ≥ GM ≥ HM (equal only when all values are equal); for two numbers GM² = AM·HM.

### 6.2 Dispersion
- Range = max − min · IQR = Q₃ − Q₁ · mean deviation = Σ\|x − x̄\|/n.
- 📌 **Variance σ² = Σ(x − x̄)²/n = (Σx²/n) − x̄²** · SD σ = √σ². Sample variance divides by **n − 1** (unbiased).
- 📌 **Coefficient of variation CV = (σ / x̄) × 100 %** — compares spread across data sets with different units/means (lower CV = more consistent).
- 🔢 Data 2, 3, 3, 5, 7, 10: mean 5, median (3 + 5)/2 = 4, mode 3; Σ(x − 5)² = 46 → σ² = 46/6 ≈ 7.67, σ ≈ 2.77 (sample variance 46/5 = 9.2).

### 6.3 ⭐ Effect of changing every value
| Operation on each value | Mean, median, mode | SD, range | Variance |
|---|---|---|---|
| Add constant c | + c | unchanged | unchanged |
| Multiply by k | × k | × \|k\| | × k² |
| y = a·x + b | a·x̄ + b | \|a\|·σ | a²σ² |

**[Src: ME-Reasoning p.108]**

## 7. Correlation & Regression (awareness)
- Pearson r = Cov(X, Y)/(σₓσᵧ), **−1 ≤ r ≤ 1**. r = +1 / −1: perfect positive / negative **linear** relation; r = 0: no linear relation (there may still be a non-linear one).
- ⚠ EM p.27 says "r close to −1 means least dependent" — wrong: \|r\| ≈ 1 means **strongest** linear dependence; r ≈ 0 means weakest. Covariance alone is scale-dependent; use r to judge strength.
- Regression line of y on x passes through (x̄, ȳ); slope b_yx = r·σᵧ/σₓ; r² = b_yx·b_xy.

---

## Last-day revision sheet
| Item | Formula / value |
|---|---|
| Union | P(A ∪ B) = P(A) + P(B) − P(A ∩ B) |
| At least one | 1 − P(none) |
| Independent | P(A ∩ B) = P(A)P(B) |
| Mutually exclusive | P(A ∩ B) = 0 (⇒ dependent if both possible) |
| Conditional | P(A \| B) = P(A ∩ B)/P(B) |
| Total probability | P(E) = Σ P(Bᵢ)P(E \| Bᵢ) |
| Bayes | P(Bᵢ \| E) = P(Bᵢ)P(E \| Bᵢ) / P(E) |
| Variance | E(X²) − [E(X)]² |
| E(aX + b) / Var(aX + b) | aE(X) + b / a²Var(X) |
| Binomial | mean np, variance npq |
| Poisson | mean = variance = λ; λ = np |
| Uniform (a, b) | mean (a + b)/2, variance (b − a)²/12 |
| Exponential | mean 1/λ, variance 1/λ², P(X > t) = e^(−λt) |
| Normal | Z = (X − μ)/σ; 68 / 95 / 99.7 % |
| Die | mean 3.5, variance 35/12 |
| Empirical | Mode ≈ 3 Median − 2 Mean |
| CV | σ/x̄ × 100 % |
| Grouped median | L + ((N/2 − cf)/f)·h |
| Grouped mode | L + ((f₁ − f₀)/(2f₁ − f₀ − f₂))·h |
| Chebyshev | P(\|X − μ\| < kσ) ≥ 1 − 1/k² |
| Correlation | −1 ≤ r ≤ 1 |

**One-liners**
1. ⭐ Mutually exclusive ≠ independent; with non-zero probabilities they can't be both.
2. Probability of an exact value of a continuous variable is 0.
3. ⭐ Bayes = prior × likelihood ÷ total; posteriors sum to 1.
4. Most likely sum of two dice is 7 (probability 1/6).
5. "At least one" problems: use the complement.
6. Adding a constant shifts the mean but leaves SD and variance unchanged.
7. Multiplying by k multiplies SD by \|k\| and variance by k².
8. ⭐ Poisson: mean = variance; binomial: variance < mean.
9. Poisson approximates binomial when n is large and p is small (λ = np).
10. Binomial is symmetric only when p = ½.
11. ⭐ Exponential is memoryless.
12. Exponential mean = 1/λ, so a larger rate means shorter waits.
13. Normal: mean = median = mode; symmetric; area within ±1σ ≈ 68 %.
14. Uniform variance (b − a)²/12.
15. Positive skew: mean > median > mode.
16. Median is robust to outliers; mean is not.
17. Sample variance divides by n − 1.
18. Lower CV = more consistent data.
19. AM ≥ GM ≥ HM.
20. r = 0 means no **linear** relation only.
21. Expected tosses for the first head = 2; for two heads = 4.
22. Sum of independent Poisson (or normal) variables stays Poisson (normal).
23. E(X + Y) = E(X) + E(Y) always; Var adds only when independent (or uncorrelated).
24. Without replacement → hypergeometric; with replacement → binomial.
25. Total area under any PDF = 1; Σ of any PMF = 1.

## Dropped as outside TPSC syllabus
- From the EM source (pp. 38–132): recurrence relations, combinatorics beyond basic counting, graph theory, set theory, logic, linear algebra, numerical methods, calculus — all outside this exam.
- Joint-distribution tables and conditional expectation (EM p.25–28) — kept only Cov/independence rules.
- Hypothesis testing, sampling distributions, moment-generating functions — not named in the syllabus.

> ⚠ **Note on this file:** the reviewer agent stalled before writing, so this file was completed by the main session from that agent's saved review notes on the Engineering-Maths scan plus standard textbook material. Every worked answer was re-derived by hand.
