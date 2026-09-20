# Week 8 Question Bank — Computer Networks

**Syllabus §11** · 216 questions · Practice set · +1 / −0.33 marking

> Ground every answer in `05_Notes/Week_08_Computer_Networks.md`. Cover the answer key; attempt all, then self-check the numericals.

---

## Part A — OSI & TCP/IP layering

**Q1.** Routing and logical (IP) addressing are the responsibility of which OSI layer?
(A) Data link  (B) Network  (C) Transport  (D) Session

**Q2.** Encryption and compression (data representation) are functions of which OSI layer?
(A) Application  (B) Session  (C) Presentation  (D) Transport

**Q3.** Dialog control, synchronisation and checkpointing belong to which OSI layer?
(A) Session  (B) Presentation  (C) Transport  (D) Data link

**Q4.** Framing and physical (MAC) addressing are performed at which OSI layer?
(A) Physical  (B) Data link  (C) Network  (D) Transport

**Q5.** The protocol data unit (PDU) of the transport layer is called a
(A) Frame  (B) Packet  (C) Segment  (D) Bit

**Q6.** The PDU at the network layer is a
(A) Frame  (B) Packet / datagram  (C) Segment  (D) Bit

**Q7.** "Frame" is the data unit of which OSI layer?
(A) Physical  (B) Data link  (C) Network  (D) Transport

**Q8.** A router primarily operates at which OSI layer?
(A) Layer 1  (B) Layer 2  (C) Layer 3  (D) Layer 4

**Q9.** A hub / repeater operates at which OSI layer?
(A) Physical  (B) Data link  (C) Network  (D) Transport

**Q10.** The correct top-to-bottom order (layer 7 → 1) of the OSI model is
(A) Application, Presentation, Session, Transport, Network, Data link, Physical
(B) Application, Session, Presentation, Transport, Network, Data link, Physical
(C) Application, Presentation, Session, Network, Transport, Data link, Physical
(D) Application, Transport, Session, Presentation, Network, Data link, Physical

**Q11.** The TCP/IP reference model consists of how many layers?
(A) 3  (B) 4  (C) 5  (D) 7

**Q12.** Which OSI layers have **no** separate counterpart in the TCP/IP model?
(A) Physical and data link
(B) Session and presentation
(C) Network and transport
(D) Application and transport

**Q13.** The TCP/IP Application layer maps to which OSI layers?
(A) Application only
(B) Application + Presentation + Session
(C) Application + Transport
(D) Presentation + Session

**Q14.** As data moves down the protocol stack, each layer adds its own
(A) trailer only  (B) header  (C) checksum only  (D) nothing

**Q15.** According to the notes, if asked for a single answer, ARP is best placed at which layer?
(A) Data link  (B) Network  (C) Transport  (D) Physical

**Q16.** Which statement correctly distinguishes the OSI and TCP/IP models?
(A) OSI protocols were implemented before its model was written
(B) The TCP/IP model was described *after* its protocols were already implemented
(C) OSI is the model on which the real Internet runs
(D) The TCP/IP model has seven layers

---

## Part B — Switching

**Q17.** Which switching technique sets up a dedicated physical path before any data flows?
(A) Datagram  (B) Circuit  (C) Message  (D) Virtual circuit

**Q18.** In datagram (packet) switching, packets of one message
(A) always follow the same path and arrive in order
(B) may follow different paths and arrive out of order
(C) reserve bandwidth end-to-end
(D) share one short VC identifier

**Q19.** Which switching method requires the **full destination address in every packet**?
(A) Circuit  (B) Virtual circuit  (C) Datagram  (D) None

**Q20.** Virtual circuit switching is best described as
(A) reserving dedicated bandwidth like circuit switching
(B) a logical path set up first, so packets follow one route in order, without reserving bandwidth
(C) each packet routed fully independently
(D) transmission with no setup phase

**Q21.** ATM and MPLS are examples of which switching technique?
(A) Circuit switching  (B) Datagram switching  (C) Virtual circuit switching  (D) Message switching

**Q22.** Which technique makes the most efficient use of a shared link for bursty traffic (statistical multiplexing)?
(A) Circuit switching  (B) Datagram switching  (C) Dedicated leased line  (D) FDM circuit

---

## Part C — Delays & performance

**Q23.** Transmission delay is given by
(A) d / v  (B) L / B  (C) B × RTT  (D) 2 × propagation delay

**Q24.** Propagation delay depends on
(A) packet size and bandwidth
(B) distance and medium's signal speed
(C) bandwidth only
(D) packet size only

**Q25.** A 1500-byte packet is sent on a 10 Mbps link. The transmission delay is
(A) 0.12 ms  (B) 1.2 ms  (C) 12 ms  (D) 0.6 ms

**Q26.** A link is 2000 km long and the signal travels at 2 × 10⁸ m/s. The propagation delay is
(A) 1 ms  (B) 10 ms  (C) 100 ms  (D) 20 ms

**Q27.** Round-trip time (RTT) is approximately
(A) equal to the propagation delay
(B) 2 × propagation delay
(C) equal to the transmission delay
(D) L / B

**Q28.** The bandwidth–delay product equals
(A) bandwidth × RTT  (B) bandwidth / RTT  (C) L / B  (D) d / v

**Q29.** A 10 Mbps link has an RTT of 20 ms. The bandwidth–delay product is
(A) 200,000 bits  (B) 20,000 bits  (C) 2,000,000 bits  (D) 2,000 bits

**Q30.** A packet of 1000 bytes is transmitted on a 100 Mbps link. The transmission delay is
(A) 8 µs  (B) 80 µs  (C) 800 µs  (D) 0.8 µs

**Q31.** On a long-distance link, which delay typically dominates?
(A) transmission delay  (B) propagation delay  (C) processing delay  (D) framing delay

---

## Part D — Physical layer & channel capacity

**Q32.** The Nyquist formula for the capacity of a **noiseless** channel is
(A) B log₂(1 + S/N)  (B) 2B log₂ L  (C) B log₂ L  (D) 2B log₂(1 + S/N)

**Q33.** The Shannon capacity of a **noisy** channel is
(A) B log₂(1 + S/N)  (B) 2B log₂ L  (C) 2B log₂(1 + S/N)  (D) B log₂(S/N)

**Q34.** For a channel with B = 3000 Hz and S/N = 3, the Shannon capacity is
(A) 3000 bps  (B) 6000 bps  (C) 9000 bps  (D) 12,000 bps

**Q35.** Using Nyquist with 4 signal levels and B = 3000 Hz, the capacity is
(A) 6000 bps  (B) 12,000 bps  (C) 3000 bps  (D) 24,000 bps

**Q36.** A signal-to-noise ratio of 30 dB corresponds to an S/N power ratio of
(A) 30  (B) 1000  (C) 100  (D) 300

**Q37.** Using Nyquist with 8 signal levels and B = 2000 Hz, the maximum data rate is
(A) 6000 bps  (B) 12,000 bps  (C) 16,000 bps  (D) 8000 bps

**Q38.** When both the Nyquist and Shannon limits apply, the achievable data rate is
(A) the larger of the two  (B) the smaller of the two  (C) their sum  (D) their average

---

## Part E — Framing & error detection

**Q39.** In bit stuffing, the sender inserts a 0 after how many consecutive 1s in the data?
(A) four  (B) five  (C) six  (D) seven

**Q40.** The HDLC framing flag pattern is
(A) 01111110  (B) 11111111  (C) 01111111  (D) 00000000

**Q41.** The data sequence `01111110` after bit stuffing becomes
(A) 011111010  (B) 011111110  (C) 0111101110  (D) 011111100

**Q42.** Which error-detection method is the strongest, detecting all burst errors shorter than the generator's degree?
(A) Simple parity  (B) Checksum  (C) CRC  (D) 2-D parity

**Q43.** A single (simple) parity bit fails to detect
(A) all single-bit errors
(B) any odd number of bit errors
(C) all even numbers of bit errors
(D) burst errors of length 1

**Q44.** CRC computation uses which arithmetic?
(A) binary with carries  (B) modulo-2 (XOR)  (C) decimal  (D) 1's-complement addition

