# Day 08 Notes — Switch Interfaces

## CCNA 200-301

---

# 1. Switch Interface

Examples:

```text
FastEthernet0/1
GigabitEthernet0/1
GigabitEthernet0/2
```

A switch interface sends and receives network traffic.

---

# 2. Speed

Common Ethernet speeds:

```text
10 Mbps
100 Mbps
1 Gbps
10 Gbps
```

Speed = rate at which data can be transmitted.

---

# 3. Duplex

## Half-Duplex

```text
A → B
B → A
```

One direction at a time.

## Full-Duplex

```text
A ⇄ B
```

Both directions simultaneously.

Modern switched Ethernet normally uses full-duplex.

---

# 4. Auto-Negotiation

Ethernet devices can negotiate compatible:

```text
Speed
Duplex
```

General best practice:

```text
Both ends → compatible auto-negotiation
```

A forced setting on one side can cause a mismatch with a negotiating peer.

---

# 5. Interface Status

Important concepts:

```text
Administrative status
Operational status
```

Healthy example:

```text
up/up
```

Disable:

```text
shutdown
```

Enable:

```text
no shutdown
```

---

# 6. Important Commands

Quick summary:

```text
show ip interface brief
```

Detailed information:

```text
show interfaces
```

One interface:

```text
show interfaces gigabitEthernet0/1
```

Status summary:

```text
show interfaces status
```

Configuration:

```text
show running-config
```

Connectivity:

```text
ping <destination-IP>
```

---

# 7. Interface Counters

Important counters:

```text
Input packets
Output packets
Input bytes
Output bytes
Input errors
Output errors
CRC errors
Collisions
Drops
```

Counters are useful for troubleshooting.

---

# 8. CRC Errors

CRC = Cyclic Redundancy Check.

CRC errors indicate received frames failed CRC validation.

Possible causes:

```text
Bad cable
Bad connector
Physical-layer problem
Interface/hardware problem
```

---

# 9. Collisions

Collisions are associated with shared/half-duplex Ethernet.

Modern switched full-duplex Ethernet normally should not have normal collisions.

---

# 10. Troubleshooting Flow

```text
Physical
   ↓
Interface status
   ↓
Speed / Duplex
   ↓
Counters / Errors
   ↓
VLAN / Config
   ↓
IP
   ↓
Ping
```

---

# 11. Packet Tracer Practice

Topology:

```text
PC1 ───────── Switch
```

Check:

```text
show ip interface brief
```

Then:

```text
show interfaces gigabitEthernet0/1
```

Generate traffic:

```text
ping <destination-IP>
```

Check counters again.

---

# 12. Shutdown Lab

```text
enable
configure terminal
interface gigabitEthernet0/1
shutdown
```

Verify:

```text
show ip interface brief
```

Enable:

```text
no shutdown
```

Verify again.

---

# 13. Quick Memory Sheet

```text
Speed
→ Transmission rate

Half-duplex
→ One direction at a time

Full-duplex
→ Both directions simultaneously

Auto-negotiation
→ Negotiates compatible speed/duplex

shutdown
→ Disable interface

no shutdown
→ Enable interface

show ip interface brief
→ Quick overview

show interfaces
→ Detailed statistics

show interfaces status
→ Status/VLAN summary

CRC
→ Received frame failed CRC validation

up/up
→ Interface + line protocol operational
```

---

# 14. Self-Test

### Q1. What is duplex?

How data transmission occurs in both directions.

### Q2. Half-duplex?

One direction at a time.

### Q3. Full-duplex?

Both directions simultaneously.

### Q4. What does auto-negotiation do?

Negotiates compatible Ethernet capabilities such as speed and duplex.

### Q5. How do you disable an interface?

```text
shutdown
```

### Q6. How do you enable it?

```text
no shutdown
```

### Q7. Quick interface command?

```text
show ip interface brief
```

### Q8. Detailed interface command?

```text
show interfaces
```

### Q9. What can CRC errors indicate?

A physical/link problem or another condition causing received frames to fail CRC validation.

### Q10. What does up/up indicate?

The interface is enabled and the line protocol is operational.

---

# 🎯 Main Takeaway

> **When troubleshooting a switch interface, start from the physical and link layers. Check the connection, status, speed, duplex, counters, and errors before assuming the problem is IP.**
