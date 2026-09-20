# Week 9 Question Bank — Communication + Probability & Statistics

**Syllabus §4 + §1** · 173 questions · Practice set · +1 / −0.33 marking

> Definitional and plug-in-formula level throughout — Communication is an ECE section inside a CS paper, so no derivations are needed. Attempt in blocks, then self-check against the key and worked solutions.

---

## Part A — Random signals, noise & PSD

**Q1.** The Wiener–Khinchin theorem states that the power spectral density (PSD) of a WSS random process is the
(A) Fourier transform of its autocorrelation function  (B) derivative of its autocorrelation function  (C) Fourier transform of the signal waveform itself  (D) square of its mean value

**Q2.** For a wide-sense-stationary process, the autocorrelation at zero lag R_X(0) equals
(A) the mean value  (B) the average power E[X²]  (C) the variance only  (D) zero

**Q3.** Which property of the autocorrelation function R_X(τ) is correct?
(A) It is an odd function of τ  (B) It is even and attains its maximum at τ = 0  (C) It is always negative  (D) It equals the PSD directly

**Q4.** White noise is characterised by a power spectral density that is
(A) flat (constant) over all frequencies  (B) an impulse at f = 0  (C) Gaussian-shaped in frequency  (D) zero everywhere

**Q5.** The autocorrelation function of white noise is
(A) a constant for all τ  (B) a sinc function  (C) an impulse, (N₀/2)·δ(τ)  (D) a decaying exponential

**Q6.** In "additive white Gaussian noise", the word **white** refers to
(A) the amplitude probability distribution  (B) a flat power spectral density across all frequencies  (C) the noise being Gaussian  (D) the noise having zero mean

**Q7.** Which statement about AWGN is correct?
(A) "White" and "Gaussian" describe the same property  (B) White (flat spectrum) and Gaussian (amplitude distribution) are two independent properties — a process can be white but not Gaussian  (C) White noise is always Gaussian  (D) Gaussian noise is always white

**Q8.** A random process of PSD S_X(f) passes through an LTI system with transfer function H(f). The output PSD is
(A) H(f)·S_X(f)  (B) |H(f)|·S_X(f)  (C) |H(f)|²·S_X(f)  (D) |H(f)|²·S_X(f)²

**Q9.** White noise of PSD N₀/2 passes through an ideal lowpass filter of bandwidth B (from −B to +B) with unity gain. The output noise power is
(A) N₀B/2  (B) N₀B  (C) 2N₀B  (D) N₀/2

**Q10.** The thermal (Johnson) noise power available in a bandwidth B at absolute temperature T is
(A) kT/B  (B) kTB  (C) kT²B  (D) k/(TB)

**Q11.** By Friis' formula, the overall noise figure of a cascaded receiver is dominated by
(A) the first stage — which is why the low-noise amplifier comes first  (B) the last stage  (C) the stage with the highest gain  (D) all stages equally

---

## Part B — Amplitude modulation

**Q12.** The transmission bandwidth of a conventional AM (DSB-FC) signal with message bandwidth f_m is
(A) f_m  (B) 2f_m  (C) f_m/2  (D) 4f_m

**Q13.** The transmission bandwidths of DSB-SC and SSB signals, for a message bandwidth f_m, are respectively
(A) 2f_m and f_m  (B) f_m and 2f_m  (C) 2f_m and 2f_m  (D) f_m and f_m

**Q14.** Which statement about AM bandwidths is correct?
(A) DSB-SC halves the bandwidth compared with AM  (B) SSB occupies 2f_m  (C) DSB-SC still occupies 2f_m; only SSB halves the bandwidth to f_m  (D) all three variants occupy f_m

**Q15.** For an AM signal of modulation index μ, the total transmitted power in terms of the carrier power P_c is
(A) P_c(1 + μ²)  (B) P_c(1 + μ²/2)  (C) P_c(1 + 2μ²)  (D) P_c·μ²/2

**Q16.** The power efficiency of a conventional AM signal is
(A) μ²/2  (B) μ²/(2 + μ²)  (C) μ²/(1 + μ²)  (D) μ/(2 + μ)

**Q17.** At 100% modulation (μ = 1), the fraction of the total transmitted power carried by both sidebands together is
(A) 25%  (B) 33.3%  (C) 50%  (D) 66.7%

**Q18.** An oscilloscope trace of an AM wave shows A_max = 15 V and A_min = 5 V. The modulation index is
(A) 0.25  (B) 0.5  (C) 0.75  (D) 1.0

**Q19.** A modulation index μ > 1 in conventional AM causes
(A) higher efficiency  (B) overmodulation and envelope distortion  (C) reduced bandwidth  (D) coherent detection

**Q20.** An AM transmitter has a carrier power of 100 W and is modulated to μ = 0.6. The total transmitted power is
(A) 118 W  (B) 100 W  (C) 136 W  (D) 150 W

**Q21.** The power efficiency of a conventional AM signal at μ = 0.5 is approximately
(A) 33.3%  (B) 25%  (C) 11.1%  (D) 50%

**Q22.** Which modulation scheme requires coherent (synchronous) detection because it has no transmitted carrier to define the envelope?
(A) AM (DSB-FC)  (B) DSB-SC  (C) any AM signal  (D) none of them

---

## Part C — Superheterodyne receiver

**Q23.** The standard intermediate frequency (IF) for an AM broadcast receiver is
(A) 455 kHz  (B) 10.7 MHz  (C) 45 MHz  (D) 10 kHz

**Q24.** The standard intermediate frequency for an FM broadcast receiver is
(A) 455 kHz  (B) 10.7 MHz  (C) 70 MHz  (D) 100 kHz

**Q25.** In a superheterodyne receiver, the image frequency is given by
(A) f_signal + f_IF  (B) f_signal + 2·f_IF  (C) f_signal − 2·f_IF  (D) 2·f_signal + f_IF

**Q26.** A superheterodyne receiver is tuned to a station at 1000 kHz with IF = 455 kHz. The image frequency is
(A) 1455 kHz  (B) 1910 kHz  (C) 545 kHz  (D) 910 kHz

**Q27.** The image frequency in a superheterodyne receiver must be rejected
(A) at the IF amplifier  (B) at the detector  (C) by the RF stage, before the mixer  (D) it cannot be rejected

---

## Part D — Angle modulation (FM / PM)

**Q28.** The FM modulation index β is
(A) f_m/Δf  (B) Δf/f_m  (C) Δf·f_m  (D) Δf + f_m

**Q29.** By Carson's rule, the bandwidth of an FM signal with peak deviation Δf and maximum modulating frequency f_m is
(A) 2Δf  (B) 2f_m  (C) 2(Δf + f_m)  (D) Δf + f_m

**Q30.** For FM broadcast with Δf = 75 kHz and f_m = 15 kHz, the Carson bandwidth is
(A) 90 kHz  (B) 150 kHz  (C) 180 kHz  (D) 200 kHz