**Q45.** Data = `1010`, generator G = `1011` (degree 3). The CRC (remainder) transmitted is
(A) 011  (B) 101  (C) 001  (D) 111

**Q46.** If the CRC generator has degree r, how many zeros are appended to the data before division?
(A) r  (B) r + 1  (C) r − 1  (D) 2r

**Q47.** In CRC, the receiver accepts the frame as error-free when the remainder is
(A) all ones  (B) zero  (C) equal to the generator  (D) equal to the data

**Q48.** Which of these uses a 1's-complement **checksum** rather than CRC?
(A) Ethernet  (B) IP, TCP and UDP  (C) HDLC  (D) Token Ring

---

## Part F — Hamming distance & Hamming code

**Q49.** To **detect** up to d bit errors, the minimum Hamming distance must satisfy
(A) d_min ≥ d  (B) d_min ≥ d + 1  (C) d_min ≥ 2d  (D) d_min ≥ 2d + 1

**Q50.** To **correct** up to d bit errors, the minimum Hamming distance must satisfy
(A) d_min ≥ d  (B) d_min ≥ d + 1  (C) d_min ≥ 2d  (D) d_min ≥ 2d + 1

**Q51.** A code whose minimum Hamming distance is 3 can
(A) correct 2 errors  (B) detect 3 errors  (C) correct 1 or detect 2 errors  (D) correct 3 errors

**Q52.** A code with minimum Hamming distance 5 can correct how many bit errors?
(A) 1  (B) 2  (C) 3  (D) 4

**Q53.** In a Hamming code, the number of parity bits r for m data bits must satisfy
(A) 2ʳ ≥ m + r + 1  (B) 2ʳ ≥ m + r  (C) 2ʳ ≥ m + 1  (D) 2ʳ ≥ 2m

**Q54.** For m = 4 data bits, the minimum number of parity bits required is
(A) 2  (B) 3  (C) 4  (D) 5

**Q55.** For m = 8 data bits, the minimum number of parity bits required is
(A) 3  (B) 4  (C) 5  (D) 8

**Q56.** In a Hamming code, the parity bits are placed at positions
(A) 1, 2, 3, 4 …  (B) powers of 2 (1, 2, 4, 8 …)  (C) the last positions  (D) all even positions

**Q57.** In a Hamming code the parity checks at positions 1 and 4 fail. The erroneous bit is at position
(A) 3  (B) 4  (C) 5  (D) 2

---

## Part G — Flow control & sliding window

**Q58.** The utilisation (efficiency) of a sliding-window protocol is
(A) W(1 + 2a)  (B) W / (1 + 2a)  (C) 1 / (1 + 2a)  (D) (1 + 2a) / W

**Q59.** In the efficiency formula, the parameter a equals
(A) T_trans / T_prop  (B) T_prop / T_trans  (C) T_prop × T_trans  (D) RTT

**Q60.** In Stop-and-Wait, the sender and receiver window sizes are respectively
(A) 1 and 1  (B) N and 1  (C) N and N  (D) 1 and N

**Q61.** With an m-bit sequence number, the maximum sender window in Go-Back-N is
(A) 2ᵐ  (B) 2ᵐ − 1  (C) 2ᵐ⁻¹  (D) m

**Q62.** With an m-bit sequence number, the maximum sender window in Selective Repeat is
(A) 2ᵐ  (B) 2ᵐ − 1  (C) 2ᵐ⁻¹  (D) m

**Q63.** The receiver window size in Go-Back-N is
(A) 1  (B) N  (C) 2ᵐ  (D) 2ᵐ⁻¹

**Q64.** The receiver window size in Selective Repeat is
(A) 1  (B) N  (C) 2ᵐ − 1  (D) 0

**Q65.** On detecting a lost frame, Go-Back-N retransmits
(A) only the lost frame
(B) the lost frame and all frames sent after it
(C) nothing
(D) the entire sequence space from 0

**Q66.** With T_trans = 1 ms and T_prop = 4 ms (a = 4), the efficiency of Stop-and-Wait is
(A) 11.1%  (B) 77.8%  (C) 50%  (D) 20%

**Q67.** With a = 4 and a Go-Back-N window of 7, the efficiency is
(A) 11.1%  (B) 77.8%  (C) 44.4%  (D) 100%

**Q68.** With a 4-bit sequence number, the maximum Go-Back-N window is
(A) 8  (B) 15  (C) 16  (D) 7

**Q69.** With a 4-bit sequence number, the maximum Selective Repeat window is
(A) 7  (B) 8  (C) 15  (D) 16

**Q70.** The optimum window size for 100% link utilisation is
(A) 2a  (B) 1 + 2a  (C) 1 + a  (D) 2 + a

---

## Part H — Medium access control

**Q71.** The maximum channel efficiency of **pure ALOHA** is approximately
(A) 18.4%  (B) 36.8%  (C) 50%  (D) 100%

**Q72.** The maximum channel efficiency of **slotted ALOHA** is approximately
(A) 18.4%  (B) 36.8%  (C) 50%  (D) 100%

**Q73.** The vulnerable period of pure ALOHA is
(A) 1 frame time  (B) 2 frame times  (C) half a frame time  (D) one RTT

**Q74.** The throughput of pure ALOHA is given by
(A) S = G·e^(−G)  (B) S = G·e^(−2G)  (C) S = G²·e^(−G)  (D) S = 2G·e^(−G)

**Q75.** In CSMA/CD, when a station detects a collision it
(A) continues transmitting the full frame
(B) aborts immediately, sends a jam signal, then backs off
(C) increases transmission power
(D) switches to another channel

**Q76.** In binary exponential backoff, after the nth collision the station waits a random number of slots chosen from
(A) [0, n]  (B) [0, 2ⁿ − 1]  (C) [1, 2ⁿ]  (D) [0, n²]

**Q77.** The minimum frame size in CSMA/CD is given by
(A) T_prop × Bandwidth  (B) 2 × T_prop × Bandwidth  (C) Bandwidth / T_prop  (D) T_trans × Bandwidth

**Q78.** In 10 Mbps Ethernet with a round-trip propagation delay of 51.2 µs, the minimum frame size is
(A) 64 bytes  (B) 512 bytes  (C) 128 bytes  (D) 46 bytes

**Q79.** A 100 Mbps CSMA/CD LAN spans 2.5 km with signal speed 2 × 10⁸ m/s. The minimum frame size is
(A) 64 bytes  (B) 312.5 bytes  (C) 625 bytes  (D) 128 bytes

**Q80.** CSMA/CA is used instead of CSMA/CD in
(A) wired Ethernet  (B) 802.11 wireless LANs  (C) Token Ring  (D) FDDI

**Q81.** The hidden-terminal problem in wireless networks is addressed by
(A) CSMA/CD  (B) the RTS/CTS handshake  (C) STP  (D) binary backoff

---

## Part I — Ethernet, bridging, devices & domains

**Q82.** The size range of an Ethernet frame (excluding preamble/SFD) is
(A) 46–1500 bytes  (B) 64–1518 bytes  (C) 20–1500 bytes  (D) 64–1500 bytes

**Q83.** The Ethernet MTU (maximum payload) is
(A) 1518 bytes  (B) 1500 bytes  (C) 64 bytes  (D) 46 bytes

**Q84.** A MAC address is how many bits long?
(A) 32  (B) 48  (C) 64  (D) 128

**Q85.** The minimum Ethernet payload (padded if smaller) is
(A) 46 bytes  (B) 64 bytes  (C) 26 bytes  (D) 18 bytes

**Q86.** Which device separates broadcast domains?
(A) Hub  (B) Switch  (C) Router  (D) Repeater

**Q87.** A switch creates one separate ___ domain per port.
(A) broadcast  (B) collision  (C) both broadcast and collision  (D) neither

**Q88.** A hub operates at which layer, and how many collision domains does it create?
(A) Layer 1; one collision domain shared by all ports
(B) Layer 2; one collision domain per port
(C) Layer 3; one per port
(D) Layer 1; one per port

