# 07 · Computer Networks — Precise Notes
> **TPSC ATO (IT) Paper-II §11** · ~11 marks (estimate) · Syllabus: *"Computer Networks — concept of layering: OSI and TCP/IP stacks; packet, circuit and virtual circuit switching; data link layer: framing, error detection, MAC, Ethernet bridging; routing protocols: shortest path, flooding, distance vector and link state; fragmentation and IP addressing, IPv4, CIDR; ARP, DHCP, ICMP; NAT; transport layer: flow and congestion control, UDP, TCP, sockets; application layer: DNS, SMTP, HTTP, FTP, Email"*
> Backbone: Sanchit Sir (Knowledge Gate). Also drawn from: Pearson GATE guide, CN-Notes (file 4), Ekxam (file 6), "Made Easy" (file 7). Refs like **[Src: Sanchit p.42]** point into `_source_pdfs/07_Computer_Networks/` — open them for diagrams. Page = PDF page index.

## Which notes are worth your time

| File | By | Format | Pages | Rating /5 | Best for · weakness |
|---|---|---|---|---|---|
| 1.CN.pdf (**Pearson**) | Pearson GATE guide | Typed, 2-column | 75 | 3.5 | ~150 practice MCQs with keys + year-tagged PYQs; app protocols, devices, NAT, token bucket · few numericals; several factual slips |
| 2.CN_Sanchit_Sir_Notes.pdf (**Sanchit**) | Knowledge Gate | Typed (Forouzan-based) | 299 | 4.5 | Full theory + GATE PYQs 2003–19 under each topic; best on fragmentation, subnetting, TCP · no DORA, NAT, BGP, IPv6, VLAN, HTTP codes; a few wrong worked answers |
| 3.Ace_Academy_CN_Class_Notes.pdf (**Ace**) | Ace Academy | Handwritten photocopy, watermark | 136 | 2 | Basic class jottings · unstructured, blank pages, some wrong statements |
| 4.CN_Notes.pdf (**CN-Notes**) | Unnamed lecture notes | Clean CamScanner handwriting | 179 | 3.5 | Clearest scan: numericals, STP walk-through, device-domain table, DNS diagrams · no PYQ tags |
| 5.Computer_Network-CS.pdf (**Wiki-CS**) | Wiki Engineering (raghul.org) | Faint handwritten photocopy | 178 | 1.5 | Solved window/RTO drills · barely legible, messy |
| 6.Computer_Networks.pdf (**Ekxam**) | Unnamed (ekxam.com) | Coloured handwritten photos | 115 | 3 | Only source with IPv6 header & IPv4-vs-IPv6 list · photographed spreads, obsolete IPv6 prefix table |
| 7.Computer_Networks_Hand_Written_Notes_Made_Easy.pdf (**MadeEasy**) | Labelled Made Easy; actually Techbits/Sajal photos | Handwritten phone photos, watermark | 139 | 2.5 | Readable traceroute/ICMP, FTP pages · watermark on every page, low contrast |

**If you open only one PDF besides these notes:** open **Pearson (1.CN.pdf)** and do its Practice Problems 1–2 (keys included) — closest to the TPSC MCQ format. Use **CN-Notes (file 4)** only for diagrams (STP p.166–167, DNS p.176).

## Topic map

| § | Topic | Priority | Typically asked as |
|---|---|---|---|
| 1 | Layering, OSI vs TCP/IP, devices | ⭐⭐⭐ | Which layer does X; PDU names; device ↔ domain |
| 2 | Switching, delays | ⭐⭐ | Circuit vs packet T/F; delay over k links |
| 3 | Framing, error detection | ⭐⭐⭐ | Bit-stuffed output; CRC remainder; dmin rules |
| 4 | Flow control (SW, GBN, SR) | ⭐⭐⭐ | Efficiency; min frame size; sequence bits |
| 5 | MAC, Ethernet, bridging | ⭐⭐⭐ | ALOHA max; CSMA/CD min frame; frame fields; STP |
| 6 | IPv4 header, fragmentation | ⭐⭐⭐ | HLEN/length decode; fragment offsets |
| 7 | Addressing, subnetting, CIDR, IPv6 | ⭐⭐⭐ | NID/broadcast; hosts; aggregation; longest prefix |
| 8 | Routing | ⭐⭐ | DV vs LS; count-to-infinity; RIP/OSPF/BGP facts |
| 9 | ARP, DHCP, ICMP, NAT | ⭐⭐ | What maps what; ICMP types; traceroute; private ranges |
| 10 | UDP, TCP, congestion, sockets | ⭐⭐⭐ | Header sizes; TCP states; cwnd trace; socket order |
| 11 | DNS, e-mail, HTTP, FTP | ⭐⭐⭐ | Ports; push/pull; DNS records; HTTP methods/codes |

## 1. Layering — OSI and TCP/IP

### 1.1 Layer · function · protocol · PDU

| OSI | Layer | TCP/IP | Core job (MCQ keywords) | Protocols | PDU | Device |
|---|---|---|---|---|---|---|
| 7 | Application | Application | User services: mail, file, directory, remote login | HTTP, FTP, SMTP, DNS, DHCP, SNMP, Telnet | Message | Gateway |
| 6 | Presentation | (Application) | Translation, ⭐**encryption**, ⭐**compression** | MIME, JPEG, MPEG, (TLS) | Data | — |
| 5 | Session | (Application) | ⭐**Dialog control**, ⭐**synchronisation/checkpoints** | RPC, NetBIOS | Data | — |
| 4 | Transport | Transport | ⭐**Process-to-process** (ports), segmentation, end-to-end flow & error control | TCP, UDP, SCTP | Segment / user datagram | — |
| 3 | Network | Internet | ⭐**Host-to-host**, logical (IP) addressing, ⭐**routing**, fragmentation | IP, ICMP, IGMP, ARP*, OSPF | Packet / datagram | Router |
| 2 | Data link (LLC + MAC) | Link | ⭐**Hop-to-hop**, ⭐**framing**, MAC addressing, medium access | Ethernet, Wi-Fi, PPP, HDLC | Frame | Bridge, switch |
| 1 | Physical | Link | Bits → signals, ⭐**bit synchronisation**, data rate | RS-232, 10BASE-T | Bit | Hub, repeater |

\* ARP: Forouzan/Sanchit file it under the network layer; Kurose says it straddles L2/L3 — pick whichever one appears in the options. [Src: Sanchit p.8–17]

- ⭐ Flow & error control exist at both L2 (one link) and L4 (end-to-end).
- ⭐ TCP/IP (RFC 1122) has 4 layers; Forouzan's 5-layer version splits Link into physical + data link. Session and presentation have no TCP/IP layer of their own.
- Only L2 adds a trailer (CRC). Addresses: MAC 48-bit (L2), IP 32/128-bit (L3), port 16-bit (L4).

🎯 **How it's asked:** wrong pair = "data link ↔ bit synchronisation" (GATE-2014); application-layer PDU = message (GATE-2012); S → R → R → D visits the network layer 4 times, the data link 6 times (GATE-2013).

