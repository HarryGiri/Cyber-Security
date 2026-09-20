# 🛡️ Cybersecurity — Index & Progress

> A navigation and progress tracker for my cybersecurity learning journey.

**Focus:** Cybersecurity → Penetration Testing → Red Teaming  
**Approach:** Theory → Hands-On Practice → Documentation → Projects



# 📌 Quick Navigation

| Section                                               | Description                              |
| ----------------------------------------------------- | ---------------------------------------- |
| [01 — Foundations](01-FOUNDATIONS/)                   | Core cybersecurity fundamentals          |
| [02 — Recon & Enumeration](02-RECON-ENUMERATION/)     | Reconnaissance, scanning and enumeration |
| [03 — Web Security](03-WEB-SECURITY/)                 | Web application and API security         |
| [04 — Windows & AD](04-WINDOWS-AD/)                   | Windows and Active Directory security    |
| [05 — Privilege Escalation](05-PRIVILEGE-ESCALATION/) | Linux and Windows privilege escalation   |
| [Labs](06-LABS/)                                      | Hands-on labs and challenges             |
| [Tools](07-TOOLS/)                                    | Security tools and usage notes           |
| [Projects](08-PROJECTS/)                              | Practical security projects              |
| [Python Tools](09-PYTHON-TOOLS/)                      | Security automation and Python utilities |
| [Reports](10-REPORTS/)                                | Lab and security assessment reports      |



# 📚 01 — Foundations

### Networking

**Topics**

* OSI & TCP/IP models
* IPv4 / IPv6
* TCP / UDP
* Ports & protocols
* DNS
* DHCP
* ARP
* Routing
* HTTP / HTTPS
* Network troubleshooting

**Progress:** 🟢 In Progress / Completed Topics

→ [Networking](01-FOUNDATIONS/Networking/)


### Linux

**Topics**

* Linux filesystem
* Command line
* Users & groups
* File permissions
* Processes
* Services
* Package management
* Networking commands
* SSH
* Bash basics
* Linux enumeration
* Linux privilege escalation

**Progress:** 🟡 In Progress

→ [Linux](01-FOUNDATIONS/Linux/)

---

### Python

**Topics**

* Python fundamentals
* File handling
* Networking with Python
* Requests
* Sockets
* Automation
* Subprocesses
* Parsing
* Security scripting

**Progress:** 🟡 In Progress

→ [Python](01-FOUNDATIONS/Python/)

---

# 🔎 02 — Recon & Enumeration

### Nmap

* Host discovery
* Port scanning
* Service/version detection
* OS detection
* NSE
* Scan optimization
* Output formats

→ [Nmap](02-RECON-ENUMERATION/Nmap/)

### DNS

* DNS fundamentals
* Record types
* DNS enumeration
* Subdomains
* Zone transfer concepts
* DNS reconnaissance

→ [DNS](02-RECON-ENUMERATION/DNS/)

### Service Enumeration

* HTTP
* SSH
* FTP
* SMB
* SMTP
* DNS
* Common service enumeration techniques

→ [Service Enumeration](02-RECON-ENUMERATION/Service-Enumeration/)



# 🌐 03 — Web Security

### HTTP

* Requests & responses
* Methods
* Headers
* Cookies
* Sessions
* Status codes
* Authentication
* HTTPS

→ [HTTP](03-WEB-SECURITY/HTTP/)

### Authentication

* Authentication mechanisms
* Session management
* Authentication vulnerabilities
* Brute-force concepts
* Session-related weaknesses

→ [Authentication](03-WEB-SECURITY/Authentication/)

### Access Control

* Authorization
* IDOR / BOLA
* Privilege boundaries
* Horizontal access control
* Vertical access control

→ [Access Control](03-WEB-SECURITY/Access-Control/)

### SQL Injection

* SQL fundamentals
* Injection concepts
* Detection
* Authentication bypass concepts
* Data extraction concepts
* Prevention

→ [SQLi](03-WEB-SECURITY/SQLi/)

### XSS

* Reflected XSS
* Stored XSS
* DOM-based XSS
* Detection
* Impact
* Mitigation

→ [XSS](03-WEB-SECURITY/XSS/)

### SSRF

* SSRF fundamentals
* Server-side requests
* Internal resources
* Detection
* Impact
* Mitigation

→ [SSRF](03-WEB-SECURITY/SSRF/)

### APIs

* REST APIs
* HTTP methods
* Authentication
* Authorization
* API enumeration
* Common API vulnerabilities
* API testing with Burp Suite

→ [APIs](03-WEB-SECURITY/APIs/)

 

# 🪟 04 — Windows & Active Directory

### Windows

* Windows fundamentals
* Users & groups
* Services
* Processes
* File permissions
* Registry
* PowerShell
* Windows networking

### Active Directory

* Domains
* Domain Controllers
* Users & groups
* Organizational Units
* Kerberos
* NTLM
* LDAP
* SMB
* Group Policy
* AD enumeration
* Common attack paths