**Q89.** A 24-port switch creates how many collision domains and broadcast domains?
(A) 24 and 24  (B) 24 and 1  (C) 1 and 24  (D) 1 and 1

**Q90.** A router with 4 active interfaces creates how many broadcast domains?
(A) 1  (B) 2  (C) 4  (D) 8

**Q91.** The Spanning Tree Protocol (IEEE 802.1D) is used to
(A) stop IP packets looping via TTL
(B) prevent layer-2 loops and broadcast storms
(C) detect collisions
(D) fragment large frames

**Q92.** When a switch receives a frame whose destination MAC is not in its table, it
(A) drops the frame
(B) floods it out all ports except the incoming one
(C) forwards it only to the router
(D) buffers it indefinitely

---

## Part J — IPv4 header & fragmentation

**Q93.** The minimum and maximum sizes of the IPv4 header are respectively
(A) 20 and 60 bytes  (B) 20 and 40 bytes  (C) 40 and 60 bytes  (D) 8 and 20 bytes

**Q94.** The IHL field expresses the header length in units of
(A) bytes  (B) bits  (C) 4-byte words  (D) 8-byte words

**Q95.** The fragment offset field is measured in units of
(A) 1 byte  (B) 4 bytes  (C) 8 bytes  (D) 16 bytes

**Q96.** The More Fragments (MF) flag is set to 1 on
(A) the last fragment only
(B) all fragments except the last
(C) all fragments
(D) only the first fragment

**Q97.** The primary purpose of the TTL field is to
(A) measure round-trip time
(B) prevent packets from looping forever
(C) set the priority
(D) count fragments

**Q98.** The IP protocol number for TCP is
(A) 1  (B) 6  (C) 17  (D) 41

**Q99.** The IP protocol number for ICMP is
(A) 1  (B) 6  (C) 17  (D) 2

**Q100.** The IPv4 header checksum covers
(A) the header and the data
(B) the header only
(C) the data only
(D) the options field only

**Q101.** Reassembly of IP fragments takes place at
(A) every router along the path
(B) the next hop
(C) the final destination only
(D) the source

**Q102.** A 4000-byte datagram (20-byte header + 3980 data bytes) crosses a link of MTU 1500. Into how many fragments is it split?
(A) 2  (B) 3  (C) 4  (D) 5

**Q103.** For the same 4000-byte datagram over MTU 1500, the fragment offset value carried by the **third** fragment is
(A) 185  (B) 296  (C) 370  (D) 2960

**Q104.** For the same datagram, the number of data bytes in the **last** fragment is
(A) 1480  (B) 1020  (C) 1040  (D) 520

**Q105.** A 2400-byte datagram (20-byte header + 2380 data) is fragmented onto an MTU of 700. The fragment offset of the **fourth** fragment is
(A) 170  (B) 255  (C) 340  (D) 85

---

## Part K — IPv4 addressing

**Q106.** The first-octet range of Class A addresses is
(A) 0–127  (B) 1–126  (C) 128–191  (D) 192–223

**Q107.** An address whose first octet is 200 belongs to which class?
(A) A  (B) B  (C) C  (D) D

**Q108.** Class D addresses (224–239) are reserved for
(A) private use  (B) loopback  (C) multicast  (D) experimental use

**Q109.** The IPv4 loopback address block is
(A) 10.0.0.0/8  (B) 127.0.0.0/8  (C) 169.254.0.0/16  (D) 192.168.0.0/16

**Q110.** Which of the following is a private (non-routable) address range?
(A) 11.0.0.0/8  (B) 172.16.0.0/12  (C) 192.169.0.0/16  (D) 128.0.0.0/8

**Q111.** The default subnet mask of a Class B network is
(A) 255.0.0.0  (B) 255.255.0.0  (C) 255.255.255.0  (D) 255.255.255.255

**Q112.** The address block 169.254.0.0/16 is used for
(A) multicast  (B) loopback  (C) link-local (APIPA) self-assignment  (D) broadcast

**Q113.** The limited broadcast address is
(A) 0.0.0.0  (B) 127.0.0.1  (C) 255.255.255.255  (D) 224.0.0.1

---

## Part L — Subnetting & CIDR

**Q114.** The number of usable host addresses in a block with prefix /n is
(A) 2^(32−n)  (B) 2^(32−n) − 2  (C) 2^n − 2  (D) 2^(32−n) + 2

**Q115.** A /26 network provides how many usable host addresses?
(A) 30  (B) 62  (C) 64  (D) 126

**Q116.** A /27 network provides how many usable host addresses?
(A) 14  (B) 30  (C) 32  (D) 62

**Q117.** A /30 network provides how many usable host addresses?
(A) 1  (B) 2  (C) 4  (D) 6

**Q118.** A /20 network contains how many total addresses?
(A) 1024  (B) 2048  (C) 4096  (D) 8192

**Q119.** The subnet mask for the prefix /27 is
(A) 255.255.255.192  (B) 255.255.255.224  (C) 255.255.255.240  (D) 255.255.255.128

**Q120.** The last octet of the subnet mask for /26 is
(A) 128  (B) 192  (C) 224  (D) 240

**Q121.** The block size (address increment) of a /26 subnet is
(A) 32  (B) 64  (C) 128  (D) 16

**Q122.** To which subnet does the host 200.10.5.100/27 belong?
(A) 200.10.5.64  (B) 200.10.5.96  (C) 200.10.5.100  (D) 200.10.5.128

**Q123.** The broadcast address of the subnet containing 200.10.5.100/27 is
(A) 200.10.5.95  (B) 200.10.5.127  (C) 200.10.5.126  (D) 200.10.5.128

**Q124.** From 192.168.1.0/24 you need 5 subnets, each with at least 25 usable hosts. The correct prefix is
(A) /25  (B) /26  (C) /27  (D) /28

**Q125.** The blocks 192.168.0.0/24, 192.168.1.0/24, 192.168.2.0/24 and 192.168.3.0/24 aggregate (supernet) to
(A) 192.168.0.0/21  (B) 192.168.0.0/22  (C) 192.168.0.0/23  (D) 192.168.0.0/20

**Q126.** How many /26 subnets fit inside a single /24 network?
(A) 2  (B) 4  (C) 8  (D) 16

**Q127.** For 172.16.0.0/20, the block size in the third octet is 16, so the next subnet after 172.16.0.0 is
(A) 172.16.1.0  (B) 172.16.15.0  (C) 172.16.16.0  (D) 172.16.32.0

**Q128.** The host 192.168.1.130 with a /25 mask belongs to which subnet?
(A) 192.168.1.0/25  (B) 192.168.1.64/25  (C) 192.168.1.128/25  (D) 192.168.1.192/25

**Q129.** A subnet must accommodate 100 hosts. The smallest prefix (longest mask) that works is
(A) /24  (B) /25  (C) /26  (D) /23

**Q130.** In VLSM design, subnets should be allocated
(A) smallest requirement first
(B) largest requirement first
(C) in random order
(D) alphabetically by name

**Q131.** Which set of blocks **cannot** be aggregated into a single supernet?
(A) 192.168.0.0/24 … 192.168.3.0/24
(B) 192.168.4.0/24 … 192.168.7.0/24
(C) 192.168.1.0/24 … 192.168.4.0/24
(D) 10.0.0.0/24 … 10.0.1.0/24

**Q132.** A /29 subnet provides how many usable hosts?
(A) 2  (B) 4  (C) 6  (D) 8

**Q133.** The subnet mask 255.255.255.240 corresponds to which prefix?
(A) /26  (B) /27  (C) /28  (D) /29

---

## Part M — IPv6

**Q134.** An IPv6 address is how many bits long?
(A) 32  (B) 64  (C) 128  (D) 256

**Q135.** The IPv6 base header has a fixed size of
(A) 20 bytes  (B) 32 bytes  (C) 40 bytes  (D) 60 bytes

**Q136.** Which address type does **not** exist in IPv6?
(A) Unicast  (B) Multicast  (C) Anycast  (D) Broadcast

