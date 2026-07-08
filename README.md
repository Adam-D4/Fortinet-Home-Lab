# Fortinet-Home-Lab

Enterprise IT home lab covering Windows Server/AD fundamentals (DNS, DHCP, GPO, file shares, account administration), Entra ID hybrid identity, Intune device management, and FortiGate networking/security. Built to demonstrate hands-on skills.

## Environment

- **Host:** Windows 10, 32GB RAM, VirtualBox 7.2.6
- **DC01** — Windows Server 2025, domain controller for `fortinetlab.local`
- **FortiGate VM** — FortiOS v7.6.7, evaluation license
- **WIN10** — Windows 10 client, domain-joined, Hybrid Entra Joined, Intune-enrolled
- **WIN10-UEFI-BITLOCKER** — separate VM built for BitLocker testing (UEFI + TPM 2.0)

## Phases

**1. Domain Infrastructure Build**
Installed Windows Server 2025, configured AD DS, DNS, and DHCP, and promoted the server to a Domain Controller for `fortinetlab.local`.

**2. Windows Client Deployment**
Deployed a Windows 10 client, verified DHCP/DNS, and joined it to the domain.

**3. Active Directory Administration**
Built out OU structure, created users and security groups, and practiced account lifecycle management (resets, disables, moves, unlocks).

**4. DHCP Configuration**
Configured scope options and verified lease behavior.

**5. DNS Fundamentals**
Tested name resolution, simulated a DNS failure, and restored correct configuration.

**6. Group Policy**
Created and deployed GPOs for password policy, account lockout, restrictions, and screen lock.

**7. File Shares & NTFS Permissions**
Built a departmental share structure and tested share vs. NTFS permission behavior.

**8. Account Lockout & Recovery**
Simulated and resolved account lockout via ADUC and PowerShell.

**9. DNS Troubleshooting**
Simulated a DNS misconfiguration and practiced systematic issue isolation.

**10. BitLocker Encryption & AD Recovery**
Built a UEFI/TPM 2.0-enabled VM, enabled BitLocker, configured GPO-based recovery key escrow to Active Directory, and simulated a helpdesk recovery scenario.

**11. Microsoft Entra ID Hybrid Identity Sync**
Configured Entra Connect Sync with Password Hash Sync and Seamless SSO, resolving real-world sync and clock-skew issues.

**12. FortiGate LAN-to-WAN Connectivity**
Built out FortiGate's core routing and firewall policy to provide internet access to the internal domain network.

**13. Intune Hybrid Microsoft Entra Join**
Enrolled a domain-joined client into Intune, resolved OU/sync scoping issues, and deployed device configuration profiles.

**14. SSL Deep Inspection**
Deployed FortiGate's SSL/SSH inspection profile with certificate distribution via Intune, and documented real licensing/architectural limitations.

## Skills Demonstrated

Windows Server administration, Active Directory & Group Policy, DNS/DHCP, SMB file services & NTFS permissions, Microsoft Entra ID, Microsoft Intune, FortiGate/FortiOS administration, PKI/certificate deployment, network security policy, and structured technical troubleshooting/documentation.
