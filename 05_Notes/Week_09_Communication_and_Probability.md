# Week 9 — Analog & Digital Communication + Probability & Statistics

**Syllabus §4:** Autocorrelation and PSD, white noise, filtering of random signals through LTI systems, AM and FM, superheterodyne receivers, circuits for analog communications, information theory, entropy, mutual information and channel capacity theorem, digital communications, PCM, DPCM, digital modulation schemes (ASK/PSK/FSK), QAM, MAP and ML decoding, matched filter receiver, calculation of bandwidth/SNR/BER, fundamentals of error correction, Hamming codes, timing and frequency synchronization, ISI and its mitigation, basics of TDMA/FDMA/CDMA.
**Syllabus §1:** Random variables. Uniform, normal, exponential, Poisson and binomial distributions. Mean, median, mode and standard deviation. Conditional probability and Bayes theorem.

**Estimated marks: ~8 + ~7 = ~15**

---

## 💡 How to approach this week

**Part A (Communication) is an ELECTRONICS section sitting inside a computer-science paper.** Most CS candidates skip it and simply donate ~8 marks.

⭐ **Do not derive anything.** The questions are asked at a **definitional and plug-in-the-formula** level, not at a derivation level. Learn the concepts in plain language, memorise the formula sheet, and you will convert the great majority of these marks for a fraction of the effort other sections demand.

**Part B (Probability) is the ENTIRE Engineering Mathematics content of this syllabus.** Linear algebra and calculus are **not examinable** — Annexure-C lists exactly one mathematics section, "Probability and Statistics". So this is a small, closed, highly learnable syllabus. ⭐ **Bayes' theorem and the five-distribution table alone cover most of what is asked.**

---

# PART A — ANALOG & DIGITAL COMMUNICATION

## 💡 What a communication system does

You want to send information (speech, video, data) from A to B over a physical medium. Three problems arise immediately:

1. **The message is at the wrong frequency.** Speech occupies 0–4 kHz. You cannot radiate 4 kHz efficiently (the antenna would need to be kilometres long), and every speaker would occupy the same band. ⭐ **Solution: MODULATION** — shift the message onto a high-frequency carrier.
2. **Noise corrupts the signal.** ⭐ **Solution:** noise-resistant modulation (FM), optimum receivers (matched filters), and error-correcting codes.
3. **The channel has finite capacity.** ⭐ **Solution:** understand the limit (Shannon) and code efficiently (Huffman, PCM).

The file follows exactly that order.

---

## 1. Random signals and noise

### 1.1 💡 Autocorrelation and power spectral density

**Autocorrelation** answers: *"how similar is this signal to a time-shifted copy of itself?"*

📌 **R_X(τ) = E[X(t) · X(t + τ)]**

💡 A slowly varying signal stays similar to itself for a long shift, so its autocorrelation decays slowly. A rapidly fluctuating signal decorrelates almost immediately.

**Properties:**
📌 ⭐ **R_X(0) = E[X²] = the AVERAGE POWER of the signal** — and this is its **maximum** value
📌 R_X(τ) = R_X(−τ) — it is an **even** function
📌 |R_X(τ)| ≤ R_X(0)

**Power Spectral Density (PSD)** answers: *"how is the signal's power distributed across frequency?"*

📌 ⭐⭐ **The PSD is the FOURIER TRANSFORM of the autocorrelation.** This is the **Wiener–Khinchin theorem** — the single most important link between the time and frequency descriptions of a random signal.

📌 **Total power = ∫ S_X(f) df = R_X(0)** — both descriptions must agree on the power.

### 1.2 ⭐⭐ White noise

📌 ⭐ **White noise has a POWER SPECTRAL DENSITY that is CONSTANT (FLAT) over all frequencies:** S(f) = N₀/2.

💡 **Why "white":** by analogy with white light, which contains all visible frequencies in equal measure.

📌 ⭐ **Its autocorrelation is an IMPULSE:** R(τ) = (N₀/2)·δ(τ).
💡 **What that means physically:** samples taken at any two *distinct* instants are **completely uncorrelated**. Knowing the noise now tells you nothing about the noise a moment later.

⚠⚠ ⭐ **"White" describes the SPECTRUM, not the amplitude distribution.**
**AWGN** = Additive **White** **Gaussian** Noise — and *white* (flat spectrum) and *Gaussian* (bell-curve amplitudes) are two **independent** properties. A signal can be white but not Gaussian, or Gaussian but not white.

⚠ Ideal white noise has **infinite** total power (a flat spectrum over infinite bandwidth), so R(0) = ∞. It is a mathematical **idealisation**; the practical model is **band-limited** white noise.

📌 **Thermal (Johnson) noise power: N = kTB**, where k = 1.38 × 10⁻²³ J/K, T is temperature in kelvin, B is bandwidth.

### 1.3 ⭐ Filtering a random signal through an LTI system

📌 ⭐⭐ **S_Y(f) = |H(f)|² · S_X(f)**

💡 **In words:** the output PSD is the input PSD multiplied by the **SQUARED MAGNITUDE** of the filter's transfer function.

💡 **Why squared:** PSD is a *power* quantity. A filter scales *amplitude* by |H(f)|, and power goes as amplitude squared.

⚠ ⭐ **The most common error here is using |H(f)| instead of |H(f)|².**

📌 Output power = ∫ |H(f)|² S_X(f) df
📌 Output mean: μ_Y = μ_X · H(0)

🔢 White noise of PSD N₀/2 passed through an ideal low-pass filter of bandwidth B and gain 1:
Output power = (N₀/2) × 2B = **N₀B** (integrating over −B to +B).

**Noise figure** F = (input SNR)/(output SNR) ≥ 1 — how much a stage degrades the SNR.
**Friis formula** for cascaded stages: F = F₁ + (F₂−1)/G₁ + (F₃−1)/(G₁G₂) + … ⭐ **The FIRST stage dominates**, which is why the low-noise amplifier comes first in every receiver.

---

## 2. ⭐⭐ Amplitude modulation

### 💡 The idea

Take a high-frequency **carrier** `cos(2πf_c t)` and let the **message** vary its **amplitude**.

📌 **s(t) = A_c [1 + μ·m(t)] · cos(2πf_c t)**

The envelope of the transmitted wave traces the message — which is why a simple diode "envelope detector" can recover it, and why AM broadcast receivers were cheap enough to be ubiquitous in the 1930s.

📌 ⭐ **Modulation index μ = A_m / A_c**, and equivalently
📌 ⭐ **μ = (A_max − A_min) / (A_max + A_min)** (measurable from an oscilloscope trace)

⚠ ⭐ **μ > 1 is OVERMODULATION** → the envelope is distorted and inverts (phase reversal), and the envelope detector fails. μ = 1 is the maximum usable.

### 2.1 ⭐⭐ Bandwidth of the AM variants

💡 Multiplying by a carrier **shifts** the message spectrum up to f_c, producing a mirror-image pair of **sidebands** — one above the carrier (USB) and one below (LSB).

| Scheme | ⭐ Bandwidth | Carrier sent? | Power efficiency | Receiver |
|---|---|---|---|---|
| ⭐ **AM (DSB-FC)** | ⭐ **2f_m** | ✅ Yes | ⭐ **Poor** | Simple envelope detector |
| ⭐ **DSB-SC** | ⭐ **2f_m** | ❌ Suppressed | Better | Needs coherent detection |
| ⭐ **SSB** | ⭐ **f_m** | ❌ Suppressed | ⭐ **Best** | Needs coherent detection |
| **VSB** | Between f_m and 2f_m | Partial (a vestige) | Good | Used for analog TV video |

⚠ ⭐ **Suppressing the CARRIER does not reduce the BANDWIDTH** — DSB-SC still occupies 2f_m, because both sidebands remain. **Only SSB halves the bandwidth**, by discarding one (redundant) sideband.

