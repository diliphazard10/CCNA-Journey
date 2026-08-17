# Day 03 Notes — TCP/IP Model & OSI Model

## CCNA 200-301 v1.1 | Domain 1 — Network Fundamentals

---

## 1. Why Networking Models?

Networking models divide complex communication into layers.

### Benefits

- Common vocabulary
- Easier troubleshooting
- Protocol organization
- Vendor interoperability
- Easier learning and design

Basic concept:

```text
Application
    ↓
Transport
    ↓
Network
    ↓
Data Link
    ↓
Physical
```

---

# 2. Basic Networking History

## OSI

**OSI = Open Systems Interconnection**

The OSI reference model was developed by ISO as a common framework for understanding network communication.

It has **7 layers**.

## TCP/IP

TCP/IP developed from networking research associated with ARPANET and the U.S. Department of Defense research community.

It became the foundation of the modern Internet.

### Remember

```text
OSI
→ Primarily a reference model

TCP/IP
→ Practical protocol suite + model
```

---

# 3. OSI Model

```text
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
```

| Layer | Name | Main Function |
|---:|---|---|
| 7 | Application | Network services |
| 6 | Presentation | Data representation |
| 5 | Session | Session management |
| 4 | Transport | End-to-end transport |
| 3 | Network | Logical addressing/routing |
| 2 | Data Link | Frames/MAC/local delivery |
| 1 | Physical | Bits/physical transmission |

---

# 4. Layer 7 — Application

Network services used by applications.

Examples:

```text
HTTP
HTTPS
DNS
DHCP
SSH
FTP
SMTP
```

Think:

> What network service does the application need?

---

# 5. Layer 6 — Presentation

Traditionally concerned with:

- Data formatting
- Encoding
- Encryption/decryption
- Compression

Modern TCP/IP implementations often handle these functions across applications and libraries rather than as a distinct layer.

---

# 6. Layer 5 — Session

Traditionally concerned with:

- Establishing sessions
- Managing sessions
- Terminating sessions

Modern TCP/IP systems often do not implement a separate Session layer.

---

# 7. Layer 4 — Transport

Main protocols:

```text
TCP
UDP
```

## TCP

- Connection-oriented
- Reliable delivery mechanisms
- Sequencing
- Acknowledgments
- Retransmission
- Flow control

## UDP

- Connectionless
- Lower overhead
- No TCP-style reliability mechanisms

---

# 8. Layer 3 — Network

Main protocol:

```text
IP
```

Responsibilities:

- Logical addressing
- Routing
- Packet forwarding

Example:

```text
192.168.1.10
```

Primary device:

```text
Router
```

---

# 9. Layer 2 — Data Link

Responsibilities:

- Ethernet frames
- MAC addresses
- Switching
- VLANs
- Local delivery

Primary device:

```text
Switch
```

---

# 10. Layer 1 — Physical

Deals with physical transmission of bits.

Examples:

- Copper
- Fiber
- Radio
- Electrical signals
- Optical signals
- Connectors
- Interfaces

Remember:

```text
Copper → Electrical
Fiber → Light
```

---

# 11. TCP/IP Model

Common 4-layer representation:

```text
4. Application
3. Transport
2. Internet
1. Network Access
```

---

# 12. OSI ↔ TCP/IP Mapping

```text
OSI                         TCP/IP

Application ────────┐
Presentation ───────┼──→ Application
Session ────────────┘

Transport ─────────────→ Transport

Network ───────────────→ Internet

Data Link ─────────┐
Physical ──────────┴──→ Network Access
```

---

# 13. Encapsulation

Sender moves down the stack:

```text
Application data
      ↓
Transport header + data
      ↓
Network header + segment
      ↓
Data Link header/trailer + packet
      ↓
Bits
```

This is:

> **Encapsulation**

---

# 14. Decapsulation

Receiver moves up the stack:

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment / Datagram
 ↓
Application data
```

This is:

> **Decapsulation**

---

# 15. PDU Names

| Layer | PDU |
|---|---|
| Application | Data |
| Transport | Segment / Datagram |
| Network | Packet |
| Data Link | Frame |
| Physical | Bits |

TCP:

```text
Data
 ↓
TCP Segment
 ↓
IP Packet
 ↓
Ethernet Frame
 ↓
Bits
```

UDP:

```text
Data
 ↓
UDP Datagram
 ↓
IP Packet
 ↓
Ethernet Frame
 ↓
Bits
```

---

# 16. Packet Flow

Example:

```text
PC1 → Switch → Router → Server
```

Sender:

```text
Data
 ↓
Segment
 ↓
Packet
 ↓
Frame
 ↓
Bits
```

Receiver:

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment
 ↓
Data
```

---

# 17. Switch vs Router

## Switch

Primarily Layer 2.

Uses:

```text
Destination MAC
```