### 1.2 Devices box

| Device | Layer | Splits collision domain | Splits broadcast domain |
|---|---|---|---|
| Repeater, hub | 1 | No | No |
| Bridge, switch | 2 | Yes, each port | No (unless VLANs) |
| Router | 3 | Yes | Yes, each interface |
| Gateway (protocol converter) | up to 7 | Yes | Yes |

⚠ A bridge uses MAC addresses and a router uses IP addresses (GATE-2004 reverses them). 🎯 15 hosts on 8-port switches with no uplinks → **3** switches (GATE-2019). [Src: CN-Notes p.169]

## 2. Switching and delays

### 2.1 Circuit vs datagram vs virtual circuit

| | Circuit | Datagram (packet) | Virtual circuit |
|---|---|---|---|
| Setup / teardown | Yes | No | Yes |
| Resources | Reserved end-to-end | On demand (FCFS queues) | Can be reserved at setup |
| Path | Fixed | Per packet, independent | Fixed for all packets |
| Header carries | Nothing extra | Full src + dst address | Short VC ID, rewritten per switch |
| Order | In order | May reorder or lose | In order |
| Delay | Setup, then constant | Variable (queuing) → jitter | Setup + low per-packet cost |
| Utilisation | Wasted when idle | Best | Medium |
| Example | Telephone | Internet IP | ATM, Frame Relay, X.25 |

⚠ Packet switching gives **more** delay variation, not less (GATE-2004 FALSE statement). [Src: Sanchit p.22–23]

### 2.2 Delays, BDP, throughput

📌 **Formulas**
- Tt = L/B · Tp = d/v (≈ 2 × 10⁸ m/s in cable) · plus queuing and processing · **a = Tp/Tt**.
- One packet, n routers: (n + 1)(Tt + Tp + proc) + n · queue [Src: Sanchit p.65].
- **P packets over k store-and-forward links: (k + P − 1) · Tt + k · Tp.**
- BDP = B × Tp (bits in the pipe one way; full duplex holds 2 · B · Tp) · path throughput = min link rate.

🔢 **GATE-2014.** 1000-byte file, 100-byte header per packet, 3 links, 10⁶ B/s, Tt only.
1 packet: 3 × 1.1 = 3.3 ms.
10 packets of 200 B: (3 + 9) × 0.2 = 2.4 ms.
20 packets of 150 B: (3 + 19) × 0.15 = 3.3 ms → T1 = T3 > T2 (headers vs pipelining).

🎯 1000 packets × 1000 bits, 3 links, 1 Mbps, 1 ms propagation → (3 + 999) + 3 = **1005 ms** (GATE-2012); optimum packet size for a 24-byte message, 3-byte header, 2 hops → **9 B** (GATE-2005).

## 3. Data link layer — framing and error detection

### 3.1 Framing

- Fixed size (ATM 53-byte cells) needs no delimiter. Variable size uses character count (obsolete), byte stuffing or bit stuffing.
- **Byte stuffing:** flag byte at both ends; insert ESC before every flag or ESC byte inside the data (PPP: flag 0x7E, ESC 0x7D). [Src: Sanchit p.107]
- **Bit stuffing** (HDLC flag **01111110**): insert a **0 after every five consecutive 1s**, whatever the next bit; the receiver removes it.

🔢 GATE-2014: output 01111100101 = 0·11111·**0**·0101 → input **0111110101**.
⚠ Flag 0111 → stuff after every "011": 01110110 → **0110101100** (GATE-2004).

### 3.2 Error detection and correction

| Method | How | Catches | Used in |
|---|---|---|---|
| Simple parity | 1 bit makes the 1-count even/odd; dmin = 2 | Odd number of errors only | Serial, memory |
| 2-D parity | Row + column parity | All 1-, 2-, 3-bit errors; corrects single-bit errors | Old block codes |
| Internet checksum | 16-bit one's-complement sum, complemented; receiver sum → all 1s | Most errors; misses reordered words | IP (header only), TCP, UDP, ICMP |
| CRC | Append r zeros, mod-2 divide by (r + 1)-bit g(x), append remainder | All bursts ≤ r | Ethernet CRC-32 (trailer), HDLC |

🔢 **Checksum (4-bit):** 7 + 11 + 12 + 0 + 6 = 36 = 100100₂ → wrap: 0100 + 10 = 0110 → checksum = **1001 (9)**. Receiver: 36 + 9 = 45 = 101101₂ → 1101 + 10 = 1111 → complement 0 → accept.

🔢 **CRC (GATE-2017):** data 01011011, g = x³ + x + 1 = 1011 → divide 1011011000 (leading 0 dropped):
```
1011011000
1011        → 0000011000
     1011   → 0000001110
      1011  → 0000000101   remainder 101
```
Send **01011011101**; the receiver's remainder 000 → accept. (11001001 with x³ + 1 → 11001001**011**, GATE-2007.)

📌 **CRC rules** (r = degree): x⁰ term + ≥ 2 terms → all single-bit errors; factor (x + 1) → all odd-count errors; bursts ≤ r always caught; burst r + 1 caught with probability 1 − (½)^(r−1); longer bursts 1 − (½)^r. [Src: Sanchit p.104]
⚠ Sanchit p.104 puts the CRC "in the frame header" — it is the **trailer** (FCS).

📌 **Hamming distance**

| To guarantee | Need |
|---|---|
| Detect s errors | dmin ≥ s + 1 |
| Correct t errors | dmin ≥ 2t + 1, so t = ⌊(dmin − 1)/2⌋ |
| Correct t and detect s (s > t) | dmin ≥ s + t + 1 |

- d(x, y) = number of 1s in x ⊕ y; for a linear code dmin = min weight of a non-zero codeword.
- Hamming code: **2^r ≥ m + r + 1**; check bits at positions 1, 2, 4, 8…; (7, 4) has dmin = 3 (corrects 1 or detects 2).

🎯 {00000, 01011, 10101, 11110} → dmin 3, corrects 1 (GATE-2017); {00000000, 00001111, 01010101, 10101010, 11110000} → dmin 4 → corrects **1** (GATE-2007); minimum corrupted bits in a 2-D parity table = 3 (GATE-2008).
⚠ Sanchit p.92 gives the GATE-2007 answer as "3" — correct is **1**.

## 4. Flow control — Stop-and-Wait, Go-Back-N, Selective Repeat

📌 **Stop-and-Wait:** cycle = Tt + 2Tp → **η = 1/(1 + 2a)**, throughput = L/(Tt + 2Tp). One-bit sequence numbers (0, 1). With error probability p, n packets need n/(1 − p) transmissions (p = 0.2, 100 packets → 125, GATE-2006).

