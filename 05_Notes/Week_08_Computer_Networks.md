# Week 8 — Computer Networks

**Syllabus §11:** Concept of layering: OSI and TCP/IP protocol stacks. Basics of packet, circuit and virtual circuit switching. Data link layer: framing, error detection, medium access control, Ethernet bridging. Routing protocols: shortest path, flooding, distance vector and link state routing. Fragmentation and IP addressing, IPv4, CIDR notation. Basics of IP support protocols (ARP, DHCP, ICMP), Network Address Translation (NAT). Transport layer: flow control and congestion control, UDP, TCP, sockets. Application layer protocols: DNS, SMTP, HTTP, FTP, Email.
**Estimated marks: ~11**

---

## 1. ⭐⭐ Layering

### 1.1 OSI reference model (7 layers)

| # | Layer | Function | Unit | Devices | Protocols |
|---|---|---|---|---|---|
| 7 | **Application** | User services | Data | — | HTTP, FTP, SMTP, DNS, DHCP, SNMP, Telnet |
| 6 | **Presentation** | Translation, **encryption**, **compression** | Data | — | SSL/TLS, JPEG, MPEG, ASCII |
| 5 | **Session** | Session establishment, **dialog control**, synchronisation, checkpointing | Data | — | RPC, NetBIOS, PPTP |
| 4 | ⭐ **Transport** | **End-to-end** delivery, **segmentation**, flow & error control, **port addressing** | **Segment** | Gateway | ⭐ **TCP, UDP**, SCTP |
| 3 | ⭐ **Network** | ⭐ **Routing**, **logical (IP) addressing**, **fragmentation** | **Packet / Datagram** | ⭐ **Router**, layer-3 switch | ⭐ **IP, ICMP, IGMP, ARP\*, RIP, OSPF, BGP** |
| 2 | ⭐ **Data link** | ⭐ **Framing**, **physical (MAC) addressing**, error detection, **flow control**, MAC | **Frame** | ⭐ **Switch, bridge**, NIC | Ethernet, PPP, HDLC, ARP\*, Token Ring |
| 1 | **Physical** | Bits over the medium; encoding, signalling, topology | **Bit** | ⭐ **Hub, repeater**, cable, modem | RS-232, DSL, 10BASE-T |

\* ⚠ **ARP's layer is genuinely disputed** — it is most often placed at layer 2 (data link) because it deals in MAC addresses, but many textbooks list it at layer 3 as an "IP support protocol" (as the TPSC syllabus itself does). If asked, prefer **data link (layer 2)** unless the option set suggests network layer.

⭐ **Mnemonic (layer 7 → 1):** **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
⭐ **(layer 1 → 7):** **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way

### 1.2 ⭐ TCP/IP model (4 layers)

| TCP/IP layer | Maps to OSI |
|---|---|
| **Application** | Application + Presentation + Session |
| **Transport** | Transport |
| **Internet** | Network |
| **Network Access / Link** | Data link + Physical |

⭐ **The session and presentation layers have no separate counterpart in TCP/IP** — their functions are absorbed into the application layer.
⚠ Some textbooks present a **5-layer hybrid** (splitting network access into data link and physical). Read the question.

| | **OSI** | **TCP/IP** |
|---|---|---|
| Layers | 7 | 4 |
| Origin | Theoretical reference model | Implemented protocols first |
| Service/interface separation | Clearly defined | Blurred |
| Transport reliability | Connection-oriented only | Both (TCP and UDP) |
| Usage | Teaching/reference | ⭐ **The actual Internet** |

### 1.3 ⭐ Switching

| | **Circuit switching** | **Datagram (packet) switching** | **Virtual circuit switching** |
|---|---|---|---|
| Path setup | ⭐ **Dedicated, before transfer** | None | Logical circuit set up first |
| Resource reservation | ✅ Yes | ❌ No | Partial |
| Packets follow | Same path | ⭐ **Possibly different paths** | Same path |
| Ordering | Guaranteed | ⭐ **Not guaranteed** | Guaranteed |
| Addressing | Path set up once | Full address in **every** packet | Short VC identifier |
| Bandwidth use | Inefficient if idle | ⭐ **Efficient (statistical multiplexing)** | Efficient |
| Example | Traditional telephony | ⭐ **The Internet (IP)** | ATM, Frame Relay, MPLS |

### 1.4 ⭐ Delays and performance

📌 **Transmission delay = packet size / bandwidth** (L/B)
📌 **Propagation delay = distance / propagation speed** (d/v)
📌 **Total one-way delay = transmission + propagation + queuing + processing**
📌 ⭐ **RTT (round-trip time) ≈ 2 × propagation delay** (plus transmission and processing)
📌 **Bandwidth–delay product = bandwidth × RTT** — the "capacity of the pipe", i.e. bits in flight

