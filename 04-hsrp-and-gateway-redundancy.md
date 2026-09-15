# HSRP & Gateway Redundancy

## 1. Overview

Hot Standby Router Protocol (HSRP) is used to provide redundant default gateways for the enterprise VLANs.

HSRP allows two distribution switches to share a virtual IP address that acts as the default gateway for hosts within a VLAN.

If the active distribution switch becomes unavailable, the standby distribution switch can take over the gateway function.

---

## 2. HSRP Design

The enterprise network uses HSRP between DIST1 and DIST2.

The design uses:

- DIST1 as an HSRP participant
- DIST2 as an HSRP participant
- A shared virtual IP address for each VLAN
- HSRP active/standby roles
- HSRP preemption
- Configured HSRP priority

The virtual gateway uses the `.1` address within each VLAN subnet.

---

## 3. HSRP Virtual Gateway Addressing

| VLAN | Network | HSRP Virtual IP |
|---:|---|---|
| 10 | 192.168.10.0/24 | 192.168.10.1 |
| 20 | 192.168.20.0/24 | 192.168.20.1 |
| 30 | 192.168.30.0/24 | 192.168.30.1 |
| 40 | 192.168.40.0/24 | 192.168.40.1 |
| 50 | 192.168.50.0/24 | 192.168.50.1 |
| 60 | 192.168.60.0/24 | 192.168.60.1 |
| 99 | 192.168.99.0/24 | To be verified |

---

## 4. HSRP Verification

HSRP status was verified on both distribution switches using:

```text
show standby


The command was used to verify:

HSRP state
Virtual IP address
Active router
Standby router
HSRP priority
Preemption status
HSRP timers
5. Observed HSRP Operation

The verification showed that HSRP is operating between DIST1 and DIST2.

The active gateway role is distributed across the VLANs rather than relying on a single distribution switch.

For example:

VLAN 10 — DIST1 is Active
VLAN 20 — DIST2 is Active
VLAN 30 — DIST1 is Active
VLAN 40 — DIST2 is Active

This provides gateway redundancy while also allowing both distribution switches to participate in forwarding.

6. HSRP Priority and Preemption

HSRP priority is configured to influence which distribution switch becomes Active for a VLAN.

Preemption is enabled.

This allows a higher-priority router to regain the Active role after recovering from a failure, according to the configured HSRP behavior.

The verified HSRP output shows a configured priority of 120 on the observed DIST1 groups.

7. Gateway Redundancy

The HSRP virtual IP is presented to end devices as the default gateway.

For example:

VLAN 10
Network:        192.168.10.0/24
DIST1 SVI:      192.168.10.2
DIST2 SVI:      192.168.10.3
HSRP Gateway:   192.168.10.1

Hosts therefore use the HSRP virtual address rather than depending directly on the physical SVI address of a single distribution switch.

8. Verification Evidence

HSRP verification screenshots are stored in the SCREENSHOTS directory.

Evidence includes:

DIST1 HSRP verification — first page
DIST1 HSRP verification — second page
DIST2 HSRP verification — first page
DIST2 HSRP verification — second page

These screenshots provide evidence of the HSRP state, virtual gateway addresses, active/standby relationships, priority and preemption configuration.

9. VLAN 99

VLAN 99 is the Server / Infrastructure VLAN.

Its network is:

192.168.99.0/24

The HSRP gateway for VLAN 99 will be documented after the server/infrastructure gateway configuration has been fully verified.

10. Key Design Benefits

HSRP provides:

Default gateway redundancy
Improved network availability
Automatic gateway failover
Reduced dependency on a single distribution switch
Better resilience at the distribution layer
Support for redundant enterprise network design
11. Key Lesson

Gateway redundancy is important in an enterprise network because a single distribution switch failure should not automatically remove the default gateway for an entire VLAN.

HSRP provides a shared virtual gateway while allowing multiple distribution switches to participate in gateway availability.