**Q137.** In IPv6, fragmentation (if needed) is performed by
(A) every router  (B) the source host (via path MTU discovery)  (C) the destination  (D) the first-hop router

---

## Part N — Routing

**Q138.** The count-to-infinity problem is associated with
(A) link state routing  (B) distance vector routing  (C) flooding  (D) source routing

**Q139.** RIP is which type of protocol, and what metric does it use?
(A) link state, cost  (B) distance vector, hop count  (C) path vector, policy  (D) distance vector, bandwidth

**Q140.** In RIP, the value used as "infinity" is
(A) 15  (B) 16  (C) 255  (D) ∞ (unbounded)

**Q141.** OSPF is which type of routing protocol, and which algorithm does it run?
(A) distance vector, Bellman–Ford
(B) link state, Dijkstra
(C) path vector, Dijkstra
(D) link state, Bellman–Ford

**Q142.** BGP is classified as
(A) a distance-vector interior protocol
(B) a link-state interior protocol
(C) a path-vector exterior protocol
(D) a flooding protocol

**Q143.** Split horizon means a router will
(A) advertise a route back on the interface it was learned from
(B) never advertise a route back out the interface it was learned on
(C) flood link-state advertisements everywhere
(D) run Dijkstra on every update

**Q144.** In link state routing, each router shares its link-state information with
(A) its direct neighbours only
(B) all routers, by flooding
(C) the default gateway only
(D) a central controller

**Q145.** A routing table has entries 192.168.0.0/16, 192.168.1.0/24 and 192.168.1.128/25. For destination 192.168.1.130, which entry is used?
(A) 192.168.0.0/16  (B) 192.168.1.0/24  (C) 192.168.1.128/25  (D) the default route

**Q146.** In flooding, a received packet is forwarded
(A) on the shortest path only
(B) on every link except the one it arrived on
(C) back to the source
(D) to the default gateway

**Q147.** Which converges faster after a topology change?
(A) distance vector  (B) link state  (C) both identical  (D) flooding

**Q148.** In distance vector routing, a router exchanges its distance table with
(A) all routers in the network
(B) its directly connected neighbours only
(C) only the destination
(D) a route reflector

---

## Part O — Support protocols (ARP, DHCP, ICMP, NAT)

**Q149.** ARP resolves
(A) an IP address into a MAC address
(B) a MAC address into an IP address
(C) a domain name into an IP address
(D) a port number into a process

**Q150.** RARP performs the mapping
(A) IP → MAC  (B) MAC → IP  (C) name → IP  (D) IP → name

**Q151.** The DHCP address-assignment sequence is
(A) DORA (Discover, Offer, Request, Acknowledge)
(B) DROA
(C) ODRA
(D) RODA

**Q152.** DHCP uses which UDP ports for the server and client respectively?
(A) 53 / 54  (B) 67 / 68  (C) 68 / 67  (D) 80 / 8080

**Q153.** DHCP runs over which transport protocol, and why?
(A) TCP, for reliability
(B) UDP, because the client has no IP address yet to set up TCP
(C) ICMP
(D) SCTP

**Q154.** The `ping` utility uses which protocol?
(A) TCP  (B) UDP  (C) ICMP  (D) ARP

**Q155.** `traceroute` works by exploiting which ICMP message?
(A) Echo Reply  (B) Time Exceeded (from expiring TTL)  (C) Redirect  (D) Source Quench

**Q156.** How many port numbers does ICMP use?
(A) one  (B) two  (C) none — it rides directly on IP  (D) 1024

**Q157.** In PAT (NAT overload), multiple internal hosts sharing one public IP are distinguished by
(A) MAC addresses  (B) port numbers  (C) TTL values  (D) sequence numbers

**Q158.** Which NAT variant maps many private addresses to a single public address?
(A) Static NAT  (B) Dynamic NAT  (C) PAT / NAT overload  (D) Twice NAT

**Q159.** An ARP request is sent as a ___ and the ARP reply as a ___.
(A) unicast / broadcast  (B) broadcast / unicast  (C) broadcast / broadcast  (D) multicast / unicast

**Q160.** A drawback of NAT is that it
(A) encrypts all traffic
(B) breaks end-to-end connectivity and complicates peer-to-peer/VoIP
(C) resolves names to addresses
(D) increases the IPv4 address space

---

## Part P — Transport layer

**Q161.** TCP establishes a connection using
(A) a two-way handshake
(B) a three-way handshake (SYN, SYN-ACK, ACK)
(C) a four-way handshake
(D) no handshake

**Q162.** TCP connection termination normally requires
(A) 2 segments  (B) 3 segments  (C) 4 segments  (D) 1 segment

**Q163.** The minimum and maximum sizes of the TCP header are
(A) 8 and 20 bytes  (B) 20 and 40 bytes  (C) 20 and 60 bytes  (D) 20 and 65,535 bytes

**Q164.** The UDP header size is
(A) 8 bytes  (B) 20 bytes  (C) 12 bytes  (D) 16 bytes

**Q165.** Which of the following is true of UDP?
(A) It is connection-oriented and reliable
(B) It is connectionless, with no flow or congestion control
(C) It guarantees in-order delivery
(D) It uses a three-way handshake

**Q166.** TCP sequence numbers count
(A) segments  (B) bytes  (C) packets  (D) frames

**Q167.** How many flag bits does the TCP header carry (URG, ACK, PSH, RST, SYN, FIN)?
(A) 4  (B) 5  (C) 6  (D) 8

**Q168.** The TCP window-size field is how many bits wide?
(A) 8  (B) 16  (C) 32  (D) 4

**Q169.** During which TCP phase does the congestion window grow **exponentially**?
(A) slow start  (B) congestion avoidance  (C) fast recovery  (D) after a timeout only

**Q170.** During congestion avoidance, the congestion window grows
(A) exponentially  (B) linearly (about 1 MSS per RTT)  (C) not at all  (D) it is halved each RTT

**Q171.** Fast retransmit is triggered by
(A) a timeout  (B) 3 duplicate ACKs  (C) a single duplicate ACK  (D) a zero window

**Q172.** On a retransmission timeout, the congestion window is set to
(A) half its value  (B) 1 MSS  (C) ssthresh  (D) unchanged

**Q173.** Flow control in TCP protects the ___, while congestion control protects the ___.
(A) network / receiver  (B) receiver / network  (C) sender / receiver  (D) receiver / sender

**Q174.** Starting with cwnd = 1 MSS in slow start (RTT 1 → cwnd = 1), after how many RTTs does cwnd first reach 8 (ssthresh = 8)?
(A) 3  (B) 4  (C) 5  (D) 8

**Q175.** With cwnd = 12 MSS, a **timeout** occurs. The new ssthresh and cwnd are
(A) 6 and 6  (B) 6 and 1  (C) 12 and 1  (D) 6 and 12

**Q176.** With cwnd = 12 MSS, **three duplicate ACKs** occur (TCP Reno, fast recovery). The new cwnd is
(A) 1  (B) 6  (C) 12  (D) 3

**Q177.** The sender's effective (allowed) window equals
(A) the receiver window  (B) the congestion window  (C) min(receiver window, congestion window)  (D) their sum

**Q178.** AIMD stands for
(A) Additive Increase, Multiplicative Decrease
(B) Additive Increase, Multiplicative Increase
(C) Absolute Increase, Marginal Decrease
(D) Adaptive Interval, Managed Delay

---

## Part Q — Sockets & ports

**Q179.** A socket is defined by the pair
(A) (MAC address, port)  (B) (IP address, port)  (C) (IP address, MAC address)  (D) (port, protocol)

**Q180.** A TCP connection is uniquely identified by
(A) the destination port  (B) a 4-tuple (src IP, src port, dst IP, dst port)  (C) the source IP  (D) a 2-tuple (src IP, dst IP)

**Q181.** The well-known port range is
(A) 0–1023  (B) 1024–49151  (C) 49152–65535  (D) 0–65535

**Q182.** The dynamic / ephemeral port range is
(A) 0–1023  (B) 1024–49151  (C) 49152–65535  (D) 0–255

---

## Part R — Application layer

