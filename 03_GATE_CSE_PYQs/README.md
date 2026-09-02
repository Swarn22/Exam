# GATE Computer Science — Previous Year Questions

Two complete views of the GATE CSE archive:

- **`Year_wise/`** — the actual question papers, one PDF per year/set, **2000 → 2026 (27 years)**, with official answer keys
- **`Subject_wise/`** — every GATE CSE question since **1987**, split into one PDF per subject, folders named to match the TPSC syllabus sections

---

## `Year_wise/` — 42 official papers, 2000–2026

`Year_wise/Question_Papers/` (42 files) · `Year_wise/Answer_Keys/` (26 files, covering 2011–2026)

| Year | Sets | Year | Sets |
|---|---|---|---|
| 2026 | CS-1, CS-2 | 2012 | 1 |
| 2025 | Set 1, Set 2 | 2011 | 1 |
| 2024 | Set 1, Set 2 | 2010 | 1 |
| 2023 | 1 | 2009 | 1 |
| 2022 | 1 | 2008 | CS, IT |
| 2021 | Set 1, Set 2 | 2007 | CS, IT |
| 2020 | 1 | 2006 | CS, IT |
| 2019 | 1 | 2005 | CS, IT |
| 2018 | 1 | 2004 | CS, IT |
| 2017 | Set 1, Set 2 | 2003 | 1 |
| 2016 | Set 1, Set 2 | 2002 | 1 |
| 2015 | Set 1, 2, 3 | 2001 | 1 |
| 2014 | Set 1, 2, 3 | 2000 | 1 |
| 2013 | 1 | | |

**GATE 2026 CS-1 and CS-2 are the official IIT Guwahati master question papers and final answer keys** (`gate2026.iitg.ac.in`). Papers for 2000–2025 are the standard official papers with their official keys where released.

The separate **CS and IT papers for 2004–2008** are both included. The old GATE-IT papers are worth attempting: they lean towards networks, databases, software engineering and web/IT topics — **closer to the TPSC ATO syllabus than GATE-CS is**.

---

## `Subject_wise/` — split by TPSC syllabus section

Each PDF contains every GATE CSE question on that subject since 1987, **with worked solutions and answer keys**, plus topic-wise key concepts and formula references.

### Paper-I equivalents

| Folder | Questions |
|---|---|
| `Paper1_01_English_Verbal` | 165 |
| `Paper1_02_Reasoning_and_Mental_Ability` | 264 (analytical 48 · quantitative 197 · spatial 19) |

### Paper-II

| Folder | Questions | Study week |
|---|---|---|
| `Paper2_S01_Probability_and_Statistics` | 125 | 9 |
| `Paper2_S02_Digital_Logic` | 313 | 1 |
| `Paper2_S03_Computer_Organization_and_Architecture` | 251 | 2 |
| `Paper2_S05_Data_Structures_and_Programming` | 370 (DS 238 · C 131 · misc 1) | 3–4 |
| `Paper2_S06_Algorithms` | 358 | 5 |
| `Paper2_S07_Compiler_Design` | 242 | 11 |
| `Paper2_S08_Operating_System` | 343 | 6 |
| `Paper2_S09_Databases` | 302 | 7 |
| `Paper2_S11_Computer_Networks` | 226 | 8 |
| **Total in-syllabus** | **~2,530** | |

### ⚠ No GATE folder exists for these TPSC sections

§4 Analog & Digital Communication · §10 Information Systems & Software Engineering · §12 Web Technologies · §13 Cyber Security & Emerging Tech · §14 Cloud Technology

That is **~31 marks (26% of Paper-II)** with zero GATE coverage. Use `02_State_PSC_PYQs/Subject_wise/` for those — it is the reason that folder exists.

### `ZZ_Outside_TPSC_Syllabus_optional/` — skip these

| Chapter | Questions | Why skip |
|---|---|---|
| Theory of Computation | 293 | Not in Annexure-C at all |
| Discrete Maths — Set Theory & Algebra | 173 | Engineering Maths is limited to Probability & Statistics |
| Discrete Maths — Graph Theory | 88 | Same (graph *terminology* is covered under DS/Algorithms) |
| Discrete Maths — Mathematical Logic | 78 | Same |
| Discrete Maths — Combinatory | 51 | Same (basic counting is covered under Probability) |
| Engineering Maths — Linear Algebra | 112 | Same |
| Engineering Maths — Calculus | 69 | Same |
| **Total avoided** | **864** | |

Skipping these is roughly **a quarter of the entire GATE CSE archive**. Verify against Annexure-C yourself before committing — but the syllabus text is unambiguous: Engineering Mathematics consists of exactly one section, "Probability and Statistics".

---

## `_source_volumes/` — the unsplit originals

| File | Contents |
|---|---|
| `GO_GATE_CSE_Volume1.pdf` | Discrete maths, engineering maths, general aptitude |
| `GO_GATE_CSE_Volume2.pdf` | Algorithms, compiler design, data structures, programming, theory of computation |
| `GO_GATE_CSE_Volume3.pdf` | CO & architecture, computer networks, databases, digital logic, operating systems |
| `GO_Engineering_Mathematics_and_Aptitude.pdf` | Engineering maths + general aptitude across **all** GATE branches |
| `GO_Aptitude_All_Branches.pdf` | Every GATE general-aptitude question, all branches — a large extra pool for Paper-I |

Keep these: the split files preserve each chapter's own answer key, but the source volumes retain the full table of contents and cross-references.

**`GO_Aptitude_All_Branches.pdf` is under-rated for this exam.** Paper-I's reasoning and quantitative section is 15 marks, and this file holds thousands of aptitude questions drawn from every GATE paper — far more than the CS-only pool.

---

## How to use this folder

1. **GATE is harder than your target exam.** GATE CSE questions are analytical and multi-step; TPSC ATO gives you ~65 seconds per question across 170 questions. Use GATE PYQs to build *depth*, then use `02_State_PSC_PYQs/` to calibrate to the *actual* speed and style.
2. **Do not attempt full GATE papers as mocks** — the pattern (65 questions, NAT questions, 100 marks) does not match TPSC's 170-question OMR MCQ format. Use them as question pools, and use `04_Mock_Tests/` for timed practice.
3. **Exception: the GATE-IT papers (2004–2008)** are worth attempting whole. Their emphasis on networks, DBMS, SE and IT topics is the closest GATE ever came to this syllabus.
4. **Every question here has a worked solution.** When you get one wrong, read the solution, then log it in `01_Study_Plan/Weekly_Progress_Tracker.md` — do not just check the answer.

---

## Sources

- [GATE 2026 official question papers & answer keys — IIT Guwahati](https://gate2026.iitg.ac.in/QPs-answer-keys.html)
- [GATE CSE/IT previous year papers archive — GeeksforGeeks](https://www.geeksforgeeks.org/gate/original-gate-previous-year-question-papers-cse-and-it-gq/)
- [GATE Overflow — GO-PDFs releases (subject-wise volumes with solutions)](https://github.com/GATEOverflow/GO-PDFs/releases)
- [GATE Overflow — previous years' questions](https://gateoverflow.in/previous-years)

*Compiled 01–02 Sep 2026. 2026 papers are official IIT Guwahati PDFs; earlier years are the standard official papers and keys. Subject-wise splits were generated from the GATE Overflow volumes by chapter bookmark, so page and answer-key integrity within each chapter is preserved.*
