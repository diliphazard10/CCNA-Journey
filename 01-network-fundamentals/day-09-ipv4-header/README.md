# Day 09 — IPv4 Header

> **CCNA 200-301 · IPv4 Packet Structure**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-09-green)
![Topic](https://img.shields.io/badge/Topic-IPv4%20Header-orange)

## 📌 Overview

Today I learned about the **IPv4 packet structure** and studied the fields of the **IPv4 header** in detail.

## 🎯 Learning Objectives

- Explain the IPv4 packet and header structure.
- Identify the major IPv4 header fields.
- Explain Version, IHL, DSCP, ECN and Total Length.
- Explain Identification, Flags and Fragment Offset.
- Explain TTL and how routers change it.
- Explain the Protocol field.
- Explain the IPv4 Header Checksum.
- Identify source and destination IPv4 addresses.
- Understand IPv4 options and padding.
- Analyze IPv4 packets in Packet Tracer Simulation Mode.

---

# 📦 1. IPv4 Packet Structure

```text
+-------------------------------+
|          IPv4 Header          |
+-------------------------------+
|            Payload            |
+-------------------------------+
```

The IPv4 header contains Layer 3 control information. The payload carries upper-layer data such as a TCP segment, UDP datagram, or ICMP message.

A standard IPv4 header without options is **20 bytes**. Options can make it larger.

---

# 🧩 2. IPv4 Header Fields

```text
Version
IHL
DSCP
ECN
Total Length
Identification
Flags
Fragment Offset
TTL
Protocol
Header Checksum
Source Address
Destination Address
Options + Padding
```

## Version

- **4 bits**
- Identifies the IP version.
- IPv4 has a value of `4`.

## IHL — Internet Header Length

- **4 bits**
- Specifies IPv4 header length in 32-bit words.
- Minimum value: `5`
- `5 × 4 bytes = 20 bytes`

## DSCP

- **6 bits**
- Differentiated Services Code Point.
- Used for traffic classification and QoS.

## ECN

- **2 bits**
- Explicit Congestion Notification.
- Allows congestion signaling when supported and configured.

## Total Length

- **16 bits**
- Specifies the entire IPv4 packet size, including header and payload.
- Maximum value represented: **65,535 bytes**.

## Identification

- **16 bits**
- Used with fragmentation.
- Fragments from the same original IPv4 packet share the same identification value.

## Flags

- **3 bits**
- Controls fragmentation.
- Important flags:
  - `DF` — Don't Fragment
  - `MF` — More Fragments

## Fragment Offset

- **13 bits**
- Identifies where a fragment belongs within the original packet.
- Works with Identification and Flags.

## TTL — Time To Live

- **8 bits**
- Prevents packets from circulating indefinitely.
- A router normally decreases TTL by 1 when forwarding a packet.

Example:

```text
Host → TTL 64
Router 1 → TTL 63
Router 2 → TTL 62
Destination → TTL 62
```

If TTL reaches zero, the packet is discarded. A router can send an ICMP Time Exceeded message.

> TTL is effectively a hop-count limit during forwarding, not a timer measured in seconds.

## Protocol

- **8 bits**
- Identifies the upper-layer protocol carried inside IPv4.

Common values:

```text
ICMP = 1
TCP  = 6
UDP  = 17
```

## Header Checksum

- **16 bits**
- Detects errors in the IPv4 header.
- It does not protect the payload.
- Because fields such as TTL change at routers, the IPv4 header checksum is recalculated during forwarding.

## Source Address

- **32 bits**
- IPv4 address of the sender.

## Destination Address

- **32 bits**
- IPv4 address of the intended destination.
- Routers use it for Layer 3 forwarding decisions.

## Options and Padding

- Optional.
- The minimum IPv4 header is 20 bytes.
- Options increase the header size.
- Padding aligns the header to a 32-bit boundary.

---

# 📋 3. Header Field Summary

| Field | Size | Purpose |
|---|---:|---|
| Version | 4 bits | IP version |
| IHL | 4 bits | Header length |
| DSCP | 6 bits | QoS classification |
| ECN | 2 bits | Congestion notification |
| Total Length | 16 bits | Entire packet size |
| Identification | 16 bits | Fragment identification |
| Flags | 3 bits | Fragmentation control |
| Fragment Offset | 13 bits | Fragment position |
| TTL | 8 bits | Hop-limit mechanism |
| Protocol | 8 bits | Upper-layer protocol |
| Header Checksum | 16 bits | IPv4 header error detection |
| Source Address | 32 bits | Sender |
| Destination Address | 32 bits | Receiver |
| Options + Padding | Variable | Optional information/alignment |

---

# 🔄 4. Encapsulation

```text
Application Data
       ↓
TCP/UDP Header + Data
       ↓
IPv4 Header + TCP/UDP Segment
       ↓
Ethernet Header + IPv4 Packet + Ethernet Trailer
```

This connects today's lesson to the TCP/IP and OSI models from Day 3.

---

# 🚦 5. What Happens at a Router?

A router generally:

```text
Receive Layer 2 frame
        ↓
Process IPv4 packet
        ↓
Decrement TTL
        ↓
Recalculate IPv4 header checksum
        ↓
Look up destination IP
        ↓
Forward toward next hop
        ↓
Build a new Layer 2 frame
```

Important observation:

```text
Layer 2 header → changes at each hop
TTL → decreases at each router
Source/Destination IP → normally remain unchanged
```

NAT and some other features can modify IP addresses.

---

# 🧪 6. Packet Tracer Lab

Suggested topology:

```text
PC1 ── R1 ── R2 ── PC2
```

Send traffic:

```text
PC1 → ping PC2
```

Use **Simulation Mode** and inspect the IPv4 packet as it travels.

Observe:

```text
Source IP
Destination IP
TTL
Protocol
IPv4 header
Layer 2 header
```

## Lab Questions

1. What is the source IP?
2. What is the destination IP?
3. What is the TTL before the router?
4. What is the TTL after the router?
5. What is the Protocol value?
6. Does the Layer 2 header stay the same?
7. Which IPv4 header fields change during normal router forwarding?

---

# 🧠 7. CCNA Memory Sheet

```text
IPv4 version
→ 4

Minimum IPv4 header
→ 20 bytes

IHL
→ Header length
→ Minimum = 5

Total Length
→ Header + Payload
→ Maximum = 65,535 bytes

Identification
→ Fragment identification

DF
→ Don't Fragment

MF
→ More Fragments

Fragment Offset
→ Fragment position

TTL
→ Decreases by 1 at each router

Protocol
→ Upper-layer protocol

ICMP
→ 1

TCP
→ 6

UDP
→ 17

Header Checksum
→ IPv4 header

Source/Destination
→ 32-bit IPv4 addresses
```

---

# ⚠️ 8. Common Mistakes

### Mistake 1 — TTL is seconds

TTL is used as a hop-count limit during forwarding.

### Mistake 2 — Header checksum covers the payload

IPv4 Header Checksum applies to the IPv4 header.

### Mistake 3 — Protocol field means IPv4

The Protocol field identifies the upper-layer protocol, such as TCP, UDP, or ICMP.

### Mistake 4 — Routers forward the same Ethernet frame

Routers normally create a new Layer 2 frame for the next link.

### Mistake 5 — IPv4 headers are always 20 bytes

20 bytes is the minimum. Options can increase the header size.

---

# 📚 9. Revision Questions

1. What is the minimum IPv4 header size?
2. What does Version identify?
3. What does IHL represent?
4. What is the minimum IHL value?
5. What does Total Length include?
6. What is the maximum IPv4 packet size represented by Total Length?
7. What is Identification used for?
8. What do DF and MF mean?
9. What is Fragment Offset used for?
10. Why does a router decrement TTL?
11. What happens when TTL reaches zero?
12. What does Protocol identify?
13. What are the protocol numbers for TCP, UDP and ICMP?
14. What does the Header Checksum protect?
15. What are the sizes of the source and destination addresses?
16. Why can an IPv4 header be larger than 20 bytes?
17. What happens to the Layer 2 frame when a router forwards an IPv4 packet?

---

# 📈 10. Day 09 Reflection

## What I Learned

- IPv4 packet structure
- IPv4 header
- Header fields
- TTL
- Protocol
- Source and destination IP
- Fragmentation fields
- Header checksum
- Options and padding
- Packet encapsulation
- Packet analysis

## What I Need to Practice

- Memorizing the IPv4 header fields
- Understanding each field's purpose
- Observing TTL changes across routers
- Understanding TCP/UDP/ICMP protocol numbers
- Understanding fragmentation fields
- Analyzing IPv4 packets in Packet Tracer

---

# 🚀 Day 09 Status

**Completed ✅**

- [x] IPv4 packet structure
- [x] IPv4 header fields
- [x] TTL
- [x] Protocol
- [x] Source/Destination IP
- [x] Fragmentation fields
- [x] Header checksum
- [x] Packet analysis
- [x] Simulation practice

---

