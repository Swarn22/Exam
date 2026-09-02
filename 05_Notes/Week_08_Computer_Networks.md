# Week 8 — Computer Networks

**Syllabus §11:** Concept of layering: OSI and TCP/IP protocol stacks. Basics of packet, circuit and virtual circuit switching. Data link layer: framing, error detection, medium access control, Ethernet bridging. Routing protocols: shortest path, flooding, distance vector and link state routing. Fragmentation and IP addressing, IPv4, CIDR notation. Basics of IP support protocols (ARP, DHCP, ICMP), Network Address Translation (NAT). Transport layer: flow control and congestion control, UDP, TCP, sockets. Application layer protocols: DNS, SMTP, HTTP, FTP, Email.
**Estimated marks: ~11**

---

## 💡 What this subject is about

Getting a message from one computer to another sounds simple until you list what must be solved:

- Turning bits into electrical/optical signals (**physical**)
- Deciding whose turn it is to transmit on a shared wire (**data link**)
- Finding a route across thousands of intermediate networks (**network**)
- Recovering from lost packets and not overwhelming the receiver (**transport**)
- Agreeing on what the message *means* (**application**)

Trying to solve all of that at once is hopeless. So networking is organised in **layers**, each solving one problem and using the layer below. Understanding the layer model is therefore the single most important thing in this subject — and it is also the most heavily asked.

---

# 1. ⭐⭐⭐ Layering

## 1.1 💡 Why layers

💡 **Postal analogy.** You write a letter (application). You put it in an envelope with an address (transport/network). The post office routes it through sorting centres (network). A van carries it on each leg (data link). The road carries the van (physical).

⭐ **Each layer:**
- provides a **service** to the layer above
- uses the **service** of the layer below
- can be **replaced** without disturbing the others (swap the van for a train; the letter is unaffected)

⭐ **Encapsulation:** as data moves down the stack, each layer adds its own **header**. At the receiver each layer strips its own header off.

```
Application:                    [ DATA ]
Transport:            [TCP hdr][ DATA ]           → SEGMENT
Network:      [IP hdr][TCP hdr][ DATA ]           → PACKET / DATAGRAM
Data link: [Eth][IP hdr][TCP hdr][ DATA ][CRC]    → FRAME
Physical:  10110100101110010110...                 → BITS
```

## 1.2 ⭐⭐⭐ The OSI reference model (7 layers)

| # | Layer | 💡 Job | Unit | ⭐ Devices | ⭐ Protocols |
|---|---|---|---|---|---|
| 7 | **Application** | Services the user actually wants | Data | — | HTTP, FTP, SMTP, DNS, DHCP, SNMP, Telnet |
| 6 | **Presentation** | ⭐ **Translation, ENCRYPTION, COMPRESSION** — data *representation* | Data | — | SSL/TLS, JPEG, MPEG, ASCII |
| 5 | **Session** | ⭐ **Session setup/teardown, DIALOG CONTROL, synchronisation, checkpointing** | Data | — | RPC, NetBIOS, PPTP |
| 4 | ⭐ **Transport** | ⭐ **END-TO-END delivery, SEGMENTATION, reliability, flow control, PORT addressing** | ⭐ **Segment** | Gateway | ⭐ **TCP, UDP**, SCTP |
| 3 | ⭐ **Network** | ⭐ **ROUTING, LOGICAL (IP) ADDRESSING, FRAGMENTATION** | ⭐ **Packet / datagram** | ⭐ **ROUTER**, layer-3 switch | ⭐ **IP, ICMP, IGMP, RIP, OSPF, BGP**, ARP* |
| 2 | ⭐ **Data link** | ⭐ **FRAMING, PHYSICAL (MAC) ADDRESSING, error detection, MAC/medium access** | ⭐ **Frame** | ⭐ **SWITCH, BRIDGE**, NIC | Ethernet, PPP, HDLC, ARP*, Token Ring |
| 1 | **Physical** | Bits on the medium — voltages, encoding, connectors, topology | ⭐ **Bit** | ⭐ **HUB, REPEATER**, cable, modem | RS-232, DSL, 10BASE-T |

⭐ **Mnemonics:**
- Layer 7 → 1: **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
- Layer 1 → 7: **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way

⚠ ⭐ **ARP's layer is genuinely disputed.** It is most often placed at **layer 2** (it deals in MAC addresses and does not cross routers), but many textbooks — and the TPSC syllabus itself — list it as a "network-layer IP support protocol". ⭐ **If asked, prefer layer 2 (data link)**, unless the option set clearly wants network layer.

### ⭐ The three most-asked layer facts

📌 ⭐ **Routing and IP addressing → NETWORK layer (3)**
📌 ⭐ **Framing and MAC addressing → DATA LINK layer (2)**
📌 ⭐ **Encryption and compression → PRESENTATION layer (6)**

⚠ ⭐ **Both the data link layer and the transport layer do "flow control and error control"** — but the data link layer does it **hop-by-hop** (across one link) while the transport layer does it **end-to-end** (across the whole path).

## 1.3 ⭐⭐ The TCP/IP model (4 layers)

| TCP/IP layer | ⭐ Maps to OSI layers |
|---|---|
| **Application** | Application + **Presentation + Session** |
| **Transport** | Transport |
| **Internet** | Network |
| **Network Access / Link** | Data link + Physical |

📌 ⭐⭐ **The SESSION and PRESENTATION layers have NO separate counterpart in TCP/IP** — their functions are folded into the application layer.

⚠ ⭐ Some textbooks present a **5-layer hybrid** (splitting network access into physical and data link). ⭐ **Read the question:** if the options include 4 and 5, and it says "TCP/IP model", the intended answer is normally **4**.

| | **OSI** | ⭐ **TCP/IP** |
|---|---|---|
| Layers | **7** | ⭐ **4** |
| Origin | Designed as a theoretical **reference model** first | ⭐ **Protocols were implemented first**, the model described afterwards |
| Service/interface separation | Clearly defined | Blurred |
| Transport reliability | Connection-oriented only | ⭐ **Both** (TCP reliable, UDP unreliable) |
| Real-world usage | Teaching and reference | ⭐ **The actual Internet** |

## 1.4 ⭐⭐ Switching

### 💡 The three ways to move data through a network

**Circuit switching** — set up a **dedicated physical path** before any data flows, hold it for the whole conversation, tear it down at the end. Traditional telephony.
💡 *Like reserving an entire lane of a motorway for your journey.* Guaranteed quality, but the lane sits empty whenever you pause.

**Datagram (packet) switching** — break the message into **packets**, each carrying the full destination address, and let each packet find its own way. The Internet.
💡 *Like posting 100 numbered postcards.* They may take different routes and arrive out of order, but the network is shared efficiently.

**Virtual circuit switching** — set up a **logical** path first (so all packets follow the same route and stay in order), but do not reserve bandwidth. ATM, Frame Relay, MPLS.
💡 *A compromise: a fixed itinerary, but a shared vehicle.*

| | **Circuit switching** | ⭐ **Datagram switching** | **Virtual circuit** |
|---|---|---|---|
| Path setup | ⭐ **Dedicated, before transfer** | ❌ None | Logical circuit first |
| Bandwidth reserved | ✅ Yes | ❌ No | Partially |
| Packets follow | Same path | ⭐ **Possibly DIFFERENT paths** | Same path |
| Order guaranteed | ✅ | ⭐ **❌ No** | ✅ |
| Addressing | Set up once | ⭐ **Full address in EVERY packet** | Short VC identifier |
| Efficiency if idle | ⭐ **Wasteful** | ⭐ **Efficient (statistical multiplexing)** | Efficient |
| Example | Telephone network | ⭐ **The Internet (IP)** | ATM, MPLS |

## 1.5 ⭐⭐ Delays and performance

### 💡 The four delays

📌 ⭐ **Transmission delay = packet size ÷ bandwidth** (L/B)
💡 *How long it takes to push all the bits onto the wire.* Depends on **packet size** and **link speed**.

📌 ⭐ **Propagation delay = distance ÷ propagation speed** (d/v)
💡 *How long a bit takes to travel down the wire.* Depends on **distance** and **medium** — **not** on packet size.

📌 **Queuing delay** — time spent waiting in a router's buffer (variable, load-dependent).
📌 **Processing delay** — time for a router to examine the header.

⚠⚠ ⭐ **Transmission delay depends on packet size and bandwidth; propagation delay depends on distance and medium.** Confusing these is the standard trap.

### 🔢 Worked examples

🔢 **A 1500-byte packet on a 10 Mbps link:**
```
Transmission delay = (1500 × 8 bits) / 10⁷ bps = 12000/10⁷ = 1.2 ms
```

🔢 **A 2000 km link, signal speed 2 × 10⁸ m/s:**
```
Propagation delay = 2 × 10⁶ m / 2 × 10⁸ m/s = 10 ms
```
⭐ Note the propagation delay (10 ms) dwarfs the transmission delay (1.2 ms) here — typical for long links, and the reason sliding-window protocols matter (§3.4).

📌 ⭐ **RTT (Round-Trip Time) ≈ 2 × propagation delay** (plus transmission and processing).
📌 ⭐ **Bandwidth–delay product = bandwidth × RTT** — the number of bits "in flight" in the pipe. ⭐ **This is the minimum window size needed to keep the link fully utilised.**

