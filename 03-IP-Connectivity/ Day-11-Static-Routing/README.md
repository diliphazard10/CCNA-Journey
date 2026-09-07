# Day 11 — Static Routing

> **CCNA 200-301 · IP Connectivity · Static Routing**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-11-green)
![Topic](https://img.shields.io/badge/Topic-Static%20Routing-orange)

---

## 📌 Day 11 Overview

Today I learned how to manually tell a router where to send traffic using **static routes**.

### Topics Covered
- Static routes
- Static route configuration
- Next-hop and exit-interface routes
- Default gateway
- Default route concept
- Default route configuration
- Verification and troubleshooting

## 🎯 Learning Objectives

By the end of Day 11, I should be able to:
- Explain what a static route is.
- Configure an IPv4 static route.
- Understand next-hop and exit-interface static routes.
- Explain the difference between a default gateway and a default route.
- Configure an IPv4 default route.
- Verify and troubleshoot static routes.

---

## 🛣️ 1. What Is a Static Route?

A **static route** is a route manually configured by a network administrator.

```text
ip route <destination-network> <subnet-mask> <next-hop-IP>
```

Example:

```text
R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

This tells R1:

```text
To reach 192.168.2.0/24
→ send the packet toward 10.0.0.2
```

---

## 🔧 2. Static Route Configuration

Cisco IOS syntax:

```text
ip route <destination-network> <subnet-mask> <next-hop-IP>
```

Example:

```text
R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

Breakdown:

```text
ip route
→ create a static route

192.168.2.0
→ destination network

255.255.255.0
→ destination subnet mask

10.0.0.2
→ next-hop IP
```

---

## ➡️ 3. Next-Hop Static Route

A next-hop static route specifies the IP address of the next router.

```text
R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

Topology:

```text
LAN 1        R1          R2        LAN 2
192.168.1.0/24 ── 10.0.0.1 ── 10.0.0.2 ── 192.168.2.0/24
```

---

## 🔌 4. Exit-Interface Static Route

A static route can specify the outgoing interface.

```text
R1(config)# ip route 192.168.2.0 255.255.255.0 GigabitEthernet0/1
```

For CCNA, understand both:

```text
Next-hop static route
Exit-interface static route
```

---

## 🧭 5. Static Routes in the Routing Table

Verify with:

```text
show ip route
```

A static route is normally shown with:

```text
S
```

Example:

```text
S 192.168.2.0/24 [1/0] via 10.0.0.2
```

The default Administrative Distance of an IPv4 static route is:

```text
1
```

---

## 🌎 6. Default Route Concept

A **default route** is used when no more specific route matches a destination.

IPv4 default route:

```text
0.0.0.0/0
```

Think:

```text
Specific route found?
        ↓
       YES → use it

       NO
        ↓
Use default route
```

---

## ⚙️ 7. Configure an IPv4 Default Route

Cisco IOS:

```text
ip route 0.0.0.0 0.0.0.0 <next-hop-IP>
```

Example:

```text
R1(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

Routing table:

```text
S* 0.0.0.0/0 [1/0] via 10.0.0.2
```

The `*` indicates a candidate default route.

---

## 🏠 8. Default Gateway

A **default gateway** is the router or Layer 3 device a host sends traffic to when the destination is outside its local subnet.

Example:

```text
PC1
IP:      192.168.1.10
Mask:    255.255.255.0
Gateway: 192.168.1.1
```

For a remote destination such as `192.168.2.20`, PC1 sends the frame toward:

```text
Default gateway → 192.168.1.1
```

---

## 🔄 9. Default Gateway vs Default Route

| Concept | Used By | Purpose |
|---|---|---|
| Default gateway | Host | Where to send traffic for remote networks |
| Default route | Router | Where to forward traffic when no specific route exists |

Remember:

```text
Host → default gateway
Router → default route
```

---

## 🧪 10. Packet Tracer Lab

Topology:

```text
PC1 ── R1 ── R2 ── PC2
```

Example networks:

```text
PC1 LAN → 192.168.1.0/24
R1-R2   → 10.0.0.0/30
PC2 LAN → 192.168.2.0/24
```

R1:

```text
R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

R2:

```text
R2(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

Test:

```text
PC1> ping 192.168.2.10
```

---

## 🧪 11. Default Route Lab

Practice a default route:

```text
R1(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

Verify:

```text
R1# show ip route
```

Look for:

```text
S* 0.0.0.0/0
```

---

## 🔍 12. Verification Commands

```text
show ip route
show ip route static
show ip route 192.168.2.0
show ip interface brief
ping <destination-IP>
traceroute <destination-IP>
```

---

## 🛠️ 13. Troubleshooting Flow

```text
1. Check interface status
        ↓
2. Check IP addressing
        ↓
3. Check routing table
        ↓
4. Check static route
        ↓
5. Check next hop
        ↓
6. Check return route
        ↓
7. Ping
        ↓
8. Traceroute
```

Important:

> A working route in one direction does not guarantee that return traffic has a route back.

---

## ⚠️ 14. Common Mistakes

- Wrong destination network
- Wrong subnet mask
- Wrong next-hop address
- Interface is down
- Forgetting the return route
- Confusing default gateway with default route

---

## 🧠 15. CCNA Memory Sheet

```text
Static route
→ Manually configured route

Static route command
→ ip route <network> <mask> <next-hop>

Static route code
→ S

Static route default AD
→ 1

Default route
→ 0.0.0.0/0

Default route command
→ ip route 0.0.0.0 0.0.0.0 <next-hop>

Default route code
→ S*

Default gateway
→ Host's path to remote networks

Router default route
→ Router's fallback route

Verification
→ show ip route
→ show ip route static
```

---

## 📚 16. Revision Questions

1. What is a static route?
2. Why would an administrator use a static route?
3. What command creates a static IPv4 route?
4. What does `S` mean in the routing table?
5. What is the default AD of a static route?
6. What is a next-hop static route?
7. What is an exit-interface static route?
8. What is an IPv4 default route?
9. What command configures an IPv4 default route?
10. What does `S*` mean?
11. What is a default gateway?
12. What is the difference between a default gateway and a default route?
13. Why is a return route important?
14. Which command displays the routing table?
15. How would you troubleshoot a static route that is not working?

---

## 📈 17. Day 11 Reflection

### What I Learned
- Static routes
- Static route configuration
- Default gateway
- Default route concept
- Default route configuration
- Verification and troubleshooting

### What I Need to Practice
- Writing `ip route` commands without looking them up
- Reading `S` and `S*` routes
- Configuring routes in both directions
- Understanding next-hop vs exit-interface routes
- Distinguishing default gateway from default route

---

## 🚀 Day 11 Status

**Completed ✅**

- [x] Static routing
- [x] Static route configuration
- [x] Next-hop static routes
- [x] Exit-interface static routes
- [x] Default gateway
- [x] Default route concept
- [x] Default route configuration
- [x] Verification
- [x] Packet Tracer practice

---



