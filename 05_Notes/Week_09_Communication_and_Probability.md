# Week 9 — Analog & Digital Communication + Probability & Statistics

**Syllabus §4:** Autocorrelation and PSD, white noise, filtering of random signals through LTI systems, AM and FM, superheterodyne receivers, circuits for analog communications, information theory, entropy, mutual information and channel capacity theorem, digital communications, PCM, DPCM, digital modulation schemes (ASK/PSK/FSK), QAM, MAP and ML decoding, matched filter receiver, calculation of bandwidth/SNR/BER, fundamentals of error correction, Hamming codes, timing and frequency synchronization, ISI and its mitigation, basics of TDMA/FDMA/CDMA.
**Syllabus §1:** Random variables. Uniform, normal, exponential, Poisson and binomial distributions. Mean, median, mode and standard deviation. Conditional probability and Bayes theorem.

**Estimated marks: ~8 + ~7 = ~15**

> ⭐ **Strategy.** Section 4 is an **ECE** section sitting inside a CS paper. Most candidates skip it and donate ~8 marks. Do **not** attempt to derive anything — learn the **formula sheet and the definitions**. That alone converts the great majority of these questions, because they are asked at a definitional/plug-in level.
>
> ⭐ Section 1 is the **entire** Engineering Mathematics content of this syllabus. Linear algebra and calculus are **not examinable**.

---

# PART A — ANALOG & DIGITAL COMMUNICATION

## 1. Random signals and noise

### 1.1 Autocorrelation and PSD

📌 **Autocorrelation** R_X(τ) = E[X(t)·X(t+τ)] — how similar a signal is to a time-shifted version of itself.

**Properties:**
- 📌 **R_X(0) = E[X²] = average power** (the maximum value)
- R_X(τ) = R_X(−τ) — **even function**
- |R_X(τ)| ≤ R_X(0)

📌 ⭐ **Power Spectral Density (PSD) S_X(f) is the Fourier transform of the autocorrelation** — this is the **Wiener–Khinchin theorem**.
📌 Total power = ∫ S_X(f) df = R_X(0)

### 1.2 ⭐ White noise
📌 ⭐ **White noise has a PSD that is CONSTANT (flat) over all frequencies**, S(f) = N₀/2.
📌 Its autocorrelation is an **impulse**: R(τ) = (N₀/2)·δ(τ) — samples at distinct times are uncorrelated.

⚠ "White" refers to the **flat spectrum** (by analogy with white light), not to the amplitude distribution. **AWGN** = Additive **White Gaussian** Noise — white (spectrum) *and* Gaussian (distribution) are two independent properties.
⚠ R(0) is **infinite** for ideal white noise (infinite power) — it is a mathematical idealisation. Band-limited white noise is the practical model.

**Thermal (Johnson) noise:** 📌 **N = kTB** where k = 1.38×10⁻²³ J/K.

### 1.3 Filtering random signals through LTI systems
📌 ⭐ **S_Y(f) = |H(f)|² · S_X(f)** — the output PSD is the input PSD scaled by the **squared magnitude** of the transfer function.
📌 Output power = ∫ |H(f)|² S_X(f) df
📌 Mean: μ_Y = μ_X · H(0)

⚠ Note the **squared** magnitude — the most common error here is using |H(f)| instead of |H(f)|².

**Noise figure** F = (input SNR)/(output SNR) ≥ 1. **Friis formula** for cascaded stages: F = F₁ + (F₂−1)/G₁ + … — the first stage dominates.

---

## 2. ⭐ Amplitude modulation

📌 **AM signal:** s(t) = A_c[1 + μ·m(t)]·cos(2πf_c t)
📌 ⭐ **Modulation index μ = A_m / A_c**, also μ = (A_max − A_min)/(A_max + A_min)

| Scheme | ⭐ Bandwidth | Carrier | Power efficiency |
|---|---|---|---|
| ⭐ **AM (DSB-FC)** | ⭐ **2f_m** | Present | Poor (carrier wastes power) |
| ⭐ **DSB-SC** | ⭐ **2f_m** | Suppressed | Better |
| ⭐ **SSB** | ⭐ **f_m** | Suppressed | ⭐ **Best** — half the bandwidth |
| **VSB** | Between f_m and 2f_m | Partial | Used in analog TV video |