for Ethernet forwarding decisions.

## Router

Primarily Layer 3.

Uses:

```text
Destination IP
```

for forwarding decisions.

---

# 18. What Changes at a Router?

Example:

```text
PC1
 |
 | Frame A
 v
Router
 |
 | Frame B
 v
Server
```

The Layer 2 frame can change at every routed hop.

MAC addresses are link-local and can therefore change from one Ethernet link to another.

The Layer 3 IP packet is forwarded toward its destination.

---

# 19. Important Traffic Types

## ARP

Resolves an IPv4 address to a MAC address on the local network.

```text
IPv4
 ↓
ARP
 ↓
MAC
```

## ICMP

Used for control and diagnostic messages.

Example:

```text
ping
```

## DNS

Resolves names to IP addresses.

```text
Name → DNS → IP
```

## TCP

Reliable, connection-oriented transport.

## UDP

Connectionless transport with lower overhead.

---

# 20. Packet Tracer Simulation Mode

Simulation Mode allows traffic to be observed step by step.

### Workflow

```text
1. Build topology
2. Generate traffic
3. Enter Simulation Mode
4. Select events
5. Advance through events
6. Open packet details
7. Analyze layers
```

---

# 21. Packet Analysis

When examining a packet, look for:

### Layer 2

```text
Source MAC
Destination MAC
```

### Layer 3

```text
Source IP
Destination IP
```

### Layer 4

```text
TCP/UDP
Source port
Destination port
```

### Application

```text
HTTP
DNS
DHCP
SSH
```

Exact fields depend on the traffic.

---

# 22. OSI Troubleshooting Method

### Layer 1

- Cable?
- Interface up?
- Physical signal?

### Layer 2

- VLAN?
- MAC learning?
- Ethernet?

### Layer 3

- IP?
- Mask?
- Route?

### Layer 4

- TCP/UDP?
- Port?
- Transport connectivity?

### Layers 5–7

- Session?
- DNS?
- Application service?

---

# 23. Practical Troubleshooting Example

Problem:

> PC cannot access a web server.

Check:

```text
Layer 1
↓
Is the link up?

Layer 2
↓
Is the VLAN/switching correct?

Layer 3
↓
Can the PC reach the server IP?

Layer 4
↓
Is the required TCP port reachable?

Application
↓
Is the web service working?
```

---

# 24. OSI Memory Aids

Layer 7 → Layer 1:

> **All People Seem To Need Data Processing**

```text
A → Application
P → Presentation
S → Session
T → Transport
N → Network
D → Data Link
P → Physical
```

Layer 1 → Layer 7:

> **Please Do Not Throw Sausage Pizza Away**

```text
P → Physical
D → Data Link
N → Network
T → Transport
S → Session
P → Presentation
A → Application
```

---

# 25. CCNA Memory Points

```text
OSI = 7 layers

TCP/IP = commonly 4 layers

Layer 4 → TCP / UDP

Layer 3 → IP / routing

Layer 2 → Ethernet / MAC / switching

Layer 1 → Bits / physical media

Encapsulation → down

Decapsulation → up

Switch → primarily Layer 2

Router → primarily Layer 3

ARP → IPv4-to-MAC resolution on local network

ICMP → control/diagnostic messages

DNS → name resolution
```

---

# 26. Revision Questions

1. Why are networking models useful?
2. What does OSI stand for?
3. How many OSI layers exist?
4. Name the seven layers.
5. What are the common TCP/IP layers?
6. How are OSI and TCP/IP mapped?
7. What is encapsulation?
8. What is decapsulation?
9. What is the Layer 2 PDU?
10. What is the Layer 3 PDU?
11. What are the Layer 4 protocols?
12. What is the purpose of IP?
13. What address does a switch use for Layer 2 forwarding?
14. What address does a router use for Layer 3 forwarding?
15. Why can MAC addresses change across routers?
16. What does ARP do?
17. What does ICMP do?
18. What does DNS do?
19. Why is Simulation Mode useful?
20. How does OSI help troubleshoot networks?

---

# 27. Final Day 03 Takeaway

```text
Application
     ↓
Transport
     ↓
Network
     ↓
Data Link
     ↓
Physical
```

Network communication is a layered process.

Data is:

```text
Encapsulated
    ↓
Transmitted
    ↓
Decapsulated
```

Packet Tracer Simulation Mode makes the process visible and helps connect the theoretical OSI/TCP-IP models to actual network traffic.

---

# 28. Personal Reflection

## I understood

- OSI model
- TCP/IP model
- Layer responsibilities
- Encapsulation
- Decapsulation
- Packet flow
- Simulation Mode

## I need more practice with

- Mapping protocols to layers
- Identifying PDUs
- Understanding router behavior
- Identifying fields that change at each hop
- Troubleshooting by layer
