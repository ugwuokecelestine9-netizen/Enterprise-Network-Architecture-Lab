# IP Addressing and VLAN Design

## Overview

The enterprise network uses VLAN segmentation to separate departments, improve security, reduce broadcast domains, and provide a structured IP addressing scheme.

Each department is assigned a dedicated VLAN and IP subnet. Layer 3 switching provides inter-VLAN routing, while HSRP provides redundant default-gateway services.

---

## VLAN Structure

| VLAN | Name | Purpose |
|------|------|---------|
| 10 | Management | Network/device management |
| 20 | HR | Human Resources users |
| 30 | Finance | Finance department users |
| 40 | Sales | Sales department users |
| 50 | IT | IT and administrative users |
| 60 | Guest | Guest network access |
| 99 | Server/Infrastructure | Servers and infrastructure services |

---

## IP Addressing Scheme

The network uses private IPv4 addressing with a /24 subnet for each major VLAN.

| VLAN | Network Address | Subnet Mask | Purpose |
|------|-----------------|-------------|---------|
| 10 | 192.168.10.0/24 | 255.255.255.0 | Management |
| 20 | 192.168.20.0/24 | 255.255.255.0 | HR |
| 30 | 192.168.30.0/24 | 255.255.255.0 | Finance |
| 40 | 192.168.40.0/24 | 255.255.255.0 | Sales |
| 50 | 192.168.50.0/24 | 255.255.255.0 | IT |
| 60 | 192.168.60.0/24 | 255.255.255.0 | Guest |
| 99 | 192.168.99.0/24 | 255.255.255.0 | Server/Infrastructure |

---

## Default Gateway and HSRP

The distribution layer provides the Layer 3 gateway for the VLANs.

HSRP is used to provide gateway redundancy between the distribution switches.

For VLAN 20:

- HSRP Virtual IP: `192.168.20.1`
- DIST2 address: `192.168.20.3`

For the Server/Infrastructure VLAN:

- HSRP Virtual IP: `192.168.99.1`
- DIST1 address: `192.168.99.2`
- DIST2 address: `192.168.99.3`

The HSRP virtual address is used by hosts as their default gateway, allowing gateway availability to continue if one distribution switch becomes unavailable.

---

## Server Addressing

The Server/Infrastructure VLAN uses VLAN 99.

| Device | IP Address | Role |
|--------|------------|------|
| HSRP Virtual Gateway | 192.168.99.1 | Default gateway |
| DIST1 | 192.168.99.2 | Distribution switch |
| DIST2 | 192.168.99.3 | Distribution switch |
| DHCP Server | 192.168.99.10 | DHCP services |
| DNS Server | 192.168.99.11 | DNS services |
| Web Server | 192.168.99.12 | HTTP/Web services |

---

## VLAN Design Objectives

The VLAN structure was designed to provide:

- Departmental network segmentation
- Smaller broadcast domains
- Logical separation of users
- Controlled inter-VLAN communication
- Centralized server access
- Improved network security
- Easier troubleshooting and administration
- Support for ACL-based access control

---

## DHCP

DHCP is used to dynamically assign IP addresses to client devices.

DHCP pools were configured for the user VLANs, including:

- VLAN 10 — Management
- VLAN 20 — HR
- VLAN 30 — Finance

The centralized DHCP server is located in VLAN 99 at:

`192.168.99.10`

Reserved/excluded addresses are used where necessary to prevent DHCP from assigning addresses that are required for network infrastructure.

---

## Design Summary

The addressing scheme follows a simple and predictable structure:

`VLAN number → corresponding IP subnet`

For example:

- VLAN 20 → `192.168.20.0/24`
- VLAN 30 → `192.168.30.0/24`
- VLAN 40 → `192.168.40.0/24`
- VLAN 99 → `192.168.99.0/24`

This makes the network easier to understand, administer, troubleshoot, and scale.

---

## Validation

Connectivity was tested between the distribution switches and the infrastructure services.

Examples of successful tests included:

```text
DIST2# ping 192.168.99.10
Success rate is 100 percent (5/5)

DIST2# ping 192.168.99.12
Success rate is 100 percent (5/5)