**Q31.** An FM signal has Δf = 10 kHz and f_m = 5 kHz. Its Carson bandwidth is
(A) 15 kHz  (B) 20 kHz  (C) 30 kHz  (D) 10 kHz

**Q32.** Which statement about FM transmitted power is correct?
(A) It varies with the modulation index  (B) It is constant regardless of modulation — modulation only redistributes power among carrier and sidebands  (C) It increases with β  (D) It is zero when unmodulated

**Q33.** Compared with AM, FM offers
(A) poorer noise immunity  (B) better noise immunity at the cost of wider bandwidth  (C) less bandwidth than AM  (D) constant power in AM instead

**Q34.** The phase-modulation index β_PM is
(A) dependent on f_m  (B) independent of f_m  (C) equal to Δf/f_m  (D) always exactly 1

**Q35.** For wideband FM (β ≫ 1), the bandwidth is approximately
(A) 2f_m  (B) 2Δf  (C) Δf  (D) f_m

---

## Part E — Information theory

**Q36.** The self-information of an event of probability p = 1/8 is
(A) 1 bit  (B) 2 bits  (C) 3 bits  (D) 8 bits

**Q37.** The entropy of a discrete source with symbol probabilities pᵢ is
(A) Σ pᵢ log₂ pᵢ  (B) −Σ pᵢ log₂ pᵢ  (C) −Σ log₂ pᵢ  (D) Σ pᵢ²

**Q38.** The maximum entropy of a source with 8 equally likely symbols is
(A) 8 bits/symbol  (B) 4 bits/symbol  (C) 3 bits/symbol  (D) 2 bits/symbol

**Q39.** The entropy of a binary source with p = 0.5 for each symbol is
(A) 0 bit  (B) 0.5 bit  (C) 1 bit  (D) 2 bits

**Q40.** A source has four symbols with probabilities {0.5, 0.25, 0.125, 0.125}. Its entropy is
(A) 2 bits/symbol  (B) 1.75 bits/symbol  (C) 1.5 bits/symbol  (D) 1.9 bits/symbol

**Q41.** A channel of bandwidth 3000 Hz has S/N = 3. By the Shannon–Hartley theorem, its capacity is
(A) 3000 bps  (B) 6000 bps  (C) 9000 bps  (D) 12000 bps

**Q42.** A channel of bandwidth 4000 Hz has S/N = 255. Its Shannon capacity is
(A) 16000 bps  (B) 24000 bps  (C) 32000 bps  (D) 8000 bps

**Q43.** By Nyquist's noiseless formula, a channel of bandwidth 3000 Hz using L = 16 signal levels has capacity
(A) 12000 bps  (B) 24000 bps  (C) 48000 bps  (D) 6000 bps

**Q44.** The mutual information I(X;Y) between channel input and output is zero if and only if
(A) the channel is perfect  (B) X and Y are statistically independent  (C) X = Y  (D) the capacity is maximum

**Q45.** By the source-coding theorem, the minimum achievable average codeword length is
(A) log₂ M  (B) H(X), the source entropy  (C) 0  (D) 2·H(X)

---

## Part F — Sampling, quantisation, PCM / DPCM / DM

**Q46.** By the sampling theorem, a signal band-limited to f_m must be sampled at a rate of at least
(A) f_m  (B) 2f_m  (C) f_m/2  (D) 4f_m

**Q47.** Telephone speech band-limited to about 4 kHz is sampled at
(A) 4 kHz  (B) 8 kHz  (C) 16 kHz  (D) 44.1 kHz

**Q48.** Sampling a signal below its Nyquist rate causes
(A) aliasing  (B) quantisation noise  (C) companding  (D) no effect

**Q49.** A PCM system using 256 quantisation levels needs how many bits per sample?
(A) 6  (B) 7  (C) 8  (D) 16

**Q50.** Telephony PCM samples at 8 kHz with 8 bits/sample. The bit rate is
(A) 32 kbps  (B) 48 kbps  (C) 64 kbps  (D) 128 kbps

**Q51.** The signal-to-quantisation-noise ratio of an n = 8 uniform quantiser is
(A) 48 dB  (B) 49.9 dB  (C) 56 dB  (D) 6 dB

**Q52.** In uniform PCM, each additional bit per sample improves the SNR by about
(A) 3 dB  (B) 6 dB  (C) 10 dB  (D) 20 dB

**Q53.** The quantisation noise power of a uniform quantiser with step size Δ is
(A) Δ/12  (B) Δ²/12  (C) Δ²/6  (D) Δ/6

**Q54.** DPCM achieves a lower bit rate than PCM because it encodes
(A) each sample independently  (B) the difference between the sample and a predicted value  (C) always exactly one bit  (D) the frequency of the signal

**Q55.** Delta modulation transmits how many bits per sample?
(A) 1  (B) 2  (C) 4  (D) 8

**Q56.** Slope-overload distortion in delta modulation occurs when the
(A) step size is too small to track a fast-changing signal  (B) step size is too large  (C) sampling rate is too high  (D) number of levels is too high

**Q57.** Granular (hunting) noise in delta modulation occurs when the
(A) step size is too small  (B) step size is too large for a slowly varying signal  (C) signal is aliased  (D) signal is overmodulated

**Q58.** The two standard companding laws are
(A) μ-law (μ = 255) and A-law (A = 87.6)  (B) μ-law (87.6) and A-law (255)  (C) both set to 100  (D) NRZ and RZ

**Q59.** An audio CD samples at 44.1 kHz, 16 bits/sample, 2 channels. Its bit rate is
(A) 0.7 Mbps  (B) 1.41 Mbps  (C) 2.8 Mbps  (D) 0.35 Mbps

---

## Part G — Digital modulation & optimum reception

**Q60.** Which digital modulation scheme has the **worst** noise performance, because information is carried in the amplitude that noise attacks?
(A) ASK  (B) PSK  (C) FSK  (D) QAM

**Q61.** Which binary digital modulation scheme has the **best** noise performance?
(A) ASK  (B) FSK  (C) PSK  (D) none differ

**Q62.** Which scheme is the **most bandwidth-efficient** by using both amplitude and phase?
(A) ASK  (B) FSK  (C) QAM  (D) BPSK

**Q63.** A 16-QAM system operates at 2400 baud. Its bit rate is
(A) 2400 bps  (B) 4800 bps  (C) 9600 bps  (D) 38400 bps

**Q64.** A QPSK system operates at 1000 baud. Its bit rate is
(A) 1000 bps  (B) 2000 bps  (C) 4000 bps  (D) 500 bps

**Q65.** A 64-QAM system operates at 1 Mbaud. Its bit rate is
(A) 1 Mbps  (B) 6 Mbps  (C) 8 Mbps  (D) 64 Mbps

**Q66.** A 9600 bps link uses 8-PSK. Its symbol (baud) rate is
(A) 9600 baud  (B) 4800 baud  (C) 3200 baud  (D) 1200 baud

