Live URL:  https://aminbiography.github.io/linux-cti/

---   
          
# Linux for CTI     

This repository documents **essential Linux knowledge** required for **Cyber Threat Intelligence (CTI)**, SOC operations, threat hunting, and security automation.
Each section includes **commands, explanations, and expected outputs**.
 
---
 
## Linux Core Concepts

```
filesystem, permissions, users, processes, networking, logs, services,
bash scripting, package management, security, monitoring
```

---

## 1) Linux Distributions and Installation

Common Linux distributions used in CTI and security:

* Ubuntu
* Debian
* Kali Linux
* Red Hat / Rocky Linux
* Parrot OS

Check OS details:

```bash
cat /etc/os-release
```

**Output (example):**

```text
NAME="Ubuntu"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
```

---

## 2) Linux Shell Basics

Check current user:

```bash
whoami
```

**Output:**

```text
amein
```

Check hostname:

```bash
hostname
```

**Output:**

```text
cti-lab
```

---

## 3) Linux File System Structure

Key directories:

| Directory | Purpose                     |
| --------- | --------------------------- |
| /         | Root filesystem             |
| /etc      | Configuration files         |
| /var      | Logs, spool files           |
| /home     | User home directories       |
| /tmp      | Temporary files             |
| /usr      | User binaries and libraries |

List root directories:

```bash
ls /
```

**Output (example):**

```text
bin  boot  dev  etc  home  lib  proc  tmp  usr  var
```

---

## 4) Working with Files and Directories

Create directories and files:

```bash
mkdir cti-labs
cd cti-labs
touch report.txt
```

List files:

```bash
ls -l
```

**Output:**

```text
-rw-r--r-- 1 amein amein 0 report.txt
```

---

## 5) Viewing File Contents

```bash
echo "Threat report draft" > report.txt
cat report.txt
```

**Output:**

```text
Threat report draft
```

Other useful commands:

```bash
less report.txt
head report.txt
tail report.txt
```

---

## 6) File Permissions and Ownership

Check permissions:

```bash
ls -l report.txt
```

**Output:**

```text
-rw-r--r-- 1 amein amein report.txt
```

Change permissions:

```bash
chmod 600 report.txt
```

Change ownership (requires sudo):

```bash
sudo chown root:root report.txt
```

---

## 7) Users and Groups

View current user ID:

```bash
id
```

**Output:**

```text
uid=1000(amein) gid=1000(amein) groups=1000(amein)
```

List users:

```bash
cat /etc/passwd
```

---

## 8) Process Management

List running processes:

```bash
ps aux
```

**Output (sample):**

```text
root     1023  0.0  systemd
amein    2345  0.1  bash
```

Real-time monitoring:

```bash
top
```

Kill a process:

```bash
kill 2345
```

---

## 9) Disk Usage and Monitoring

Check disk usage:

```bash
df -h
```

**Output:**

```text
Filesystem  Size  Used Avail Use%
/dev/sda1    50G   12G   36G  25%
```

Check directory size:

```bash
du -sh /var/log
```

---

## 10) Networking Basics

Check IP address:

```bash
ip a
```

**Output (example):**

```text
inet 192.168.1.20/24
```

Check active connections:

```bash
ss -tulnp
```

---

## 11) DNS and Connectivity Testing

```bash
ping google.com
```

**Output:**

```text
64 bytes from google.com: icmp_seq=1 ttl=117
```

DNS lookup:

```bash
nslookup google.com
```

---

## 12) Package Management (APT)

Update package list:

```bash
sudo apt update
```

Install a package:

```bash
sudo apt install curl
```

Verify installation:

```bash
curl --version
```

---

## 13) Log Analysis (Critical for CTI)

System logs:

```bash
ls /var/log
```

Authentication logs:

```bash
sudo cat /var/log/auth.log
```

**Output (example):**

```text
Failed password for invalid user admin from 45.33.32.156
```

---

## 14) Searching Logs and Files (grep)

```bash
grep "Failed password" /var/log/auth.log
```

**Output:**

```text
Failed password for root from 45.33.32.156
```

Recursive search:

```bash
grep -R "malware" /var/log
```

---

## 15) Bash Variables and Environment

```bash
export CTI_LEVEL=advanced
echo $CTI_LEVEL
```

**Output:**

```text
advanced
```

---

## 16) Bash Scripting Basics

Create script:

```bash
nano scan.sh
```

Script content:

```bash
#!/bin/bash
echo "Starting CTI scan..."
date
```

Make executable:

```bash
chmod +x scan.sh
./scan.sh
```

**Output:**

```text
Starting CTI scan...
Mon Dec 15 07:30:12 UTC 2025
```

---

## 17) Conditional Logic in Bash

```bash
if [ -f report.txt ]; then
  echo "Report exists"
else
  echo "Report missing"
fi
```

**Output:**

```text
Report exists
```

---

## 18) Loops in Bash

```bash
for ip in 8.8.8.8 1.1.1.1; do
  ping -c 1 $ip
done
```

**Output (example):**

```text
PING 8.8.8.8
PING 1.1.1.1
```

---

## 19) Cron Jobs (Automation)

Edit cron jobs:

```bash
crontab -e
```

Example:

```bash
0 2 * * * /home/amein/scan.sh
```

Runs script daily at 02:00.

---

## 20) System Services (systemd)

Check service status:

```bash
systemctl status ssh
```

Start / stop service:

```bash
sudo systemctl restart ssh
```

---

## 21) File Integrity and Hashing

```bash
sha256sum report.txt
```

**Output:**

```text
a3f5c1e7f2d9... report.txt
```

Used in malware analysis and IOC validation.

---

## 22) Archive and Compression

```bash
tar -czvf logs.tar.gz /var/log
```

Extract:

```bash
tar -xzvf logs.tar.gz
```

---

## 23) Permissions Abuse Detection

Find world-writable files:

```bash
find / -perm -002 -type f 2>/dev/null
```

---

## 24) Network Capture (tcpdump)

```bash
sudo tcpdump -i eth0
```

Save capture:

```bash
sudo tcpdump -i eth0 -w traffic.pcap
```

---

## 25) Linux Security Basics

Check open ports:

```bash
sudo netstat -tulnp
```

Check firewall:

```bash
sudo ufw status
```

---

## 26) SSH and Remote Access

```bash
ssh user@192.168.1.10
```

Generate SSH key:

```bash
ssh-keygen
```

---

## 27) Sudo and Privilege Escalation Awareness

```bash
sudo -l
```

**Output:**

```text
User amein may run the following commands
```

Critical for privilege escalation assessments.

---

## 28) Malware Analysis Utilities

Install tools:

```bash
sudo apt install strings binutils
```

Extract strings:

```bash
strings suspicious.bin
```

---

## 29) File System Monitoring

```bash
inotifywait -m /var/log
```

Detects file changes in real time.

---

## 30) Linux for CTI Use Cases

* Log analysis
* Threat hunting
* IOC validation
* Malware triage
* Automation with Bash
* Network monitoring
* Incident response

---

## Final Notes

This repository is designed to be:

* SOC-ready
* CTI-aligned
* Beginner → advanced
* Interview and lab friendly
* Automation-focused

---


Just tell me how deep you want to go.
