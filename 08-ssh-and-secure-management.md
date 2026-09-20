# 08 — SSH & Secure Device Management

## Objective

Implement secure remote management across the enterprise network using Secure Shell (SSH) instead of insecure Telnet access.

SSH provides encrypted remote management sessions and allows network administrators to securely access routers and Layer 3 switches.

---

## Devices Configured

SSH management was configured on the following network devices:

- CORE
- DIST1
- DIST2
- LAGOS-ROUTER
- ABUJA-ROUTER
- EDGE

---

## SSH Configuration

The following configuration was applied to each supported device.

### 1. Set the Domain Name

```cisco
ip domain-name enterprise.local


The VTY lines were configured to:

Authenticate users against the local username database.

Accept SSH connections.

Prevent Telnet access.


         Verification

SSH was verified using:

show ip ssh

The device successfully accepted the SSH configuration and generated the RSA keys.

The configuration was saved successfully:

Building configuration...
[OK]
Packet Tracer Observation

During SSH configuration, Packet Tracer displayed:

%SSH-5-ENABLED: SSH 1.99 has been enabled

even though:

ip ssh version 2

was configured.

This behavior is associated with the SSH implementation used by the Packet Tracer device. The configuration command was accepted and RSA keys were successfully generated.

Security Configuration

The VTY lines were restricted to SSH:

line vty 0 4
login local
transport input ssh

This means remote management through the VTY lines requires:

A valid local username.
Authentication using the local database.
An SSH connection.

Telnet was not permitted on the configured VTY lines.

Troubleshooting / Lessons Learned

Packet Tracer displayed:

"SSH 1.99 has been enabled"

Security Configuration

The VTY lines were restricted to SSH:

line vty 0 4
login local
transport input ssh

This means remote management through the VTY lines requires:

A valid local username.
Authentication using the local database.
An SSH connection.

Telnet was not permitted on the configured VTY lines.

Troubleshooting / Lessons Learned
Issue

Packet Tracer displayed:

SSH 1.99 has been enabled

after configuring:

ip ssh version 2
Investigation

The RSA keys were successfully generated and the SSH configuration commands were accepted.

                        Resolution

The configuration was retained because Packet Tracer accepted the SSH version command and generated the required RSA keys.

This was documented as a Packet Tracer-specific behavior rather than changing the configuration unnecessarily.

Verification Commands

The following command can be used to verify SSH:
show ip ssh

                        Result

SSH-based secure device management was configured across the enterprise infrastructure.The VTY lines were restricted to SSH access, local authentication was enabled, and RSA keys were generated for SSH operation.