**Q67.** The maximum output SNR of a matched filter, for a pulse of energy E in AWGN of PSD N₀/2, is
(A) E/N₀  (B) 2E/N₀  (C) N₀/2E  (D) E²/N₀

**Q68.** Which statement about the matched filter is correct?
(A) It removes inter-symbol interference  (B) It minimises distortion  (C) It maximises output SNR but does NOT remove ISI  (D) It is a type of equaliser

**Q69.** The impulse response of a matched filter for a pulse s(t) over [0, T] is
(A) s(t)  (B) s(−t)  (C) s(T − t)  (D) s(t + T)

**Q70.** How do MAP and ML decoding differ?
(A) ML uses prior probabilities  (B) MAP uses prior probabilities of the symbols; ML does not  (C) both ignore priors  (D) MAP uses only the likelihood

**Q71.** MAP decoding reduces to ML decoding when
(A) the priors are known  (B) all symbols are equally likely  (C) the noise is zero  (D) never

**Q72.** For the same bit-error rate, coherent BPSK requires
(A) 3 dB more power than BFSK  (B) 3 dB less power than BFSK  (C) the same power as BFSK  (D) BFSK is always better

**Q73.** QAM varies the carrier's
(A) amplitude only  (B) phase only  (C) amplitude and phase together  (D) frequency

---

## Part H — ISI, synchronization, error correction & multiple access

**Q74.** Inter-symbol interference (ISI) is
(A) noise added by an amplifier  (B) adjacent symbols contaminating each other's sampling instants  (C) carrier leakage into the message  (D) rounding error in quantisation

**Q75.** A 1 Mbaud signal uses raised-cosine pulse shaping with roll-off α = 0.5. Its bandwidth is
(A) 0.5 MHz  (B) 0.75 MHz  (C) 1.0 MHz  (D) 1.5 MHz

**Q76.** Inter-symbol interference is removed by
(A) a matched filter  (B) an equaliser  (C) a limiter  (D) a mixer

**Q77.** A **wide-open** eye diagram indicates
(A) severe ISI  (B) little ISI and good noise/timing margins  (C) high noise only  (D) aliasing

**Q78.** For a Hamming code with m data bits and r parity bits, the required relation is
(A) 2ʳ ≥ m + r + 1  (B) 2ʳ ≥ m + 1  (C) r ≥ m  (D) 2ᵐ ≥ r + 1

**Q79.** A single-error-correcting Hamming code for m = 4 data bits is the
(A) (6,4) code  (B) (7,4) code  (C) (8,4) code  (D) (5,4) code

**Q80.** The (7,4) Hamming code has d_min = 3, so it can
(A) correct 2 and detect 3 errors  (B) correct 1 and detect 2 errors  (C) correct 3 errors  (D) only detect 1 error

**Q81.** To **correct** up to d errors, a code's minimum distance must satisfy
(A) d_min ≥ d  (B) d_min ≥ d + 1  (C) d_min ≥ 2d + 1  (D) d_min ≥ 2d

**Q82.** Convolutional codes are optimally decoded by the
(A) Viterbi algorithm  (B) Huffman algorithm  (C) Bayes rule  (D) Nyquist criterion

**Q83.** In FDMA, TDMA and CDMA, users are separated respectively by
(A) frequency band / time slot / orthogonal code  (B) time slot / frequency band / orthogonal code  (C) orthogonal code / frequency band / time slot  (D) all by time slot

**Q84.** The processing gain of a CDMA / spread-spectrum system is
(A) bit rate / chip rate  (B) chip rate / bit rate  (C) chip rate × bit rate  (D) always 1

**Q85.** Which line code is self-clocking, with a transition in the middle of every bit?
(A) NRZ  (B) RZ  (C) Manchester  (D) AMI

**Q86.** Which code is designed for burst-error correction (used in CDs, DVDs, QR codes)?
(A) Hamming  (B) simple parity  (C) Reed–Solomon  (D) BPSK

---

## Part I — Basic probability & counting

**Q87.** The addition rule of probability states P(A ∪ B) =
(A) P(A)·P(B)  (B) P(A) + P(B)  (C) P(A) + P(B) − P(A ∩ B)  (D) P(A) + P(B) + P(A ∩ B)

**Q88.** Two events A and B are **independent** if
(A) P(A ∩ B) = 0  (B) P(A ∩ B) = P(A)·P(B)  (C) P(A|B) = 0  (D) P(A ∪ B) = 1

**Q89.** Two events are **mutually exclusive** if
(A) P(A ∩ B) = P(A)·P(B)  (B) P(A ∩ B) = 0  (C) P(A) = P(B)  (D) they are independent

**Q90.** Which statement about independent vs mutually exclusive events is correct?
(A) They are the same thing  (B) Mutually exclusive events with non-zero probability are independent  (C) They are different; mutually exclusive events with non-zero probability are actually dependent  (D) All independent events are mutually exclusive

**Q91.** Conditional probability P(A|B) equals
(A) P(A ∩ B)/P(B)  (B) P(A ∩ B)/P(A)  (C) P(A)·P(B)  (D) P(B)/P(A)

**Q92.** The probability of the complement of A is
(A) 1 − P(A)  (B) 1 + P(A)  (C) P(A) − 1  (D) 1/P(A)

**Q93.** If P(A) = 0.3 and P(B) = 0.4 and A, B are independent, then P(A ∪ B) is
(A) 0.7  (B) 0.58  (C) 0.12  (D) 0.5

**Q94.** A fair die is rolled twice. The probability that the sum is 7 is
(A) 1/6  (B) 1/9  (C) 1/12  (D) 5/36

**Q95.** A single fair die is rolled. The probability of an even number is
(A) 1/3  (B) 1/2  (C) 2/3  (D) 1/6

**Q96.** One card is drawn from a standard 52-card deck. The probability it is a king is
(A) 1/52  (B) 1/13  (C) 1/4  (D) 4/13

**Q97.** Which statement about permutations and combinations is correct?
(A) In ⁿPᵣ order does not matter  (B) In ⁿCᵣ order matters  (C) In ⁿPᵣ order matters; in ⁿCᵣ order does not  (D) Both are identical

**Q98.** The number of ways to choose a committee of 3 from 10 people is
(A) 120  (B) 720  (C) 30  (D) 1000

**Q99.** A box has 3 red and 2 blue balls. Two are drawn **without replacement**. P(both red) is
(A) 9/25  (B) 3/10  (C) 2/5  (D) 1/2

**Q100.** For the same box (3 red, 2 blue), two balls drawn **with replacement**. P(both red) is
(A) 9/25  (B) 3/10  (C) 6/25  (D) 1/2

---

## Part J — Bayes' theorem & total probability

