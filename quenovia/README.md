# Hackviser – Quenovia (Warm-up) Write-up

## Overview
This lab demonstrates a full attack chain starting from a file upload vulnerability
and ending with root privilege escalation via misconfigured cron jobs.

---

## Enumeration
- Web service running on port 80
- File upload functionality identified on visa application page
- Uploaded files accessible under `/uploads` directory

---

## Initial Access – File Upload Vulnerability
- Client-side file type restriction bypassed by modifying HTML `accept` attribute
- Arbitrary file upload confirmed
- Web shell uploaded to the server
- Remote command execution achieved via web shell

---

## Post-Exploitation
- Web root enumeration revealed database configuration file
- Database credentials discovered in application source code

---

## Privilege Escalation
- System-wide cron jobs enumerated
- Root-owned cron job executing `clean_logs.sh` every minute
- Script sourced a writable configuration file
- Command injection via sourced config file
- Reverse shell obtained with root privileges

---

## Key Takeaways
- Client-side validations are not security controls
- File upload vulnerabilities can easily lead to RCE
- Cron jobs combined with writable config files are dangerous
- Proper permission management is critical

---

## Disclaimer
This write-up is for **educational purposes only**.
All actions were performed in a controlled lab environment.
No sensitive data or real credentials are disclosed.

---

**Author:** Melek Akar  
**Platform:** Hackviser  
**Category:** File Upload / Linux Privilege Escalation
