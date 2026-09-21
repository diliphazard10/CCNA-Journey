# Day 13 — Subnetting Part 2 — Detailed Notes

## 1. Core Formulas

```text
IPv4 = 32 bits

Host bits = 32 - prefix length

Subnets = 2^borrowed bits

Total addresses = 2^host bits

Traditional usable hosts = 2^host bits - 2

Block size = 256 - interesting-octet mask value
```

The network address is the first address in a subnet. The broadcast address is the final address.

---

## 2. Classful Terminology

Historically:

| Class | Traditional Range | Default Prefix |
|---|---|---|
| A | 1–126 | /8 |
| B | 128–191 | /16 |
| C | 192–223 | /24 |

Modern networks use CIDR, so these classes do not determine the actual prefix.

For this lesson:

```text
Class C-style starting network → /24
Class B-style starting network → /16
```

---

# 3. Class C Subnetting

Start with:

```text
192.168.10.0/24
```

Mask:

```text
255.255.255.0
```

There are 8 host bits.

### /25

```text
Mask: 255.255.255.128
Host bits: 7
Total addresses: 128
Usable hosts: 126
Block size: 128
```

Networks:

```text
.0
.128
```

### /26

```text
Mask: 255.255.255.192
Host bits: 6
Total addresses: 64
Usable hosts: 62
Block size: 64
```

Networks:

```text
.0
.64
.128
.192
```

### /27

```text
Mask: 255.255.255.224
Host bits: 5
Total addresses: 32
Usable hosts: 30
Block size: 32
```

Networks:

```text
.0
.32
.64
.96
.128
.160
.192
.224
```

### /28

```text
Mask: 255.255.255.240
Host bits: 4
Total addresses: 16
Usable hosts: 14
Block size: 16
```

### /29

```text
Mask: 255.255.255.248
Host bits: 3
Total addresses: 8
Usable hosts: 6
Block size: 8
```

### /30

```text
Mask: 255.255.255.252
Host bits: 2
Total addresses: 4
Usable hosts: 2
Block size: 4
```

---

## 4. Class C Quick Reference

| Prefix | Mask | Host Bits | Total | Traditional Usable | Block |
|---|---|---:|---:|---:|---:|
| /25 | 255.255.255.128 | 7 | 128 | 126 | 128 |
| /26 | 255.255.255.192 | 6 | 64 | 62 | 64 |
| /27 | 255.255.255.224 | 5 | 32 | 30 | 32 |
| /28 | 255.255.255.240 | 4 | 16 | 14 | 16 |
| /29 | 255.255.255.248 | 3 | 8 | 6 | 8 |
| /30 | 255.255.255.252 | 2 | 4 | 2 | 4 |

---

# 5. Finding a Class C Subnet

Example:

```text
192.168.25.117/27
```

Mask:

```text
255.255.255.224
```

Block size:

```text
256 - 224 = 32
```

Subnet boundaries:

```text
0, 32, 64, 96, 128, ...
```

117 falls between 96 and 127.

Therefore:

```text
Network:   192.168.25.96
Broadcast: 192.168.25.127
Usable:    192.168.25.97 - 192.168.25.126
```

---

# 6. Moving to Class B

Start with:

```text
172.16.0.0/16
```

Default mask:

```text
255.255.0.0
```

Initially there are 16 host bits.

When the prefix becomes larger than `/16`, bits are borrowed from the third octet first.

---

# 7. /16 → /17

```text
Prefix: /17
Mask: 255.255.128.0
Block size: 128
```

Networks:

```text
172.16.0.0/17
172.16.128.0/17
```

Host bits:

```text
15
```

Traditional usable hosts:

```text
32766
```

---

# 8. /16 → /18

```text
Prefix: /18
Mask: 255.255.192.0
Block size: 64
```

Networks:

```text
172.16.0.0/18
172.16.64.0/18
172.16.128.0/18
172.16.192.0/18
```

Host bits:

```text
14
```

Traditional usable hosts:

```text
16382
```

---

# 9. /16 → /20

This is an important example.

```text
Prefix: /20
Mask: 255.255.240.0
```

Binary third octet:

```text
11110000
```

The third octet is the interesting octet.

Block size:

```text
256 - 240 = 16
```

Networks begin:

```text
172.16.0.0/20
172.16.16.0/20
172.16.32.0/20
172.16.48.0/20
172.16.64.0/20
172.16.80.0/20
...
```

Borrowed bits:

```text
20 - 16 = 4
```

Number of subnets:

```text
2^4 = 16
```

Host bits:

```text
32 - 20 = 12
```

Total addresses:

```text
2^12 = 4096
```

Traditional usable:

```text
4094
```

---

# 10. /20 Broadcast Example

Given:

```text
172.16.32.0/20
```

The next network is:

```text
172.16.48.0
```

Therefore:

```text
Broadcast = 172.16.47.255
```

Usable range:

```text
172.16.32.1 - 172.16.47.254
```

---

# 11. Other Class B Prefixes

### /21

```text
Mask: 255.255.248.0
Block size: 8
Borrowed bits: 5
Subnets from /16: 32
Host bits: 11
Traditional usable hosts: 2046
```

Networks:

```text
172.16.0.0
172.16.8.0
172.16.16.0
172.16.24.0
...
```

