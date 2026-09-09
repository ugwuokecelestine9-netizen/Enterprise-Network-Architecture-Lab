# Layer 3 & Inter-VLAN Routing

## 1. Overview
# Layer 3 & Inter-VLAN Routing

## 1. Overview

The enterprise network uses multilayer Cisco switches to provide Layer 3 connectivity between the different VLANs.

Instead of relying on an external router for every VLAN, the distribution switches perform inter-VLAN routing using Switch Virtual Interfaces (SVIs).

This design allows devices in different VLANs to communicate through the Layer 3 distribution layer while maintaining logical network segmentation.

The Layer 3 design also provides a foundation for redundancy, dynamic routing, security policies, and connectivity to the rest of the enterprise network.


## 2. Layer 3 Distribution

The distribution layer is responsible for providing Layer 3 services within the enterprise network.

The design uses Cisco multilayer switches at the distribution layer. These switches perform routing functions in addition to traditional Layer 2 switching.

The distribution layer provides:

- Inter-VLAN routing
- Default gateway services for VLANs
- Routing between internal network segments
- Connectivity toward the core/routing layer
- Redundant gateway functionality using HSRP
- A central point for applying Layer 3 network policies

### Role of the Distribution Switches

The distribution switches act as the Layer 3 boundary between the access layer and the rest of the enterprise network.

User devices connect to access switches at Layer 2. Traffic destined for another VLAN is forwarded to the appropriate SVI on the distribution switch, where the Layer 3 routing decision is made.

This approach reduces the need to send internal VLAN-to-VLAN traffic through external routers and provides a more scalable enterprise design.

## 3. Switch Virtual Interfaces (SVIs)## 2. Layer 3 Distribution

## 3. Switch Virtual Interfaces (SVIs)

Switch Virtual Interfaces (SVIs) are used on the multilayer distribution switches to provide Layer 3 gateways for the VLANs.

Each SVI represents a VLAN at Layer 3 and provides the default gateway through which devices in that VLAN can communicate with other networks.

The enterprise network uses SVIs for the following VLANs:

| VLAN | Department / Purpose | Network |
|------|----------------------|---------|
| VLAN 10 | Management | 192.168.10.0/24 |
| VLAN 20 | HR | 192.168.20.0/24 |
| VLAN 30 | Finance | 192.168.30.0/24 |
| VLAN 40 | Sales | 192.168.40.0/24 |
| VLAN 50 | IT | 192.168.50.0/24 |
| VLAN 60 | Guest | 192.168.60.0/24 |
| VLAN 99 | Server / Infrastructure | 192.168.99.0/24 |

### SVI Function

For example, a device in VLAN 20 uses the VLAN 20 SVI as its default gateway.

```text
HR Device
   |
   | VLAN 20
   v
Access Switch
   |
   v
Distribution Switch
   |
   | SVI - VLAN 20
   v
Layer 3 Routing


## 4. SVI Addressing## 3. Switch Virtual Interfaces (SVIs)

Switch Virtual Interfaces (SVIs) are used on the multilayer distribution switches to provide Layer 3 gateways for the VLANs.

Each SVI represents a VLAN at Layer 3 and provides the default gateway through which devices in that VLAN can communicate with other networks.

The enterprise network uses SVIs for the following VLANs:

| VLAN | Department / Purpose | Network |
|------|----------------------|---------|
| VLAN 10 | Management | 192.168.10.0/24 |
| VLAN 20 | HR | 192.168.20.0/24 |
| VLAN 30 | Finance | 192.168.30.0/24 |
| VLAN 40 | Sales | 192.168.40.0/24 |
| VLAN 50 | IT | 192.168.50.0/24 |
| VLAN 60 | Guest | 192.168.60.0/24 |
| VLAN 99 | Server / Infrastructure | 192.168.99.0/24 |

### SVI Function

For example, a device in VLAN 20 uses the VLAN 20 SVI as its default gateway.

```text
HR Device
   |
   | VLAN 20
   v
Access Switch
   |
   v
Distribution Switch
   |
   | SVI - VLAN 20
   v
Layer 3 Routing



## 5. Inter-VLAN Routing


## 5. Inter-VLAN Routing

Inter-VLAN routing allows devices located in different VLANs and IP subnets to communicate.

In this enterprise design, inter-VLAN routing is performed by the multilayer distribution switches using SVIs.

Traffic does not remain within the Layer 2 VLAN when the destination is located on a different subnet. Instead, the source device sends the packet to its default gateway, which is provided by the appropriate SVI.

### Example Traffic Flow

Consider a device in the HR department communicating with a device in the Finance department:

```text
HR PC
192.168.20.x
   |
   | VLAN 20
   v
Access Switch
   |
   v
Distribution Switch
   |
   | SVI / Layer 3 Routing
   |
   v
VLAN 30
   |
   v
Finance PC
192.168.30.x

 ## 6. Layer 3 Routed Links

The enterprise network uses dedicated Layer 3 routed links between selected network devices.

Unlike a traditional switchport, a routed interface does not belong to a VLAN. The interface operates directly at Layer 3 and is assigned an IP address from a point-to-point subnet.

This design was used to establish Layer 3 connectivity between the core, distribution, and other routing infrastructure.

### Routed Interface Design

The Layer 3 links follow a point-to-point addressing model.

```text
Layer 3 Device A
      |
      | Routed Link
      | /30 subnet
      |
Layer 3 Device B




## 8. HSRP and Default Gateway Redundancy

## 9. Verification & Testing

## 10. Troubleshooting

## 11. Key Design Benefits

## 12. Key Lessons Learned
