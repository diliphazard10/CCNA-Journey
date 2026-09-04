# Day 09 Notes — IPv4 Header

## IPv4 Packet

```text
+----------------------+
|     IPv4 Header      |
+----------------------+
|       Payload        |
+----------------------+
```

Minimum header:

```text
20 bytes
```

## Header Fields

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

## Key Field Details

### Version
```text
4 bits
IPv4 = 4
```

### IHL
```text
4 bits
Minimum = 5
5 × 4 bytes = 20 bytes
```

### DSCP
```text
6 bits
QoS / traffic classification
```

### ECN
```text
2 bits
Congestion notification
```

### Total Length
```text
16 bits
Header + Payload
Maximum = 65,535 bytes
```

### Identification
```text
16 bits
Used for fragmentation
```

### Flags
```text
3 bits
DF = Don't Fragment
MF = More Fragments
```

### Fragment Offset
```text
13 bits
Fragment position
```

### TTL
```text
8 bits
Decreases by 1 at each router
```

Example:

```text
64 → 63 → 62
```

### Protocol
```text
8 bits

ICMP = 1
TCP  = 6
UDP  = 17
```

### Header Checksum
```text
16 bits
Checks IPv4 header
```

TTL changes at routers, so the IPv4 header checksum is recalculated.

### Source Address
```text
32 bits
Sender IPv4 address
```

### Destination Address
```text
32 bits
Destination IPv4 address
```

## Router Processing

```text
Receive frame
    ↓
Process IPv4 packet
    ↓
TTL - 1
    ↓
Recalculate checksum
    ↓
Route using destination IP
    ↓
New Layer 2 frame
    ↓
Forward
```

Remember:

```text
Layer 2 header → changes
TTL → decreases
IP addresses → normally remain the same
```

## Encapsulation

```text
Application Data
↓
TCP/UDP + Data
↓
IPv4 + TCP/UDP
↓
Ethernet + IPv4 + Trailer
```

## Quick Memory

```text
IPv4 = 4
Minimum header = 20 bytes
IHL minimum = 5
Total Length = header + payload
TTL = hop-count limit
TCP = 6
UDP = 17
ICMP = 1
Checksum = IPv4 header
DF = Don't Fragment
MF = More Fragments
```

## Self-Test

1. Minimum IPv4 header? → 20 bytes
2. Version? → 4
3. Minimum IHL? → 5
4. TTL change at router? → -1
5. TCP protocol number? → 6
6. UDP protocol number? → 17
7. ICMP protocol number? → 1
8. Checksum protects? → IPv4 header
9. Source/Destination address size? → 32 bits each
10. Does Layer 2 remain unchanged across routers? → No
