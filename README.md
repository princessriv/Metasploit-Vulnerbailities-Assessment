# Metasploit-Vulnerbailities-Assessment
# Metasploitable Vulnerability Assessment (Sanitized)

> **⚠️ Important:** This file is sanitized for public display. All real IP addresses, MAC addresses, hostnames and other identifying details have been replaced with placeholders (`TARGET_IP`, `ATTACKER_IP`, `VM_MAC`). Do **not** publish raw screenshots or logs that reveal your real public IP.

---

## Project summary
**Project:** Metasploitable Vulnerability Assessment (lab)  
**Objective:** Perform safe, controlled host discovery, service enumeration, and vulnerability scanning on an intentionally vulnerable Metasploitable VM to learn common attack vectors and mitigation strategies.  
**Scope:** Single lab target in an isolated environment (NAT or Host-only). No external or third-party systems were targeted.

---

## Environment (sanitized)
- **Attacker (Kali Linux VM):** `ATTACKER_VM` — placeholder IP: `ATTACKER_IP`  
- **Target (Metasploitable VM):** `TARGET_VM` — placeholder IP: `TARGET_IP`  
- **Network:** Isolated lab network (use NAT or Host-only)  
- **Tools used:** `netdiscover`, `nmap` (with `-sV`, `-sC`, `--script=vuln`), `ftp` client, `msfconsole` (Metasploit) — all actions performed in a lab-only environment

---

## Methodology (high level)
1. **Discovery:** find live hosts on the lab subnet using `netdiscover`.  
2. **Enumeration:** full TCP port scan and service/version detection with `nmap`.  
3. **Vulnerability scanning:** run NSE vulnerability scripts (`--script=vuln`) to highlight known issues.  
4. **Validation:** manual checks (e.g., anonymous FTP) and controlled exploit validation inside the isolated lab.  
5. **Sanitization:** redact or remove any identifying details before publishing results.

---

## Key commands (sanitized examples)
Replace `TARGET_IP` with your lab target only when running in a private environment.

```bash
# show local interfaces
ip addr

# discover hosts on local subnet (example)
sudo netdiscover -i eth0 -r 192.168.xxx.0/24

# full TCP scan with service detection
nmap -p- -sV -sC TARGET_IP

# vulnerability scan (NSE vuln scripts)
nmap -p- -sV --script=vuln TARGET_IP

# targeted ports scan
nmap -p21,22,80,111,139,445,8180 -sV --script=vuln TARGET_IP

# interactive FTP test (anonymous)
ftp TARGET_IP
# login: anonymous (press Enter)  password: (press Enter)
# then run `ls`, `ls -la`

# (Lab-only) Example Metasploit workflow (do NOT run against public systems)
# msfconsole
# use exploit/unix/ftp/vsftpd_234_backdoor
# set RHOST TARGET_IP
# run

Notable findings (sanitized)

FTP (port 21): vsftpd 2.3.4 — flagged as vulnerable by NSE scripts; anonymous login observed in the lab environment.

SSH (port 22): older OpenSSH version detected.

HTTP / Tomcat (ports 80, 8180): sample servlets and admin pages visible; management endpoints present.

Java RMI / drb: registry endpoints observed and flagged by vulnerability scripts.

SMB / NFS / legacy services: multiple intentionally exposed legacy services (telnet, rsh, etc.) typical of Metasploitable.



---

Short step-by-step summary (what I did)

1. Ran netdiscover to locate live hosts on the lab subnet.


2. Performed a comprehensive nmap -p- -sV -sC scan to enumerate open ports and service banners.


3. Executed nmap --script=vuln to surface known vulnerabilities and references.


4. Manually tested anonymous FTP (lab-only) to confirm access.


5. Prioritized lab exploit demonstrations (e.g., vsftpd backdoor) and recommended follow-ups for safe demonstration within an isolated environment.




---

Suggested follow-up exercises (lab-only)

Exploit validation: use Metasploit modules for vsftpd or Java RMI in the isolated VM; document commands and sanitized outputs.

Web app analysis: run directory enumeration (e.g., gobuster) against Tomcat; test sample servlets for input validation issues.

SMB enumeration: use enum4linux, smbclient to list shares and check for writable shares.

Privilege escalation: enumerate SUID files, cron jobs, and outdated packages inside the VM to practice local escalation techniques.

Post-exploitation reporting: produce a sanitized report showing the exploitation steps and remediation.



---

Remediation recommendations (what to advise a client)

Patch or replace vulnerable services: upgrade or remove old software (e.g., vsftpd).

Disable anonymous and legacy services: disable anonymous FTP, Telnet, rlogin, rexec; use SSH with key-based authentication.

Harden web applications: remove sample apps, secure Tomcat manager, and disable AJP if not required.

Network segmentation & firewalling: restrict access to management ports, enforce least privilege, and use ACLs.

Regular scanning & inventory: maintain an updated inventory of running services and schedule regular vulnerability scans.

Use lab-safe network settings: for learning, use NAT or Host-only networks and never run broad scans from a public/home IP.



