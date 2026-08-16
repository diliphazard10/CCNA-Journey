
# Day 02 — Network Interfaces, Ethernet & Cabling

> **CCNA 200-301 v1.1 · Domain 1 — Network Fundamentals**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-02-green)
![Topic](https://img.shields.io/badge/Topic-Interfaces%20%26%20Cabling-orange)
![Lab](https://img.shields.io/badge/Lab-Cisco%20Packet%20Tracer-red)

---

## 📌 Day 02 Overview

Today I studied the physical side of networking: **network interfaces, Ethernet, bits and bytes, copper Ethernet cabling, fiber optics, Ethernet standards, speed, duplex, and basic Cisco interface verification**.

A network engineer needs to understand not only IP addresses and routing, but also what happens underneath them at the physical and data-link layers.

### Study Focus

- Network interfaces
- Physical vs logical interfaces
- Cisco interface naming
- Bits and bytes
- Ethernet fundamentals
- Copper Ethernet
- Twisted-pair cabling
- Cat5e, Cat6 and Cat6a
- Fiber optic cabling
- Single-mode vs multimode fiber
- Ethernet standards
- Speed and duplex
- Interface status
- Basic physical-layer troubleshooting
- Cisco interface verification commands

---

# 🎯 Learning Objectives

By the end of Day 02, I should be able to:

- Explain what a network interface is.
- Distinguish between physical and logical interfaces.
- Recognize common Cisco Ethernet interface names.
- Explain the difference between bits and bytes.
- Explain the basic purpose of Ethernet.
- Describe how copper Ethernet transmits data.
- Describe how fiber optic Ethernet transmits data.
- Compare single-mode and multimode fiber.
- Explain common copper cable categories.
- Recognize common Ethernet standards such as `10BASE-T`, `100BASE-TX`, `1000BASE-T`, and `10GBASE-T`.
- Explain speed and duplex.
- Recognize an `up/up` interface.
- Identify an administratively disabled interface.
- Use basic Cisco interface verification commands.
- Begin troubleshooting physical and interface-related problems.

---

# 🧠 1. Network Interfaces

A **network interface** is the connection point through which a device sends and receives network traffic.

A device may have multiple interfaces.

Example:

```text
             R1
        ┌───────────┐
        │           │
     G0/0         G0/1
        │           │
      LAN 1       LAN 2
```

Interfaces can be either:

- **Physical**
- **Logical**

---

## 🔌 Physical Interface

A physical interface represents actual network hardware.

Examples:

```text
FastEthernet0/1
GigabitEthernet0/0
GigabitEthernet0/1
TenGigabitEthernet0/1
```

A physical Ethernet interface can connect to another device using an Ethernet cable.

```text
PC ───── Ethernet Cable ───── Switch
```

---

## 🧩 Logical Interface

A logical interface is created through software/configuration rather than representing a separate physical port.

Examples:

```text
Loopback0
VLAN interfaces
Router subinterfaces
```

Example:

```text
interface loopback0
```

Router-on-a-stick can use subinterfaces such as:

```text
interface gigabitEthernet 0/0.10
```

---

# 🔤 2. Cisco Interface Naming

Cisco IOS uses structured interface names.

Example:

```text
GigabitEthernet0/0
```

Short form:

```text
Gi0/0
```

Common abbreviations:

| Full Interface Type | Abbreviation | Typical Meaning |
|---|---|---|
| FastEthernet | `Fa` | 100 Mbps-class Ethernet |
| GigabitEthernet | `Gi` | 1 Gbps-class Ethernet |
| TenGigabitEthernet | `Te` | 10 Gbps-class Ethernet |

Examples:

```text
Fa0/1
Gi0/0
Gi0/1
Te0/1
```

> **Note:** Interface numbering depends on the specific Cisco device model.

---

# 🔢 3. Bits and Bytes

A **bit** is the smallest unit of digital information.

A bit can have one of two values:

```text
0
1
```

A **byte** contains 8 bits.

```text
1 Byte = 8 bits
```

### Important distinction

| Symbol | Meaning |
|---|---|
| `b` | bit |
| `B` | Byte |

Therefore:

```text
Mb = megabits
MB = megabytes

Gb = gigabits
GB = gigabytes
```

Network speeds are normally expressed in **bits per second**:

```text
100 Mbps
1 Gbps
10 Gbps
```

Storage is commonly expressed in **bytes**:

```text
500 GB
1 TB
```

---

# 🌐 4. Ethernet

**Ethernet** is a family of technologies widely used for wired local area networks.

Ethernet operates primarily at:

- **OSI Layer 1 — Physical**
- **OSI Layer 2 — Data Link**

Ethernet defines characteristics such as:

- Physical media
- Signaling
- Ethernet frames
- MAC addressing
- Transmission speeds
- Duplex operation

Ethernet standards are developed under the **IEEE 802.3** family.

Common Ethernet connections include:

```text
PC → Switch
Server → Switch
Access Point → Switch
Switch → Router
```

---

# 🧱 5. Ethernet Frame

At Layer 2, Ethernet carries information using **frames**.

A simplified Ethernet frame contains:

```text
┌─────────────────┬─────────────────┬──────────────┬──────────┬─────┐
│ Destination MAC │ Source MAC      │ Type/Length  │ Data     │ FCS │
└─────────────────┴─────────────────┴──────────────┴──────────┴─────┘
```

A switch uses the destination MAC address when making Layer 2 forwarding decisions.

---

# 🧵 6. Copper Ethernet

Copper Ethernet uses **electrical signals** to transmit data.

Common twisted-pair Ethernet categories include:

- Cat5e
- Cat6
- Cat6a

Copper Ethernet cables contain twisted pairs of copper conductors.

The twisting helps reduce:

- Electromagnetic interference
- Crosstalk

A typical twisted-pair Ethernet cable contains:

```text
4 twisted pairs
8 conductors
```

---

# 📦 7. Common Copper Cable Categories

## Cat5e

Cat5e is widely used for Gigabit Ethernet.

Commonly associated with:

```text
1000BASE-T
```

Typical structured cabling channel distance:

```text
Up to approximately 100 meters
```

Actual performance depends on the installation and applicable standards.

---

## Cat6

Cat6 provides improved electrical performance compared with Cat5e.

It supports:

```text
1 Gbps
```

and can support higher-speed Ethernet over shorter distances depending on the standard and installation.

Cat6 is common in modern structured cabling.

---

## Cat6a

Cat6a is designed for higher-performance copper Ethernet.

It is commonly used for:

```text
10GBASE-T
```

and is designed to support 10 Gbps up to approximately:

```text
100 meters
```

under appropriate installation conditions.

---

# 🔄 8. Straight-Through vs Crossover

Historically, different Ethernet cable wiring arrangements were commonly used for different device combinations.

For example:

```text
PC → Switch
```

traditionally used straight-through cabling.

A direct connection such as:

```text
PC → PC
Switch → Switch
```

could traditionally require crossover cabling.

However, modern Ethernet devices commonly support **Auto-MDI/MDIX**, which can automatically detect and compensate for the required pair configuration.

Therefore, the old straight-through/crossover distinction is less operationally important on modern equipment.

---

# 💡 9. Fiber Optic Cabling

Fiber optic cable transmits data using **light** instead of electrical signals.

Simplified process:

```text
Electrical signal
       ↓
Optical transmitter
       ↓
      Light
       ↓
 Fiber optic cable
       ↓
 Optical receiver
       ↓
Electrical signal
```

### Advantages

- Long transmission distances
- High bandwidth
- Excellent resistance to electromagnetic interference
- Electrical isolation
- Useful for backbone connections

Common uses:

- ISP networks
- WAN links
- Campus backbones
- Building-to-building connections
- Data centers
- High-speed uplinks

---

# 🔦 10. Single-Mode Fiber

Single-mode fiber is designed to carry a single primary propagation mode of light.

### Characteristics

- Smaller core
- Long-distance capability
- High bandwidth
- Common in ISP and backbone networks
- Suitable for long-distance links

Typical applications:

```text
ISP
 │
 ├──── Long fiber link ────┤
 │
Core / backbone network
```

---

# 🔆 11. Multimode Fiber

Multimode fiber allows multiple propagation modes of light.

### Characteristics

- Larger core than single-mode
- Generally used for shorter distances
- Common in data centers
- Common in campus environments
- Often practical for short high-speed links

---

# 🆚 12. Single-Mode vs Multimode

| Feature | Single-Mode | Multimode |
|---|---|---|
| Core | Smaller | Larger |
| Propagation | Single primary mode | Multiple modes |
| Typical distance | Longer | Shorter |
| Common use | ISP / WAN / backbone | Data center / campus |
| Equipment | Optimized for long-distance links | Optimized for shorter links |

> Exact supported distance depends on the transceiver, Ethernet standard, fiber specification, and optical budget.

---

# ⚖️ 13. Copper vs Fiber

| Feature | Copper | Fiber |
|---|---|---|
| Signal | Electrical | Light |
| EMI resistance | Lower | Very high |
| Typical distance | Shorter | Longer |
| Electrical isolation | No | Yes |
| PoE | Supported in appropriate implementations | Not normally carried over standard fiber |
| Installation | Generally easier | Requires specialized handling |
| Weight | Generally heavier | Generally lighter |
| Cost | Often lower | Can be higher |

---

# 📜 14. Ethernet Standards

Ethernet standards are primarily defined under:

```text
IEEE 802.3
```

Examples:

| Standard | Speed | Medium |
|---|---:|---|
| `10BASE-T` | 10 Mbps | Twisted-pair copper |
| `100BASE-TX` | 100 Mbps | Twisted-pair copper |
| `1000BASE-T` | 1 Gbps | Twisted-pair copper |
| `10GBASE-T` | 10 Gbps | Twisted-pair copper |

---

## Understanding `1000BASE-T`

A simplified interpretation:

```text
1000 → 1000 Mbps
BASE → Baseband
T → Twisted-pair copper
```

Therefore:

```text
1000BASE-T = 1 Gbps Ethernet over twisted-pair copper
```

Similarly:

```text
10GBASE-T
```

means 10 Gigabit Ethernet over twisted-pair copper.

---

# ⚡ 15. Speed

Common Ethernet speeds include:

```text
10 Mbps
100 Mbps
1 Gbps
10 Gbps
40 Gbps
100 Gbps
```

The actual supported speed depends on:

- Network interface
- Switch/router port
- Cable
- Transceiver
- Ethernet standard
- Distance

The link cannot operate beyond the capabilities of its components.

---

# 🔄 16. Duplex

Duplex describes how an interface transmits and receives data.

## Half-Duplex

Data can travel in both directions, but not simultaneously.

```text
A → B
B → A
```

Only one direction at a time.

---

## Full-Duplex

Both devices can transmit and receive simultaneously.

```text
A → B
B → A
```

at the same time.

Modern switched Ethernet networks normally use:

```text
Full-duplex
```

---

# ⚠️ 17. Duplex Mismatch

A duplex mismatch occurs when connected interfaces use incompatible duplex settings.

Possible symptoms:

- Slow performance
- Packet errors
- Late collisions
- Retransmissions
- Poor throughput

Useful command:

```text
show interfaces
```

Look for:

```text
duplex
speed
errors
```

---

# 🖥️ 18. Cisco Interface Status

Cisco IOS commonly reports two important interface states.

Example:

```text
GigabitEthernet0/0 is up, line protocol is up
```

Conceptually:

```text
up/up
```

The first status represents the physical layer.

The second represents the line protocol.

The desired normal operational state is:

```text
up/up
```

---

# 🚫 19. Administratively Down

If an interface has been manually disabled:

```text
shutdown
```

it can appear as:

```text
administratively down
```

To enable it:

```text
interface gigabitEthernet 0/0
no shutdown
```

---

# 🔎 20. Cisco Interface Verification Commands

## `show ip interface brief`

```text
show ip interface brief
```

Provides a quick summary of:

- Interface
- IP address
- Status
- Protocol

---

## `show interfaces`

```text
show interfaces
```

Provides detailed information such as:

- Interface status
- Hardware information
- Speed
- Duplex
- Errors
- Traffic statistics
- MAC address
- MTU

---

## `show interfaces status`

On supported switches:

```text
show interfaces status
```

Provides a concise summary of switch ports.

---

# 🧪 21. Day 02 Lab

The lab focused on identifying interfaces, Ethernet connections, cable types, and basic interface status.

### Basic topology

```text
           R1
           |
           |
          SW1
         /   \
       PC1   PC2
```

### Main goals

- Identify Ethernet interfaces
- Understand copper Ethernet connections
- Examine interface names
- Check interface status
- Practice basic Cisco verification commands

---

# 🔧 22. Basic Troubleshooting Workflow

When an Ethernet interface is not working:

### 1. Check physical connectivity

- Is the cable connected?
- Is the correct cable/media being used?
- Is the correct interface connected?

### 2. Check interface status

```text
show ip interface brief
```

### 3. Check for administrative shutdown

Look for:

```text
administratively down
```

### 4. Check detailed interface information

```text
show interfaces
```

### 5. Check speed and duplex

Look for mismatches.

### 6. Check interface errors

Look for:

- Input errors
- CRC errors
- Collisions
- Drops

### 7. Check Layer 3 configuration

Verify:

- IP address
- Subnet mask
- Default gateway

---

# 📊 23. Important Terminology

### Bandwidth

The theoretical capacity of a link.

Example:

```text
1 Gbps
```

---

### Throughput

The actual amount of data successfully transferred.

Throughput can be lower than the theoretical bandwidth.

---

### Latency

The time required for data to travel from one point to another.

---

### Attenuation

The reduction in signal strength as a signal travels through a medium.

---

### Interference

Unwanted signals that can affect communication.

Copper is more susceptible to electromagnetic interference than fiber.

---

### Crosstalk

Unwanted interference between signals traveling through adjacent copper pairs.

Twisting helps reduce crosstalk.

---

# 🏢 24. Example Network Design

A small office might look like:

```text
                 Internet
                    |
             Router / Firewall
                    |
               Core Switch
              /           \
       Access Switch      Server
          /      \
        PCs       AP
                   |
             Wireless Clients
```

Possible media:

```text
PC → Access Switch
      |
    Copper

Access Switch → Core Switch
      |
 Copper or Fiber
 depending on speed/distance

Building A → Building B
      |
    Fiber
```

The correct medium depends on:

- Distance
- Required speed
- Environment
- Equipment
- Budget
- Future requirements

---

# 🧠 25. Key Takeaways

1. A network interface is a connection point for network communication.
2. Interfaces can be physical or logical.
3. Ethernet is widely used for wired LANs.
4. Ethernet uses frames at Layer 2.
5. Copper uses electrical signaling.
6. Fiber uses optical signaling.
7. Single-mode fiber is generally used for longer distances.
8. Multimode fiber is generally used for shorter distances.
9. `1 Byte = 8 bits`.
10. Network speeds are normally measured in bits per second.
11. Ethernet standards belong primarily to IEEE 802.3.
12. Cat5e, Cat6 and Cat6a are copper cabling categories.
13. Full-duplex allows simultaneous transmission and reception.
14. Duplex mismatches can cause performance problems.
15. `show ip interface brief` is an important Cisco verification command.
16. `show interfaces` provides detailed interface information.
17. Physical-layer problems should be checked before assuming an IP/routing problem.

---

# 📝 26. CCNA Revision Questions

1. What is a network interface?

2. What is the difference between a physical and logical interface?

3. What is the difference between a bit and a byte?

4. How many bits are in one byte?

5. What is Ethernet?

6. Which IEEE standard family defines Ethernet?

7. What type of signal does copper Ethernet use?

8. What type of signal does fiber use?

9. What is the difference between single-mode and multimode fiber?

10. Which medium is more resistant to electromagnetic interference?

11. What is Cat5e?

12. What is Cat6?

13. What is Cat6a?

14. What does `1000BASE-T` represent?

15. What is full-duplex?

16. What is duplex mismatch?

17. What does `show ip interface brief` display?

18. What does `show interfaces` display?

19. What does `administratively down` mean?

20. Why might fiber be selected instead of copper for a backbone connection?

---

# 📌 27. Quick Revision Card

```text
1 Byte = 8 bits

Ethernet = IEEE 802.3

Copper → Electrical signal
Fiber → Light

Single-mode → Longer distance
Multimode → Shorter distance

Full-duplex → Send + receive simultaneously

Cat5e → Common Gigabit Ethernet
Cat6 → Higher-performance copper
Cat6a → Common choice for 10GBASE-T

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

# 📈 28. Day 02 Reflection

## What I Learned

- Network interfaces
- Ethernet
- Bits and bytes
- Copper Ethernet
- Fiber optic cables
- Single-mode and multimode fiber
- Ethernet standards
- Speed and duplex
- Cisco interface verification

## What I Need to Improve

- Exact Ethernet standards and media combinations
- Fiber standards and supported distances
- Physical-layer troubleshooting
- Interface errors
- Speed and duplex troubleshooting

## Main Takeaway

> Networking does not begin with IP addresses alone. A network engineer must understand the physical interface, transmission medium, signal, Ethernet technology, and interface status before troubleshooting higher-layer problems.

---

# 🚀 Day 02 Status

**Completed ✅**

### Topics Covered

- [x] Network interfaces
- [x] Physical interfaces
- [x] Logical interfaces
- [x] Cisco interface naming
- [x] Bits and bytes
- [x] Ethernet
- [x] Copper Ethernet
- [x] Cat5e
- [x] Cat6
- [x] Cat6a
- [x] Fiber optics
- [x] Single-mode fiber
- [x] Multimode fiber
- [x] Ethernet standards
- [x] Speed
- [x] Duplex
- [x] Interface status
- [x] Cisco interface verification

---

**Next:** Day 03 — Network Topologies & Network Architecture
