# 🔐 Cisco Ethical Hacker — Quick Notes

> Concepts → Methodology → Attacks → Tools → Reporting

## 01. Ethical Hacking

* Ethical hacking = **authorized security testing**
* Goals:

  * Find vulnerabilities
  * Validate controls
  * Assess risk
  * Recommend remediation
* **Authorization comes first**
* Never test outside the agreed scope.

### Threat / Vulnerability / Risk

* **Threat** → Potential danger
* **Vulnerability** → Weakness
* **Risk** → Potential impact/loss

### Pentest Flow

`Authorization → Scope → Recon → Scanning → Enumeration → Vulnerability Analysis → Exploitation → Post-Exploitation → Reporting → Remediation → Retest`

### Methodologies

* PTES
* NIST
* OWASP
* Rules of Engagement (RoE)

---

## 02. Planning & Scoping

### GRC

* **Governance** → Direction & control
* **Risk** → Identify → Analyze → Treat → Monitor
* **Compliance** → Follow laws, policies & standards

### Scope

* **In-Scope** → Allowed targets
* **Out-of-Scope** → Do not test

Before testing:

* Written authorization
* Defined scope
* Testing window
* Restrictions
* Communication channel
* Emergency procedure

### Test Types

* **Black Box** → Little/no internal information
* **Gray Box** → Partial information
* **White Box** → Extensive information

---

## 03. Recon & Scanning

### Recon

**Passive**

* No direct target interaction
* Search engines, DNS, public docs, certificates, code repos

**Active**

* Direct interaction
* Host discovery, port scanning, service detection

### Important Tools

| Tool         | Use                    |
| ------------ | ---------------------- |
| `whois`      | Domain information     |
| `dig`        | DNS queries            |
| `nslookup`   | DNS lookup             |
| `traceroute` | Network path           |
| `ping`       | Connectivity           |
| `nmap`       | Host/service discovery |

### Common Ports

```text
21    FTP
22    SSH
23    Telnet
25    SMTP
53    DNS
80    HTTP
110   POP3
143   IMAP
443   HTTPS
445   SMB
3389  RDP
```

> Open port ≠ automatically vulnerable.

### Vulnerability Scanning

* **False Positive** → Reported but not actually vulnerable
* **False Negative** → Vulnerability exists but scanner misses it
* CVSS → Common vulnerability severity system

---

## 04. Social Engineering

Targets **people**, not just technology.

### Common Types

* Phishing
* Spear phishing
* Vishing
* Smishing
* Pretexting
* Baiting
* Tailgating
* Impersonation

### Influence Techniques

* Authority
* Urgency
* Fear
* Trust
* Curiosity
* Scarcity

### Defense

* Security awareness
* MFA
* Verification procedures
* Email filtering
* Physical access controls
* Least privilege

---

## 05. Network Security

### Common Weaknesses

* Weak authentication
* Unpatched services
* Misconfiguration
* Insecure protocols
* Excessive exposure
* Weak access controls

### MITM

Attacker positions between communicating parties.

Possible impact:

* Traffic interception
* Data manipulation
* Credential theft

### ARP Spoofing

Attempts to associate attacker's MAC address with another host's IP.

Defense:

* Dynamic ARP Inspection
* VLAN segmentation
* Switch security
* Network monitoring

### Wireless

```text
WEP  → Legacy / insecure
WPA  → Older standard
WPA2 → Widely deployed
WPA3 → Newer standard
```

Risks:

* Weak passwords
* Rogue AP
* Evil Twin
* Misconfiguration
* Deauthentication
* Unsecured networks

---

## 06. Application Security

### OWASP

Major web security areas:

* Injection
* Authentication failures
* Authorization failures
* XSS
* CSRF
* SSRF
* Security misconfiguration
* File inclusion
* Business logic flaws

### Injection

Untrusted input becomes part of a command/query.

Examples:

* SQL Injection
* Command Injection
* LDAP Injection

Defense:

* Parameterized queries
* Prepared statements
* Input validation
* Least privilege

### Authentication vs Authorization

```text
Authentication → Who are you?
Authorization  → What can you access?
Accounting     → What did you do?
```

### XSS

Attacker-controlled script executes in a victim's browser.

Types:

* Stored
* Reflected
* DOM-based

Defense:

* Output encoding
* Input validation
* CSP
* Secure cookies

### CSRF

Tricks an authenticated browser into performing an unwanted action.

Defense:

* CSRF tokens
* SameSite cookies
* Origin/Referer validation
* Re-authentication

### SSRF

Server is influenced to make requests on behalf of the attacker.

Defense:

* URL allowlists
* Network segmentation
* Egress filtering
* Metadata protections

### LFI / RFI

* **LFI** → Local File Inclusion
* **RFI** → Remote File Inclusion

### Business Logic

Application works as coded, but the **workflow can be abused**.

