# Day 05 Notes — Ethernet LAN Switching & Ethernet Frames Part 1

## CCNA 200-301 v1.1

---

# 1. Ethernet

Ethernet is the dominant technology used for wired LANs.

It defines:

- Frame format
- MAC addressing
- Local frame delivery
- Media access
- Physical characteristics through Ethernet standards

Ethernet is primarily associated with:

```text
Layer 2 → Data Link
Layer 1 → Physical
```

---

# 2. Ethernet Frame

```text
+---------------------+
| Preamble             |
+---------------------+
| SFD                  |
+---------------------+
| Destination MAC      |
+---------------------+
| Source MAC           |
+---------------------+
| EtherType / Length   |
+---------------------+
| Data / Payload       |
+---------------------+
| FCS                  |
+---------------------+
```

---

# 3. Ethernet Frame Fields

| Field | Size | Purpose |
|---|---:|---|
| Preamble | 7 bytes | Synchronization |
| SFD | 1 byte | Indicates frame start |
| Destination MAC | 6 bytes | Layer 2 destination |
| Source MAC | 6 bytes | Layer 2 source |
| EtherType/Length | 2 bytes | Protocol identification or length |
| Payload | 46–1500 bytes | Carries higher-layer data |
| FCS | 4 bytes | Error detection |

For Ethernet II:

```text
Destination MAC
      ↓
Source MAC
      ↓
EtherType
      ↓
Payload
      ↓
FCS
```

---

# 4. Important EtherTypes

```text
0x0800 → IPv4
0x0806 → ARP
0x86DD → IPv6
```

---

# 5. FCS

FCS:

> Frame Check Sequence

Purpose:

```text
Error detection
```

It uses a cyclic redundancy check.

Important:

```text
FCS detects errors.
FCS does NOT correct errors.
```

FCS:

```text
4 bytes
```

---

# 6. Ethernet Frame Size

Traditional Ethernet:

```text
Minimum frame = 64 bytes
Maximum frame = 1518 bytes
```

These values exclude:

```text
Preamble
SFD
```

Typical Ethernet II:

```text
6 + 6 + 2 + 46–1500 + 4
```

---

# 7. MAC Address

MAC:

> Media Access Control

Traditional Ethernet MAC:

```text
48 bits
=
6 bytes
```

Example:

```text
00:1A:2B:3C:4D:5E
```

---

# 8. MAC Address Structure

Traditional MAC:

```text
48 bits
```

Conceptually:

```text
First 24 bits
     ↓
OUI

Last 24 bits
     ↓
Interface/device portion
```

---

# 9. Source vs Destination MAC

Normal Ethernet unicast frames contain:

```text
Source MAC
Destination MAC
```

The switch learns from:

```text
Source MAC
```

The switch forwards using:

```text
Destination MAC
```

---

# 10. Unicast

Unicast means:

> One sender → one intended destination

Example:

```text
PC1 ─────────→ PC2
```

---

# 11. Known Unicast

Destination MAC exists in the switch MAC table.

Example:

```text
MAC Address          Port
---------------------------
AAAA.AAAA.AAAA       Fa0/1
BBBB.BBBB.BBBB       Fa0/2
```

If:

```text
Destination = BBBB.BBBB.BBBB
```

the switch forwards:

```text
→ Fa0/2
```

---

# 12. Unknown Unicast

Destination MAC is a unicast address but is not in the MAC table.

Example:

```text
Destination:
CCCC.CCCC.CCCC
```

No matching table entry:

```text
Unknown unicast
       ↓
Flood
```

---

# 13. Flooding

Flooding means the switch sends the frame out multiple appropriate ports within the same Layer 2 domain/VLAN, except the receiving port.

```text
PC1 → Switch
          ├──→ PC2
          ├──→ PC3
          └──→ PC4
```

---

# 14. MAC Learning

Switches learn MAC addresses from the:

```text
SOURCE MAC
```

Example:

```text
Source MAC = AAAA.AAAA.AAAA
Incoming port = Fa0/1
```

Switch learns:

```text
AAAA.AAAA.AAAA → Fa0/1
```

---

# 15. MAC Address Table

Example:

```text
MAC Address          Port
---------------------------
AAAA.AAAA.AAAA       Fa0/1
BBBB.BBBB.BBBB       Fa0/2
CCCC.CCCC.CCCC       Fa0/3
```

Concept:

```text
MAC Address → Switch Port
```