| | Stop-and-Wait | Go-Back-N | Selective Repeat |
|---|---|---|---|
| Sender window (m-bit seq) | 1 | ≤ 2^m − 1 | ≤ 2^(m−1) |
| Receiver window | 1 | 1 | = sender window |
| Sequence numbers needed | 2 | Ws + 1 | 2Ws |
| ACKs | Individual | **Cumulative**, no NAK | Individual + **NAK** |
| Timers | 1 | 1 (oldest frame) | 1 per frame |
| On loss | Resend frame | Resend **all** outstanding | Resend **only** the lost frame |
| Out-of-order arrivals | — | Discarded | Buffered |
| Efficiency (Ws < 1 + 2a) | 1/(1 + 2a) | Ws/(1 + 2a) | Ws/(1 + 2a) |

[Src: Sanchit p.69–78 — window diagrams; comparison p.78]

📌 Full pipe needs **Ws ≥ 1 + 2a**. Always **Ws + Wr ≤ 2^m** (distinct numbers = M + N, GATE-2004). Max SR window with n bits = 2^(n−1) (GATE-2005).
📌 Sequence bits: generic "sliding window" = ⌈log₂(1 + 2a)⌉ (GATE-2007 key: log₂((2LtR + K)/K)); SR = ⌈log₂(2Ws)⌉. Piggybacking = the ACK rides in reverse-direction data.

🔢 **SR (GATE-2014):** 1 KB frames, 1.5 Mbps, Tp = 50 ms, 60 % utilisation.
Tt ≈ 5.46 ms → 1 + 2a ≈ 19.3.
Ws = 0.6 × 19.3 ≈ 12 → SR needs 24 numbers → **5 bits**.

🔢 **SW with ACK time (GATE-2016):** 1000-B frame at 80 kbps (100 ms) + 100-B ACK at 8 kbps (100 ms) + 2 × 100 ms propagation = 400 ms → **2500 B/s**.

🎯 50 % utilisation at 64 kbps, Tp 20 ms → Tt ≥ 40 ms → **320 B** (GATE-2015); GBN, 1 + 2a = 201 → **8 bits** (GATE-2015); GBN window 3, 9 packets, every 5th transmission lost → **16** (GATE-2006).

## 5. MAC sublayer, Ethernet and bridging

### 5.1 ALOHA and CSMA

| Protocol | Vulnerable time | Throughput | Max |
|---|---|---|---|
| Pure ALOHA | 2Tfr | G·e^(−2G) | **18.4 %** at G = ½ |
| Slotted ALOHA | Tfr | G·e^(−G) | **36.8 %** at G = 1 |
| CSMA | Tp | Depends on persistence | — |

- n stations each sending with probability p: P(exactly one) = **n·p·(1 − p)^(n−1)** (GATE-2007); maximum at p = 1/n.
- ALOHA backoff after K collisions: R ∈ {0 … 2^K − 1} slots of Tp (or Tfr). [Src: Sanchit p.26–35]
- Persistence when the channel is busy:
  - **1-persistent** keeps sensing, sends as soon as idle → most collisions (Ethernet);
  - **non-persistent** waits a random time before sensing again → idle waste;
  - **p-persistent** (slotted) sends with probability p, else defers one slot.

🎯 Slots with p = 0.1, 0.2, 0.3, 0.4: Σ pᵢ Π(1 − pⱼ) = 0.4404 → key picks nearest option 0.462 (GATE-2015).

### 5.2 CSMA/CD, backoff and the Ethernet frame

📌 **Tfr ≥ 2Tp → Lmin = 2 · Tp · B**; Dmax = Tfr · v/2. 10 Mbps Ethernet: **512 bits = 64 B**, slot time 51.2 µs. Efficiency 1/(1 + 6.4a) [Src: Sanchit p.36–40, p.115].
📌 **BEB:** after the n-th collision pick K ∈ {0 … 2^min(n,10) − 1} × 512 bit-times; abort after 16 attempts. A jam signal forces every station to notice the collision.

🔢 20 Mbps, Tp 40 µs → 1600 bits = **200 B** (GATE-2016).
🔢 Backoff race (GATE-2004): K_A ∈ {0, 1}, K_B ∈ {0 … 3} → P(A wins) = ½·¾ + ½·½ = **0.625**.

| Preamble | SFD | Dest MAC | Src MAC | Length/Type | Data + pad | CRC |
|---|---|---|---|---|---|---|
| 7 B | 1 B (10101011) | 6 B | 6 B | 2 B | 46–1500 B | 4 B |

- Preamble + SFD are added at the physical layer and **not counted**: frame = **64–1518 B** (1522 with a VLAN tag). Min data 46 = 64 − 18 (shorter data is padded). [Src: Sanchit p.113–114; CN-Notes p.70]
- Type ≥ 0x0600 = EtherType (0x0800 IPv4, 0x0806 ARP); ≤ 1500 = length.
- MAC 48-bit (24-bit OUI). LSB of the first byte 0 = unicast, 1 = multicast; all 1s = broadcast.
- Ethernet is connectionless with no ACK. 10 Mbps uses Manchester → bit rate = ½ baud (GATE-2007).
- IEEE: 802.3 Ethernet · 802.11 Wi-Fi · 802.5 token ring · 802.4 token bus · 802.1D STP · 802.1Q VLAN · 802.2 LLC.

⚠ Sanchit p.113's MAC example has 4 bytes — a MAC address is 6. "Ethernet = bus" holds only for classic coax; switched full-duplex Ethernet needs no CSMA/CD. "Single Protocol Data Unit" for L1 (Sanchit p.111, CN-Notes p.70) isn't standard — the L1 unit is the bit.

🎯 1 Gbps, 1 km, 2 × 10⁸ m/s → **10,000 bits** (GATE-2005); 500 Mbps, 10⁴-bit frames → max **2 km** (GATE-2013); CSMA/CD unsuitable for satellite links (GATE-2005).

### 5.3 CSMA/CA and controlled access

- **CSMA/CA (802.11):** collisions can't be detected (weak signal, hidden terminals), so it avoids them: wait an **IFS** (SIFS < DIFS; shorter = higher priority), random **contention window** with BEB (the timer freezes while busy), then a positive **ACK**. **RTS/CTS** + NAV fixes hidden terminals. [Src: Sanchit p.41–42]
- **Controlled access** is collision-free [Src: Sanchit p.44–50]:
  - reservation — mini-slots;
  - polling — poll / select / NAK;
  - token passing — logical ring: token ring, token bus, FDDI dual ring.
- 🔢 Polling (GATE-2007): 800 µs per turn + 80 µs poll → 8000/880 µs = **100/11 Mbps**.

### 5.4 Bridges, STP, switches

- **Learning bridge:** records source MAC → port; forwards known unicast frames, filters same-port frames, **floods** unknown and broadcast frames. It can't fragment, so mixing MTUs fails [Src: CN-Notes p.166].
- **STP (802.1D)** removes loops (broadcast storms, duplicates) [Src: CN-Notes p.166–167; Pearson p.31, GATE-2006]:
  1. Root bridge = lowest bridge ID.
  2. Each other bridge: **root port** = least cost to the root.
  3. Each LAN: **designated bridge/port** = closest to the root (tie → lower ID).
  4. Root + designated ports forward; the rest are **blocked** (BPDUs exchanged).
