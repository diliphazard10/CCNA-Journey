# Day 02 — Network Interfaces & Cabling
## CCNA 200-301 v1.1 | Domain 1 — Network Fundamentals

---

## 1. Network Interface

A network interface is the point through which a device sends and receives network traffic.

### Physical interfaces

Actual hardware ports:

```text
FastEthernet0/1
GigabitEthernet0/0
GigabitEthernet0/1
TenGigabitEthernet0/1
```

### Logical interfaces

Software/configuration-based interfaces:

```text
Loopback0
VLAN interfaces
Router subinterfaces
```

Example:

```text
interface loopback0
```

Router-on-a-stick example:

```text
interface gigabitEthernet 0/0.10
```

---

# 2. Cisco Interface Naming

Examples:

```text
FastEthernet0/1
GigabitEthernet0/0
TenGigabitEthernet0/1
```

Common abbreviations:

| Full Name | Short Form |
|---|---|
| FastEthernet | `Fa` |
| GigabitEthernet | `Gi` |
| TenGigabitEthernet | `Te` |

Examples:

```text
Fa0/1
Gi0/0
Gi0/1
Te0/1
```

> Interface numbering varies by device model.

---

# 3. Bits and Bytes

A **bit** is a binary digit:

```text
0 or 1
```

A **byte** contains 8 bits:

```text
1 Byte = 8 bits
```

### Important symbols

```text
b = bit
B = Byte
```

Therefore:

```text
Mb = megabits
MB = megabytes

Gb = gigabits
GB = gigabytes
```

### Networking

Network speeds are normally measured in bits per second:

```text
100 Mbps
1 Gbps
10 Gbps
```

Storage is commonly measured in bytes:

```text
500 GB
1 TB
```

---

# 4. Ethernet

Ethernet is a family of wired LAN technologies.

Ethernet operates primarily at:

- OSI Layer 1 — Physical
- OSI Layer 2 — Data Link

Ethernet includes specifications for:

- Physical media
- Signaling
- Frames
- MAC addressing
- Speeds
- Duplex

Ethernet standards are primarily defined by:

```text
IEEE 802.3
```

---

# 5. Ethernet Frame

A simplified Ethernet frame:

```text
┌─────────────────┬─────────────────┬──────────────┬──────────┬─────┐
│ Destination MAC │ Source MAC      │ Type/Length  │ Data     │ FCS │
└─────────────────┴─────────────────┴──────────────┴──────────┴─────┘
```

Switches use destination MAC addresses when making Layer 2 forwarding decisions.

---

# 6. Copper Ethernet

Copper Ethernet uses **electrical signals**.

Common cable categories:

- Cat5e
- Cat6
- Cat6a

Twisted-pair Ethernet cable normally contains:

```text
4 twisted pairs
8 conductors
```

Twisting reduces:

- Electromagnetic interference
- Crosstalk

---

# 7. Cat5e

Cat5e is widely used for Gigabit Ethernet.

Commonly associated with:

```text
1000BASE-T
```

Typical structured cabling channel:

```text
approximately 100 m
```

Actual performance depends on installation and applicable standards.

---

# 8. Cat6

Cat6 provides improved electrical performance over Cat5e.

Commonly supports:

```text
1 Gbps
```

and can support higher-speed Ethernet over shorter distances depending on the standard and installation.

---

# 9. Cat6a

Cat6a is designed for higher-performance copper Ethernet.

Commonly used with:

```text
10GBASE-T
```

Designed for 10 Gbps up to approximately:

```text
100 m
```

under appropriate conditions.

---

# 10. Straight-Through and Crossover

Historically:

```text
PC → Switch
```

used straight-through cabling.

Connections such as:

```text
PC → PC
Switch → Switch
```

could require crossover cables.

Modern interfaces commonly support:

```text
Auto-MDI/MDIX
```

which automatically detects and compensates for the required pair arrangement.

Therefore, manual cable-type selection is less important on modern equipment.

---

# 11. Fiber Optic

Fiber transmits data using **light**.

```text
Electrical
   ↓
Optical transmitter
   ↓
 Light
   ↓
 Fiber
   ↓
Optical receiver
   ↓
Electrical
```

### Advantages

- Long distance
- High bandwidth
- Excellent EMI resistance
- Electrical isolation
- Useful for backbone links

Common uses:

- ISP networks
- WAN
- Campus backbone
- Building-to-building
- Data centers
- High-speed uplinks

---

# 12. Single-Mode Fiber

Single-mode fiber carries a single primary propagation mode.

Characteristics:

- Small core
- Long distance
- High bandwidth
- Common in ISP/backbone networks

Typical use:

```text
Long-distance backbone
ISP
WAN
```

---

# 13. Multimode Fiber

Multimode fiber allows multiple propagation modes.

Characteristics:

- Larger core
- Generally shorter distances
- Common in data centers
- Common in campus networks

---

# 14. Single-Mode vs Multimode

| Feature | Single-Mode | Multimode |
|---|---|---|
| Core | Smaller | Larger |
| Modes | Single primary mode | Multiple modes |
| Distance | Longer | Shorter |
| Common use | ISP/WAN/backbone | Data center/campus |

