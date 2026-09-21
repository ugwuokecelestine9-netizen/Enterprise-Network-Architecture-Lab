# 10 — DHCP Snooping

## Objective

Implement DHCP Snooping at the access layer to protect the enterprise network against unauthorized or rogue DHCP servers.

DHCP Snooping allows the switch to distinguish between trusted and untrusted DHCP paths and prevents DHCP server responses from unauthorized ports.

---

## DHCP Snooping Configuration

DHCP Snooping was enabled globally on the access switch:

```cisco
ip dhcp snooping

     DHCP Snooping was enabled for the required enterprise VLANs:
ip dhcp snooping vlan 10,20,30,40,50,60

Trusted Interface

The uplink interface toward the network infrastructure was configured as trusted:

interface fastEthernet0/11
ip dhcp snooping trust
exit

Fa0/11 was selected as the trusted interface because it is the network uplink/trunk.

Untrusted Access Ports

The end-device ports remained untrusted:

Fa0/1
Fa0/2
Fa0/3
Fa0/4
Fa0/5
Fa0/6
Fa0/7
Fa0/8
Fa0/9
Fa0/10

These ports connect to end-user devices and therefore should not be trusted as DHCP server sources.

          Verification

DHCP Snooping was verified with:

show ip dhcp snooping

The verification showed:

Switch DHCP snooping is enabled

DHCP Snooping was configured for:

VLAN 10
VLAN 20
VLAN 30
VLAN 40
VLAN 50
VLAN 60

The interface status showed:

Fa0/1  — Trusted: no
Fa0/2  — Trusted: no
Fa0/3  — Trusted: no
Fa0/4  — Trusted: no
Fa0/5  — Trusted: no
Fa0/6  — Trusted: no
Fa0/7  — Trusted: no
Fa0/8  — Trusted: no
Fa0/9  — Trusted: no
Fa0/10 — Trusted: no
Fa0/11 — Trusted: yes

DHCP Snooping Binding Table

The binding table was checked using:

show ip dhcp snooping binding

The current result was:

Total number of bindings: 0

No DHCP Snooping bindings were present at the time of verification.

This result was documented as observed rather than assuming that DHCP bindings had been learned.

Packet Tracer Observation

Packet Tracer initially reported:

Switch DHCP snooping is disabled

even though the VLAN and trusted-interface configuration was already present.

DHCP Snooping was then enabled globally with:

ip dhcp snooping

After enabling it, verification showed:

Switch DHCP snooping is enabled

The configuration was saved successfully using:

write memory
Security Design

The DHCP Snooping design follows the principle that:

End-user access ports are untrusted.
The legitimate DHCP/network uplink is trusted.
DHCP Snooping is enabled only on the required VLANs.

This helps prevent unauthorized DHCP server responses from reaching clients through user-facing access ports.

      Verification Commands

The following commands were used:

show ip dhcp snooping
show ip dhcp snooping binding


          Evidence

Screenshots documenting this phase are stored in the repository's screenshots directory.

Evidence files
DHCP-SNOOPING-VERIFICATION & DHCP-SNOOPING-BINDING.png

The verification screenshot demonstrates that DHCP Snooping is enabled, the required VLANs are protected, access ports remain untrusted, and the uplink is trusted.