### 2.1 ⭐ AM power relations

📌 ⭐ **P_total = P_c (1 + μ²/2)**
📌 **Sideband power P_SB = P_c · μ²/2** (split equally between the two sidebands)
📌 ⭐ **Efficiency η = μ² / (2 + μ²)**

🔢 At **μ = 1** (100% modulation): P_total = 1.5 P_c; sideband power = 0.5 P_c.
⭐ **Fraction of power in the sidebands = 0.5/1.5 = 33.3%**; efficiency = 1/3.
⭐ **Two-thirds of an AM transmitter's power is in the carrier, which carries no information** — this is precisely why DSB-SC and SSB exist.

⚠ **μ > 1 causes overmodulation** → envelope distortion and phase reversal; the envelope detector fails.

### 2.2 Detection
- **Envelope detector:** simple diode + RC; works only for AM with μ ≤ 1. Requires RC time constant: 1/f_c ≪ RC ≪ 1/f_m.
- **Coherent (synchronous) detection:** needed for DSB-SC and SSB; requires a locally generated carrier synchronised in frequency and phase.

### 2.3 ⭐ Superheterodyne receiver

**Block diagram:** RF amplifier → **Mixer** (with **Local Oscillator**) → **IF amplifier** → Detector → AF amplifier → Speaker

📌 ⭐ **Standard IF for AM broadcast = 455 kHz**; for FM broadcast = **10.7 MHz**.
📌 **f_LO = f_signal + f_IF** (high-side injection)
📌 ⭐ **Image frequency f_image = f_signal + 2·f_IF**

🔢 Signal at 1000 kHz, IF = 455 kHz → f_LO = 1455 kHz → **image = 1000 + 910 = 1910 kHz**.

⭐ **Why heterodyne?** Converting every station to a **fixed IF** lets one highly selective, fixed-tuned IF amplifier do the filtering, giving uniform selectivity and gain across the band.
⭐ **Image rejection** is done by the RF stage *before* mixing — the IF stage cannot remove an image, because after mixing it is indistinguishable from the wanted signal.

---

## 3. ⭐ Angle modulation (FM and PM)

📌 **FM:** the instantaneous **frequency** varies with the message. **PM:** the **phase** varies.
📌 ⭐ **Frequency deviation Δf = k_f · A_m**
📌 ⭐ **FM modulation index β = Δf / f_m**
📌 **PM modulation index β_PM = k_p · A_m** (independent of f_m)

📌 ⭐⭐ **Carson's rule: BW = 2(Δf + f_m) = 2·f_m·(β + 1)**

🔢 Δf = 75 kHz, f_m = 15 kHz (FM broadcast) → BW = 2(75 + 15) = **180 kHz** (allocated 200 kHz).

| | **Narrowband FM (β ≪ 1)** | **Wideband FM (β ≫ 1)** |
|---|---|---|
| Bandwidth | ≈ 2f_m (like AM) | ≈ 2Δf |
| Noise performance | Modest | Excellent |

⭐ **FM vs AM:**

| | AM | ⭐ **FM** |
|---|---|---|
| Noise immunity | Poor | ⭐ **Excellent** (amplitude limiting removes amplitude noise) |
| Bandwidth | 2f_m (narrow) | Much wider |
| Transmitted power | Varies with modulation | ⭐ **Constant** |
| Circuit complexity | Simple | Complex |

📌 **FM has a constant total transmitted power** regardless of modulation — modulation redistributes power among sidebands (Bessel function amplitudes) but does not change the total.
**Pre-emphasis / de-emphasis** improves FM's high-frequency SNR.

---

## 4. ⭐ Information theory

📌 ⭐ **Self-information I(x) = log₂(1/p) = −log₂ p** bits
📌 ⭐ **Entropy H(X) = −Σ pᵢ log₂ pᵢ** bits/symbol — the average information per symbol

