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

     / SHOW EVIDENCE/
The following verification screenshots are stored in the SCREENSHOTS directory:

DIST1-SHOW-VLAN-BRIEF.png
DIST2-SHOW-VLAN-BRIEF.png
DIST1-show-ip-interface-brief.png
DIST2-show-ip-interface-brief.png
These screenshots provide evidence of the VLAN configuration and Layer 3 SVI status on the distribution switches.
Additional ping verification screenshots will be added when final inter-VLAN connectivity testing is completed.

   VLAN 99 – Server / Infrastructure

VLAN 99 is reserved for server and infrastructure services.
Its network is:
192.168.99.0/24
The Layer 3 gateway configuration for VLAN 99 is intentionally left for separate verification.
This is important because the server/infrastructure VLAN is associated with infrastructure services and gateway redundancy.
The final VLAN 99 gateway and HSRP state will be documented after verification.


    DESIGN BENEFIT:

The Layer 3 design provides:

Efficient inter-VLAN routing
Local routing at the distribution layer
Reduced dependency on external routers for internal communication
Clear separation of Layer 2 and Layer 3 functions
Improved scalability
Better fault isolation
Support for redundant distribution-layer gateway design
A structured path toward the core, firewall and external network


         /THE VLANS MUST HAVE;/

A functioning enterprise network requires more than simply creating VLANs.
The VLANs must have:
1.Correct Layer 2 configuration
2.Correct Layer 3 SVIs
3.Correct gateway addressing
4.Correct routing
5.Correct upstream connectivity
6.Proper verification

The troubleshooting process demonstrated the importance of verifying each layer individually before moving to the next stage

   /KEY LESSON/
A functioning enterprise network requires more than simply creating VLANs.
