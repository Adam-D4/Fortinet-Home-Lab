# Phase 12: SSL Deep Inspection

This phase turns on SSL deep inspection on the FortiGate so it can see inside HTTPS traffic. Because the firewall re-signs that traffic, I pushed its CA certificate out to the client using both GPO and Intune, and I ran into a real limit in the eval license that I wrote up honestly.

## What I Did

On the FortiGate I selected the customizable deep-inspection SSL/SSH profile and exported its CA certificate (Fortinet_CA_SSL). To make clients trust the re-signed traffic, I distributed that CA two ways. First via on-prem Group Policy: I created a "FortiGate SSL Inspection CA Trust" GPO, imported the certificate into Computer Configuration → Public Key Policies → Trusted Root Certification Authorities, forced `gpupdate` on DC01 and the client, and confirmed through an MMC Certificates snap-in that the certificate landed in the machine's Trusted Root store. Then via Intune (the method I kept): a Trusted Certificate configuration profile targeting the Computer certificate store (Root), assigned to all devices, which I confirmed in `certlm.msc` after syncing the client. On the firewall I bound the custom-deep-inspection profile to the LAN-to-WAN policy and enabled the Web Filter alongside it (SSL inspection needs another profile active to actually engage). Browsing to an HTTPS site then showed the certificate had been re-issued by the FortiGate's CA rather than the site's real issuer, which is direct proof the firewall was intercepting and re-signing the connection.

## Key Takeaways

Deep SSL inspection is a man-in-the-middle by design, so it only works if every client trusts the firewall's inspection CA, which is exactly why certificate distribution (GPO or Intune) is inseparable from the feature. Doing it both ways was a useful comparison: GPO is the classic on-prem approach, while an Intune Trusted Certificate profile is the cloud-managed equivalent, and I retained Intune as the real method. The honest limitation: the evaluation license/VM tier generates its SSL inspection CA with a weak 512-bit RSA key, and the evaluation tier blocked generating a stronger 2048-bit replacement. Modern browsers reject 512-bit keys outright (ERR_CERT_WEAK_KEY), so although interception provably worked, and the re-signed certificate chain confirms it, full, reliable SSL inspection isn't achievable on this lab tier. Recognizing and documenting a hard licensing/architectural constraint is itself a real-world skill.

## Screenshots

**Selecting the customizable deep-inspection SSL/SSH profile**
![SSL inspection profiles](./images/01-ssl-inspection-profiles.png)

**Exporting the FortiGate's SSL inspection CA certificate (Fortinet_CA_SSL)**
![Download CA certificate](./images/02-download-ca-certificate.png)

**Creating the GPO to distribute the inspection CA**
![Create GPO](./images/03-create-gpo.png)

**Importing the CA into Trusted Root Certification Authorities via GPO**
![GPO certificate import wizard](./images/04-gpo-cert-import-wizard.png)

**CA certificate imported into the GPO's Trusted Root store**
![GPO certificate imported](./images/05-gpo-cert-imported.png)

**Forcing gpupdate on DC01**
![gpupdate on DC01](./images/06-gpupdate-dc01.png)

**Forcing gpupdate on the WIN10 client**
![gpupdate on WIN10](./images/07-gpupdate-win10.png)

**Building an MMC Certificates snap-in for the computer account**
![MMC Certificates snap-in](./images/08-mmc-certificates-snapin.png)

**CA certificate present in the client's Trusted Root store (via GPO)**
![Certificate landed on WIN10](./images/09-cert-landed-win10-gpo.png)

**Creating a Trusted Certificate profile in Intune (the retained method)**
![Intune create certificate profile](./images/10-intune-create-cert-profile.png)

**Configuring the Intune profile with Fortinet_CA_SSL.cer to the Root store**
![Intune certificate profile config](./images/11-intune-cert-profile-config.png)

**Assigning the certificate profile to all devices**
![Intune certificate profile, all devices](./images/12-intune-cert-profile-all-devices.png)

**Syncing the client to pull the new Intune profile**
![Sync WIN10 to Intune](./images/13-sync-win10-intune.png)

**Confirming the CA certificate in certlm on the client**
![Certificate in certlm](./images/14-cert-in-certlm.png)

**Binding the custom-deep-inspection profile to the LAN-to-WAN policy**
![Bind deep inspection to policy](./images/15-bind-deep-inspection-policy.png)

**Enabling the Web Filter alongside SSL inspection on the policy**
![Enable Web Filter](./images/16-enable-web-filter.png)

**HTTPS traffic re-signed by the FortiGate CA, interception confirmed**
![FortiGate re-signed certificate](./images/17-fortigate-resigned-cert.png)
