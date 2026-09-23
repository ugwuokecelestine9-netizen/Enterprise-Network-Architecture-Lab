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

Test Results
Destination	Purpose	Result
192.168.20.1	VLAN 20 HSRP Gateway	Successful
192.168.99.10	DHCP Server	Successful
192.168.99.11	DNS Server	Successful
192.168.99.12	Web Server	Successful

These tests confirmed that the client could communicate with its local gateway and reach the required infrastructure services across VLANs.

<img width="727" height="869" alt="12-5-Show-cdp-neighbors show-ip-interface-brief" src="https://github.com/user-attachments/assets/90829804-126f-4ca8-8679-ffb416ad4b3c" />
<img width="727" height="869" alt="12-4-show-arp show-ip-route-192 168 99 0 ping-192 168 99 3" src="https://github.com/user-attachments/assets/3834c608-0a1d-41e3-92d6-213f30cf9941" />
