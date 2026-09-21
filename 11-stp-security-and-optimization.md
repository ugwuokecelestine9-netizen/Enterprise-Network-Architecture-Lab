# 11 — STP Security & Optimization

## Objective

Configure and verify Spanning Tree Protocol (STP) security features on end-device access ports.

The main objectives were:

- Improve host-port convergence using PortFast.
- Protect the Layer 2 topology using BPDU Guard.
- Maintain normal STP operation on switch uplinks.
- Document the STP security configuration across the access layer.

---

## STP Design

The enterprise network uses Layer 2 access switches connected to the distribution/network infrastructure.

The access switches have:

- End-device access ports connected to PCs.
- Uplink/trunk ports connected toward the distribution layer.

PortFast and BPDU Guard were applied to **end-device access ports only**.

The uplink/trunk ports were not configured with PortFast because they participate in the normal STP topology.

---

## PortFast

PortFast was enabled on end-device access ports.

Example configuration:

```cisco
interface FastEthernet0/1
spanning-tree portfast

The same configuration was applied to the appropriate PC-facing access ports.

Purpose

PortFast allows an access port connected to an end device to transition to the forwarding state more quickly.

This helps prevent unnecessary STP transition delays when devices such as PCs are connected or restarted.

BPDU Guard

BPDU Guard was enabled on the same end-device access ports:

interface FastEthernet0/1
spanning-tree bpduguard enable
Purpose

BPDU Guard protects PortFast-enabled access ports from receiving unexpected Bridge Protocol Data Units (BPDUs).

If an unauthorized switch is connected to a protected end-device port and sends BPDUs, BPDU Guard can place the port into an error-disabled state, helping prevent an unauthorized device from affecting the STP topology.

Access-Port Security Combination

The access ports in this lab use multiple Layer 2 security controls together.

The configuration includes:

switchport port-security
ip dhcp snooping limit rate 10
spanning-tree portfast
spanning-tree bpduguard enable

This provides multiple layers of protection on user-facing ports:

             Security Feature	Purpose
Port Security	Restricts unauthorized MAC addresses
DHCP Snooping	Helps prevent rogue DHCP activity
PortFast	Provides fast forwarding for end devices
BPDU Guard	Protects against unexpected BPDUs on host ports
Uplink Protection

The access-switch uplink is treated differently from end-device ports.

The uplink participates in the STP topology and therefore was not configured with:

spanning-tree portfast or spanning-tree bpduguard enable on the uplink.

This preserves normal STP behavior between network infrastructure devices.

STP Verification

STP operation was verified using:

show spanning-tree

The output confirmed the switch's STP information, including:

VLAN-specific spanning-tree instances
Root bridge information
Bridge ID
Port roles
Port states
STP path costs
Interface participation in STP
Interface-Level Verification

The access-port STP state was also checked using:

show spanning-tree interface fa0/1

The command confirmed that the access interface participates in STP across the configured VLANs.

PortFast & BPDU Guard Verification

The running configuration was examined to verify the security configuration.

The access-port configuration showed:

spanning-tree portfast
spanning-tree bpduguard enable

These commands were visible on the configured end-device access ports.

The verification was performed across the access-layer VLAN switches, including VLAN 10, VLAN 20, VLAN 30, VLAN 40, and VLAN 50/60 switch configurations.

Packet Tracer Consideration

Packet Tracer provides a more limited IOS command set than physical Cisco IOS environments.

Some detailed STP verification commands were not available in the simulator.

Therefore, verification was performed using the commands supported by the Packet Tracer device, including:

show spanning-tree
show spanning-tree interface fa0/1

and the running configuration.

The documentation records the commands and output actually available in the simulated environment.

                 Evidence

The following screenshots were captured and uploaded to the repository:

STP-VERIFICATION.png
VLAN-specific PortFast/BPDU Guard verification screenshots for the access switches.

The VLAN-specific screenshots demonstrate the presence of:

spanning-tree portfast
spanning-tree bpduguard enable on the configured end-device ports.

               Result

STP security and optimization were implemented on the access layer.

PortFast was applied to end-device access ports to improve convergence for host connections, while BPDU Guard was enabled to protect those ports from unexpected BPDUs.
