# DHCP and Dynamic IP Address Assignment

## Objective

The objective of this section is to configure and verify dynamic IPv4 address assignment for end devices across the VLAN-based enterprise network.

Lab 5 uses a centralized DHCP server to dynamically provide IP addresses, default gateways, and DNS information to client devices.

## DHCP Server

The dedicated DHCP server is configured as follows:

| Parameter | Address |
|---|---|
| DHCP Server | `192.168.99.10` |
| DNS Server | `192.168.99.11`|
| MAIL SERVER |`192.168.99.13` |
| WEB SERVER |`192.168.99.12`|
| FILE SERVER |`192.168.99.14`|

| VLAN 20 Gateway | `192.168.20.1` |

## DHCP Operation

The DHCP request follows this general path:

PC Client  
↓  
Access Switch  
↓  
Multilayer Switch  
↓  
DHCP Relay  
↓  
DHCP Server `192.168.99.10`

The multilayer switching infrastructure forwards DHCP requests from the client VLANs to the centralized DHCP server.

## Verification

DHCP functionality was verified from PC1 using:

```text
ipconfig /all

PC1 successfully received the following configuration:

IPv4 Address:     192.168.20.14
Subnet Mask:      255.255.255.0
Default Gateway:  192.168.20.1
DHCP Server:      192.168.99.10
DNS Server:       192.168.99.11
Investigation

The following command was checked on the Cisco network devices:

show ip dhcp pool

No DHCP pools were displayed on the following devices:

DISTRIBUTION-SW1
DIST2
CORE
LAGOS-ROUTER
ABUJA-ROUTER

This initially suggested that DHCP might not be configured on the network infrastructure.

Further investigation was performed on PC1 using:

ipconfig /all

The output identified the DHCP server as:

192.168.99.10

This confirmed that DHCP was being provided by a dedicated server rather than by an IOS DHCP pool on the Cisco routers or multilayer switches.

DHCP Verification Result

PC1 successfully obtained its IPv4 configuration dynamically.

DHCP Status: WORKING

The client received:

IP Address: 192.168.20.14
Default Gateway: 192.168.20.1
DHCP Server: 192.168.99.10
DNS Server: 192.168.99.11
Evidence
PC1 DHCP Configuration

The PC1 ipconfig /all output provides evidence that:

The PC is using DHCP.
The PC received a valid IPv4 address.
The correct VLAN 20 gateway was assigned.
The centralized DHCP server was identified.
The correct DNS server was assigned.
Conclusion

DHCP was successfully verified in Lab 5.

The network uses a centralized DHCP server at 192.168.99.10, while DNS services are provided by 192.168.99.11.

PC1 successfully received a dynamic address from the DHCP server, confirming that DHCP operation for VLAN 20 is functioning correctly.
