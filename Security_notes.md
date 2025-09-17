# Security Notes — Data Sanitization & Safe Publication

This repository contains a sanitized write-up of a Metasploitable lab assessment. The purpose of this document is to describe the operational security (OpSec) steps taken to ensure no private or identifying information is published.

## What was sanitized
- **IP addresses:** All real IP addresses and hostnames have been replaced with placeholders (`TARGET_IP`, `ATTACKER_IP`, `VM_MAC`, etc.).  
- **Screenshots:** No raw screenshots with identifying information were published. If screenshots were used, they were saved as sanitized copies (cropped or redacted) and the originals were kept offline.  
- **Logs & pcaps:** No raw packet captures or logs containing public IPs, MAC addresses, or hostnames were included in the repository. Any log excerpts used are sanitized or redacted.

## How screenshots were sanitized
Recommended steps used when creating sanitized screenshots:
1. Open the image in a trusted editor (Paint, Preview, GIMP, Photoshop).  
2. Locate any fields containing IP addresses, MACs, usernames, hostnames, timestamps or other identifying metadata.  
3. Either crop the image to remove these fields, or place a solid rectangle or blur effect over them. Optionally overlay the placeholder text (e.g., `TARGET_IP`).  
4. Export the sanitized image using a new filename such as `screenshots/screenshot_sanitized_01.png`. Never overwrite the original until you have a secure backup offline.

## Git hygiene before publishing
If any sensitive file was accidentally committed to version control, follow these practices:
- **Do not** simply delete the file and commit — the data remains in history.  
- Use repository-cleaning tools (BFG, git-filter-repo) or contact Git hosting support to remove files from history.  
- After history rewrite, rotate any credentials that may have been exposed and inform collaborators about the forced-push.

## Lab network configuration recommendations (for safe testing)
- Use **NAT** or **Host-only** networking for VMs in local labs. Avoid Bridged mode on public/home networks.  
- If testing remotely, use an isolated cloud lab or rented testing environment — never run broad scans from your primary public IP.  
- Maintain separate user accounts and SSH keys for lab usage. Rotate keys regularly.

## Incident response (if you discover a leak)
1. Immediately take the repo or resources offline (unpublish or make private).  
2. Remove sensitive files from the repo history (BFG or git-filter-repo).  
3. Rotate any affected credentials and keys.  
4. If you believe an attacker may have accessed systems, notify your institution/IT/security team and preserve logs for investigation.

## Contact / Notes
If you need assistance with sanitizing specific screenshots or removing content from git history, consider using an offline backup and contacting repository support (e.g., GitHub Support) for assistance with cache removal.
