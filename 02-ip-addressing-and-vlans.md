# IP Addressing & VLANs

## 1. Overview

The enterprise network uses a structured IP addressing scheme and VLAN segmentation to separate departments, management traffic, guest traffic, and network infrastructure.

Each department is assigned its own VLAN and IP subnet. This provides logical separation between different parts of the organization while allowing controlled communication through the Layer 3 distribution layer.

The addressing plan uses private IPv4 address space with a /24 subnet for each major VLAN.

## 2. VLAN Addressing Plan

Each department is assigned a dedicated VLAN and IPv4 subnet using a /24 prefix.

The Layer 3 distribution switches provide SVI interfaces for the user VLANs. The SVI addressing follows a consistent scheme, with DIST1 using the `.2` address and DIST2 using the `.3` address within each VLAN subnet.

| VLAN | Name | Network | DIST1 SVI | DIST2 SVI |
|------|------|---------|-----------|-----------|
| 10 | Management | 192.168.10.0/24 | 192.168.10.2 | 192.168.10.3 |
| 20 | HR | 192.168.20.0/24 | 192.168.20.2 | 192.168.20.3 |
| 30 | Finance | 192.168.30.0/24 | 192.168.30.2 | 192.168.30.3 |
| 40 | Sales | 192.168.40.0/24 | 192.168.40.2 | 192.168.40.3 |
| 50 | IT | 192.168.50.0/24 | 192.168.50.2 | 192.168.50.3 |
| 60 | Guest | 192.168.60.0/24 | 192.168.60.2 | 192.168.60.3 |
| 99 | Server / Infrastructure | 192.168.99.0/24 | To be verified | To be verified |

The SVI verification confirmed that VLANs 10 through 60 are operational on both distribution switches.

The VLAN 99 SVI configuration is documented separately because its current state requires additional verification of the server/infrastructure gateway and HSRP configuration.


# IP Addressing and VLANs

## 1. Overview

The enterprise network uses VLAN segmentation to logically separate departments and infrastructure services.

Each major department is assigned a dedicated VLAN and IPv4 subnet. This provides logical separation, improves security, reduces broadcast domains, and creates a structured addressing scheme.

Layer 3 distribution switches provide the default gateways for the user VLANs through Switch Virtual Interfaces (SVIs).

The addressing scheme uses a consistent /24 subnet for each VLAN.

---

## 2. VLAN Addressing Plan

Each department is assigned a dedicated VLAN and IPv4 subnet using a /24 prefix.

The Layer 3 distribution switches provide SVI interfaces for the user VLANs.

A consistent addressing scheme is used:

- DIST1 uses the `.2` address within each VLAN subnet.
- DIST2 uses the `.3` address within each VLAN subnet.

| VLAN | Name | Network | DIST1 SVI | DIST2 SVI |
|---:|---|---|---|---|
| 10 | Management | 192.168.10.0/24 | 192.168.10.2 | 192.168.10.3 |
| 20 | HR | 192.168.20.0/24 | 192.168.20.2 | 192.168.20.3 |
| 30 | Finance | 192.168.30.0/24 | 192.168.30.2 | 192.168.30.3 |
| 40 | Sales | 192.168.40.0/24 | 192.168.40.2 | 192.168.40.3 |
| 50 | IT | 192.168.50.0/24 | 192.168.50.2 | 192.168.50.3 |
| 60 | Guest | 192.168.60.0/24 | 192.168.60.2 | 192.168.60.3 |
| 99 | Server / Infrastructure | 192.168.99.0/24 | To be verified | To be verified |

---

## 3. VLAN Roles

### VLAN 10 – Management

Used for network and device management.

Management traffic is logically separated from normal departmental user traffic.

### VLAN 20 – HR

Used for Human Resources users.

Access to other departmental VLANs is restricted according to the network security policy.

### VLAN 30 – Finance

Used for Finance users.

Access to other departmental VLANs is restricted according to the network security policy.

### VLAN 40 – Sales

Used for Sales users.

Access to other departmental VLANs is restricted according to the network security policy.

### VLAN 50 – IT

Used for IT and administrative users.

This VLAN is intended to have broader administrative access across the enterprise network.

### VLAN 60 – Guest

Used to isolate guest devices from internal departmental networks.

### VLAN 99 – Server / Infrastructure

Dedicated to infrastructure services and servers.

This VLAN is treated separately from the normal user VLANs and requires additional verification of its Layer 3 gateway and redundancy configuration.

---

## 4. Layer 3 SVI Design

The distribution switches perform Layer 3 gateway functions for the user VLANs.

Each VLAN requiring Layer 3 connectivity is represented by an SVI on the distribution switches.

For the user VLANs:

- DIST1 provides the `.2` SVI address.
- DIST2 provides the `.3` SVI address.

This design allows inter-VLAN routing to occur at the distribution layer rather than requiring internal traffic to travel through an external router.

---

## 5. Verification

The VLAN configuration was verified using:

```text
show vlan brief
