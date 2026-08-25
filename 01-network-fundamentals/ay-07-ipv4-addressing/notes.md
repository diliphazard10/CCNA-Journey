# Day 07 Notes — IPv4 Addressing

## CCNA 200-301 · Network Fundamentals

---

# 1. IPv4

IPv4 = Internet Protocol version 4

```text
Layer 3
Logical addressing
32 bits
```

Example:

```text
192.168.1.10
```

---

# 2. IPv4 Structure

```text
4 octets
×
8 bits each
=
32 bits
```

Example:

```text
192.168.1.10
```

Each octet:

```text
0–255
```

Binary place values:

```text
128 64 32 16 8 4 2 1
```

---

# 3. Network + Host

An IPv4 address contains:

```text
Network portion
+
Host portion
```

The subnet mask/prefix determines the boundary.

Example:

```text
192.168.1.10/24
```

```text
Network bits = 24
Host bits    = 8
```

---

# 4. Subnet Mask

Example:

```text
255.255.255.0
```

Binary:

```text
11111111.11111111.11111111.00000000
```

Memory:

```text
1 → network
0 → host
```

---

# 5. CIDR

CIDR = Classless Inter-Domain Routing

Example:

```text
192.168.1.10/24
```

`/24` means:

```text
24 network bits
8 host bits
```

---

# 6. /24 Network

Given:

```text
192.168.1.10/24
```

Network:

```text
192.168.1.0
```

First usable:

```text
192.168.1.1
```

Last usable:

```text
192.168.1.254
```

Broadcast:

```text
192.168.1.255
```

Total:

```text
2^8 = 256
```

Typical usable hosts:

```text
256 - 2 = 254
```

---

# 7. Default Gateway

Used to reach remote networks.

Example:

```text
PC:
192.168.1.10/24

Gateway:
192.168.1.1
```

Same subnet:

```text
PC1 → PC2
```

Remote subnet:

```text
PC1 → Gateway → Router → Remote Network
```

---

# 8. Private IPv4 Ranges

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

---

# 9. Special Addresses

Loopback:

```text
127.0.0.0/8
```

Common:

```text
127.0.0.1
```

Link-local:

```text
169.254.0.0/16
```

Unspecified:

```text
0.0.0.0
```

Default route:

```text
0.0.0.0/0
```

---

# 10. IPv4 Traffic Types

```text
Unicast:
1 → 1

Broadcast:
1 → all

Multicast:
1 → group
```

---

# 11. IPv4 Configuration

Basic settings:

```text
IP address
Subnet mask/prefix
Default gateway
```

Example:

```text
IP:
192.168.1.10

Mask:
255.255.255.0

Gateway:
192.168.1.1
```

---

# 12. Useful Commands

Packet Tracer PC:

```text
ipconfig
```

Connectivity:

```text
ping 192.168.1.20
```

---

# 13. CCNA Memory Sheet

```text
IPv4
→ 32 bits

Octets
→ 4

Each octet
→ 8 bits

Octet range
→ 0–255

Subnet mask
→ Network/host boundary

/24
→ 24 network + 8 host

/24 total
→ 256 addresses

/24 typical usable
→ 254 hosts

Network
→ Identifies the subnet

Broadcast
→ Reaches all hosts in the local subnet

Private:
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16

Loopback:
127.0.0.0/8

Link-local:
169.254.0.0/16

Gateway:
→ Remote network access
```

---

# 14. Quick Self-Test

### Q1
IPv4 size?

```text
32 bits
```

### Q2
Octets?

```text
4
```

### Q3
Bits per octet?

```text
8
```

### Q4
Maximum octet value?

```text
255
```

### Q5
What does `/24` mean?

```text
24 network bits
8 host bits
```

### Q6
Network of `192.168.1.10/24`?

```text
192.168.1.0
```

### Q7
Broadcast?

```text
192.168.1.255
```

### Q8
Private 10-range?

```text
10.0.0.0/8
```

### Q9
Private 172-range?

```text
172.16.0.0/12
```

### Q10
Private 192-range?

```text
192.168.0.0/16
```

### Q11
Loopback?

```text
127.0.0.1
```

### Q12
Default gateway purpose?

```text
Reach destinations outside the local subnet
```

---

# 15. Final Concept

```text
IPv4 Address
      │
      ├── Network Portion
      │
      └── Host Portion
             │
             ↓
        Subnet Mask
             │
      ┌──────┴──────┐
      ↓             ↓
 Network         Broadcast
 Address          Address
```

> **Most important idea: the subnet mask/prefix determines which part of an IPv4 address represents the network and which part represents the host.**