**Q183.** DNS ordinary queries use which transport protocol and port?
(A) TCP 53  (B) UDP 53  (C) UDP 67  (D) TCP 80

**Q184.** Which DNS record maps a name to an IPv4 address?
(A) A  (B) AAAA  (C) CNAME  (D) MX

**Q185.** Which DNS record maps a name to an IPv6 address?
(A) A  (B) AAAA  (C) PTR  (D) NS

**Q186.** Which DNS record identifies the mail server for a domain?
(A) A  (B) CNAME  (C) MX  (D) SOA

**Q187.** A CNAME record provides
(A) an IPv4 address  (B) an alias to another name  (C) a mail server  (D) a reverse lookup

**Q188.** In a **recursive** DNS query, the chain of servers is chased by
(A) the client  (B) the queried server  (C) the root only  (D) the authoritative server only

**Q189.** HTTP is described as a ___ protocol.
(A) connection-oriented  (B) stateless  (C) stateful  (D) reliable-at-layer-7

**Q190.** The well-known port numbers for HTTP, HTTPS, SMTP and DNS are respectively
(A) 80, 443, 25, 53  (B) 8080, 443, 110, 53  (C) 80, 8443, 25, 69  (D) 443, 80, 53, 25

**Q191.** Which HTTP status-code class indicates a **client** error?
(A) 2xx  (B) 3xx  (C) 4xx  (D) 5xx

**Q192.** The status code 500 means
(A) success  (B) redirection  (C) client error  (D) internal server error

**Q193.** Which HTTP method is **not** idempotent?
(A) GET  (B) PUT  (C) DELETE  (D) POST

**Q194.** A persistent HTTP connection (HTTP/1.1 keep-alive)
(A) opens a new TCP connection per object
(B) reuses one TCP connection for many objects
(C) uses UDP
(D) requires no handshake

**Q195.** SMTP is used for
(A) retrieving mail from the server
(B) sending/pushing mail (client→server and server→server)
(C) name resolution
(D) file transfer

**Q196.** Which mail-retrieval protocol keeps messages on the server and synchronises across devices?
(A) SMTP  (B) POP3  (C) IMAP  (D) MIME

**Q197.** The default ports for POP3 and IMAP are respectively
(A) 25 and 110  (B) 110 and 143  (C) 143 and 110  (D) 25 and 143

**Q198.** MIME was introduced because SMTP by itself carries only
(A) binary data  (B) 7-bit ASCII text  (C) compressed data  (D) encrypted data

**Q199.** FTP uses which two TCP ports?
(A) 20 (control) and 21 (data)
(B) 21 (control) and 20 (data)
(C) 21 (control) and 22 (data)
(D) 20 and 22

**Q200.** In FTP **passive** mode, the data connection is opened by
(A) the server connecting back to the client
(B) the client (making it NAT-friendly)
(C) a third-party relay
(D) the DNS server

**Q201.** FTP keeps command/reply exchange on a connection that is
(A) opened and closed for each file
(B) persistent for the whole session (control connection, port 21)
(C) over UDP
(D) shared with the data transfer

---

## Part S — Paper-I (English, Reasoning, GK)

**Q202.** Choose the word most nearly **opposite** in meaning to **TRANSPARENT**.
(A) Clear  (B) Opaque  (C) Obvious  (D) Visible

**Q203.** Select the correct sentence.
(A) He is senior than me by three years.
(B) He is senior to me by three years.
(C) He is more senior than me by three years.
(D) He is senior from me by three years.

**Q204.** In a row of 40 students, Rahul is 12th from the left end. What is his position from the right end?
(A) 27th  (B) 28th  (C) 29th  (D) 30th

**Q205.** The compound interest on ₹10,000 at 10% per annum for 2 years, compounded annually, is
(A) ₹2,000  (B) ₹2,100  (C) ₹2,200  (D) ₹2,310

**Q206.** The longest river of Tripura is the
(A) Gomati  (B) Khowai  (C) Manu  (D) Muhuri

**Q207.** Choose the correctly spelt word.
(A) Occassion  (B) Occasion  (C) Ocassion  (D) Occassion

**Q208.** Find the next term: 2, 6, 12, 20, 30, ?
(A) 40  (B) 42  (C) 44  (D) 36

**Q209.** If in a code MONDAY is written as OQPFCA, then FRIDAY is written as
(A) HTKFCA  (B) HTKFAC  (C) HKTFCA  (D) GTKFCA

**Q210.** A train 150 m long running at 54 km/h crosses a pole in
(A) 8 s  (B) 10 s  (C) 12 s  (D) 15 s

**Q211.** The synonym of **METICULOUS** is
(A) careless  (B) thorough  (C) hasty  (D) doubtful

**Q212.** The capital of Tripura is
(A) Agartala  (B) Aizawl  (C) Imphal  (D) Kohima

**Q213.** If A : B = 2 : 3 and B : C = 4 : 5, then A : C is
(A) 8 : 15  (B) 2 : 5  (C) 8 : 12  (D) 6 : 5

**Q214.** Fill in the blank: "She has been living here ___ 2010."
(A) for  (B) since  (C) from  (D) by

**Q215.** The average of the first 10 natural numbers is
(A) 5  (B) 5.5  (C) 6  (D) 4.5

**Q216.** Tripura became a full-fledged state of India in
(A) 1949  (B) 1956  (C) 1972  (D) 1963

---
---

# ✅ Answer Key

| Q | A | Q | A | Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | B | 37 | B | 73 | B | 109 | B | 145 | C | 181 | A |
| 2 | C | 38 | B | 74 | B | 110 | B | 146 | B | 182 | C |
| 3 | A | 39 | B | 75 | B | 111 | B | 147 | B | 183 | B |
| 4 | B | 40 | A | 76 | B | 112 | C | 148 | B | 184 | A |
| 5 | C | 41 | A | 77 | B | 113 | C | 149 | A | 185 | B |
| 6 | B | 42 | C | 78 | A | 114 | B | 150 | B | 186 | C |
| 7 | B | 43 | C | 79 | B | 115 | B | 151 | A | 187 | B |
| 8 | C | 44 | B | 80 | B | 116 | B | 152 | B | 188 | B |
| 9 | A | 45 | A | 81 | B | 117 | B | 153 | B | 189 | B |
| 10 | A | 46 | A | 82 | B | 118 | C | 154 | C | 190 | A |
| 11 | B | 47 | B | 83 | B | 119 | B | 155 | B | 191 | C |
| 12 | B | 48 | B | 84 | B | 120 | B | 156 | C | 192 | D |
| 13 | B | 49 | B | 85 | A | 121 | B | 157 | B | 193 | D |
| 14 | B | 50 | D | 86 | C | 122 | B | 158 | C | 194 | B |
| 15 | A | 51 | C | 87 | B | 123 | B | 159 | B | 195 | B |
| 16 | B | 52 | B | 88 | A | 124 | C | 160 | B | 196 | C |
| 17 | B | 53 | A | 89 | B | 125 | B | 161 | B | 197 | B |
| 18 | B | 54 | B | 90 | C | 126 | B | 162 | C | 198 | B |
| 19 | C | 55 | B | 91 | B | 127 | C | 163 | C | 199 | B |
| 20 | B | 56 | B | 92 | B | 128 | C | 164 | A | 200 | B |
| 21 | C | 57 | C | 93 | A | 129 | B | 165 | B | 201 | B |
| 22 | B | 58 | B | 94 | C | 130 | B | 166 | B | 202 | B |
| 23 | B | 59 | B | 95 | C | 131 | C | 167 | C | 203 | B |
| 24 | B | 60 | A | 96 | B | 132 | C | 168 | B | 204 | C |
| 25 | B | 61 | B | 97 | B | 133 | C | 169 | A | 205 | B |
| 26 | B | 62 | C | 98 | B | 134 | C | 170 | B | 206 | A |
| 27 | B | 63 | A | 99 | A | 135 | C | 171 | B | 207 | B |
| 28 | A | 64 | B | 100 | B | 136 | D | 172 | B | 208 | B |
| 29 | A | 65 | B | 101 | C | 137 | B | 173 | B | 209 | A |
| 30 | B | 66 | A | 102 | B | 138 | B | 174 | B | 210 | B |
| 31 | B | 67 | B | 103 | C | 139 | B | 175 | B | 211 | B |
| 32 | B | 68 | B | 104 | B | 140 | B | 176 | B | 212 | A |
| 33 | A | 69 | B | 105 | B | 141 | B | 177 | C | 213 | A |
| 34 | B | 70 | B | 106 | B | 142 | C | 178 | A | 214 | B |
| 35 | B | 71 | A | 107 | C | 143 | B | 179 | B | 215 | B |
| 36 | B | 72 | B | 108 | C | 144 | B | 180 | B | 216 | C |