🔢 A 10 Mbps link with 20 ms RTT: BDP = 10⁷ × 0.02 = **200,000 bits = 25 KB**. If your window is smaller, the link idles.

---

# 2. ⭐ Physical layer basics

## 💡 Channel capacity — the two limits

📌 ⭐ **Nyquist (NOISELESS channel): C = 2B log₂ L** bps
where B = bandwidth in Hz, L = number of distinct signal levels.
💡 *The limit imposed by bandwidth alone.* More signal levels → more bits per symbol.

📌 ⭐ **Shannon (NOISY channel): C = B log₂(1 + S/N)** bps
💡 *The limit imposed by noise.* No amount of clever encoding beats it.

📌 **SNR in dB = 10 log₁₀(S/N)** — so to convert back, S/N = 10^(dB/10).

### 🔢 Worked examples

🔢 **B = 3000 Hz, S/N = 3:**
C = 3000 × log₂(1 + 3) = 3000 × log₂4 = 3000 × 2 = ⭐ **6000 bps**

🔢 **B = 3000 Hz, SNR = 30 dB:**
S/N = 10^(30/10) = 1000 → C = 3000 × log₂1001 ≈ 3000 × 9.97 ≈ ⭐ **29,900 bps**
*(This is roughly why an old dial-up telephone line topped out near 30 kbps on a plain modem.)*

🔢 **Nyquist with 4 levels, B = 3000 Hz:** C = 2 × 3000 × log₂4 = **12,000 bps**

⭐ **In practice you compute both and take the SMALLER** — the channel is limited by whichever constraint bites first.

## Other physical-layer items

**Transmission modes:** simplex (one way) · half-duplex (both ways, one at a time) · full-duplex (both simultaneously).
**Multiplexing:** FDM (frequency) · TDM (time — synchronous or statistical) · WDM (wavelength, for fibre) · CDM (code).
**Media:** twisted pair (UTP/STP) · coaxial · ⭐ **optical fibre** (highest bandwidth, immune to EMI, no crosstalk, hard to tap) · wireless.
**Topologies:** bus · star · ring · **mesh** (📌 a full mesh of n nodes needs ⭐ **n(n−1)/2** links) · tree · hybrid.

---

# 3. ⭐⭐⭐ Data link layer

## 💡 What this layer must solve

The physical layer delivers a stream of bits, which may be corrupted, and the medium may be shared. So the data link layer must:
1. Mark where each **frame** starts and ends (**framing**)
2. **Detect** (and sometimes correct) errors
3. Stop a fast sender swamping a slow receiver (**flow control**)
4. Decide **whose turn it is** on a shared medium (**medium access control**)

## 3.1 ⭐ Framing

### 💡 The problem

The receiver gets `101100110111000...` — where does one frame end and the next begin?

| Method | 💡 How | Weakness |
|---|---|---|
| **Character/byte count** | Start each frame with its length | ⚠ If the count itself is corrupted, all subsequent framing is lost |
| **Character (byte) stuffing** | Delimit with a flag byte; insert an escape byte (DLE) before any accidental flag in the data | Byte-oriented only |
| ⭐ **Bit stuffing** | Flag = `01111110`. ⭐ **In the data, after five consecutive 1s, the sender INSERTS a 0** | The receiver removes it |
| **Physical layer coding violations** | Use an illegal signal pattern as a delimiter | Medium-specific |

💡 **Why bit stuffing works:** the flag is the only place six consecutive 1s can appear, because the sender guarantees the payload never contains more than five in a row.

🔢 Data `0111111111100` → after every run of five 1s, insert a 0:
`01111101111`**0**`1100` — the receiver strips the stuffed 0s.

## 3.2 ⭐⭐ Error detection

### 💡 Why redundancy is needed

You cannot detect an error by looking at data alone — any bit pattern is a valid pattern. You must send **extra bits** whose relationship to the data can be checked.

