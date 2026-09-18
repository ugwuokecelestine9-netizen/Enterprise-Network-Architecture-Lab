# NAT and PAT Configuration

## Objective

Configure Network Address Translation (NAT) and Port Address Translation (PAT) on the EDGE router so that internal enterprise networks can be translated through the router's outside interface.

## Internal Networks

The following internal networks were included in the NAT policy:

- VLAN 10 — 192.168.10.0/24
- VLAN 20 — 192.168.20.0/24
- VLAN 30 — 192.168.30.0/24
- VLAN 40 — 192.168.40.0/24
- VLAN 50 — 192.168.50.0/24
- VLAN 60 — 192.168.60.0/24
- VLAN 99 — 192.168.99.0/24

## NAT/PAT Implementation

NAT/PAT was implemented on the EDGE router.

### NAT Inside Interface

The interface connecting the EDGE router toward the internal firewall/network was configured as the NAT inside interface:

```cisco
interface gigabitEthernet0/0/0
 ip nat inside