---

# 📝 Detailed Solutions

**Q1. (B)** The network layer handles logical (IP) addressing, routing/forwarding and fragmentation. Physical (MAC) addressing is the data link layer's job.

**Q2. (C)** Translation, encryption and compression — all about data *representation* — are presentation-layer (layer 6) functions.

**Q3. (A)** Session setup/teardown, dialog control, synchronisation and checkpointing are session-layer (layer 5) functions.

**Q4. (B)** Framing, MAC addressing, error detection and medium access all sit at the data link layer (layer 2).

**Q5. (C)** The transport-layer PDU is the segment. Network = packet/datagram, data link = frame, physical = bit.

**Q6. (B)** The network layer's PDU is the packet (also called a datagram).

**Q7. (B)** The frame is the data link layer's PDU.

**Q8. (C)** A router is a layer-3 (network) device — it forwards on IP addresses.

**Q9. (A)** Hubs and repeaters are pure layer-1 (physical) devices that only regenerate bits.

**Q10. (A)** Top to bottom: Application, Presentation, Session, Transport, Network, Data link, Physical ("All People Seem To Need Data Processing").

**Q11. (B)** TCP/IP has 4 layers: Application, Transport, Internet, Network Access (Link).

**Q12. (B)** The session and presentation layers have no separate TCP/IP counterpart; their functions are folded into the application layer.

**Q13. (B)** The TCP/IP application layer absorbs OSI's Application + Presentation + Session layers.

**Q14. (B)** Encapsulation: each layer prepends its own header as data descends the stack; the receiver strips them on the way up.

**Q15. (A)** ARP's layer is disputed, but the notes advise preferring layer 2 (data link) — it deals in MAC addresses and never crosses a router.

**Q16. (B)** TCP/IP's protocols were implemented first and the model described afterwards; OSI was a theoretical reference model designed first.

**Q17. (B)** Circuit switching reserves a dedicated physical path for the whole conversation (traditional telephony).

**Q18. (B)** In datagram switching each packet is routed independently, so they may take different paths and arrive out of order.

**Q19. (C)** Datagram switching carries the full destination address in every packet; virtual circuits use a short VC identifier.

**Q20. (B)** A virtual circuit sets up a logical path first (packets follow one route, stay ordered) but does not reserve bandwidth — a compromise between circuit and datagram.

**Q21. (C)** ATM, Frame Relay and MPLS are virtual-circuit technologies.

**Q22. (B)** Datagram switching shares the link efficiently through statistical multiplexing — ideal for bursty traffic; circuit switching wastes idle capacity.

**Q23. (B)** Transmission delay = packet size ÷ bandwidth = L/B — the time to push all bits onto the wire.

**Q24. (B)** Propagation delay = distance ÷ signal speed (d/v); it is independent of packet size and bandwidth.

**Q25. (B)** (1500 × 8) / 10⁷ = 12000 / 10⁷ = 1.2 ms.

**Q26. (B)** d/v = 2 × 10⁶ m / 2 × 10⁸ m/s = 10 ms.

**Q27. (B)** RTT ≈ 2 × propagation delay (plus small transmission/processing terms).

**Q28. (A)** Bandwidth–delay product = bandwidth × RTT — the number of bits "in flight."

**Q29. (A)** 10⁷ bps × 0.02 s = 200,000 bits (= 25 KB).

**Q30. (B)** (1000 × 8) / 10⁸ = 8000 / 10⁸ = 80 µs.

**Q31. (B)** On long links propagation delay (d/v) dominates — this is why sliding-window protocols matter.

**Q32. (B)** Nyquist (noiseless): C = 2B log₂L.

**Q33. (A)** Shannon (noisy): C = B log₂(1 + S/N).

**Q34. (B)** C = 3000 × log₂(1 + 3) = 3000 × log₂4 = 3000 × 2 = 6000 bps.

**Q35. (B)** C = 2B log₂L = 2 × 3000 × log₂4 = 2 × 3000 × 2 = 12,000 bps.

**Q36. (B)** S/N = 10^(dB/10) = 10^(30/10) = 10³ = 1000.

**Q37. (B)** C = 2 × 2000 × log₂8 = 2 × 2000 × 3 = 12,000 bps.

**Q38. (B)** Compute both Nyquist and Shannon and take the smaller — the channel is limited by whichever constraint bites first.

**Q39. (B)** After five consecutive 1s in the data, the sender inserts a 0; the receiver removes it.

**Q40. (A)** The HDLC flag is 01111110 — the only place six 1s in a row can legitimately appear.

**Q41. (A)** Input 0 1111 1 1 0: after the fifth consecutive 1 a 0 is stuffed → 0 11111 **0** 1 0 = 011111010.

**Q42. (C)** CRC is the strongest of the listed methods, detecting all burst errors shorter than the generator's degree; used by Ethernet.

**Q43. (C)** A single parity bit catches all odd numbers of errors but misses every even number of bit errors.

**Q44. (B)** CRC divides using modulo-2 (XOR) arithmetic — no carries or borrows.

**Q45. (A)** Append 3 zeros: 1010000 ÷ 1011 (mod-2) gives remainder 011, so the CRC is 011 and the transmitted frame is 1010011.

**Q46. (A)** Exactly r zeros are appended, where r is the degree of the generator.

**Q47. (B)** A remainder of 0 after dividing the received frame by the generator means no error was detected.

**Q48. (B)** IP, TCP and UDP use a 1's-complement checksum; Ethernet/HDLC/Token Ring use CRC.

**Q49. (B)** To detect up to d errors, d_min ≥ d + 1.

**Q50. (D)** To correct up to d errors, d_min ≥ 2d + 1 (correction is harder, needs the larger distance).

**Q51. (C)** d_min = 3: detect 2 (3 ≥ 2+1) or correct 1 (3 ≥ 2×1+1).

**Q52. (B)** Correct d needs 2d+1 ≤ 5 → d = 2.

**Q53. (A)** Hamming: 2ʳ ≥ m + r + 1 (r parity bits must locate any of m+r positions plus "no error").

**Q54. (B)** r = 3: 2³ = 8 ≥ 4 + 3 + 1 = 8 ✅ → the (7,4) code. r = 2 gives 4 < 4+2+1 = 7.

**Q55. (B)** r = 4: 2⁴ = 16 ≥ 8 + 4 + 1 = 13 ✅; r = 3 gives 8 < 8+3+1 = 12.

**Q56. (B)** Parity bits occupy positions that are powers of 2: 1, 2, 4, 8, ….

**Q57. (C)** The syndrome is the binary number of the failed checks: positions 1 and 4 → 101₂ = 5, so bit 5 is wrong.

**Q58. (B)** Sliding-window efficiency η = W / (1 + 2a).

**Q59. (B)** a = T_propagation / T_transmission.

**Q60. (A)** Stop-and-Wait uses sender window 1 and receiver window 1.

**Q61. (B)** Go-Back-N needs one spare sequence number → max window 2ᵐ − 1.

**Q62. (C)** Selective Repeat needs the window ≤ half the sequence space → 2ᵐ⁻¹.

**Q63. (A)** Go-Back-N's receiver accepts only in order, so its receiver window is 1.

**Q64. (B)** Selective Repeat buffers out-of-order frames, so its receiver window is N.

**Q65. (B)** On loss, GBN retransmits the lost frame and all frames sent after it (cumulative ACKs, no receiver buffering).

