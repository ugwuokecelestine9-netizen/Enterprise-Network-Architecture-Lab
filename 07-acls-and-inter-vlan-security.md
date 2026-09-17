# 06 - ACL and Security

## 1. Overview

Access Control Lists (ACLs) were implemented to control communication between the different departmental VLANs.

The objective was to provide controlled inter-VLAN communication while allowing required infrastructure services such as DHCP and DNS.

The security policy restricts direct communication between user VLANs while maintaining access to approved infrastructure services.

---

## 2. VLAN Security Policy

The enterprise network contains the following major VLANs:

| VLAN | Department | Network |
|------|------------|---------|
| 10 | Management | 192.168.10.0/24 |
| 20 | HR | 192.168.20.0/24 |
| 30 | Finance | 192.168.30.0/24 |
| 40 | Sales | 192.168.40.0/24 |
| 50 | IT | 192.168.50.0/24 |
| 60 | Guest | 192.168.60.0/24 |
| 99 | Server / Infrastructure | 192.168.99.0/24 |

The security design follows the principle that departmental VLANs should not freely communicate with other departmental VLANs.

Management and IT are intended to have broader administrative access, while HR, Finance, Sales, and Guest are restricted from directly accessing other departmental networks.

---

## 3. ACL Structure

Separate extended ACLs were created for the departmental VLANs.

The ACLs include:

- HR-OUT
- FINANCE-OUT
- SALES-OUT
- GUEST-OUT
- Additional ACL entries for controlling other traffic flows

The ACLs contain explicit permit statements for required infrastructure services before the inter-VLAN restrictions.

---

## 4. Infrastructure Services Allowed

The ACL policy allows required infrastructure traffic, including:

- DHCP
- DNS
- HTTP/Web access to the designated web server

The infrastructure servers are located in VLAN 99.

| Service | IP Address | Purpose |
|---------|------------|---------|
| DHCP Server | 192.168.99.10 | Automatic IP address assignment |
| DNS Server | 192.168.99.11 | DNS name resolution |
| Web Server | 192.168.99.12 | HTTP/Web services |

Example permitted traffic includes:

