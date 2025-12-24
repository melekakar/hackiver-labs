# Moonshade – Hackviser Lab Write-up

This write-up documents the exploitation steps performed in the **Moonshade**
lab on the Hackviser platform.  
The scenario focuses on **SMB enumeration, credential extraction, password
cracking, RDP access, and local privilege escalation** on a Windows system.

> ⚠️ Educational purposes only.  
> All actions were performed in a controlled lab environment.

---

## 🔍 Information Gathering

Initial port scanning revealed that the target system was running
**SMB** and **RDP** services.

Key observations:
- SMB shares were accessible without authentication
- RDP service was exposed and later used for initial access

---

## 📂 SMB Enumeration

Anonymous SMB enumeration was performed to list shared resources.

A backup share named:


was discovered.  
Inside this share, critical Windows registry backup files were found:

- `sam_file`
- `system_file`
- `security_file`

These files contain credential-related information required for offline analysis.

---

## 🔐 Credential Dumping (SAM & SYSTEM)

The downloaded registry files were used to extract local user password hashes.

Tool used:
- `impacket-secretsdump`

This resulted in a local SAM dump containing NTLM password hashes.

---

## 🔑 Password Cracking

From the extracted data, the **edward** user account was identified.

- Hash type: NTLM
- Tool used: `hashcat`
- Wordlist: `rockyou.txt`

The password for the user was successfully cracked:

---

## 🖥️ RDP Access

Using the recovered credentials, remote desktop access was established.

- Service: RDP
- Username: `edward`
- Password: `twilight`

This provided an initial foothold on the Windows target system.

---

## ⚙️ Post-Exploitation Enumeration

After logging in, further enumeration was performed to identify stored credentials
and potential privilege escalation paths.

Command used:
```powershell
cmdkey /list
🚀 Meterpreter Shell Access
To escalate privileges, a Meterpreter payload was generated and executed.
Steps:
A meterpreter reverse_tcp payload was created using msfvenom
The payload was transferred to the target via a temporary HTTP server
A Metasploit handler was configured and started
The payload was executed on the Windows system
This resulted in a successful Meterpreter session.
⬆️ Privilege Escalation
With an active Meterpreter session, local exploit enumeration was performed.
Module used:
multi/recon/local_exploit_suggester
The system was found vulnerable to:
cve_2020_0787_bits_arbitrary_file_move
The exploit was executed successfully, resulting in elevated privileges.
👑 SYSTEM Access
After exploitation, the session was upgraded to NT AUTHORITY\SYSTEM.
This allowed access to protected files belonging to other users on the system.
📧 Sensitive File Access
With SYSTEM-level privileges, the following file was accessed:
email_addresses.txt
The file contained internal email address information associated with the
company.hv domain.
✅ Conclusion
In this lab, the following objectives were successfully completed:
SMB anonymous access exploitation
Offline credential extraction from SAM & SYSTEM
NTLM password cracking
RDP-based initial access
Meterpreter shell establishment
Local privilege escalation to SYSTEM
Access to restricted user files
This lab demonstrates the real-world risk of exposed backups, weak passwords,
and unpatched local privilege escalation vulnerabilities.
🧠 Key Takeaways
Never expose registry backups via network shares
Enforce strong password policies
Restrict anonymous SMB access
Regularly patch Windows systems
🧪 Lab completed successfully on Hackviser
