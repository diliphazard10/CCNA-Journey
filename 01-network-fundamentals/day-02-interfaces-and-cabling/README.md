# Day 02 — Network Interfaces, Ethernet & Cabling

## CCNA 200-301 v1.1

**Domain:** 1.0 Network Fundamentals  
**Day:** 02  
**Topics:** Network Interfaces, Ethernet, Copper Cabling, Fiber Optics, Bits & Bytes, Ethernet Standards  
**Lab Tool:** Cisco Packet Tracer

---

# 🎯 Learning Objectives

Today's study focused on understanding how network devices physically connect and communicate through network interfaces and transmission media.

By the end of Day 2, I aimed to understand:

- What a network interface is
- What an Ethernet interface does
- The difference between bits and bytes
- How data is transmitted over a network
- Copper Ethernet cabling
- Fiber optic cabling
- Single-mode fiber
- Multimode fiber
- Ethernet standards
- Speed and duplex
- Interface naming on Cisco devices
- Basic interface status
- The difference between physical and logical interfaces
- Basic Cisco interface verification commands

---

# 🧠 1. What Is a Network Interface?

A network interface is the connection point through which a device communicates with a network.

A network device can have multiple interfaces.

For example, a router may have:

```text
Router R1

G0/0
G0/1
G0/2

Each interface can connect the router to a different network or device.

Example:

LAN 1
  |
G0/0
 R1
G0/1
  |
LAN 2

Interfaces can be physical or logical.

🔌 2. Physical Interface

A physical interface represents an actual hardware connection.

Examples:

GigabitEthernet0/0
GigabitEthernet0/1
FastEthernet0/1

A physical Ethernet interface normally connects using an Ethernet cable.

Example:

PC ───── Ethernet Cable ───── Switch
🧩 3. Logical Interface

A logical interface does not necessarily represent a physical port.

Examples include:

Loopback interface
VLAN interface
Router subinterface

Example:

interface loopback0

Logical interfaces are created through configuration and can provide logical network functions without requiring a dedicated physical port.

⚡ 4. Bits and Bytes

A bit is the smallest unit of digital data.

A bit has two possible values:

0
1

A byte consists of 8 bits.

1 Byte = 8 bits

Examples:

8 bits = 1 byte
16 bits = 2 bytes
32 bits = 4 bytes
64 bits = 8 bytes

Networking speeds are normally expressed in bits per second.

Examples:

100 Mbps
1 Gbps
10 Gbps

Storage capacity is commonly expressed in bytes.

Examples:

1 GB
10 GB
100 GB
🌐 5. Ethernet

Ethernet is one of the most widely used technologies for local area networks.

Ethernet defines how devices communicate over a LAN.

Common Ethernet connections include:

PC → Switch
Server → Switch
Access Point → Switch
Switch → Router

Ethernet commonly uses twisted-pair copper cables or fiber optic media.

🔢 6. Ethernet Speeds

Common Ethernet speeds include:

10 Mbps
100 Mbps
1 Gbps
10 Gbps
40 Gbps
100 Gbps

The exact speed supported depends on:

Interface
Cable
Ethernet standard
Distance
Network hardware
🔗 7. Ethernet Interfaces

Cisco devices use interface names such as:

FastEthernet0/1
GigabitEthernet0/0
GigabitEthernet0/1

Common abbreviations:

Fa = FastEthernet
Gi = GigabitEthernet
Te = TenGigabitEthernet

Examples:

Fa0/1
Gi0/0
Gi0/1
Te0/1
🧵 8. Copper Ethernet Cable

Copper Ethernet cables use electrical signals to transmit data.

A common type is twisted-pair Ethernet cable.

Examples include:

Cat5e
Cat6
Cat6a

Copper Ethernet cables contain pairs of twisted copper wires.

The twisting helps reduce electromagnetic interference and crosstalk.

📡 9. Common Copper Ethernet Categories
Cat5e

Commonly used for Gigabit Ethernet.

Typical maximum channel/installation distance is around:

100 meters

Cat5e is widely used in LAN installations.

Cat6

Cat6 provides improved performance and reduced interference compared with older cable categories.

It can support:

1 Gbps

and can support higher speeds over shorter distances depending on the installation and standard.

Cat6a

Cat6a is designed for higher-performance Ethernet environments and is commonly associated with:

10 Gbps

up to approximately:

100 meters

under appropriate installation conditions.

🔄 10. Straight-Through and Crossover

Traditional Ethernet cabling used different cable wiring arrangements depending on the devices being connected.

Historically:

PC → Switch

used a straight-through cable.

And:

PC → PC
Switch → Switch

could require a crossover cable.

However, modern Ethernet interfaces commonly support:

Auto-MDI/MDIX

which allows interfaces to automatically detect the required pair configuration.

Therefore, in modern networks, the distinction is less operationally important than it once was.

💡 11. Fiber Optic Cable

Fiber optic cable transmits data using light instead of electrical signals.

Basic concept:

Electrical data
      ↓
Optical transmitter
      ↓
Light
      ↓
Fiber
      ↓
Optical receiver
      ↓
Electrical data

Advantages include:

Long transmission distances
High bandwidth
Resistance to electromagnetic interference
Useful for backbone connections
Useful between network buildings
🔦 12. Single-Mode Fiber

Single-mode fiber is designed to carry light over a single primary propagation mode.

It is commonly used for:

Long-distance links
ISP networks
WAN connections
Campus backbone
Data center interconnections

Single-mode fiber generally supports much longer distances than multimode fiber.

🔆 13. Multimode Fiber

Multimode fiber allows multiple propagation modes.

It is commonly used for shorter-distance applications such as:

Data centers
Building backbones
Campus networks
Server rooms

Multimode fiber is generally less suitable than single-mode fiber for very long-distance transmission.

🆚 14. Copper vs Fiber
Feature	Copper	Fiber
Signal	Electrical	Light
Common use	LAN access	Backbone/uplinks
EMI resistance	Lower	Very high
Distance	Usually shorter	Usually longer
Installation	Generally easier	Requires more specialized handling
Cost	Usually lower	Often higher
Weight	Heavier	Lighter
Electrical isolation	No	Yes
📏 15. Cable Distance

Distance is an important consideration when selecting transmission media.

Typical twisted-pair Ethernet deployments are designed around:

100 meters

for the structured cabling channel.

Fiber can support significantly longer distances depending on:

Fiber type
Transceiver
Ethernet standard
Optical budget
Data rate

Therefore, the correct question is not simply:

"Which cable is faster?"

The better question is:

"Which transmission medium and Ethernet standard are appropriate for this speed and distance?"

📜 16. Ethernet Standards

Ethernet standards are developed under IEEE 802.3.

Examples include:

10BASE-T
100BASE-TX
1000BASE-T
10GBASE-T
10BASE-T
10 Mbps
Baseband Ethernet
Twisted-pair copper
100BASE-TX

Also known as Fast Ethernet.

100 Mbps
Twisted-pair copper
1000BASE-T

Gigabit Ethernet over twisted-pair copper.

1 Gbps
Cat5e or better commonly used
10GBASE-T

10 Gigabit Ethernet over twisted-pair copper.

10 Gbps

It commonly uses Cat6a or suitable higher-performance cabling for full-distance deployment.

🔍 17. Understanding Ethernet Naming

Consider:

1000BASE-T

A simplified interpretation is:

1000 = 1000 Mbps
BASE = Baseband
T = Twisted-pair copper

Another example:

10GBASE-T

means:

10G = 10 Gigabit
BASE = Baseband
T = Twisted-pair
🔄 18. Speed and Duplex

An Ethernet interface can operate with different speed and duplex settings.

Examples:

Speed:
10 Mbps
100 Mbps
1000 Mbps


Duplex:
Half-duplex
Full-duplex

Modern switched Ethernet networks normally use:

Full-duplex

Full-duplex allows simultaneous transmission and reception.

⚠️ 19. Duplex Mismatch

A duplex mismatch can cause serious network performance problems.

Possible symptoms include:

Slow communication
Interface errors
Late collisions
Retransmissions
Poor network performance

A useful verification command is:

show interfaces
🖥️ 20. Cisco Interface Status

Cisco interfaces commonly show two important status values.

Example:

GigabitEthernet0/0
up
up

The first status generally represents the physical layer status.

The second represents the line protocol status.

The desired state is normally:

up
up
🔎 21. Cisco Interface Verification Commands

Commands practiced:

show ip interface brief

This provides a quick overview of interfaces, IP addresses and status.

show interfaces

This provides detailed information about an interface.

It can show:

Interface status
Hardware information
Speed
Duplex
Errors
Traffic statistics
MAC address
MTU
show interfaces status

On supported switches, this provides a concise overview of switch ports.

🧪 22. Packet Tracer Lab

The Day 2 lab focused on examining interfaces and different physical connection types.

Basic topology:

PC1 ───── SW1 ───── R1
          |
         PC2

The purpose was to identify:

Ethernet interfaces
Copper connections
Device interface names
Interface status
Basic Ethernet connectivity
🧪 23. Lab Verification

Commands used:

show ip interface brief

and:

show interfaces

The objective was to understand what information Cisco IOS provides about network interfaces.

🧠 Key Takeaways
A network interface is the connection point between a device and a network.
Physical interfaces correspond to hardware ports.
Logical interfaces are software-defined interfaces.
Ethernet is a major LAN networking technology.
Copper Ethernet uses electrical signals.
Fiber optic Ethernet uses light.
Single-mode fiber is generally used for longer distances.
Multimode fiber is generally used for shorter distances.
Network speeds are measured in bits per second.
One byte contains eight bits.
Ethernet standards are developed under IEEE 802.3.
Cable type, Ethernet standard, transceiver and distance all affect network design.
show ip interface brief is one of the most useful Cisco troubleshooting commands.
Interface status should be checked before troubleshooting higher-layer problems.
🔧 Troubleshooting Approach

When an Ethernet interface is not working, I should check:

Is the cable connected?
Is the correct interface being used?
Is the interface administratively enabled?
Is the interface physically up?
Is the line protocol up?
Is speed correct?
Is duplex correct?
Are there interface errors?
Is the IP configuration correct?
Is the problem physical, Layer 2, or Layer 3?