🔢 1500-byte packet on a 10 Mbps link: transmission delay = 12,000 bits / 10⁷ bps = **1.2 ms**.
🔢 2000 km link at 2×10⁸ m/s: propagation delay = 2×10⁶ / 2×10⁸ = **10 ms**.

⚠ **Transmission delay depends on packet size and bandwidth; propagation delay depends on distance and medium** — never on packet size.

---

## 2. ⭐ Physical layer basics

📌 ⭐ **Nyquist (noiseless channel): C = 2B log₂L** bps, where L = number of signal levels
📌 ⭐ **Shannon (noisy channel): C = B log₂(1 + S/N)** bps
📌 **SNR in dB = 10 log₁₀(S/N)**

🔢 B = 3000 Hz, S/N = 3 → C = 3000 × log₂4 = **6000 bps**.
🔢 B = 3000 Hz, SNR = 30 dB → S/N = 1000 → C ≈ 3000 × 9.97 ≈ **29,900 bps**.

**Transmission modes:** simplex · half-duplex · full-duplex.
**Multiplexing:** FDM · TDM (synchronous/statistical) · WDM · CDM.
**Media:** twisted pair (UTP/STP) · coaxial · **optical fibre** (highest bandwidth, immune to EMI, no crosstalk) · wireless.
**Topologies:** bus · star · ring · mesh (📌 a full mesh of n nodes needs **n(n−1)/2** links) · tree · hybrid.

---

## 3. ⭐⭐ Data link layer

### 3.1 Framing
- **Character/byte count** — fragile if the count is corrupted.
- **Character stuffing (byte stuffing)** — escape (DLE) before accidental flags.
- ⭐ **Bit stuffing** — after five consecutive 1s, insert a 0. The flag is `01111110`.
- Physical layer coding violations.

🔢 Data `011111111111011111110` → bit-stuffed: insert a 0 after each run of five 1s.

### 3.2 ⭐ Error detection

