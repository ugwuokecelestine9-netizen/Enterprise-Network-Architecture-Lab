# IP Addressing & VLANs

## 1. Overview

The enterprise network uses a structured IP addressing scheme and VLAN segmentation to separate departments, management traffic, guest traffic, and network infrastructure.

Each department is assigned its own VLAN and IP subnet. This provides logical separation between different parts of the organization while allowing controlled communication through the Layer 3 distribution layer.

The addressing plan uses private IPv4 address space with a /24 subnet for each major VLAN.

The VLANs implemented in the network are:

| VLAN | Name | Purpose | Network |
|------|------|---------|---------|
| 10 | Management | Network management | 192.168.10.0/24 |
| 20 | HR | Human Resources | 192.168.20.0/24 |
| 30 | Finance | Finance department | 192.168.30.0/24 |
| 40 | Sales | Sales department | 192.168.40.0/24 |
| 50 | IT | IT department | 192.168.50.0/24 |
| 60 | Guest | Guest network | 192.168.60.0/24 |
| 99 | Server/Infrastructure | Servers and network infrastructure | 192.168.99.0/24 |