Exact distance depends on the fiber, transceiver and Ethernet standard.

---

# 15. Copper vs Fiber

| Feature | Copper | Fiber |
|---|---|---|
| Signal | Electrical | Light |
| EMI resistance | Lower | Very high |
| Distance | Generally shorter | Generally longer |
| Electrical isolation | No | Yes |
| PoE | Supported in appropriate implementations | Not normally over standard fiber |
| Installation | Generally easier | More specialized |
| Weight | Generally heavier | Generally lighter |

---

# 16. Ethernet Standards

IEEE Ethernet standards:

```text
802.3
```

Common examples:

| Standard | Speed | Medium |
|---|---:|---|
| `10BASE-T` | 10 Mbps | Twisted-pair copper |
| `100BASE-TX` | 100 Mbps | Twisted-pair copper |
| `1000BASE-T` | 1 Gbps | Twisted-pair copper |
| `10GBASE-T` | 10 Gbps | Twisted-pair copper |

### Decode the name

```text
1000BASE-T

1000 → 1000 Mbps
BASE → Baseband
T → Twisted-pair
```

---

# 17. Speed

Common Ethernet speeds:

```text
10 Mbps
100 Mbps
1 Gbps
10 Gbps
40 Gbps
100 Gbps
```

Supported speed depends on:

- Interface
- Switch/router port
- Cable
- Transceiver
- Ethernet standard
- Distance

---

# 18. Duplex

### Half-duplex

Transmit or receive, but not both simultaneously.

```text
A → B
B → A
```

### Full-duplex

Transmit and receive simultaneously.

```text
A → B
B → A
```

Modern switched Ethernet normally uses full-duplex.

---

# 19. Duplex Mismatch

A duplex mismatch occurs when connected interfaces use incompatible duplex settings.

Symptoms can include:

- Slow performance
- Errors
- Late collisions
- Retransmissions
- Poor throughput

Check with:

```text
show interfaces
```

---

# 20. Interface Status

Normal:

```text
up/up
```

Example:

```text
GigabitEthernet0/0 is up, line protocol is up
```

Conceptually:

```text
First status  → physical layer
Second status → line protocol
```

### Administratively down

Usually means the interface was disabled using:

```text
shutdown
```

Enable it with:

```text
interface gigabitEthernet 0/0
no shutdown
```

---

# 21. Cisco Verification Commands

## Quick interface overview

```text
show ip interface brief
```

Shows:

- Interface
- IP address
- Status
- Protocol

## Detailed interface information

```text
show interfaces
```

Can show:

- Status
- Speed
- Duplex
- Errors
- Traffic statistics
- MAC address
- MTU

## Switch port summary

```text
show interfaces status
```

---

# 22. Physical-Layer Troubleshooting

Use this order:

### 1. Physical connection

- Cable connected?
- Correct interface?
- Correct media?

### 2. Interface status

```text
show ip interface brief
```

### 3. Administrative state

Check for:

```text
administratively down
```

### 4. Detailed interface

```text
show interfaces
```

### 5. Speed and duplex

Check for mismatch.

### 6. Errors

Look for:

- CRC
- Input errors
- Collisions
- Drops

### 7. Layer 3

Check:

- IP address
- Mask
- Gateway

---

# 23. Important Terminology

### Bandwidth
The theoretical capacity of a link.

Example:

```text
1 Gbps
```

### Throughput
Actual successfully transferred data.

### Latency
Time required for data to travel from source to destination.

### Attenuation
Reduction of signal strength over distance.

### Interference
Unwanted signals affecting communication.

### Crosstalk
Unwanted interference between adjacent copper pairs.

---

# 24. Quick Memory Sheet

```text
1 Byte = 8 bits

b = bit
B = Byte

Ethernet = IEEE 802.3

Copper → Electrical signal
Fiber → Light

Single-mode → Longer distance
Multimode → Shorter distance

Full-duplex → Send + receive simultaneously

Cat5e → Common Gigabit Ethernet
Cat6 → Higher-performance copper
Cat6a → Common for 10GBASE-T

show ip interface brief
→ Quick interface overview

show interfaces
→ Detailed interface information

up/up
→ Physical + line protocol operational

administratively down
→ Interface disabled by configuration
```

---

# 25. Revision Questions

1. What is a network interface?
2. Physical vs logical interface?
3. Bit vs byte?
4. How many bits are in a byte?
5. What is Ethernet?
6. What IEEE family defines Ethernet?
7. Copper signal type?
8. Fiber signal type?
9. Single-mode vs multimode?
10. Which is more resistant to EMI?
11. What is Cat5e?
12. What is Cat6?
13. What is Cat6a?
14. What does 1000BASE-T mean?
15. What is full-duplex?
16. What is duplex mismatch?
17. What does `show ip interface brief` show?
18. What does `show interfaces` show?
19. What does `administratively down` mean?
20. Why use fiber for a backbone?

---

# 26. Day 02 Core Takeaway

> A network engineer must understand the physical interface, transmission medium, signal, Ethernet technology, and interface state before moving upward to IP and routing troubleshooting.