**Properties:**
- 📌 ⭐ **H is maximum when all symbols are equally likely**, giving **H_max = log₂ M** for M symbols.
- H = 0 when one symbol has probability 1 (no uncertainty).
- 0 ≤ H(X) ≤ log₂ M.

🔢 Binary source with p = 0.5 each → H = **1 bit/symbol** (maximum).
🔢 Source with p = {0.5, 0.25, 0.125, 0.125} → H = 0.5(1) + 0.25(2) + 0.125(3) + 0.125(3) = **1.75 bits/symbol**.

📌 **Joint entropy** H(X,Y) · **Conditional entropy** H(Y|X)
📌 ⭐ **Mutual information I(X;Y) = H(X) − H(X|Y) = H(Y) − H(Y|X) = H(X) + H(Y) − H(X,Y)**
- I(X;Y) ≥ 0; I(X;Y) = 0 iff X and Y are independent.
- **Channel capacity C = max I(X;Y)** over input distributions.

📌 ⭐⭐ **Shannon–Hartley theorem: C = B log₂(1 + S/N)** bits/second
📌 **Nyquist (noiseless): C = 2B log₂ L** bps

🔢 B = 3000 Hz, S/N = 3 → C = 3000 log₂4 = **6000 bps**
🔢 B = 4000 Hz, S/N = 255 → C = 4000 log₂256 = 4000 × 8 = **32,000 bps**

⭐ **Source coding theorem:** the minimum average codeword length ≥ H(X). **Code efficiency = H(X)/L̄.**
**Source codes:** Shannon–Fano, ⭐ **Huffman** (optimal prefix-free code), Lempel–Ziv (universal).
📌 **Kraft's inequality** for a prefix code: Σ 2^(−lᵢ) ≤ 1.

---

## 5. ⭐ Digital communication

### 5.1 ⭐ Sampling and quantisation

📌 ⭐ **Sampling theorem: f_s ≥ 2·f_m** (the **Nyquist rate**). Below this → **aliasing**.
📌 **Nyquist interval = 1/(2f_m)**

📌 ⭐ **Number of bits per sample: n = log₂ L** for L quantisation levels
🔢 L = 256 → n = **8 bits/sample**

📌 ⭐ **Bit rate = f_s × n** bits/second
🔢 Speech: f_m = 4 kHz → f_s = 8 kHz; 8 bits/sample → 64 kbps (standard PCM voice channel).

📌 **Quantisation step size Δ = (V_max − V_min)/L = 2V/2ⁿ**
📌 **Quantisation noise power = Δ²/12**
📌 ⭐⭐ **SNR of a uniform quantiser (dB) = 6.02n + 1.76**

🔢 n = 8 → SNR ≈ 6.02(8) + 1.76 = **49.9 dB**.
⭐ **Each extra bit improves SNR by about 6 dB.**

**Non-uniform quantisation / companding:** **μ-law** (North America/Japan, μ = 255) and **A-law** (Europe/India, A = 87.6) compress the signal before uniform quantisation, improving SNR for low-amplitude signals.

### 5.2 ⭐ PCM, DPCM, DM

| Technique | Idea | Bit rate |
|---|---|---|
| ⭐ **PCM** | Sample → quantise → encode each sample independently | Highest |
| ⭐ **DPCM** | Encode the **difference** from a **predicted** value → fewer bits (exploits correlation) | Lower |
| **ADPCM** | DPCM with an adaptive predictor/quantiser | Lower still |
| ⭐ **Delta Modulation (DM)** | 1-bit DPCM — transmit only whether the signal rose or fell | ⭐ **1 bit/sample** |
| **ADM** | Adaptive step size | |

⭐ **Delta modulation's two errors:**
- ⭐ **Slope overload distortion** — the step size is too small to track a fast-changing signal. 📌 Avoided when **Δ·f_s ≥ max|dm/dt|**.
- ⭐ **Granular (hunting) noise** — the step size is too large for a slowly varying signal, causing oscillation about the true value.
⚠ These pull in opposite directions, which is why **adaptive** delta modulation exists.

