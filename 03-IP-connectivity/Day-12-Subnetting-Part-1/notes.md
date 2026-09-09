# Day 12 — Subnetting Part 1 — Detailed Notes

## 1. IPv4 Review

An IPv4 address contains **32 bits**, normally written as four 8-bit octets.

Example:

```text
192.168.1.10
```

The address has a network portion and a host portion. The prefix length tells us where the network portion ends.

---

## 2. CIDR

CIDR stands for **Classless Inter-Domain Routing**.

Example:

```text
192.168.1.0/24
```

`/24` means:

```text
24 network bits
8 host bits
```

because:

```text
32 - 24 = 8
```

The equivalent mask is:

```text
255.255.255.0
```

Binary:

```text
11111111.11111111.11111111.00000000
```

`1` = network bit  
`0` = host bit

---

## 3. Common Prefixes

| Prefix | Subnet Mask | Host Bits |
|---|---|---:|
| /8 | 255.0.0.0 | 24 |
| /16 | 255.255.0.0 | 16 |
| /24 | 255.255.255.0 | 8 |
| /25 | 255.255.255.128 | 7 |
| /26 | 255.255.255.192 | 6 |
| /27 | 255.255.255.224 | 5 |
| /28 | 255.255.255.240 | 4 |
| /29 | 255.255.255.248 | 3 |
| /30 | 255.255.255.252 | 2 |

Remember:

```text
Network bits + Host bits = 32
```

---

## 4. Why Subnet?

Subnetting divides one larger network into smaller networks.

Benefits:
- Better address organization
- Smaller broadcast domains
- More efficient addressing
- Easier network management
- Logical separation of network segments

Example:

```text
192.168.1.0/24
```

can be divided into:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

---

## 5. Borrowing Host Bits

Start with:

```text
192.168.1.0/24
```

The last octet has 8 host bits:

```text
00000000
```

Borrow 2 bits:

```text
11 000000
```

Now the prefix becomes:

```text
/24 + 2 = /26
```

There are 6 host bits remaining.

---

## 6. Number of Subnets

If `n` bits are borrowed:

```text
Number of subnets = 2^n
```

Examples:

```text
Borrow 1 bit → 2 subnets
Borrow 2 bits → 4 subnets
Borrow 3 bits → 8 subnets
Borrow 4 bits → 16 subnets
```

---

## 7. Number of Hosts

If `h` host bits remain:

```text
Total addresses = 2^h
```

For traditional IPv4 subnet calculations:

```text
Usable hosts = 2^h - 2
```

Example for `/26`:

```text
Host bits = 32 - 26 = 6

Total = 2^6 = 64

Usable = 64 - 2 = 62
```

The two reserved addresses are the network and broadcast addresses.

---

## 8. Basic /24 → /26 Example

Given:

```text
192.168.1.0/24
```

Need 4 subnets.

### Step 1 — Borrow bits

```text
2^2 = 4
```

Borrow 2 bits.

### Step 2 — New prefix

```text
/24 + 2 = /26
```

### Step 3 — Mask

```text
255.255.255.192
```

### Step 4 — Block size

```text
256 - 192 = 64
```

So subnet addresses increase by 64.

### Result

| Subnet | Network | Usable Range | Broadcast |
|---|---|---|---|
| 1 | 192.168.1.0/26 | .1–.62 | .63 |
| 2 | 192.168.1.64/26 | .65–.126 | .127 |
| 3 | 192.168.1.128/26 | .129–.190 | .191 |
| 4 | 192.168.1.192/26 | .193–.254 | .255 |

Each subnet has:

```text
64 total addresses
62 usable hosts
```

---

## 9. Network Address

The network address identifies the subnet.

Example:

```text
192.168.1.64/26
```

Network address:

```text
192.168.1.64
```

It is not normally assigned to a host.

---

## 10. Broadcast Address

The broadcast address is the final address in a subnet.

For:

```text
192.168.1.64/26
```

the next subnet starts at:

```text
192.168.1.128
```

Therefore the broadcast is:

```text
192.168.1.127
```

