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


NAT Outside Interface

The intended outside interface was configured as:

interface gigabitEthernet0/0/1
 ip nat outside
NAT ACL

An ACL was created to identify the internal networks:

access-list 1 permit 192.168.10.0 0.0.0.255
access-list 1 permit 192.168.20.0 0.0.0.255
access-list 1 permit 192.168.30.0 0.0.0.255
access-list 1 permit 192.168.40.0 0.0.0.255
access-list 1 permit 192.168.50.0 0.0.0.255
access-list 1 permit 192.168.60.0 0.0.0.255
access-list 1 permit 192.168.99.0 0.0.0.255
PAT Configuration

PAT was configured using interface overload:

ip nat inside source list 1 interface gigabitEthernet0/0/1 overload

The overload keyword enables multiple internal hosts to share the address of the outside interface using different port numbers.

VERIFICATION:

The NAT configuration was verified with:

show ip nat translations
show ip nat statistics

The NAT statistics confirmed:

Outside Interfaces: GigabitEthernet0/0/1
Inside Interfaces: GigabitEthernet0/0/0
Total translations: 0
Hits: 0
Misses: 0
Packet Tracer Limitation

The ASA used in this Packet Tracer lab did not accept the expected ASA NAT commands such as:

object network
nat (inside,outside)

The ASA returned:

% Invalid input detected

and:

% Unrecognized command

Therefore, NAT/PAT was implemented on the EDGE router instead.

LAB SCOPE

This lab does not include an external ISP/WAN router. Therefore, live NAT translations were not generated.

The NAT/PAT configuration itself was successfully accepted and verified on the EDGE router.

CONCLUSION

NAT/PAT configuration was completed on the EDGE router. The configuration identifies the internal enterprise networks, marks the inside/outside interfaces, and enables PAT using interface overload.
