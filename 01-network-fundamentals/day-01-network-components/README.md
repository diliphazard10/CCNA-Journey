# Day 01 — Network Components & Basic Network

## CCNA 200-301 v1.1

**Domain:** 1.0 Network Fundamentals  
**Topic:** Network Components  
**Study Day:** 01  
**Lab Tool:** Cisco Packet Tracer

---

## 🎯 Objectives

Today's objectives were:

- Understand common network components
- Understand the role of routers
- Understand the role of Layer 2 switches
- Understand the basic concept of Layer 3 switching
- Understand endpoints and servers
- Understand Access Points
- Understand firewalls
- Understand IPS
- Build a basic Cisco network in Packet Tracer
- Build a simple topology
---

What is a network ?
-A computer network is a digital communication network which allows nodes to share resources.

Nodes
    -Router
    -PC
    -Laptop
    -Server
    -Phones
    -etc.


  Client
    -A client is a device that access a services made available by the server.
  Server
    - A server is a device that provides functions or services for clients.

    
## 🧠 Network Components/Devices

  # Switches
      -It has many network interfaces /ports for end hosts to connect to (usually 24+)
      -Provides connectivity to hosts within the same network (LAN)
      -Do not provides connectivity between LANs /over the internet
      -Important cisco switches series are cisco catalyst 2960 , catalyst 3560/3850, catalyst 9200/9300 series 

  # Router
      -Router have fewer network interfaces than switch
      -Are used to provide connectivity between LANs
      -Are therefore used to send data over the internet.
      -Popular Router series are ISR 1000, ISR900 ,ISR 4000, etc.

  # Firewall
      -Monitor and control network traffic based on configured rules or policy.
      -Can be placed inside the network or outside the network.
      -Next Generation Firewalls include more modern and advanced filtering capabilities.
      -Some common firewalls are ASA 5500-x , Firepower 2100, etc.
      -Network Firewalls
        -Are hardware devices that filters traffic between networks.
      -Host-based Firewalls
        - Are software application that filters traffic entering and exiting a host machine like pc, laptop.

 

---

## 🔀 Switch vs Router

### Layer 2 Switch

A Layer 2 switch primarily uses MAC addresses to forward Ethernet frames.

Example:

PC1 → Switch → PC2

The switch learns which MAC address is reachable through which port.

### Router

A router connects different IP networks and makes forwarding decisions using IP addresses and its routing table.

Example:

LAN 1 → Router → LAN 2




---

## 🌐 Basic Network Topology

The lab topology was:

London Branch                                      Tokyo Branch
           
PC1 ── SW1── R1 ── FW1 ── The Internet ── R2── FW2 ── SW2 ── SRV1
        │                         │                    │
       PC2                        │                   SRV2
                              Attacker