- **Switch** = multiport bridge with full-duplex ports; store-and-forward checks the CRC, cut-through forwards after reading the destination MAC.

### 5.5 VLAN (added — not in sources)

- Logical LAN = separate broadcast domain on one switch. 802.1Q tag = 4 B (TPID 0x8100, 12-bit VLAN ID → 4094 VLANs).
- Trunks carry many VLANs; inter-VLAN traffic needs a router or L3 switch.

## 6. Network layer — IPv4 header and fragmentation

### 6.1 IPv4 header (20–60 B) [Src: Sanchit p.124–145; Pearson p.57]

| Field | Bits | Remember |
|---|---|---|
| Version | 4 | 4 (6 for IPv6) |
| HLEN | 4 | ×4 bytes: 5–15 → 20–60 B |
| Service type (DSCP + ECN) | 8 | Precedence + TOS bits (old view) |
| Total length | 16 | ≤ **65,535**; data = total − 4·HLEN |
| Identification | 16 | Copied into all fragments |
| Flags | 3 | Reserved, **DF**, **MF** |
| Fragment offset | 13 | In **8-byte** units |
| TTL | 8 | −1 per hop; 0 → drop + ICMP; ⭐ prevents looping |
| Protocol | 8 | 1 ICMP, 2 IGMP, 6 TCP, 17 UDP, 89 OSPF |
| Header checksum | 16 | **Header only**; recomputed per router |
| Source, destination | 32 + 32 | Unchanged (unless NAT) |
| Options | ≤ 40 B | Record route (≤ **9** addresses), source route, timestamp |

- Routers change TTL, checksum and fragment fields — **never the source address** (GATE-2015). TTL, checksum and offset may all differ at the destination (GATE-2014).
- Decoding: first byte 0x45 = v4 with 20-B header; 0x42 → HLEN 8 B → invalid. In 4500 0028 0001 0000 **01**02…, TTL = 1 [Src: Sanchit p.143].
- Ethernet carries a CRC, IP a checksum (GATE-2006).

### 6.2 Fragmentation

📌 **Rules**
- Payload per fragment = largest multiple of 8 ≤ MTU − header (the last fragment may be shorter). Offset = preceding payload bytes ÷ 8.
- ID is copied; MF = 1 except on the last fragment. The source or any router may fragment; **only the destination reassembles**.
- DF = 1 and too big → drop + ICMP type 3 code 4.
- First byte = offset × 8; last byte = offset × 8 + (total − 4·HLEN) − 1. Extra overhead = (fragments − 1) × header.
- Position: MF 1 + offset 0 → first · MF 1 + offset ≠ 0 → middle · MF 0 + offset ≠ 0 → last · MF 0 + offset 0 → unfragmented.

🔢 **GATE-2018:** 4500-B datagram (20 B IP + 4480 B payload), MTU 600.
Per fragment: ⌊580/8⌋ × 8 = 576 B → 8 fragments (7 × 576 + 448).
Offsets 0, 72, **144**, 216 … 504; the last has MF = 0 and total length 468.

🎯 1000-B datagram, MTU 100 → **13** fragments (GATE-2016); UDP 8880 + 8 B, MTU 1500 → 7 fragments, last offset **1110** (GATE-2015); MF 0, HLEN 10, total 400, offset 300 → last fragment, bytes 2400–2759 (GATE-2013).

## 7. IP addressing — classful, subnetting, CIDR, IPv6

### 7.1 Classful and special addresses [Src: Sanchit p.165–174]

| Class | Lead bits | 1st octet | Mask | Networks | Hosts each |
|---|---|---|---|---|---|
| A | 0 | 1–126 usable | /8 | 126 | 2²⁴ − 2 |
| B | 10 | 128–191 | /16 | 2¹⁴ | 65,534 |
| C | 110 | 192–223 | /24 | 2²¹ | 254 |
| D | 1110 | 224–239 | — | Multicast | — |
| E | 1111 | 240–255 | — | Reserved | — |

- Host bits all 0 = network address; all 1 = **directed broadcast** (routable). **255.255.255.255** = limited broadcast (never forwarded).
- 0.0.0.0 = "this host" (0.0.0.0/0 = default route); 127/8 = loopback; 169.254/16 = APIPA.
- ⭐ **Private (RFC 1918): 10.0.0.0/8 · 172.16.0.0/12 (172.16–31) · 192.168.0.0/16** [Src: Pearson p.56].
- ⚠ Sanchit p.167: "0.0.0.0 reserved for broadcasting" — wrong; class A loses networks **0** (this network) and **127** (loopback).

### 7.2 Subnetting

📌 NID = IP AND mask · broadcast = IP OR (NOT mask) · hosts = 2^h − 2 · **block = 256 − interesting mask octet**; NID octet = largest multiple of the block ≤ the IP octet. A router-to-router link needs a /30 (block of 4) [Src: CN-Notes p.170].

🔢 141.121.119.168 /22 (255.255.252.0): block 4 in octet 3 → 116.
NID **141.121.116.0**, broadcast **141.121.119.255**, 1022 hosts.

🔢 203.112.111.117/27: block 32 → NID .96, broadcast .127, hosts .97–.126.

⚠ Subnet-zero trap: GATE-2007 (class B, 6-bit subnet) keys "62 subnets, 1022 hosts" (2^s − 2), but GATE-2005 (64 departments → 255.255.252.0) uses 2^s — follow the options.
🎯 Class B with 255.255.248.0 → **2046** hosts (GATE-2008); which mask separates .113 and .91 → /27 (GATE-2010); C1 (/17) sees C2 as local but C2 (/18) sees C1 as remote (GATE-2006).

### 7.3 CIDR, VLSM, aggregation, longest-prefix match

📌 /n → 2^(32−n) addresses. A valid block is **contiguous**, **power-of-2 sized**, and its **first address is divisible by the size**. VLSM: allocate the largest block first [Src: Sanchit p.188–199].

🔢 14.24.74.0/24 for 120, 60 and 10 hosts → .0/25, .128/26, .192/28 (48 addresses spare).

- **Supernetting:** 128.56.24.0/24 … 27.0/24 = 2¹⁰ addresses, 24 = 000110**00** → **128.56.24.0/22** (the mask loses 1s).
- **Longest-prefix match:** AND the destination with each mask; the longest matching prefix wins; otherwise the default route. 131.23.151.76 matches /12 and 131.22.0.0/15 → /15, interface 1 (GATE-2014) [Src: Sanchit p.224–227].

🎯 Last host of 200.10.11.144/27 = **.158** (GATE-2015); halve/quarter 245.248.128.0/20 → 245.248.136.0/21 + 245.248.128.0/22 (GATE-2012); 100.1.2.32–.47 → **/28**.
⚠ Sanchit p.191 gives the last address of 167.199.170.82/27 as .255 — correct is **.95**. His p.185/p.193 VLSM answers have overlapping or mislabelled blocks — check them with the block rule. His p.197 rule "all blocks must be the same size" isn't needed (/25 + /26 + /26 = /24 is valid).