**Line coding:** NRZ · RZ · **Manchester** (self-clocking, transition mid-bit) · Differential Manchester · AMI · bipolar.

### 5.3 ⭐ Digital modulation schemes

| Scheme | What varies | Bandwidth efficiency | Noise performance |
|---|---|---|---|
| ⭐ **ASK** | Amplitude | Low | ⭐ **Worst** (amplitude is noise-sensitive) |
| ⭐ **FSK** | Frequency | Lowest (needs most BW) | Better than ASK |
| ⭐ **PSK (BPSK)** | Phase | Good | ⭐ **Best of the binary schemes** |
| **QPSK** | Phase, 4 levels | 2 bits/symbol | Same BER as BPSK at same E_b/N₀ |
| ⭐ **QAM** | ⭐ **Amplitude AND phase** | ⭐ **Highest** | Needs higher SNR |

📌 **Bit rate = symbol (baud) rate × log₂M**
🔢 16-QAM at 2400 baud → 2400 × log₂16 = 2400 × 4 = **9600 bps**.
🔢 QPSK: 2 bits/symbol; 8-PSK: 3 bits/symbol; 64-QAM: 6 bits/symbol.

📌 **Bandwidth (raised cosine, roll-off α): BW = (1 + α) × symbol rate**
📌 **ASK/PSK bandwidth ≈ 2 × bit rate / log₂M**; **FSK bandwidth ≈ 2Δf + 2f_b**

📌 **BER for coherent BPSK: P_e = Q(√(2E_b/N₀))**
📌 **BER for coherent BFSK: P_e = Q(√(E_b/N₀))** — needs 3 dB more power than BPSK for the same BER.
⭐ **BER decreases as E_b/N₀ increases.** Higher-order modulation (more bits/symbol) requires **higher SNR** for the same BER — the fundamental bandwidth/power trade-off.

### 5.4 ⭐ Optimum reception

⭐ **Matched filter:** the receiver filter whose impulse response is the time-reversed, delayed transmitted pulse, h(t) = s(T−t).
📌 ⭐ **It MAXIMISES the output SNR at the sampling instant in AWGN.**
📌 Maximum output SNR = **2E/N₀**.
⚠ The matched filter maximises SNR — it does **not** minimise distortion or ISI.
**Correlator receiver** is an equivalent implementation.

⭐ **MAP vs ML decoding:**

| | ⭐ **ML (Maximum Likelihood)** | ⭐ **MAP (Maximum A Posteriori)** |
|---|---|---|
| Maximises | P(received \| sent) | P(sent \| received) |
| Uses prior probabilities | ❌ No | ⭐ **✅ Yes** |
| Optimal when | Priors are equal/unknown | Priors are known |
| Minimises | — | ⭐ **Probability of error (overall optimal)** |

⭐ **MAP reduces to ML when all symbols are equally likely.** MAP is the optimum decision rule in general.

### 5.5 ⭐ ISI and synchronization

⭐ **Inter-Symbol Interference (ISI):** pulse spreading (from band-limiting or multipath) causes each symbol to smear into its neighbours.

⭐ **Mitigation:**
1. ⭐ **Nyquist criterion for zero ISI** — the pulse must be zero at all other sampling instants. Minimum bandwidth = R_s/2 (ideal sinc, impractical).
2. ⭐ **Raised-cosine pulse shaping** — 📌 BW = (1+α)·R_s/2, with roll-off 0 ≤ α ≤ 1; α = 0 is the ideal minimum, α = 1 doubles the bandwidth but is far easier to implement.
3. ⭐ **Equalisation** at the receiver — zero-forcing, MMSE, adaptive (LMS), decision-feedback.
4. **Eye diagram** — the visual diagnostic: a **wide open eye** means low ISI and good noise margin; eye closure indicates ISI and jitter.

**Synchronization:**
- **Timing (symbol/clock) synchronization** — sampling at the correct instant (early-late gate, Gardner).
- **Frequency and carrier-phase synchronization** — PLL, Costas loop, squaring loop.
- **Frame synchronization** — preambles/sync words.
⚠ Coherent detection needs carrier phase recovery; **non-coherent** detection avoids it at a ~1–3 dB SNR penalty.