---

## 07. Cloud / Mobile / IoT

### Cloud Risks

* IAM issues
* Misconfigured storage
* Exposed APIs
* Excessive permissions
* Insecure interfaces
* Poor network configuration

**Least Privilege:** Give only required permissions.

### Cloud Models

* IaaS
* PaaS
* SaaS

Security follows a **shared responsibility model**.

### Mobile Risks

* Insecure storage
* Weak authentication
* Insecure APIs
* Excessive permissions
* Unencrypted communication
* Reverse engineering

### IoT Risks

* Default credentials
* Infrequent updates
* Exposed services
* Limited resources

Defense:

* Change defaults
* Update firmware
* Segment networks
* Disable unnecessary services
* Monitor devices

---

## 08. Post-Exploitation

Purpose: understand **impact after authorized access**.

### Key Concepts

```text
Initial Access
      ↓
   Foothold
      ↓
Privilege Escalation
      ↓
Enumeration
      ↓
Lateral Movement
```

### Privilege Escalation

* **Vertical** → User → Admin/Root
* **Horizontal** → Access another user's resources

### Lateral Movement

`System A → System B`

### Enumeration

Look for:

* Users/groups
* Processes
* Services
* Network connections
* Files
* Shares
* Installed software

### Persistence

Only when explicitly authorized; document and remove after testing.

---

## 09. Reporting

A finding should be:

`Discovered → Validated → Documented → Explained → Remediated → Retested`

### Report Structure

**Executive Summary**

* Purpose
* Major findings
* Business impact
* Recommendations

**Technical Finding**

* Finding
* Description
* Affected asset
* Evidence
* Severity
* Impact
* Remediation
* References

### PoC

Good PoC:

* Reproducible
* Minimal
* Safe
* Documented

### Good Remediation

* Specific
* Practical
* Prioritized
* Technically accurate

---

## 10. Tools & Code

### Scripting

Useful languages:

* Python
* Bash
* PowerShell
* JavaScript

Uses:

* Automation
* Log analysis
* Data processing
* Network/API interaction
* Tool development

### Static vs Dynamic

```text
Static  → Analyze without execution
Dynamic → Analyze while running
```

### Important Tools

| Tool         | Main Use                  |
| ------------ | ------------------------- |
| `Nmap`       | Network/service discovery |
| `Wireshark`  | Packet analysis           |
| `Burp Suite` | Web testing               |
| `Metasploit` | Security testing          |
| `Nikto`      | Web server assessment     |
| `Gobuster`   | Content discovery         |
| `Nessus`     | Vulnerability assessment  |
| `OpenVAS`    | Vulnerability scanning    |
| `John`       | Password auditing         |
| `Hashcat`    | Hash/password auditing    |
| `Netcat`     | Network connections       |

> Tool output = **evidence**, not automatically proof. Validate findings.

---

# 🧠 High-Value Revision

### CIA Triad

* **Confidentiality** → Prevent unauthorized disclosure
* **Integrity** → Prevent unauthorized modification
* **Availability** → Keep systems accessible

### Important Differences

```text
Threat        → Potential danger
Vulnerability → Weakness
Risk          → Potential impact

Authentication → Identity
Authorization  → Permissions

Passive Recon → Indirect
Active Recon  → Direct

Static  → Without execution
Dynamic → During execution

Black Box → Low information
Gray Box  → Partial information
White Box → High information

LFI → Local File Inclusion
RFI → Remote File Inclusion

XSS  → Script executes in victim's browser
CSRF → Victim's browser performs unwanted action

Privilege Escalation → User → Higher privilege
Lateral Movement      → System A → System B
```

## ⚡ Attack → Defense

| Attack               | Main Defense                        |
| -------------------- | ----------------------------------- |
| Phishing             | Awareness + MFA                     |
| Brute Force          | MFA + Rate limiting                 |
| SQLi                 | Parameterized queries               |
| XSS                  | Output encoding + CSP               |
| CSRF                 | CSRF tokens + SameSite              |
| SSRF                 | Allowlists + Network controls       |
| MITM                 | Encryption + Certificate validation |
| ARP Spoofing         | Dynamic ARP Inspection              |
| Evil Twin            | Secure authentication               |
| Misconfiguration     | Hardening + Secure defaults         |
| Excessive Privileges | Least privilege                     |

---

## 🎯 Mental Model

```text
AUTHORIZATION
      ↓
    SCOPE
      ↓
    RECON
      ↓
   SCANNING
      ↓
 ENUMERATION
      ↓
 VULNERABILITY
      ↓
 EXPLOITATION
      ↓
POST-EXPLOITATION
      ↓
   EVIDENCE
      ↓
  REPORTING
      ↓
 REMEDIATION
      ↓
   RETEST
```

> **Only test systems you own or have explicit authorization to test.**
