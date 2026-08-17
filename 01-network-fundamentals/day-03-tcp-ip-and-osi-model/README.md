# Day 03 — TCP/IP Model, OSI Model & Packet Flow Analysis

> **CCNA 200-301 v1.1 · Domain 1 — Network Fundamentals**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-03-green)
![Topic](https://img.shields.io/badge/Topic-TCP%2FIP%20%26%20OSI-orange)
![Lab](https://img.shields.io/badge/Lab-Cisco%20Packet%20Tracer-red)

---

## 📌 Day 03 Overview

Today I studied the **TCP/IP model** and **OSI model**, including their purpose, basic history, layers, similarities, differences, and how network communication can be understood layer by layer.

In the lab, I used **Cisco Packet Tracer Simulation Mode** to observe different types of network traffic moving through a topology and analyzed the information associated with different layers as packets traveled through the network.

This is an important foundation for CCNA troubleshooting because a network engineer needs to identify **which layer a problem belongs to**.

---

# 🎯 Learning Objectives

By the end of Day 03, I should be able to:

- Explain why networking models are used.
- Describe the OSI reference model.
- Describe the TCP/IP model.
- Identify all 7 OSI layers.
- Identify the commonly used 4-layer TCP/IP model.
- Map TCP/IP layers to OSI layers.
- Explain the purpose of each OSI layer.
- Recognize common protocols and technologies associated with each layer.
- Explain encapsulation and decapsulation.
- Understand how data moves through a network.
- Use Packet Tracer Simulation Mode to observe traffic.
- Analyze different traffic types layer by layer.
- Use the OSI model as a troubleshooting framework.

---

# 🕰️ 1. Why Networking Models Exist

Computer networks contain many technologies from different vendors. A standardized model gives engineers a common way to describe how those technologies interact.

Networking models provide:

- A common vocabulary
- Separation of responsibilities
- Easier troubleshooting
- Better protocol design
- Vendor interoperability
- A structured way to understand communication

Instead of thinking about networking as one huge process, we divide communication into layers.

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

# 🕰️ 2. Basic Networking History

Early computer networks included many proprietary technologies and vendor-specific systems. As networking expanded, there was a need for standards and common architectures.

## OSI

**OSI = Open Systems Interconnection**

The OSI reference model was developed by the **International Organization for Standardization (ISO)** as a common reference framework for network communication.

The OSI model has **7 layers**.

## TCP/IP

The TCP/IP protocol suite developed from networking research associated with **ARPANET** and the U.S. Department of Defense research community.

TCP/IP became the foundation of modern Internet networking.

### Important distinction

The OSI model is primarily a **reference model**.

TCP/IP is both:

- A practical protocol suite
- A networking model/architecture

---

# 🧱 3. OSI Model

The OSI model has **7 layers**:

```text
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
```

| Layer | Name | Main Responsibility |
|---:|---|---|
| 7 | Application | Network services to applications |
| 6 | Presentation | Data representation and formatting |
| 5 | Session | Session establishment and management |
| 4 | Transport | End-to-end transport |
| 3 | Network | Logical addressing and routing |
| 2 | Data Link | Frames, MAC addressing, local delivery |
| 1 | Physical | Bits and physical transmission |

---

# 🟦 Layer 7 — Application

Provides network services used by applications.

Examples:

- HTTP
- HTTPS
- DNS
- DHCP
- SSH
- FTP
- SMTP

Examples:

```text
Web browser → Web server
DNS client → DNS server
SSH client → SSH server
```

> The Application layer is not simply "the application itself." It represents network services and protocols used by applications.

---

# 🟪 Layer 6 — Presentation

Traditionally concerned with how data is represented.

Concepts associated with this layer include:

- Data formatting
- Encoding
- Encryption/decryption
- Compression/decompression

In modern TCP/IP networks, these functions are often implemented across applications and libraries rather than as a separate protocol layer.

---

# 🟩 Layer 5 — Session

Traditionally concerned with:

- Establishing sessions
- Managing sessions
- Terminating sessions

Modern TCP/IP systems often do not implement a separate Session layer.

---

# 🟨 Layer 4 — Transport

Provides end-to-end transport services.

Important protocols:

- **TCP**
- **UDP**

## TCP

TCP is connection-oriented and provides mechanisms such as:

- Connection establishment
- Sequencing
- Acknowledgments
- Retransmission
- Flow control

## UDP

UDP is connectionless and provides a simpler transport service with less overhead than TCP.

Common use cases include DNS, DHCP, and applications where low overhead is important.

---

# 🟧 Layer 3 — Network

Responsible for logical addressing and routing.

The most important protocol is:

```text
IP
```

Example IPv4 address:

```text
192.168.1.10
```

Routers operate primarily at Layer 3 and make forwarding decisions based on Layer 3 information.

Common concepts:

- IP addressing
- Routing
- Packets
- Routers

---

# 🟥 Layer 2 — Data Link

Handles communication over a local link.

Important concepts:

- Ethernet frames
- MAC addresses
- Switching
- VLANs
- Local delivery

A switch primarily operates at Layer 2.

```text
PC ─── Ethernet ─── Switch
```

---

# ⬛ Layer 1 — Physical

Responsible for transmitting raw bits over a physical medium.

Examples:

- Copper cable
- Fiber optic cable
- Radio
- Electrical signals
- Optical signals
- Connectors
- Physical interfaces

From Day 2:

```text
Copper → electrical signals
Fiber → light
```

---

# 🧩 4. TCP/IP Model

The TCP/IP model is commonly represented using **4 layers**:

```text
4. Application
3. Transport
2. Internet
1. Network Access
```

---

# 📊 5. TCP/IP vs OSI

| TCP/IP | OSI |
|---|---|
| Application | Application |
| | Presentation |
| | Session |
| Transport | Transport |
| Internet | Network |
| Network Access | Data Link |
| | Physical |

The TCP/IP Application layer broadly covers functionality represented by the OSI Application, Presentation and Session layers.

The TCP/IP Network Access layer broadly covers the OSI Data Link and Physical layers.

---

# 🔄 6. Layer Mapping

```text
OSI                          TCP/IP

7. Application ───────┐
6. Presentation ──────┼──→ Application
5. Session ───────────┘

4. Transport ─────────────→ Transport

3. Network ───────────────→ Internet

2. Data Link ──────────┐
1. Physical ──────────┴──→ Network Access
```

---

# 📦 7. Encapsulation

When a device sends data, information moves **down through the networking stack**.

Conceptually:

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

Each layer adds information needed for communication.

This process is called **encapsulation**.

---

# 🔓 8. Decapsulation

When the receiving device receives the data, information moves **up through the stack**.

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

The receiving device processes and removes the relevant headers/trailers.

This is called **decapsulation**.

---

# 📦 9. Protocol Data Units (PDUs)

Common PDU names:

| Layer | PDU |
|---|---|
| Application | Data |
| Transport | Segment / Datagram |
| Network | Packet |
| Data Link | Frame |
| Physical | Bits |

TCP example:

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

UDP example:

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

> Terminology can vary between textbooks and vendors, but these are the common CCNA terms.

---

# 🧭 10. What Happens When a PC Sends Data?

Example:

```text
PC1 → Switch → Router → Server
```

At the sender:

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

At the receiver:

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

# 🔬 11. Packet Tracer Simulation Mode

Cisco Packet Tracer provides **Simulation Mode**, which allows network traffic to be observed step by step.

It is useful for understanding:

- Protocol operation
- Packet movement
- Encapsulation
- Layer interactions
- Device behavior
- Different traffic types

### Lab workflow

```text
1. Build topology
2. Generate traffic
3. Enter Simulation Mode
4. Select relevant events
5. Advance through events
6. Inspect packet details
7. Identify information at different layers
```

---

# 🧪 12. Day 03 Lab

The lab focused on observing network traffic in Simulation Mode.

### Objectives

- Generate traffic between devices.
- Observe packets moving through the topology.
- Identify different traffic types.
- Follow traffic between devices.
- Inspect packet information.
- Relate observed information to OSI/TCP-IP layers.
- Understand what changes as traffic crosses network devices.

---

# 🌐 13. Traffic Types Observed

Different network activities can generate different protocols.

## ARP

ARP resolves an IPv4 address to a MAC address on the local network.

```text
IPv4 address
     ↓
    ARP
     ↓
MAC address
```

## ICMP

ICMP is used for network control and diagnostic messages.

A common example is:

```text
ping
```

## DNS

DNS resolves names to IP addresses.

```text
www.example.com
        ↓
      DNS
        ↓
    IP address
```

## TCP

TCP provides reliable, connection-oriented transport.

## UDP

UDP provides connectionless transport with lower overhead than TCP.

---

# 🔍 14. Analyzing a Packet in Simulation Mode

When inspecting an event, look for information associated with different layers.

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
TCP or UDP
Source port
Destination port
```

### Application

Protocol-specific information such as:

```text
HTTP
DNS
DHCP
SSH
```

The exact fields depend on the traffic being examined.

---

# 🧠 15. Layer-by-Layer Example

Imagine:

```text
PC1 → Switch → Router → Server
```

A packet may contain:

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
etc.
```

---

# 🔀 16. What Happens at a Switch?

A switch primarily makes Layer 2 forwarding decisions using MAC addresses.

Conceptually:

```text
PC1
 |
 | Ethernet frame
 v
SW1
 |
 | → Correct switch port
 v
PC2
```

The switch checks its MAC address table and determines where to forward the frame.

---

# 🚦 17. What Happens at a Router?

A router primarily makes forwarding decisions using Layer 3 information.

It examines the destination IP address and determines the next hop/outgoing interface.

A router removes the incoming Layer 2 frame and creates a new Layer 2 frame for the outgoing link.

---

# 🔁 18. Important Observation from the Lab

One of the most important lessons is:

> **Layer 2 information can change from one link to another, while the Layer 3 packet is forwarded toward the final destination.**

Example:

```text
PC1
 |
 | Ethernet Frame A
 v
Router
 |
 | Ethernet Frame B
 v
Server
```

Frame A and Frame B can have different MAC addresses because they belong to different local links.

---

# 🛠️ 19. Using OSI for Troubleshooting

## Layer 1 — Physical

Check:

- Cable
- Interface status
- Signal
- Physical connectivity

## Layer 2 — Data Link

Check:

- VLAN
- MAC learning
- Ethernet link
- Switching

## Layer 3 — Network

Check:

- IP address
- Subnet mask
- Routing
- Reachability

## Layer 4 — Transport

Check:

- TCP/UDP
- Ports
- Transport connectivity

## Layers 5–7

Check:

- Sessions
- DNS
- Application protocols
- Application services

---

# 🧠 20. Why the OSI Model Matters for CCNA

Do not learn OSI only as a memorization exercise.

Use it to identify where a problem may exist.

Example:

```text
No link light
      ↓
Think Layer 1

Correct link but wrong VLAN
      ↓
Think Layer 2

Can reach local network but not remote network
      ↓
Think Layer 3

IP connectivity works but application connection fails
      ↓
Investigate Layer 4 and above
```

---

# 🧠 21. OSI Memory Aids

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

# 📊 22. OSI vs TCP/IP Quick Comparison

| Feature | OSI | TCP/IP |
|---|---|---|
| Layers | 7 | Commonly 4 |
| Type | Reference model | Protocol suite + model |
| Application separation | 3 upper layers | Combined |
| Network layer | Network | Internet |
| Physical/Data Link | Separate | Commonly combined as Network Access |

---

# 📌 23. Key Takeaways

1. Networking models divide complex communication into layers.
2. The OSI model has 7 layers.
3. TCP/IP is commonly represented with 4 layers.
4. TCP/IP is the foundation of modern Internet networking.
5. OSI is primarily a reference model.
6. Encapsulation occurs as data moves down the stack.
7. Decapsulation occurs as data moves up the stack.
8. TCP is connection-oriented and provides reliability mechanisms.
9. UDP is connectionless.
10. IP provides logical addressing and routing.
11. Ethernet provides local Layer 2 communication.
12. Switches primarily forward using MAC addresses.
13. Routers primarily forward using IP addresses.
14. Simulation Mode makes protocol behavior visible.
15. Different traffic types can be analyzed layer by layer.
16. The OSI model is a practical troubleshooting framework.

---


# 📝 25. Revision Questions

1. Why are networking models useful?
2. What does OSI stand for?
3. How many OSI layers are there?
4. Name all seven OSI layers.
5. How many layers are commonly used in the TCP/IP model?
6. What is the main difference between OSI and TCP/IP?
7. What happens during encapsulation?
8. What happens during decapsulation?
9. What is the Layer 2 PDU?
10. What is the Layer 3 PDU?
11. What are the common Layer 4 protocols?
12. What is the purpose of IP?
13. What address does a switch primarily use for Layer 2 forwarding?
14. What address does a router primarily use for Layer 3 forwarding?
15. Why can MAC addresses change as traffic crosses routers?
16. What is ARP used for?
17. What is ICMP used for?
18. Why is Packet Tracer Simulation Mode useful?
19. How can the OSI model help troubleshoot a network?

---

# 📈 26. Day 03 Reflection

## What I Learned

- Networking models
- Basic networking history
- OSI model
- TCP/IP model
- Layer responsibilities
- Encapsulation
- Decapsulation
- Protocol Data Units
- ARP
- ICMP
- TCP
- UDP
- DNS
- Packet Tracer Simulation Mode
- Traffic analysis
- Layer-by-layer analysis
- OSI troubleshooting

## What I Need to Improve

- Memorizing all OSI layers and responsibilities
- Mapping TCP/IP layers to OSI
- Identifying PDUs quickly
- Recognizing protocols by layer
- Understanding exactly what changes when traffic crosses a router

## Main Takeaway

> **The OSI and TCP/IP models are not just memorization topics. They give me a structured way to understand what is happening to network traffic and where to look when something goes wrong.**

---

# 🚀 Day 03 Status

**Completed ✅**

- [x] Networking models
- [x] Basic networking history
- [x] OSI model
- [x] TCP/IP model
- [x] OSI/TCP-IP mapping
- [x] Layer responsibilities
- [x] Encapsulation
- [x] Decapsulation
- [x] PDUs
- [x] TCP
- [x] UDP
- [x] DNS
- [x] Packet Tracer Simulation Mode
- [x] Traffic analysis
- [x] Layer-by-layer analysis

---

**Next:** Day 04 — IPv4 Addressing & Subnetting