**Q101.** Bayes' theorem for a partition {Bⱼ} is P(Bᵢ|A) =
(A) P(A|Bᵢ)·P(Bᵢ) / Σⱼ P(A|Bⱼ)·P(Bⱼ)  (B) P(A|Bᵢ)·P(A)  (C) P(Bᵢ)/P(A)  (D) P(A ∩ Bᵢ)

**Q102.** Machine A makes 60% of items (2% defective); machine B makes 40% (5% defective). Given a defective item, the probability it came from A is
(A) 0.300  (B) 0.375  (C) 0.500  (D) 0.625

**Q103.** A disease affects 1% of a population. A test has 99% sensitivity and a 5% false-positive rate. Given a positive result, the probability of actually having the disease is about
(A) 0.99  (B) 0.167  (C) 0.50  (D) 0.05

**Q104.** Bag 1 has 3 red and 2 black balls; Bag 2 has 1 red and 4 black. A bag is chosen at random and a red ball drawn. P(it came from Bag 1) is
(A) 0.5  (B) 0.6  (C) 0.75  (D) 0.3

**Q105.** Machines M1, M2, M3 make 50%, 30%, 20% of output with defect rates 3%, 4%, 5%. Given a defective item, the probability it came from M3 is
(A) 0.200  (B) 0.270  (C) 0.500  (D) 0.100

**Q106.** For the two-bag setup of Q104, the overall probability of drawing a red ball is
(A) 0.30  (B) 0.40  (C) 0.50  (D) 0.20

**Q107.** The law of total probability for a partition {Bᵢ} states P(A) =
(A) Σ P(A|Bᵢ)·P(Bᵢ)  (B) Π P(A|Bᵢ)  (C) P(A)·P(B)  (D) max P(A|Bᵢ)

**Q108.** In Bayesian terms, the posterior equals
(A) (likelihood × prior) / evidence  (B) the likelihood only  (C) the prior only  (D) evidence / prior

**Q109.** A box has 2 fair coins and 1 two-headed coin. One coin is chosen at random and flipped, landing heads. P(it was the two-headed coin) is
(A) 1/2  (B) 1/3  (C) 2/3  (D) 1

**Q110.** In the medical-test problem, the posterior probability is surprisingly low mainly because
(A) the test is poorly designed  (B) the disease is rare (base-rate effect)  (C) the sensitivity is low  (D) the sample is small

---

## Part K — Random variables, expectation & variance

**Q111.** For a discrete random variable with PMF p(x), the probabilities satisfy
(A) Σ p(x) = 0  (B) Σ p(x) = 1  (C) Σ p(x) = ∞  (D) Σ p(x) = n

**Q112.** For a continuous random variable, the probability P(X = a) at any single point a is
(A) 1  (B) 0  (C) f(a)  (D) 0.5

**Q113.** The cumulative distribution function is defined as
(A) F(x) = P(X ≤ x), non-decreasing  (B) F(x) = P(X = x)  (C) F(x) = P(X ≥ x)  (D) F(x) = f(x)/x

**Q114.** For a discrete random variable, E[X] equals
(A) Σ x  (B) Σ x·p(x)  (C) Σ p(x)  (D) Σ x²·p(x)

**Q115.** The variance of X is most conveniently computed as
(A) E[X²] − (E[X])²  (B) (E[X])² − E[X²]  (C) E[X²] + (E[X])²  (D) E[X] − E[X²]

**Q116.** For constants a and b, E[aX + b] equals
(A) a·E[X]  (B) a·E[X] + b  (C) a·E[X] + b²  (D) E[X] + b

**Q117.** For constants a and b, Var(aX + b) equals
(A) a·Var(X)  (B) a·Var(X) + b  (C) a²·Var(X)  (D) a²·Var(X) + b²

**Q118.** If E[X] = 5, then E[3X + 2] is
(A) 15  (B) 17  (C) 5  (D) 7

**Q119.** If Var(X) = 4, then Var(3X + 2) is
(A) 12  (B) 14  (C) 36  (D) 38

**Q120.** If Var(X) = 4, then the standard deviation of (3X + 2) is
(A) 2  (B) 6  (C) 12  (D) 36

**Q121.** E[X + Y] equals E[X] + E[Y]
(A) always, even if X and Y are dependent  (B) only if X and Y are independent  (C) only if X and Y are disjoint  (D) never

**Q122.** Var(X + Y) = Var(X) + Var(Y) holds
(A) always  (B) only if X and Y are independent  (C) never  (D) only if X and Y are dependent

**Q123.** The expected value of a single roll of a fair die is
(A) 3  (B) 3.5  (C) 4  (D) 6

---

## Part L — The five named distributions

**Q124.** For a binomial distribution B(n, p), the mean is
(A) np  (B) np(1 − p)  (C) p  (D) n

**Q125.** For a binomial distribution B(n, p), the variance is
(A) np  (B) np(1 − p)  (C) λ  (D) p

**Q126.** For B(10, 0.5), the mean and variance are respectively
(A) 5 and 5  (B) 5 and 2.5  (C) 10 and 5  (D) 5 and 10

**Q127.** The probability of exactly 3 heads in 5 tosses of a fair coin is
(A) 0.3125  (B) 0.5  (C) 0.25  (D) 0.1

**Q128.** For a Poisson distribution with parameter λ, the mean and variance are
(A) λ and λ²  (B) λ and λ  (C) λ² and λ  (D) λ and √λ

**Q129.** Calls arrive at λ = 4 per hour (Poisson). P(exactly 2 calls in an hour) is about
(A) 0.1465  (B) 0.018  (C) 0.27  (D) 0.5

**Q130.** For a Poisson process with λ = 3, the probability of zero events is about
(A) 0.0498  (B) 0.15  (C) 0.333  (D) 0.20

**Q131.** The Poisson distribution approximates the binomial when
(A) n is small and p is large  (B) n is large and p is small, with λ = np  (C) always  (D) never

**Q132.** For an exponential distribution with rate λ, the mean is
(A) λ  (B) 1/λ  (C) λ²  (D) 1/λ²

**Q133.** For an exponential distribution with rate λ, the variance is
(A) 1/λ  (B) 1/λ²  (C) λ  (D) λ²

**Q134.** If calls arrive at λ = 0.5 per hour, the mean waiting time between calls is
(A) 0.5 h  (B) 2 h  (C) 1 h  (D) 4 h

**Q135.** Which named distribution is memoryless?
(A) normal  (B) exponential  (C) uniform  (D) binomial

**Q136.** For a uniform distribution U(a, b), the mean is
(A) (a + b)/2  (B) (b − a)/2  (C) ab  (D) a + b

**Q137.** The variance of U(0, 10) is
(A) 8.33  (B) 5  (C) 10  (D) 100

**Q138.** The mean of U(2, 8) is
(A) 4  (B) 5  (C) 3  (D) 6

**Q139.** For a normal distribution, the mean, median and mode are
(A) all equal  (B) mean > median > mode  (C) mode is largest  (D) all different