| Method | Detects |
|---|---|
| **Simple parity** | All **odd** numbers of bit errors; misses even-numbered errors |
| **2-D parity** | All 1-, 2- and 3-bit errors; can correct single-bit errors |
| **Checksum** (1's complement) | Used by IP, TCP, UDP; weaker than CRC |
| ⭐ **CRC (Cyclic Redundancy Check)** | ⭐ **Strongest** — all burst errors shorter than the generator polynomial's degree |

⭐ **CRC procedure:** append r zeros to the data (r = degree of generator G), divide by G using **modulo-2 (XOR) division**, and the r-bit remainder becomes the CRC. The receiver divides the whole received frame by G — **remainder 0 ⇒ no error detected**.

🔢 Data `1010`, G = `1011` (degree 3 ⇒ append 3 zeros → `1010000`). Modulo-2 divide by 1011 → remainder `011`. Transmitted frame = **`1010011`**.

### 3.3 ⭐ Hamming distance & error correction

📌 **Hamming distance** between two codewords = number of differing bit positions.
📌 ⭐ **To DETECT up to d errors: d_min ≥ d + 1**
📌 ⭐ **To CORRECT up to d errors: d_min ≥ 2d + 1**

⚠ These two are constantly swapped. Detection needs d+1; correction needs 2d+1.

📌 ⭐ **Hamming code parity bits:** for m data bits, r parity bits must satisfy **2ʳ ≥ m + r + 1**
🔢 m = 4 → r = 3 (2³ = 8 ≥ 4+3+1 = 8) ✅ → the (7,4) Hamming code.
🔢 m = 8 → r = 4 (2⁴ = 16 ≥ 8+4+1 = 13) ✅

Parity bits sit at positions 1, 2, 4, 8, … (powers of 2). Parity bit at position 2ⁱ checks all positions whose binary representation has bit i set. The **syndrome** (the binary number formed by the failed parity checks) gives the position of the erroneous bit directly.

### 3.4 ⭐⭐ Flow control protocols

📌 ⭐ **Efficiency (utilisation) η = W / (1 + 2a)** where **a = T_prop / T_trans** and W = window size

| Protocol | Sender window | Receiver window | ⭐ Max window with m-bit seq. no. | Efficiency |
|---|---|---|---|---|
| ⭐ **Stop-and-Wait** | 1 | 1 | 1 (needs 1 bit) | 1/(1+2a) |
| ⭐ **Go-Back-N (GBN)** | N | ⭐ **1** | ⭐ **2ᵐ − 1** | N/(1+2a) |
| ⭐ **Selective Repeat (SR)** | N | ⭐ **N** | ⭐ **2ᵐ⁻¹** | N/(1+2a) |

⭐ **Why the window limits differ:**
- GBN needs **one spare** sequence number so a retransmission is distinguishable from new data → 2ᵐ − 1.
- SR has a receiver window too, and sender + receiver windows must not overlap ambiguously → at most **half** the sequence space, 2ᵐ⁻¹.

| | **Go-Back-N** | **Selective Repeat** |
|---|---|---|
| On error | ⭐ Retransmits the frame **and all following** | ⭐ Retransmits **only the lost frame** |
| Receiver buffering | Not needed | Needed |
| ACKs | Cumulative | Individual |
| NAK support | — | Yes |
| Complexity | Simpler | More complex |
| Bandwidth on errors | Wasteful | Efficient |

🔢 T_trans = 1 ms, T_prop = 4 ms ⇒ a = 4. Stop-and-Wait efficiency = 1/(1+8) = **11.1%**. With GBN, W = 7 → 7/9 = **77.8%**.
📌 **Optimum window size for 100% utilisation = 1 + 2a.**

### 3.5 ⭐⭐ Medium Access Control (MAC)

**(a) Random access**

| Protocol | ⭐ Max efficiency |
|---|---|
| ⭐ **Pure ALOHA** | ⭐ **1/(2e) ≈ 18.4%** (at G = 0.5) |
| ⭐ **Slotted ALOHA** | ⭐ **1/e ≈ 36.8%** (at G = 1) |
| CSMA | Better than ALOHA |
| **CSMA/CD** | High on wired LANs |
| **CSMA/CA** | Used in 802.11 wireless |

📌 Pure ALOHA throughput S = G·e^(−2G); slotted ALOHA S = G·e^(−G).

⭐ **CSMA/CD (Ethernet):** listen before transmit; if a collision is detected, abort, send a jam signal, and back off using **binary exponential backoff** (after the n-th collision, wait a random multiple of the slot time in [0, 2ⁿ − 1], capped at n = 10, giving up after 16 attempts).

⭐ **Minimum frame size** exists so a sender is still transmitting when the earliest possible collision signal returns:
📌 **T_trans ≥ 2 × T_prop**, i.e. **minimum frame size = 2 × T_prop × Bandwidth**

🔢 10 Mbps Ethernet, max round-trip propagation 51.2 μs → min frame = 10⁷ × 51.2×10⁻⁶ = 512 bits = ⭐ **64 bytes**.

⭐ **CSMA/CA** (wireless) uses **collision avoidance** because collision *detection* is impractical on radio (hidden-terminal problem): RTS/CTS handshake, interframe spacing, and ACKs.

**(b) Controlled access:** reservation · polling · token passing.
**(c) Channelization:** FDMA · TDMA · CDMA.

### 3.6 ⭐ Ethernet and bridging

**Ethernet (IEEE 802.3) frame:** Preamble (7 B) | SFD (1 B) | **Destination MAC (6 B)** | **Source MAC (6 B)** | Length/Type (2 B) | **Data (46–1500 B)** | CRC/FCS (4 B)
📌 Frame size range **64 to 1518 bytes** (excluding preamble); ⭐ **MTU = 1500 bytes**.

**MAC address:** 48 bits (6 bytes), written as 12 hex digits; first 24 bits are the OUI (manufacturer). Broadcast = `FF:FF:FF:FF:FF:FF`.

⭐ **Devices and domains:**

| Device | Layer | Collision domains | Broadcast domains |
|---|---|---|---|
| **Hub / Repeater** | 1 | ⭐ **1 (shared)** | 1 |
| **Bridge / Switch** | 2 | ⭐ **One per port** | 1 (unless VLANs) |
| ⭐ **Router** | 3 | Per port | ⭐ **One per port — separates broadcast domains** |

⭐ **Only a router (or a VLAN) separates broadcast domains.** A switch separates collision domains but forwards broadcasts.

**Switch operation:** learns source MACs into a **MAC address table**; forwards known unicast to one port; **floods** unknown unicast, broadcast and multicast. **Spanning Tree Protocol (STP, 802.1D)** prevents loops.
**Switching methods:** store-and-forward · cut-through · fragment-free.

---

## 4. ⭐⭐ Network layer

### 4.1 ⭐ IPv4 header (20–60 bytes)

| Field | Size | Note |
|---|---|---|
| Version | 4 bits | 4 |
| **IHL** | 4 bits | Header length in 4-byte words; ⭐ min 5 (20 B), max 15 (60 B) |
| Type of Service / DSCP | 8 bits | QoS |
| **Total Length** | 16 bits | ⭐ Header + data; max **65,535** bytes |
| ⭐ **Identification** | 16 bits | Same for all fragments of a datagram |
| ⭐ **Flags** | 3 bits | Reserved, **DF** (Don't Fragment), ⭐ **MF** (More Fragments) |
| ⭐ **Fragment Offset** | 13 bits | ⭐ In units of **8 bytes** |
| ⭐ **TTL** | 8 bits | Decremented by each router; 0 ⇒ discard + ICMP Time Exceeded |
| **Protocol** | 8 bits | ⭐ TCP = 6, UDP = 17, ICMP = 1 |
| **Header Checksum** | 16 bits | Header only; recomputed at each hop |
| Source / Destination IP | 32 bits each | |
| Options + Padding | 0–40 bytes | |

### 4.2 ⭐ Fragmentation

📌 **Fragment offset is measured in 8-byte units**, so every fragment except the last must carry a multiple of 8 bytes of data.
📌 **MF = 1** for all fragments except the last; **MF = 0** on the last.
📌 All fragments of one datagram share the same **Identification**.
⭐ **Reassembly happens only at the final destination**, never at intermediate routers.

🔢 A 4000-byte datagram (20 B header + 3980 B data) crossing a link with **MTU 1500**:
Each fragment carries at most 1500 − 20 = 1480 bytes of data; 1480 is a multiple of 8 ✅

| Fragment | Data bytes | Offset (bytes) | Offset field (÷8) | MF |
|---|---|---|---|---|
| 1 | 1480 | 0 | 0 | 1 |
| 2 | 1480 | 1480 | 185 | 1 |
| 3 | 1020 | 2960 | 370 | 0 |

### 4.3 ⭐⭐ IPv4 addressing

**32 bits**, written as four dotted decimal octets.

⭐ **Classful addressing:**

| Class | Leading bits | First octet range | Default mask | Network / Host bits |
|---|---|---|---|---|
| **A** | 0 | 1–126 | 255.0.0.0 (/8) | 8 / 24 |
| **B** | 10 | 128–191 | 255.255.0.0 (/16) | 16 / 16 |
| **C** | 110 | 192–223 | 255.255.255.0 (/24) | 24 / 8 |
| **D** | 1110 | 224–239 | — | **Multicast** |
| **E** | 1111 | 240–255 | — | Reserved/experimental |

⭐ **Reserved / special addresses:**

| Range | Purpose |
|---|---|
| **127.0.0.0/8** | ⭐ **Loopback** (127.0.0.1) |
| **10.0.0.0/8** | ⭐ Private (Class A) |
| **172.16.0.0/12** | ⭐ Private (Class B) |
| **192.168.0.0/16** | ⭐ Private (Class C) |
| **169.254.0.0/16** | Link-local (APIPA) |
| **0.0.0.0** | This host / default route |
| **255.255.255.255** | Limited broadcast |

### 4.4 ⭐⭐⭐ Subnetting and CIDR

**This is the single most reliably asked topic in the networks section. Make it a 30-second reflex.**

📌 **Host bits = 32 − prefix**
📌 ⭐ **Total addresses in a block = 2^(32 − prefix)**
📌 ⭐ **Usable hosts = 2^(32 − prefix) − 2** (subtract the network and broadcast addresses)
📌 **Number of subnets when borrowing k bits = 2ᵏ**
📌 **Block size (increment) in the last varying octet = 256 − (mask octet value)**

⭐ **Prefix → mask table (memorise):**

| Prefix | Mask (last octet) | Addresses | Usable hosts |
|---|---|---|---|
| /24 | 0 | 256 | 254 |
| /25 | **128** | 128 | 126 |
| /26 | **192** | 64 | ⭐ **62** |
| /27 | **224** | 32 | ⭐ **30** |
| /28 | **240** | 16 | 14 |
| /29 | **248** | 8 | 6 |
| /30 | **252** | 4 | ⭐ **2** (point-to-point links) |
| /31 | 254 | 2 | 0 (special RFC 3021 use) |
| /32 | 255 | 1 | host route |

| Prefix | Mask | Addresses |
|---|---|---|
| /20 | 255.255.240.0 | 4096 |
| /21 | 255.255.248.0 | 2048 |
| /22 | 255.255.252.0 | 1024 |
| /23 | 255.255.254.0 | 512 |
| /16 | 255.255.0.0 | 65,536 |

🔢 **`192.168.10.0/26`** → host bits 6 → 64 addresses, ⭐ **62 usable**; 4 subnets from the /24.
Subnets: `.0–.63`, `.64–.127`, `.128–.191`, `.192–.255`. For the second: network `.64`, broadcast `.127`, usable `.65–.126`.

🔢 **`172.16.0.0/20`** → host bits 12 → 2¹² = ⭐ **4096 addresses**, 4094 usable.

🔢 **Which subnet does 200.10.5.100/27 belong to?**
Block size = 256 − 224 = 32 → boundaries at .0, .32, .64, .96, .128…
100 falls in **.96–.127** → network **200.10.5.96**, broadcast **200.10.5.127**, usable .97–.126.

⭐ **Supernetting / route aggregation:** combine contiguous blocks into a shorter prefix. To aggregate, the blocks must be contiguous and the count a power of 2, aligned on a boundary.
🔢 `192.168.0.0/24` … `192.168.3.0/24` (4 blocks) aggregate to **`192.168.0.0/22`**.

**VLSM (Variable Length Subnet Masking):** different subnet sizes within one network — allocate largest requirements first.

### 4.5 IPv6
**128 bits**, eight groups of four hex digits; `::` compresses one run of zero groups.
⭐ **Fixed 40-byte header**, no checksum, **no fragmentation by routers** (the source does path MTU discovery), extension headers for options. Address types: unicast, multicast, **anycast** (⚠ **no broadcast** in IPv6). Autoconfiguration (SLAAC). Transition: dual stack, tunnelling, translation.

### 4.6 ⭐⭐ Routing

| Approach | Mechanism | Convergence | Knowledge |
|---|---|---|---|
| **Flooding** | Send on every link except the incoming one | — | None; wasteful but robust |
| ⭐ **Distance vector** | Exchange **distance vectors** with **neighbours only** | ⭐ **Slow** | Knows only distances |
| ⭐ **Link state** | **Flood** link-state info to **all** routers; each builds the full map and runs Dijkstra | ⭐ **Fast** | ⭐ **Full topology** |
| **Path vector** | Advertises full AS paths | — | Used by BGP |

⭐ **Distance vector (Bellman–Ford based, e.g. RIP):**
- Updates periodically (RIP: every 30 s) to neighbours only.
- ⭐ **Count-to-infinity problem:** bad news propagates slowly, with routers incrementing each other's costs indefinitely.
- **Mitigations:** ⭐ **split horizon** (don't advertise a route back on the interface it was learned from) · **poison reverse** · **hold-down timers** · defining a small "infinity" (⭐ **RIP's infinity is 16**, so max hop count is 15).

⭐ **Link state (e.g. OSPF):** floods LSAs, each router builds an identical topology database and runs **Dijkstra** locally. Faster convergence, no count-to-infinity, but more memory/CPU and more complex.

| Protocol | Type | Metric | Scope |
|---|---|---|---|
| ⭐ **RIP** | Distance vector | Hop count (max 15) | Interior (IGP) |
| ⭐ **OSPF** | ⭐ **Link state** | Cost (bandwidth-based) | Interior (IGP) |
| **IGRP/EIGRP** | Hybrid/advanced DV | Composite | Interior (Cisco) |
| ⭐ **BGP** | ⭐ **Path vector** | Policy-based | ⭐ **Exterior (EGP)** — between autonomous systems |

**Routing table lookup:** ⭐ **longest prefix match** wins.
**Static vs dynamic routing** · unicast vs multicast (IGMP, PIM, DVMRP) vs broadcast.

### 4.7 ⭐ IP support protocols

| Protocol | Purpose |
|---|---|
| ⭐ **ARP** | ⭐ **IP → MAC**. Broadcast request, unicast reply; results cached in the ARP table |
| **RARP** | MAC → IP (obsolete; replaced by DHCP) |
| ⭐ **DHCP** | Dynamically assigns IP, mask, gateway, DNS. ⭐ **DORA: Discover → Offer → Request → Acknowledge**. Ports **67 (server) / 68 (client)**, over UDP |
| ⭐ **ICMP** | Error reporting and diagnostics: Echo Request/Reply (⭐ **`ping`**), Destination Unreachable, **Time Exceeded** (⭐ `traceroute`), Redirect, Source Quench. ⚠ ICMP reports errors but does **not correct** them |
| **IGMP** | Multicast group management |

⭐ **NAT (Network Address Translation):** rewrites private source addresses (and ports, in **NAPT/PAT**) to a public address, letting many hosts share few public IPs. It was the main mitigation for IPv4 exhaustion.
- **Types:** static NAT (1:1) · dynamic NAT (pool) · ⭐ **PAT/NAT overload** (many:1 using port numbers).
- ⚠ **Drawbacks:** breaks end-to-end connectivity, complicates peer-to-peer and inbound connections, and violates the layering principle (a layer-3 device inspecting layer-4 ports).

---

## 5. ⭐⭐ Transport layer

### 5.1 ⭐ TCP vs UDP

| | ⭐ **TCP** | ⭐ **UDP** |
|---|---|---|
| Connection | ⭐ **Connection-oriented** | ⭐ **Connectionless** |
| Reliability | ⭐ **Reliable** (ACKs, retransmission) | ⭐ **Unreliable, best-effort** |
| Ordering | Guaranteed | Not guaranteed |
| ⭐ **Header size** | ⭐ **20–60 bytes** | ⭐ **8 bytes** |
| Flow control | ✅ Sliding window | ❌ |
| Congestion control | ✅ | ❌ |
| Speed / overhead | Slower, higher | ⭐ **Faster, minimal** |
| Data unit | Segment (byte stream) | Datagram (message) |
| Duplicate detection | ✅ | ❌ |
| Uses | HTTP, FTP, SMTP, SSH, Telnet | ⭐ **DNS, DHCP, TFTP, SNMP, RIP**, VoIP, streaming, games |

### 5.2 ⭐ TCP header (20–60 bytes)

Source Port (16) | Destination Port (16) | ⭐ **Sequence Number (32)** | ⭐ **Acknowledgement Number (32)** | HLEN (4) | Reserved (6) | ⭐ **Flags (6: URG, ACK, PSH, RST, SYN, FIN)** | ⭐ **Window Size (16)** | Checksum (16) | Urgent Pointer (16) | Options

📌 The **window size field is 16 bits**, capping the window at 65,535 bytes — the **window scaling** option extends this.
📌 Sequence numbers count **bytes**, not segments.

### 5.3 ⭐ Connection management

⭐ **Three-way handshake (establishment):**
1. Client → Server: **SYN** (seq = x)
2. Server → Client: **SYN + ACK** (seq = y, ack = x+1)
3. Client → Server: **ACK** (ack = y+1)

⭐ **Four-way handshake (termination):** FIN → ACK → FIN → ACK. The initiator then waits in **TIME_WAIT** (2×MSL) to absorb delayed duplicates.

⚠ **Establishment is 3 segments; termination is 4.** Also note the **half-open** state during termination.
**States:** CLOSED, LISTEN, SYN_SENT, SYN_RECEIVED, ESTABLISHED, FIN_WAIT_1/2, CLOSE_WAIT, LAST_ACK, TIME_WAIT.

### 5.4 ⭐ Flow control
**Sliding window**, advertised by the receiver's window field. **Zero-window** stops the sender until a window update arrives.
- ⭐ **Silly Window Syndrome:** tiny segments waste bandwidth. Fixes: **Nagle's algorithm** (sender side — buffer small writes until an ACK arrives) and **Clark's solution / delayed ACK** (receiver side).

📌 **Effective window = min(receiver window, congestion window)**

### 5.5 ⭐⭐ Congestion control

⭐ **Four phases:**

| Phase | Behaviour |
|---|---|
| ⭐ **Slow start** | cwnd starts at 1 MSS and ⭐ **doubles every RTT (exponential)** until it reaches `ssthresh` |
| ⭐ **Congestion avoidance** | cwnd increases by ⭐ **1 MSS per RTT (linear / additive increase)** |
| ⭐ **Fast retransmit** | On ⭐ **3 duplicate ACKs**, retransmit immediately without waiting for a timeout |
| ⭐ **Fast recovery** | ssthresh = cwnd/2; cwnd = ssthresh; resume congestion avoidance (TCP Reno) |

**On timeout (severe congestion):** ssthresh = cwnd/2, **cwnd resets to 1**, restart slow start.
⭐ The overall behaviour is **AIMD — Additive Increase, Multiplicative Decrease.**

🔢 cwnd = 1, ssthresh = 8, MSS-sized units:
RTT 1: 1 → RTT 2: 2 → RTT 3: 4 → RTT 4: 8 (ssthresh reached, switch to linear) → RTT 5: 9 → RTT 6: 10 …
If a timeout occurs at cwnd = 10: ssthresh = 5, cwnd = 1, slow start again.

⚠ **Flow control protects the receiver; congestion control protects the network.** They are different mechanisms with different feedback.

**Congestion approaches:** open loop (prevention) vs closed loop (detect & react). Techniques: leaky bucket (constant output rate) vs **token bucket** (allows bursts), ECN, RED.

**TCP variants:** Tahoe (no fast recovery) · **Reno** (adds fast recovery) · New Reno · CUBIC (Linux default) · BBR.

### 5.6 Sockets & ports
📌 A **socket** = (IP address, port number). A TCP connection is identified by the **4-tuple** (source IP, source port, destination IP, destination port).
📌 **Port ranges:** well-known **0–1023** · registered **1024–49151** · dynamic/ephemeral **49152–65535**.
**Socket API:** `socket()` → `bind()` → `listen()` → `accept()` (server); `socket()` → `connect()` (client); then `send()`/`recv()` → `close()`.

---

## 6. ⭐⭐ Application layer

### 6.1 ⭐ Well-known port numbers (memorise)

| Port | Protocol | Transport |
|---|---|---|
| **20 / 21** | ⭐ **FTP** (data / control) | TCP |
| **22** | SSH | TCP |
| **23** | Telnet | TCP |
| **25** | ⭐ **SMTP** | TCP |
| **53** | ⭐ **DNS** | ⭐ **UDP** (TCP for zone transfers & large responses) |
| **67 / 68** | ⭐ **DHCP** (server / client) | UDP |
| **69** | TFTP | UDP |
| **80** | ⭐ **HTTP** | TCP |
| **110** | POP3 | TCP |
| **143** | IMAP | TCP |
| **161 / 162** | SNMP | UDP |
| **443** | ⭐ **HTTPS** | TCP |
| **3306** | MySQL | TCP |

### 6.2 ⭐ DNS
Hierarchical, distributed name→IP database. Hierarchy: **root → TLD (.com, .in) → authoritative** servers.

| Resolution | Behaviour |
|---|---|
| ⭐ **Recursive** | The client asks one server, which does all the work and returns the final answer |
| ⭐ **Iterative** | Each server returns a **referral** to the next server; the client chases the chain |

⭐ **Record types:** **A** (IPv4) · **AAAA** (IPv6) · **CNAME** (alias) · **MX** (mail exchange) · **NS** (name server) · **PTR** (reverse lookup) · **SOA** (start of authority) · **TXT**.
Uses **UDP port 53** (fast, small messages); falls back to TCP for responses > 512 bytes and for zone transfers. Caching with TTL reduces load.

### 6.3 ⭐ HTTP
**Stateless**, request–response, over TCP port 80 (443 for HTTPS).

| Method | Purpose |
|---|---|
| **GET** | Retrieve (idempotent, safe; parameters in URL) |
| **POST** | Submit data (not idempotent; data in body) |
| **PUT** | Create/replace (idempotent) |
| **DELETE** | Remove |
| **HEAD** | Headers only |
| PATCH, OPTIONS, TRACE, CONNECT | |

⭐ **Status code classes:**

| Class | Meaning | Examples |
|---|---|---|
| **1xx** | Informational | 100 Continue |
| **2xx** | Success | ⭐ **200 OK**, 201 Created, 204 No Content |
| **3xx** | Redirection | 301 Moved Permanently, 302 Found, 304 Not Modified |
| **4xx** | ⭐ **Client error** | 400 Bad Request, 401 Unauthorized, 403 Forbidden, ⭐ **404 Not Found**, 405 Method Not Allowed |
| **5xx** | ⭐ **Server error** | ⭐ **500 Internal Server Error**, 502 Bad Gateway, 503 Service Unavailable |

⭐ **Non-persistent (HTTP/1.0)** — a new TCP connection per object; ⭐ **persistent (HTTP/1.1, keep-alive)** — reuses one connection, avoiding repeated handshakes.
**Cookies** provide state over a stateless protocol. **HTTP/2** adds multiplexing, header compression and server push.

### 6.4 ⭐ Email

| Protocol | Role | Port |
|---|---|---|
| ⭐ **SMTP** | ⭐ **Push / sending** (client→server, server→server) | 25 |
| ⭐ **POP3** | ⭐ **Pull / retrieval** — typically **downloads and deletes**; single-device | 110 |
| ⭐ **IMAP** | ⭐ **Pull / retrieval** — keeps mail **on the server**, supports folders and multi-device sync | 143 |

⭐ **SMTP sends; POP3/IMAP retrieve.** SMTP is 7-bit ASCII only, so **MIME** encodes attachments and non-ASCII content.
Components: User Agent (UA), Mail Transfer Agent (MTA), Mail Access Agent (MAA).

### 6.5 ⭐ FTP
⭐ Uses **two TCP connections**: **control on port 21** (persistent, commands) and **data on port 20** (opened per transfer).
- **Active mode:** the server initiates the data connection back to the client (problematic with NAT/firewalls).
- **Passive mode:** the client initiates both connections (NAT-friendly).
⚠ FTP transmits credentials in **plaintext** — use SFTP (over SSH) or FTPS (over TLS).

**Other application protocols:** Telnet (insecure remote login) · SSH (encrypted) · SNMP (network management) · NTP (time) · LDAP (directory).

---

## 7. Rapid-fire facts ⭐

| Fact | Value |
|---|---|
| OSI layers | 7 |
| TCP/IP layers | 4 |
| Missing in TCP/IP | Session, presentation |
| Routing layer | Network (3) |
| Framing layer | Data link (2) |
| Encryption/compression layer | Presentation (6) |
| Router separates | Broadcast domains |
| Switch separates | Collision domains |
| Hub layer | Physical (1) |
| Shannon capacity | B log₂(1+S/N) |
| Nyquist | 2B log₂L |
| Strongest error detection | CRC |
| Detect d errors | d_min ≥ d+1 |
| Correct d errors | d_min ≥ 2d+1 |
| Hamming parity bits | 2ʳ ≥ m+r+1 |
| GBN max window | 2ᵐ − 1 |
| SR max window | 2ᵐ⁻¹ |
| Efficiency | W/(1+2a) |
| Pure / slotted ALOHA | 18.4% / 36.8% |
| Ethernet min frame | 64 bytes |
| Ethernet MTU | 1500 bytes |
| MAC address size | 48 bits |
| IPv4 header | 20–60 bytes |
| IPv6 header | 40 bytes fixed |
| Fragment offset unit | 8 bytes |
| Reassembly happens at | Final destination only |
| Loopback | 127.0.0.0/8 |
| /26 usable hosts | 62 |
| /27 usable hosts | 30 |
| /30 usable hosts | 2 |
| /20 addresses | 4096 |
| Routing table lookup | Longest prefix match |
| RIP infinity | 16 (max 15 hops) |
| OSPF type | Link state (Dijkstra) |
| BGP type | Path vector, exterior |
| Count-to-infinity | Distance vector |
| ARP maps | IP → MAC |
| DHCP sequence | DORA |
| ping uses | ICMP |
| TCP / UDP header | 20–60 / 8 bytes |
| TCP handshake | 3-way (4-way teardown) |
| Slow start growth | Exponential |
| Congestion avoidance growth | Linear (AIMD) |
| Fast retransmit trigger | 3 duplicate ACKs |
| HTTP / HTTPS port | 80 / 443 |
| DNS port | 53 (UDP) |
| SMTP port | 25 |
| FTP ports | 21 control, 20 data |
| 404 | Not Found (client error) |
| SMTP vs POP3/IMAP | Send vs retrieve |

---

## 8. Common traps ⚠

1. **Detect d errors needs d+1; correct d errors needs 2d+1.**
2. **GBN receiver window is 1**; SR's is N.
3. **GBN max window 2ᵐ−1, SR max window 2ᵐ⁻¹.**
4. **Pure ALOHA 18.4%, slotted 36.8%** — not the reverse.
5. **Fragment offset is in 8-byte units**, not bytes.
6. **Reassembly only at the destination** — never at intermediate routers.
7. **Usable hosts = 2^h − 2** — do not forget to subtract network and broadcast.
8. **Switches do not separate broadcast domains; routers do.**
9. **DNS uses UDP** (port 53), not TCP, for ordinary queries.
10. **SMTP is for sending only** — POP3/IMAP retrieve.
11. **FTP uses two connections** (21 control, 20 data).
12. **Flow control ≠ congestion control.**
13. **TCP establishment is 3-way, termination is 4-way.**
14. **Transmission delay depends on packet size; propagation delay does not.**
15. **ICMP reports errors but does not fix them**, and has no ports.

---

## 9. Practice

- GATE: [`Paper2_S11_Computer_Networks/`](../03_GATE_CSE_PYQs/Subject_wise/Paper2_S11_Computer_Networks/) — **226 questions**
- State-PSC level: [`Paper2_S11_Computer_Networks/`](../02_State_PSC_PYQs/Subject_wise/Paper2_S11_Computer_Networks/) — **537 questions** (the largest single subject folder)
- Test: [`Week_08_Test.md`](../04_Mock_Tests/Week_08_Test.md)

**Priority order if short on time:** ⭐ **subnetting/CIDR** (drill until reflexive) → the port-number table → OSI layer↔protocol↔device tables → TCP vs UDP and congestion control phases → sliding window formulas → ALOHA/CSMA-CD efficiency and minimum frame size → fragmentation → routing protocol comparison → DNS/HTTP/SMTP/FTP specifics.
