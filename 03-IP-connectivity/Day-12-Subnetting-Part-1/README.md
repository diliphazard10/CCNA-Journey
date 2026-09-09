# Day 12  — Subnetting Part 1

> **CCNA 200-301 · Network Layer · IP Connectivity**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-12-green)
![Topic](https://img.shields.io/badge/Topic-Subnetting%20Part 1-orange)

---


Today I studied the fundamentals of IPv4 subnetting, with a focus on **CIDR notation** and the **basic subnetting process**.

### Topics Covered
- IPv4 addressing review
- CIDR notation and prefix length
- Subnet masks
- Network bits vs. host bits
- Why subnetting is used
- Borrowing host bits
- Number of subnets
- Number of hosts per subnet
- Network address
- Broadcast address
- Usable host range
- Basic subnetting calculations

### What I Learned

CIDR represents an IPv4 network with a prefix length, for example:

```text
192.168.1.0/24
```

A `/24` means 24 network bits and 8 host bits.

Subnetting divides a larger network into smaller logical networks by borrowing bits from the host portion.

### Basic Subnetting Process

1. Identify the original prefix.
2. Determine the required number of subnets or hosts.
3. Determine how many host bits to borrow.
4. Calculate the new prefix.
5. Determine the subnet mask.
6. Calculate the block size.
7. Find network and broadcast addresses.
8. Determine the usable host range.

### Packet Tracer Lab

The lab divides `192.168.10.0/24` into four `/26` subnets and assigns an address from each subnet to a PC.

See `lab/README.md`.

### Key Takeaways

- IPv4 addresses contain 32 bits.
- `Host bits = 32 - prefix length`.
- Borrowing host bits creates smaller subnets.
- `2^borrowed_bits` gives the number of subnets.
- `2^host_bits` gives total addresses per subnet.
- Traditional usable hosts = `2^host_bits - 2`.
- The first address is the network address and the last is the broadcast address.

### Revision Questions

1. What does `/24` mean?
2. How many host bits are in `/26`?
3. How many `/26` subnets can be made from a `/24`?
4. How many usable hosts are in a `/26`?
5. What is the broadcast address of `192.168.1.64/26`?

### Progress

- [x] Learned CIDR
- [x] Understood network and host bits
- [x] Learned the basic subnetting process
- [x] Practiced basic subnet calculations
- [x] Completed a basic Packet Tracer subnetting lab

**Next:** Continue subnetting practice and improve calculation speed.
