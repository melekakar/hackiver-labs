# Hackviser – Able (Warm-up) Write-up

## Overview
This write-up documents the solution process for the **Able** warm-up machine
on the Hackviser platform. The lab focuses on information disclosure,
credential discovery, and Linux privilege escalation using capabilities.

---

## Enumeration
- Open services identified using Nmap:
  - FTP (21)
  - SSH (22)
- Anonymous FTP access was enabled

---

## Information Disclosure
- A file named **readme** was accessible via anonymous FTP
- The file contained sensitive information, including a leaked username
- The leaked user account was later used for SSH access

---

## Initial Access
- SSH access obtained using credentials derived from exposed information
- User was a member of the **sysadmins** group

---

## File & Group Analysis
- The FTP file belonged to the **sysadmins** group
- Additional files owned by this group were identified in system directories
- - Files belonging to the **sysadmins** group were located under the `/configs` directory
- A VPN configuration file related to the admin user was identified during enumeration

---
## Configuration & Credential Discovery
- Group-based file enumeration revealed configuration files under `/configs`
- A VPN configuration file belonging to the **admin** user was identified
- The file contained network-related information used during the lab

---
## Privilege Escalation
- System capabilities were enumerated using `getcap`
- The binary **python3.9** was found to have the `cap_setuid` capability
- Privilege escalation was achieved via GTFOBins technique
- Root access successfully obtained

---

## Key Takeaways
- Anonymous services can lead to critical information disclosure
- Small leaks can enable full system compromise
- Linux capabilities can be abused for privilege escalation

---

## Disclaimer
This write-up is shared strictly for **educational purposes**.
No credentials, configuration files, or sensitive data are disclosed.

- Able (Warm-up) – FTP Information Disclosure & Linux Capabilities
---
Author: Melek Akar  
Platform: Hackviser  
Category: Linux Privilege Escalation / Capabilities