### 7.4 IPv6 basics [Src: Ekxam p.103–115; Pearson p.60]

- 128-bit address in 8 hex groups. Drop leading zeros; one run of zero groups becomes **"::" (once per address)**.
- **Fixed 40-B base header:** version 4, traffic class 8, **flow label 20**, payload length 16, **next header 8**, **hop limit 8**, addresses 128 + 128.
- Differences from IPv4:
  - no header checksum;
  - **routers never fragment** (source only, after Path MTU discovery);
  - options become extension headers;
  - no broadcast (multicast/anycast instead);
  - NDP replaces ARP; minimum MTU 1280.
- Address types: global 2000::/3 · link-local FE80::/10 · unique-local FC00::/7 · multicast FF00::/8 · loopback ::1.
- Transition: dual stack, tunnelling (IPv6-in-IPv4), translation (NAT64).
- ⚠ Ekxam p.113's prefix table (010 provider-based, 100 geographic) is the obsolete RFC 1884 allocation.
- 🎯 Field common to IPv4 and IPv6 = **version**; fixed header = IPv6. Field widths: UDP port 16, MAC 48, next header 8, TCP sequence 32 (GATE-2018).

## 8. Routing — flooding, shortest path, distance vector, link state

- Routing builds the table; forwarding uses it. Static vs dynamic. An **AS** is one administration; intra-domain IGPs are RIP and OSPF, the inter-domain protocol is BGP.
- **Flooding:** send on all lines except the incoming one. It always finds the **shortest path** and is robust, but duplicates packets (limit with a hop count or seen-sequence numbers). Link-state routing uses it to spread LSPs. [Src: Sanchit p.200]

### 8.1 Distance vector (Bellman-Ford) [Src: Sanchit p.203–211; Pearson p.24]

- 📌 D_x(y) = min over neighbours v { c(x, v) + D_v(y) }. Each router sends its **whole vector to its neighbours** periodically (RIP every 30 s) and on change.
- 🔢 J's link costs: A 8, I 10, H 12, K 6. Their claimed costs to G: 18, 31, 6, 31 → 26, 41, **18**, 37 → "G: 18 via H".
- **Count-to-infinity:** bad news travels slowly; two routers keep raising each other's cost. Remedies: small infinity (**16**), **split horizon**, **poison reverse**, hold-down timers, triggered updates.
- ⚠ Split horizon cures only 2-node loops ("DV with split horizon avoids persistent loops" is FALSE, GATE-2014).

### 8.2 Link state (Dijkstra) and OSPF [Src: Sanchit p.215–223; Pearson p.25–27]

- Sequence: HELLO → measure link costs → **LSP** (ID, sequence number, age, neighbours) **flooded to all** → identical **LSDB** at every router → each runs **Dijkstra** locally (add the closest tentative node, update neighbours).
- **OSPF:** link state, cost metric, **areas** around backbone **area 0**, DR/BDR; runs directly over **IP protocol 89**.

| | Distance vector | Link state |
|---|---|---|
| Knows | Neighbours' vectors | Whole topology |
| Sends | Whole table → neighbours | Own links → **all** routers |
| Algorithm | Bellman-Ford, distributed | Dijkstra at every node |
| Convergence | Slow; count-to-infinity | Fast |
| CPU/memory | Low | Higher |

| | RIP | OSPF | BGP |
|---|---|---|---|
| Type | Intra-AS, DV | Intra-AS, LS | **Inter-AS, path vector** |
| Metric | Hops (max 15, **16 = ∞**) | Link cost | Policy, AS-path |
| Carried over | **UDP 520** | **IP 89** | **TCP 179** |
| Updates | 30 s; 180 s expiry; 120 s garbage | On change; Hello 10 s | Incremental UPDATEs |

### 8.3 BGP essentials (added — not in sources; sources only name it)

- Each route carries its **AS-PATH**; a router rejects routes containing its own AS → loop-free.
- Path choice follows **policy**, not pure shortest path. eBGP runs between ASes, iBGP inside one.

🎯 RIP = DV over UDP; OSPF = LS but **not** over TCP (GATE-2017); LS needs more computation but converges faster (GATE-2014); count-to-infinity is DV-only, and DV sends fewer messages (GATE-2008).

## 9. ARP, RARP, DHCP, ICMP and NAT

### 9.1 ARP and RARP [Src: Sanchit p.146–152]

- **ARP:** IP → MAC. Request **broadcast** (target MAC field all 0s), reply **unicast**, result cached. 28-B packet; operation 1 = request, 2 = reply; EtherType 0x0806.
- For a remote destination the host ARPs for the **default gateway**. MAC addresses change per hop; IP addresses don't.
- **RARP:** MAC → IP for diskless hosts; its broadcast can't cross routers → obsolete → BOOTP → DHCP.

### 9.2 DHCP — DORA (added — not in sources; they only note DHCP replaced RARP/BOOTP, UDP 67)

| Step | Message | Direction |
|---|---|---|
| D | DISCOVER | Client 0.0.0.0:68 → 255.255.255.255:67 (broadcast) |
| O | OFFER | Server → client (proposed IP + lease) |
| R | REQUEST | Client broadcast (accepts one offer) |
| A | ACK | Server → client (NAK if refused) |

- Gives IP, mask, gateway, DNS server and lease. Renew at **50 %** (T1), rebind at 87.5 % (T2). A **relay agent** reaches servers on other subnets.
- 🎯 The protocol **not** used to map one address to another = **DHCP** (GATE-2016); ARP = MAC for an IP (GATE-2005).

### 9.3 ICMP [Src: Sanchit p.153–157; MadeEasy p.90]

- Sent **inside IP (protocol 1), no ports**. Reports errors to the **source** without correcting them; error messages carry the original IP header + first 8 B of its data.

| Type | Message |
|---|---|
| 0 / 8 | Echo reply / request — **ping** |
| 3 | Destination unreachable (code 3 port, code 4 fragmentation needed + DF) |
| 5 | Redirect |
| 11 | **Time exceeded** (TTL = 0 → traceroute; reassembly timeout) |
| 12 | Parameter problem |
| 4 · 13/14 · 9/10 | Source quench (deprecated) · timestamp · router advertisement/solicitation |

- No ICMP error is generated about another ICMP error, about non-first fragments, or about multicast/broadcast datagrams.
- **traceroute** sends probes with TTL = 1, 2, 3…; each router answers with Time Exceeded; the destination answers with Port Unreachable (UDP probes) or Echo Reply (Windows tracert).
- ⚠ A closed UDP port → ICMP Port Unreachable; a closed TCP port → **RST** (RFC 1122). Sanchit p.276 keys GATE-2006 as "both".
- ⚠ Pearson p.42 says ICMP uses "TCP and UDP port 7" — wrong: it rides directly in IP.

### 9.4 NAT and PAT [Src: Pearson p.56, MCQ p.47]

