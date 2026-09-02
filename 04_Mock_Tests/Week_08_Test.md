# Week 8 Mock Test — Computer Networks

**Syllabus §11** · 25 questions · **30 minutes** · +1 / −0.33 · No calculator

---

## Part A — Computer Networks (Q1–Q20)

**Q1.** Routing and logical (IP) addressing are the responsibility of which OSI layer?
(A) Data link  (B) Network  (C) Transport  (D) Session

**Q2.** The TCP/IP reference model consists of how many layers?
(A) 3  (B) 4  (C) 5  (D) 7

**Q3.** Which OSI layers are **absent** as separate layers in the TCP/IP model?
(A) Physical and data link
(B) Session and presentation
(C) Network and transport
(D) Application and transport

**Q4.** A network is given as `192.168.10.0/26`. The number of **usable host addresses** per subnet is
(A) 30  (B) 62  (C) 64  (D) 126

**Q5.** The subnet mask corresponding to the prefix `/27` is
(A) 255.255.255.192  (B) 255.255.255.224  (C) 255.255.255.240  (D) 255.255.255.128

**Q6.** The minimum and maximum sizes of the IPv4 header are respectively
(A) 20 and 60 bytes  (B) 20 and 40 bytes  (C) 40 and 60 bytes  (D) 8 and 20 bytes

**Q7.** The IPv6 header has a **fixed** size of
(A) 20 bytes  (B) 32 bytes  (C) 40 bytes  (D) 60 bytes

**Q8.** TCP establishes a connection using
(A) a two-way handshake
(B) a three-way handshake (SYN, SYN-ACK, ACK)
(C) a four-way handshake
(D) no handshake

**Q9.** Which of the following is true of UDP?
(A) It is connection-oriented and reliable
(B) It is connectionless, with no flow or congestion control
(C) It guarantees in-order delivery
(D) It uses a three-way handshake

**Q10.** With an m-bit sequence number field, the maximum sender window sizes for **Go-Back-N** and **Selective Repeat** are respectively
(A) 2ᵐ and 2ᵐ  (B) 2ᵐ − 1 and 2ᵐ⁻¹  (C) 2ᵐ⁻¹ and 2ᵐ − 1  (D) 2ᵐ and 2ᵐ⁻¹

**Q11.** The maximum channel utilisation (efficiency) of **pure ALOHA** and **slotted ALOHA** are respectively
(A) 18.4% and 36.8%  (B) 36.8% and 18.4%  (C) 50% and 100%  (D) 25% and 50%

**Q12.** The minimum frame size in standard 10 Mbps Ethernet is
(A) 32 bytes  (B) 46 bytes  (C) 64 bytes  (D) 1518 bytes

**Q13.** The protocol that resolves a known IP address into the corresponding MAC address is
(A) RARP  (B) ARP  (C) ICMP  (D) DHCP

**Q14.** The `ping` utility uses which protocol?
(A) TCP  (B) UDP  (C) ICMP  (D) ARP

**Q15.** The well-known port numbers for HTTP, HTTPS, SMTP and DNS are respectively
(A) 80, 443, 25, 53  (B) 8080, 443, 110, 53  (C) 80, 8443, 25, 69  (D) 443, 80, 53, 25

**Q16.** To **detect** up to `d` bit errors, the minimum Hamming distance of a code must be at least
(A) d  (B) d + 1  (C) 2d  (D) 2d + 1

**Q17.** The "count-to-infinity" problem is associated with which routing approach?
(A) Link state routing  (B) Distance vector routing  (C) Flooding  (D) Source routing

**Q18.** Which routing protocol uses Dijkstra's shortest-path algorithm over a complete topology map?
(A) RIP  (B) OSPF  (C) BGP  (D) ARP

**Q19.** Network Address Translation (NAT) primarily
(A) encrypts traffic between networks
(B) allows many private hosts to share one or a few public IP addresses
(C) resolves domain names to IP addresses
(D) compresses packet headers

**Q20.** In TCP congestion control, the congestion window grows **exponentially** during which phase?
(A) Slow start  (B) Congestion avoidance  (C) Fast recovery  (D) Retransmission timeout

---

## Part B — Paper-I (Q21–Q25)

**Q21.** Choose the word most nearly **opposite** in meaning to **TRANSPARENT**.
(A) Clear  (B) Opaque  (C) Obvious  (D) Visible

**Q22.** Select the correct sentence.
(A) He is senior than me by three years.
(B) He is senior to me by three years.
(C) He is more senior than me by three years.
(D) He is senior from me by three years.

**Q23.** In a row of 40 students, Rahul is 12th from the left end. What is his position from the right end?
(A) 27th  (B) 28th  (C) 29th  (D) 30th

**Q24.** The compound interest on ₹10,000 at 10% per annum for 2 years, compounded annually, is
(A) ₹2,000  (B) ₹2,100  (C) ₹2,200  (D) ₹2,310

**Q25.** The longest river of Tripura is
(A) Gomati  (B) Khowai  (C) Manu  (D) Muhuri

---
---

# ✅ Answer Key & Explanations

> Stop. Only read past this line after your 30 minutes are up.

| Q | Ans | Q | Ans | Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 6 | A | 11 | A | 16 | B | 21 | B |
| 2 | B | 7 | C | 12 | C | 17 | B | 22 | B |
| 3 | B | 8 | B | 13 | B | 18 | B | 23 | C |
| 4 | B | 9 | B | 14 | C | 19 | B | 24 | B |
| 5 | B | 10 | B | 15 | A | 20 | A | 25 | A |

