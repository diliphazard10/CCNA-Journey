# Day 05 — Ethernet LAN Switching & Ethernet Frames Part 1

> **CCNA 200-301 v1.1 · Network Fundamentals / Network Access**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-05-green)
![Topic](https://img.shields.io/badge/Topic-Ethernet%20%26%20LAN%20Switching-orange)
![Lab](https://img.shields.io/badge/Lab-Cisco%20Packet%20Tracer-red)

---

## 📌 Day 05 Overview

Today I studied **Ethernet LAN switching** and learned how Ethernet frames are built and forwarded through a switch.

Topics covered:

- Ethernet frames
- Ethernet frame header and trailer
- Ethernet frame fields
- MAC addresses
- Source and destination MAC addresses
- Unicast frames
- Known unicast
- Unknown unicast
- Frame flooding
- MAC address learning
- MAC address tables
- How a switch decides where to forward a frame

This is a fundamental CCNA topic because Ethernet switching is the foundation of communication inside a local-area network.

---

# 🎯 Learning Objectives

By the end of Day 05, I should be able to:

- Explain what Ethernet is.
- Explain what an Ethernet frame is.
- Identify the major fields in an Ethernet frame.
- Explain the Ethernet header and trailer.
- Explain source and destination MAC addresses.
- Explain what a unicast frame is.
- Distinguish known unicast from unknown unicast.
- Explain why switches flood unknown unicast frames.
- Explain how a switch learns MAC addresses.
- Explain what a MAC address table contains.
- Explain how a switch uses its MAC address table to forward frames.
- Predict switch behavior when the destination MAC is known or unknown.

---

# 🌐 1. What Is Ethernet?

**Ethernet** is the most common technology used for wired Local Area Networks (LANs).

Ethernet defines rules for communication over a local network, including:

- Frame format
- MAC addressing
- Media access
- Local frame delivery

Ethernet is primarily associated with the **OSI Data Link Layer (Layer 2)**, while Ethernet physical standards also define Layer 1 characteristics such as cables, signals, and speeds.

Example LAN:

```text
PC1 ───┐
       │
PC2 ───┼─── Switch
       │
PC3 ───┘
```

---

# 📦 2. What Is an Ethernet Frame?

An Ethernet frame is the Layer 2 unit used to transport data across an Ethernet network.

A simplified frame:

```text
+------------------+------------------+
| Destination MAC  | Source MAC       |
+------------------+------------------+
| EtherType/Length | Payload          |
+------------------+------------------+
| FCS              |
+------------------+
```

A more complete representation:

```text
+----------+------+-------------+-------------+-------------+
| Preamble | SFD  | Destination | Source      | EtherType   |
+----------+------+-------------+-------------+-------------+
|                    Data / Payload                         |
+-----------------------------------------------------------+
| FCS                                                       |
+-----------------------------------------------------------+
```

---

# 🧱 3. Ethernet Frame Structure

```text
Preamble
   ↓
Start Frame Delimiter
   ↓
Destination MAC Address
   ↓
Source MAC Address
   ↓
EtherType / Length
   ↓
Payload
   ↓
Frame Check Sequence
```

| Field | Purpose |
|---|---|
| Preamble | Synchronization |
| SFD | Marks the start of the frame |
| Destination MAC | Layer 2 destination |
| Source MAC | Layer 2 source |
| EtherType/Length | Upper-layer protocol identification or length |
| Data/Payload | Carries higher-layer information |
| FCS | Detects transmission errors |

---

# 🟦 4. Preamble

The **Preamble** is used for synchronization between transmitting and receiving devices.

```text
Preamble = 7 bytes
```

It comes before the SFD and frame fields.

---

# 🟪 5. Start Frame Delimiter (SFD)

The **Start Frame Delimiter (SFD)** indicates that the actual Ethernet frame is about to begin.

```text
Preamble
   ↓
SFD
   ↓
Frame
```

SFD:

```text
1 byte
```

---

# 🟩 6. Destination MAC Address

The Destination MAC Address identifies the intended Layer 2 recipient.

Example:

```text
Destination:
AA:AA:AA:AA:AA:AA
```

A switch examines the destination MAC address when deciding where to forward an Ethernet frame.

---

# 🟨 7. Source MAC Address

The Source MAC Address identifies the device that sent the frame.

Example:

```text
Source:
11:11:11:11:11:11
```

A switch uses the source MAC address to **learn** which MAC address is associated with which switch port.

This is one of the most important Ethernet switching concepts.

---

# 🟧 8. EtherType / Length

In Ethernet II frames, the field after the source MAC address is the **EtherType** field.

Common EtherTypes:

```text
0x0800 → IPv4
0x0806 → ARP
0x86DD → IPv6
```

In IEEE 802.3 frame formats, the corresponding field can indicate payload length.

For CCNA, understand the common Ethernet II structure and recognize EtherType as an important field.

---

# 🟥 9. Data / Payload

The payload contains higher-layer information.

Example:

```text
Ethernet Frame
    ↓
IPv4 Packet
    ↓
TCP Segment
    ↓
Application Data
```

Another example:

```text
Ethernet Frame
    ↓
ARP Message
```

Typical Ethernet payload:

```text
46–1500 bytes
```

---

# ⬛ 10. Frame Check Sequence (FCS)

The **Frame Check Sequence (FCS)** is used for error detection.

It uses a cyclic redundancy check.

FCS:

```text
4 bytes
```

Important:

> FCS detects errors; it does not correct them.

---

# 📏 11. Ethernet Frame Size

Traditional Ethernet frame sizes:

```text
Minimum = 64 bytes
Maximum = 1518 bytes
```

These values refer to the frame from the Destination MAC through the FCS and exclude the preamble and SFD.

Typical Ethernet II frame:

```text
Destination MAC     6 bytes
Source MAC          6 bytes
EtherType           2 bytes
Payload             46–1500 bytes
FCS                 4 bytes
--------------------------------
Total               64–1518 bytes
```

> VLAN tagging adds 4 bytes to the Ethernet frame, so a tagged Ethernet frame can be larger than 1518 bytes.

---

# 🧬 12. MAC Addresses

MAC stands for:

> **Media Access Control**

A traditional Ethernet MAC address is:

```text
48 bits = 6 bytes
```

Example:

```text
00:1A:2B:3C:4D:5E
```

Other notation:

```text
00-1A-2B-3C-4D-5E
```

---

# 🔢 13. MAC Address Structure

A traditional MAC address can be viewed as:

```text
First 24 bits        Last 24 bits
      ↓                    ↓
     OUI             Device/interface
```

The first 24 bits are associated with the **Organizationally Unique Identifier (OUI)**.

The remaining bits identify the interface within that allocation.

---

# 🎯 14. Source and Destination MAC

Normal Ethernet unicast frames contain:

```text
Source MAC
Destination MAC
```

Example:

```text
PC1
MAC = 00:11:22:33:44:55

        ↓ Ethernet Frame

Source:
00:11:22:33:44:55

Destination:
AA:BB:CC:DD:EE:FF
```

---

# 📡 15. Unicast Frame

A **unicast** frame is intended for one specific Layer 2 destination.

Example:

```text
PC1 ─────→ PC2
```

Frame:

```text
Source MAC      = PC1
Destination MAC = PC2
```

---

# 🟢 16. Known Unicast

A **known unicast** occurs when the switch already knows the destination MAC address and the corresponding outgoing port.

Example:

```text
MAC Address          Port
---------------------------
AAAA.AAAA.AAAA       Fa0/1
BBBB.BBBB.BBBB       Fa0/2
```

Frame:

```text
Source      = AAAA.AAAA.AAAA
Destination = BBBB.BBBB.BBBB
```

The switch finds:

```text
BBBB.BBBB.BBBB → Fa0/2
```

Therefore, it forwards the frame only out:

```text
Fa0/2
```

---

# ❓ 17. Unknown Unicast

An **unknown unicast** occurs when:

- The destination MAC is a unicast MAC address.
- The switch does not have that destination MAC in its MAC address table.

Example:

```text
Destination:
CCCC.CCCC.CCCC
```

MAC table:

```text
AAAA.AAAA.AAAA → Fa0/1
BBBB.BBBB.BBBB → Fa0/2
```

No entry exists for:

```text
CCCC.CCCC.CCCC
```

Therefore:

```text
Unknown unicast
      ↓
Flood
```

---

# 🌊 18. Flooding

Flooding means sending a frame out multiple appropriate ports within the same Layer 2 domain/VLAN, excluding the port where the frame was received.

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

If the switch does not know PC2's MAC address:

```text
PC1 → Switch
          ├──→ PC2
          ├──→ PC3
          └──→ PC4
```

The destination device accepts the frame if the destination MAC matches.

Other devices discard it because the destination MAC does not match them.

---

# 🧠 19. Why Does a Switch Flood Unknown Unicast?

The switch has no information telling it which port leads to the destination MAC address.

Instead of dropping the frame, the switch sends it out the other appropriate ports.

This allows the destination to receive the frame.

At the same time, the switch can learn from the **source MAC address**.

---

# 🧠 20. MAC Address Learning

Switches dynamically learn MAC addresses.

Suppose:

```text
PC1
MAC = AAAA.AAAA.AAAA
```

PC1 sends a frame into:

```text
Fa0/1
```

The switch examines:

```text
Source MAC = AAAA.AAAA.AAAA
```

It learns:

```text
AAAA.AAAA.AAAA → Fa0/1
```

This information is stored in the MAC address table.

---

# 📋 21. MAC Address Table

A switch maintains a MAC address table, also called a forwarding table.

Example:

```text
MAC Address          Port
---------------------------
AAAA.AAAA.AAAA       Fa0/1
BBBB.BBBB.BBBB       Fa0/2
CCCC.CCCC.CCCC       Fa0/3
```

The switch uses this table to make Layer 2 forwarding decisions.

---

# 🔄 22. How a Switch Learns and Forwards

Simplified process:

```text
Frame arrives
     ↓
Learn source MAC
     ↓
Look at destination MAC
     ↓
Is destination known?
   /        YES       NO
  ↓         ↓
Forward    Flood
to known   out other
port       appropriate ports
```

---

# 🧪 23. Example: First Communication

Topology:

```text
PC1 ─── Switch ─── PC2
         |
        PC3
```

Initial MAC table:

```text
(empty)
```

PC1 sends a frame to PC2.

### Step 1 — Learn Source

The switch learns:

```text
PC1 MAC → PC1's port
```

### Step 2 — Check Destination

PC2's MAC is not in the table.

### Step 3 — Flood

The switch floods the frame out the other appropriate ports.

PC2 receives it.

PC3 also sees the frame but discards it because the destination MAC is not PC3's MAC.

---

# 🔄 24. Example: Later Communication

After learning:

```text
PC1 MAC → Fa0/1
PC2 MAC → Fa0/2
```

PC1 sends another frame to PC2.

The switch:

```text
1. Learns/refreshes PC1's source MAC
2. Looks up PC2's destination MAC
3. Finds Fa0/2
4. Sends frame only to Fa0/2
```

No flooding is necessary.

---

# 🧭 25. Switching Decision Process

When a frame arrives:

### Step 1

Look at the **source MAC**.

```text
Source MAC → learn/update table
```

### Step 2

Look at the **destination MAC**.

```text
Destination MAC → search table
```

### Step 3

If destination is known:

```text
Forward out associated port
```

### Step 4

If destination is unknown unicast:

```text
Flood out other appropriate ports
```

---

# 🆚 26. Known vs Unknown Unicast

| Type | Destination in MAC table? | Switch behavior |
|---|---:|---|
| Known unicast | Yes | Forward to specific port |
| Unknown unicast | No | Flood within relevant VLAN |

Remember:

> **Known = specific port**

> **Unknown = flood**

---

# 📡 27. Unicast vs Flooding

A unicast frame is addressed to one destination.

Flooding is a **forwarding behavior** used when the switch does not know the destination location for an unknown unicast.

Therefore:

```text
Unknown unicast
      ↓
Destination is one device
      ↓
Switch does not know its port
      ↓
Floods frame
```

Do not confuse **unicast addressing** with **switch flooding behavior**.

---

# 🧠 28. Important Switch Concepts

A Layer 2 switch primarily uses:

```text
MAC addresses
```

A switch learns from:

```text
Source MAC address
```

A switch forwards based on:

```text
Destination MAC address
```

Unknown unicast:

```text
Flood
```

Known unicast:

```text
Forward to specific port
```

---

# 🔬 29. Packet Tracer Lab

Recommended topology:

```text
PC1 ───┐
       │
PC2 ───┼─── Switch
       │
PC3 ───┘
```

### Suggested experiment

1. Start with a fresh or initialized switch.
2. Connect three PCs.
3. Configure IP addresses.
4. Generate traffic from PC1 to PC2.
5. Enter Simulation Mode.
6. Inspect the first Ethernet frame.
7. Identify source and destination MAC addresses.
8. Observe whether the destination MAC is known.
9. Observe flooding if the destination is unknown.
10. Inspect the switch MAC address table.
11. Generate the same communication again.
12. Observe known unicast forwarding.
13. Compare the first transmission with later transmissions.

---

# 🔎 30. Useful Cisco Commands

Display the MAC address table:

```text
Switch# show mac address-table
```

Display interface status:

```text
Switch# show interfaces status
```

Display interface details:

```text
Switch# show interfaces
```

Display running configuration:

```text
Switch# show running-config
```

---

# 🧪 31. What to Observe in Packet Tracer

When using Simulation Mode, inspect:

### Ethernet frame

Look for:

```text
Source MAC
Destination MAC
```

### First transmission

Ask:

```text
Is destination MAC known?
```

If not:

```text
Unknown unicast → flooding
```

### Later transmission

Ask:

```text
Has the switch learned the destination MAC?
```

If yes:

```text
Known unicast → specific port
```

---

# 📸 32. Recommended GitHub Evidence

Add screenshots from your actual Packet Tracer lab:

```text
screenshots/
├── 01-topology.png
├── 02-first-frame.png
├── 03-unknown-unicast-flooding.png
├── 04-mac-address-table.png
├── 05-known-unicast.png
└── 06-ethernet-frame-details.png
```

Save the actual Packet Tracer file:

```text
lab/
└── day-05-ethernet-switching.pkt
```

Do not create fake screenshots. Your GitHub repository should document the lab you actually performed.

---

# 🧠 33. Common Mistakes

### Mistake 1 — Thinking switches learn destination MAC addresses from the destination field

Switches learn MAC addresses from the:

```text
Source MAC address
```

---

### Mistake 2 — Thinking unknown unicast means broadcast

They are different.

```text
Unknown unicast
→ Destination is a specific unicast MAC
→ Switch does not know the port
→ Switch floods
```

Broadcast:

```text
Destination = FF:FF:FF:FF:FF:FF
```

---

### Mistake 3 — Thinking flooding means the frame becomes a broadcast

Flooding describes what the switch does with the frame.

The destination MAC remains the original destination MAC.

---

### Mistake 4 — Thinking a switch always sends frames everywhere

No.

If the destination MAC is known:

```text
Specific port
```

If it is an unknown unicast:

```text
Flood
```

---

# 📚 34. Revision Questions

1. What is Ethernet?
2. What is an Ethernet frame?
3. What is the purpose of the Destination MAC address?
4. What is the purpose of the Source MAC address?
5. What is the purpose of the EtherType field?
6. What is the purpose of the FCS?
7. How large is a traditional MAC address?
8. What is a unicast frame?
9. What is a known unicast?
10. What is an unknown unicast?
11. Why does a switch flood an unknown unicast?
12. What information does a switch use to learn MAC addresses?
13. What is a MAC address table?
14. How does a switch forward a known unicast?
15. Does the destination MAC change during flooding?
16. What happens to a flooded frame at a device that is not the destination?
17. What command displays the MAC address table?
18. Why is MAC learning important?
19. What happens during the first communication between two devices?
20. Why can later communication be more efficient?

---

# 📈 35. Day 05 Reflection

## What I Learned

- Ethernet LANs
- Ethernet frames
- Ethernet header
- Ethernet trailer
- Preamble
- Start Frame Delimiter
- Destination MAC
- Source MAC
- EtherType
- Payload
- FCS
- MAC addresses
- Unicast
- Known unicast
- Unknown unicast
- Flooding
- MAC address learning
- MAC address tables
- Switch forwarding decisions

## What I Need to Practice

- Drawing the Ethernet frame structure from memory.
- Identifying each Ethernet frame field.
- Reading source and destination MAC addresses.
- Understanding the difference between known and unknown unicast.
- Understanding why switches flood.
- Reading a switch MAC address table.
- Predicting which switch port a frame will exit.

## Main Takeaway

> **A switch learns source MAC addresses, looks up destination MAC addresses, and forwards known unicast frames to a specific port. If the destination unicast MAC is unknown, the switch floods the frame within the relevant VLAN.**

---

# 🚀 Day 05 Status

**Completed ✅**

- [x] Ethernet LAN switching
- [x] Ethernet frames
- [x] Ethernet frame header
- [x] Ethernet frame trailer
- [x] Preamble
- [x] Start Frame Delimiter
- [x] Destination MAC
- [x] Source MAC
- [x] EtherType / Length
- [x] Payload
- [x] FCS
- [x] MAC addresses
- [x] Unicast frames
- [x] Known unicast
- [x] Unknown unicast
- [x] Flooding
- [x] MAC address learning
- [x] MAC address table
- [x] Switch forwarding decisions
- [x] Packet Tracer analysis

---

**Next:** Day 06 — Ethernet LAN Switching Part 2