- Border router maps private ↔ public addresses. Variants: static (1:1), dynamic (pool), **PAT/NAPT** (many:1 by port). Table: (192.168.1.10, 5000) ↔ (203.0.113.5, 62001).
- It rewrites IP address + checksum and TCP/UDP port + checksum. It saves IPv4 space and hides the internal topology.
- Drawbacks:
  - breaks end-to-end addressing;
  - inbound connections need port forwarding;
  - FTP-active/SIP need an ALG;
  - conflicts with IPsec AH;
  - the 16-bit port field limits mappings.

## 10. Transport layer — UDP, TCP, flow and congestion control, sockets

### 10.1 Ports, UDP vs TCP

- Ports (16-bit): well-known **0–1023**, registered 1024–49151, ephemeral **49152–65535**. Socket address = IP + port; a connection = 5-tuple (protocol, src IP, src port, dst IP, dst port). [Src: Sanchit p.230–232]
- **UDP header (8 B):** src port, dst port, length (≥ 8), checksum (optional in IPv4, mandatory in IPv6; pseudo-header included). Max data = 65,535 − 28 = **65,507 B**.
- 🔢 CB84 000D 001C 001C → ports 52100 → 13, length 28 → 20 B of data [Src: Sanchit p.274].

| | TCP | UDP |
|---|---|---|
| Connection | 3-way handshake, full duplex | None |
| Delivery | Reliable, ordered **byte stream** | Best effort, keeps message boundaries |
| Flow / congestion control | Yes | No |
| Header | 20–60 B | 8 B |
| Typical apps | HTTP, FTP, SMTP, POP3, IMAP, SSH, BGP | DNS, DHCP, SNMP, TFTP, RIP, VoIP, **multicast** |

### 10.2 TCP header (20–60 B) [Src: Sanchit p.237–248]

| Field | Bits | Remember |
|---|---|---|
| Source / destination port | 16 + 16 | — |
| Sequence number | 32 | First data byte of the segment; random ISN |
| Acknowledgement number | 32 | Next byte expected (cumulative) |
| HLEN · Reserved | 4 · 6 | ×4 → 20–60 B |
| Flags | 6 | **URG, ACK, PSH, RST, SYN, FIN** |
| Window | 16 | rwnd ≤ 65,535 B unscaled |
| Checksum | 16 | Mandatory; pseudo-header (protocol 6) |
| Urgent pointer | 16 | Valid if URG = 1 |
| Options | ≤ 40 B | MSS, window scale (≤ 14), SACK, timestamps |

- PSH = deliver immediately; RST = abort. Ethernet MSS = 1500 − 40 = **1460** [Src: Ekxam p.80].
- "TCP has no selective-ACK option" and "TCP connections are message streams" are both FALSE (GATE-2015).

### 10.3 Handshake and teardown [Src: Sanchit p.249–252, states diagram p.252]

```
Client: SYN, seq=x                 ──▶  Server (LISTEN → SYN-RCVD)
Client ◀── SYN+ACK, seq=y, ack=x+1
Client: ACK, seq=x+1, ack=y+1      ──▶  both ESTABLISHED
```
- **SYN and FIN each consume 1 sequence number**; a pure ACK consumes none.
- Close is 4 segments with half-close (FIN, ACK, FIN, ACK), or 3 when FIN+ACK is combined.
- Active closer: FIN-WAIT-1 → **FIN-WAIT-2** → **TIME-WAIT** (2 MSL) → CLOSED. Passive closer: CLOSE-WAIT → LAST-ACK → CLOSED.
- SYN flood is a DoS attack → see the Cyber Security file.
- 🎯 The client waits for the server's FIN in **FIN-WAIT-2** (GATE-2017); server LISTEN → SYN-RCVD → ESTABLISHED, and losing the SYN+ACK means no connection (GATE-2008).

### 10.4 Sequence numbers, wrap-around, window scale

- Segments with seq 230 and 290 → the first carries **60 B**; if it is lost the receiver ACKs **230** (GATE-2007).
- 📌 **Wrap-around time = 2³² B ÷ bytes per second** → 1 Gbps ≈ **34 s** (GATE-2018).
- 📌 Scaling is needed when B × RTT > 65,535 B: 1,048,560 bps → RTT > **500 ms**; max window 65,535 × 2¹⁴ (GATE-2015).
- ⚠ Sanchit p.240 gives a segment lifetime of 180 s; RFC 793 defines **MSL = 2 min**. Use the value the question gives.

### 10.5 Flow control, silly-window syndrome, timers [Src: Sanchit p.260, p.265–271]

- **Sender window = min(rwnd, cwnd)**: cwnd 4 KB with rwnd 6 KB → 4096 B (GATE-2005). TCP's window behaves like GBN (cumulative ACK, no NAK) and like SR (buffers out-of-order data).
- Silly-window cures: **Nagle** (sender buffers small writes until an ACK or a full MSS) and **Clark** (receiver advertises only when an MSS or half the buffer is free).
- Timers:
  - retransmission (RTO);
  - persistence — zero-window probes;
  - keep-alive — 2 h idle, then 10 probes **75 s** apart;
  - TIME-WAIT — 2 MSL.
- 📌 **Basic RTO:** RTT_new = α·RTT_old + (1 − α)·RTT_sample; RTO = 2 × RTT_new.
- 📌 **Jacobson:** D_new = α·D_old + (1 − α)·\|RTT_old − sample\|; **RTO = RTT_new + 4·D_new**. RFC 6298 puts weight ⅛ (and ¼ for the deviation) on the new sample.
- 📌 **Karn:** ignore RTT samples from retransmitted segments; **double the RTO** on each timeout.
- 🔢 RTT 40, samples 26, 32, 24, α = 0.9 → 38.6 → 37.94 → **36.55 ms** [Src: Pearson p.47].
- ⚠ Pearson p.40 says keep-alive probes are 75 *ms* apart — it's **75 s**. The RTO is adaptive, not fixed (GATE-2007).

### 10.6 Congestion control [Src: Sanchit p.260–264; Pearson p.40 graph]

- **cwnd** is known only to the sender; **ssthresh** separates the phases.
- **Slow start:** cwnd = 1 MSS, +1 MSS per ACK → **doubles every RTT** until ssthresh.
- **Congestion avoidance (additive increase):** **+1 MSS per RTT**.
- **Timeout:** ssthresh = cwnd/2, cwnd = 1, slow start again.
- **3 duplicate ACKs:** **fast retransmit** of the missing segment. Reno **fast recovery** sets ssthresh = cwnd/2 and cwnd = ssthresh, then continues in avoidance; Tahoe drops to 1.
- ⚠ Sanchit p.263's "+1 per ACK" in avoidance describes slow start. His initial ssthresh = (rwnd/MSS)/2 (p.261) is a coaching convention — use the question's value.

