# Week 10 Mock Test — Web Technologies + Cloud + Cyber Security & Emerging Tech

**Syllabus §12, §14, §13** · 25 questions · **30 minutes** · +1 / −0.33

> These three sections are worth ~15 marks and are **purely definitional** — no numericals, no derivations. They are the cheapest marks in Paper-II and the ones a GATE-only preparation misses entirely.

---

## Part A — Web Technologies (Q1–Q7)

**Q1.** Which of the following is a **semantic** element introduced in HTML5?
(A) `<div>`  (B) `<span>`  (C) `<article>`  (D) `<b>`

**Q2.** In the CSS box model, the correct order of layers from the content outwards is
(A) content → border → padding → margin
(B) content → padding → border → margin
(C) content → margin → padding → border
(D) padding → content → border → margin

**Q3.** Which of the following has the **highest** specificity in CSS?
(A) Element selector (`p`)  (B) Class selector (`.intro`)  (C) ID selector (`#header`)  (D) Universal selector (`*`)

**Q4.** An XML document that conforms to the syntax rules of XML but has not been checked against any DTD or schema is said to be
(A) valid  (B) well-formed  (C) parsed  (D) normalised

**Q5.** In the MVC architecture, the component responsible for handling user input and updating the model is the
(A) Model  (B) View  (C) Controller  (D) Router

**Q6.** A **reverse proxy** server primarily
(A) hides client identities from external servers
(B) sits in front of web servers and forwards client requests to them, providing load balancing and caching
(C) translates private IP addresses to public ones
(D) resolves domain names

**Q7.** Which statement correctly distinguishes REST from SOAP?
(A) REST is a protocol; SOAP is an architectural style
(B) REST is an architectural style typically using HTTP verbs and JSON; SOAP is a protocol using XML messaging
(C) Both are protocols using XML only
(D) REST requires WSDL; SOAP does not

---

## Part B — Cloud Technology (Q8–Q13)

**Q8.** A customer who rents virtual machines, storage and networking, and manages the operating system and applications themselves, is using
(A) SaaS  (B) PaaS  (C) IaaS  (D) FaaS

**Q9.** Gmail and Salesforce are examples of which cloud service model?
(A) IaaS  (B) PaaS  (C) SaaS  (D) DaaS

**Q10.** Which of the following is **not** one of the NIST essential characteristics of cloud computing?
(A) On-demand self-service
(B) Rapid elasticity
(C) Permanent local storage
(D) Measured service

**Q11.** A **type-1** hypervisor
(A) runs directly on the bare-metal hardware
(B) runs as an application on a host operating system
(C) is used only for containers
(D) cannot support multiple guest operating systems

**Q12.** Compared with virtual machines, containers
(A) each include a full guest operating system
(B) share the host OS kernel and are therefore lighter and faster to start
(C) provide stronger hardware-level isolation
(D) cannot be orchestrated

**Q13.** Edge computing primarily aims to
(A) centralise all processing in a single large data centre
(B) process data close to where it is generated, reducing latency and bandwidth use
(C) eliminate the need for networks
(D) replace all cloud storage

---

## Part C — Cyber Security & Emerging Technologies (Q14–Q20)

**Q14.** In the OWASP Top 10 (2021 edition), the category ranked **A01** is
(A) Injection
(B) Broken Access Control
(C) Cryptographic Failures
(D) Server-Side Request Forgery

**Q15.** The most effective defence against SQL injection is
(A) hiding error messages
(B) using parameterised queries / prepared statements
(C) using HTTPS
(D) increasing password length

**Q16.** Cross-Site Scripting (XSS) allows an attacker to
(A) inject and execute malicious scripts in another user's browser
(B) read arbitrary files from the server's disk
(C) crash the database server
(D) intercept traffic on the physical layer

**Q17.** Which statement about symmetric and asymmetric cryptography is correct?
(A) Symmetric uses two different keys; asymmetric uses one
(B) Symmetric uses one shared key and is faster; asymmetric uses a public/private key pair and is slower
(C) Both use the same key
(D) Asymmetric cryptography cannot be used for digital signatures

