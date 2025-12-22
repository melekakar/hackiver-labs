# Hackviser – Glitch Machine Write-up

## Overview
This write-up documents the steps and methodology used to successfully solve
the **Glitch** machine on the Hackviser platform.

The focus is on vulnerability identification, exploitation workflow, and
privilege escalation techniques.

---

## Enumeration
- Open ports identified via Nmap
- Services discovered:
  - SSH (22)
  - HTTP (80)
- Web server detected: **Nostromo 1.9.6**

---

## Vulnerability Analysis
- **CVE-2019-16278**
- Nostromo directory traversal leading to remote command execution
- Exploitation performed using Metasploit Framework

---

## Initial Access
- Remote command execution achieved
- Reverse shell obtained
- Linux kernel version identified using standard enumeration commands

---

## Privilege Escalation
- Kernel version vulnerable to **Dirty Pipe (CVE-2022-0847)**
- Local privilege escalation successfully performed
- Root access achieved

---

## Key Takeaways
- Importance of accurate service version detection
- Chaining RCE with local privilege escalation
- Understanding kernel-level vulnerabilities in Linux systems

---

## Disclaimer
This content is shared strictly for **educational purposes**.
No sensitive data, credentials, hashes, or exploit source code are included.

- Glitch – RCE & Linux Privilege Escalation (Dirty Pipe)
---
Author: Melek Akar  
Platform: Hackviser  
Category: Linux Privilege Escalation
