# Full-Length Mock Blueprint — 170 marks / 180 minutes

Take these in **Week 12** (Mon / Wed / Fri). The weekly tests prove you know a subject; only a full-length attempt proves you can hold accuracy and pace across 170 questions and three hours.

---

## The blueprint

Assemble each mock to this exact composition. It mirrors the advertisement's fixed Paper-I split and the estimated Paper-II weightage.

### Paper-I — 50 questions

| Section | Q | Source folder |
|---|---|---|
| English composition | 15 | `*/Subject_wise/Paper1_01_English_Verbal/` |
| General mental ability & logical reasoning | 15 | `*/Subject_wise/Paper1_02_Reasoning_and_Mental_Ability/` and `03_GATE_CSE_PYQs/_source_volumes/GO_Aptitude_All_Branches.pdf` |
| General knowledge & current affairs | 20 | Your own Tripura GK + current-affairs compilation |

### Paper-II — 120 questions

| § | Section | Q | Source folder (either PYQ tree) |
|---|---|---|---|
| 1 | Probability & Statistics | 7 | `Paper2_S01_Probability_and_Statistics/` |
| 2 | Digital Logic | 9 | `Paper2_S02_Digital_Logic/` |
| 3 | Computer Organization & Architecture | 9 | `Paper2_S03_Computer_Organization_and_Architecture/` |
| 4 | Analog & Digital Communication | 8 | `Paper2_S04_Analog_and_Digital_Communication/` |
| 5 | Data Structures & Programming | 14 | `Paper2_S05_Data_Structures_and_Programming/` |
| 6 | Algorithms | 11 | `Paper2_S06_Algorithms/` |
| 7 | Compiler Design | 6 | `Paper2_S07_Compiler_Design/` |
| 8 | Operating System | 11 | `Paper2_S08_Operating_System/` |
| 9 | Databases | 11 | `Paper2_S09_Databases/` |
| 10 | Information Systems & Software Engineering | 8 | `Paper2_S10_Information_Systems_and_Software_Engineering/` |
| 11 | Computer Networks | 11 | `Paper2_S11_Computer_Networks/` |
| 12 | Web Technologies | 6 | `Paper2_S12_Web_Technologies/` |
| 13 | Cyber Security & Emerging Tech | 5 | `Paper2_S13_Cyber_Security_and_Emerging_Tech/` |
| 14 | Cloud Technology | 4 | `Paper2_S14_Cloud_Technology/` |
| | **Total** | **120** | |

---

## Assembling a mock (about 20 minutes)

1. For each section, open the folder and pick the required number of questions **without reading the solutions**. Write only the question numbers and their source file on a sheet — that is your paper.
2. **Weight the sources deliberately:**
   - **Mock A — state-PSC calibrated.** Draw ~75% from `02_State_PSC_PYQs/` (ISRO/NIELIT/UGC-NET). Closest to the real difficulty and pace.
   - **Mock B — mixed.** 50/50 between the two PYQ trees.
   - **Mock C — stress test.** ~65% from `03_GATE_CSE_PYQs/`. Harder than the real paper; if you clear the cut-offs here you have margin.
3. Prefer questions **you have not already seen** during the week's drilling. If you recognise one, replace it.
4. Sequence them **Paper-I first (1–50), then Paper-II (51–170)** — the real paper's order.

### Faster alternative for Mock A

Skip assembly entirely and use a real paper: **`02_State_PSC_PYQs/Papers/Kerala_PSC/KeralaPSC_2026_DeputyManagerIT_AssistantProgrammer_QP_050-2026.pdf`** (100 questions, official answer key included). Scale your timing to 1 hour 45 minutes. It is the closest existing analogue to an ATO (IT) paper, and it is a genuine, unseen exam.

---

## Rules for the attempt

Non-negotiable if the result is to mean anything:

- **180 minutes, one sitting.** No pauses, no lookups, no phone.
- **Use a real OMR-style answer sheet.** Draw a 170-row grid with four bubbles per row and darken them. Do not answer in the margin of the question — the whole point is to rehearse transcription.
- **Sit at a table**, not on a bed or sofa. Same time of day as the exam if it has been announced.
- **No calculator.** Nothing in the syllabus needs one.
- Keep a **rough sheet** and number your working by question — you will want it during review.

---

## Scoring

| | |
|---|---|
| Correct | +1 |
| Wrong | −1/3 |
| Unattempted | 0 |

Compute **three** numbers, not one:

```
Paper-I  net  = correct − (wrong / 3)          → must be ≥ 27.5  (UR) / 22.5 (SC/ST/PH)
Paper-II net  = correct − (wrong / 3)          → must be ≥ 66    (UR) / 54   (SC/ST/PH)
Accuracy      = correct / attempted × 100
```

**Both paper cut-offs must be cleared independently.** The advertisement sets the minimum *in each subject*, so a strong Paper-II cannot compensate for a weak Paper-I.

---

## Time strategy to rehearse

| Pass | What | Budget | Cumulative |
|---|---|---|---|
| 1 | Paper-I (Q1–50) — mostly recall, move fast | 40 min | 0:40 |
| 2 | Paper-II — every question answerable in under a minute; **flag and skip** the rest | 80 min | 2:00 |
| 3 | Flagged numericals (OS, CN, COA, DBMS) | 45 min | 2:45 |
| 4 | OMR verification + calculated guesses on eliminated-to-two questions | 15 min | 3:00 |

**Do not break this order.** The most common way to lose marks in a 170-question paper is spending eight minutes on a hard pipeline numerical in the first hour and running out of time for forty easy definitional questions in Sections 10–14.

**Guessing rule:** attempt if you can eliminate **at least two** options (expected value turns positive). Skip pure guesses — at −1/3, blind guessing across four options is break-even at best and adds variance you do not want near a hard cut-off.

---

## Review (2+ hours per mock — longer than the attempt)

1. Mark it, applying the penalty. Record all three numbers in the tracker.
2. **Section-wise breakdown.** Which of the 14 sections cost you the most marks in absolute terms? That is where Tuesday and Thursday go.
3. Split every wrong answer into `concept-gap` vs `silly error`. Concept gaps need re-study; silly errors need process changes (read the question twice, recheck the OMR row, redo the arithmetic).
4. **Check your unattempted questions.** If you skipped 30 questions and could actually have done 20 of them, your problem is pace, not knowledge — and pace is fixable in a week.
5. Log every wrong answer in the error log in `01_Study_Plan/Weekly_Progress_Tracker.md`.

---

## Reading the results

| Paper-II net | Reading |
|---|---|
| 85+ | Comfortably above the cut-off. Protect it — revise, don't cram new material. |
| 66–84 | Clearing UR, but with no margin. Target the two weakest sections. |
| 54–65 | Clears the reserved-category cut-off, not UR. Push the high-weightage sections (§5, §6, §8, §9, §11). |
| < 54 | Below both cut-offs. Prioritise the ~31 easy definitional marks in §4, §10, §12, §13, §14 — the fastest available gains. |

| Paper-I net | Reading |
|---|---|
| 35+ | Strong. Maintain the daily hour. |
| 27.5–34 | Clearing UR, thin margin. Almost always the GK block — expand the Tripura and current-affairs compilation. |
| < 27.5 | **The most urgent problem in your preparation**, regardless of how good Paper-II looks. |

---

## Progress log

| Mock | Date | Type | P-I net /50 | P-II net /120 | Total /170 | Accuracy | Attempted | Weakest 2 sections |
|---|---|---|---|---|---|---|---|---|
| A | | State-PSC calibrated | | | | | | |
| B | | Mixed | | | | | | |
| C | | GATE-weighted stress | | | | | | |

Expect Mock C to score lowest — it is deliberately harder than the real paper. What matters is the **trend in accuracy and in unattempted count** across the three.