---

**Q1 — (B).** The network layer handles logical addressing (IP), routing and forwarding, fragmentation and reassembly. The data link layer handles *physical* (MAC) addressing within a single link.

**Q2 — (B).** TCP/IP has 4 layers: Application, Transport, Internet, Network Access (Link). *(Some textbooks show a 5-layer hybrid splitting the last into physical and data link — read the question's wording.)*

**Q3 — (B).** The **session and presentation** layers have no separate counterpart; their functions are folded into TCP/IP's application layer.

**Q4 — (B).** /26 leaves 32 − 26 = 6 host bits → 2⁶ = 64 addresses, minus the network and broadcast addresses = **62** usable hosts. (It also yields 4 subnets from a /24.)

**Q5 — (B).** /27 = 27 ones then 5 zeros. The last octet is 11100000 = 224 → **255.255.255.224**. Worth memorising: /25→128, /26→192, /27→224, /28→240, /29→248, /30→252.

**Q6 — (A).** IPv4 header: minimum **20 bytes** (IHL = 5), maximum **60 bytes** (IHL = 15) when options are present.

**Q7 — (C).** IPv6 fixed header is **40 bytes** — larger than IPv4's minimum, but fixed and simpler (no checksum, no fragmentation fields), with extension headers used for options.

**Q8 — (B).** SYN → SYN-ACK → ACK. Connection *teardown* takes four segments (FIN, ACK, FIN, ACK), which is a separate common question.

**Q9 — (B).** UDP is connectionless, unreliable, unordered, and has no flow or congestion control — an 8-byte header versus TCP's 20. Its advantage is low latency and overhead.

**Q10 — (B).** Go-Back-N needs one unused sequence number to distinguish a retransmission from new data → **2ᵐ − 1**. Selective Repeat needs the window to be at most half the sequence space → **2ᵐ⁻¹**.

**Q11 — (A).** Pure ALOHA peaks at 1/2e ≈ **18.4%**; slotted ALOHA halves the vulnerable period, doubling this to 1/e ≈ **36.8%**.

**Q12 — (C).** **64 bytes** (512 bits). The minimum exists so a transmitting station is still sending when the furthest collision signal returns — otherwise CSMA/CD cannot detect the collision.

**Q13 — (B).** ARP: IP → MAC. **RARP** does the reverse (MAC → IP) and is largely superseded by DHCP.

**Q14 — (C).** `ping` sends ICMP Echo Request and awaits Echo Reply. `traceroute` also uses ICMP (Time Exceeded messages).

**Q15 — (A).** HTTP **80**, HTTPS **443**, SMTP **25**, DNS **53**. Also worth memorising: FTP 20 (data)/21 (control), SSH 22, Telnet 23, POP3 110, IMAP 143.

**Q16 — (B).** To **detect** d errors you need d_min ≥ **d + 1**; to **correct** d errors you need d_min ≥ 2d + 1. Option D is the correction formula — the intended trap.

**Q17 — (B).** In distance vector routing, bad news propagates slowly: routers keep incrementing each other's costs toward infinity. Mitigations include split horizon, poison reverse and defining a small "infinity" (16 in RIP).

**Q18 — (B).** OSPF is a link-state protocol: every router floods link-state advertisements, builds an identical topology database, and runs **Dijkstra** locally. RIP is distance vector; BGP is path vector.

**Q19 — (B).** NAT rewrites source addresses/ports so a whole private network can share a small pool of public addresses — the main reason IPv4 exhaustion was survivable.

**Q20 — (A).** In slow start the congestion window doubles every RTT (exponential) until it reaches the threshold, after which **congestion avoidance** grows it linearly (additive increase).

**Q21 — (B).** *Transparent* = allowing light through, clear; its opposite is **opaque**. A, C and D are all synonyms.

**Q22 — (B).** Latin comparatives — *senior, junior, superior, inferior, prior, preferable* — take **to**, never *than*, and are never used with *more*.

**Q23 — (C).** Position from right = total − position from left + 1 = 40 − 12 + 1 = **29th**. The "+1" is what most people drop.

**Q24 — (B).** Amount = 10000 × (1.1)² = 10000 × 1.21 = 12,100. CI = 12,100 − 10,000 = **₹2,100**. (Simple interest would have been ₹2,000 — option A is the trap.)

**Q25 — (A).** The **Gomati** is Tripura's longest river, rising in the Dumboor Lake area and flowing west into Bangladesh. Tripura's other main rivers are the Khowai, Manu, Muhuri, Haora, Dhalai and Feni.

---

## Score

| | |
|---|---|
| Part A (Computer Networks) | ___ / 20 |
| Part B (Paper-I) | ___ / 5 |
| Raw total | ___ / 25 |
| After −1/3 penalty | ___ |

**Weak-area pointers:** missed Q4/Q5 → **drill subnetting and CIDR until it is 30-second reflex** — it is the most reliably asked networks topic; missed Q10–Q12/Q16 → redo the data link layer; missed Q17/Q18 → redo routing protocols; missed Q8/Q9/Q20 → redo TCP. Memorise the port-number table and the OSI layer→protocol table outright. Then drill `03_GATE_CSE_PYQs/Subject_wise/Paper2_S11_Computer_Networks/` (226 questions) and the 537 state-PSC-level ones.