### 2.2 ⭐⭐ AM power relations

📌 ⭐ **P_total = P_c (1 + μ²/2)**
📌 **Sideband power P_SB = P_c · μ²/2**, split equally between the two sidebands
📌 ⭐ **Efficiency η = μ² / (2 + μ²)**

### 🔢⭐ The key calculation

**At μ = 1 (100% modulation):**
```
P_total = P_c (1 + 1/2) = 1.5 P_c
P_sidebands = 0.5 P_c
Fraction of power in the sidebands = 0.5 / 1.5 = 1/3 = 33.3%
```
⭐ **So even at maximum modulation, only 33.3% of the transmitted power carries information — TWO-THIRDS is wasted on the carrier**, which conveys nothing.

⭐ **This single fact is the entire justification for DSB-SC and SSB**, and it is the most-asked AM question.

🔢 **At μ = 0.5:** P_total = P_c(1 + 0.125) = 1.125 P_c; efficiency = 0.25/2.25 = **11.1%** — worse still.
🔢 **If the carrier power is 100 W and μ = 0.6:** P_total = 100(1 + 0.18) = **118 W**; each sideband carries 9 W.

### 2.3 Detection

⭐ **Envelope detector** — a diode, a resistor and a capacitor. Works only for **AM with μ ≤ 1**. The RC time constant must satisfy `1/f_c ≪ RC ≪ 1/f_m` (fast enough to follow the message, slow enough to smooth the carrier).

⭐ **Coherent (synchronous) detection** — multiply by a **locally generated carrier that is synchronised in both frequency and phase**, then low-pass filter. Required for DSB-SC and SSB (which have no carrier to define the envelope). More complex — hence AM broadcast's choice of the wasteful DSB-FC.

### 2.4 ⭐⭐ The superheterodyne receiver

### 💡 The idea

**The problem:** a receiver must tune across the whole AM band (540–1600 kHz) while providing sharp selectivity (rejecting the adjacent station 10 kHz away). Building a filter that is simultaneously *tunable* and *very sharp* is extremely hard.

⭐ **The solution (Armstrong, 1918): shift EVERY station down to the SAME fixed frequency**, called the **Intermediate Frequency (IF)**, and put all the sharp filtering and gain there — in a filter that never has to tune.

```
Antenna → RF amplifier → MIXER → IF amplifier → Detector → AF amp → Speaker
                           ↑      (fixed freq,
                    Local Oscillator  sharp filter,
                     (tunable)        most of the gain)
```

📌 ⭐ **Standard IF: 455 kHz for AM broadcast; 10.7 MHz for FM broadcast.**
📌 **f_LO = f_signal + f_IF** (high-side injection)

### ⭐⭐ The image frequency problem

💡 The mixer produces both the **difference** and the **sum** of its inputs. So *two* input frequencies map to the same IF:
- the wanted signal at f_LO − f_IF
- an unwanted signal at f_LO + f_IF

📌 ⭐ **Image frequency f_image = f_signal + 2·f_IF**

### 🔢 Worked example

**Wanted station at 1000 kHz, IF = 455 kHz:**
```
f_LO    = 1000 + 455 = 1455 kHz
f_image = 1000 + 2(455) = 1910 kHz
```
Check: 1910 − 1455 = 455 ✅ — the image also lands on the IF.

⭐⭐ **Crucial point: the image MUST be rejected by the RF stage, BEFORE the mixer.** Once mixed, the image is at exactly the same frequency as the wanted signal and is **indistinguishable** — no amount of IF filtering can remove it.

⭐ **A higher IF pushes the image further away, making it easier to reject — but a lower IF gives better selectivity.** That trade-off is why 455 kHz was chosen.

---

## 3. ⭐⭐ Angle modulation (FM and PM)

### 💡 The idea

Instead of varying the carrier's amplitude, vary its **frequency** (FM) or **phase** (PM). The amplitude stays **constant**.

⭐ **Why this is a huge win:** most noise adds itself to the **amplitude** of a signal. If the information is not in the amplitude, a **limiter** circuit can simply clip the received signal to a constant amplitude, **throwing the noise away**. This is why FM radio sounds clean and AM radio hisses.

📌 ⭐ **Frequency deviation Δf = k_f · A_m** — how far the carrier swings, set by the message *amplitude*
📌 ⭐ **FM modulation index β = Δf / f_m**
📌 **PM modulation index β_PM = k_p · A_m** — ⭐ **independent of f_m** (a key FM/PM difference)

### 3.1 ⭐⭐ Carson's rule

📌 ⭐⭐ **BW = 2(Δf + f_m) = 2·f_m·(β + 1)**

💡 Unlike AM, FM's spectrum is theoretically **infinite** (Bessel-function sidebands extend forever). Carson's rule is the practical estimate that captures ~98% of the power.

### 🔢 Worked examples

🔢 **FM broadcast: Δf = 75 kHz, f_m = 15 kHz:**
```
BW = 2(75 + 15) = 180 kHz
```
⭐ (Regulators allocate 200 kHz per FM station — the extra is a guard band.) Compare AM broadcast's 10 kHz channels: ⭐ **FM trades ~20× the bandwidth for its noise immunity.**

🔢 **Δf = 10 kHz, f_m = 5 kHz:** β = 2, BW = 2(10+5) = **30 kHz**

| | **Narrowband FM (β ≪ 1)** | **Wideband FM (β ≫ 1)** |
|---|---|---|
| Bandwidth | ≈ **2f_m** (same as AM) | ≈ **2Δf** |
| Noise performance | Modest | ⭐ **Excellent** |

### 3.2 ⭐ FM vs AM

| | **AM** | ⭐ **FM** |
|---|---|---|
| Noise immunity | ⭐ **Poor** | ⭐ **Excellent** (amplitude limiting) |
| Bandwidth | Narrow (2f_m) | ⭐ **Much wider** |
| Transmitted power | ⭐ **Varies with modulation** | ⭐ **CONSTANT** |
| Circuit complexity | Simple | Complex |
| Range | Longer (skywave) | Line of sight |

📌 ⭐ **FM's total transmitted power is CONSTANT regardless of modulation.** Modulation only **redistributes** power among the carrier and sidebands (the Bessel-function amplitudes) — it never changes the total. ⭐ A directly-asked fact.

⭐ **Pre-emphasis / de-emphasis** — boost high message frequencies before transmission and cut them (along with the noise) after reception, improving high-frequency SNR.

---

## 4. ⭐⭐ Information theory

### 💡 The idea

Shannon's 1948 insight: **information is surprise.** A message that tells you something you already expected carries little information; a message that tells you something improbable carries a lot.

📌 ⭐ **Self-information I(x) = log₂(1/p) = −log₂ p** bits

🔢 "The sun rose today" (p ≈ 1) → I ≈ **0 bits** — no information.
🔢 A fair coin landing heads (p = 0.5) → I = log₂2 = **1 bit**.
🔢 One specific outcome of a fair die (p = 1/6) → I = log₂6 ≈ **2.58 bits**.

### 4.1 ⭐⭐ Entropy

📌 ⭐ **Entropy H(X) = −Σ pᵢ log₂ pᵢ** bits per symbol

💡 **What it means:** the **average** information per symbol, i.e. the average number of bits genuinely needed to encode a symbol from this source. It is the source's fundamental compressibility limit.

**Properties:**
📌 ⭐ **H is MAXIMUM when all symbols are EQUALLY LIKELY**, giving ⭐ **H_max = log₂ M** for M symbols
📌 **H = 0** when one symbol has probability 1 (no uncertainty, no information)
📌 **0 ≤ H(X) ≤ log₂ M**

💡 **Why uniform maximises entropy:** uncertainty is greatest when you have no idea which symbol is coming. Any skew makes the source more predictable, hence less informative per symbol.

### 🔢 Worked examples

