# Day 07 — IPv4 Addressing

> **CCNA 200-301 · Network Fundamentals · IPv4 Addressing**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-07-green)
![Topic](https://img.shields.io/badge/Topic-IPv4%20Addressing-orange)
![Section](https://img.shields.io/badge/Section-Network%20Fundamentals-purple)

---

## 📌 Day 07 Overview

Today I learned about **IPv4 addressing**, one of the fundamental topics in computer networking and an important part of the **CCNA 200-301** exam.

IPv4 provides logical Layer 3 addressing so devices can identify source and destination networks and hosts.

### Topics Covered

- IPv4 address and 32-bit structure
- Four octets and binary/decimal representation
- Network and host portions
- Subnet masks
- CIDR notation
- Network, host, and broadcast addresses
- Default gateway
- Private and public IPv4
- Special IPv4 addresses
- Unicast, broadcast, and multicast
- Basic IPv4 configuration
- Packet Tracer practice

---

# 🎯 Learning Objectives

By the end of Day 07, I should be able to:

- Explain what IPv4 is and why it is used.
- Explain that IPv4 addresses are 32 bits.
- Explain the four-octet format.
- Understand decimal and binary representation.
- Explain network and host portions.
- Explain the purpose of a subnet mask.
- Read CIDR notation such as `/24`.
- Identify a network address, usable host range, and broadcast address.
- Explain the purpose of a default gateway.
- Distinguish private and public IPv4 addresses.
- Recognize common special IPv4 ranges.
- Understand unicast, broadcast, and multicast.
- Configure and verify IPv4 addresses in Packet Tracer.

---

# 🌐 1. What Is IPv4?

IPv4 stands for **Internet Protocol version 4**.

IPv4 is a Layer 3 protocol that provides logical addressing and supports routing between networks.

Example:

```text
192.168.1.10
```

An IPv4 address contains:

```text
32 bits
```

---

# 🧩 2. IPv4 Address Structure

An IPv4 address is divided into:

```text
4 octets
```

Each octet contains:

```text
8 bits
```

Therefore:

```text
8 + 8 + 8 + 8 = 32 bits
```

Example:

```text
192.168.1.10
```

The four octets are:

```text
192
168
1
10
```

Each octet ranges from:

```text
0 – 255
```

because 8 bits provide 256 possible values.

---

# 💻 3. Binary Representation

The binary place values of one octet are:

```text
128 64 32 16 8 4 2 1
```

Example:

```text
192 = 11000000
10  = 00001010
```

Therefore:

```text
192.168.1.10
```

can be represented as:

```text
11000000.10101000.00000001.00001010
```

Binary becomes especially important when learning subnetting.

---

# 🧠 4. Network Portion and Host Portion

An IPv4 address is divided into:

```text
Network portion
+
Host portion
```

The subnet mask or prefix length determines the boundary.

Example:

```text
192.168.1.10/24
```

The `/24` means:

```text
24 network bits
8 host bits
```

because:

```text
32 - 24 = 8
```

---

# 📏 5. Subnet Mask

Example:

```text
IP Address:
192.168.1.10

Subnet Mask:
255.255.255.0
```

Binary:

```text
11111111.11111111.11111111.00000000
```

Remember:

```text
1s → network portion
0s → host portion
```

---

# 🔢 6. CIDR Notation

CIDR stands for:

> **Classless Inter-Domain Routing**

Instead of writing:

```text
192.168.1.10
255.255.255.0
```

we can write:

```text
192.168.1.10/24
```

`/24` means:

```text
24 network bits
8 host bits
```

---

# 🏠 7. Network Address

The network address identifies the network itself.

For:

```text
192.168.1.10/24
```

the network address is:

```text
192.168.1.0
```

The network address is not normally assigned to an individual host.

---

# 💻 8. Usable Host Addresses

For:

```text
192.168.1.0/24
```

the typical usable host range is:

```text
192.168.1.1
through
192.168.1.254
```

---

# 📢 9. Broadcast Address

The broadcast address is used to send traffic to all hosts within the local IPv4 subnet.

For:

```text
192.168.1.0/24
```

the broadcast address is:

```text
192.168.1.255
```

Therefore:

```text
Network:
192.168.1.0

Usable hosts:
192.168.1.1 – 192.168.1.254

Broadcast:
192.168.1.255
```

---

# 🧮 10. /24 Example

| Item | Value |
|---|---|
| IP address | 192.168.1.10 |
| Prefix | /24 |
| Subnet mask | 255.255.255.0 |
| Network address | 192.168.1.0 |
| First usable | 192.168.1.1 |
| Last usable | 192.168.1.254 |
| Broadcast | 192.168.1.255 |
| Host bits | 8 |
| Total addresses | 256 |
| Typical usable hosts | 254 |

The total number of addresses is:

```text
2^8 = 256
```

Traditionally, two are reserved for the network and broadcast addresses:

```text
256 - 2 = 254 usable host addresses
```

---

# 🚪 11. Default Gateway

A default gateway is normally the router interface that a host uses to reach destinations outside its local subnet.

Example:

```text
PC
IP:      192.168.1.10/24
Gateway: 192.168.1.1
```

Same subnet:

```text
PC1 → PC2
```

Remote subnet:

```text
PC1 → Default Gateway → Router → Remote Network
```

A host does not normally send same-subnet traffic to the default gateway.

---

# 🔒 12. Private IPv4 Addresses

Private IPv4 ranges are commonly used inside local networks.

### 10.0.0.0/8

```text
10.0.0.0 – 10.255.255.255
```

### 172.16.0.0/12

```text
172.16.0.0 – 172.31.255.255
```

### 192.168.0.0/16

```text
192.168.0.0 – 192.168.255.255
```

These ranges are not globally routable on the public Internet.

---

# 🌍 13. Public IPv4 Addresses

Public IPv4 addresses are globally routable addresses used for Internet communication, subject to routing and policy.

A common network design is:

```text
Private LAN
    ↓
Router / NAT
    ↓
Public Internet
```

---

# ⭐ 14. Common Special IPv4 Addresses

### 0.0.0.0

Can represent an:

```text
unspecified address
```

It is also used in:

```text
0.0.0.0/0
```

to represent the default route.

### 127.0.0.0/8

Loopback range.

Common example:

```text
127.0.0.1
```

Used by a host to refer to itself.

### 169.254.0.0/16

IPv4 link-local range used for automatic addressing in certain situations when normal configuration is unavailable.

---

# 🏷️ 15. IPv4 Traffic Types

### Unicast

One sender to one destination:

```text
1 → 1
```

### Broadcast

One sender to all hosts in the local broadcast domain:

```text
1 → all
```

### Multicast

One sender to a subscribed group:

```text
1 → group
```

---

# 🔌 16. IPv4 Configuration

Basic IPv4 configuration includes:

```text
IP address
Subnet mask / prefix length
Default gateway
```

Example:

```text
IP address:
192.168.1.10

Subnet mask:
255.255.255.0

Default gateway:
192.168.1.1
```

---

# 🧪 17. Packet Tracer Lab

Create:

```text
PC1 ─── Switch ─── PC2
```

Configure:

```text
PC1
IP: 192.168.1.10
Mask: 255.255.255.0
Gateway: 192.168.1.1
```

```text
PC2
IP: 192.168.1.20
Mask: 255.255.255.0
Gateway: 192.168.1.1
```

Test:

```text
PC1 → ping 192.168.1.20
```

Expected result:

```text
Successful replies
```

---

# 🔎 18. Verify IPv4 Configuration

On a Packet Tracer PC:

```text
ipconfig
```

This can show:

```text
IP address
Subnet mask
Default gateway
```

Test connectivity:

```text
ping 192.168.1.20
```

---

# 🧪 19. Suggested Lab Experiments

## Experiment A — Same Subnet

Configure:

```text
PC1 = 192.168.1.10/24
PC2 = 192.168.1.20/24
```

Test:

```text
ping 192.168.1.20
```

Observe the communication.

## Experiment B — Different Subnets

Configure hosts on different networks and connect them through appropriate Layer 3 routing equipment.

Example:

```text
PC1 = 192.168.1.10/24
PC2 = 192.168.2.20/24
```

Observe what changes when the hosts are on different networks.

## Experiment C — Wrong Subnet Mask

Give a host an incorrect subnet mask and test connectivity.

Observe how the host decides whether the destination is local or remote.

---

# 🧠 20. CCNA Memory Sheet

```text
IPv4
→ Layer 3 logical addressing

IPv4 size
→ 32 bits

Octets
→ 4

Bits per octet
→ 8

Octet range
→ 0–255

Subnet mask
→ Identifies network vs host bits

CIDR /24
→ 24 network bits + 8 host bits

192.168.1.10/24
→ Network: 192.168.1.0
→ Broadcast: 192.168.1.255
→ Usable hosts: .1 – .254

Private ranges
→ 10.0.0.0/8
→ 172.16.0.0/12
→ 192.168.0.0/16

Loopback
→ 127.0.0.0/8

Link-local
→ 169.254.0.0/16

Default gateway
→ Used to reach remote networks
```

---

# ⚠️ 21. Common Mistakes

### Mistake 1 — IPv4 is 64 bits

Incorrect:

```text
IPv4 = 64 bits
```

Correct:

```text
IPv4 = 32 bits
```

IPv6 is 128 bits.

### Mistake 2 — Every IPv4 address is public

Incorrect.

Private IPv4 addresses are widely used inside local networks.

### Mistake 3 — The subnet mask is another IP address

The subnet mask has a different purpose:

```text
Network bits
Host bits
```

### Mistake 4 — The default gateway is required for same-subnet communication

A host communicating with another host on the same subnet does not normally need to send the packet to the default gateway.

### Mistake 5 — Network and broadcast addresses are normal host addresses

For a traditional `/24` network:

```text
192.168.1.0
```

is the network address.

```text
192.168.1.255
```

is the broadcast address.

They are not normally assigned to hosts.

---

# 📚 22. Revision Questions

1. What does IPv4 stand for?
2. How many bits are in an IPv4 address?
3. How many octets are in an IPv4 address?
4. How many bits are in each octet?
5. What is the range of values in one octet?
6. What is a subnet mask?
7. What does `/24` mean?
8. How many host bits are in a `/24`?
9. What is the network address of `192.168.1.10/24`?
10. What is the broadcast address?
11. What is the usable host range?
12. What is a default gateway?
13. When does a host use its default gateway?
14. What are the three private IPv4 ranges?
15. What is `127.0.0.1`?
16. What is the purpose of `169.254.0.0/16`?
17. What is unicast?
18. What is broadcast?
19. What is multicast?
20. What is the difference between an IP address and a MAC address?

---

# 📈 23. Day 07 Reflection

## What I Learned

- IPv4 addressing
- 32-bit IPv4 addresses
- Octets
- Binary representation
- Network and host portions
- Subnet masks
- CIDR notation
- Network addresses
- Host addresses
- Broadcast addresses
- Default gateway
- Private IPv4
- Public IPv4
- Special IPv4 addresses
- IPv4 traffic types
- Basic IPv4 configuration
- Packet Tracer IPv4 lab

## What I Need to Practice

- Binary conversion
- Reading subnet masks
- Understanding prefix notation
- Finding network addresses
- Finding broadcast addresses
- Finding usable host ranges
- Identifying private IPv4 ranges
- Understanding when a default gateway is used
- Configuring IPv4 addresses in Packet Tracer

---

# 🚀 Day 07 Status

**Completed ✅**

- [x] IPv4 addressing
- [x] 32-bit address structure
- [x] Octets
- [x] Binary representation
- [x] Network/host portions
- [x] Subnet masks
- [x] CIDR
- [x] Network address
- [x] Broadcast address
- [x] Default gateway
- [x] Private/public IPv4
- [x] Special IPv4 addresses
- [x] Packet Tracer practice

---