→ [Windows & AD](04-WINDOWS-AD/)

**Progress:** 🔴 Not Started / Planned

 

# ⬆️ 05 — Privilege Escalation

## Linux Privilege Escalation

* Enumeration
* SUID / SGID
* Sudo
* Cron jobs
* PATH issues
* Services
* File permissions
* Capabilities
* Kernel-related concepts

→ [Linux Privilege Escalation](05-PRIVILEGE-ESCALATION/Linux/)

 

## Windows Privilege Escalation

* Enumeration
* Services
* Scheduled tasks
* Registry
* Weak permissions
* Token privileges
* Credentials
* PowerShell
* Common misconfigurations

→ [Windows Privilege Escalation](05-PRIVILEGE-ESCALATION/Windows/)

 

# 🧪 LABS

Hands-on practice across multiple cybersecurity training platforms.

| Platform     | Focus                              | Progress       |
| ------------ | ---------------------------------- | -------------- |
| PortSwigger  | Web Security                       | 🟡 In Progress |
| TryHackMe    | Pentesting / Security Fundamentals | 🟡 In Progress |
| OverTheWire  | Linux / Command Line               | 🟡 In Progress |
| Hack The Box | Pentesting / Labs                  | 🟡 In Progress |

### Lab Documentation

For significant labs, I document:

* Objective
* Reconnaissance
* Enumeration
* Vulnerability
* Exploitation concept
* Evidence
* Lessons learned

→ [View Labs](06-LABS/)



# 🛠️ TOOLS

| Tool            | Primary Use                        |
| --------------- | ---------------------------------- |
| Nmap            | Network scanning & enumeration     |
| Burp Suite      | Web security testing               |
| Wireshark       | Network traffic analysis           |
| Gobuster        | Directory/DNS enumeration          |
| Netcat          | Network connections & testing      |
| Linux Utilities | System enumeration & investigation |

→ [View Tools](07-TOOLS/)

---

# 🚀 PROJECTS

Practical projects designed to demonstrate security methodology rather than only theoretical knowledge.

### Planned / Current Projects

* [ ] Network Security Assessment
* [ ] Web & API Security Assessment
* [ ] Active Directory Security Assessment
* [ ] VAPT Project

Projects should demonstrate:

```text
Recon
 ↓
Enumeration
 ↓
Vulnerability Identification
 ↓
Validation
 ↓
Impact Analysis
 ↓
Remediation
 ↓
Report
```

→ [View Projects](08-PROJECTS/)

---

# 🐍 PYTHON TOOLS

Security-focused Python utilities developed while learning.

### Planned Areas

* [ ] Network utilities
* [ ] Port scanner
* [ ] Recon automation
* [ ] HTTP utilities
* [ ] Log analysis
* [ ] Security automation
* [ ] Enumeration helpers

→ [View Python Tools](09-Python%20Tools/)

---

# 📝 REPORTS

Security reports documenting practical work.

### Report Structure

```text
01 — Scope
02 — Executive Summary
03 — Methodology
04 — Reconnaissance
05 — Enumeration
06 — Findings
07 — Evidence
08 — Impact
09 — Remediation
10 — Conclusion
```

→ [View Reports](10-Reports/)

---

# 📊 Overall Progress

### Foundations

* [x] Networking fundamentals
* [ ] Linux fundamentals
* [ ] Python for security
* [ ] Web fundamentals

### Reconnaissance

* [ ] Nmap
* [ ] DNS enumeration
* [ ] Service enumeration

### Web Security

* [ ] HTTP
* [ ] Authentication
* [ ] Access Control
* [ ] SQL Injection
* [ ] XSS
* [ ] SSRF
* [ ] API Security

### Windows / AD

* [ ] Windows fundamentals
* [ ] Active Directory fundamentals
* [ ] AD enumeration
* [ ] Common AD attack paths

### Privilege Escalation

* [ ] Linux privilege escalation
* [ ] Windows privilege escalation

### Practical

* [ ] 100+ quality labs/challenges
* [ ] Web security project
* [ ] Network assessment
* [ ] AD assessment
* [ ] VAPT project
* [ ] Security reports
* [ ] Python security tools



# 📈 Practical Learning Philosophy


             THEORY
                ↓
             PRACTICE
                ↓
          UNDERSTAND
                ↓
           DOCUMENT
                ↓
             BUILD
                ↓
            REPEAT


**Target allocation:**

> 30% Theory → 70% Practical

The purpose of this repository is not simply to collect notes.

It is a record of:

**What I learned → What I practiced → What I built → What I documented**

---

# ⚠️ Disclaimer

All activities documented in this repository are performed in intentionally vulnerable environments, CTF platforms, personally controlled systems, or systems for which I have explicit authorization to test.

This repository is intended for **educational and authorized security testing purposes only**.