### /22

```text
Mask: 255.255.252.0
Block size: 4
Borrowed bits: 6
Subnets from /16: 64
Host bits: 10
Traditional usable hosts: 1022
```

Networks:

```text
172.16.0.0
172.16.4.0
172.16.8.0
172.16.12.0
...
```

### /23

```text
Mask: 255.255.254.0
Block size: 2
Borrowed bits: 7
Subnets from /16: 128
Host bits: 9
Traditional usable hosts: 510
```

Networks:

```text
172.16.0.0
172.16.2.0
172.16.4.0
172.16.6.0
...
```

---

# 12. Class B Quick Reference

Starting with `/16`:

| Prefix | Mask | Block Size | Subnets from /16 | Traditional Usable Hosts |
|---|---|---:|---:|---:|
| /17 | 255.255.128.0 | 128 | 2 | 32766 |
| /18 | 255.255.192.0 | 64 | 4 | 16382 |
| /19 | 255.255.224.0 | 32 | 8 | 8190 |
| /20 | 255.255.240.0 | 16 | 16 | 4094 |
| /21 | 255.255.248.0 | 8 | 32 | 2046 |
| /22 | 255.255.252.0 | 4 | 64 | 1022 |
| /23 | 255.255.254.0 | 2 | 128 | 510 |
| /24 | 255.255.255.0 | 1 | 256 | 254 |

---

# 13. Finding the Interesting Octet

Look at the mask.

Example:

```text
255.255.240.0
```

The third octet is neither 255 nor 0:

```text
255.255.240.0
       ^
```

Therefore it is the interesting octet.

For:

```text
255.255.255.192
```

the fourth octet is interesting.

---

# 14. Worked Class B Example

Find the subnet containing:

```text
172.20.77.100/20
```

Mask:

```text
255.255.240.0
```

Interesting octet:

```text
3rd
```

Block size:

```text
256 - 240 = 16
```

Third-octet boundaries:

```text
0, 16, 32, 48, 64, 80, 96, ...
```

77 falls in the 64–79 range.

Therefore:

```text
Network:   172.20.64.0
Broadcast: 172.20.79.255
Usable:    172.20.64.1 - 172.20.79.254
```

---

# 15. General Method

For any subnetting problem:

1. Identify the prefix.
2. Calculate host bits.
3. Convert prefix to mask if needed.
4. Find the interesting octet.
5. Calculate block size.
6. Find the network boundary containing the given IP.
7. Find the next network.
8. Broadcast = one address before the next network.
9. Usable range = network + 1 through broadcast - 1.

---

# 16. Common Mistakes

### Mistake 1

Looking only at the fourth octet.

With Class B subnetting, the third octet is often the interesting octet.

### Mistake 2

Using the mask value as the block size.

For:

```text
255.255.240.0
```

the block size is:

```text
256 - 240 = 16
```

### Mistake 3

Forgetting that the broadcast is before the next network.

### Mistake 4

Confusing `/20` with 20 host bits.

`/20` means:

```text
20 network bits
12 host bits
```

### Mistake 5

Treating Class A/B/C as the modern routing model.

CIDR is the modern model. Class terminology is mainly useful here as a learning framework.

---

# 17. Day 13 Memory Sheet

```text
IPv4 = 32 bits
Host bits = 32 - prefix
Subnets = 2^borrowed bits
Total addresses = 2^host bits
Traditional usable = 2^host bits - 2
Block size = 256 - interesting-octet mask value

Network = first address
Broadcast = last address
Usable = network + 1 through broadcast - 1
```

Class B-style `/16` masks:

```text
/17 = 255.255.128.0
/18 = 255.255.192.0
/19 = 255.255.224.0
/20 = 255.255.240.0
/21 = 255.255.248.0
/22 = 255.255.252.0
/23 = 255.255.254.0
/24 = 255.255.255.0
```

---

# 18. Self-Test

### Class C

1. Find the mask for `/28`.
2. Find the block size of `/28`.
3. How many usable hosts are in `/29`?
4. Find network and broadcast for `192.168.5.73/27`.
5. Find network and broadcast for `192.168.100.201/28`.

### Class B

6. Find the mask for `/20`.
7. Find the block size of `/20`.
8. How many `/20` subnets come from a `/16`?
9. Find network and broadcast for `172.16.77.50/20`.
10. Find network and broadcast for `172.20.130.10/22`.

### Answers

```text
1. 255.255.255.240
2. 16
3. 6
4. Network 192.168.5.64, Broadcast 192.168.5.95
5. Network 192.168.100.192, Broadcast 192.168.100.207
6. 255.255.240.0
7. 16
8. 16
9. Network 172.16.64.0, Broadcast 172.16.79.255
10. Network 172.20.128.0, Broadcast 172.20.131.255
```

---

# 19. Day 13 Summary

Today I moved from basic subnetting into more varied problems:

```text
Class C-style /24
      ↓
/25 /26 /27 /28 /29 /30
      ↓
Class B-style /16
      ↓
/17 /18 /19 /20 /21 /22 /23 /24
      ↓
Subnetting across the third octet
```

The most important skill is finding the **interesting octet**, calculating the **block size**, and identifying the **network, broadcast, and usable host range**.