🔢 **Binary source, p = 0.5 each:** H = −(0.5 log₂0.5 + 0.5 log₂0.5) = 0.5 + 0.5 = ⭐ **1 bit/symbol** (the maximum for 2 symbols).

🔢 **Binary source, p = 0.9 / 0.1:** H = −(0.9 log₂0.9 + 0.1 log₂0.1) = 0.137 + 0.332 = **0.469 bits/symbol** — much less than 1, because the source is predictable.

🔢 **Four symbols with p = {0.5, 0.25, 0.125, 0.125}:**
```
H = 0.5(1) + 0.25(2) + 0.125(3) + 0.125(3)
  = 0.5 + 0.5 + 0.375 + 0.375 = 1.75 bits/symbol
```
⭐ Compare log₂4 = 2 bits for a fixed-length code — so a good code (Huffman, Week 5) can save 12.5% here.

🔢 **Eight equally likely symbols:** H = log₂8 = **3 bits/symbol** (and no compression is possible).

### 4.2 ⭐ Mutual information and channel capacity

📌 **Joint entropy** H(X,Y) · **Conditional entropy** H(Y|X)
📌 ⭐ **Mutual information I(X;Y) = H(X) − H(X|Y) = H(Y) − H(Y|X) = H(X) + H(Y) − H(X,Y)**

💡 **What it means:** *how much does receiving Y tell you about X?* It is the uncertainty about X, minus the uncertainty that remains about X after seeing Y.
- I(X;Y) ≥ 0 always
- ⭐ **I(X;Y) = 0 if and only if X and Y are independent** (the output tells you nothing about the input — a useless channel)

📌 **Channel capacity C = max I(X;Y)**, maximised over all input distributions.

### 4.3 ⭐⭐ The channel capacity theorems

📌 ⭐⭐ **Shannon–Hartley: C = B log₂(1 + S/N)** bits per second
📌 ⭐ **Nyquist (noiseless): C = 2B log₂ L** bps, where L = number of signal levels

💡 **What Shannon's theorem says:** below capacity C, **error-free** communication is possible (with clever enough coding). **Above** C it is impossible, no matter what you do. It is a hard physical limit.

### 🔢 Worked examples

🔢 **B = 3000 Hz, S/N = 3:** C = 3000 log₂4 = ⭐ **6000 bps**
🔢 **B = 4000 Hz, S/N = 255:** C = 4000 log₂256 = 4000 × 8 = ⭐ **32,000 bps**
🔢 **B = 1 MHz, SNR = 20 dB:** S/N = 100 → C = 10⁶ × log₂101 ≈ 10⁶ × 6.66 = **6.66 Mbps**

