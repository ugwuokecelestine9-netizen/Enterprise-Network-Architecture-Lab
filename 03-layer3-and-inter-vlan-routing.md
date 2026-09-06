# Layer 3 Switching and Inter-VLAN Routing

## Overview

The enterprise network uses multilayer switches to provide Layer 3 routing between VLANs.

Instead of relying on a separate router for every VLAN, the distribution switches perform routing using Switch Virtual Interfaces (SVIs).

This design provides efficient inter-VLAN communication while keeping the network scalable and easier to manage.

---

## Layer 3 Distribution

The distribution layer consists of multilayer Cisco switches operating at Layer 3.

The switches provide:

- VLAN gateway functions
- Inter-VLAN routing
- Routing between internal network segments
- HSRP gateway redundancy
- Connectivity toward the rest of the enterprise network

---

## Switch Virtual Interfaces (SVIs)

Each VLAN requiring Layer 3 connectivity is represented by an SVI on the distribution layer.

An SVI provides the default gateway for devices within its VLAN.

For example:

```text
VLAN 20
192.168.20.0/24
        |
        v
Layer 3 SVI
        |
        v
Inter-VLAN Routing



       [ ROUTING DESIGN ]
THE OVERALL TRAFFIC FLOW FOLLOWS THE ENTERPRISE HIERRARCHY

Access Layer
     |
     v
Distribution Layer
     |
     v
Core / Routing Layer
     |
     v
Firewall
     |
     v
Edge Router / External Network


Verification

Inter-VLAN and Layer 3 connectivity were tested using ICMP ping tests.

Connectivity was also tested between the distribution switches and infrastructure services in VLAN 99.

Successful examples included:

DIST2# ping 192.168.99.10
Success rate is 100 percent (5/5)

DIST2# ping 192.168.99.12
Success rate is 100 percent (5/5)

The testing process was also used to identify connectivity problems during the implementation and troubleshooting stages.


Key Design Benefits

The Layer 3 design provides:

Efficient inter-VLAN routing
Reduced dependency on external routers for internal VLAN communication
Better scalability
Clear separation between Layer 2 and Layer 3 functions
Improved fault isolation
Support for redundant default gateways through HSRP
Key Lesson

A major lesson from this implementation was that successful Layer 3 connectivity depends on more than simply creating VLANs.

The VLANs, SVIs, IP addressing, routing paths, gateway configuration, and security policies must all work together.

Testing each layer individually made troubleshooting much easier