```text
UDP → 192.168.99.10 → DHCP
UDP/TCP → 192.168.99.11 → DNS
TCP → 192.168.99.12 → HTTP

5. HR ACL Policy

The HR ACL restricts HR users from directly accessing the other departmental VLANs and the server/infrastructure network.

The policy includes restrictions against:

192.168.10.0/24  - Management
192.168.30.0/24  - Finance
192.168.40.0/24  - Sales
192.168.50.0/24  - IT
192.168.60.0/24  - Guest
192.168.99.0/24  - Server / Infrastructure

Required infrastructure traffic is permitted before the restrictions.

6. Finance ACL Policy

The Finance ACL restricts Finance users from directly communicating with the other departmental VLANs and the server/infrastructure network.

The policy restricts access to:

192.168.10.0/24  - Management
192.168.20.0/24  - HR
192.168.40.0/24  - Sales
192.168.50.0/24  - IT
192.168.60.0/24  - Guest
192.168.99.0/24  - Server / Infrastructure

Required infrastructure services remain permitted.

7. Sales ACL Policy

The Sales ACL restricts Sales users from directly accessing other departmental networks and the server/infrastructure network.

The policy restricts access to:

192.168.10.0/24  - Management
192.168.20.0/24  - HR
192.168.30.0/24  - Finance
192.168.50.0/24  - IT
192.168.60.0/24  - Guest
192.168.99.0/24  - Server / Infrastructure

Required infrastructure services remain permitted.

8. Guest ACL Policy

The Guest VLAN is isolated from the internal departmental networks.

Guest traffic is restricted from accessing:

192.168.10.0/24  - Management
192.168.20.0/24  - HR
192.168.30.0/24  - Finance
192.168.40.0/24  - Sales
192.168.50.0/24  - IT
192.168.99.0/24  - Server / Infrastructure

Required infrastructure services are permitted according to the ACL policy.

9. ACL Implementation Challenge

During implementation, several ACL application methods were tested.

The initial ACL configurations were successfully created, but Packet Tracer did not consistently attach or enforce the ACLs as expected.

During this stage, inter-VLAN traffic remained permitted even though the ACL entries existed.

Further testing and modification of the ACL implementation were required.

A different ACL implementation supported by the Packet Tracer environment was eventually used.

After this change, the ACL policy began enforcing the intended inter-VLAN restrictions.

10. Packet Tracer Verification Behavior

An important observation was made during verification.

The command:

show ip interface vlan 20

reported:

## Outgoing access list is not set
Inbound access list is not set#

Similar output was observed on other VLAN interfaces.

However, controlled traffic testing showed that the configured ACL policy was actually blocking the intended inter-VLAN traffic.

Therefore, the not set output from the Packet Tracer SVI interface display was not used as the only indicator of ACL functionality.

ACL functionality was verified using:

ACL configuration
Actual traffic behavior
Inter-VLAN connectivity tests
ACL counters where available

This troubleshooting experience demonstrates the importance of validating security policies through actual network behavior rather than relying on a single CLI status field.

11. ACL Verification

The configured ACLs were inspected using:

show access-lists

This confirmed that the departmental ACLs existed and contained the intended permit and deny statements.

Example structure:

permit required infrastructure traffic
deny restricted inter-VLAN traffic
permit ip any any

The final permit statement allows traffic not explicitly restricted by the departmental policy.

12. Traffic Testing

Inter-VLAN traffic was tested to verify the security policy.

Examples of restricted communication included:

HR → Finance
Finance → HR
Sales → HR
Sales → Finance
Guest → Internal VLANs
Departmental VLANs → Server/Infrastructure VLAN

The expected behavior was that restricted departmental traffic would be blocked.

Required infrastructure services such as DHCP and DNS remained available.

13. Example ACL Verification

The following command was used to inspect an SVI:

show ip interface vlan 20

The output confirmed that the VLAN was operational:

Vlan20 is up, line protocol is up
Internet address is 192.168.20.3/24
Helper address is 192.168.99.10

The same verification process was used for other departmental VLANs.

14. Security Design Summary

The ACL implementation provides logical segmentation between departments.

The design prevents unrestricted lateral movement between departmental VLANs while allowing required infrastructure services.

The resulting security model is:

                ┌─────────────────────┐
                │ Server/Infrastructure│
                │      VLAN 99         │
                └──────────┬──────────┘
                           │
                     Controlled Access
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
      HR VLAN          Finance VLAN        Sales VLAN
    VLAN 20             VLAN 30             VLAN 40
        │                  │                  │
        └──────── Restricted Inter-VLAN ─────┘

        Management VLAN 10 → Administrative Access
        IT VLAN 50         → Administrative Access
        Guest VLAN 60      → Restricted Internal Access

15. Verification Evidence

The SCREENSHOTS directory contains evidence collected during ACL implementation and verification.

Relevant screenshots include:

ACL configuration output
HR ACL entries
Finance ACL entries
Sales ACL entries
Guest ACL entries
SVI ACL-status verification
Inter-VLAN traffic testing
Successful and blocked connectivity tests

These screenshots document both the final configuration and the troubleshooting process.

16. Key Troubleshooting Lesson

One of the major lessons from this stage was that configuration presence does not always guarantee expected behavior.

The ACL entries existed before the desired traffic restrictions became effective.

The troubleshooting process therefore followed this sequence:

ACL Configuration
       ↓
Traffic Test
       ↓
Unexpected Result
       ↓
ACL Implementation Review
       ↓
Alternative Implementation
       ↓
Traffic Test
       ↓
Restrictions Successfully Enforced

This demonstrates the importance of combining configuration verification with real traffic testing when troubleshooting network security.

17. Final Status

ACL implementation and verification completed.

The network now has:

VLAN-based segmentation
Departmental inter-VLAN restrictions
Controlled access to infrastructure services
Guest isolation
Administrative access considerations for Management and IT
Documented ACL troubleshooting
Traffic-based ACL verification.