⭐ **Note how capacity grows only LOGARITHMICALLY with SNR but LINEARLY with bandwidth** — which is why modern systems chase bandwidth (5G's millimetre waves) rather than transmit power.

### 4.4 Source coding

📌 ⭐ **Source coding theorem: the minimum achievable average codeword length ≥ H(X).** You cannot compress below the entropy.
📌 **Code efficiency = H(X) / L̄**, where L̄ is the actual average codeword length.
📌 **Kraft's inequality** for a prefix-free code: Σ 2^(−lᵢ) ≤ 1

**Source codes:** Shannon–Fano · ⭐ **Huffman (optimal prefix-free code — see Week 5)** · Lempel–Ziv (universal, no prior statistics needed — the basis of ZIP and GIF).

---

## 5. ⭐⭐ Digital communication

### 💡 Why go digital

An analog signal degrades a little at every amplifier — and the degradation accumulates irreversibly. A digital signal can be **regenerated**: as long as you can still tell a 1 from a 0, you rebuild a perfect copy. Add error-correcting codes and you get essentially error-free transmission over arbitrarily long distances. That is the whole case for digitisation.

Getting from analog to digital takes three steps: **sample → quantise → encode**.

## 5.1 ⭐⭐ Sampling

📌 ⭐⭐ **Sampling theorem (Nyquist): f_s ≥ 2·f_m**

💡 **What it says:** a signal band-limited to f_m Hz is **completely determined** by samples taken at twice that rate. Nothing is lost.

📌 **The minimum rate 2f_m is the NYQUIST RATE**; 1/(2f_m) is the **Nyquist interval**.
⚠ ⭐ **Sampling below the Nyquist rate causes ALIASING** — high frequencies masquerade as low ones and cannot be separated afterwards. Prevented by an **anti-aliasing low-pass filter** before sampling.

🔢 **Telephone speech** is band-limited to ~4 kHz → f_s = **8 kHz** (the actual telephony standard).
🔢 **Audio CD:** human hearing to 20 kHz → f_s = 44.1 kHz (slightly above 40 kHz, for filter margin).

## 5.2 ⭐⭐ Quantisation

💡 Samples are still analog *in amplitude*. **Quantisation** rounds each sample to one of L discrete levels — and this rounding is an **irreversible** loss, called **quantisation noise**.

📌 ⭐ **Bits per sample n = log₂ L**
📌 ⭐ **Bit rate = f_s × n** bits per second
📌 **Step size Δ = (V_max − V_min)/L = 2V/2ⁿ**
📌 **Quantisation noise power = Δ²/12**

📌 ⭐⭐ **SNR of a uniform quantiser (dB) = 6.02n + 1.76**

💡 ⭐ **The practical meaning: EACH EXTRA BIT buys about 6 dB of SNR.** That single sentence is worth remembering; it explains why 16-bit audio (≈98 dB) sounds so much better than 8-bit (≈50 dB).

### 🔢 Worked examples

🔢 **256 quantisation levels:** n = log₂256 = ⭐ **8 bits/sample**
🔢 **Telephony PCM:** f_s = 8 kHz, n = 8 → bit rate = 8000 × 8 = ⭐ **64 kbps** (the standard voice channel — this is where the number 64 kbps comes from)
🔢 **SNR for n = 8:** 6.02(8) + 1.76 = ⭐ **49.9 dB**
🔢 **SNR for n = 16:** 6.02(16) + 1.76 = **98.1 dB**
🔢 **Audio CD bit rate:** 44,100 samples/s × 16 bits × 2 channels = **1.41 Mbps**

⭐ **Companding (non-uniform quantisation):** speech spends most of its time at low amplitudes, where a uniform quantiser's fixed step is proportionally huge. **Companding** compresses the signal (fine steps for small amplitudes, coarse for large) before uniform quantisation, then expands it after. ⭐ **μ-law** (North America/Japan, μ = 255) and ⭐ **A-law** (Europe/India, A = 87.6).

## 5.3 ⭐⭐ PCM, DPCM and Delta Modulation

### 💡 The idea — exploiting redundancy

Consecutive samples of speech or video are **highly correlated** — sample 1001 is usually very close to sample 1000. Encoding each sample independently (PCM) therefore wastes bits. **Encode the DIFFERENCE instead**, which needs fewer bits for the same accuracy.

| Technique | 💡 What is encoded | Bit rate |
|---|---|---|
| ⭐ **PCM** | Each sample **independently** | ⭐ **Highest** |
| ⭐ **DPCM** | The **DIFFERENCE** between the sample and a **PREDICTED** value | Lower |
| **ADPCM** | DPCM with an **adaptive** predictor/quantiser | Lower still |
| ⭐ **Delta Modulation (DM)** | ⭐ **1-bit DPCM** — transmit only whether the signal went **up or down** | ⭐ **1 bit/sample** |
| **ADM** | DM with an **adaptive step size** | |

### ⭐⭐ Delta modulation's two errors

DM sends one bit per sample: "+1 step" or "−1 step". This creates two failure modes that pull in **opposite** directions:

⭐ **1. Slope overload distortion** — the ⭐ **step size is TOO SMALL** to track a **fast-changing** signal. The staircase cannot keep up and lags behind.
📌 ⭐ **Avoided when Δ · f_s ≥ max|dm/dt|** (the staircase's maximum slope must exceed the signal's)

⭐ **2. Granular (hunting) noise** — the ⭐ **step size is TOO LARGE** for a **slowly varying** signal. The output oscillates up-down-up-down around the true value.

⚠ ⭐ **These two requirements CONFLICT** — reducing Δ cures granular noise but worsens slope overload, and vice versa. ⭐ **That conflict is precisely why ADAPTIVE delta modulation exists:** it enlarges Δ when tracking fast changes and shrinks it when the signal is flat.

**Line coding:** NRZ · RZ · ⭐ **Manchester** (a transition in the middle of every bit → **self-clocking**, so no separate clock line is needed) · Differential Manchester · AMI · bipolar.

## 5.4 ⭐⭐⭐ Digital modulation schemes

### 💡 The idea

To send bits over a radio or telephone channel, you must impress them onto a carrier. You can vary the carrier's **amplitude**, **frequency**, **phase**, or a combination.

| Scheme | ⭐ What varies | Bandwidth efficiency | ⭐ Noise performance |
|---|---|---|---|
| ⭐ **ASK** | **Amplitude** | Low | ⭐ **WORST** — amplitude is exactly what noise attacks |
| ⭐ **FSK** | **Frequency** | ⭐ **Lowest** (needs the most bandwidth) | Better than ASK |
| ⭐ **PSK (BPSK)** | **Phase** | Good | ⭐ **BEST of the binary schemes** |
| **QPSK** | Phase, 4 states | **2 bits/symbol** | Same BER as BPSK at equal E_b/N₀ |
| ⭐ **QAM** | ⭐ **Amplitude AND phase** | ⭐ **HIGHEST** | Needs a higher SNR |

💡 **Why PSK beats ASK:** the two BPSK symbols are at phases 0° and 180° — **diametrically opposite** in the signal space, i.e. as far apart as possible for a given power. ASK's symbols (on/off) are only half as far apart, so noise flips them more easily.

💡 **Why QAM is the most efficient:** by using both amplitude and phase it packs many symbols into the signal space (16-QAM = 4 bits/symbol, 256-QAM = 8 bits/symbol). But packing them closer means noise needs less energy to cause an error — hence the SNR requirement. ⭐ **This is the fundamental bandwidth/power trade-off**, and it is why your WiFi drops from 256-QAM to QPSK when you walk away from the router.

### ⭐ Rate formulas

📌 ⭐⭐ **Bit rate = symbol (baud) rate × log₂ M**, where M is the number of symbols

### 🔢 Worked examples

🔢 **16-QAM at 2400 baud:** bit rate = 2400 × log₂16 = 2400 × 4 = ⭐ **9600 bps**
🔢 **QPSK at 1000 baud:** 1000 × 2 = **2000 bps**
🔢 **64-QAM at 1 Mbaud:** 1 × 10⁶ × 6 = **6 Mbps**
🔢 **A 9600 bps link using 8-PSK:** baud rate = 9600 / log₂8 = 9600/3 = **3200 baud**

⚠ ⭐ **Baud rate ≠ bit rate** unless M = 2. Baud counts *symbols per second*; bit rate counts *bits per second*.

📌 **Bandwidth (raised-cosine pulse, roll-off α): BW = (1 + α) × symbol rate**
📌 **ASK/PSK bandwidth ≈ 2 × bit rate / log₂M** · **FSK bandwidth ≈ 2Δf + 2f_b**

### ⭐ Bit Error Rate (BER)

📌 **Coherent BPSK: P_e = Q(√(2E_b/N₀))**
📌 **Coherent BFSK: P_e = Q(√(E_b/N₀))**

⭐ **BPSK needs 3 dB LESS power than BFSK for the same BER** (the factor of 2 inside the square root).
⭐ **BER falls as E_b/N₀ rises**, and higher-order modulation needs higher E_b/N₀ for the same BER.

## 5.5 ⭐⭐ Optimum reception

### ⭐⭐ The matched filter

📌 ⭐ **A matched filter's impulse response is the TIME-REVERSED, DELAYED version of the transmitted pulse:** h(t) = s(T − t).

📌 ⭐⭐ **It MAXIMISES the output signal-to-noise ratio at the sampling instant, in additive white Gaussian noise.**
📌 **Maximum output SNR = 2E/N₀**, where E is the pulse energy.

💡 **Intuition:** the filter correlates the noisy received waveform against the *known* pulse shape. Wherever the received signal resembles the expected pulse, the correlation is large; noise, being uncorrelated with the pulse, largely cancels itself out over the integration.

⚠⚠ ⭐ **The matched filter MAXIMISES SNR. It does NOT minimise distortion and it does NOT remove ISI.** (Removing ISI is the equaliser's job — §5.6.) This distinction is a favourite trap.

⭐ A **correlator receiver** is a mathematically equivalent implementation.

### ⭐⭐ MAP vs ML decoding

| | ⭐ **ML (Maximum Likelihood)** | ⭐ **MAP (Maximum A Posteriori)** |
|---|---|---|
| Maximises | **P(received \| sent)** | **P(sent \| received)** |
| ⭐ Uses prior probabilities? | ⭐ **❌ No** | ⭐ **✅ YES** |
| Optimal when | Priors are equal or unknown | Priors are known |
| Minimises | Likelihood-based error | ⭐ **The overall probability of error** |

💡 **The difference in plain terms.** ML asks *"which transmitted symbol would most likely have produced this received waveform?"* MAP asks *"given this waveform, which transmitted symbol is most probable?"* — and to answer that you need to know how often each symbol is sent in the first place.

🔢 If a source sends '0' 90% of the time, and a received waveform is marginally closer to '1', **ML** says '1' but **MAP** may still say '0' — because '0' was far more likely a priori. MAP is right more often.

📌 ⭐ **MAP reduces to ML when all symbols are EQUALLY LIKELY** (the priors cancel out). ⭐ **MAP is the overall optimum decision rule.**

⭐ *(Note the parallel with Bayes' theorem in Part B — MAP is literally Bayes' rule applied to detection.)*

## 5.6 ⭐⭐ ISI and synchronization

### 💡 Inter-Symbol Interference

Any band-limiting (a filter, a cable) **spreads** a pulse in time. Multipath propagation does the same. So each symbol's energy smears into its neighbours' time slots.

📌 ⭐ **ISI = Inter-Symbol Interference** — adjacent symbols contaminate each other's sampling instants, causing errors even with no noise at all.

### ⭐⭐ The four mitigations

⭐ **1. Nyquist criterion for zero ISI** — the pulse must be **zero at every OTHER sampling instant** (only non-zero at its own). The ideal such pulse is a `sinc`, giving the minimum possible bandwidth **R_s/2** — but a sinc decays slowly and is impossible to build.

⭐ **2. Raised-cosine pulse shaping** — the practical solution.
📌 ⭐ **BW = (1 + α) × R_s/2**, with roll-off factor **0 ≤ α ≤ 1**
- **α = 0** → the ideal minimum bandwidth (an unbuildable sinc)
- **α = 1** → double the minimum bandwidth, but easy to implement and tolerant of timing error
🔢 A 1 Mbaud signal with α = 0.5 needs BW = 1.5 × 0.5 = **0.75 MHz**.

⭐ **3. Equalisation at the receiver** — a filter that **inverts** the channel's distortion. Types: zero-forcing, MMSE, **adaptive** (LMS — trains itself on a known preamble), decision-feedback.

⭐ **4. The EYE DIAGRAM — the diagnostic tool.** Overlay many received symbol periods on an oscilloscope.
- ⭐ **A WIDE OPEN eye** → little ISI, good noise margin, wide timing tolerance
- ⭐ **A closing eye** → ISI and jitter; the vertical opening measures noise margin, the horizontal opening measures timing margin

### ⭐ Synchronization

| Type | 💡 What it recovers |
|---|---|
| ⭐ **Timing (symbol/clock) synchronization** | *When* to sample — the correct instant within each symbol. Early-late gate, Gardner algorithm |
| ⭐ **Frequency and carrier-phase synchronization** | The carrier's exact frequency and phase, needed for coherent detection. **PLL**, **Costas loop**, squaring loop |
| **Frame synchronization** | Where a frame begins — via preambles/sync words |

⚠ ⭐ **Coherent detection requires carrier phase recovery. NON-COHERENT detection avoids it** (e.g. envelope detection of ASK, or differential PSK) **at the cost of about 1–3 dB in SNR.**

## 5.7 ⭐ Error correction

📌 ⭐ **Channel coding theorem (Shannon):** reliable communication is achievable for **any rate R < C**. Coding is what makes it possible.

| Code | 💡 Capability |
|---|---|
| Parity check | Detects **odd** numbers of errors only |
| ⭐ **Hamming code** | ⭐ **Single-error CORRECTING**, double-error detecting (with an extra overall parity bit — "SECDED") |
| Cyclic (CRC) | Very strong **detection** (see Week 8) |
| **BCH, Reed–Solomon** | Multiple and **burst** error correction — CDs, DVDs, QR codes, deep-space links |
| **Convolutional** | Continuous stream; decoded by the ⭐ **Viterbi algorithm** (which is an ML decoder) |
| **Turbo, LDPC** | Near-Shannon-limit performance; used in 4G/5G and WiFi |

📌 ⭐⭐ **Hamming code: 2ʳ ≥ m + r + 1** (m data bits, r parity bits)

🔢 m = 4 → r = 3 (2³ = 8 ≥ 8 ✅) → the ⭐ **(7,4) Hamming code**
🔢 m = 11 → r = 4 (16 ≥ 16 ✅) → the **(15,11)** code
🔢 m = 8 → r = 4 (16 ≥ 13 ✅)

📌 **Code rate = k/n.** A **block code (n,k)** carries k data bits in n transmitted bits, adding n−k redundant bits.
📌 ⭐ **Detect d errors: d_min ≥ d + 1. CORRECT d errors: d_min ≥ 2d + 1.** *(Same rule as Week 8 — it appears in both syllabus sections.)*
📌 ⭐ **The (7,4) Hamming code has d_min = 3** → corrects **1** error, detects **2**.

⭐ **Syndrome decoding:** the parity checks that fail, read as a binary number, **give the position of the erroneous bit directly** — which you flip.

## 5.8 ⭐⭐ Multiple access

### 💡 The idea

Many users must share one channel. Three ways to divide it up:

| Technique | ⭐ How users are separated | 💡 Analogy |
|---|---|---|
| ⭐ **FDMA** | ⭐ **A different FREQUENCY BAND each, all the time** | Everyone speaks at once, but each at a different pitch |
| ⭐ **TDMA** | ⭐ **A different TIME SLOT each, using the full bandwidth** | Everyone takes turns speaking |
| ⭐ **CDMA** | ⭐ **ALL users share the FULL bandwidth ALL the time, separated by ORTHOGONAL CODES** | Everyone speaks at once, in different languages — you filter for yours |
| **SDMA** | Spatial separation (directional beams) | |
| **OFDMA** | Orthogonal subcarriers — used in 4G/5G, WiFi | |

**Requirements:** FDMA needs **guard bands** (filters are imperfect); TDMA needs **guard times** and tight **synchronisation**; CDMA needs **power control** (the **near-far problem** — a nearby loud user drowns a distant one).

### ⭐ How CDMA works

Each user's data bit is multiplied by a unique high-rate **orthogonal spreading code** (a Walsh code). The receiver **correlates** the composite received signal with the desired user's code: that user's data emerges, while all other users' contributions average to near zero (because their codes are orthogonal) and appear as low-level noise.

📌 ⭐ **Processing gain = chip rate / bit rate**
⭐ **Spread spectrum forms:** DSSS (direct sequence) and FHSS (frequency hopping).
⭐ **CDMA has "soft capacity"** — adding users degrades quality gradually rather than causing hard blocking, unlike FDMA/TDMA which have a fixed number of channels.

---

# PART B — PROBABILITY & STATISTICS

## 6. ⭐⭐ Basic probability

### 💡 The foundations

📌 0 ≤ P(A) ≤ 1 · P(certain event) = 1 · P(impossible) = 0 · **P(A′) = 1 − P(A)**

📌 ⭐ **Addition rule: P(A ∪ B) = P(A) + P(B) − P(A ∩ B)**
💡 **Why subtract the intersection:** adding P(A) and P(B) counts the overlap twice, so you remove one copy.

📌 **Mutually exclusive (disjoint):** P(A ∩ B) = 0 ⇒ P(A ∪ B) = P(A) + P(B)
📌 ⭐ **Multiplication rule: P(A ∩ B) = P(A) · P(B|A)**
📌 ⭐ **Independence: P(A ∩ B) = P(A) · P(B)**, equivalently **P(A|B) = P(A)**

### ⚠⚠ Independent vs mutually exclusive

⭐ **These are completely different — and often confused.**

- ⭐ **Mutually exclusive** = they cannot happen **together** (rolling a 3 and rolling a 5 on one die)
- ⭐ **Independent** = one happening tells you **nothing** about the other (a coin flip and a die roll)

⭐ **In fact, for events of non-zero probability, mutually exclusive events are DEPENDENT** — because if A occurred, you now know for certain that B did not. That is maximum information, the opposite of independence.

### 6.1 ⭐ Conditional probability

📌 ⭐ **P(A|B) = P(A ∩ B) / P(B)**, for P(B) > 0

💡 **What it means:** you have been told B happened, so restrict the whole universe to B and ask what fraction of *that* is also A.

📌 **Law of total probability:** if {B₁, B₂, …} partition the sample space,
**P(A) = Σ P(A|Bᵢ) · P(Bᵢ)**

## 6.2 ⭐⭐⭐ Bayes' theorem

> ⭐⭐ **Bayes appears in this exam almost every time. If you learn one thing from Part B, learn this.**

### 💡 The idea

Bayes' theorem **reverses** a conditional probability. You know P(evidence | cause); you want P(cause | evidence).

💡 **Example of the reversal:** it is easy to state *"if a machine is faulty, 5% of its output is defective"*. What you actually need to know is *"this item is defective — how likely is it that the faulty machine made it?"* Bayes converts one into the other.

📌 ⭐⭐ **P(Bᵢ | A) = [ P(A|Bᵢ) · P(Bᵢ) ] / Σⱼ [ P(A|Bⱼ) · P(Bⱼ) ]**

📌 In words: ⭐ **posterior = (likelihood × prior) / evidence**, where the **evidence** in the denominator is the **sum over ALL the ways the observation could have arisen**.

⭐ **The method that never fails:** build the denominator as the total probability of the observation, adding up every path that produces it.

### 🔢⭐ Worked example 1 — the factory problem

**Machine A makes 60% of items with a 2% defect rate; Machine B makes 40% with a 5% defect rate. An item is found defective. What is the probability it came from A?**

**Step 1 — write down what you have:**
```
P(A) = 0.6      P(D|A) = 0.02
P(B) = 0.4      P(D|B) = 0.05
```

**Step 2 — compute each path to "defective":**
```
Via A:  0.6 × 0.02 = 0.012
Via B:  0.4 × 0.05 = 0.020
Total P(D) = 0.032
```

**Step 3 — take the fraction:**
```
P(A|D) = 0.012 / 0.032 = 0.375
```
⭐ **Answer: 0.375**

💡 **Sanity check:** A makes more items but is more reliable, so given a defect it is *less* likely to be A's — and indeed 0.375 < 0.6. ✅

### 🔢⭐ Worked example 2 — the medical test (base-rate neglect)

**A disease affects 1% of the population. A test has 99% sensitivity (detects the disease when present) and a 5% false-positive rate. You test positive. What is the probability you have the disease?**

```
P(D) = 0.01,  P(no D) = 0.99
P(+|D) = 0.99,  P(+|no D) = 0.05

Via D:     0.01 × 0.99 = 0.0099
Via no D:  0.99 × 0.05 = 0.0495
Total P(+) = 0.0594

P(D|+) = 0.0099 / 0.0594 ≈ 0.167
```
⭐ **Answer: only about 16.7%**

💡 **Why so low, counter-intuitively?** Because the disease is **rare**. Among 10,000 people, 100 have it (99 test positive) but 9,900 do not (495 test positive anyway). So of 594 positives, only 99 are genuine. ⭐ **This is called base-rate neglect, and it is exactly why this example is an exam favourite.**

### 🔢 Worked example 3 — two bags

**Bag 1 has 3 red and 2 black balls; Bag 2 has 1 red and 4 black. A bag is chosen at random and a red ball is drawn. What is the probability it came from Bag 1?**
```
Via Bag 1: 0.5 × 3/5 = 0.30
Via Bag 2: 0.5 × 1/5 = 0.10
Total = 0.40
P(Bag 1 | red) = 0.30/0.40 = 0.75
```
⭐ **Answer: 0.75**

## 6.3 ⭐ Counting and simple probability

📌 **Permutations** ⁿPᵣ = n!/(n−r)! — **order matters**
📌 **Combinations** ⁿCᵣ = n!/(r!(n−r)!) — **order does not matter**
📌 ⁿCᵣ = ⁿC₍ₙ₋ᵣ₎ · Σᵣ ⁿCᵣ = 2ⁿ

### 🔢⭐ With vs without replacement — always check

**A box has 3 red and 2 blue balls. Two are drawn. P(both red)?**

⭐ **WITHOUT replacement** (the first ball is not returned, so the second draw's odds change):
```
P = (3/5) × (2/4) = 6/20 = 3/10 = 0.3
```

⭐ **WITH replacement** (the first ball is returned, so the draws are independent):
```
P = (3/5) × (3/5) = 9/25 = 0.36
```

⚠ ⭐ **Exam options routinely include both answers.** Read whether the question says "with replacement", "without replacement", or "simultaneously" (which means *without*).

🔢 **A fair die rolled twice — P(sum = 9)?**
Favourable: (3,6), (4,5), (5,4), (6,3) = 4 out of 36 = ⭐ **1/9**

---

# 7. ⭐⭐ Random variables

## 💡 The idea

A **random variable** attaches a **number** to each outcome of an experiment, so you can do arithmetic with randomness.

🔢 Toss 3 coins. The outcome is `HTH`; the random variable "number of heads" is **2**.

- **Discrete RV** — takes countably many values (a die roll, a count). Described by a **PMF** p(x), with Σp(x) = 1.
- **Continuous RV** — takes any value in a range (a height, a waiting time). Described by a **PDF** f(x), with ∫f(x)dx = 1.

⚠ ⭐ **For a CONTINUOUS random variable, P(X = a) = 0 for any single point.** Only intervals have non-zero probability. (This is why the PDF's *value* is not a probability — it is a density.)

📌 **CDF F(x) = P(X ≤ x)** — non-decreasing, F(−∞) = 0, F(+∞) = 1, and f(x) = dF/dx.

## 7.1 ⭐⭐ Expectation and variance

📌 ⭐ **E[X] = Σ x·p(x)** (discrete) or **∫ x·f(x) dx** (continuous)
💡 The **mean** — the long-run average value, or the "centre of mass" of the distribution.

📌 ⭐⭐ **Var(X) = E[X²] − (E[X])²**
💡 The **spread** — the average squared distance from the mean. ⭐ This computational form (`E[X²] − mean²`) is far easier to use than the definition Σ(x−μ)²p(x), and it is what exams expect.

📌 ⭐ **σ = √Var(X)** — the **standard deviation**, in the same units as the data.

### ⭐⭐ The four properties that get asked

📌 ⭐ **E[aX + b] = a·E[X] + b**
📌 ⭐⭐ **Var(aX + b) = a² · Var(X)**
💡 Note two things: the constant **b vanishes** (shifting the data does not change its spread) and **a is SQUARED** (variance is in squared units).

📌 ⭐⭐ **E[X + Y] = E[X] + E[Y]** — ⭐ **ALWAYS true, even for DEPENDENT variables.** This is the **linearity of expectation**, and it is remarkably powerful.
📌 ⭐⭐ **Var(X + Y) = Var(X) + Var(Y)** — ⭐ **ONLY if X and Y are INDEPENDENT.**

⚠⚠ ⭐ **Linearity of expectation needs NO independence; additivity of variance DOES.** This asymmetry is a standard exam point.

🔢 If E[X] = 5 and Var(X) = 4:
- E[3X + 2] = 3(5) + 2 = **17**
- Var(3X + 2) = 9 × 4 = **36** (the +2 has no effect; the 3 is squared)
- σ(3X + 2) = **6**

---

# 8. ⭐⭐⭐ The five named distributions

> ⭐⭐ **The syllabus names exactly five: uniform, normal, exponential, Poisson, binomial. Memorise this table completely — direct lookups are common.**

| Distribution | Type | PMF/PDF | ⭐ **Mean** | ⭐ **Variance** | 💡 When it applies |
|---|---|---|---|---|---|
| **Bernoulli** | Discrete | p, 1−p | **p** | **p(1−p)** | ⭐ A **single** yes/no trial |
| ⭐ **Binomial** B(n,p) | Discrete | ⁿCₓ pˣ(1−p)ⁿ⁻ˣ | ⭐ **np** | ⭐ **np(1−p)** | ⭐ Number of successes in **n independent trials** |
| ⭐ **Poisson** P(λ) | Discrete | e^(−λ)λˣ/x! | ⭐ **λ** | ⭐ **λ** | ⭐ **Rare events in a fixed interval** |
| ⭐ **Uniform** U(a,b) | Continuous | 1/(b−a) | ⭐ **(a+b)/2** | ⭐ **(b−a)²/12** | All values equally likely |
| ⭐ **Exponential** Exp(λ) | Continuous | λe^(−λx), x ≥ 0 | ⭐ **1/λ** | ⭐ **1/λ²** | ⭐ **WAITING TIME between Poisson events** |
| ⭐ **Normal** N(μ,σ²) | Continuous | (1/σ√2π)e^(−(x−μ)²/2σ²) | ⭐ **μ** | ⭐ **σ²** | ⭐ Sums of many small effects (CLT) |

## 8.1 💡 Understanding each one

### ⭐ Binomial — counting successes

Fixed number of trials n, each independent, each with the same success probability p. Count the successes.

🔢 Toss a fair coin 10 times. Number of heads is B(10, 0.5): mean = 10 × 0.5 = **5**, variance = 10 × 0.5 × 0.5 = **2.5**.
🔢 P(exactly 3 heads in 5 tosses) = ⁵C₃ (0.5)³(0.5)² = 10 × 1/32 = **10/32 = 0.3125**

⭐ **Note the variance np(1−p) is ALWAYS LESS than the mean np** (since 1−p < 1). A quick sanity check.

### ⭐⭐ Poisson — counting rare events

Events occurring **independently at a constant average rate** in a fixed interval of time or space. λ is the average count per interval.

🔢 Calls arriving at a switchboard, typos per page, accidents per month, packets arriving at a router.

📌 ⭐⭐ **Poisson's signature: MEAN = VARIANCE = λ.** No other named distribution has this.

⭐ **Poisson approximates the Binomial** when **n is large and p is small**, with **λ = np**.
💡 *Why:* many trials, each individually unlikely → the count of successes clusters like a Poisson.

🔢 λ = 4 calls/hour. P(exactly 2 calls in an hour) = e⁻⁴ × 4²/2! = e⁻⁴ × 8 ≈ 0.0183 × 8 = ⭐ **0.1465**
🔢 λ = 3. P(no events) = e⁻³ ≈ **0.0498**

### ⭐ Exponential — the waiting time

📌 The **time between** consecutive Poisson events. If events arrive at rate λ per hour, the gap between them is Exp(λ) with mean **1/λ**.

🔢 Calls arrive at λ = 0.5 per hour → mean waiting time between calls = 1/0.5 = ⭐ **2 hours**.

📌 ⭐⭐ **Exponential is MEMORYLESS: P(X > s + t | X > s) = P(X > t)**
💡 **What that means:** if a component has already survived 5 years, its remaining expected life is the *same* as a brand-new one. The distribution has no memory of elapsed time.
⭐ **The exponential (continuous) and geometric (discrete) are the ONLY memoryless distributions.**

### ⭐ Uniform — all values equally likely

🔢 U(0, 10): mean = (0+10)/2 = **5**; variance = 100/12 = **8.33**.
🔢 U(2, 8): mean = **5**; variance = 36/12 = **3**.

### ⭐⭐ Normal — the bell curve

Symmetric, bell-shaped, defined by its mean μ and standard deviation σ.

📌 ⭐ **For a normal distribution, MEAN = MEDIAN = MODE** (perfect symmetry).
📌 ⭐ **Standardisation: Z = (X − μ)/σ** converts any normal to the **standard normal** N(0,1), so one table serves all.

📌 ⭐⭐ **The empirical (68–95–99.7) rule:**
- ⭐ **~68%** of values within **1σ** of the mean
- ⭐ **~95%** within **2σ**
- ⭐ **~99.7%** within **3σ**

🔢 Marks are N(60, 10²). Then ~68% of students score between **50 and 70**; ~95% between **40 and 80**; ~99.7% between **30 and 90**.

📌 ⭐⭐ **Central Limit Theorem (CLT):** the **sum (or mean) of a large number of independent random variables tends to a NORMAL distribution — REGARDLESS of the original distribution.**

💡 ⭐ **Why the normal distribution is everywhere:** almost every real measurement is the accumulation of many small independent influences (height = thousands of genetic and environmental factors), and the CLT says such sums are normal. This is the single most important theorem in statistics.

---

# 9. ⭐⭐ Descriptive statistics

## 9.1 ⭐ Measures of central tendency

| Measure | 📌 Definition | ⭐ Property |
|---|---|---|
| ⭐ **Mean** | Σx / n | Uses **every** value → ⭐ **SENSITIVE to outliers** |
| ⭐ **Median** | The **middle** value of sorted data (mean of the two middle values if n is even) | ⭐ **ROBUST to outliers** |
| ⭐ **Mode** | The **most frequent** value | May not exist, or may be multiple (bimodal) |

### 🔢 Worked examples

🔢 **Data: 2, 3, 3, 5, 7**
```
Mean   = (2+3+3+5+7)/5 = 20/5 = 4
Median = 3 (the middle of five sorted values)
Mode   = 3 (appears twice)
```

🔢 **Data: 1, 2, 3, 4, 100** — the outlier's effect
```
Mean   = 110/5 = 22    ← dragged far up by the 100
Median = 3             ← unaffected
```
⭐ **This is why incomes are reported as a MEDIAN**, not a mean — a few billionaires would make the mean meaningless.

🔢 **Even count: 4, 7, 9, 12** → median = (7+9)/2 = **8**

### ⭐ Skewness relations

📌 **Symmetric:** mean = median = mode
📌 ⭐ **Positively (right) skewed:** mean > median > mode (a long right tail pulls the mean up)
📌 ⭐ **Negatively (left) skewed:** mean < median < mode
📌 ⭐ **Empirical relation (moderately skewed): Mode ≈ 3·Median − 2·Mean**

🔢 Mean = 30, median = 32 → Mode ≈ 3(32) − 2(30) = 96 − 60 = **36**

## 9.2 ⭐ Measures of dispersion

📌 **Range = max − min** (simplest, but uses only two values)
📌 ⭐ **Population variance σ² = Σ(xᵢ − μ)² / N**
📌 ⭐ **Sample variance s² = Σ(xᵢ − x̄)² / (n − 1)** ⚠ **note the n−1 (Bessel's correction)**
📌 ⭐ **Standard deviation σ = √variance** — in the **same units** as the data, which is why it is preferred for reporting
📌 **Coefficient of variation = (σ/μ) × 100%** — for comparing spreads measured on different scales
📌 **Quartiles Q1, Q2 (=median), Q3; IQR = Q3 − Q1**

💡 **Why sample variance divides by n−1:** using the sample mean (rather than the true mean) makes the deviations slightly too small, biasing the estimate downward. Dividing by n−1 instead of n corrects that bias.

### 🔢 Worked example

**Data: 2, 4, 4, 4, 5, 5, 7, 9**
```
Mean = 40/8 = 5
Deviations:        −3, −1, −1, −1, 0, 0, 2, 4
Squared:            9,  1,  1,  1, 0, 0, 4, 16   → sum = 32
Population variance = 32/8 = 4   →  σ = 2
Sample variance     = 32/7 ≈ 4.57 → s ≈ 2.14
```

### ⭐⭐ Effect of transforming the data

📌 ⭐ **Adding a constant c to every value:** mean → mean + c; ⭐ **variance and SD UNCHANGED**
📌 ⭐ **Multiplying every value by k:** mean → k × mean; **variance → k² × variance**; **SD → |k| × SD**

💡 **Why:** shifting the whole data set moves the centre but not the spread. Scaling stretches both, and variance is in squared units.

🔢 Data with mean 50, SD 10. Add 5 to every value → mean **55**, SD **10**. Multiply every value by 2 → mean **100**, SD **20**, variance ×4.

## 9.3 Correlation and regression (awareness)

📌 **Correlation coefficient r ∈ [−1, +1]**: +1 perfect positive linear relationship, −1 perfect negative, 0 no **linear** relationship.
⚠ ⭐ **r = 0 does NOT mean "no relationship"** — only no *linear* one (a perfect parabola can have r = 0).
⚠⚠ ⭐ **Correlation does NOT imply causation.**

---

# 10. ⭐ Rapid-fire facts

## Communication

| Fact | Value |
|---|---|
| **White noise PSD** | ⭐ **Flat/constant** over all frequencies |
| White noise autocorrelation | An **impulse** |
| "White" refers to | The **spectrum**, not the distribution |
| **PSD is the Fourier transform of** | ⭐ **Autocorrelation** (Wiener–Khinchin) |
| R_X(0) equals | **Average power** |
| **Output PSD through an LTI system** | ⭐ **\|H(f)\|² · S_X(f)** |
| Thermal noise | N = kTB |
| First stage dominates noise figure | Friis formula |
| **AM bandwidth** | ⭐ **2f_m** |
| **DSB-SC / SSB bandwidth** | ⭐ **2f_m / f_m** |
| Modulation index | A_m/A_c = (A_max−A_min)/(A_max+A_min) |
| **AM total power** | ⭐ **P_c(1 + μ²/2)** |
| **Sideband power at μ = 1** | ⭐ **33.3%** |
| AM efficiency | μ²/(2+μ²) |
| μ > 1 causes | **Overmodulation**, envelope distortion |
| Envelope detector works for | AM with μ ≤ 1 only |
| DSB-SC/SSB need | **Coherent** detection |
| **Carson's rule** | ⭐ **BW = 2(Δf + f_m)** |
| FM modulation index | Δf/f_m |
| PM modulation index | Independent of f_m |
| **AM IF / FM IF** | ⭐ **455 kHz / 10.7 MHz** |
| **Image frequency** | ⭐ **f_s + 2f_IF** |
| Image must be rejected | **Before** the mixer (RF stage) |
| FM transmitted power | ⭐ **Constant** |
| **Entropy** | ⭐ **−Σ p log₂ p** |
| **Max entropy** | ⭐ **log₂M** (equally likely) |
| Mutual information = 0 means | X and Y independent |
| **Shannon capacity** | ⭐ **B log₂(1 + S/N)** |
| Nyquist capacity | 2B log₂L |
| Capacity grows with SNR | **Logarithmically** |
| Source coding limit | Average length ≥ H(X) |
| **Sampling theorem** | ⭐ **f_s ≥ 2f_m** |
| Below Nyquist rate | **Aliasing** |
| **Bits per sample** | ⭐ **n = log₂L** |
| Bit rate | f_s × n |
| **PCM SNR (dB)** | ⭐ **6.02n + 1.76** (≈6 dB per bit) |
| Telephony PCM | 8 kHz × 8 bits = **64 kbps** |
| Quantisation noise power | Δ²/12 |
| Companding standards | μ-law (255) / A-law (87.6) |
| DPCM encodes | The **difference** from a prediction |
| Delta modulation | **1 bit/sample** |
| **DM errors** | ⭐ **Slope overload (step too small) / granular noise (step too large)** |
| Slope overload avoided when | Δ·f_s ≥ max\|dm/dt\| |
| Self-clocking line code | **Manchester** |
| **Best binary digital modulation** | ⭐ **PSK** |
| Worst noise performance | **ASK** |
| **Most bandwidth-efficient** | ⭐ **QAM** |
| **Bit rate** | ⭐ **Baud rate × log₂M** |
| BPSK vs BFSK | BPSK needs **3 dB less** power |
| **Matched filter** | ⭐ **MAXIMISES output SNR** (= 2E/N₀) |
| Matched filter h(t) | s(T − t) |
| **MAP vs ML** | ⭐ **MAP uses priors; equal when priors are equal** |
| MAP minimises | Probability of error |
| **Zero-ISI pulse** | ⭐ **Raised cosine, BW = (1+α)R_s/2** |
| **ISI diagnostic** | ⭐ **Eye diagram** (wide open = good) |
| ISI removed by | **Equalisation** |
| Non-coherent detection penalty | 1–3 dB |
| **Hamming parity bits** | ⭐ **2ʳ ≥ m + r + 1** |
| (7,4) Hamming d_min | **3** → corrects 1, detects 2 |
| Convolutional code decoder | **Viterbi** (ML) |
| Burst error correction | Reed–Solomon |
| **FDMA / TDMA / CDMA** | ⭐ **Frequency / time / orthogonal CODES, full bandwidth** |
| CDMA processing gain | Chip rate / bit rate |
| CDMA problem | Near-far (needs power control) |

## Probability

| Fact | Value |
|---|---|
| P(A∪B) | **P(A)+P(B)−P(A∩B)** |
| Independence | **P(A∩B) = P(A)P(B)** |
| Mutually exclusive | P(A∩B) = 0 |
| Independent vs mutually exclusive | ⭐ **Different — and incompatible** |
| Conditional probability | P(A∩B)/P(B) |
| **Bayes** | ⭐ **P(A\|Bᵢ)P(Bᵢ) / Σ P(A\|Bⱼ)P(Bⱼ)** |
| **Var(X)** | ⭐ **E[X²] − (E[X])²** |
| **Var(aX+b)** | ⭐ **a²Var(X)** |
| **E[X+Y]** | ⭐ **E[X]+E[Y] — ALWAYS** |
| **Var(X+Y)** | ⭐ **Sum ONLY if independent** |
| Continuous RV: P(X = a) | **0** |
| **Binomial mean / variance** | ⭐ **np / np(1−p)** |
| **Poisson mean / variance** | ⭐ **λ / λ** |
| **Exponential mean / variance** | ⭐ **1/λ / 1/λ²** |
| **Uniform mean / variance** | ⭐ **(a+b)/2 / (b−a)²/12** |
| Normal mean / variance | μ / σ² |
| Poisson approximates | Binomial with large n, small p (λ = np) |
| **Memoryless distributions** | ⭐ **Exponential, geometric** |
| **Normal empirical rule** | ⭐ **68 / 95 / 99.7** |
| Standardisation | Z = (X−μ)/σ |
| **CLT** | Sums tend to **normal**, whatever the original |
| Normal: mean, median, mode | ⭐ **All equal** |
| **Robust to outliers** | ⭐ **Median** |
| Right skewed | Mean > median > mode |
| **Mode ≈** | **3·Median − 2·Mean** |
| Sample variance divides by | ⭐ **n − 1** |
| Add constant c | Mean shifts, ⭐ **SD unchanged** |
| Multiply by k | Mean × k, variance × k², SD × \|k\| |
| Correlation r = 0 | No **linear** relationship |

---

# 11. ⚠ Common traps

**Communication**
1. ⭐ **"White" refers to the FLAT SPECTRUM, not to Gaussianity.**
2. ⭐ **Output PSD uses |H(f)|², not |H(f)|.**
3. ⭐⭐ **DSB-SC bandwidth is still 2f_m** — only **SSB** halves it. Suppressing the carrier saves power, not bandwidth.
4. ⭐ **Carson's rule is 2(Δf + f_m)**, not 2Δf.
5. ⭐ **Image frequency = f_s + 2f_IF**, and it must be rejected **before** the mixer.
6. ⭐ **PCM SNR = 6.02n + 1.76 dB** — about 6 dB per bit.
7. ⭐⭐ **Slope overload = step too SMALL; granular noise = step too LARGE.** Opposite causes.
8. ⭐ **The matched filter maximises SNR; it does NOT remove ISI.**
9. ⭐ **MAP uses priors; ML does not.**
10. ⭐ **Detect d errors needs d+1; CORRECT d needs 2d+1.**
11. **Baud rate ≠ bit rate** unless M = 2.
12. **FM's total transmitted power is constant.**

**Probability**
13. ⭐⭐ **Poisson: MEAN = VARIANCE = λ** (not λ²).
14. ⭐⭐ **Independent ≠ mutually exclusive** — for non-zero probabilities they are incompatible.
15. ⭐⭐ **Var(aX + b) = a²Var(X)** — the constant vanishes and a is **squared**.
16. ⭐⭐ **Expectation is additive always; variance only for independent variables.**
17. ⭐ **With vs without replacement** changes the answer — read the question.
18. ⭐ **Sample variance divides by n−1**, population by N.
19. **For a continuous RV, P(X = a) = 0.**
20. **Correlation does not imply causation, and r = 0 does not mean "unrelated".**

---

# 12. Practice

- **Probability:** GATE [`Paper2_S01_Probability_and_Statistics/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S01_Probability_and_Statistics/) — **125 questions**; state-PSC level [`Paper2_S01_.../`](../02_State_PSC_PYQs/Subject_wise/Paper2_S01_Probability_and_Statistics/) — 50 questions
- **Communication:** [`Paper2_S04_Analog_and_Digital_Communication/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S04_Analog_and_Digital_Communication/) — 46 questions (DSP + information theory). ⚠ **No GATE CSE coverage exists for this section**, so these notes are your primary source.
- Also relevant: `02_State_PSC_PYQs/Papers/Other_State_PSCs/Arunachal_Pradesh_PSC/` includes an **Electronics and Communication Engineering** paper.
- Test: [`Week_09_Test.md`](../04_Mock_Tests/Week_09_Test.md)

**Priority order if short on time:**
⭐ **Communication** — the formula sheet (AM/FM bandwidth and power, Carson, Shannon, Nyquist, PCM SNR, Hamming bound) → the digital-modulation comparison → entropy → matched filter and MAP/ML definitions → FDMA/TDMA/CDMA. ⭐ **Do not attempt derivations — none are needed.**
⭐ **Probability** — **Bayes' theorem** (asked almost every time) → the five-distribution mean/variance table → mean/median/mode/SD → expectation and variance properties.
