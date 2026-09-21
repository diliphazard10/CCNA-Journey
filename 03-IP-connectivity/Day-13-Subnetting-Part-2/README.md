# Day 13 — Subnetting Part 2

## CCNA 200-301 — IP Connectivity

Today I continued IPv4 subnetting practice, focusing on **Class C-style /24 networks** and **Class B-style /16 networks**.

> Class A/B/C terminology is historical. Modern IPv4 uses CIDR, but these terms are useful for learning subnetting.

## Topics Covered

- Class C subnetting practice
- /25, /26, /27, /28, /29, /30
- Network address and broadcast address
- Usable host range
- Block size
- Class B subnetting
- /16 networks
- /17 through /24
- Borrowing bits in the third octet
- Finding the interesting octet
- Subnetting practice

## Class C Example

Starting network:

```text
192.168.10.0/24
```

Subnetting to `/27` gives:

```text
192.168.10.0/27
192.168.10.32/27
192.168.10.64/27
192.168.10.96/27
192.168.10.128/27
192.168.10.160/27
192.168.10.192/27
192.168.10.224/27
```

A `/27` has 5 host bits, 32 total addresses, and 30 traditional usable host addresses.

## Class B Example

Starting network:

```text
172.16.0.0/16
```

Subnetting to `/20`:

```text
Mask:       255.255.240.0
Block size: 16
```

The networks begin:

```text
172.16.0.0/20
172.16.16.0/20
172.16.32.0/20
172.16.48.0/20
...
```

## Key Takeaways

- Find the prefix first.
- Find the interesting octet.
- Calculate block size with `256 - mask value`.
- The first address is the network address.
- The last address is the broadcast address.
- Subnetting a `/16` to `/20` creates 16 subnets.
- A `/20` has 12 host bits and 4094 traditional usable host addresses.

## Lab

The Packet Tracer lab contains both Class C and Class B subnetting exercises.

See `lab/README.md`.

## Revision Questions

1. What is the block size of `/27`?
2. How many `/27` subnets fit in a `/24`?
3. How many usable hosts are in `/27`?
4. What is the mask for `/20`?
5. What is the interesting octet in `255.255.240.0`?
6. What is the block size of `/20`?
7. How many `/20` subnets fit in a `/16`?
8. What is the broadcast of `172.16.32.0/20`?

## Progress

- [x] Practiced Class C-style subnetting
- [x] Practiced /25 through /30
- [x] Practiced block-size calculations
- [x] Learned Class B-style /16 subnetting
- [x] Practiced subnetting across the third octet
- [x] Completed Packet Tracer exercises

**Next:** Continue subnetting practice and improve calculation speed.
