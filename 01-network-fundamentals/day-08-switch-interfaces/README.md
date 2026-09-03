# Day 08 — Switch Interfaces

> **CCNA 200-301 · Network Access · Switch Interfaces**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-08-green)
![Topic](https://img.shields.io/badge/Topic-Switch%20Interfaces-orange)

## 📌 Day 08 Overview

Today I learned how to examine and troubleshoot **switch interfaces**.

### Topics Covered

- Interface speed
- Duplex
- Half-duplex and full-duplex
- Auto-negotiation
- Interface status
- Interface counters
- Interface errors
- CRC errors
- Cisco IOS interface verification commands
- Basic interface troubleshooting

## 🎯 Learning Objectives

By the end of Day 08, I should be able to:

- Explain interface speed and duplex.
- Explain half-duplex and full-duplex.
- Explain auto-negotiation.
- Understand why speed and duplex settings must be compatible.
- Identify administrative and operational interface status.
- Use Cisco IOS commands to inspect interfaces.
- Read interface counters.
- Recognize common interface errors.
- Troubleshoot a basic Ethernet link.

---

# 🔌 1. Switch Interfaces

A switch interface is a physical connection used to send and receive network traffic.

Examples:

```text
FastEthernet0/1
GigabitEthernet0/1
GigabitEthernet0/2
```

Each interface can have its own configuration and operational state.

---

# ⚡ 2. Interface Speed

Speed determines how quickly an interface can transmit data.

Common Ethernet speeds:

```text
10 Mbps
100 Mbps
1 Gbps
10 Gbps
```

Examples:

```text
FastEthernet → commonly 100 Mbps
GigabitEthernet → commonly 1 Gbps
```

The actual speed depends on the capabilities and configuration of both ends of the link.

---

# 🔄 3. Duplex

Duplex describes how an interface sends and receives data.

## Half-Duplex

Only one side can transmit at a time:

```text
A → B
B → A
```

## Full-Duplex

Both sides can transmit and receive simultaneously:

```text
A ⇄ B
```

Modern switched Ethernet normally uses full-duplex operation.

---

# 🤝 4. Auto-Negotiation

Auto-negotiation allows connected Ethernet devices to determine compatible capabilities.

It can negotiate settings such as:

```text
Speed
Duplex
```

A good general approach is to allow both ends to negotiate when supported.

> Avoid manually forcing one side while leaving the other side to negotiate, because this can create a speed/duplex mismatch.

---

# ⚠️ 5. Speed and Duplex Mismatch

A mismatch can cause poor network performance.

Example:

```text
Switch → Full Duplex
PC     → Half Duplex
```

Possible symptoms include:

- Poor performance
- Collisions
- Late collisions
- Interface errors
- Packet loss
- Retransmissions

Always check both ends of the link.

---

# 🟢 6. Interface Status

Two important concepts are:

```text
Administrative status
Operational status
```

A commonly healthy state is:

```text
up / up
```

This means the interface is enabled and the line protocol is operational.

An interface can be administratively disabled with:

```text
shutdown
```

and enabled again with:

```text
no shutdown
```

---

# 🔎 7. show ip interface brief

One of the most useful Cisco commands is:

```text
show ip interface brief
```

It provides a quick overview of interfaces.

Example:

```text
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/1     unassigned      YES unset  up                    up
GigabitEthernet0/2     unassigned      YES unset  down                  down
```

Important fields:

```text
Status
Protocol
```

---

# 🧰 8. show interfaces

For detailed information:

```text
show interfaces gigabitEthernet0/1
```

Information can include:

```text
Interface status
Line protocol
MAC address
MTU
Speed
Duplex
Input packets
Output packets
Input errors
Output errors
CRC errors
Collisions
Drops
```

---

# 📊 9. Interface Counters

Interface counters show traffic statistics and can help identify problems.

Important counters include:

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

Compare counters over time and after generating traffic to understand what is happening on the link.

---

# ❌ 10. Common Interface Errors

## CRC Errors

CRC errors mean received frames failed the Cyclic Redundancy Check.

Possible causes include:

```text
Damaged cable
Bad connector
Physical-layer problem
Interface/hardware problem
```

## Input Errors

Errors detected while receiving traffic.

## Output Errors

Problems encountered while transmitting traffic.

## Collisions

Collisions are associated with shared or half-duplex Ethernet.

Modern switched full-duplex Ethernet normally should not have normal collisions.

---

# 🧪 11. Packet Tracer Lab

Create:

```text
PC1 ───────── Switch
```

Connect PC1 to a switch interface.

Check the interface:

```text
show interfaces gigabitEthernet0/1
```

Then check the summary:

```text
show ip interface brief
```

Record:

```text
Speed:
Duplex:
Input packets:
Output packets:
Input errors:
Output errors:
CRC:
Collisions:
```

Generate traffic with:

```text
ping <destination-IP>
```

Run the interface command again and observe the counters.

---

# 🔬 12. Shutdown / No Shutdown Lab

Enter interface configuration:

```text
enable
configure terminal
interface gigabitEthernet0/1
```

Disable:

```text
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

Observe the interface status before and after.

---

# 🔬 13. Interface Troubleshooting Flow

Use this basic sequence:

```text
1. Physical connection
        ↓
2. Interface status
        ↓
3. Speed / Duplex
        ↓
4. Counters / Errors
        ↓
5. VLAN / Configuration
        ↓
6. IP Configuration
        ↓
7. Connectivity test
```

Useful commands:

```text
show ip interface brief
show interfaces status
show interfaces
show running-config
ping <destination-IP>
```

---

# 🧠 14. Quick Comparison

| Topic | Meaning |
|---|---|
| Speed | Rate at which data is transmitted |
| Duplex | How transmission occurs in both directions |
| Half-duplex | One direction at a time |
| Full-duplex | Both directions simultaneously |
| Auto-negotiation | Devices negotiate compatible capabilities |
| Administrative status | Whether the interface is enabled/disabled |
| Operational status | Whether the interface is currently operational |
| Interface counters | Traffic and error statistics |
| CRC errors | Received frames failing CRC validation |

---

# 🧠 15. CCNA Memory Sheet

```text
Speed
→ 10 Mbps / 100 Mbps / 1 Gbps / 10 Gbps etc.

Duplex
→ Half or Full

Half-duplex
→ One direction at a time

Full-duplex
→ Both directions simultaneously

Auto-negotiation
→ Negotiates compatible Ethernet capabilities

shutdown
→ Administratively disables interface

no shutdown
→ Enables interface

show ip interface brief
→ Quick interface overview

show interfaces
→ Detailed interface information

show interfaces status
→ Interface/VLAN status summary

CRC errors
→ Received frames failed CRC validation

up/up
→ Interface and line protocol operational
```

---

# 📚 16. Revision Questions

1. What does interface speed mean?
2. What is duplex?
3. What is the difference between half-duplex and full-duplex?
4. What is auto-negotiation?
5. Why should speed and duplex settings be compatible?
6. What does `up/up` mean?
7. What does `shutdown` do?
8. What does `no shutdown` do?
9. What does `show ip interface brief` display?
10. What does `show interfaces` provide?
11. What are interface counters?
12. What can CRC errors indicate?
13. Why are collisions generally unexpected on modern full-duplex switched Ethernet?
14. Why should you check both ends of an Ethernet link?
15. Which command gives a quick interface summary?
16. Which command provides detailed interface statistics?

---

# 📈 17. Day 08 Reflection

## What I Learned

- Switch interfaces
- Interface speed
- Duplex
- Half-duplex
- Full-duplex
- Auto-negotiation
- Interface status
- Interface counters
- Interface errors
- CRC errors
- Cisco IOS verification commands
- Basic interface troubleshooting

## What I Need to Practice

- Reading `show ip interface brief`
- Reading `show interfaces`
- Understanding interface status
- Checking speed and duplex
- Reading interface counters
- Identifying CRC and other errors
- Troubleshooting a switch-to-PC link in Packet Tracer

---



