# Day 11 — Static Routing Notes

## Static Route

A static route is manually configured by a network administrator.

```text
ip route <destination-network> <subnet-mask> <next-hop-IP>
```

Example:

```text
R1(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

## Next-Hop Static Route

```text
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

The router uses `10.0.0.2` as the next hop.

## Exit-Interface Static Route

```text
ip route 192.168.2.0 255.255.255.0 GigabitEthernet0/1
```

The router sends traffic through the specified interface.

## Routing Table

Static routes appear as:

```text
S
```

Example:

```text
S 192.168.2.0/24 [1/0] via 10.0.0.2
```

Default static-route AD:

```text
1
```

## Default Route

IPv4 default route:

```text
0.0.0.0/0
```

Configuration:

```text
R1(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

Routing table:

```text
S* 0.0.0.0/0 [1/0] via 10.0.0.2
```

## Default Gateway

A host uses a default gateway to reach destinations outside its local subnet.

Remember:

```text
Host → default gateway
Router → default route
```

## Packet Tracer Lab

```text
PC1 ── R1 ── R2 ── PC2
```

Networks:

```text
PC1 LAN → 192.168.1.0/24
R1-R2   → 10.0.0.0/30
PC2 LAN → 192.168.2.0/24
```

R1:

```text
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

R2:

```text
ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

Test:

```text
ping 192.168.2.10
```

## Default Route Practice

```text
R1(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

Verify:

```text
show ip route
```

## Verification Commands

```text
show ip route
show ip route static
show ip route <destination-network>
show ip interface brief
ping <destination-IP>
traceroute <destination-IP>
```

## Troubleshooting

```text
Check interface
      ↓
Check IP address
      ↓
Check routing table
      ↓
Check static route
      ↓
Check next hop
      ↓
Check return route
      ↓
Ping
      ↓
Traceroute
```

## Quick Memory

```text
S   = Static
S*  = Static candidate default

Static AD = 1

Default route = 0.0.0.0/0

Host → default gateway
Router → default route

Configure → ip route
Verify    → show ip route
```

### Main Takeaway

> Static routing lets an administrator manually define a path to a destination. A default route provides a fallback path when no more specific route exists, while a default gateway is the router a host uses to reach destinations outside its local subnet.
