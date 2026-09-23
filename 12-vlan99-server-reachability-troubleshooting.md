# VLAN 99 Server Reachability Troubleshooting

## 1. Overview

During final network verification, communication between the Server VLAN (VLAN 99) and the distribution switches was not working correctly.

DHCP was successfully operating, and the server devices were reachable within VLAN 99, but communication with the distribution switches required further troubleshooting.

The investigation focused on VLAN 99 connectivity, routing, ARP, and the physical trunk connection.

---

## 2. VLAN 99 Addressing

| Device | VLAN 99 IP Address |
|---|---|
| SERVER-SWITCH | 192.168.99.1/24 |
| DIST1 | 192.168.99.2/24 |
| DIST2 | 192.168.99.3/24 |
| DHCP Server | 192.168.99.10/24 |
| DNS Server | 192.168.99.11/24 |
| Web Server | 192.168.99.12/24 |

Network:

```text
192.168.99.0/24

3. Initial Symptoms

The following behavior was observed:

DHCP was working successfully.
Servers within VLAN 99 were reachable.
SERVER-SWITCH could reach DIST1.
SERVER-SWITCH could not initially reach DIST2 at 192.168.99.3.
VLAN 99 interfaces were operational.
ARP information showed VLAN 99 devices.
The physical connection between DIST1 and SERVER-SWITCH was investigated.
4. Physical Connectivity Verification

CDP was used to verify the actual physical connections.

The output confirmed:

DIST1 Fa0/5 <----> SERVER-SWITCH Fa0/6

The interfaces were configured as an 802.1Q trunk carrying VLAN 99.

DIST1 Fa0/5
     |
     | 802.1Q Trunk
     | VLAN 99
     |
SERVER-SWITCH Fa0/6

This confirmed that VLAN 99 had a Layer 2 path between the distribution and server switches.

5. VLAN 99 Verification

SERVER-SWITCH was checked with:

show ip interface brief

VLAN 99 was operational:

Vlan99    192.168.99.1    up    up

ARP information also showed the VLAN 99 devices:

192.168.99.2    ARPA    Vlan99
192.168.99.3    ARPA    Vlan99
192.168.99.10   ARPA    Vlan99

This confirmed that the devices were visible on VLAN 99.

6. Routing Table Investigation

The routing table on SERVER-SWITCH was examined.

The following routes were initially present:

C 192.168.99.0/24 is directly connected, Vlan99

S 192.168.99.3/32 [1/0] via 10.10.10.18

The /32 static route was unnecessary because 192.168.99.3 already belonged to the directly connected VLAN 99 network.

The /32 route was more specific than the /24 connected route and therefore affected route selection for traffic destined specifically for 192.168.99.3.

7.            Root Cause

The root cause was an unnecessary static host route:

192.168.99.3/32 via 10.10.10.18

Instead of allowing traffic to reach 192.168.99.3 directly through VLAN 99, the static host route directed the traffic toward the routed 10.10.10.18 path.

This conflicted with the intended VLAN 99 Layer 2 design.

8. Corrective Action

The incorrect static route was removed:

enable
configure terminal
no ip route 192.168.99.3 255.255.255.255 10.10.10.18
end

The routing table was checked again:

show ip route 192.168.99.0

The specific /32 route was no longer present.

The network was now using:

C 192.168.99.0/24 is directly connected, Vlan99
9. Final Verification

Connectivity to DIST2 was tested:

ping 192.168.99.3

        Result:

Success rate is 100 percent

This confirmed that SERVER-SWITCH could successfully communicate with DIST2 through VLAN 99.

        10. Additional Cleanup

Another unnecessary static host route was identified:

192.168.99.2/32 via 10.10.10.9

Because DIST1 is also directly connected to VLAN 99, this route is unnecessary.

         It can be removed with:

"enable
configure terminal
no ip route 192.168.99.2 255.255.255.255 10.10.10.9
end"

After removal, VLAN 99 should rely on its directly connected network:

C 192.168.99.0/24 is directly connected, Vlan99

VLAN 99 communication was successfully restored.

The troubleshooting demonstrated the importance of verifying Layer 2 connectivity, ARP, and routing decisions when diagnosing inter-device communication problems.

                          Lessons Learned
Check the real connection first. CDP showed that DIST1 Fa0/5 was connected to SERVER-SWITCH, not DIST2 as the old description suggested.
Check routing when a VLAN is working but one device cannot be reached. The VLAN and trunk were fine; the problem was the routing table.
The /32 route was the problem. 192.168.99.3/32 was sending traffic through 10.10.10.18 instead of directly through VLAN 99.
Remove unnecessary static routes. Devices already on the same VLAN should communicate directly through that VLAN.
Test after every change. Removing the bad route immediately gave us 100% ping success to 192.168.99.3
