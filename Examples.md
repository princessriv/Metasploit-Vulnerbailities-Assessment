# Examples — How to reproduce scans (SANITIZED)

> NOTE: These examples use placeholders. Replace `TARGET_IP` with the IP of your isolated lab VM only. Do not run these commands against external systems without explicit authorization.

## Quick discovery
```bash
# show interface addresses
ip addr

# quick ARP discovery on your lab subnet
sudo netdiscover -i eth0 -r 192.168.xxx.0/24
Full port & service enumeration

# full TCP scan with service version detection and default NSE scripts
nmap -p- -sV -sC TARGET_IP

Vulnerability enumeration (NSE)

# use NSE vulnerability scripts to surface known issues
nmap -p- -sV --script=vuln TARGET_IP

Targeted scans (example)

# scan common service ports
nmap -p21,22,80,111,139,445,8180 -sV --script=vuln TARGET_IP

Manual validation (lab-only)

# interactive FTP check (anonymous)
ftp TARGET_IP
# login as: anonymous   (press Enter)
# password: (press Enter)
# commands: ls, ls -la

Notes

Always run these commands only on systems you own or have explicit permission to test.

Replace TARGET_IP with your lab VM's IP only and ensure the VM is on an isolated NAT/Host-only network.

