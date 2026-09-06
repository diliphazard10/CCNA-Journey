# Day 10 — Routing Fundamentals Notes

## 1. What Is Routing?

Routing is the process of determining where packets should be forwarded to reach a destination network.

```text
Source
  ↓
Router
  ↓
Destination
```

Routing is mainly a Layer 3 function.

---

## 2. Router

A router:

- Connects different IP networks.
- Examines destination IP addresses.
- Uses a routing table.
- Selects the best route.
- Forwards packets toward the destination.

---

## 3. Routing Table

Command:

```text
show ip route
```

Example:

```text
C    192.168.1.0/24 is directly connected
L    192.168.1.1/32 is directly connected
```

A route may contain:

```text
Destination prefix
Route source
Administrative distance
Metric
Next hop
Outgoing interface
```

---

## 4. Connected Route

Created when a router interface has an IP address and is operational.

Example:

```text
C 192.168.1.0/24 is directly connected, GigabitEthernet0/0
```

`C` = Connected.

Meaning:

```text
192.168.1.0/24
→ directly connected network
```

---

## 5. Local Route

Represents the router's own interface IP.

Example:

```text
L 192.168.1.1/32 is directly connected, GigabitEthernet0/0
```

`L` = Local.

`/32` means one exact IPv4 address.

Remember:

```text
C → network connected to me
L → exact IP belongs to me
```

---

## 6. Route Selection

The important concepts are:

```text
1. Longest Prefix Match
2. Administrative Distance
3. Metric
```

---

## 7. Longest Prefix Match

The most specific matching route wins.

Example:

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```

Destination:

```text
10.10.10.50
```

Winner:

```text
10.10.10.0/24
```

Because:

```text
/24 > /16 > /8
```

---

## 8. Administrative Distance

AD = Administrative Distance.

It compares the trustworthiness of different routing sources when they provide the same destination prefix.

Lower is better.

Common Cisco values:

```text
Connected = 0
Static    = 1
EIGRP     = 90
OSPF      = 110
RIP       = 120
```

Example:

```text
OSPF = 110
RIP  = 120
```

OSPF wins because:

```text
110 < 120
```

---

## 9. Metric

A metric is used by a routing protocol to select the best path among routes learned through that protocol.

Examples:

```text
OSPF  → Cost
RIP   → Hop count
EIGRP → Composite metric
```

Important:

```text
AD ≠ Metric
```

AD compares routing sources.

Metric compares paths within a routing protocol.

---

## 10. Next Hop

Example:

```text
Destination: 192.168.3.0/24
Next Hop:    10.0.0.2
```

The router forwards the packet toward:

```text
10.0.0.2
```

---

## 11. Outgoing Interface

Example:

```text
C 192.168.1.0/24 is directly connected, GigabitEthernet0/0
```

The packet leaves through:

```text
GigabitEthernet0/0
```

---

## 12. Default Route

IPv4 default route:

```text
0.0.0.0/0
```

It is used when no more specific route matches.

```text
Specific route?
    ↓
   Yes → use it

   No
    ↓
Default route
```

---

## 13. Important Cisco Commands

```text
show ip route
show ip route connected
show ip route local
show ip route <destination>
show ip interface brief
ping <destination-IP>
traceroute <destination-IP>
```

---

## 14. Packet Tracer Lab

Topology:

```text
PC1 ── R1 ── R2 ── PC2
```

Tasks:

1. Configure router interfaces.
2. Configure IP addresses.
3. Verify interface status.
4. Run `show ip route`.
5. Identify `C` routes.
6. Identify `L` routes.
7. Test connectivity.
8. Analyze route selection.

---

## 15. Route Selection Practice

Routes:

```text
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```

Destination:

```text
10.10.10.50
```

Selected route:

```text
10.10.10.0/24
```

Reason:

```text
Longest Prefix Match
```

---

## 16. Troubleshooting Flow

```text
Check interface
      ↓
Check IP address
      ↓
Check routing table
      ↓
Check destination route
      ↓
Check longest prefix
      ↓
Check next hop
      ↓
Ping
      ↓
Traceroute
```

---

## 17. Quick Memory

```text
C = Connected
L = Local

Connected
→ Directly connected network

Local
→ Router's own IP
→ /32

Longest Prefix Match
→ Most specific route wins

AD
→ Lower is better

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
→ Best path within a routing protocol

Default route
→ 0.0.0.0/0

Routing table
→ show ip route
```

---

# 🎯 Main Takeaway

> **A router uses its routing table to decide where to forward packets. When multiple routes match a destination, the most specific route wins through Longest Prefix Match. If the same destination prefix is learned from different routing sources, Administrative Distance helps select the preferred source, and the routing protocol's metric helps select the best path within that protocol.**
