# OSPF and Dynamic Routing

## 1. Overview

Open Shortest Path First (OSPF) is used in this enterprise network to provide dynamic routing between Layer 3 devices.

The purpose of implementing OSPF is to allow the network infrastructure to dynamically discover routing information and maintain connectivity between different parts of the enterprise network.

The Layer 3 distribution switches participate in OSPF and establish neighbor relationships with other OSPF-enabled devices across the network.

This provides a scalable alternative to manually configuring static routes for every network.

---

## 2. OSPF Design

The enterprise network uses OSPF as its dynamic routing protocol.

The Layer 3 distribution switches operate as routing devices and participate in OSPF.

OSPF is used over the routed Layer 3 connections between network devices.

The VLAN interfaces provide the default gateways for the departmental networks, while OSPF is responsible for exchanging routing information between participating Layer 3 devices.

### Main routing components

| Component | Role |
|---|---|
| DIST1 | Layer 3 distribution switch participating in OSPF |
| DIST2 | Layer 3 distribution switch participating in OSPF |
| OSPF | Dynamic interior gateway routing protocol |
| VLAN SVIs | Default gateways for departmental VLANs |
| Routed interfaces | Layer 3 links used for routing between network devices |

---

## 3. OSPF Neighbor Formation

OSPF routers and Layer 3 switches must establish neighbor relationships before they can exchange link-state information.