**Q140.** For a normal distribution, approximately what percentage of values lie within one standard deviation of the mean?
(A) 50%  (B) 68%  (C) 95%  (D) 99.7%

**Q141.** Marks are distributed as N(60, 10²). Approximately 95% of students score between
(A) 50 and 70  (B) 40 and 80  (C) 30 and 90  (D) 55 and 65

**Q142.** The Central Limit Theorem states that the sum (or mean) of many independent random variables tends to a
(A) normal distribution, regardless of the original distribution  (B) Poisson distribution  (C) normal distribution only if the originals are normal  (D) uniform distribution

---

## Part M — Descriptive statistics & correlation

**Q143.** For the data set 2, 3, 3, 5, 7 the mean, median and mode are respectively
(A) 4, 3, 3  (B) 3, 4, 3  (C) 4, 5, 3  (D) 4, 3, 5

**Q144.** Which measure of central tendency is most robust to outliers?
(A) mean  (B) median  (C) range  (D) standard deviation

**Q145.** The mean of the data set 1, 2, 3, 4, 100 is
(A) 3  (B) 22  (C) 11  (D) 20

**Q146.** The median of the data set 4, 7, 9, 12 is
(A) 7  (B) 8  (C) 9  (D) 9.5

**Q147.** For a moderately skewed distribution with mean 30 and median 32, the mode (by the empirical relation) is about
(A) 34  (B) 36  (C) 28  (D) 30

**Q148.** In a positively (right) skewed distribution,
(A) mean > median > mode  (B) mean < median < mode  (C) all are equal  (D) mode > mean

**Q149.** The population variance of 2, 4, 4, 4, 5, 5, 7, 9 is
(A) 4  (B) 4.57  (C) 2  (D) 32

**Q150.** The sample variance divides the sum of squared deviations by
(A) n  (B) n − 1  (C) n + 1  (D) N

**Q151.** If a constant is added to every value in a data set, the standard deviation
(A) increases  (B) is unchanged  (C) increases by the constant  (D) doubles

**Q152.** If every value in a data set is multiplied by k, the variance is
(A) multiplied by k  (B) multiplied by k²  (C) unchanged  (D) divided by k

**Q153.** The standard deviation is preferred over the variance for reporting because it is
(A) in squared units  (B) in the same units as the data  (C) unitless  (D) always a percentage

**Q154.** The range of a data set is
(A) max − min  (B) max + min  (C) the mean  (D) Q3 − Q1

**Q155.** Which measure is most sensitive to outliers?
(A) median  (B) mode  (C) mean  (D) IQR

**Q156.** The correlation coefficient r always lies in the interval
(A) [0, 1]  (B) [−1, 1]  (C) [−∞, ∞]  (D) [0, ∞]

**Q157.** Which statement is correct?
(A) Correlation implies causation  (B) Correlation does not imply causation  (C) Correlation and causation are identical  (D) Causation is unrelated to data

**Q158.** A correlation coefficient r = 0 means there is
(A) no relationship at all  (B) no *linear* relationship (a non-linear one may still exist)  (C) a perfect relationship  (D) causation

---

## Part N — Paper-I (English, Reasoning, GK)

**Q159.** Choose the word most nearly similar in meaning to **PRUDENT**.
(A) Reckless  (B) Wise and cautious  (C) Wealthy  (D) Talkative

**Q160.** Fill in the blank: *"The committee is divided ___ its opinion on the matter."*
(A) on  (B) in  (C) at  (D) from

**Q161.** If 5 × 4 = 15, 7 × 6 = 35 and 9 × 8 = 63, then 11 × 10 = ?
(A) 88  (B) 99  (C) 100  (D) 110

**Q162.** The ratio of the ages of A and B is 3 : 5. After 10 years it becomes 5 : 7. The present age of A is
(A) 12 years  (B) 15 years  (C) 18 years  (D) 20 years

**Q163.** Tripura shares an international border with which country?
(A) Myanmar  (B) Bangladesh  (C) China  (D) Bhutan

**Q164.** Choose the word most nearly **opposite** in meaning to **BENEVOLENT**.
(A) Kind  (B) Generous  (C) Malevolent  (D) Gentle

**Q165.** Doctor : Hospital :: Teacher : ?
(A) Student  (B) School  (C) Book  (D) Class

**Q166.** Find the next term: 2, 6, 12, 20, 30, ?
(A) 36  (B) 40  (C) 42  (D) 44

**Q167.** The capital of Tripura is
(A) Aizawl  (B) Agartala  (C) Shillong  (D) Imphal

**Q168.** The average of the first five natural numbers (1 to 5) is
(A) 2.5  (B) 3  (C) 3.5  (D) 4

**Q169.** In a code each letter is replaced by the previous letter of the alphabet (A→Z rule notwithstanding, B→A, I→H, etc.). How is **BIRD** written?
(A) AHQC  (B) CJSE  (C) AHQD  (D) AGQC

**Q170.** Pointing to a man, a woman says, "His mother is the only daughter of my mother." How is the woman related to the man?
(A) Sister  (B) Mother  (C) Aunt  (D) Grandmother

**Q171.** Choose the synonym of **ABUNDANT**.
(A) Scarce  (B) Plentiful  (C) Rare  (D) Empty

**Q172.** Which is the longest river flowing within India?
(A) Ganga  (B) Brahmaputra  (C) Godavari  (D) Yamuna

**Q173.** The simple interest on ₹1000 at 10% per annum for 2 years is
(A) ₹100  (B) ₹200  (C) ₹210  (D) ₹220

---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | A | 30 | C | 59 | B | 88 | B | 117 | C | 146 | B |
| 2 | B | 31 | C | 60 | A | 89 | B | 118 | B | 147 | B |
| 3 | B | 32 | B | 61 | C | 90 | C | 119 | C | 148 | A |
| 4 | A | 33 | B | 62 | C | 91 | A | 120 | B | 149 | A |
| 5 | C | 34 | B | 63 | C | 92 | A | 121 | A | 150 | B |
| 6 | B | 35 | B | 64 | B | 93 | B | 122 | B | 151 | B |
| 7 | B | 36 | C | 65 | B | 94 | A | 123 | B | 152 | B |
| 8 | C | 37 | B | 66 | C | 95 | B | 124 | A | 153 | B |
| 9 | B | 38 | C | 67 | B | 96 | B | 125 | B | 154 | A |
| 10 | B | 39 | C | 68 | C | 97 | C | 126 | B | 155 | C |
| 11 | A | 40 | B | 69 | C | 98 | A | 127 | A | 156 | B |
| 12 | B | 41 | B | 70 | B | 99 | B | 128 | B | 157 | B |
| 13 | A | 42 | C | 71 | B | 100 | A | 129 | A | 158 | B |
| 14 | C | 43 | B | 72 | B | 101 | A | 130 | A | 159 | B |
| 15 | B | 44 | B | 73 | C | 102 | B | 131 | B | 160 | B |
| 16 | B | 45 | B | 74 | B | 103 | B | 132 | B | 161 | B |
| 17 | B | 46 | B | 75 | B | 104 | C | 133 | B | 162 | B |
| 18 | B | 47 | B | 76 | B | 105 | B | 134 | B | 163 | B |
| 19 | B | 48 | A | 77 | B | 106 | B | 135 | B | 164 | C |
| 20 | A | 49 | C | 78 | A | 107 | A | 136 | A | 165 | B |
| 21 | C | 50 | C | 79 | B | 108 | A | 137 | A | 166 | C |
| 22 | B | 51 | B | 80 | B | 109 | A | 138 | B | 167 | B |
| 23 | A | 52 | B | 81 | C | 110 | B | 139 | A | 168 | B |
| 24 | B | 53 | B | 82 | A | 111 | B | 140 | B | 169 | A |
| 25 | B | 54 | B | 83 | A | 112 | B | 141 | B | 170 | B |
| 26 | B | 55 | A | 84 | B | 113 | A | 142 | A | 171 | B |
| 27 | C | 56 | A | 85 | C | 114 | B | 143 | A | 172 | A |
| 28 | B | 57 | B | 86 | C | 115 | A | 144 | B | 173 | B |
| 29 | C | 58 | A | 87 | C | 116 | B | 145 | B | | |

