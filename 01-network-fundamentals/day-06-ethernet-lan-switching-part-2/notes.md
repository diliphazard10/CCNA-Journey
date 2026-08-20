# Day 06 Notes — Ethernet LAN Switching Part 2

## CCNA 200-301

---

# 1. Ethernet Frame Size

Traditional Ethernet:

```text
Minimum = 64 bytes
Maximum = 1518 bytes
```

Frame calculation:

```text
Destination MAC = 6
Source MAC      = 6
Type/Length     = 2
Payload         = minimum 46
FCS             = 4
--------------------
Total           = 64 bytes
```

---

# 2. Padding

If the actual upper-layer data is too small to produce the minimum Ethernet frame size, padding is added.

```text
Small payload
     ↓
Padding added
     ↓
Minimum Ethernet frame size
```

Padding is not application data.

---

# 3. IP Address vs MAC Address

IP:

```text
Layer 3
Logical address
Example: 192.168.1.10
```

MAC:

```text
Layer 2
Ethernet address
Example: AAAA.AAAA.AAAA
```

Memory:

```text
IP  → logical addressing
MAC → local Ethernet delivery
```

---

# 4. ARP

ARP:

> Address Resolution Protocol

Purpose:

```text
IPv4 address → MAC address
```

Example:

```text
192.168.1.20
      ↓ ARP
BBBB.BBBB.BBBB
```

ARP resolves a local IPv4 next-hop address to its Ethernet MAC address.

---

# 5. ARP Request

Question:

```text
Who has 192.168.1.20?
```

Typical Ethernet destination:

```text
FF:FF:FF:FF:FF:FF
```

Therefore, an ARP request is broadcast on the local LAN.

---

# 6. ARP Reply

The device owning the requested IPv4 address responds:

```text
192.168.1.20 is at
BBBB.BBBB.BBBB
```

The requesting host can cache:

```text
192.168.1.20 → BBBB.BBBB.BBBB
```

---

# 7. ARP Table

An ARP table/cache maps:

```text
IPv4 address → MAC address
```

Example:

```text
IPv4 Address       MAC Address
---------------------------------
192.168.1.20        BBBB.BBBB.BBBB
192.168.1.30        CCCC.CCCC.CCCC
```

---

# 8. MAC Address Table

A switch maintains:

```text
MAC address → switch port
```

Example:

```text
AAAA.AAAA.AAAA → Fa0/1
BBBB.BBBB.BBBB → Fa0/2
CCCC.CCCC.CCCC → Fa0/3
```

---

# 9. ARP Table vs MAC Table

```text
ARP:
IP → MAC

Switch:
MAC → Port
```

ARP table is generally on:

```text
PC / router
```

MAC address table is on:

```text
Ethernet switch
```

---

# 10. Ping

Ping tests IP connectivity.

Typical sequence:

```text
ICMP Echo Request
        ↓
ICMP Echo Reply
```

Example:

```text
ping 192.168.1.20
```

---

# 11. ICMP

ICMP:

> Internet Control Message Protocol

Ping commonly uses:

```text
Echo Request
Echo Reply
```

---

# 12. First Ping

If the destination MAC is not known:

```text
1. Check ARP cache
2. ARP Request
3. ARP Request is broadcast
4. Switch floods broadcast
5. ARP Reply
6. Learn IP → MAC
7. ICMP Echo Request
8. ICMP Echo Reply
```

Simplified:

```text
ARP Request
     ↓
ARP Reply
     ↓
ICMP Echo Request
     ↓
ICMP Echo Reply
```

---

# 13. Later Ping

If the ARP mapping is cached:

```text
ICMP Echo Request
     ↓
ICMP Echo Reply
```

A new ARP request is not necessarily needed immediately.

---

# 14. ARP and MAC Learning

ARP request enters switch:

```text
Source MAC = PC1
Destination MAC = FF:FF:FF:FF:FF:FF
```

Switch learns:

```text
PC1 MAC → incoming port
```

ARP reply enters:

```text
Source MAC = PC2
```

Switch learns:

```text
PC2 MAC → incoming port
```

---

# 15. Local Communication

```text
Destination IPv4
       ↓
ARP
       ↓
Destination MAC
       ↓
Ethernet Frame
       ↓
Switch MAC Table
       ↓
Correct Port
       ↓
Destination
```

---

# 16. Remote Communication

For a remote destination:

```text
PC → Default Gateway → Remote Network
```

The host normally ARPs for:

```text
Default Gateway's MAC
```

It does not ARP for the remote server's MAC address.

---

# 17. Packet Tracer Lab

Topology:

```text
PC1 ───┐
       │
PC2 ───┼─── Switch
       │
PC3 ───┘
```

Example:

```text
PC1 = 192.168.1.10 /24
PC2 = 192.168.1.20 /24
PC3 = 192.168.1.30 /24
```

Test:

```text
ping 192.168.1.20
```

Use Simulation Mode.

Observe:

```text
ARP Request
ARP Reply
ICMP Echo Request
ICMP Echo Reply
```

---

# 18. Useful Commands

End device:

```text
arp -a
```

Cisco device:

```text
show arp
```

Switch:

```text
show mac address-table
```

Connectivity:

```text
ping 192.168.1.20
```

---

# 19. CCNA Memory Sheet

```text
Ethernet minimum
→ 64 bytes

Padding
→ Fills small payloads

ARP
→ IPv4 → MAC

ARP Request
→ Broadcast

Broadcast MAC
→ FF:FF:FF:FF:FF:FF

ARP Reply
→ Provides requested MAC

ARP table
→ IP → MAC

Switch MAC table
→ MAC → Port

Ping
→ ICMP Echo Request/Reply

First ping
→ ARP may happen first

Remote destination
→ ARP for default gateway MAC
```

---

# 20. Self-Test

### Q1
Minimum Ethernet frame?

```text
64 bytes
```

### Q2
Why padding?

```text
To meet the minimum Ethernet frame size
```

### Q3
ARP resolves?

```text
IPv4 address → MAC address
```

### Q4
ARP request destination MAC?

```text
FF:FF:FF:FF:FF:FF
```

### Q5
ARP table?

```text
IP → MAC
```

### Q6
Switch MAC table?

```text
MAC → Port
```

### Q7
Ping uses?

```text
ICMP Echo Request / Echo Reply
```

### Q8
What may happen before the first ping?

```text
ARP resolution
```

### Q9
For a remote destination, what MAC does the host normally need?

```text
Default gateway's MAC
```

---

# 21. Final Summary

Remember this chain:

```text
Destination IPv4
       ↓
ARP
       ↓
Destination/next-hop MAC
       ↓
Ethernet Frame
       ↓
Switch MAC Table
       ↓
Correct Port
       ↓
Destination
```

And:

```text
ARP table:
IP → MAC

MAC address table:
MAC → Port

Ping:
ICMP Echo Request/Reply
```