---

# 16. Switch Decision Process

```text
Frame arrives
     ↓
Read Source MAC
     ↓
Learn/update table
     ↓
Read Destination MAC
     ↓
Is destination known?
   /        YES       NO
  ↓         ↓
Forward    Flood
specific   other
port       ports
```

---

# 17. First Communication

Initially:

```text
MAC table = empty
```

PC1 sends to PC2.

Switch:

```text
1. Learns PC1 source MAC
2. Does not know PC2 destination MAC
3. Floods frame
```

PC2 receives it.

Other devices see the frame but discard it if they are not the destination.

---

# 18. Later Communication

After learning:

```text
PC1 MAC → Fa0/1
PC2 MAC → Fa0/2
```

PC1 sends to PC2.

Switch:

```text
1. Learn/refresh source
2. Look up destination
3. Find Fa0/2
4. Forward only to Fa0/2
```

No flooding.

---

# 19. Known vs Unknown Unicast

| Type | Table entry? | Action |
|---|---:|---|
| Known unicast | Yes | Specific port |
| Unknown unicast | No | Flood |

Memory:

```text
KNOWN
→ Specific port

UNKNOWN
→ Flood
```

---

# 20. Unicast vs Flooding

Unicast describes:

```text
One intended destination
```

Flooding describes:

```text
Switch forwarding behavior
```

Therefore:

```text
Unknown unicast
       ↓
Switch floods
```

The destination MAC does not become a broadcast MAC.

---

# 21. Broadcast vs Unknown Unicast

Broadcast:

```text
FF:FF:FF:FF:FF:FF
```

Unknown unicast:

```text
Specific unicast MAC
but
not in MAC table
```

Both may result in multiple ports receiving a frame, but they are different concepts.

---

# 22. Useful Commands

Display MAC table:

```text
show mac address-table
```

Interface status:

```text
show interfaces status
```

Interface details:

```text
show interfaces
```

Running configuration:

```text
show running-config
```

---

# 23. Packet Tracer Lab

Topology:

```text
PC1 ───┐
       │
PC2 ───┼─── Switch
       │
PC3 ───┘
```

Experiment:

```text
1. Start with a fresh switch.
2. Connect three PCs.
3. Configure IP addresses.
4. Generate traffic.
5. Enter Simulation Mode.
6. Inspect the Ethernet frame.
7. Identify source MAC.
8. Identify destination MAC.
9. Observe unknown unicast flooding.
10. Inspect MAC address table.
11. Generate traffic again.
12. Observe known unicast forwarding.
```

---

# 24. What to Watch

First transmission:

```text
Destination unknown
        ↓
Flood
```

After MAC learning:

```text
Destination known
        ↓
Specific port
```

Most important:

> **Switches learn source MAC addresses and use destination MAC addresses for forwarding decisions.**

---

# 25. CCNA Memory Sheet

```text
Ethernet
→ Wired LAN technology

MAC
→ Layer 2 address

MAC size
→ 48 bits / 6 bytes

Switch learns from
→ Source MAC

Switch forwards based on
→ Destination MAC

Known unicast
→ Specific port

Unknown unicast
→ Flood

Broadcast
→ FF:FF:FF:FF:FF:FF

FCS
→ Error detection

EtherType
→ Identifies upper-layer protocol in Ethernet II
```

---

# 26. Self-Test

### Q1. How many bits are in a traditional Ethernet MAC address?

```text
48 bits
```

### Q2. What MAC address does a switch learn from?

```text
Source MAC
```

### Q3. What MAC address does a switch use for forwarding decisions?

```text
Destination MAC
```

### Q4. What happens when the destination unicast MAC is unknown?

```text
Flood
```

### Q5. What happens when the destination MAC is known?

```text
Forward to the associated port
```

### Q6. What is FCS used for?

```text
Error detection
```

### Q7. What is the Ethernet broadcast MAC address?

```text
FF:FF:FF:FF:FF:FF
```

---

# 27. Final Summary

The most important switching process:

```text
Frame arrives
     ↓
Learn Source MAC
     ↓
Check Destination MAC
     ↓
Known?
  /   Yes   No
 ↓     ↓
Forward Flood
```

Remember:

> **Switches learn source MAC addresses.**

> **Switches use destination MAC addresses to forward frames.**

> **Known unicast → specific port.**

> **Unknown unicast → flood within the relevant VLAN.**
