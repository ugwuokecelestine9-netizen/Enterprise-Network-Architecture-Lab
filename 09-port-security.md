
# 09 — Port Security

## Objective

Implement Layer 2 Port Security on end-device access ports to prevent unauthorized devices from connecting to the enterprise network.

Port Security was configured on access switches to control the number of MAC addresses permitted on individual access ports.

---

## Security Design

Port Security was applied to end-user access ports rather than trunk/uplink interfaces.

For example, on the VLAN 20 access switch:

- Fa0/1–Fa0/10 — PC access ports
- Fa0/11 — trunk/uplink port
- Fa0/12–Fa0/24 — unused ports

The trunk interface was not configured with Port Security because it is used for network infrastructure connectivity.

---

## Port Security Configuration

The access ports were configured using the following security settings:

```cisco
interface range fastEthernet0/1 - 10
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
exit

Configuration Explanation
Access Mode
switchport mode access

Ensures the ports operate as access ports for end devices.

Enable Port Security
switchport port-security

     Enables MAC-address-based port security.

Maximum MAC Addresses
switchport port-security maximum 1

Allows one authorized MAC address on each secured access port.

       Sticky MAC Learning
switchport port-security mac-address sticky

Allows the switch to dynamically learn the connected device's MAC address and associate it with the port.

         Violation Action
"switchport port-security violation shutdown"

Places the port into a shutdown/err-disabled security state if an unauthorized MAC address violates the configured policy.

        Verification

Port Security was verified using:

show port-security

     Interface-specific verification:

"show port-security interface fastEthernet0/1"

Learned secure MAC addresses were checked using:

"show port-security address"

These commands were used to verify the Port Security state, maximum MAC-address limit, violation mode, and learned secure MAC addresses.

              Trunk Protection Consideration

Port Security was not applied to the trunk/uplink interface.

For example:

Fa0/11 — trunk

This interface carries network traffic between infrastructure devices and therefore was left outside the end-device Port Security configuration.

               Security Result

Port Security provides an additional Layer 2 security control by limiting which devices can use protected access ports.

The configuration helps protect the enterprise access layer against unauthorized devices being connected to secured switch ports.