🔢 **cwnd trace** (MSS, ssthresh = 8; if doubling overshoots, cap at ssthresh):
```
RTT : 1 2 3 4 5  6  7  8 | 9 10 11 12 13 14 | 15 16
cwnd: 1 2 4 8 9 10 11 12 | 1  2  4  6  7  8 |  4  5
                timeout → ssthresh 6 ↑     3 dup ACK → ssthresh = cwnd = 4 ↑
```
🎯 Slow start: only "cwnd doubles every RTT" is true (GATE-2018); timeout at 32 KB, MSS 2 KB, RTT 100 ms → 2→16 in 3 RTTs, then +2 KB per RTT for 8 RTTs → **≈ 1100 ms** (GATE-2014); cwnd starts at 2, ssthresh 8, timeout in the 5th transmission → **7 MSS** at the 10th (GATE-2012); "TCP guarantees a minimum rate" is FALSE (GATE-2004).

📌 **Leaky bucket:** constant output rate; overflowing packets are dropped. **Token bucket:** tokens arrive at rate r up to capacity C; bursts allowed; tokens (not packets) are discarded. Max burst **S = C/(M − r)** [Src: Pearson p.26–27].
🔢 C 16 Mb, r 2 Mbps, M 10 Mbps → **2 s** (GATE-2008).
🔢 C 1 MB, M 20 MB/s, r 10 MB/s, 12 MB to send → 0.1 s burst (2 MB) + 1 s for the remaining 10 MB → **1.1 s** (GATE-2017).

### 10.7 Sockets API [Src: Sanchit p.272]

- TCP server: `socket → bind → listen → accept → recv/send → close`. TCP client: `socket → connect → send/recv → close`.
- `listen()` makes a socket passive (GATE-2014); `connect()` sends the SYN (GATE-2008); `accept()` returns a **new** connected socket; order bind, listen, accept, recv (GATE-2015).
- `SOCK_STREAM` = TCP, `SOCK_DGRAM` = UDP (`sendto/recvfrom`, no listen/accept). A connected UDP socket has one peer and can call `connect()` again (GATE-2017).

## 11. Application layer — DNS, e-mail, HTTP, FTP

### 11.1 DNS [Src: Sanchit p.278–283; Pearson p.44–45; CN-Notes p.175–176]

- Distributed hierarchical database: inverted tree of ≤ **128 levels**, labels ≤ **63** chars, names ≤ 255.
- Hierarchy: root (13 server identities) → TLD (.com, .org, .in, in-addr.arpa) → authoritative (primary + secondary) servers; the local resolver caches answers for their TTL.
- **Recursive** query: the server returns the final answer (host → local DNS). **Iterative** query: the server returns a referral (local → root → TLD → authoritative).
- **UDP 53** for queries (≤ 512 B), **TCP 53** for zone transfers and large answers. A resource record = (name, TTL, class, type, value).
- 🎯 After a reboot the browser sends **DNS query → TCP SYN → HTTP GET** (GATE-2016); DNS uses UDP (GATE-2007).

#### DNS record types (added — not in sources)

| Type | Maps |
|---|---|
| A / AAAA | Name → IPv4 / IPv6 |
| CNAME | Alias → canonical name |
| MX | Domain → mail server |
| NS | Zone → name server |
| PTR | IP → name (reverse) |
| SOA / TXT | Zone authority data / text (SPF) |

### 11.2 E-mail [Src: Sanchit p.292–295; Pearson p.43]

- User agent → **SMTP** (sender → its server → receiving server; **push**, TCP **25**, 7-bit ASCII; MAIL FROM, RCPT TO, DATA; 250 OK, 354 start input) → **POP3/IMAP** (**pull**). Webmail uses HTTP at both ends and SMTP between servers.
- **MIME** carries non-ASCII mail: Content-Type (text/html, image/jpeg, multipart/mixed), Content-Transfer-Encoding (**base64** = 3 bytes → 4 chars, quoted-printable).

| | POP3 | IMAP4 |
|---|---|---|
| TCP port | **110** (POP3S 995) | **143** (IMAPS 993) |
| Mail | Downloaded; delete (default) or keep mode | Stays on server |
| Folders, search, header-first, partial fetch | No | **Yes** |

⚠ Pearson p.42 says "POP: UDP 110" — POP3 uses **TCP**.
🎯 Send/retrieve = **SMTP, POP3** (GATE-2019); send = SMTP, download = POP, web = HTTP (GATE-2011); e-mail runs over TCP (GATE-2012); stateful = FTP, POP3 (GATE-2016).

### 11.3 HTTP [Src: Sanchit p.284–291; CN-Notes p.177]

- TCP **80** (HTTPS 443); **stateless**, **in-band**.
- Versions: HTTP/1.0 non-persistent; **HTTP/1.1 persistent by default** + pipelining + Host header; HTTP/2 multiplexing; HTTP/3 over QUIC/UDP.
- 📌 Non-persistent: 2 RTT + transfer time per object; N objects need N + 1 connections. Persistent: ≈ 1 RTT per extra object.
- **Cookies** (Set-Cookie → Cookie) add state. A proxy cache uses a conditional GET → **304** Not Modified.
- **HTTPS** = HTTP over TLS (confidentiality, integrity, authentication) → Cyber Security file.

| Method | Meaning |
|---|---|
| GET / HEAD | Retrieve / headers only |
| POST | Submit data in body (not idempotent) |
| PUT / DELETE / PATCH | Upload-replace (**client → server**) / remove / partial update |
| OPTIONS / TRACE / CONNECT | Capabilities / echo / proxy tunnel |

⚠ Pearson p.43 says PUT sends a document from the server to the client — it goes **client → server**. Persistent connections date from **HTTP/1.1**, not "2.0".

#### HTTP status codes (added — not in sources)

| Class | Key codes |
|---|---|
| 1xx info | 100 Continue, 101 Switching Protocols |
| 2xx success | **200 OK**, 201 Created, 204 No Content |
| 3xx redirect | **301** Moved Permanently, 302 Found, **304** Not Modified |
| 4xx client error | 400 Bad Request, **401** Unauthorized, **403** Forbidden, **404** Not Found |
| 5xx server error | **500** Internal Error, 502 Bad Gateway, **503** Service Unavailable |

### 11.4 FTP and relatives [Src: Sanchit p.296–297; MadeEasy p.137]

- **FTP** over TCP opens two connections: **control 21** (stays up the whole session; USER, PASS, RETR, STOR) and **data 20** (one per file). That split is **out-of-band** control; FTP is **stateful**.
- Passwords travel in plaintext. Data types: ASCII, EBCDIC, image. Transmission modes: stream (default), block, compressed.

#### FTP active vs passive (added — not in sources)