### 5.6 ⭐ Error correction

**Channel coding theorem:** reliable communication is possible for any rate R < C.

| Code | Type |
|---|---|
| Parity check | Detects odd errors only |
| ⭐ **Hamming code** | ⭐ **Single-error correcting, double-error detecting (SECDED with extra parity)** |
| Cyclic (CRC) | Powerful detection |
| BCH, Reed–Solomon | Multiple/burst error correction (CDs, DVDs, QR codes) |
| Convolutional | Continuous; decoded with the **Viterbi algorithm** (an ML decoder) |
| Turbo, LDPC | Near-Shannon-limit performance |

📌 ⭐ **Hamming code: 2ʳ ≥ m + r + 1** (m data bits, r parity bits)
🔢 m = 4 → r = 3, the **(7,4) Hamming code** · m = 11 → r = 4, the (15,11) code

📌 **Code rate = k/n** · **Block code (n,k)** adds n−k redundant bits.
📌 **Hamming distance:** detect d errors needs d_min ≥ d+1; correct d errors needs **d_min ≥ 2d+1**.
📌 The (7,4) Hamming code has **d_min = 3** → corrects 1 error, detects 2.

⭐ **Syndrome decoding:** the syndrome is the pattern of failed parity checks; interpreted as a binary number it gives the **position of the erroneous bit** directly.

### 5.7 ⭐ Multiple access

| Technique | Separation | Note |
|---|---|---|
| ⭐ **FDMA** | ⭐ **Frequency band** per user, all the time | Needs guard bands; analog-friendly |
| ⭐ **TDMA** | ⭐ **Time slot** per user, full bandwidth | Needs guard times and synchronization; GSM |
| ⭐ **CDMA** | ⭐ **Orthogonal spreading code**; ⭐ **all users share the FULL bandwidth ALL the time** | Spread spectrum; soft capacity; needs power control (near-far problem) |
| SDMA | Spatial separation (beamforming) | |
| OFDMA | Orthogonal subcarriers | 4G/5G |

⭐ **CDMA basis:** each user's data is multiplied by a unique **orthogonal (Walsh) code**; the receiver correlates with that code to recover the data while other users appear as noise. **Spread spectrum** forms: DSSS and FHSS. 📌 **Processing gain = chip rate / bit rate**.

---

# PART B — PROBABILITY & STATISTICS

## 6. ⭐ Basic probability

