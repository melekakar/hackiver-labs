# Supervisor XML-RPC RCE – Hackviser Lab

## Platform
- Hackviser
- Category: Linux / Web
- Difficulty: Medium

## Enumeration
- Nmap scan revealed:
  - 22/tcp (SSH)
  - 9001/tcp (Supervisor Web Interface)

## Vulnerability
- Supervisor version 3.3.2
- XML-RPC interface vulnerable to RCE

## Exploitation Summary
- Reverse shell obtained via Metasploit
- Initial access as low-privileged user

## Privilege Escalation
- SUID binaries enumerated
- Python SUID binary abused
- Root access achieved

## Proof
- `whoami` → root

## Lessons Learned
- Exposed management services are critical risks
- Version enumeration is key
- SUID misconfigurations can lead to full compromise

## Disclaimer
This write-up is for educational purposes only.
All actions were performed in a legal lab environment.
