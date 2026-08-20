# Day 06 — Ethernet LAN Switching Part 2

> **CCNA 200-301 · Ethernet LAN Switching, ARP, Ping & Address Tables**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-06-green)
![Topic](https://img.shields.io/badge/Topic-Ethernet%20Switching%20Part%202-orange)
![Lab](https://img.shields.io/badge/Lab-Cisco%20Packet%20Tracer-red)

---

## 📌 Day 06 Overview

Today I continued studying **Ethernet LAN switching**.

The main focus was understanding how devices use **ARP and ICMP ping** to communicate over an Ethernet LAN, and how switches use **MAC address tables** while end devices use **ARP tables**.

### Topics Covered

- Ethernet packet/frame size
- Minimum Ethernet frame size
- Padding
- ARP
- ARP request
- ARP reply
- ARP table
- MAC address table
- Ping
- ICMP
- How ARP and ping work together
- How switches learn MAC addresses during communication
- How IP addresses and MAC addresses work together

---

# 🎯 Learning Objectives

By the end of Day 06, I should be able to:

- Explain why Ethernet has a minimum frame size.
- Explain what padding is.
- Explain what ARP does.
- Explain why ARP is required on an IPv4 Ethernet LAN.
- Explain the difference between an IP address and a MAC address.
- Explain an ARP request and ARP reply.
- Explain an ARP table.
- Explain a MAC address table.
- Distinguish an ARP table from a switch MAC address table.
- Explain what ping does.
- Explain the role of ICMP in ping.
- Trace the basic process of a first ping between two hosts.
- Explain how ARP and MAC learning happen during communication.
- Analyze ARP and ICMP traffic in Packet Tracer Simulation Mode.

---

# 🌐 1. The Big Picture

When two hosts communicate on the same IPv4 Ethernet LAN:

```text
Application
     ↓
ICMP / IP
     ↓
ARP resolves IPv4 → MAC
     ↓
Ethernet frame
     ↓
Switch
     ↓
Destination host
```

Two different address types are involved:

```text
IP Address
→ Layer 3 logical address

MAC Address
→ Layer 2 Ethernet address
```

ARP helps a host discover the MAC address associated with a local IPv4 next-hop address.

---

# 📦 2. Ethernet Frame Size

Traditional Ethernet has a minimum frame size of:

```text
64 bytes
```

A typical maximum Ethernet II frame size without an 802.1Q VLAN tag is:

```text
1518 bytes
```

The minimum frame size is important because it was tied to the original Ethernet CSMA/CD collision-detection operation.

---

# 🧩 3. Why Does Ethernet Need Padding?

If the upper-layer data is very small, Ethernet still needs to meet its minimum frame size requirement.

The sender can add:

```text
Padding
```

to make the payload large enough.

Example:

```text
Small data
   ↓
Not enough payload bytes
   ↓
Padding added
   ↓
Ethernet frame reaches minimum size
```

> **Padding fills the Ethernet payload when the upper-layer data is too small to meet the minimum Ethernet frame size.**

Padding is not application data.

---

# 📏 4. Minimum Ethernet Frame Calculation

A traditional Ethernet frame contains:

```text
Destination MAC = 6 bytes
Source MAC      = 6 bytes
Type/Length     = 2 bytes
Payload         = minimum 46 bytes
FCS             = 4 bytes
--------------------------------
Total           = 64 bytes
```

Therefore:

```text
6 + 6 + 2 + 46 + 4 = 64 bytes
```

If the actual upper-layer data is less than 46 bytes, padding can be added.

---

# 🔗 5. IP Address vs MAC Address

These are different.

### IP Address

Used for:

```text
Layer 3 logical addressing
```

Example:

```text
192.168.1.10
```

### MAC Address

Used for:

```text
Layer 2 local Ethernet delivery
```

Example:

```text
00:11:22:33:44:55
```

Easy memory:

```text
IP  → logical addressing
MAC → local Ethernet delivery
```

---

# 🧠 6. What Is ARP?

ARP stands for:

> **Address Resolution Protocol**

ARP is used with IPv4 to discover the MAC address associated with an IPv4 address on the local network.

Example:

```text
PC1 wants to send to:

IP = 192.168.1.20
```

PC1 knows the destination IP but needs a MAC address for the Ethernet frame.

ARP asks:

```text
Who has 192.168.1.20?
```

The device owning that IP responds with its MAC address.

---

# 📢 7. ARP Request

An ARP request essentially asks:

> Who has this IPv4 address?

Example:

```text
PC1:
Who has 192.168.1.20?
Tell 192.168.1.10
```

An ARP request is sent as an Ethernet broadcast on the local LAN.

Destination MAC:

```text
FF:FF:FF:FF:FF:FF
```

Every device in the relevant broadcast domain can receive the request.

Only the device configured with the requested IPv4 address should respond.

---

# 📬 8. ARP Reply

The device that owns the requested IP sends an ARP reply.

Example:

```text
PC2:
192.168.1.20 is at
BBBB.BBBB.BBBB
```

PC1 can then learn:

```text
192.168.1.20 → BBBB.BBBB.BBBB
```

PC1 can use that MAC address when creating Ethernet frames.

---

# 📋 9. ARP Table

An end device maintains an ARP cache/table containing IP-to-MAC mappings.

Example:

```text
IPv4 Address       MAC Address
---------------------------------
192.168.1.20        BBBB.BBBB.BBBB
192.168.1.30        CCCC.CCCC.CCCC
```

The important relationship is:

```text
IP address → MAC address
```

---

# 🆚 10. ARP Table vs MAC Address Table

Do not confuse these.

## ARP Table

Usually maintained by:

```text
PC / router
```

Maps:

```text
IPv4 address → MAC address
```

Example:

```text
192.168.1.20 → BBBB.BBBB.BBBB
```

## MAC Address Table

Maintained by:

```text
Ethernet switch
```

Maps:

```text
MAC address → switch port
```

Example:

```text
BBBB.BBBB.BBBB → Fa0/2
```

---

# 🔄 11. Putting the Tables Together

Suppose:

```text
PC1
IP  = 192.168.1.10
MAC = AAAA.AAAA.AAAA

PC2
IP  = 192.168.1.20
MAC = BBBB.BBBB.BBBB
```

PC1's ARP table:

```text
192.168.1.20 → BBBB.BBBB.BBBB
```

Switch MAC table:

```text
AAAA.AAAA.AAAA → Fa0/1
BBBB.BBBB.BBBB → Fa0/2
```

Together:

```text
IP address
   ↓
ARP table
   ↓
Destination MAC
   ↓
Switch MAC table
   ↓
Destination switch port
```

This is a key CCNA concept.

---

# 📡 12. What Is Ping?

`ping` is a network troubleshooting and connectivity-testing utility.

Normal ping uses:

```text
ICMP Echo Request
```

and expects:

```text
ICMP Echo Reply
```

Example:

```text
PC1 → ping 192.168.1.20
```

If the destination responds:

```text
ICMP Echo Reply
```

returns to PC1.

---

# 📨 13. ICMP

ICMP stands for:

> **Internet Control Message Protocol**

ICMP is used for network control, diagnostics, and error reporting.

Ping commonly uses:

```text
ICMP Echo Request
ICMP Echo Reply
```

> Ping is not a Layer 2 protocol. It uses IP/ICMP, while Ethernet carries the packets over the local network.

---

# 🔬 14. What Happens During the First Ping?

Consider:

```text
PC1 ─── Switch ─── PC2
```

PC1:

```text
192.168.1.10
```

PC2:

```text
192.168.1.20
```

PC1 starts:

```text
ping 192.168.1.20
```

If PC1 does not already know PC2's MAC address:

```text
1. PC1 checks its ARP cache.
2. PC1 does not find 192.168.1.20.
3. PC1 sends an ARP request.
4. Switch receives the Ethernet broadcast.
5. Switch learns PC1's source MAC.
6. Switch floods the broadcast within the relevant VLAN.
7. PC2 receives the ARP request.
8. PC2 sends an ARP reply.
9. PC1 learns PC2's IP-to-MAC mapping.
10. PC1 sends the ICMP Echo Request.
11. Switch uses its MAC table to forward the frame.
12. PC2 sends an ICMP Echo Reply.
13. PC1 receives the reply.
```

---

# 🧠 15. First Ping vs Later Ping

First communication may involve:

```text
ARP Request
     ↓
ARP Reply
     ↓
ICMP Echo Request
     ↓
ICMP Echo Reply
```

Later communication may not require a new ARP request if the ARP entry is still valid:

```text
ICMP Echo Request
     ↓
ICMP Echo Reply
```

This is why the first packet can behave differently from later packets.

---

# 🌊 16. ARP Request and Flooding

ARP requests use the Ethernet broadcast MAC:

```text
FF:FF:FF:FF:FF:FF
```

The switch floods broadcasts within the relevant VLAN.

Example:

```text
             PC2
              ↑
              |
PC1 → Switch ─┼──→ PC3
              |
              ↓
             PC4
```

ARP request:

```text
PC1 → Switch
          ├──→ PC2
          ├──→ PC3
          └──→ PC4
```

PC2 responds because it owns the requested IP.

---

# 🧠 17. What Does the Switch Learn During ARP?

When the ARP request enters the switch from PC1:

```text
Source MAC = PC1's MAC
```

The switch can learn:

```text
PC1 MAC → incoming port
```

Because the ARP request is a broadcast, the switch floods it out the other appropriate ports.

When PC2 sends the ARP reply, the switch sees PC2's source MAC and can learn:

```text
PC2 MAC → PC2's port
```

Therefore ARP traffic can help populate the switch MAC address table.

---

# 🔄 18. Communication Flow

A simplified same-LAN communication process:

```text
Application
    ↓
IP packet
    ↓
Need destination MAC?
    ↓
ARP
    ↓
Destination MAC learned
    ↓
Ethernet frame
    ↓
Switch checks destination MAC
    ↓
Forward to destination port
    ↓
Destination receives frame
```

---

# 🧪 19. Packet Tracer Lab

Build:

```text
PC1 ───┐
       │
PC2 ───┼─── Switch
       │
PC3 ───┘
```

Assign IP addresses in the same subnet.

Example:

```text
PC1 = 192.168.1.10 /24
PC2 = 192.168.1.20 /24
PC3 = 192.168.1.30 /24
```

Then:

```text
PC1 → ping 192.168.1.20
```

Use:

```text
Simulation Mode
```

and inspect the packets.

---

# 🔎 20. What to Analyze in Simulation Mode

### 1. ARP Request

Check:

```text
Source MAC
Destination MAC
Sender IP
Target IP
```

You should recognize:

```text
Destination MAC = FF:FF:FF:FF:FF:FF
```

### 2. ARP Reply

Check how PC2 provides:

```text
Its MAC address
```

for the requested IPv4 address.

### 3. ICMP Echo Request

After ARP resolution, inspect:

```text
Source IP
Destination IP
Source MAC
Destination MAC
ICMP Echo Request
```

### 4. ICMP Echo Reply

Inspect the response from PC2.

---

# 📋 21. Useful Verification Commands

On many end devices:

```text
arp -a
```

On a Cisco device, depending on platform/context:

```text
show arp
```

For the switch MAC address table:

```text
show mac address-table
```

To test connectivity:

```text
ping 192.168.1.20
```

---

# 🧪 22. Suggested Lab Experiments

## Experiment A — ARP

1. Build a small LAN.
2. Configure IP addresses.
3. Clear/empty ARP information if your simulator allows it.
4. Start Simulation Mode.
5. Ping another local host.
6. Observe the ARP request.
7. Observe the ARP reply.
8. Inspect the ARP table.

## Experiment B — MAC Learning

1. Check the switch MAC table before traffic.
2. Generate ARP traffic.
3. Check the MAC table again.
4. Identify which MAC addresses were learned.
5. Match each MAC address to a switch port.

## Experiment C — Ping

1. Ping the destination for the first time.
2. Observe ARP + ICMP.
3. Ping the same destination again.
4. Compare the second attempt.
5. Notice that ARP may not be repeated immediately because the ARP mapping can already be cached.

---

# 🧠 23. Important Differences

| Concept | Purpose | Mapping |
|---|---|---|
| ARP table | IPv4-to-MAC resolution | IP → MAC |
| MAC address table | Switch Layer 2 forwarding | MAC → Port |
| Ping | Connectivity test | ICMP Echo Request/Reply |
| ARP request | Discover MAC for IPv4 address | Broadcast |
| ARP reply | Provide requested MAC | Usually unicast response |
| Ethernet frame | Local Layer 2 delivery | MAC addresses |

---

# ⚠️ 24. Common Mistakes

### Mistake 1 — ARP maps MAC to IP

For normal ARP cache use, think:

```text
IP → MAC
```

---

### Mistake 2 — ARP is used for every destination on the Internet

ARP resolves a local IPv4 next-hop address.

For a remote destination, a host normally resolves the MAC address of its **default gateway**, not the remote host's MAC address.

---

### Mistake 3 — Ping is ARP

They are different:

```text
ARP
→ Resolves IPv4 address to MAC

Ping
→ Uses ICMP Echo Request/Reply
```

ARP may happen before the first ping on a local Ethernet network.

---

### Mistake 4 — The switch has an ARP table

A Layer 2 switch primarily maintains a:

```text
MAC address table
```

An end host maintains an:

```text
ARP cache/table
```

---

### Mistake 5 — Every ping starts with ARP

Not necessarily.

If the ARP entry is already cached and valid, the host can send the IP packet without another ARP request.

---

# 📚 25. Revision Questions

1. What is the minimum traditional Ethernet frame size?
2. Why does Ethernet require a minimum frame size?
3. What is padding?
4. When is Ethernet padding needed?
5. What does ARP stand for?
6. What problem does ARP solve?
7. What information does an ARP table store?
8. What is the destination MAC address of a typical ARP request?
9. What is the Ethernet broadcast MAC address?
10. What does an ARP reply provide?
11. What is the difference between an ARP table and a MAC address table?
12. What does ping normally use?
13. What are ICMP Echo Request and Echo Reply?
14. What can happen before the first ping packet is sent?
15. How can ARP traffic help a switch learn MAC addresses?
16. Why might a second ping not require another ARP request?
17. Does a host ARP for the remote Internet server's MAC address?
18. What MAC address does a host normally need when sending traffic to a remote network?
19. Which table maps IP addresses to MAC addresses?
20. Which table maps MAC addresses to switch ports?

---

# 📈 26. Day 06 Reflection

## What I Learned

- Ethernet minimum frame size
- Padding
- ARP
- ARP requests
- ARP replies
- ARP table
- MAC address table
- Ping
- ICMP Echo Request
- ICMP Echo Reply
- IP-to-MAC resolution
- MAC-to-port switching
- ARP flooding
- MAC address learning
- First ping behavior

## What I Need to Practice

- Explaining why Ethernet uses padding.
- Drawing an ARP request and reply.
- Identifying broadcast MAC addresses.
- Reading an ARP table.
- Reading a switch MAC address table.
- Explaining how ARP and ping work together.
- Analyzing the first ping in Packet Tracer Simulation Mode.
- Explaining the difference between local and remote destinations.

## Main Takeaway

> **ARP resolves a local IPv4 next-hop address to a MAC address. The Ethernet frame then uses MAC addresses for local delivery, while the switch uses its MAC address table to decide which port should receive a known unicast frame. Ping uses ICMP Echo Request and Echo Reply to test IP connectivity.**

---

# 🚀 Day 06 Status

**Completed ✅**

- [x] Ethernet frame size
- [x] Minimum Ethernet frame size
- [x] Padding
- [x] ARP
- [x] ARP request
- [x] ARP reply
- [x] ARP table
- [x] MAC address table
- [x] Ping
- [x] ICMP Echo Request
- [x] ICMP Echo Reply
- [x] MAC address learning
- [x] ARP flooding
- [x] Packet Tracer Simulation Mode analysis

---

**Next:** Day 07 — IPv4 Addressing Part 1
