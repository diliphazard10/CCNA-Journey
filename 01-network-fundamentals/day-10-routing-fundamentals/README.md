# Day 10 — Routing Fundamentals

> **CCNA 200-301 · Network Layer · Routing Fundamentals**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-10-green)
![Topic](https://img.shields.io/badge/Topic-Routing%20Fundamentals-orange)

---

## 📌 Day 10 Overview

Today I learned the fundamentals of **IP routing** and how routers decide where to send packets.

### Topics Covered

- What is routing?
- What is a router?
- Routing table
- Connected routes
- Local routes
- Routing table entries
- Route selection
- Longest Prefix Match
- Administrative Distance
- Metric
- Next-hop routing
- Default route concept

---

# 🎯 Learning Objectives

By the end of Day 10, I should be able to:

- Explain what routing is.
- Explain the role of a router.
- Explain what a routing table contains.
- Understand connected routes.
- Understand local routes.
- Understand how a router selects a route.
- Explain Longest Prefix Match.
- Understand Administrative Distance at a basic level.
- Understand metrics at a basic level.
- Explain next-hop forwarding.
- Read basic Cisco routing-table output.

---

# 🌐 1. What Is Routing?

**Routing** is the process of determining the path that packets should take from a source network to a destination network.

Example:

```text
PC1
 |
 R1
 |
 R2
 |
PC2
```

If PC1 wants to communicate with PC2, routers examine the destination IP address and determine where to forward the packet.

Routing is primarily a **Layer 3 / Network Layer** function.

---

# 🚦 2. What Is a Router?

A router connects different IP networks and forwards packets between them.

Example:

```text
        R1
     /      LAN A      LAN B
```

A router uses its **routing table** to make forwarding decisions.

---

# 📋 3. Routing Table

A routing table is a collection of routes that tells the router how to reach destination networks.

Example:

```text
R1# show ip route
```

A simplified routing table could look like:

```text
C    192.168.1.0/24 is directly connected
L    192.168.1.1/32 is directly connected
C    10.0.0.0/30 is directly connected
L    10.0.0.1/32 is directly connected
```

Important information can include:

```text
Route
Prefix
Next hop
Outgoing interface
Route source
Metric
Administrative distance
```

---

# 🔗 4. Connected Route

A **connected route** is automatically created when an interface is configured with an IP address and is operational.

Example:

```text
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
```

The router can install:

```text
C 192.168.1.0/24 is directly connected, GigabitEthernet0/0
```

`C` means:

```text
Connected
```

This tells the router that the `192.168.1.0/24` network is directly connected.

---

# 🎯 5. Local Route

A **local route** represents the IP address assigned to the router's own interface.

Example:

```text
L 192.168.1.1/32 is directly connected, GigabitEthernet0/0
```

`L` means:

```text
Local
```

The `/32` means that the route identifies one exact IPv4 address.

So:

```text
C 192.168.1.0/24
```

represents the connected network.

While:

```text
L 192.168.1.1/32
```

represents the router's own interface IP address.

---

# 🔍 6. Connected vs Local Route

| Route | Example | Meaning |
|---|---|---|
| Connected | `192.168.1.0/24` | Directly connected network |
| Local | `192.168.1.1/32` | Router's own interface address |

Think:

```text
C → The network is connected to me.

L → This exact IP belongs to me.
```

---

# 🧭 7. Route Selection

A router may have multiple routes that could potentially match a destination.

The router must choose the best route.

The most important first step is:

> **Longest Prefix Match**

The route with the most specific matching prefix is preferred.

Example:

```text
10.0.0.0/8
10.1.0.0/16
10.1.1.0/24
```

Destination:

```text
10.1.1.50
```

All three routes can match, but:

```text
10.1.1.0/24
```

is the most specific.

Therefore:

```text
/24 wins over /16
/16 wins over /8
```

---

# 🧠 8. Longest Prefix Match

Remember:

```text
More specific prefix
        ↓
Better match
```

Example:

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```

For:

```text
10.10.10.25
```

the router selects:

```text
10.10.10.0/24
```

because `/24` is the longest matching prefix.

---

# 🏆 9. Route Selection Order

For routes to the same destination prefix, Cisco route selection considers:

### 1. Longest Prefix Match

The most specific route wins.

Example:

```text
/24 > /16 > /8
```

### 2. Administrative Distance

If multiple routes to the **same destination prefix** come from different routing sources, the route with the lower Administrative Distance is preferred.

Common examples:

```text
Connected = 0
Static = 1
EIGRP = 90
OSPF = 110
RIP = 120
```

These values are useful to remember for CCNA.

### 3. Metric

If routes come from the same routing protocol, the protocol's metric is used to select the best path.

Different routing protocols calculate metrics differently.

---

# 📊 10. Administrative Distance

Administrative Distance (AD) indicates how trustworthy a routing source is compared with other routing sources.

Lower AD is preferred.

Common Cisco values:

| Route Source | AD |
|---|---:|
| Connected | 0 |
| Static | 1 |
| EIGRP | 90 |
| OSPF | 110 |
| RIP | 120 |

Example:

```text
OSPF → 110
RIP  → 120
```

If both provide routes to the same destination prefix, OSPF has the lower AD and is preferred.

> **AD compares different sources of routing information. It is not the same thing as a routing protocol's metric.**

---

# 📏 11. Metric

A **metric** is a value used by a routing protocol to determine which path is better among routes learned through that same protocol.

Examples:

```text
OSPF → Cost
RIP  → Hop count
EIGRP → Composite metric
```

In general:

```text
Better metric
→ Preferred path
```

The exact meaning of "better" depends on the routing protocol.

---

# 🛣️ 12. Next Hop

A route can tell the router where to send a packet next.

Example:

```text
Destination: 192.168.3.0/24
Next Hop:    10.0.0.2
```

The router forwards the packet toward:

```text
10.0.0.2
```

This is called the **next-hop router**.

---

# 🔌 13. Outgoing Interface

A route can also identify the interface through which the packet should leave.

Example:

```text
C 192.168.1.0/24 is directly connected, GigabitEthernet0/0
```

The router knows:

```text
Destination network
        ↓
GigabitEthernet0/0
```

---

# 🌎 14. Default Route

A default route is used when no more specific route matches the destination.

IPv4 default route:

```text
0.0.0.0/0
```

It matches all IPv4 destinations, but it is the least specific IPv4 prefix.

Think:

```text
Specific route exists?
       ↓
      YES → use it

      NO
       ↓
Default route
```

---

# 🧪 15. Cisco CLI Practice

Display the routing table:

```text
show ip route
```

Display only connected routes:

```text
show ip route connected
```

Display only local routes:

```text
show ip route local
```

Check a specific route:

```text
show ip route 192.168.1.0
```

Check interfaces:

```text
show ip interface brief
```

Test connectivity:

```text
ping <destination-IP>
```

Trace the path:

```text
traceroute <destination-IP>
```

---

# 🧪 16. Packet Tracer Lab

Build:

```text
PC1 ── R1 ── R2 ── PC2
```

Configure IP addresses on the router interfaces.

Then check:

```text
show ip route
```

Identify:

```text
C = Connected
L = Local
```

Record the routes.

Example:

```text
C 192.168.1.0/24
L 192.168.1.1/32

C 10.0.0.0/30
L 10.0.0.1/32
```

Then inspect the routing table on both routers.

---

# 🔬 17. Route Selection Lab

Create routes that overlap.

Example:

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```

Test a destination:

```text
10.10.10.50
```

Determine which route is selected.

Answer:

```text
10.10.10.0/24
```

because it is the longest matching prefix.

---

# 🔧 18. Troubleshooting Flow

When a router cannot reach a destination:

```text
1. Check interface status
        ↓
2. Check IP addressing
        ↓
3. Check routing table
        ↓
4. Find the destination network
        ↓
5. Check longest prefix match
        ↓
6. Check next hop / outgoing interface
        ↓
7. Check neighboring router
        ↓
8. Test with ping / traceroute
```

---

# 📚 19. Revision Questions

1. What is routing?
2. What is the main purpose of a router?
3. What is a routing table?
4. What does `C` mean in `show ip route`?
5. What does `L` mean in `show ip route`?
6. What is a connected route?
7. What is a local route?
8. Why is a local route normally `/32`?
9. What is Longest Prefix Match?
10. Which route wins: `/16` or `/24` when both match?
11. What is Administrative Distance?
12. Is a lower or higher AD preferred?
13. What is a routing metric?
14. What is a next hop?
15. What is an outgoing interface?
16. What is an IPv4 default route?
17. Which command displays the routing table?
18. How can you inspect the route selected for a specific destination?

---

# 🧠 20. CCNA Memory Sheet

```text
Routing
→ Process of selecting a path for packets

Router
→ Connects different IP networks
→ Makes Layer 3 forwarding decisions

Routing table
→ Contains routes used for forwarding

C
→ Connected route

L
→ Local route

Connected route
→ Directly connected network

Local route
→ Router's own interface IP
→ Usually /32

Route selection
1. Longest Prefix Match
2. Administrative Distance
3. Metric

Longest Prefix Match
→ Most specific matching prefix wins

AD
→ Lower is preferred

Connected AD
→ 0

Static AD
→ 1

EIGRP AD
→ 90

OSPF AD
→ 110

RIP AD
→ 120

Metric
→ Used by a routing protocol to select its best path

Default route
→ 0.0.0.0/0

Routing table command
→ show ip route
```

---

# 📈 21. Day 10 Reflection

## What I Learned

- What routing is
- What routers do
- Routing tables
- Connected routes
- Local routes
- Route selection
- Longest Prefix Match
- Administrative Distance
- Metrics
- Next hop
- Outgoing interface
- Default route concept

## What I Need to Practice

- Reading `show ip route`
- Identifying `C` and `L` routes
- Understanding `/32` local routes
- Performing Longest Prefix Match
- Understanding AD vs metric
- Following a packet through multiple routers
- Troubleshooting missing routes

---

# 🚀 Day 10 Status

**Completed ✅**

- [x] Routing fundamentals
- [x] Routing tables
- [x] Connected routes
- [x] Local routes
- [x] Route selection
- [x] Longest Prefix Match
- [x] Administrative Distance
- [x] Metrics
- [x] Next hop
- [x] Packet Tracer practice

---