---

# 📝 Detailed Solutions

**Q1. (A)** The Wiener–Khinchin theorem: the PSD is the Fourier transform of the autocorrelation function — the fundamental time↔frequency link for random signals.

**Q2. (B)** R_X(0) = E[X²] is the average power, and it is the maximum value of the autocorrelation.

**Q3. (B)** Autocorrelation is even, R_X(τ) = R_X(−τ), with |R_X(τ)| ≤ R_X(0), so its peak is at τ = 0.

**Q4. (A)** White noise has a flat (constant) PSD, S(f) = N₀/2, over all frequencies — by analogy with white light.

**Q5. (C)** The Fourier transform of a constant is an impulse, so white noise has autocorrelation (N₀/2)·δ(τ): samples at distinct instants are uncorrelated.

**Q6. (B)** "White" describes the spectrum (flat PSD), not the amplitude distribution.

**Q7. (B)** White (flat spectrum) and Gaussian (amplitude distribution) are independent properties; a process can be white without being Gaussian.

**Q8. (C)** Output PSD = |H(f)|²·S_X(f). Power scales with amplitude squared, hence |H(f)|² — a common trap is using |H(f)|.

**Q9. (B)** Output power = ∫₋ᵦ⁺ᵦ (N₀/2) df = (N₀/2)(2B) = **N₀B**.

**Q10. (B)** Thermal noise power N = kTB (k = 1.38×10⁻²³ J/K).

**Q11. (A)** By Friis, F = F₁ + (F₂−1)/G₁ + …, so the first stage dominates — hence the LNA is placed first.

**Q12. (B)** AM produces upper and lower sidebands, each of width f_m → total **2f_m**.

**Q13. (A)** DSB-SC keeps both sidebands → 2f_m; SSB transmits one → f_m.

**Q14. (C)** Suppressing the carrier saves power, not bandwidth: DSB-SC is still 2f_m; only SSB halves it to f_m.

**Q15. (B)** P_total = P_c(1 + μ²/2): carrier power plus μ²/2·P_c in the sidebands.

**Q16. (B)** Efficiency η = μ²/(2 + μ²), the fraction of total power in the sidebands.

**Q17. (B)** At μ = 1: P_total = 1.5 P_c, sideband power = 0.5 P_c → 0.5/1.5 = **33.3%**.

**Q18. (B)** μ = (A_max − A_min)/(A_max + A_min) = (15 − 5)/(15 + 5) = 10/20 = **0.5**.

**Q19. (B)** μ > 1 is overmodulation: the envelope distorts and inverts, and the envelope detector fails.

**Q20. (A)** P_total = P_c(1 + μ²/2) = 100(1 + 0.36/2) = 100(1 + 0.18) = **118 W**.

**Q21. (C)** η = μ²/(2 + μ²) = 0.25/2.25 = **11.1%**.

**Q22. (B)** DSB-SC (and SSB) have no transmitted carrier, so they need coherent detection; AM (DSB-FC) uses a simple envelope detector.

**Q23. (A)** Standard AM broadcast IF = **455 kHz**.

**Q24. (B)** Standard FM broadcast IF = **10.7 MHz**.

**Q25. (B)** Image frequency = f_signal + 2·f_IF; both the wanted and image frequencies mix down to the IF.

**Q26. (B)** f_image = 1000 + 2(455) = **1910 kHz** (check: 1910 − f_LO = 1910 − 1455 = 455 ✅).

**Q27. (C)** Once mixed, the image lands exactly on the IF and is indistinguishable, so it must be rejected by the RF stage before the mixer.

**Q28. (B)** FM modulation index β = Δf/f_m.

**Q29. (C)** Carson's rule: BW = 2(Δf + f_m).

**Q30. (C)** BW = 2(75 + 15) = 2(90) = **180 kHz** (FM broadcast; 200 kHz is allocated with guard band).

**Q31. (C)** BW = 2(10 + 5) = **30 kHz** (β = Δf/f_m = 2).

**Q32. (B)** FM total transmitted power is constant; modulation only redistributes it among carrier and Bessel sidebands.

**Q33. (B)** FM has better noise immunity (amplitude limiting) at the cost of much wider bandwidth.

**Q34. (B)** The PM index β_PM = k_p·A_m is independent of f_m — a key FM/PM distinction.

