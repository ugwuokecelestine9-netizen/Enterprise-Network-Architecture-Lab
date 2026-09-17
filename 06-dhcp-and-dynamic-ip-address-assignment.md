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