```text
show ip ospf neighbor

The Packet Tracer IOS used in this lab did not accept:

show ospf neighbors

The accepted command was:

show ip ospf neighbor

This is an important troubleshooting observation because Cisco IOS syntax can vary between platforms and Packet Tracer device implementations.

4. DIST2 OSPF Neighbor Verification

The DIST2 device was checked using:

show ip ospf neighbor

The verification output showed multiple OSPF neighbors.

Observed neighbor states included:

FULL/DR
FULL/BDR

A FULL state indicates that the OSPF adjacency has reached a fully synchronized state.

The output observed on DIST2 included the following neighbor IDs:

Neighbor ID	State	Address	Interface
5.5.5.5	FULL/DR	10.10.10.22	GigabitEthernet0/1
2.2.2.2	FULL/DR	192.168.20.2	Vlan20
2.2.2.2	FULL/BDR	192.168.40.2	Vlan40
2.2.2.2	FULL/BDR	192.168.60.2	Vlan60
2.2.2.2	FULL/BDR	192.168.10.2	Vlan10
2.2.2.2	FULL/BDR	192.168.30.2	Vlan30
2.2.2.2	FULL/BDR	192.168.50.2	Vlan50
6.6.6.6	FULL/DR	10.10.10.13	GigabitEthernet0/2
2.2.2.2	FULL/DR	10.10.10.17	FastEthernet0/4

The exact neighbor relationships above are taken from the DIST2 verification output.
What the verification demonstrates

The presence of FULL OSPF relationships demonstrates that OSPF adjacency formation is occurring on DIST2.

The DR and BDR designations are part of OSPF's neighbor relationship process on multi-access network segments.

5. DIST1 OSPF Verification

DIST1 was also verified using:

show ip ospf neighbor

and:

show ip route

The corresponding verification screenshot is stored in the project screenshots directory.

The purpose of the DIST1 verification is to confirm that OSPF is operating from the second Layer 3 distribution switch and that its routing information can be reviewed independently from DIST2.

6. OSPF Routing Table Verification

The routing table was checked using:

show ip route

The command displays the routes currently known by the Layer 3 switch.

The routing table uses route codes to identify how routes were learned.

Important route codes include:

C  = Connected
S  = Static
O  = OSPF

For example:

C  192.168.10.0/24

means that the network is directly connected to the device.

An OSPF-learned route would normally appear with:

O

in the routing table.

7. DIST2 Routing Table Evidence

The DIST2 routing table verification showed the following directly connected networks:

10.10.10.12/30
10.10.10.16/30
10.10.10.20/30

192.168.10.0/24
192.168.20.0/24
192.168.30.0/24
192.168.40.0/24
192.168.50.0/24
192.168.60.0/24

The VLAN networks are directly connected through the Layer 3 SVI interfaces.

The verification output also showed: "Gateway of last resort is not set"

This means that no default route was present in the displayed DIST2 routing table at the time of verification.

8. Relationship Between VLANs and OSPF

The departmental VLANs provide logical network segmentation.

The current VLAN addressing plan is:

VLAN	Department	Network
10	Management	192.168.10.0/24
20	HR	192.168.20.0/24
30	Finance	192.168.30.0/24
40	Sales	192.168.40.0/24
50	IT	192.168.50.0/24
60	Guest	192.168.60.0/24
99	Server / Infrastructure	192.168.99.0/24

The Layer 3 distribution switches provide SVI interfaces for the departmental VLANs.

Because the switches operate at Layer 3, they can perform inter-VLAN routing locally.

OSPF operates separately as the dynamic routing protocol used to exchange routes between participating Layer 3 devices.

9. Routed Layer 3 Links

The Layer 3 switches also use routed interfaces for infrastructure connectivity.

The DIST2 verification showed these connected /30 networks:

10.10.10.12/30
10.10.10.16/30
10.10.10.20/30

These small point-to-point subnets are used for Layer 3 connectivity between network devices.

Using /30 addressing on point-to-point infrastructure links provides two usable IPv4 addresses per subnet.

10. OSPF Neighbor States

The following OSPF states are important when troubleshooting:

FULL

The neighbor relationship has completed the OSPF adjacency process and the devices have synchronized their link-state databases.

DR

DR stands for Designated Router.

On multi-access OSPF networks, the DR is selected to reduce the amount of adjacency and update traffic required between routers.

BDR

BDR stands for Backup Designated Router.

The BDR provides a backup role for the DR.

The verification output from DIST2 showed both:

FULL/DR

and:

FULL/BDR

This confirms that the OSPF process is forming established adjacencies.

11. OSPF Verification Commands

The following commands were used during the verification process:

Verify OSPF neighbors
show ip ospf neighbor
Verify the routing table
show ip route
Verify interface addressing and status
show ip interface brief

These commands provide complementary information:

show ip ospf neighbor verifies OSPF adjacency.
show ip route verifies routes installed in the routing table.
show ip interface brief verifies interface IP addresses and operational status.

12. Troubleshooting Observation

During OSPF verification, the following command was initially attempted:

show ospf neighbors

Packet Tracer returned:

% Invalid input detected at '^' marker.

The correct command supported by the device was:

show ip ospf neighbor

This demonstrates an important practical troubleshooting lesson:

When a command is rejected, verify the IOS command syntax and available command set before assuming that the routing protocol itself is malfunctioning.

Packet Tracer may also support a more limited command set than physical Cisco IOS devices.

13. Verification Evidence

The project includes screenshots documenting the OSPF verification process.

DIST1

Evidence:
SCREENSHOTS/SHOW-IP-OSPF-NEIGHBOR and SHOW-IP-ROUTE_DIST1.png

This screenshot documents the OSPF neighbor and routing-table verification performed on DIST1.

DIST2

Evidence:
SCREENSHOTS/SHOW-IP-OSPF-NEIGHBOR and SHOW-IP-ROUTE_DIST2.png

This screenshot documents the OSPF neighbor and routing-table verification performed on DIST2.

The screenshots are retained as evidence of the actual Packet Tracer lab state rather than relying only on configuration text.

14. Verification Summary

The OSPF verification produced the following results:

    Test                                Result

OSPF neighbor command	       Successful using "show ip ospf neighbor"
DIST2 OSPF neighbors	       Multiple neighbors observed
OSPF adjacency state	       FULL relationships observed
DR/BDR operation	           DR and BDR states observed
DIST2 routing table          Successfully displayed
Departmental VLAN networks	 Present as directly connected networks
Default route	               Not present on the displayed DIST2 routing table
DIST1 verification	         Performed and documented with screenshot

15. Important Design Note

The presence of a FULL OSPF neighbor relationship confirms that OSPF adjacency has been established.

However, an OSPF neighbor relationship by itself does not prove that every expected remote network has been installed as an OSPF route.

For that reason, routing-table verification is performed separately using:

show ip route

An expected dynamically learned network should be verified by looking for the appropriate OSPF route code:

O

This project documentation intentionally distinguishes between:

OSPF neighbor formation
OSPF route exchange
Routes actually installed in the routing table

This prevents the documentation from claiming successful route propagation without supporting evidence.

16. Key Lessons
Lesson 1 — Neighbor adjacency and route installation are different

Seeing:

FULL

means an OSPF adjacency is established.

It does not automatically mean that every expected route has been learned and installed.

Lesson 2 — Always verify the routing table

The command:

show ip route

is essential when troubleshooting dynamic routing.

It allows the administrator to determine whether routes are:

directly connected
statically configured
dynamically learned
or missing entirely.
Lesson 3 — Understand DR and BDR

OSPF uses a Designated Router and Backup Designated Router on appropriate multi-access segments.
The verification output showed both roles operating in the lab.check out screenshot folder for evidence.