**Q66. (A)** η = 1 / (1 + 2a) = 1 / (1 + 8) = 1/9 ≈ 11.1%.

**Q67. (B)** η = W / (1 + 2a) = 7 / 9 ≈ 77.8%.

**Q68. (B)** GBN max window = 2⁴ − 1 = 15.

**Q69. (B)** SR max window = 2^(4−1) = 2³ = 8.

**Q70. (B)** For 100% utilisation the window must equal 1 + 2a.

**Q71. (A)** Pure ALOHA peaks at 1/(2e) ≈ 18.4%.

**Q72. (B)** Slotted ALOHA peaks at 1/e ≈ 36.8% (double pure ALOHA, since slotting halves the vulnerable period).

**Q73. (B)** Pure ALOHA's vulnerable period is 2 frame times (a collision occurs if another frame starts within one frame time before or after).

**Q74. (B)** Pure ALOHA throughput S = G·e^(−2G); slotted ALOHA S = G·e^(−G).

**Q75. (B)** CSMA/CD aborts on collision, sends a short jam signal, then backs off and retries.

**Q76. (B)** After the nth collision the wait is a random number of slots from [0, 2ⁿ − 1] (capped at n = 10, give up after 16).

**Q77. (B)** Minimum frame size = 2 × T_prop × Bandwidth (so the sender is still transmitting when the collision signal returns).

**Q78. (A)** 10⁷ × 51.2 × 10⁻⁶ = 512 bits = 64 bytes — exactly Ethernet's minimum.

**Q79. (B)** One-way = 2500 / 2×10⁸ = 12.5 µs; RTT = 25 µs; min frame = 10⁸ × 25×10⁻⁶ = 2500 bits = 312.5 bytes.

**Q80. (B)** 802.11 wireless uses CSMA/CA because a station cannot listen while transmitting and collisions are hard to detect on radio.

**Q81. (B)** The RTS/CTS handshake reserves the channel and solves the hidden-terminal problem.

**Q82. (B)** Ethernet frames range 64–1518 bytes (excluding preamble/SFD).

**Q83. (B)** The Ethernet MTU (max payload) is 1500 bytes.

**Q84. (B)** A MAC address is 48 bits (6 bytes), written as 12 hex digits.

**Q85. (A)** Minimum payload is 46 bytes (6+6+2+46+4 = 64), padded if less.

**Q86. (C)** Only a router (or a VLAN) separates broadcast domains; switches forward broadcasts.

**Q87. (B)** A switch creates one collision domain per port but a single broadcast domain (unless VLANs).

**Q88. (A)** A hub is a layer-1 device; all its ports share one collision domain.

**Q89. (B)** A 24-port switch = 24 collision domains, 1 broadcast domain.

**Q90. (C)** A router creates one broadcast domain per interface → 4.

**Q91. (B)** STP disables redundant links to prevent layer-2 loops and broadcast storms (layer-2 frames have no TTL).

**Q92. (B)** Unknown-destination (or broadcast/multicast) frames are flooded out all ports except the incoming one.

**Q93. (A)** IPv4 header: minimum 20 bytes (IHL = 5), maximum 60 bytes (IHL = 15).

**Q94. (C)** IHL counts the header length in 4-byte words (min 5 = 20 bytes, max 15 = 60 bytes).

**Q95. (C)** The fragment offset is measured in 8-byte units.

**Q96. (B)** MF = 1 on every fragment except the last (MF = 0 marks the last).

**Q97. (B)** TTL is decremented at each router; at 0 the packet is dropped, preventing infinite loops.

**Q98. (B)** TCP's protocol number is 6 (UDP = 17, ICMP = 1).

**Q99. (A)** ICMP's protocol number is 1.

**Q100. (B)** The IPv4 header checksum covers the header only and is recomputed at every hop (because TTL changes).

**Q101. (C)** Fragments may take different routes, so reassembly happens only at the final destination, never at intermediate routers.

**Q102. (B)** Max data per fragment = 1500 − 20 = 1480 (÷8 = 185 ✅). 3980 / 1480 → 1480 + 1480 + 1020 = 3980, so **3 fragments**.

**Q103. (C)** Offsets (÷8): fragment 1 = 0, fragment 2 = 1480/8 = 185, fragment 3 = 2960/8 = **370**.

**Q104. (B)** Last fragment carries 3980 − 1480 − 1480 = **1020** data bytes, with MF = 0.

**Q105. (B)** Max data = 700 − 20 = 680 (÷8 = 85 ✅). Fragments: 680, 680, 680, 340. Offsets: 0, 85, 170, **255** (3×85).

**Q106. (B)** Class A first octet is 1–126 (0 and 127 are reserved).

**Q107. (C)** First octet 192–223 is Class C, so 200.x.x.x is Class C.

**Q108. (C)** Class D (224–239) is reserved for multicast.

**Q109. (B)** Loopback is 127.0.0.0/8 (127.0.0.1 = "this machine").

**Q110. (B)** 172.16.0.0/12 is a private range; 192.169/16 and 11/8 are public, 128/8 is public.

**Q111. (B)** Class B default mask is 255.255.0.0 (/16).

**Q112. (C)** 169.254.0.0/16 is link-local (APIPA), self-assigned when DHCP fails.

**Q113. (C)** 255.255.255.255 is the limited broadcast (not forwarded by routers).

**Q114. (B)** Usable hosts = 2^(32−n) − 2 (subtracting the network and broadcast addresses).

**Q115. (B)** /26 → 2⁶ − 2 = 64 − 2 = 62.

**Q116. (B)** /27 → 2⁵ − 2 = 32 − 2 = 30.

**Q117. (B)** /30 → 2² − 2 = 4 − 2 = 2 (point-to-point links).

**Q118. (C)** /20 → 2^(32−20) = 2¹² = 4096 addresses.

**Q119. (B)** /27 = 27 ones then 5 zeros → last octet 11100000 = 224 → 255.255.255.224.

**Q120. (B)** /26 last octet = 11000000 = 192.

**Q121. (B)** Block size = 256 − 192 = 64.

**Q122. (B)** /27 block size = 256 − 224 = 32; boundaries …64, 96, 128. 100 lies in 96–127 → network 200.10.5.96 (100 ÷ 32 = 3 → 3×32 = 96).

**Q123. (B)** That /27 subnet spans .96–.127, so the broadcast is 200.10.5.127.

**Q124. (C)** 25 hosts needs 5 host bits (2⁵ − 2 = 30 ≥ 25; 4 bits gives only 14) → /27, which yields 2³ = 8 subnets ≥ 5 ✅.

**Q125. (B)** Four contiguous, aligned /24s combine into a /22: 192.168.0.0/22.

**Q126. (B)** /24 → /26 borrows 2 bits → 2² = 4 subnets.

**Q127. (C)** /20 block size in the third octet = 256 − 240 = 16, so 172.16.0.0 → next is 172.16.16.0.

**Q128. (C)** /25 block size = 128; boundaries .0 and .128. 130 lies in 128–255 → subnet 192.168.1.128/25.

**Q129. (B)** 100 hosts needs 7 host bits (2⁷ − 2 = 126 ≥ 100; 6 bits gives only 62) → prefix /25.

**Q130. (B)** VLSM allocates the largest requirement first, then works downward, to avoid fragmenting a block needed whole.

**Q131. (C)** 192.168.1.0 … 4.0 are not aligned on a 4-block boundary (1 is not a multiple of 4), so they cannot aggregate; the others are aligned/contiguous.

**Q132. (C)** /29 → 2³ − 2 = 8 − 2 = 6 usable hosts.

**Q133. (C)** 240 = 11110000 → 4 ones in the last octet → 24 + 4 = /28.

**Q134. (C)** An IPv6 address is 128 bits, written as eight groups of four hex digits.

**Q135. (C)** The IPv6 base header is a fixed 40 bytes (options go in extension headers).

**Q136. (D)** IPv6 has unicast, multicast and anycast — but no broadcast (its role is taken by multicast).

**Q137. (B)** In IPv6 routers do not fragment; the source performs path MTU discovery.