📌 0 ≤ P(A) ≤ 1 · P(S) = 1 · P(A') = 1 − P(A)
📌 ⭐ **Addition rule: P(A ∪ B) = P(A) + P(B) − P(A ∩ B)**
📌 **Mutually exclusive** (disjoint): P(A ∩ B) = 0 ⇒ P(A ∪ B) = P(A) + P(B)
📌 ⭐ **Multiplication rule: P(A ∩ B) = P(A)·P(B|A)**
📌 ⭐ **Independence: P(A ∩ B) = P(A)·P(B)**, equivalently P(A|B) = P(A)

⚠ ⭐ **Independent ≠ mutually exclusive.** In fact, for events of non-zero probability, mutually exclusive events are **dependent** (knowing one occurred tells you the other did not).

📌 ⭐ **Conditional probability: P(A|B) = P(A ∩ B) / P(B)**, for P(B) > 0
📌 **Total probability: P(A) = Σ P(A|Bᵢ)·P(Bᵢ)** over a partition {Bᵢ}

### 6.1 ⭐⭐ Bayes' theorem

📌 ⭐ **P(Bᵢ | A) = [ P(A|Bᵢ) · P(Bᵢ) ] / Σⱼ P(A|Bⱼ) · P(Bⱼ)**

*(posterior = likelihood × prior / evidence)*

🔢 **Worked example.** Machine A makes 60% of items with a 2% defect rate; machine B makes 40% with a 5% defect rate. An item is found defective — what is P(it came from A)?

P(A|D) = (0.02 × 0.6) / (0.02 × 0.6 + 0.05 × 0.4) = 0.012 / (0.012 + 0.020) = 0.012/0.032 = ⭐ **0.375**

🔢 **Medical test example.** Disease prevalence 1%; test sensitivity 99%; false positive rate 5%. Given a positive test:
P(D|+) = (0.99 × 0.01)/(0.99 × 0.01 + 0.05 × 0.99) = 0.0099/(0.0099 + 0.0495) = 0.0099/0.0594 ≈ **16.7%**
⭐ The counter-intuitively low answer (base-rate neglect) is exactly why this example is popular.

**Method:** always build the denominator as the **sum over all ways the evidence can occur**.

### 6.2 Counting
📌 **Permutations** ⁿPᵣ = n!/(n−r)! (order matters) · **Combinations** ⁿCᵣ = n!/(r!(n−r)!) (order does not)
📌 ⁿCᵣ = ⁿC₍ₙ₋ᵣ₎ · Σᵣ ⁿCᵣ = 2ⁿ

🔢 3 red and 2 blue balls; draw 2 **without** replacement — P(both red) = (3/5)(2/4) = 6/20 = **3/10**.
⚠ **With** replacement it would be (3/5)² = **9/25**. Always check which the question states.

---

## 7. ⭐ Random variables

📌 **Discrete RV:** PMF p(x) with Σp(x) = 1
📌 **Continuous RV:** PDF f(x) with ∫f(x)dx = 1; P(X = a) = **0** for any single point
📌 **CDF F(x) = P(X ≤ x)** — non-decreasing, F(−∞)=0, F(+∞)=1; f(x) = dF/dx

### 7.1 ⭐ Expectation and variance

📌 **E[X] = Σ x·p(x)** or **∫ x·f(x) dx**
📌 ⭐ **Var(X) = E[X²] − (E[X])²**
📌 ⭐ **σ = √Var(X)** — the standard deviation

**Properties:**
📌 ⭐ **E[aX + b] = a·E[X] + b**
📌 ⭐ **Var(aX + b) = a²·Var(X)** *(adding a constant does not change the variance)*
📌 ⭐ **E[X + Y] = E[X] + E[Y]** — **linearity of expectation, always true, even for dependent variables**
📌 **Var(X + Y) = Var(X) + Var(Y)** — ⭐ **only if X and Y are independent**

⚠ Linearity of expectation needs no independence; **additivity of variance does.**

---

## 8. ⭐⭐ The five named distributions

**These five — and only these five — are named in the syllabus. Memorise the table.**

| Distribution | Type | PMF/PDF | ⭐ Mean | ⭐ Variance | When it applies |
|---|---|---|---|---|---|
| ⭐ **Bernoulli** | Discrete | p, 1−p | **p** | **p(1−p)** | A single trial |
| ⭐ **Binomial** B(n,p) | Discrete | ⁿCₓ pˣ(1−p)ⁿ⁻ˣ | ⭐ **np** | ⭐ **np(1−p)** | Number of successes in **n independent trials** |
| ⭐ **Poisson** P(λ) | Discrete | e^(−λ)λˣ/x! | ⭐ **λ** | ⭐ **λ** | Rare events in a fixed interval |
| ⭐ **Uniform** U(a,b) | Continuous | 1/(b−a) | ⭐ **(a+b)/2** | ⭐ **(b−a)²/12** | All values equally likely |
| ⭐ **Exponential** Exp(λ) | Continuous | λe^(−λx), x ≥ 0 | ⭐ **1/λ** | ⭐ **1/λ²** | **Waiting time** between Poisson events |
| ⭐ **Normal** N(μ,σ²) | Continuous | (1/σ√2π)e^(−(x−μ)²/2σ²) | ⭐ **μ** | ⭐ **σ²** | Sums of many effects (CLT) |

### 8.1 Key properties ⭐

⭐ **Poisson: mean = variance = λ.** This is its signature and a very common one-mark question.
⭐ **Poisson approximates the Binomial** when n is large and p small, with **λ = np**.
⭐ **Exponential is memoryless:** P(X > s+t | X > s) = P(X > t). *(The geometric distribution is its discrete counterpart — the only two memoryless distributions.)*
⭐ **Binomial variance np(1−p) is always less than its mean np.**

⭐ **Normal distribution:**
- Symmetric, bell-shaped; ⭐ **mean = median = mode**.
- 📌 **Standard normal Z = (X − μ)/σ**, with μ = 0, σ = 1.
- ⭐ **The empirical (68–95–99.7) rule:**

📌 ⭐ **~68% within 1σ · ~95% within 2σ · ~99.7% within 3σ**

- ⭐ **Central Limit Theorem:** the sum (or mean) of a large number of independent random variables tends to a normal distribution **regardless of the original distribution**.

🔢 Binomial with n = 100, p = 0.3 → mean = 30, variance = 100(0.3)(0.7) = 21, σ = √21 ≈ 4.58.
🔢 Poisson with λ = 4 → P(X = 2) = e⁻⁴·4²/2! = e⁻⁴ × 8 ≈ **0.1465**.
🔢 Exponential with λ = 0.5/hour → mean waiting time = 1/0.5 = **2 hours**.

---

## 9. ⭐ Descriptive statistics

### 9.1 Measures of central tendency

📌 ⭐ **Mean** = Σx/n — uses every value; ⭐ **sensitive to outliers**
📌 ⭐ **Median** = the middle value of sorted data (average of the two middle values if n is even); ⭐ **robust to outliers**
📌 ⭐ **Mode** = the most frequent value; a data set may be unimodal, bimodal or have no mode

🔢 Data 2, 3, 3, 5, 7 → mean = 20/5 = **4**; median = **3**; mode = **3**.
🔢 Data 1, 2, 3, 4, 100 → mean = 22, median = 3. ⭐ The median is the better summary when outliers are present.

📌 **Empirical relation (moderately skewed data): Mode ≈ 3·Median − 2·Mean**
📌 Symmetric distribution: mean = median = mode.
📌 **Positively (right) skewed:** mean > median > mode. **Negatively (left) skewed:** mean < median < mode.

### 9.2 Measures of dispersion

📌 **Range** = max − min
📌 ⭐ **Variance σ² = Σ(xᵢ − μ)²/N** (population) or **Σ(xᵢ − x̄)²/(n−1)** (sample — note the **n−1**, Bessel's correction)
📌 ⭐ **Standard deviation σ = √variance** — same units as the data
📌 **Coefficient of variation = σ/μ × 100%** — for comparing dispersions of different scales
📌 **Quartiles, IQR = Q3 − Q1**

🔢 Data 2, 4, 4, 4, 5, 5, 7, 9: mean = 40/8 = 5.
Deviations: −3,−1,−1,−1,0,0,2,4 → squares 9,1,1,1,0,0,4,16 = 32. Population variance = 32/8 = **4**; **σ = 2**.

⭐ **Adding a constant to every value:** mean shifts, ⭐ **variance and SD unchanged**.
⭐ **Multiplying every value by k:** mean × k, variance × k², **SD × |k|**.

**Correlation and regression (awareness):** correlation coefficient r ∈ [−1, 1]; r = 0 means no *linear* relationship. ⚠ **Correlation does not imply causation.**

---

## 10. Rapid-fire facts ⭐

### Communication

| Fact | Value |
|---|---|
| White noise PSD | Flat/constant |
| Output PSD through LTI | \|H(f)\|²·S_X(f) |
| PSD is FT of | Autocorrelation (Wiener–Khinchin) |
| AM bandwidth | 2f_m |
| DSB-SC / SSB bandwidth | 2f_m / f_m |
| AM total power | P_c(1 + μ²/2) |
| Sideband power at μ=1 | 33.3% |
| AM efficiency | μ²/(2+μ²) |
| Carson's rule | 2(Δf + f_m) |
| FM modulation index | Δf/f_m |
| AM IF / FM IF | 455 kHz / 10.7 MHz |
| Image frequency | f_s + 2f_IF |
| Entropy | −Σp log₂p |
| Max entropy | log₂M (equally likely) |
| Shannon capacity | B log₂(1+S/N) |
| Nyquist rate | 2f_m |
| Bits per sample | log₂L |
| PCM SNR (dB) | 6.02n + 1.76 |
| DM errors | Slope overload, granular noise |
| Best binary digital modulation | PSK |
| Most bandwidth-efficient | QAM |
| Bit rate | Baud rate × log₂M |
| Matched filter | Maximises output SNR |
| MAP vs ML | MAP uses priors; equal when priors equal |
| Zero-ISI pulse | Raised cosine, BW = (1+α)R_s/2 |
| ISI diagnostic | Eye diagram |
| Hamming parity bits | 2ʳ ≥ m+r+1 |
| (7,4) Hamming d_min | 3 |
| CDMA | Full bandwidth, orthogonal codes |

### Probability

| Fact | Value |
|---|---|
| P(A∪B) | P(A)+P(B)−P(A∩B) |
| Independence | P(A∩B) = P(A)P(B) |
| Bayes | P(A\|B)P(B)/ΣP(A\|Bⱼ)P(Bⱼ) |
| Var(X) | E[X²] − (E[X])² |
| Var(aX+b) | a²Var(X) |
| E[X+Y] | E[X]+E[Y] always |
| Var(X+Y) | Sum only if independent |
| Binomial mean/variance | np / np(1−p) |
| Poisson mean/variance | λ / λ |
| Exponential mean/variance | 1/λ / 1/λ² |
| Uniform mean/variance | (a+b)/2 / (b−a)²/12 |
| Normal empirical rule | 68 / 95 / 99.7 |
| Memoryless distributions | Exponential, geometric |
| Normal: mean, median, mode | All equal |
| Mode ≈ | 3·Median − 2·Mean |
| Robust to outliers | Median |

---

## 11. Common traps ⚠

1. **"White" refers to the flat spectrum**, not Gaussianity.
2. **Output PSD uses |H(f)|², not |H(f)|.**
3. **DSB-SC bandwidth is still 2f_m** — only SSB halves it.
4. **Carson's rule is 2(Δf + f_m)**, not 2Δf.
5. **Image frequency = f_s + 2f_IF**, and it must be rejected **before** the mixer.
6. **PCM SNR = 6.02n + 1.76 dB** — roughly 6 dB per bit.
7. **Slope overload (step too small) vs granular noise (step too large)** — opposite causes.
8. **Matched filter maximises SNR; it does not remove ISI.**
9. **MAP uses priors, ML does not.**
10. **Correct d errors needs 2d+1**, detect needs d+1.
11. ⭐ **Poisson: mean = variance** (not λ²).
12. ⭐ **Independent ≠ mutually exclusive.**
13. **Var(aX+b) = a²Var(X)** — the constant b vanishes, and a is **squared**.
14. **Variance additivity requires independence; expectation linearity does not.**
15. **With vs without replacement** changes the answer — read the question.
16. **Sample variance divides by n−1**, population variance by N.

---

## 12. Practice

- GATE: [`Paper2_S01_Probability_and_Statistics/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S01_Probability_and_Statistics/) — **125 questions**
- State-PSC level: [`Paper2_S01_Probability_and_Statistics/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S01_Probability_and_Statistics/) — 50 questions
- Communication: [`Paper2_S04_Analog_and_Digital_Communication/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S04_Analog_and_Digital_Communication/) — 46 questions (DSP + information theory). ⚠ **No GATE CSE coverage exists for this section.**
- Test: [`Week_09_Test.md`](../04_Mock_Tests/Week_09_Test.md)

**Priority order if short on time:**
**Communication** — the formula sheet (AM/FM bandwidth and power, Carson, Shannon, Nyquist, PCM SNR, Hamming bound) → digital modulation comparison → entropy → matched filter/MAP-ML definitions → multiple access. **Do not attempt derivations.**
**Probability** — ⭐ **Bayes' theorem** (asked almost every time) → the five-distribution mean/variance table → mean/median/mode/SD → expectation and variance properties.