---

## 11. Usable Host Range

The usable range is:

```text
Network + 1
through
Broadcast - 1
```

For `192.168.1.64/26`:

```text
Network:   192.168.1.64
First host:192.168.1.65
Last host: 192.168.1.126
Broadcast: 192.168.1.127
```

---

## 12. Basic Subnetting Workflow

Use this order when solving problems:

1. Identify the original network.
2. Identify required subnets/hosts.
3. Determine borrowed bits.
4. Calculate the new prefix.
5. Determine the subnet mask.
6. Calculate block size.
7. List network addresses.
8. Find broadcast and usable ranges.

---

## 13. Block Size

For the relevant octet:

```text
Block size = 256 - mask value
```

Examples:

```text
/25 → 256 - 128 = 128
/26 → 256 - 192 = 64
/27 → 256 - 224 = 32
/28 → 256 - 240 = 16
/29 → 256 - 248 = 8
/30 → 256 - 252 = 4
```

---

## 14. Common Masks

```text
/24 = 255.255.255.0
/25 = 255.255.255.128
/26 = 255.255.255.192
/27 = 255.255.255.224
/28 = 255.255.255.240
/29 = 255.255.255.248
/30 = 255.255.255.252
```

---

## 15. Packet Tracer Practice

Use:

```text
192.168.10.0/24
```

Divide it into four `/26` subnets.

Topology:

```text
PC1 ── SW1
PC2 ── SW1
PC3 ── SW1
PC4 ── SW1
```

Suggested addresses:

```text
PC1: 192.168.10.10/26
PC2: 192.168.10.70/26
PC3: 192.168.10.130/26
PC4: 192.168.10.200/26
```

These belong to four different subnets.

There is no router in this lab, so PCs in different subnets should not successfully communicate. This demonstrates why Layer 3 routing is needed between different IP networks.

---

## 16. Verification

On a Packet Tracer PC:

```text
ipconfig
ping <destination-ip>
```

Useful Cisco IOS commands:

```text
show ip interface brief
show running-config
show interfaces
```

Example interface configuration:

```text
enable
configure terminal
interface gigabitEthernet 0/0
ip address 192.168.10.1 255.255.255.192
no shutdown
end
```

---

## 17. Common Mistakes

### Mistake 1
Confusing prefix length with host bits.

```text
/26 = 26 network bits + 6 host bits
```

### Mistake 2
Forgetting the network address.

The first address is reserved as the network identifier.

### Mistake 3
Forgetting the broadcast address.

The final address is the broadcast address.

### Mistake 4
Using the wrong block size.

For `/26`:

```text
256 - 192 = 64
```

So the networks increment by 64.

### Mistake 5
Assuming every address can be assigned to a host.

Traditional IPv4 subnetting reserves the network and broadcast addresses.

---

## 18. CCNA Memory Sheet

```text
IPv4 = 32 bits

Host bits = 32 - prefix length

Subnets = 2^borrowed bits

Total addresses = 2^host bits

Traditional usable hosts = 2^host bits - 2

Block size = 256 - interesting-octet mask value

Network = first address

Broadcast = last address

Usable range = network + 1 through broadcast - 1
```

---

## 19. Self-Test

### Q1
How many host bits does `/26` have?

```text
32 - 26 = 6
```

### Q2
How many total addresses are in `/26`?

```text
2^6 = 64
```

### Q3
How many traditional usable hosts?

```text
64 - 2 = 62
```

### Q4
What is the block size of `/27`?

```text
255.255.255.224
256 - 224 = 32
```

### Q5
What is the broadcast address of `192.168.1.128/26`?

The next subnet is `.192`, so:

```text
Broadcast = 192.168.1.191
```

---

## 20. Day 12 Summary

Subnetting divides a larger IPv4 network into smaller networks by borrowing bits from the host portion.

The core concepts learned today are:

```text
CIDR
Prefix length
Network bits
Host bits
Borrowed bits
Subnet mask
Block size
Network address
Broadcast address
Usable host range
```

The goal is to understand the process rather than memorize isolated numbers.