**Q138. (B)** Count-to-infinity is a distance-vector problem ("bad news travels slowly").

**Q139. (B)** RIP is a distance-vector protocol using hop count as its metric (max 15).

**Q140. (B)** RIP defines 16 as "infinity" (so max usable hop count is 15).

**Q141. (B)** OSPF is a link-state protocol; each router floods LSAs and runs Dijkstra on the full topology.

**Q142. (C)** BGP is a path-vector, exterior gateway protocol used between autonomous systems, choosing routes on policy.

**Q143. (B)** Split horizon: never advertise a route back out the interface it was learned from — a count-to-infinity mitigation.

**Q144. (B)** Link-state routers flood their link states to all routers, so each builds an identical topology map.

**Q145. (C)** Longest prefix match: all three match, and /25 is the most specific → 192.168.1.128/25.

**Q146. (B)** Flooding forwards a packet on every link except the one it arrived on.

**Q147. (B)** Link state converges faster than distance vector (full topology, Dijkstra, immune to count-to-infinity).

**Q148. (B)** Distance-vector routers exchange their distance tables with directly connected neighbours only.

**Q149. (A)** ARP maps a known IP address to its MAC address (local LAN only).

**Q150. (B)** RARP maps MAC → IP (now obsolete, replaced by DHCP).

**Q151. (A)** DHCP uses DORA: Discover, Offer, Request, Acknowledge.

**Q152. (B)** DHCP uses UDP ports 67 (server) and 68 (client).

**Q153. (B)** DHCP runs over UDP because the client has no IP address yet and cannot set up a TCP connection.

**Q154. (C)** `ping` uses ICMP Echo Request / Echo Reply.

**Q155. (B)** `traceroute` sends packets with increasing TTL and reads the ICMP Time Exceeded replies from each hop.

**Q156. (C)** ICMP has no port numbers — it rides directly on IP (protocol 1), not on a transport protocol.

**Q157. (B)** PAT distinguishes internal hosts sharing one public IP by rewriting/tracking port numbers.

**Q158. (C)** PAT (NAT overload) maps many private addresses to one public address — what home routers do.

**Q159. (B)** ARP request is broadcast ("who has this IP?"); the owner replies by unicast with its MAC.

**Q160. (B)** NAT breaks end-to-end connectivity (inbound connections need port forwarding) and complicates P2P/VoIP and violates layering.

**Q161. (B)** TCP setup is a three-way handshake: SYN → SYN-ACK → ACK.

**Q162. (C)** Teardown takes four segments (FIN, ACK, FIN, ACK) because each direction is closed independently.

**Q163. (C)** TCP header is 20–60 bytes (20 minimum, up to 40 bytes of options).

**Q164. (A)** The UDP header is a fixed 8 bytes.

**Q165. (B)** UDP is connectionless, unreliable, unordered, with no flow or congestion control.

**Q166. (B)** TCP sequence numbers count bytes, which is why TCP is a byte-stream protocol.

**Q167. (C)** TCP has 6 flags: URG, ACK, PSH, RST, SYN, FIN.

**Q168. (B)** The window-size field is 16 bits (caps the window at 65,535 bytes without scaling).

**Q169. (A)** In slow start cwnd doubles every RTT (exponential) until it reaches ssthresh.

**Q170. (B)** In congestion avoidance cwnd grows by about 1 MSS per RTT (linear, additive increase).

**Q171. (B)** Three duplicate ACKs trigger fast retransmit (immediate resend without waiting for timeout).

**Q172. (B)** On a timeout, ssthresh = cwnd/2 and cwnd resets to 1 MSS (slow start restarts).

**Q173. (B)** Flow control protects the receiver's buffer; congestion control protects the network.

**Q174. (B)** cwnd doubles each RTT: RTT1 = 1, RTT2 = 2, RTT3 = 4, RTT4 = 8 → 4 RTTs.

**Q175. (B)** On timeout: ssthresh = 12/2 = 6, cwnd resets to 1.

**Q176. (B)** Three duplicate ACKs (Reno fast recovery): ssthresh = cwnd/2 = 6, cwnd = 6 (not reset to 1).

**Q177. (C)** The effective window = min(receiver window, congestion window).

**Q178. (A)** AIMD = Additive Increase (congestion avoidance), Multiplicative Decrease (halving on loss).

**Q179. (B)** A socket = (IP address, port number).

**Q180. (B)** A TCP connection is identified by the 4-tuple (source IP, source port, destination IP, destination port).

**Q181. (A)** Well-known ports are 0–1023.

**Q182. (C)** Dynamic/ephemeral ports are 49152–65535 (registered are 1024–49151).

**Q183. (B)** DNS ordinary queries use UDP port 53 (TCP for zone transfers and large replies).

**Q184. (A)** An A record maps a name to an IPv4 address.

**Q185. (B)** An AAAA record maps a name to an IPv6 address.

**Q186. (C)** An MX record identifies the mail-exchange server for a domain.

**Q187. (B)** A CNAME record is an alias pointing to another name.

**Q188. (B)** In a recursive query the queried server chases the whole chain and returns the final answer; in iterative the client does.

**Q189. (B)** HTTP is stateless — each request is independent (state is added via cookies/sessions).

**Q190. (A)** HTTP 80, HTTPS 443, SMTP 25, DNS 53.

**Q191. (C)** 4xx = client error (e.g. 404 Not Found); 5xx = server error.

**Q192. (D)** 500 = Internal Server Error (a 5xx server-side error).

**Q193. (D)** POST is not idempotent (repeating it may create duplicate resources); GET, PUT, DELETE are idempotent.

**Q194. (B)** A persistent connection reuses one TCP connection for many objects, roughly halving page-load time.

**Q195. (B)** SMTP pushes/sends mail (client→server and server→server); POP3/IMAP retrieve.

**Q196. (C)** IMAP keeps mail on the server and syncs across devices; POP3 downloads and deletes.

**Q197. (B)** POP3 = port 110, IMAP = port 143.

**Q198. (B)** MIME exists because SMTP handles only 7-bit ASCII; MIME encodes binary/attachments/non-ASCII.

**Q199. (B)** FTP uses two TCP connections: control on port 21 (whole session) and data on port 20 (per transfer).

**Q200. (B)** In passive mode the client opens both connections, making FTP NAT/firewall-friendly (today's default).

**Q201. (B)** The control connection (port 21) is persistent for the entire session, carrying commands/replies; the data connection is opened per file.

**Q202. (B)** *Transparent* = clear/letting light through; its opposite is **opaque**. A, C, D are synonyms.

**Q203. (B)** Latin comparatives (senior, junior, superior…) take **to**, never *than*, and are never used with *more*.

**Q204. (C)** Position from right = 40 − 12 + 1 = **29th**.

**Q205. (B)** 10000 × (1.1)² = 12,100; CI = 12,100 − 10,000 = **₹2,100**.

**Q206. (A)** The **Gomati** is Tripura's longest river.

**Q207. (B)** The correct spelling is **Occasion** (one c-pair "cc", single "s").

**Q208. (B)** Differences are 4, 6, 8, 10, so next difference is 12 → 30 + 12 = **42** (pattern n(n+1)).

**Q209. (A)** Each letter shifts +2: M→O, O→Q, N→P, D→F, A→C, Y→A. Applying to FRIDAY: F→H, R→T, I→K, D→F, A→C, Y→A = **HTKFCA**.

**Q210. (B)** 54 km/h = 15 m/s; time = 150 / 15 = **10 s**.

**Q211. (B)** *Meticulous* means careful and precise → **thorough**.

**Q212. (A)** The capital of Tripura is **Agartala**.

**Q213. (A)** A:B = 2:3, B:C = 4:5 → scale to B: A:B = 8:12, B:C = 12:15 → A:C = **8:15**.

**Q214. (B)** "Since" is used with a point in time (2010); "for" is used with durations.

**Q215. (B)** Average of 1–10 = (1+10)/2 = **5.5**.

**Q216. (C)** Tripura became a full-fledged state on 21 January **1972**.
