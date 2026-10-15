# TryHackMe — Simple CTF

## Lab Overview

| Field | Details |
|---|---|
| Platform | TryHackMe |
| Room | [Simple CTF](https://tryhackme.com/room/easyctf) |
| Difficulty | Easy |
| Category | Reconnaissance, FTP, Web Enumeration, SQL Injection, SSH, Linux Privilege Escalation |
| Target | Authorized TryHackMe lab |
| Status | Completed |

## Objective

Enumerate the target, identify a vulnerable web application, investigate the vulnerability, obtain user access, and escalate privileges to root.

## 1. Reconnaissance — Nmap

### Command

```bash
nmap -p- -sV -sC -oN nmap_scan TARGET_IP
```

### Findings

| Port | Service | Observation |
|---|---|---|
| 21/tcp | FTP | vsftpd 3.0.3; anonymous access allowed |
| 80/tcp | HTTP | Apache 2.4.18 on Ubuntu |
| 2222/tcp | SSH | OpenSSH 7.2p2 on Ubuntu |

### Analysis

The scan identified three exposed services: FTP, HTTP, and SSH. These services became the primary areas for further enumeration.

**Next step:** Enumerate web directories and investigate the FTP service.

## 2. Web Enumeration — Gobuster

### Command

```bash
gobuster dir -u http://TARGET_IP/ \
  -w /usr/share/wordlists/dirb/common.txt
```

### Findings

The directory scan identified the following paths:

- `/index.html`
- `/robots.txt`
- `/simple/`

The `/simple/` directory hosted a CMS Made Simple application.

### Analysis

Discovering the application made it possible to identify its version and research potential vulnerabilities.

**Next step:** Search for publicly documented vulnerabilities affecting CMS Made Simple.

## 3. Vulnerability Research — SearchSploit

### Search command

```bash
searchsploit "CMS Made Simple"
```

### Investigation

SearchSploit was used to search the local Exploit-DB database for publicly documented CMS Made Simple vulnerabilities.

The investigation identified a potential SQL injection vulnerability associated with **CVE-2019-9053**.

Reference: [Exploit-DB — CMS Made Simple SQL Injection](https://www.exploit-db.com/exploits/46635)

### Analysis

The exploit reference provided a lead for investigating whether the deployed application was vulnerable. The application version and the exploit's affected-version requirements should be checked before concluding that the vulnerability applies.

**Next step:** Validate the vulnerability within the authorized TryHackMe target.

## 4. SQL Injection — CVE-2019-9053

### Exploit execution

The lab used the Exploit-DB script associated with exploit ID `46635`.

```bash
python2.7 46635.py -u http://TARGET_IP/simple/ \
  --crack -w /usr/share/wordlists/rockyou.txt
```

### Findings

The exploit reported account-related information, including a username and password-hash information. The password-recovery option was used to attempt offline password cracking.


### Analysis

This step demonstrated how SQL injection can expose application data and how weak passwords can increase the impact of a vulnerability.

The recovered credentials did not provide the expected CMS login access, so the next step was to investigate whether they could authenticate to another service within the lab scope.

## 5. Initial Access — SSH

### Connection

SSH was exposed on port `2222`, rather than the default port `22`.

```bash
ssh USERNAME@TARGET_IP -p 2222
```

Enter the recovered password when prompted.

### Findings

The credentials provided access to the target as a regular system user.

After login, the user flag was located and retrieved.

**Outcome:** User-level access achieved.

## 6. Linux Privilege Escalation Enumeration

### Command

```bash
sudo -l
```

### Findings

The sudo permissions indicated that Vim could be executed with elevated privileges.

### Analysis

Interactive programs such as text editors can have security implications when permitted to run with elevated privileges. Their ability to launch other programs may allow a user to escape the intended restrictions.

**Next step:** Research the security implications of running Vim through sudo.

## 7. Privilege Escalation — Vim

### Research

The Vim entry in GTFOBins documents how editor execution through sudo can result in elevated command execution when the sudo configuration permits it.

Reference: [GTFOBins — Vim and sudo](https://gtfobins.github.io/gtfobins/vim/#sudo)

### Findings

The lab's sudo configuration allowed Vim to be used to obtain root-level access.

After confirming the effective privileges, the root flag was located and retrieved.

**Outcome:** Root-level access achieved.

## Attack Chain Summary

1. Scanned all TCP ports using Nmap.
2. Identified FTP, HTTP, and SSH services.
3. Enumerated web directories using Gobuster.
4. Discovered the CMS Made Simple application.
5. Searched for known vulnerabilities using SearchSploit.
6. Investigated CVE-2019-9053 and ran the corresponding lab exploit.
7. Recovered credentials and tested them against SSH on port 2222.
8. Enumerated sudo permissions using `sudo -l`.
9. Identified Vim as a potential privilege-escalation path.
10. Obtained root-level access and retrieved the final flag.

## Security Findings and Remediation

| Finding | Recommended remediation |
|---|---|
| Anonymous FTP access | Disable anonymous access unless required and restrict file permissions. |
| Weak password | Enforce strong, unique passwords and monitor authentication attempts. |
| Vulnerable CMS | Upgrade to a patched release and maintain a software inventory. |
| Exposure of password hashes | Use a modern password-hashing algorithm with unique salts and appropriate work factors. |
| Credential reuse | Use unique credentials for each service and rotate compromised passwords. |
| Overly permissive sudo rule | Remove unnecessary privileged editor access and enforce least privilege. |

## Skills Practiced

- Nmap service and version detection
- Gobuster directory enumeration
- SearchSploit and Exploit-DB research
- SQL injection vulnerability investigation
- Password-hash analysis
- SSH authentication
- Linux sudo-permission enumeration
- GTFOBins research
- Privilege-escalation analysis
- Security reporting and remediation

## Lab Conclusion

Simple CTF demonstrated how information disclosure, a vulnerable web application, weak credentials, exposed SSH access, and an overly permissive sudo rule can combine into a complete system compromise.

The exercise reinforced the importance of systematic enumeration, evidence-based vulnerability research, credential security, least privilege, and clear technical documentation.