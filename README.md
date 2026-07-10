# Fortinet-Home-Lab

Enterprise IT home lab covering Windows Server/AD fundamentals (DNS, DHCP, GPO, file shares, account administration), Entra ID hybrid identity, Intune device management, and FortiGate networking/security. Built to demonstrate hands-on skills.

## Environment

- **Host:** Windows 10, 32GB RAM, VirtualBox 7.2.6
- **DC01**: Windows Server 2025, domain controller for `fortinetlab.local`
- **FortiGate VM**: FortiOS v7.6.7, evaluation license
- **WIN10**: Windows 10 client, domain-joined, Hybrid Entra Joined, Intune-enrolled
- **WIN10-UEFI-BITLOCKER**: separate VM built for BitLocker testing (UEFI + TPM 2.0)

## Phases

**1. [Domain Infrastructure Build](./01-domain-infrastructure)**
Installed Windows Server 2025, configured the AD DS, DNS, and DHCP roles, promoted the server to a Domain Controller for `fortinetlab.local`, and built the DHCP scope for the domain network.

**2. [Windows Client Deployment](./02-client-deployment)**
Deployed a Windows 10 client, verified DHCP/DNS, and joined it to the domain.

**3. [Active Directory Administration](./03-ad-administration)**
Built out OU structure, created users and security groups, and practiced account lifecycle management (resets, disables, moves).

**4. [Group Policy](./04-group-policy)**
Created and deployed GPOs for password policy, restrictions, and screen lock, then validated policy processing on the client.

**5. [File Shares & NTFS Permissions](./05-file-shares-permissions)**
Built a departmental share structure and tested share vs. NTFS permission behavior with a domain user.

**6. [Account Lockout & Recovery](./06-account-lockout)**
Configured a lockout policy, triggered a lockout, and resolved it via ADUC and PowerShell.

**7. [DNS Troubleshooting](./07-dns-troubleshooting)**
Simulated a DNS misconfiguration and practiced systematic issue isolation to restore name resolution.

**8. [BitLocker Encryption & AD Recovery](./08-bitlocker)**
Built a UEFI/TPM 2.0-enabled VM, enabled BitLocker, configured GPO-based recovery key escrow to Active Directory, and simulated a helpdesk recovery scenario.

**9. [Microsoft Entra ID Hybrid Identity Sync](./09-entra-id-hybrid-sync)**
Configured Entra Connect Sync with Password Hash Sync and Seamless SSO, handling the non-routable domain and verifying sync end to end.

**10. [FortiGate LAN-to-WAN Connectivity](./10-fortigate-lan-to-wan)**
Built out FortiGate's core routing and firewall policy with NAT to provide internet access to the internal domain network.

**11. [Intune Hybrid Microsoft Entra Join](./11-intune-hybrid-join)**
Enrolled a domain-joined client into Intune, resolved OU/sync scoping issues, and deployed device configuration profiles.

**12. [SSL Deep Inspection](./12-ssl-deep-inspection)**
Deployed FortiGate's SSL/SSH inspection profile with certificate distribution via Intune, and documented real licensing/architectural limitations.

## Skills Demonstrated

Windows Server administration, Active Directory & Group Policy, DNS/DHCP, SMB file services & NTFS permissions, Microsoft Entra ID, Microsoft Intune, FortiGate/FortiOS administration, PKI/certificate deployment, network security policy, and structured technical troubleshooting/documentation.