| | Active | Passive |
|---|---|---|
| Client sends | PORT (its IP + port) | PASV |
| Data connection opened by | Server (from port 20) | Client (to server's ephemeral port) |
| Behind firewall/NAT | Problematic | **Works** |

- **TFTP** UDP 69 (no login); **SFTP** over SSH 22; **FTPS** = FTP + TLS; **Telnet** TCP 23 (plaintext); **SSH** TCP 22.
- 🎯 HTTP and FTP can both use multiple TCP connections to the same server (GATE-2015); transports for multimedia, file transfer, DNS, e-mail = **UDP, TCP, UDP, TCP** (GATE-2013).

### 11.5 Well-known ports

| Port | Service | Port | Service |
|---|---|---|---|
| 20/21 | FTP data/control (TCP) | 123 | NTP (UDP) |
| 22 | SSH/SFTP (TCP) | 143 | IMAP (TCP) |
| 23 | Telnet (TCP) | 161/162 | SNMP agent/trap (UDP) |
| 25 | SMTP (TCP) | 179 | BGP (TCP) |
| 53 | DNS (UDP; TCP zone transfer) | 443 | HTTPS (TCP) |
| 67/68 | DHCP server/client (UDP) | 520 | RIP (UDP) |
| 69 | TFTP (UDP) | 587/465 | SMTP submission/SMTPS |
| 80 | HTTP (TCP) | 993/995 | IMAPS/POP3S |
| 110 | POP3 (TCP) | 3389 | RDP |

IP protocol numbers: 1 ICMP, 2 IGMP, 6 TCP, 17 UDP, 89 OSPF. EtherTypes: 0x0800 IPv4, 0x0806 ARP, 0x86DD IPv6, 0x8100 VLAN.

## Last-day revision sheet

| Item | Formula / number |
|---|---|
| Delays | Tt = L/B · Tp = d/v · a = Tp/Tt |
| P packets, k links | (k + P − 1)Tt + kTp |
| Stop-and-wait | η = 1/(1 + 2a); lossy: n/(1 − p) sends |
| Sliding window | η = Ws/(1 + 2a); full pipe Ws ≥ 1 + 2a |
| Windows (m bits) | GBN ≤ 2^m − 1 (Wr 1) · SR ≤ 2^(m−1) · Ws + Wr ≤ 2^m |
| ALOHA | Pure G·e^(−2G), 0.184 · slotted G·e^(−G), 0.368 |
| CSMA/CD | Lmin = 2·Tp·B; 64 B at 10 Mbps; slot 51.2 µs |
| BEB | K ∈ [0, 2^min(n,10) − 1]; abort after 16 |
| Ethernet frame | 7 + 1 + 6 + 6 + 2 + 46–1500 + 4; frame 64–1518 B |
| Hamming | Detect s: s + 1 · correct t: 2t + 1 · 2^r ≥ m + r + 1 |
| IPv4 | Header 20–60 B (HLEN × 4) · length ≤ 65,535 · offset × 8 |
| Fragment payload | ⌊(MTU − 20)/8⌋ × 8 |
| Subnet | Hosts 2^h − 2 · block 256 − mask octet |
| CIDR | 2^(32−n) addresses; first address divisible by size |
| Private | 10/8 · 172.16/12 · 192.168/16 |
| IPv6 | 128-bit · 40-B header · flow label 20 · hop limit 8 |
| UDP / TCP header | 8 B / 20–60 B |
| TCP wrap-around | 2³² B ÷ (B/s) |
| RTO | Basic 2·RTT · Jacobson RTT + 4D · Karn doubles |
| Token bucket | S = C/(M − r) |
| RIP | ∞ = 16 · 30/180/120 s · UDP 520 |
| DNS | 128 levels · 63-char labels · port 53 |

- ⭐ Routing + IP addressing → network layer; framing + MAC → data link; encryption + compression → presentation; dialog control → session.
- ⭐ PDUs: bit → frame → packet → segment → message.
- ⭐ Hubs split nothing; switches split collision domains; routers split both.
- ⭐ Bit stuffing adds a 0 after five 1s; the flag is 01111110.
- ⭐ Parity detects only odd error counts. The IP checksum covers only the header. The CRC sits in the trailer.
- ⭐ GBN discards out-of-order frames (cumulative ACK); SR buffers them (NAK).
- ⭐ CSMA/CD for wired Ethernet; CSMA/CA + RTS/CTS for Wi-Fi.
- ⭐ STP: lowest bridge ID = root; root + designated ports forward, the rest block.
- ⭐ TTL stops looping; record route holds ≤ 9 addresses; only the destination reassembles.
- ⭐ IPv6 routers never fragment and there is no IPv6 broadcast.
- ⭐ 255.255.255.255 is never forwarded; a directed broadcast is routable.
- ⭐ When several routes match, the longest prefix wins.
- ⭐ Flooding always finds the shortest path. Count-to-infinity is DV-only; split horizon fixes only 2-node loops.
- ⭐ RIP–DV–UDP 520 · OSPF–LS–IP 89 · BGP–path vector–TCP 179.
- ⭐ ARP request broadcast, reply unicast. DHCP = DORA on UDP 67/68.
- ⭐ ping = ICMP 8/0; traceroute = TTL expiry → ICMP 11. ICMP has no ports.
- ⭐ PAT = many hosts behind one public IP using ports.
- ⭐ SYN/FIN use 1 sequence number each; the client waits in FIN-WAIT-2; TIME-WAIT = 2 MSL.
- ⭐ Window = min(rwnd, cwnd); slow start doubles per RTT; avoidance adds 1 MSS per RTT.
- ⭐ Timeout → cwnd 1; 3 dup ACKs → fast retransmit / fast recovery.
- ⭐ Nagle = sender-side cure, Clark = receiver-side cure.
- ⭐ Server socket order: socket–bind–listen–accept; connect() sends the SYN.
- ⭐ UDP carries DNS, DHCP, SNMP, TFTP, RIP, VoIP and multicast.
- ⭐ SMTP pushes (25); POP3 (110) and IMAP (143) pull; MIME uses base64.
- ⭐ HTTP is stateless and in-band; HTTP/1.1 is persistent; cookies add state; 404 Not Found, 304 Not Modified.
- ⭐ FTP is stateful and out-of-band: 21 control, 20 data; passive mode suits firewalls.
- ⭐ DNS: UDP for queries, TCP for zone transfers; host→local recursive, local→root iterative; MX = mail, CNAME = alias, PTR = reverse.

## Dropped as outside TPSC syllabus

- Data-communication basics: components, simplex/duplex modes, network criteria, standards bodies (Sanchit p.1–7; Pearson p.2–5; CN-Notes p.60).
- Topologies, LAN/MAN/WAN categories (Sanchit p.3–7; Pearson p.3–5).
- Physical layer — line coding waveforms, baud vs bit rate, async start/stop-bit numericals, media → Communication section (Sanchit p.118–120; Ace p.60).
- Multiplexing and FDMA/TDMA/CDMA → Communication section (Sanchit p.51–54).
- Network security and cryptography (RSA, IPsec, firewalls, SSL internals) → Cyber Security file (Pearson Ch.5; Ekxam p.96–102, 110; MadeEasy p.130).
- IGMP/multicast routing, multipath routing, T/TCP, QoS flow specs (Sanchit p.158; Pearson p.24, 47, 62).
- WWW browser architecture and the cookie-advertising narrative (Sanchit p.284–288); extended RTO drill sheets (Wiki-CS p.100).
- GATE-2007 firewall-automaton question (Theory of Computation, Sanchit p.277); number-system refreshers in the scans (Ekxam p.1).