| Method | ⭐ Detects | 💡 Note |
|---|---|---|
| **Simple parity** | ⭐ **All ODD numbers of bit errors**; ⚠ **misses all EVEN-numbered errors** | 1 extra bit; weakest |
| **2-D parity** | All 1-, 2- and 3-bit errors; can **correct** single-bit errors | Parity per row and per column |
| **Checksum** (1's complement) | Used by IP, TCP, UDP | Weaker than CRC but cheap in software |
| ⭐ **CRC (Cyclic Redundancy Check)** | ⭐ **Strongest — all burst errors shorter than the generator's degree** | Cheap in hardware (a shift register); used by Ethernet |

### ⭐⭐ How CRC works

💡 **The idea:** treat the bit string as the coefficients of a polynomial, divide by an agreed **generator polynomial** using **modulo-2 (XOR) arithmetic**, and send the remainder along with the data. The receiver divides the whole received frame by the same generator; ⭐ **a remainder of 0 means no error was detected.**

**Sender's procedure:**
1. Let r = **degree** of the generator G (i.e. number of bits in G, minus 1)
2. **Append r zeros** to the data
3. Divide by G using **XOR** (no borrows, no carries)
4. The r-bit **remainder is the CRC**; transmit `data + CRC`

### 🔢 Worked example

**Data = `1010`, Generator G = `1011` (degree 3, so append 3 zeros).**

Dividend = `1010000`
```
        1001
     ┌────────
1011 │ 1010000
       1011          ← XOR
       ────
       0001000
          1011       ← XOR (shift until leading 1 aligns)
          ────
           0011      ← remainder (3 bits) = 011
```
⭐ **CRC = `011`. Transmitted frame = `1010` + `011` = `1010011`**

**Receiver:** divides `1010011` by `1011`. If the remainder is `000`, accept. ✅

## 3.3 ⭐⭐ Hamming distance and error correction

### 💡 The idea

📌 The **Hamming distance** between two codewords is the number of bit positions in which they differ.
📌 The **minimum Hamming distance d_min** of a code is the smallest distance between any two of its valid codewords.

💡 **Why d_min determines everything:** think of valid codewords as points in space and errors as small displacements.
- To **DETECT** up to d errors, no d-bit displacement may land you on another valid codeword. So the codewords must be at least **d + 1** apart.
- To **CORRECT** up to d errors, a corrupted word must still be unambiguously **closer** to its original than to any other codeword. That needs a "buffer zone" of d on each side, hence **2d + 1**.

📌 ⭐ **To DETECT up to d errors: d_min ≥ d + 1**
📌 ⭐ **To CORRECT up to d errors: d_min ≥ 2d + 1**

⚠⚠ ⭐ **These two are swapped constantly.** Detection needs **d+1**; correction needs **2d+1**. Correction is harder, so it needs the larger distance — use that to remember which is which.

🔢 A code with d_min = 3 can **detect 2** errors (3 ≥ 2+1 ✅) **or correct 1** error (3 ≥ 2×1+1 ✅).
🔢 A code with d_min = 5 can detect 4 errors or correct 2.

### ⭐⭐ Hamming code

📌 ⭐ **For m data bits, the number of parity bits r must satisfy: 2ʳ ≥ m + r + 1**

💡 **Why:** the r parity bits form a **syndrome** — an r-bit number. It must be able to indicate any of the **m + r** bit positions as the error location, **plus** the case "no error". That is m + r + 1 possibilities, needing 2ʳ ≥ m + r + 1.

🔢 m = 4 → try r = 3: 2³ = 8 ≥ 4 + 3 + 1 = 8 ✅ → the ⭐ **(7,4) Hamming code**
🔢 m = 8 → try r = 4: 2⁴ = 16 ≥ 8 + 4 + 1 = 13 ✅ → 4 parity bits
🔢 m = 11 → r = 4: 16 ≥ 11 + 4 + 1 = 16 ✅ → the (15,11) code

⭐ **Structure:** parity bits sit at positions **1, 2, 4, 8, …** (powers of 2). The parity bit at position 2ⁱ checks every position whose binary representation has bit i set.

⭐ **Syndrome decoding:** the binary number formed by the **failed** parity checks **is the position of the erroneous bit** — which you simply flip. Elegantly direct.

🔢 If parity checks at positions 1 and 4 fail, the syndrome is binary `101` = 5 → **bit 5 is wrong.**

## 3.4 ⭐⭐⭐ Flow control / sliding window protocols

### 💡 The problem

**Stop-and-Wait:** send one frame, wait for its acknowledgement, send the next.
Simple and correct — but catastrophically slow on a long link, because you spend one whole round-trip time idle per frame.

🔢 Transmission time 1 ms, propagation 4 ms each way. Per frame you spend 1 ms sending and 8 ms waiting → **1/9 of the capacity used.**

⭐ **The fix: SLIDING WINDOW.** Allow up to **W** unacknowledged frames in flight, so you keep the pipe full.

📌 ⭐ **Efficiency (utilisation) η = W / (1 + 2a)** where **a = T_propagation / T_transmission**

📌 ⭐ **Optimum window size for 100% utilisation = 1 + 2a**

💡 **Why 1 + 2a:** in the time it takes for the first ACK to come back (1 transmission time + 2 propagation times, all measured in units of transmission time), you could have sent 1 + 2a frames. Any larger window gains nothing.

### ⭐⭐ Go-Back-N vs Selective Repeat

| | **Stop-and-Wait** | ⭐ **Go-Back-N** | ⭐ **Selective Repeat** |
|---|---|---|---|
| Sender window | 1 | **N** | **N** |
| ⭐ **Receiver window** | 1 | ⭐ **1** | ⭐ **N** |
| ⭐ **Max window with m-bit seq. no.** | 1 (needs 1 bit) | ⭐ **2ᵐ − 1** | ⭐ **2ᵐ⁻¹** |
| On error | Retransmit that frame | ⭐ **Retransmit the lost frame AND ALL after it** | ⭐ **Retransmit ONLY the lost frame** |
| Receiver buffering | Not needed | ⭐ **Not needed** | ⭐ **Needed** |
| ACKs | Individual | **Cumulative** | **Individual** |
| NAK support | — | — | ✅ |
| Complexity | Simplest | Moderate | ⭐ **Most complex** |
| Bandwidth on errors | — | ⭐ **Wasteful** | ⭐ **Efficient** |

### 💡⭐ Why the maximum window sizes differ

⭐ **Go-Back-N needs 2ᵐ − 1** (one spare sequence number).
💡 *Why:* suppose m = 2 (sequence numbers 0,1,2,3) and the window were 4. The sender sends 0,1,2,3. All arrive but all ACKs are lost. The sender retransmits 0,1,2,3. The receiver, now expecting 0,1,2,3 again (it has advanced a full cycle), **cannot tell the retransmissions from new frames**. Leaving one number unused makes the windows non-overlapping and removes the ambiguity.

⭐ **Selective Repeat needs 2ᵐ⁻¹** (at most **half** the sequence space).
💡 *Why:* SR has a **receiver window too**, and it accepts out-of-order frames. Sender and receiver windows must never overlap ambiguously, and since both are size N, we need 2N ≤ 2ᵐ, i.e. N ≤ 2ᵐ⁻¹.

### 🔢 Worked examples

🔢 **T_trans = 1 ms, T_prop = 4 ms → a = 4.**
- Stop-and-Wait efficiency = 1/(1 + 8) = ⭐ **11.1%**
- With Go-Back-N, m = 3 bits → max window = 2³ − 1 = **7**; efficiency = 7/9 = ⭐ **77.8%**
- Optimum window for 100% = 1 + 2(4) = **9**, so a 4-bit sequence number (max window 15) would be needed.

🔢 **Selective Repeat with a 4-bit sequence number:** max window = 2³ = **8**.
🔢 **Go-Back-N with a 4-bit sequence number:** max window = 2⁴ − 1 = **15**.

## 3.5 ⭐⭐⭐ Medium Access Control (MAC)

### 💡 The problem

Several stations share one medium (a cable, or the air). If two transmit simultaneously, both signals are destroyed — a **collision**. Who goes when?

### ⭐ (a) Random access — ALOHA and CSMA

**Pure ALOHA** (1970, University of Hawaii): transmit whenever you have data; if no ACK arrives, wait a random time and retry.
📌 ⭐ **Maximum efficiency = 1/(2e) ≈ 18.4%** (at offered load G = 0.5)
💡 *Why so low:* a frame is destroyed if any other transmission starts within one frame-time **before or after** it — a **vulnerable period of 2 frame times**.

**Slotted ALOHA:** stations may only start at fixed slot boundaries.
📌 ⭐ **Maximum efficiency = 1/e ≈ 36.8%** (at G = 1)
💡 *Why exactly double:* slotting halves the vulnerable period to **1 frame time** — a collision now requires two stations to pick the *same* slot.

📌 Throughput formulas: pure ALOHA S = G·e^(−2G); slotted ALOHA S = G·e^(−G).

⭐ **CSMA (Carrier Sense Multiple Access)** — *"listen before you talk."* Much better, but collisions still occur because of propagation delay (two stations can both sense an idle channel and start together).
Variants: **1-persistent** (transmit as soon as idle) · **non-persistent** (wait a random time then re-sense) · **p-persistent**.

### ⭐⭐ (b) CSMA/CD — Ethernet

📌 ⭐ **CSMA with Collision Detection:** listen while transmitting; if a collision is detected, **abort immediately**, send a short **jam signal**, then **back off** and retry.

💡 *Why abort:* there is no point wasting the rest of the frame time on a frame that is already destroyed.

⭐ **Binary exponential backoff:** after the n-th collision, wait a random number of slot times chosen from **[0, 2ⁿ − 1]**. The range doubles each time (adapting to congestion), is **capped at n = 10**, and the station gives up after **16** attempts.

### ⭐⭐⭐ Minimum frame size — the key derivation

### 💡 The problem

Station A starts transmitting. Station B, at the far end, has not yet heard the signal (propagation delay) and starts too. The collision happens near B, and the damaged signal must travel back to A.

⭐ **If A has already FINISHED transmitting by the time the collision signal returns, A will never know its frame was destroyed** — and CSMA/CD breaks completely.

📌 ⭐ **Therefore: T_transmission ≥ 2 × T_propagation**
📌 ⭐ **Minimum frame size = 2 × T_propagation × Bandwidth**

### 🔢 Worked example

**10 Mbps Ethernet with a maximum round-trip propagation delay of 51.2 μs:**
```
Minimum frame size = 10⁷ bps × 51.2 × 10⁻⁶ s = 512 bits = 64 bytes
```
⭐ **This is exactly why Ethernet's minimum frame size is 64 bytes.** Frames shorter than that are padded.

🔢 **A different configuration:** 100 Mbps, 2.5 km cable, signal speed 2×10⁸ m/s.
One-way propagation = 2500/2×10⁸ = 12.5 μs → round trip = 25 μs.
Min frame = 10⁸ × 25×10⁻⁶ = 2500 bits = **312.5 bytes**.
⭐ (Fast Ethernet kept the 64-byte minimum by shortening the maximum cable length instead — the two are directly linked.)

### ⭐ (c) CSMA/CA — wireless

📌 ⭐ **Collision AVOIDANCE, used in 802.11 WiFi**, because collision **detection** is impractical on radio:
- A station cannot easily listen while transmitting (its own signal drowns everything)
- ⭐ **The hidden-terminal problem:** A and C can both reach B but cannot hear each other, so neither can detect the other's collision at B

⭐ **CSMA/CA mechanisms:** interframe spacing · random backoff **before** transmitting · ⭐ **RTS/CTS handshake** (request-to-send / clear-to-send reserves the channel and solves the hidden terminal problem) · explicit **ACKs** for every frame.

### (d) Controlled access and channelization
**Controlled:** reservation · polling · **token passing** (Token Ring, FDDI).
**Channelization:** FDMA · TDMA · CDMA (see Week 9).

## 3.6 ⭐⭐ Ethernet and bridging

### ⭐ Ethernet (IEEE 802.3) frame format

```
┌──────────┬─────┬────────┬────────┬─────────┬───────────┬─────┐
│ Preamble │ SFD │ Dest   │ Source │ Length/ │   DATA    │ CRC │
│   7 B    │ 1 B │ MAC 6B │ MAC 6B │ Type 2B │ 46–1500 B │ 4 B │
└──────────┴─────┴────────┴────────┴─────────┴───────────┴─────┘
```
📌 ⭐ **Frame size range: 64 to 1518 bytes** (excluding preamble/SFD)
📌 ⭐ **MTU (maximum payload) = 1500 bytes**
📌 Minimum payload = 46 bytes (padded if less), so that 6+6+2+46+4 = **64 bytes** minimum ✅

📌 ⭐ **MAC address = 48 bits (6 bytes)**, written as 12 hex digits. The first 24 bits are the **OUI** (manufacturer). Broadcast = `FF:FF:FF:FF:FF:FF`.

### ⭐⭐ Devices, collision domains and broadcast domains

| Device | ⭐ Layer | ⭐ Collision domains | ⭐ Broadcast domains |
|---|---|---|---|
| **Hub / Repeater** | ⭐ **1 (Physical)** | ⭐ **1 (all ports share one)** | 1 |
| **Bridge / Switch** | ⭐ **2 (Data link)** | ⭐ **One PER PORT** | 1 (unless VLANs) |
| ⭐ **Router** | ⭐ **3 (Network)** | One per port | ⭐ **One PER PORT — SEPARATES broadcast domains** |

📌 ⭐⭐ **Only a ROUTER (or a VLAN) separates broadcast domains. A switch separates collision domains but FORWARDS broadcasts.**

💡 **Why:** a switch's job is to deliver frames within one LAN, and a broadcast is addressed to the whole LAN — so it must be flooded. A router's job is to connect *different* networks, and it does not forward layer-2 broadcasts across them.

🔢 A switch with 24 ports creates **24 collision domains** and **1 broadcast domain**. A router with 4 interfaces creates **4 broadcast domains**.

### ⭐ How a switch works
1. **Learns:** records the source MAC of every incoming frame against the port it arrived on, building a **MAC address table**.
2. **Forwards:** if the destination MAC is in the table, sends the frame out that one port only.
3. ⭐ **Floods:** if the destination is **unknown**, or is a **broadcast/multicast**, sends it out **all ports except the incoming one**.

⭐ **Spanning Tree Protocol (STP, IEEE 802.1D)** disables redundant links to prevent **broadcast storms** and forwarding loops (a layer-2 loop has no TTL to stop it, so it would circulate forever).

**Switching methods:** store-and-forward (full frame, CRC checked) · cut-through (forwards after reading the destination — fastest, no error check) · fragment-free.

---

# 4. ⭐⭐⭐ Network layer

## 4.1 ⭐⭐ The IPv4 header

```
 0                   8                  16                              31
┌──────┬──────┬──────────────┬───────────────────────────────────────────┐
│Ver(4)│IHL(4)│    ToS (8)   │            Total Length (16)              │
├──────┴──────┴──────────────┼───────┬───────────────────────────────────┤
│      Identification (16)   │Flags 3│      Fragment Offset (13)         │
├─────────────┬──────────────┼───────┴───────────────────────────────────┤
│   TTL (8)   │ Protocol (8) │          Header Checksum (16)             │
├─────────────┴──────────────┴───────────────────────────────────────────┤
│                        Source IP Address (32)                          │
├────────────────────────────────────────────────────────────────────────┤
│                      Destination IP Address (32)                       │
├────────────────────────────────────────────────────────────────────────┤
│                    Options (0–40 bytes) + Padding                      │
└────────────────────────────────────────────────────────────────────────┘
```

| Field | Size | ⭐ Note |
|---|---|---|
| Version | 4 bits | 4 for IPv4 |
| ⭐ **IHL** | 4 bits | Header length in **4-byte words**. ⭐ **Min 5 (=20 bytes), max 15 (=60 bytes)** |
| ToS / DSCP | 8 bits | Quality of service |
| ⭐ **Total Length** | 16 bits | Header + data. ⭐ **Max 65,535 bytes** |
| ⭐ **Identification** | 16 bits | ⭐ **Same for all fragments of one datagram** |
| ⭐ **Flags** | 3 bits | Reserved, **DF** (Don't Fragment), ⭐ **MF** (More Fragments) |
| ⭐ **Fragment Offset** | 13 bits | ⭐ **Measured in units of 8 BYTES** |
| ⭐ **TTL** | 8 bits | Decremented by **each router**; at 0 the packet is discarded and an ICMP Time Exceeded is sent. ⭐ **Prevents packets looping forever** |
| **Protocol** | 8 bits | ⭐ **TCP = 6, UDP = 17, ICMP = 1** |
| **Header Checksum** | 16 bits | ⭐ **Covers the HEADER ONLY**, and must be recomputed at every hop (because TTL changes) |
| Source / Destination IP | 32 bits each | |

📌 ⭐ **IPv4 header: minimum 20 bytes, maximum 60 bytes.**

## 4.2 ⭐⭐ Fragmentation

### 💡 The idea

Different links have different **MTUs** (maximum transmission units) — Ethernet 1500 bytes, some tunnels less. A large datagram crossing onto a small-MTU link must be **fragmented** into pieces.

⭐ **Three rules:**
📌 ⭐ **The fragment offset is measured in 8-byte units**, so every fragment except the last must carry a payload that is a **multiple of 8 bytes**.
📌 ⭐ **MF = 1 on all fragments except the last** (MF = 0 marks the last).
📌 ⭐ All fragments of one datagram share the same **Identification** value.

⭐⭐ **Reassembly happens ONLY at the FINAL DESTINATION — never at intermediate routers.**
💡 **Why:** fragments may take different routes, so no single intermediate router is guaranteed to see them all. Also, reassembling and re-fragmenting at every hop would be wasteful.

### 🔢⭐ Worked example

**A 4000-byte datagram (20-byte header + 3980 bytes of data) crosses a link with MTU 1500.**

Each fragment can carry at most 1500 − 20 = **1480 bytes** of data. Check: 1480 ÷ 8 = 185 ✅ (a multiple of 8)

| Fragment | Data bytes | Byte range | ⭐ Offset field (÷8) | ⭐ MF | Total length |
|---|---|---|---|---|---|
| 1 | 1480 | 0–1479 | **0** | **1** | 1500 |
| 2 | 1480 | 1480–2959 | **185** | **1** | 1500 |
| 3 | 1020 | 2960–3979 | **370** | **0** | 1040 |

Check: 1480 + 1480 + 1020 = 3980 ✅

🔢 **Another:** a 2400-byte datagram (20 hdr + 2380 data) onto an MTU of 700.
Max data per fragment = 680, but 680 ÷ 8 = 85 ✅ so 680 works.
Fragments: 680, 680, 680, 340 → offsets **0, 85, 170, 255**; MF = 1,1,1,**0**.

## 4.3 ⭐⭐ IPv4 addressing

📌 A 32-bit address, written as four dotted decimal octets (`192.168.1.1`), split into a **network part** and a **host part**.

### ⭐ Classful addressing (historical, but still asked)

| Class | Leading bits | First octet | ⭐ Default mask | Network / host bits |
|---|---|---|---|---|
| **A** | 0 | **1–126** | 255.0.0.0 (**/8**) | 8 / 24 |
| **B** | 10 | **128–191** | 255.255.0.0 (**/16**) | 16 / 16 |
| **C** | 110 | **192–223** | 255.255.255.0 (**/24**) | 24 / 8 |
| **D** | 1110 | **224–239** | — | ⭐ **MULTICAST** |
| **E** | 1111 | 240–255 | — | Reserved/experimental |

⭐ **Why classful addressing was abandoned:** an organisation needing 300 hosts had to take a whole Class B (65,534 addresses), wasting 65,000. **CIDR** (§4.4) fixed this.

### ⭐ Reserved and special addresses

| Range | ⭐ Purpose |
|---|---|
| ⭐ **127.0.0.0/8** | ⭐ **LOOPBACK** (127.0.0.1 = "this machine") |
| ⭐ **10.0.0.0/8** | ⭐ Private (Class A range) |
| ⭐ **172.16.0.0/12** | ⭐ Private (Class B range) |
| ⭐ **192.168.0.0/16** | ⭐ Private (Class C range) |
| **169.254.0.0/16** | Link-local (APIPA — self-assigned when DHCP fails) |
| **0.0.0.0** | This host / the default route |
| **255.255.255.255** | Limited broadcast (not forwarded by routers) |

⭐ **Private addresses are not routable on the Internet** — they must be translated by **NAT** (§4.7).

## 4.4 ⭐⭐⭐ Subnetting and CIDR

> ⭐⭐ **This is the single most reliably asked topic in the networks section. Make it a 30-second reflex.**

### 💡 The idea

📌 **CIDR notation** `a.b.c.d/n` means "the first **n** bits are the network part; the remaining 32 − n are for hosts."

The **subnet mask** is simply n ones followed by (32 − n) zeros, written in dotted decimal.

📌 ⭐ **Host bits = 32 − prefix**
📌 ⭐ **Total addresses in a block = 2^(32 − prefix)**
📌 ⭐⭐ **USABLE HOSTS = 2^(32 − prefix) − 2**

⭐ **Why minus 2:** two addresses in every block are reserved —
- the **all-zeros** host part = the **network address** (identifies the network itself)
- the **all-ones** host part = the **broadcast address**

📌 **Number of subnets created by borrowing k host bits = 2ᵏ**
📌 ⭐ **Block size (the increment in the last varying octet) = 256 − (that octet's mask value)**

### ⭐⭐ The table to memorise

| Prefix | Mask (last octet) | Addresses | ⭐ Usable hosts |
|---|---|---|---|
| /24 | 0 | 256 | 254 |
| /25 | **128** | 128 | 126 |
| ⭐ **/26** | ⭐ **192** | 64 | ⭐ **62** |
| ⭐ **/27** | ⭐ **224** | 32 | ⭐ **30** |
| /28 | **240** | 16 | 14 |
| /29 | **248** | 8 | 6 |
| ⭐ **/30** | ⭐ **252** | 4 | ⭐ **2** (point-to-point links) |
| /31 | 254 | 2 | 0 (special RFC 3021 use) |
| /32 | 255 | 1 | A single host route |

| Prefix | Mask | Addresses |
|---|---|---|
| /16 | 255.255.0.0 | 65,536 |
| ⭐ **/20** | 255.255.**240**.0 | ⭐ **4096** |
| /21 | 255.255.248.0 | 2048 |
| /22 | 255.255.252.0 | 1024 |
| /23 | 255.255.254.0 | 512 |

⭐ **Memory hook for the mask values: 128, 192, 224, 240, 248, 252, 254, 255.** Each is the previous plus the next halving (128, +64, +32, +16, +8, +4, +2, +1).

### 🔢⭐ Worked example 1 — the standard question

**`192.168.10.0/26`**
```
Host bits       = 32 − 26 = 6
Total addresses = 2⁶ = 64
Usable hosts    = 64 − 2 = 62        ⭐
Subnets from /24= 2⁽²⁶⁻²⁴⁾ = 4
Mask            = 255.255.255.192
Block size      = 256 − 192 = 64
```
**The four subnets:**

| Subnet | Network | Usable range | Broadcast |
|---|---|---|---|
| 1 | .0 | .1 – .62 | **.63** |
| 2 | .64 | .65 – .126 | **.127** |
| 3 | .128 | .129 – .190 | **.191** |
| 4 | .192 | .193 – .254 | **.255** |

### 🔢⭐ Worked example 2 — "which subnet does this address belong to?"

**Which subnet contains `200.10.5.100/27`?**
```
Mask last octet = 224   →  Block size = 256 − 224 = 32
Boundaries: .0, .32, .64, .96, .128, .160, .192, .224
100 falls between 96 and 127
```
⭐ **Network = 200.10.5.96 · Broadcast = 200.10.5.127 · Usable = .97 – .126**

⭐ **The trick: divide the host address by the block size and take the floor.** 100 ÷ 32 = 3.125 → 3 × 32 = **96** ✅

### 🔢 Worked example 3

**`172.16.0.0/20`**
```
Host bits = 12  →  2¹² = 4096 addresses, 4094 usable
Mask = 255.255.240.0
```
⭐ Blocks: 172.16.0.0, 172.16.16.0, 172.16.32.0, 172.16.48.0, …
*(Block size in the third octet = 256 − 240 = 16.)*

### 🔢 Worked example 4 — designing subnets

**You have `192.168.1.0/24` and need 5 subnets, each with at least 25 hosts.**
- 25 hosts needs 5 host bits (2⁵ − 2 = 30 ✅; 4 bits gives only 14)
- So the prefix is 32 − 5 = **/27**
- Subnets available: 2^(27−24) = **8** ≥ 5 ✅
⭐ **Answer: /27, giving 8 subnets of 30 usable hosts each.**

### ⭐ Supernetting / route aggregation

💡 The reverse of subnetting: combine several contiguous blocks into one shorter prefix, so routers can advertise **one** route instead of many. This is what keeps the global routing table manageable.

⭐ **Requirements:** the blocks must be **contiguous**, their count must be a **power of 2**, and the first block must be **aligned** on that boundary.

🔢 `192.168.0.0/24`, `192.168.1.0/24`, `192.168.2.0/24`, `192.168.3.0/24` (4 blocks) aggregate to ⭐ **`192.168.0.0/22`** ✅
🔢 `192.168.1.0/24` … `192.168.4.0/24` (4 blocks) — ❌ **cannot** aggregate, because they are not aligned (1 is not a multiple of 4).

⭐ **VLSM (Variable Length Subnet Masking):** use different subnet sizes within one network. ⭐ **Strategy: allocate the LARGEST requirement first**, then work downwards, so you never fragment a block you needed whole.

## 4.5 ⭐ IPv6

📌 **128 bits**, written as eight groups of four hex digits, with `::` compressing **one** run of zero groups.
🔢 `2001:0db8:0000:0000:0000:ff00:0042:8329` → `2001:db8::ff00:42:8329`

⭐ **Key differences from IPv4:**
📌 ⭐ **Fixed 40-byte header** (larger than IPv4's *minimum* 20, but **fixed** and much simpler)
📌 ⭐ **No header checksum** (layers above and below already check) — so routers do no per-hop recomputation
📌 ⭐ **Routers do NOT fragment** — the **source** does path MTU discovery
📌 **Extension headers** carry options instead of a variable-length header
📌 ⭐ **Address types: unicast, multicast, ANYCAST — there is NO BROADCAST in IPv6** (its role is taken by multicast to the all-nodes group)
📌 **SLAAC** — stateless address autoconfiguration

**Transition mechanisms:** dual stack · tunnelling · translation (NAT64).

## 4.6 ⭐⭐⭐ Routing

### 💡 The problem

A router receives a packet for `203.0.113.5`. Which of its interfaces should it use? It consults a **routing table** — and the interesting question is how that table gets built.

### ⭐ The four approaches

| Approach | 💡 Mechanism | Convergence | Knowledge each router has |
|---|---|---|---|
| **Flooding** | Send on every link except the incoming one | — | None. Robust but massively wasteful |
| ⭐ **Distance vector** | Exchange **distance vectors** with **DIRECT NEIGHBOURS only**, periodically | ⭐ **SLOW** | Only distances, not topology |
| ⭐ **Link state** | **FLOOD** link-state information to **ALL routers**; each builds the complete map and runs Dijkstra locally | ⭐ **FAST** | ⭐ **The FULL topology** |
| **Path vector** | Advertise complete AS paths | — | Used by BGP for policy routing |

### ⭐⭐ Distance vector routing (Bellman–Ford based; RIP)

💡 **How it works:** each router keeps a table of `(destination, cost, next hop)`. Periodically it tells its neighbours its costs. On receiving a neighbour's vector, it checks whether going *via* that neighbour is cheaper.

📌 **Update rule:** `cost(me → D) = min over neighbours N of [ cost(me → N) + cost(N → D) ]`

⚠⚠ ⭐ **The count-to-infinity problem**

💡 **What goes wrong:** *good news travels fast, bad news travels slowly.*

🔢 A — B — C, and A goes down.
- B notices A is unreachable, but **C still advertises "I can reach A in 2 hops"** (via B — C does not know that).
- B believes C and records "A is 3 hops away, via C".
- B tells C, which now records 4. Then 5, 6, 7… **counting up to infinity.**
- The routers form a routing loop, bouncing packets between B and C, for many update cycles.

⭐ **Mitigations:**
- ⭐ **Split horizon** — never advertise a route back out on the interface you learned it from (C would not tell B about A)
- ⭐ **Poison reverse** — actively advertise such a route back with cost ∞
- **Hold-down timers** — ignore updates about a route for a while after it goes down
- ⭐ **Define a small "infinity"** — ⭐ **RIP uses 16 as infinity**, so the maximum usable hop count is **15**, bounding how long the counting can last

### ⭐⭐ Link state routing (OSPF)

💡 **How it works:** each router discovers its directly attached links and their costs, packages that into a **Link State Advertisement (LSA)**, and **floods** it to every router. Every router thus ends up with an **identical map** of the network, and independently runs ⭐ **Dijkstra's algorithm** to compute its own shortest-path tree.

| | ⭐ **Distance vector** | ⭐ **Link state** |
|---|---|---|
| What is shared | Its **distance table** | Its **link states** |
| Shared with | **Neighbours only** | ⭐ **ALL routers (flooded)** |
| Knowledge | Distances only | ⭐ **Full topology** |
| Algorithm | Bellman–Ford | ⭐ **Dijkstra** |
| Convergence | ⭐ **Slow** | ⭐ **Fast** |
| Count-to-infinity | ⭐ **✅ Suffers** | ⭐ **❌ Immune** |
| Memory/CPU | Low | Higher |
| Example | ⭐ **RIP** | ⭐ **OSPF** |

### ⭐⭐ The protocols

| Protocol | ⭐ Type | Metric | Scope |
|---|---|---|---|
| ⭐ **RIP** | ⭐ **Distance vector** | ⭐ **Hop count (max 15, infinity = 16)** | Interior (IGP) |
| ⭐ **OSPF** | ⭐ **LINK STATE (Dijkstra)** | Cost, derived from bandwidth | Interior (IGP) |
| **IGRP / EIGRP** | Advanced/hybrid DV | Composite (bandwidth, delay) | Interior (Cisco) |
| ⭐ **BGP** | ⭐ **PATH VECTOR** | ⭐ **Policy-based** | ⭐ **EXTERIOR (EGP) — between autonomous systems** |

⭐ **BGP is the routing protocol of the Internet between ISPs.** It chooses routes on business/policy grounds, not just shortest path.

### ⭐⭐ Longest prefix match

📌 ⭐ **When several routing-table entries match a destination, the router uses the one with the LONGEST prefix (most specific).**

🔢 Destination `192.168.1.130`. Table contains:
```
192.168.0.0/16   → Interface A
192.168.1.0/24   → Interface B
192.168.1.128/25 → Interface C
```
All three match. ⭐ **The /25 is the longest → Interface C.**

💡 **Why:** a longer prefix describes a smaller, more specific set of addresses — presumably a deliberate, more precise route.

**Also:** static vs dynamic routing · unicast vs **multicast** (IGMP, PIM, DVMRP) vs broadcast vs anycast.

## 4.7 ⭐⭐ IP support protocols

### ⭐ ARP (Address Resolution Protocol)

💡 **The problem:** you know a machine's **IP** address, but to put a frame on the local Ethernet you need its **MAC** address. Someone must translate.

📌 ⭐ **ARP maps IP → MAC.**

**How:** broadcast *"who has 192.168.1.5?"* to the whole LAN; the owner replies **unicast** with its MAC. Results are cached in the **ARP table** (with a timeout).

⚠ **RARP** does the reverse (MAC → IP) and is obsolete — replaced by DHCP.
⚠ ARP is **local only** — it never crosses a router. To reach a remote host you ARP for your **default gateway's** MAC.

### ⭐ DHCP (Dynamic Host Configuration Protocol)

💡 Automatically hands a joining machine its **IP address, subnet mask, default gateway and DNS servers** — so you never configure a laptop by hand.

📌 ⭐ **The DORA sequence:**
1. ⭐ **D**iscover — the client broadcasts "is there a DHCP server?"
2. ⭐ **O**ffer — server(s) offer an address
3. ⭐ **R**equest — the client requests one specific offer
4. ⭐ **A**cknowledge — the server confirms and records the **lease**

📌 ⭐ **Ports 67 (server) / 68 (client), over UDP.**
💡 *Why UDP:* the client has no IP address yet, so it cannot establish a TCP connection.

### ⭐ ICMP (Internet Control Message Protocol)

💡 IP itself has no way to report problems. ICMP is the **error-reporting and diagnostic** companion to IP.

| Message | Used by / meaning |
|---|---|
| ⭐ **Echo Request / Echo Reply** | ⭐ **`ping`** — is the host reachable? |
| **Destination Unreachable** | No route / port closed |
| ⭐ **Time Exceeded** | TTL hit 0 — ⭐ **this is how `traceroute` works** (send packets with TTL 1, 2, 3… and see who complains) |
| **Redirect** | "Use a better gateway" |
| **Source Quench** | Congestion (deprecated) |

⚠ ⭐ **ICMP REPORTS errors; it does NOT correct them.**
⚠ ⭐ **ICMP has no port numbers** (it is not a transport protocol — it rides directly on IP, protocol number 1).

### ⭐⭐ NAT (Network Address Translation)

### 💡 The idea and why it exists

IPv4 has ~4 billion addresses, which ran out. But a home with 10 devices does not need 10 *public* addresses — only the ability to reach the Internet.

📌 ⭐ **NAT rewrites the private source IP (and, in PAT, the source port) in outgoing packets to the router's single public IP, and reverses the translation on the replies.**

```
Private LAN                 NAT router              Internet
192.168.1.10:5000  ────►  203.0.113.5:40001  ────►  server
192.168.1.11:5000  ────►  203.0.113.5:40002  ────►  server
```
⭐ The **port number** is what lets the router tell the two devices' replies apart — hence "PAT" (Port Address Translation) or "NAT overload".

| Type | 💡 Mapping |
|---|---|
| **Static NAT** | One private ↔ one public (permanent) |
| **Dynamic NAT** | Private addresses drawn from a **pool** of public ones |
| ⭐ **PAT / NAT overload** | ⭐ **MANY private → ONE public**, distinguished by port number. What every home router does |

⭐ **Benefits:** conserves IPv4 addresses; hides the internal topology (a mild security side-effect).
⚠ ⭐ **Drawbacks:** breaks **end-to-end connectivity** (an outside host cannot initiate a connection inward without port forwarding); complicates peer-to-peer, VoIP and some protocols like FTP; and it **violates the layering principle** — a layer-3 device inspecting and rewriting layer-4 port numbers.

---

# 5. ⭐⭐⭐ Transport layer

## 5.1 💡 What this layer adds

The network layer delivers packets **host to host**, unreliably. The transport layer adds:
1. ⭐ **Process-to-process delivery** via **port numbers** (which of the 50 programs on this machine should get this data?)
2. **Reliability** — detect and retransmit losses (TCP)
3. **Ordering** — reassemble in sequence (TCP)
4. **Flow control** — don't swamp the receiver
5. **Congestion control** — don't swamp the network

## 5.2 ⭐⭐⭐ TCP vs UDP

| | ⭐ **TCP** | ⭐ **UDP** |
|---|---|---|
| Connection | ⭐ **Connection-oriented** (handshake first) | ⭐ **Connectionless** (just send) |
| Reliability | ⭐ **Reliable** — ACKs + retransmission | ⭐ **Unreliable, best-effort** |
| Ordering | ✅ Guaranteed | ❌ Not guaranteed |
| ⭐ **Header size** | ⭐ **20–60 bytes** | ⭐ **8 bytes** |
| Flow control | ✅ Sliding window | ❌ |
| Congestion control | ✅ | ❌ |
| Duplicate detection | ✅ | ❌ |
| Speed / overhead | Slower, higher | ⭐ **Faster, minimal** |
| Data unit | **Segment** (a byte **stream**) | **Datagram** (discrete **messages**) |
| ⭐ **Typical uses** | HTTP, FTP, SMTP, SSH, Telnet | ⭐ **DNS, DHCP, TFTP, SNMP, RIP**, VoIP, video streaming, online games |

💡 **Why anyone would choose UDP:** for a live video call, a packet that arrives 500 ms late is **useless** — retransmitting it would only add delay and jitter. Better to drop it and move on. UDP's "unreliability" is a **feature** for real-time traffic.

💡 **Why DNS uses UDP:** a query and its reply are one small packet each. Setting up a TCP connection (3 packets) to send 1 packet would triple the cost. If the reply is lost, just ask again.

## 5.3 ⭐⭐ The TCP header

```
 0                  16                                  31
┌──────────────────────┬──────────────────────────────────┐
│   Source Port (16)   │     Destination Port (16)        │
├──────────────────────┴──────────────────────────────────┤
│              ⭐ Sequence Number (32)                     │
├─────────────────────────────────────────────────────────┤
│           ⭐ Acknowledgement Number (32)                 │
├────────┬──────┬──────────┬──────────────────────────────┤
│HLEN(4) │Rsv(6)│⭐Flags(6)│      ⭐ Window Size (16)      │
├────────┴──────┴──────────┼──────────────────────────────┤
│    Checksum (16)         │     Urgent Pointer (16)      │
├──────────────────────────┴──────────────────────────────┤
│                Options (0–40 bytes)                     │
└─────────────────────────────────────────────────────────┘
```

⭐ **The six flags: URG, ACK, PSH, RST, SYN, FIN**

📌 ⭐ **Sequence numbers count BYTES, not segments.** This is why TCP is a byte-stream protocol.
📌 ⭐ **The window size field is 16 bits**, capping the window at 65,535 bytes. The **window scaling** option extends this for high-bandwidth links (recall the bandwidth–delay product from §1.5).

## 5.4 ⭐⭐ Connection management

### ⭐⭐ The three-way handshake (establishment)

```
Client                                    Server
  │                                          │
  │──────── SYN, seq = x ───────────────────►│    "I want to connect,
  │                                          │     my sequence starts at x"
  │◄─────── SYN + ACK, seq = y, ack = x+1 ───│    "OK, mine starts at y,
  │                                          │     I got your x"
  │──────── ACK, ack = y+1 ─────────────────►│    "I got your y"
  │                                          │
  │══════════ ESTABLISHED ═══════════════════│
```

💡 **Why THREE messages and not two?** Both sides must agree on **both** initial sequence numbers, and each must know the other has received its own. Two messages would leave the *client's* sequence number unconfirmed. (Three is provably the minimum for reliable two-way agreement.)

### ⭐ The four-way teardown

```
Client ──── FIN ────► Server        "I'm done sending"
Client ◄─── ACK ───── Server        "OK"
                                    (server may still send data — HALF-OPEN)
Client ◄─── FIN ───── Server        "Now I'm done too"
Client ──── ACK ────► Server        "OK"
Client waits in TIME_WAIT (2 × MSL)
```

📌 ⭐⭐ **Establishment is 3 segments; termination is 4.**
💡 **Why 4:** a TCP connection is two independent one-way streams, each closed separately. This allows a **half-open** state where one side has finished but the other is still sending.

⭐ **TIME_WAIT (2 × MSL)** ensures that delayed duplicate segments from this connection expire before the same port pair can be reused.

**States:** CLOSED, LISTEN, SYN_SENT, SYN_RECEIVED, ESTABLISHED, FIN_WAIT_1/2, CLOSE_WAIT, LAST_ACK, TIME_WAIT.

## 5.5 ⭐ Flow control

📌 ⭐ **Purpose: stop a fast sender overwhelming a SLOW RECEIVER.**

**Mechanism:** the receiver advertises its free buffer space in the **window size** field of every ACK. The sender may not have more than that much unacknowledged data in flight. A **zero window** stops the sender until an update arrives.

⭐ **Silly Window Syndrome** — the connection degenerates into sending tiny segments (a 40-byte header carrying 1 byte of data). Two fixes:
- ⭐ **Nagle's algorithm** (sender side) — buffer small writes until either a full segment accumulates or an ACK arrives
- ⭐ **Clark's solution / delayed ACK** (receiver side) — do not advertise a tiny window; wait until a decent amount of buffer is free

📌 ⭐ **Effective window = min(receiver window, congestion window)**

## 5.6 ⭐⭐⭐ Congestion control

### 💡 Flow control vs congestion control

⚠⚠ ⭐ **These are DIFFERENT mechanisms solving DIFFERENT problems:**
- ⭐ **Flow control** protects the **RECEIVER** (its buffer is finite). Feedback comes explicitly, via the window field.
- ⭐ **Congestion control** protects the **NETWORK** (routers' queues are finite). Feedback is **implicit** — TCP infers congestion from **packet loss**.

💡 **Why loss implies congestion:** on wired links, bit errors are rare. So a lost packet almost always means a router queue overflowed. TCP treats loss as its congestion signal.

### ⭐⭐ The four phases

| Phase | ⭐ Behaviour |
|---|---|
| ⭐ **1. Slow start** | cwnd starts at **1 MSS** and ⭐ **DOUBLES every RTT (EXPONENTIAL growth)** until it reaches `ssthresh` |
| ⭐ **2. Congestion avoidance** | cwnd increases by ⭐ **1 MSS per RTT (LINEAR / additive increase)** |
| ⭐ **3. Fast retransmit** | On ⭐ **3 DUPLICATE ACKs**, retransmit the missing segment **immediately**, without waiting for a timeout |
| ⭐ **4. Fast recovery** | ssthresh = cwnd/2; cwnd = ssthresh; resume **congestion avoidance** (TCP Reno) |

⭐ **On a TIMEOUT (severe congestion):** ssthresh = cwnd/2, ⭐ **cwnd RESETS to 1**, and slow start begins again.

📌 ⭐ **The overall behaviour is AIMD — Additive Increase, Multiplicative Decrease.**

💡 **Why "slow start" is a misleading name:** it starts *small* but grows *exponentially* — the fastest growth phase. It is called "slow" only relative to the pre-1988 behaviour of blasting a full window immediately.

💡 **Why three duplicate ACKs?** One or two duplicates could be caused by simple reordering. Three is strong evidence of an actual loss, and waiting for the (much longer) timeout would waste a full RTO.

### 🔢⭐ Worked example

**cwnd = 1 MSS, ssthresh = 8 MSS.**

| RTT | cwnd | Phase |
|---|---|---|
| 1 | 1 | Slow start |
| 2 | 2 | Slow start (×2) |
| 3 | 4 | Slow start (×2) |
| 4 | **8** | Slow start — **ssthresh reached, switch to linear** |
| 5 | 9 | Congestion avoidance (+1) |
| 6 | 10 | Congestion avoidance (+1) |
| 7 | 11 | Congestion avoidance (+1) |

**Now suppose a TIMEOUT occurs at cwnd = 12:**
```
ssthresh = 12/2 = 6
cwnd     = 1              ⭐ full reset
→ slow start again: 1, 2, 4, then 6 (ssthresh) → linear from there
```

**Instead, suppose 3 duplicate ACKs occur at cwnd = 12 (fast recovery):**
```
ssthresh = 6
cwnd     = 6              ⭐ NOT reset to 1
→ continue in congestion avoidance
```
⭐ **That distinction — timeout resets to 1, three duplicate ACKs halve instead — is the point of fast recovery.**

**Congestion control approaches:** open loop (prevention) vs closed loop (detect and react).
**Traffic shaping:** ⭐ **leaky bucket** (constant output rate — smooths completely, no bursts allowed) vs ⭐ **token bucket** (accumulates tokens, so **bursts are permitted** up to the bucket size). **ECN**, **RED** (Random Early Detection).

**TCP variants:** Tahoe (no fast recovery) · ⭐ **Reno** (adds fast recovery) · New Reno · **CUBIC** (Linux default) · BBR.

## 5.7 Sockets and ports

📌 ⭐ **A socket = (IP address, port number).**
📌 ⭐ **A TCP connection is identified by the 4-TUPLE: (source IP, source port, destination IP, destination port).**
💡 This is why one server on port 80 can serve thousands of clients — each connection has a distinct 4-tuple.

📌 ⭐ **Port ranges:** well-known **0–1023** · registered **1024–49151** · dynamic/ephemeral **49152–65535**

**Socket API sequence:**
```
Server: socket() → bind() → listen() → accept() → send/recv → close()
Client: socket() → connect() → send/recv → close()
```

---

# 6. ⭐⭐⭐ Application layer

## 6.1 ⭐⭐⭐ Well-known port numbers — memorise this table

| Port | Protocol | Transport |
|---|---|---|
| ⭐ **20 / 21** | ⭐ **FTP** (data / control) | TCP |
| **22** | SSH | TCP |
| **23** | Telnet | TCP |
| ⭐ **25** | ⭐ **SMTP** | TCP |
| ⭐ **53** | ⭐ **DNS** | ⭐ **UDP** (TCP for zone transfers & large replies) |
| ⭐ **67 / 68** | ⭐ **DHCP** (server / client) | UDP |
| **69** | TFTP | UDP |
| ⭐ **80** | ⭐ **HTTP** | TCP |
| **110** | POP3 | TCP |
| **143** | IMAP | TCP |
| **161 / 162** | SNMP | UDP |
| ⭐ **443** | ⭐ **HTTPS** | TCP |
| **3306** | MySQL | TCP |

## 6.2 ⭐⭐ DNS

### 💡 The idea

Humans use names (`tpsc.tripura.gov.in`); the network needs numbers (`203.0.113.5`). **DNS** is the global, distributed, hierarchical database that translates one to the other.

⭐ **Why distributed and not one giant table?** A single server would be a bottleneck, a single point of failure, and impossible to keep updated. So authority is **delegated** down a hierarchy.

```
                    . (root)
              /        |        \
           .com      .in      .org
                    /    \
                .gov.in  .ac.in
                  /
            tripura.gov.in
                /
        tpsc.tripura.gov.in
```

### ⭐ Recursive vs iterative resolution

| | ⭐ **Recursive** | ⭐ **Iterative** |
|---|---|---|
| The client asks | One server, and gets the **final answer** | One server, and gets a **REFERRAL** to the next |
| Who does the work | ⭐ **The server** chases the chain | ⭐ **The client** chases the chain |
| Typical use | Client → its local/ISP resolver | Resolver → root → TLD → authoritative |

⭐ **In practice both are used:** your laptop makes a **recursive** query to your ISP's resolver, which then makes a series of **iterative** queries up the hierarchy.

### ⭐ Record types

| Record | Purpose |
|---|---|
| ⭐ **A** | Name → **IPv4** address |
| ⭐ **AAAA** | Name → **IPv6** address |
| ⭐ **CNAME** | **Alias** to another name |
| ⭐ **MX** | **Mail exchange** server for a domain |
| **NS** | Authoritative name server |
| **PTR** | Reverse lookup (IP → name) |
| **SOA** | Start of authority (zone metadata) |
| **TXT** | Arbitrary text (SPF, DKIM, verification) |

⭐ Uses **UDP port 53** for ordinary queries; falls back to **TCP** for responses larger than 512 bytes and for **zone transfers**. **Caching with TTL** at every level is what makes the system scale.

## 6.3 ⭐⭐ HTTP

📌 **HTTP is STATELESS** — each request is independent; the server remembers nothing between them. Runs over TCP port **80** (443 for HTTPS).

💡 **Why stateless?** Simplicity and scalability — any server in a farm can handle any request. State is layered on top with **cookies**, sessions or tokens.

### ⭐ Methods

| Method | Purpose | Idempotent? | Safe? |
|---|---|---|---|
| ⭐ **GET** | Retrieve; parameters in the **URL** | ✅ | ✅ |
| ⭐ **POST** | Submit data in the **body** | ⭐ **❌ No** | ❌ |
| **PUT** | Create/replace | ✅ Yes | ❌ |
| **DELETE** | Remove | ✅ | ❌ |
| **HEAD** | Headers only, no body | ✅ | ✅ |
| PATCH, OPTIONS, TRACE, CONNECT | | | |

⚠ ⭐ **GET vs POST:** GET puts data in the URL (visible, length-limited, cacheable, bookmarkable); POST puts it in the body (not logged in the URL, no size limit, not cached).

### ⭐⭐ Status code classes

| Class | Meaning | ⭐ Examples |
|---|---|---|
| **1xx** | Informational | 100 Continue |
| **2xx** | ⭐ **Success** | ⭐ **200 OK**, 201 Created, 204 No Content |
| **3xx** | Redirection | 301 Moved Permanently, 302 Found, 304 Not Modified |
| **4xx** | ⭐ **CLIENT error** | 400 Bad Request, 401 Unauthorized, 403 Forbidden, ⭐ **404 Not Found**, 405 Method Not Allowed |
| **5xx** | ⭐ **SERVER error** | ⭐ **500 Internal Server Error**, 502 Bad Gateway, 503 Service Unavailable |

⭐ **Mnemonic: 4 = "your fault" (client), 5 = "my fault" (server).**

### ⭐ Persistent vs non-persistent

| | **Non-persistent (HTTP/1.0)** | ⭐ **Persistent (HTTP/1.1, keep-alive)** |
|---|---|---|
| TCP connections | ⭐ **A new one per object** | ⭐ **One reused for many objects** |
| Cost | 2 RTTs per object (handshake + request) | 1 RTT per object after setup |

🔢 A page with 1 HTML file and 10 images:
- **Non-persistent:** 11 TCP connections → ~22 RTTs
- **Persistent:** 1 connection → ~12 RTTs
⭐ Persistent connections roughly halve the page load time — which is why HTTP/1.1 made them the default.

**HTTP/2** adds multiplexing (many requests on one connection concurrently), header compression and server push. **HTTPS = HTTP over TLS.**

## 6.4 ⭐⭐ Email

| Protocol | ⭐ Role | Port |
|---|---|---|
| ⭐ **SMTP** | ⭐ **PUSH / SENDING** — client→server and server→server | **25** |
| ⭐ **POP3** | ⭐ **PULL / RETRIEVAL** — typically **downloads and DELETES** from the server; single-device | **110** |
| ⭐ **IMAP** | ⭐ **PULL / RETRIEVAL** — ⭐ **keeps mail ON THE SERVER**, supports folders and multi-device sync | **143** |

📌 ⭐⭐ **SMTP SENDS; POP3 and IMAP RETRIEVE.** This is the most-asked email fact.

⚠ ⭐ **POP3 vs IMAP:** POP3 downloads and removes (mail lives on one device); IMAP synchronises (mail lives on the server, so your phone and laptop see the same state). IMAP is why modern webmail works across devices.

⭐ **MIME (Multipurpose Internet Mail Extensions)** exists because SMTP was defined for **7-bit ASCII text only**. MIME encodes attachments, binary data and non-ASCII characters into ASCII so SMTP can carry them.

**Components:** User Agent (UA — your mail client) · Mail Transfer Agent (MTA — the server) · Mail Access Agent (MAA — POP3/IMAP server).

## 6.5 ⭐ FTP

📌 ⭐ **FTP uses TWO separate TCP connections:**
- ⭐ **Control connection on port 21** — persistent for the whole session, carries commands and replies
- ⭐ **Data connection on port 20** — opened and closed **for each file transfer**

💡 **Why separate them?** So you can issue commands (like abort) *while* a transfer is in progress, on a channel that is not clogged with file data.

| Mode | 💡 Who opens the data connection |
|---|---|
| **Active** | The **SERVER** connects back to the client. ⚠ Blocked by most NAT/firewalls |
| ⭐ **Passive** | The **CLIENT** opens both connections. ⭐ **NAT-friendly**, and therefore the default today |

⚠ ⭐ **FTP transmits credentials in PLAINTEXT.** Use **SFTP** (over SSH) or **FTPS** (over TLS) instead.

**Other application protocols:** Telnet (insecure remote login) · SSH (encrypted replacement) · SNMP (network management) · NTP (time sync) · LDAP (directory services).

---

# 7. ⭐ Rapid-fire facts

| Fact | Value |
|---|---|
| OSI layers / TCP-IP layers | **7 / 4** |
| Missing in TCP/IP | ⭐ **Session, presentation** |
| Routing, IP addressing | **Network (3)** |
| Framing, MAC addressing | **Data link (2)** |
| Encryption, compression | **Presentation (6)** |
| Dialog control | Session (5) |
| End-to-end delivery, ports | Transport (4) |
| Units: bit/frame/packet/segment | Physical/data link/network/transport |
| Hub / Switch / Router layer | **1 / 2 / 3** |
| **Separates broadcast domains** | ⭐ **Router only** |
| Separates collision domains | Switch (one per port) |
| **Transmission delay** | **L/B** — depends on packet size |
| **Propagation delay** | **d/v** — independent of packet size |
| Bandwidth–delay product | bandwidth × RTT |
| Shannon capacity | **B log₂(1+S/N)** |
| Nyquist capacity | **2B log₂L** |
| Bit stuffing | Insert 0 after five 1s; flag = 01111110 |
| Strongest error detection | ⭐ **CRC** |
| Simple parity misses | **Even** numbers of errors |
| **Detect d errors** | ⭐ **d_min ≥ d + 1** |
| **Correct d errors** | ⭐ **d_min ≥ 2d + 1** |
| **Hamming parity bits** | ⭐ **2ʳ ≥ m + r + 1** |
| (7,4) Hamming d_min | 3 → corrects 1, detects 2 |
| **GBN max window** | ⭐ **2ᵐ − 1** |
| **SR max window** | ⭐ **2ᵐ⁻¹** |
| GBN receiver window | **1** |
| Efficiency | **W/(1+2a)** |
| Optimum window | 1 + 2a |
| **Pure / slotted ALOHA** | ⭐ **18.4% (1/2e) / 36.8% (1/e)** |
| **Min frame size** | ⭐ **2 × T_prop × Bandwidth** |
| Ethernet min frame / MTU | ⭐ **64 bytes / 1500 bytes** |
| Ethernet frame range | 64–1518 bytes |
| MAC address size | **48 bits** |
| CSMA/CD backoff | Binary exponential, [0, 2ⁿ−1] |
| Wireless uses | **CSMA/CA** (hidden terminal, RTS/CTS) |
| Prevents layer-2 loops | **STP** |
| **IPv4 header** | ⭐ **20–60 bytes** |
| **IPv6 header** | ⭐ **40 bytes FIXED** |
| IPv4 Total Length max | 65,535 |
| **Fragment offset unit** | ⭐ **8 bytes** |
| MF flag | 1 except on the last fragment |
| **Reassembly happens at** | ⭐ **Final destination only** |
| TTL purpose | Prevent infinite loops |
| Protocol numbers TCP/UDP/ICMP | 6 / 17 / 1 |
| No broadcast in | ⭐ **IPv6** (uses multicast/anycast) |
| Loopback | **127.0.0.0/8** |
| Private ranges | 10/8, 172.16/12, 192.168/16 |
| **Usable hosts** | ⭐ **2^(32−prefix) − 2** |
| /26 / /27 / /30 usable | ⭐ **62 / 30 / 2** |
| /20 addresses | **4096** |
| Mask for /26 / /27 | 255.255.255.**192** / **224** |
| Block size | 256 − mask octet |
| **Routing table lookup** | ⭐ **Longest prefix match** |
| **RIP** | Distance vector, hop count, ⭐ **infinity = 16** |
| **OSPF** | ⭐ **Link state, Dijkstra** |
| **BGP** | ⭐ **Path vector, exterior** |
| Count-to-infinity | ⭐ **Distance vector**; fixed by split horizon |
| **ARP maps** | ⭐ **IP → MAC** |
| RARP / DHCP | MAC → IP (obsolete) / full config |
| **DHCP sequence** | ⭐ **DORA** (67/68, UDP) |
| **ping / traceroute use** | ⭐ **ICMP** (Echo / Time Exceeded) |
| ICMP has | **No ports**; reports but does not fix |
| **NAT** | Many private → one public via **ports** |
| **TCP / UDP header** | ⭐ **20–60 / 8 bytes** |
| TCP seq numbers count | ⭐ **Bytes** |
| **TCP handshake / teardown** | ⭐ **3-way / 4-way** |
| TCP flags | URG, ACK, PSH, RST, SYN, FIN |
| Window size field | 16 bits (65,535 max) |
| **Flow control protects** | ⭐ **The receiver** |
| **Congestion control protects** | ⭐ **The network** |
| **Slow start growth** | ⭐ **Exponential** |
| **Congestion avoidance growth** | ⭐ **Linear (AIMD)** |
| **Fast retransmit trigger** | ⭐ **3 duplicate ACKs** |
| On timeout, cwnd | ⭐ **Resets to 1** |
| Effective window | min(rwnd, cwnd) |
| Silly window fixes | Nagle (sender), Clark (receiver) |
| Leaky vs token bucket | Constant rate / **allows bursts** |
| Socket | (IP, port) |
| TCP connection identified by | **4-tuple** |
| **Ports** | FTP 20/21, SSH 22, SMTP 25, DNS 53, HTTP 80, POP3 110, IMAP 143, HTTPS 443 |
| **DNS uses** | ⭐ **UDP 53** |
| DNS records | A, AAAA, CNAME, MX, NS, PTR, SOA |
| Recursive vs iterative DNS | Server does the work / client does |
| HTTP is | **Stateless** |
| 404 / 500 | Client / server error |
| PUT / POST idempotent | ✅ / ⭐ **❌** |
| Persistent connection | Reuses one TCP connection |
| **SMTP vs POP3/IMAP** | ⭐ **Send vs retrieve** |
| POP3 vs IMAP | Downloads & deletes / **keeps on server** |
| MIME exists because | SMTP is 7-bit ASCII only |
| **FTP connections** | ⭐ **Two: 21 control, 20 data** |

---

# 8. ⚠ Common traps

1. ⭐⭐ **Detect d errors needs d_min ≥ d+1; CORRECT d errors needs 2d+1.**
2. ⭐⭐ **GBN's receiver window is 1**; SR's is N.
3. ⭐⭐ **GBN max window = 2ᵐ − 1; SR max window = 2ᵐ⁻¹.**
4. ⭐ **Pure ALOHA 18.4%, slotted 36.8%** — not the reverse.
5. ⭐⭐ **Fragment offset is in 8-BYTE units**, not bytes.
6. ⭐ **Reassembly happens only at the destination**, never at intermediate routers.
7. ⭐⭐ **Usable hosts = 2^h − 2** — always subtract network and broadcast.
8. ⭐⭐ **Switches do NOT separate broadcast domains; routers do.**
9. ⭐ **DNS uses UDP** (port 53), not TCP, for ordinary queries.
10. ⭐ **SMTP is for sending only** — POP3/IMAP retrieve.
11. ⭐ **FTP uses two connections** (21 control, 20 data).
12. ⭐⭐ **Flow control ≠ congestion control** (receiver vs network).
13. ⭐ **TCP establishment is 3-way; termination is 4-way.**
14. ⭐ **Transmission delay depends on packet size; propagation delay does not.**
15. ⭐ **ICMP reports errors but does not fix them, and has no port numbers.**
16. ⭐ **On a timeout cwnd resets to 1; on 3 duplicate ACKs it only halves.**
17. **The session and presentation layers are the ones missing from TCP/IP.**
18. **IPv6 has no broadcast address.**
19. **ARP is local only** — it never crosses a router.
20. **Slow start is exponential** despite the name.

---

# 9. Practice

- GATE: [`Paper2_S11_Computer_Networks/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S11_Computer_Networks/) — **226 questions**
- State-PSC level: [`Paper2_S11_Computer_Networks/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S11_Computer_Networks/) — **537 questions** (the largest single subject folder in the corpus)
- Test: [`Week_08_Test.md`](../04_Mock_Tests/Week_08_Test.md)

**Priority order if short on time:** ⭐⭐ **subnetting/CIDR — drill until reflexive** → the port-number table → the OSI layer↔protocol↔device tables → TCP vs UDP and the congestion-control phases → sliding-window formulas and max window sizes → ALOHA/CSMA-CD efficiency and minimum frame size → fragmentation → the routing-protocol comparison → DNS/HTTP/SMTP/FTP specifics.
