# Enterprise-Network-Architecture-Lab
# Enterprise Network Architecture Lab

A secure and resilient enterprise network infrastructure designed and implemented in Cisco Packet Tracer.

This project simulates a multi-department enterprise environment with VLAN segmentation, Layer 3 switching, inter-VLAN routing, HSRP redundancy, centralized network services, ACL-based security, DHCP Snooping, STP, firewall protection, and edge routing.

---

## 📌 Project Overview

The objective of this project was to design, configure, secure, troubleshoot, and validate an enterprise network infrastructure.

The network was built to simulate real-world enterprise requirements including:

- Departmental network segmentation
- Inter-VLAN communication
- Gateway redundancy
- Centralized DHCP and DNS services
- Internal web services
- Network access control
- Firewall security
- Layer 3 routing
- Access-layer protection
- End-to-end connectivity

---

## 🏗️ Network Architecture

The network follows a hierarchical enterprise design:

```text
                    WAN / INTERNET
                         |
                    EDGE ROUTER
                         |
                    FIREWALL / ASA
                         |
                     CORE L3
                         |
              +----------+----------+
              |                     |
            DIST1                 DIST2
              |                     |
        ACCESS SWITCHES       ACCESS SWITCHES
              |                     |
             PCs                   PCs

                         |
                    SERVER VLAN
                         |
              +----------+----------+
              |          |          |
             DHCP       DNS        WEB



          | VLAN | Department / Purpose     | Network     
| ---- | ------------------------ | --------------- |
| 10   | Management               | 192.168.10.0/24 |
| 20   | HR                       | 192.168.20.0/24 |
| 30   | Finance                  | 192.168.30.0/24 |
| 40   | Sales                    | 192.168.40.0/24 |
| 50   | IT                       | 192.168.50.0/24 |
| 60   | Guest                    | 192.168.60.0/24 |
| 99   | Servers / Infrastructure | 192.168.99.0/24 |

| Service     | IP Address    |
| ----------- | ------------- |
| DHCP Server | 192.168.99.10 |
| DNS Server  | 192.168.99.11 |
| Web Server  | 192.168.99.12 |

      |SECURITY FEATURES|
1.Extended ACLs
2.Departmental traffic restrictions
3.DHCP Snooping
4.Spanning Tree Protocol
5.Firewall / ASA
6.Controlled access to server infrastructure
7.Service-specific traffic permissions

           |HIGH AVAILABILITY|
HSRP was implemented at the distribution layer to provide gateway redundancy.
The design allows clients to continue using a virtual gateway even when the active distribution device changes.

       | ROUTING |
The network incorporates:

1.Inter-VLAN routing
2.Layer 3 routed links
3.Static routing
4.HSRP
5.Core-to-firewall routing
6.Firewall-to-edge routing

        | TESTING AND VERIFICATION |
The completed network was tested progressively from the end devices toward the network edge.

Testing included:

PC IP configuration
DHCP assignment
Default gateway reachability
Inter-VLAN connectivity
DNS connectivity
Web server access
ACL enforcement
Server reachability
Distribution-layer routing
Core connectivity
Firewall interfaces and routing
Edge-router connectivity
End-to-end network verification

         | TROUBLESHOOTING |

This project was not built without failures.

During development, several issues were encountered, including:

DHCP failures
ACL configuration issues[unable to attach]
Routing problems
HSRP state changes frequently
ICMP testing producing misleading results when ACLs were permitting specific application services

Each issue was investigated using a structured troubleshooting process:

Identify the symptom
        ↓
Collect information
        ↓
Test connectivity
        ↓
Check configuration
        ↓
Identify root cause
        ↓
Apply corrective action
        ↓
Retest
        ↓
Document the result


    [ DOCUMENTATION ]

Detailed documentation for this project is available in the docs/ directory.

Documentation will cover:

Project Overview
Network Topology
IP Addressing
VLAN Design
Routing
HSRP
Network Services
ACL Security
Firewall
Troubleshooting
Final Testing

         [ SKILL DEMOSTRATED ]
This project demonstrates practical experience with:

Cisco IOS configuration
VLANs
Inter-VLAN routing
Layer 3 switching
HSRP
Static routing
DHCP
DNS
HTTP
Extended ACLs
DHCP Snooping
STP
Cisco ASA firewall
Network troubleshooting
Connectivity testing
Enterprise network design

                    [ KEY LESSON ]

The most important part of this project was not simply getting the network to work.It was learning how to troubleshoot when it didn't.

The project followed a continuous cycle of : Design → Configure → Test → Troubleshoot → Fix → Retest → Document


                   [