**Q18.** A digital signature is created by encrypting the hash of a message with the
(A) sender's public key  (B) sender's private key  (C) receiver's public key  (D) receiver's private key

**Q19.** Which lightweight publish/subscribe protocol is widely used in IoT deployments?
(A) SMTP  (B) MQTT  (C) FTP  (D) SNMP

**Q20.** In a blockchain, immutability of past records is primarily achieved because
(A) records are encrypted with AES
(B) each block stores the cryptographic hash of the previous block, so altering one block invalidates all later blocks
(C) only administrators can write to the ledger
(D) blocks are stored on a single trusted server

---

## Part D — Paper-I (Q21–Q25)

**Q21.** Choose the word most nearly **opposite** in meaning to **AMBIGUOUS**.
(A) Vague  (B) Unclear  (C) Explicit  (D) Puzzling

**Q22.** Identify the error: *"One of my friends (A)/ who lives in Agartala (B)/ have invited me (C)/ for dinner. (D)"*
(A) A  (B) B  (C) C  (D) D

**Q23.** Find the odd one out: 8, 27, 64, 100, 125
(A) 27  (B) 64  (C) 100  (D) 125

**Q24.** A shopkeeper sells an article at a loss of 10%. Had he sold it for ₹90 more, he would have made a profit of 20%. The cost price of the article is
(A) ₹250  (B) ₹300  (C) ₹350  (D) ₹400

**Q25.** The Agartala–Akhaura rail link connects Tripura with
(A) Myanmar  (B) Bangladesh  (C) Nepal  (D) Bhutan

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | C | 6 | B | 11 | A | 16 | A | 21 | C |
| 2 | B | 7 | B | 12 | B | 17 | B | 22 | C |
| 3 | C | 8 | C | 13 | B | 18 | B | 23 | C |
| 4 | B | 9 | C | 14 | B | 19 | B | 24 | B |
| 5 | C | 10 | C | 15 | B | 20 | B | 25 | B |

---

**Q1 — (C).** `<article>` (along with `<header>`, `<footer>`, `<nav>`, `<section>`, `<aside>`, `<figure>`) carries meaning about its content. `<div>` and `<span>` are deliberately non-semantic; `<b>` is presentational.

**Q2 — (B).** Content, then **padding** (inside the border), then **border**, then **margin** (outside). Reversing padding and border is the usual error.

**Q3 — (C).** Specificity order: inline style > **ID** > class/attribute/pseudo-class > element > universal. `!important` overrides all of these.

**Q4 — (B).** **Well-formed** = obeys XML syntax (single root, properly nested and closed tags, quoted attributes). **Valid** = well-formed *and* conforms to a DTD or XML Schema. Every valid document is well-formed, but not vice versa.

**Q5 — (C).** The **Controller** receives input, invokes model logic and selects the view. The Model holds data and business rules; the View renders. Separation of concerns is the point.

**Q6 — (B).** A reverse proxy faces the *servers*, providing load balancing, SSL termination and caching, and hiding the backend. A **forward** proxy faces the *clients* and hides them — option A.

**Q7 — (B).** REST is an **architectural style** — stateless, resource-oriented, using HTTP verbs (GET/POST/PUT/DELETE) and usually JSON. SOAP is a **protocol** with a strict XML envelope, WSDL contracts and built-in standards for security and transactions.

**Q8 — (C).** **IaaS** delivers raw compute, storage and network; the customer manages OS upwards. In PaaS the provider also manages the OS and runtime; in SaaS the provider manages everything. "Who manages what" is the guaranteed exam question in this section.

**Q9 — (C).** Ready-to-use applications delivered over the web are **SaaS**.

**Q10 — (C).** NIST's five essential characteristics are on-demand self-service, broad network access, resource pooling, rapid elasticity and measured service. Permanent local storage is the opposite of the cloud model.

