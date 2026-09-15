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

