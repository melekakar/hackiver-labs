
# Hackviser Labs

This repository contains my **penetration testing and web security lab work**
completed on the **Hackviser platform**.

The goal of this repository is to document security findings in an **ethical,
structured, and professional write-up format**, focusing on **learning,
enumeration, and reporting** rather than exploitation for harm.

---

## Contents

This repository includes labs and write-ups related to:

- Web Application Security
- Vulnerability Analysis & Reporting
- OWASP Top 10 focused scenarios
- Ethical penetration testing (lab environments only)

---

## Labs Overview

| Lab Name | Description |
|--------|------------|
| **Able (Warm-up)** | FTP Information Disclosure & Linux Privilege Escalation |
| **Moonshade** | SMB enumeration, SAM dump, NTLM cracking, RDP access and local privilege escalation |

---

## 🛠️ Tools & Technologies

- Linux
- Nmap
- FTP
- SSH
- Linux Capabilities
- GTFOBins
- OWASP Methodology

---

## Able (Warm-up) – FTP Information Disclosure & Privilege Escalation

### Enumeration

- Open services identified:
  - FTP (21)
  - SSH (22)
- Anonymous FTP access was enabled

---

### Information Disclosure (FTP)

- An accessible file named **readme** was discovered via anonymous FTP
- The file contained misconfigured internal system notes
- A **username was accidentally leaked** in the readme file
- This information disclosure became the key entry point for further enumeration

---

### Initial Access & User Enumeration

- The leaked user account was identified on the system
- The user was found to be a member of the **sysadmins** group
- Group membership revealed access to additional system-related files and binaries

---

### Privilege Escalation

- System capabilities were enumerated using the `getcap` command
- The binary **python3.9** was found with the `cap_setuid` capability
- A known **GTFOBins technique** was used to abuse this misconfiguration
- Privilege escalation was successful and **root access was obtained**

---

### Key Takeaways

- Anonymous services can lead to critical information disclosure
- Small configuration mistakes can expose internal users and system details
- Linux capabilities are a powerful privilege escalation vector if misconfigured
- Strong enumeration often eliminates the need for brute-force attacks

---

## Disclaimer

All content in this repository:
- Is created strictly for **educational purposes**
- Was performed only in **authorized lab environments**
- Does **not** contain credentials, sensitive configuration files, or harmful payloads

Sensitive details are intentionally excluded.

---

## About Me

- Senior Management Information Systems (MIS) student
- Actively pursuing a career in **Cybersecurity**
- Focused on **Penetration Testing, SOC, and Blue Team fundamentals**
- Continuously improving through labs and CTF-style challenges

📌 This GitHub repository documents my hands-on learning and technical growth.