**Q11 — (A).** Type-1 (bare-metal / native) hypervisors — ESXi, Hyper-V, Xen — run directly on hardware and are used in data centres. Type-2 (hosted) — VirtualBox, VMware Workstation — run atop a host OS.

**Q12 — (B).** Containers virtualise at the OS level, sharing the host kernel: megabytes rather than gigabytes, and starting in milliseconds. VMs provide **stronger** isolation because each has its own kernel — so option C describes VMs, not containers.

**Q13 — (B).** Edge computing pushes processing toward the data source (devices, gateways, local nodes) to cut latency and backhaul bandwidth — critical for IoT, industrial control and real-time analytics.

**Q14 — (B).** **A01: Broken Access Control** topped the 2021 list, displacing Injection (which fell to A03). *Note: OWASP periodically revises the Top 10 — always check which edition a question refers to, and learn the current list by name for the exam.*

**Q15 — (B).** Parameterised queries separate code from data, so user input can never be interpreted as SQL. Input validation and least-privilege database accounts are useful defence-in-depth, but parameterisation is the actual fix.

**Q16 — (A).** XSS injects script that executes in **another user's browser** in the context of the trusted site — enabling session-cookie theft and defacement. The defence is output encoding plus a Content Security Policy.

**Q17 — (B).** Symmetric (AES, DES): one shared secret key, fast, but key distribution is the hard problem. Asymmetric (RSA, ECC): public/private key pair, slow, solves key distribution and enables digital signatures. Real systems use both — asymmetric to exchange a symmetric session key.

**Q18 — (B).** Signing uses the **sender's private key** on the message hash; anyone can verify with the sender's public key. This gives authentication, integrity and non-repudiation. *Encryption* for confidentiality is the reverse — the receiver's public key.

**Q19 — (B).** **MQTT** is a lightweight publish/subscribe protocol over TCP, designed for constrained devices and unreliable networks. CoAP is the other common IoT protocol (REST-like, over UDP).

**Q20 — (B).** Each block contains the hash of its predecessor, forming a chain. Tampering with any block changes its hash and breaks every subsequent link, which the distributed network immediately detects.

**Q21 — (C).** *Ambiguous* = open to more than one interpretation; its opposite is **explicit** (clearly and unmistakably stated). A, B and D are all synonyms.

**Q22 — (C).** The subject of the main clause is *One* (singular): "One of my friends … **has** invited me." The relative clause "who lives" correctly agrees with the singular *one* as well.

**Q23 — (C).** 8 = 2³, 27 = 3³, 64 = 4³, 125 = 5³ — all perfect cubes. **100** is not (it is a perfect square).

**Q24 — (B).** Let CP = x. Selling at 10% loss gives 0.9x; ₹90 more gives 1.2x. So 1.2x − 0.9x = 90 → 0.3x = 90 → x = **₹300**.

**Q25 — (B).** The **Agartala–Akhaura** rail link connects Agartala in Tripura with Akhaura in **Bangladesh**. Inaugurated in November 2023, it is a flagship India–Bangladesh connectivity project under the Act East Policy and drastically shortens the route between Tripura and Kolkata via Bangladesh.

---

## Score

| | |
|---|---|
| Part A (Web Technologies) | ___ / 7 |
| Part B (Cloud) | ___ / 6 |
| Part C (Cyber Security & Emerging Tech) | ___ / 7 |
| Part D (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Target: 20+.** These sections reward memorisation, not problem-solving, so anything below 18 is a straightforward fix rather than a conceptual gap.

**Must-memorise lists:** the OWASP Top 10 by name · IaaS/PaaS/SaaS responsibility split · NIST's five essential cloud characteristics · CSS specificity order · HTTP methods and status code classes · REST vs SOAP · symmetric vs asymmetric use cases. Available PYQs are thin here (65 web + 66 emerging-tech + 8 cloud questions in `02_State_PSC_PYQs/`), so supplement with direct study — see the "Gaps you must fill" section of `02_State_PSC_PYQs/README.md`.