**Q35. (B)** For wideband FM, BW ≈ 2Δf (Carson's rule with β ≫ 1).

**Q36. (C)** I = −log₂ p = −log₂(1/8) = log₂ 8 = **3 bits**.

**Q37. (B)** Entropy H(X) = −Σ pᵢ log₂ pᵢ bits/symbol.

**Q38. (C)** H_max = log₂ M = log₂ 8 = **3 bits/symbol** (equally likely symbols).

**Q39. (C)** H = −(0.5 log₂0.5 + 0.5 log₂0.5) = 0.5 + 0.5 = **1 bit** — the maximum for two symbols.

**Q40. (B)** H = 0.5(1) + 0.25(2) + 0.125(3) + 0.125(3) = 0.5 + 0.5 + 0.375 + 0.375 = **1.75 bits/symbol**.

**Q41. (B)** C = B log₂(1 + S/N) = 3000 log₂(1 + 3) = 3000 × 2 = **6000 bps**.

**Q42. (C)** C = 4000 log₂(1 + 255) = 4000 log₂256 = 4000 × 8 = **32000 bps**.

**Q43. (B)** Nyquist: C = 2B log₂ L = 2(3000) log₂16 = 6000 × 4 = **24000 bps**.

**Q44. (B)** I(X;Y) = 0 iff X and Y are independent — the output tells nothing about the input.

**Q45. (B)** By the source-coding theorem, average codeword length ≥ H(X); you cannot compress below the entropy.

**Q46. (B)** Nyquist sampling rate: f_s ≥ 2f_m.

**Q47. (B)** 4 kHz speech → f_s = **8 kHz** (telephony standard).

**Q48. (A)** Sampling below the Nyquist rate causes aliasing.

**Q49. (C)** n = log₂ L = log₂ 256 = **8 bits/sample**.

**Q50. (C)** Bit rate = f_s × n = 8000 × 8 = **64 kbps** (the standard voice channel).

**Q51. (B)** SNR = 6.02n + 1.76 = 6.02(8) + 1.76 = **49.9 dB**.

**Q52. (B)** Each extra bit adds 6.02 dB ≈ **6 dB** of SNR.

**Q53. (B)** Quantisation noise power = Δ²/12.

**Q54. (B)** DPCM encodes the difference between the sample and a predicted value, needing fewer bits.

**Q55. (A)** Delta modulation is 1-bit DPCM: **1 bit/sample** (up or down).

**Q56. (A)** Slope overload: the step size is too small for a fast-changing signal, so the staircase lags.

**Q57. (B)** Granular noise: the step size is too large for a slowly varying signal, causing up-down hunting. (These two errors conflict — hence ADM.)

**Q58. (A)** μ-law (μ = 255, North America/Japan) and A-law (A = 87.6, Europe/India).

**Q59. (B)** 44,100 × 16 × 2 = 1,411,200 ≈ **1.41 Mbps**.

**Q60. (A)** ASK varies amplitude — exactly what noise attacks — so it has the worst noise performance.

**Q61. (C)** BPSK (0°/180°) has diametrically opposite symbols, the best noise performance of the binary schemes.

**Q62. (C)** QAM uses both amplitude and phase, packing the most bits/symbol — most bandwidth-efficient.

**Q63. (C)** Bit rate = baud × log₂ M = 2400 × log₂16 = 2400 × 4 = **9600 bps**.

**Q64. (B)** QPSK: 1000 × log₂4 = 1000 × 2 = **2000 bps**.

**Q65. (B)** 64-QAM: 1×10⁶ × log₂64 = 1×10⁶ × 6 = **6 Mbps**.

**Q66. (C)** Baud = bit rate / log₂ M = 9600 / log₂8 = 9600/3 = **3200 baud**.

**Q67. (B)** Matched-filter maximum output SNR = 2E/N₀, where E is the pulse energy.

**Q68. (C)** The matched filter maximises SNR but does NOT remove ISI (that is the equaliser's job) — a favourite trap.

**Q69. (C)** Matched-filter impulse response is the time-reversed, delayed pulse: h(t) = s(T − t).

**Q70. (B)** MAP maximises P(sent|received) using prior probabilities; ML maximises P(received|sent) and ignores priors.

**Q71. (B)** When all symbols are equally likely the priors cancel, so MAP reduces to ML.

**Q72. (B)** BPSK's P_e = Q(√(2E_b/N₀)) vs BFSK's Q(√(E_b/N₀)): BPSK needs 3 dB less power for the same BER.

**Q73. (C)** QAM varies amplitude and phase together.

**Q74. (B)** ISI is adjacent symbols smearing into each other's sampling instants, causing errors even without noise.

**Q75. (B)** Raised-cosine BW = (1 + α)·R_s/2 = (1.5)(1×10⁶/2) = 1.5 × 0.5 = **0.75 MHz**.

**Q76. (B)** An equaliser inverts the channel distortion to remove ISI.

**Q77. (B)** A wide-open eye means little ISI and good noise/timing margins; a closing eye signals ISI and jitter.

**Q78. (A)** Hamming bound: 2ʳ ≥ m + r + 1 (r parity bits must index all positions plus the no-error case).

**Q79. (B)** m = 4 → r = 3 (2³ = 8 ≥ 4 + 3 + 1 = 8 ✅) → the **(7,4)** code.

**Q80. (B)** d_min = 3 → corrects ⌊(3−1)/2⌋ = 1 error and detects 3 − 1 = 2 errors.

**Q81. (C)** To correct d errors: d_min ≥ 2d + 1 (to detect d: d_min ≥ d + 1).

**Q82. (A)** Convolutional codes are decoded by the Viterbi algorithm (an ML decoder).

**Q83. (A)** FDMA = different frequency band; TDMA = different time slot; CDMA = orthogonal code over the full bandwidth.

**Q84. (B)** Processing gain = chip rate / bit rate.

**Q85. (C)** Manchester coding has a mid-bit transition, making it self-clocking.

**Q86. (C)** Reed–Solomon corrects burst errors (CDs, DVDs, QR codes, deep-space links).

**Q87. (C)** P(A ∪ B) = P(A) + P(B) − P(A ∩ B); the overlap is subtracted once because it was counted twice.

**Q88. (B)** Independence: P(A ∩ B) = P(A)·P(B), equivalently P(A|B) = P(A).

**Q89. (B)** Mutually exclusive means they cannot occur together: P(A ∩ B) = 0.

**Q90. (C)** Independent ≠ mutually exclusive. For non-zero probabilities, mutually exclusive events are dependent (if A occurs, B certainly did not).

**Q91. (A)** P(A|B) = P(A ∩ B)/P(B), for P(B) > 0.

**Q92. (A)** P(A′) = 1 − P(A).

**Q93. (B)** P(A ∩ B) = 0.3 × 0.4 = 0.12; P(A ∪ B) = 0.3 + 0.4 − 0.12 = **0.58**.

**Q94. (A)** Sum = 7: (1,6),(2,5),(3,4),(4,3),(5,2),(6,1) = 6/36 = **1/6**.

**Q95. (B)** Even faces {2,4,6} → 3/6 = **1/2**.

**Q96. (B)** 4 kings / 52 = **1/13**.

**Q97. (C)** ⁿPᵣ counts ordered arrangements (order matters); ⁿCᵣ counts selections (order does not).

**Q98. (A)** ¹⁰C₃ = 10!/(3!·7!) = 120.

**Q99. (B)** Without replacement: (3/5)(2/4) = 6/20 = **3/10**.

**Q100. (A)** With replacement: (3/5)(3/5) = **9/25**.

**Q101. (A)** Bayes: P(Bᵢ|A) = P(A|Bᵢ)P(Bᵢ) / Σⱼ P(A|Bⱼ)P(Bⱼ) — posterior = (likelihood × prior)/evidence.

**Q102. (B)** Via A: 0.6×0.02 = 0.012; via B: 0.4×0.05 = 0.020; total 0.032. P(A|D) = 0.012/0.032 = **0.375**.

**Q103. (B)** Via D: 0.01×0.99 = 0.0099; via no-D: 0.99×0.05 = 0.0495; total 0.0594. P(D|+) = 0.0099/0.0594 ≈ **0.167** (base-rate neglect).

**Q104. (C)** Via Bag 1: 0.5×3/5 = 0.30; via Bag 2: 0.5×1/5 = 0.10; total 0.40. P(Bag1|red) = 0.30/0.40 = **0.75**.

**Q105. (B)** Paths: 0.5×0.03 = 0.015; 0.3×0.04 = 0.012; 0.2×0.05 = 0.010; total 0.037. P(M3|D) = 0.010/0.037 ≈ **0.270**.

**Q106. (B)** Total probability P(red) = 0.30 + 0.10 = **0.40** (the denominator in Q104).

**Q107. (A)** Law of total probability: P(A) = Σ P(A|Bᵢ)·P(Bᵢ).

**Q108. (A)** Posterior = (likelihood × prior) / evidence, the evidence being the sum over all paths.

**Q109. (A)** P(H) = (2/3)(0.5) + (1/3)(1) = 1/3 + 1/3 = 2/3; P(2-headed|H) = (1/3)/(2/3) = **1/2**.

**Q110. (B)** The disease is rare, so the many false positives from the large healthy group swamp the true positives — base-rate effect.

**Q111. (B)** A valid PMF sums to 1: Σ p(x) = 1.

**Q112. (B)** For a continuous RV, P(X = a) = 0; only intervals carry probability.

**Q113. (A)** CDF F(x) = P(X ≤ x) is non-decreasing, with F(−∞) = 0, F(∞) = 1.

**Q114. (B)** E[X] = Σ x·p(x).

**Q115. (A)** Var(X) = E[X²] − (E[X])² — the computational form.

**Q116. (B)** E[aX + b] = a·E[X] + b.

**Q117. (C)** Var(aX + b) = a²·Var(X): the constant b vanishes and a is squared.

**Q118. (B)** E[3X + 2] = 3(5) + 2 = **17**.

**Q119. (C)** Var(3X + 2) = 3²·4 = **36** (the +2 has no effect).

**Q120. (B)** σ = √36 = **6**.

**Q121. (A)** Linearity of expectation: E[X + Y] = E[X] + E[Y] always, even for dependent variables.

**Q122. (B)** Var(X + Y) = Var(X) + Var(Y) only if X and Y are independent.

**Q123. (B)** E[X] = (1+2+3+4+5+6)/6 = 21/6 = **3.5**.

**Q124. (A)** Binomial mean = np.

**Q125. (B)** Binomial variance = np(1 − p), always less than the mean np.

**Q126. (B)** Mean = 10×0.5 = 5; variance = 10×0.5×0.5 = **2.5**.

**Q127. (A)** ⁵C₃(0.5)³(0.5)² = 10 × 1/32 = 10/32 = **0.3125**.

**Q128. (B)** Poisson's signature: mean = variance = λ.

**Q129. (A)** P(2) = e⁻⁴·4²/2! = e⁻⁴·8 ≈ 0.0183 × 8 = **0.1465**.

**Q130. (A)** P(0) = e⁻³ ≈ **0.0498**.

**Q131. (B)** Poisson approximates binomial when n is large and p is small, with λ = np.

**Q132. (B)** Exponential mean = 1/λ.

**Q133. (B)** Exponential variance = 1/λ².

**Q134. (B)** Mean waiting time = 1/λ = 1/0.5 = **2 h**.

**Q135. (B)** The exponential (and, discretely, the geometric) is memoryless.

**Q136. (A)** Uniform mean = (a + b)/2.

**Q137. (A)** Var = (b − a)²/12 = 100/12 = **8.33**.

**Q138. (B)** Mean = (2 + 8)/2 = **5**.

**Q139. (A)** By symmetry, a normal distribution has mean = median = mode.

**Q140. (B)** Empirical rule: ~**68%** within 1σ (95% within 2σ, 99.7% within 3σ).

**Q141. (B)** 95% within 2σ = 60 ± 20 → **40 to 80**.

**Q142. (A)** CLT: sums/means of many independent RVs tend to normal regardless of the original distribution.

**Q143. (A)** Mean = 20/5 = 4; median = 3; mode = 3.

**Q144. (B)** The median is robust to outliers.

**Q145. (B)** Mean = 110/5 = **22** (dragged up by the 100; the median would stay at 3).

**Q146. (B)** Median = (7 + 9)/2 = **8**.

**Q147. (B)** Mode ≈ 3·median − 2·mean = 3(32) − 2(30) = 96 − 60 = **36**.

**Q148. (A)** Right (positive) skew: mean > median > mode.

**Q149. (A)** Mean = 40/8 = 5; squared deviations sum = 9+1+1+1+0+0+4+16 = 32; population variance = 32/8 = **4** (σ = 2).

**Q150. (B)** Sample variance divides by n − 1 (Bessel's correction); population by N.

**Q151. (B)** Adding a constant shifts the mean but leaves the SD unchanged.

**Q152. (B)** Multiplying by k scales the variance by k² (SD by |k|).

**Q153. (B)** The SD is in the same units as the data, unlike variance (squared units).

**Q154. (A)** Range = max − min.

**Q155. (C)** The mean uses every value, so it is most sensitive to outliers.

**Q156. (B)** r ∈ [−1, +1].

**Q157. (B)** Correlation does not imply causation.

**Q158. (B)** r = 0 means no *linear* relationship; a non-linear one (e.g. a parabola) may still exist.

**Q159. (B)** *Prudent* = acting with care and forethought → **wise and cautious**.

**Q160. (B)** The standard collocation is "divided **in** its opinion".

**Q161. (B)** Rule a×b − a: 20 − 5 = 15; 42 − 7 = 35; 72 − 9 = 63; so 110 − 11 = **99**.

**Q162. (B)** Let ages be 3x, 5x. (3x+10)/(5x+10) = 5/7 → 21x + 70 = 25x + 50 → 4x = 20 → x = 5. A = 3×5 = **15**.

**Q163. (B)** Tripura is bordered on three sides by **Bangladesh** (~856 km); domestically only by Assam and Mizoram.

**Q164. (C)** The opposite of benevolent (kindly) is **malevolent** (wishing harm).

**Q165. (B)** A doctor works in a hospital as a teacher works in a **school**.

**Q166. (C)** Differences 4, 6, 8, 10, **12** → 30 + 12 = **42** (pattern n(n+1): 2,6,12,20,30,42).

**Q167. (B)** The capital of Tripura is **Agartala**.

**Q168. (B)** (1+2+3+4+5)/5 = 15/5 = **3**.

**Q169. (A)** Each letter → previous: B→A, I→H, R→Q, D→C → **AHQC**.

**Q170. (B)** "The only daughter of my mother" is the woman herself, so his mother is the woman → she is his **mother**.

**Q171. (B)** *Abundant* = existing in large quantity → **plentiful**.

**Q172. (A)** The **Ganga** is the longest river flowing within India (~2525 km).

**Q173. (B)** SI = PRT/100 = 1000×10×2/100 = **₹200**.
