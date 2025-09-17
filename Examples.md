# Examples — How to reproduce scans (SANITIZED)

> NOTE: These examples use placeholders. Replace `TARGET_IP` with the IP of your isolated lab VM only. Do not run these commands against external systems without explicit authorization.

## Quick discovery
```bash
# show interface addresses
ip addr

# quick ARP discovery on your lab subnet
sudo netdiscover -i eth0 -r 192.168.xxx.0/24
