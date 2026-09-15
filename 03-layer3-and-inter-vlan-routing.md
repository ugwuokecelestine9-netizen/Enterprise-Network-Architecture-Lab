# Layer 3 & Inter-VLAN Routing

## 1. Overview

The enterprise network uses Layer 3 switching at the distribution layer to provide routing between VLANs.

Instead of sending internal VLAN traffic to an external router, the distribution switches perform inter-VLAN routing locally using Switch Virtual Interfaces (SVIs).

This design improves internal routing efficiency, reduces unnecessary traffic through the firewall or edge router, and provides a clear separation between Layer 2 access switching and Layer 3 routing.

---

## 2. Layer 3 Routing Architecture

The enterprise network follows a hierarchical design:

```text
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


Inter-VLAN routing allows devices located in different VLANs to communicate through Layer 3 routing.

For example, traffic from a device in the HR VLAN to a device in the Finance VLAN follows this general process:


HR Host
   |
   v
VLAN 20
   |
   v
HR SVI
192.168.20.2 / 192.168.20.3
   |
   v
Layer 3 Routing
   |
   v
Finance SVI
192.168.30.2 / 192.168.30.3
   |
   v
VLAN 30
   |
   v
Finance Host


