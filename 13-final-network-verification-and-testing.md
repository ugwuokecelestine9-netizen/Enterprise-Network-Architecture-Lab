## Final End-to-End Test

The final end-to-end test was performed from a client PC in VLAN 20 to confirm that the complete network path was working correctly.

The test verified communication between the client, its HSRP gateway, and the infrastructure servers in VLAN 99.

### Client Information

The test PC received its network configuration through DHCP:

- **Client VLAN:** VLAN 20 (HR)
- **Client IP:** 192.168.20.x
- **Default Gateway:** 192.168.20.1
- **DHCP Server:** 192.168.99.10
- **DNS Server:** 192.168.99.11

### Connectivity Tests

The following destinations were tested from the client PC:

```text
ping 192.168.20.1
ping 192.168.99.10
ping 192.168.99.11
ping 192.168.99.12

