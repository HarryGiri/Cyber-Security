# Reconnaissance & Pentesting Methodology

## 1. Overview

Reconnaissance is the process of collecting information about an authorized target before attempting deeper enumeration or vulnerability validation.

The goal is not to collect as much information as possible.

The goal is to understand the target and continuously answer:

> **What do I know?**
> **What don't I know yet?**
> **What is the next logical thing to investigate?**

A good reconnaissance process reduces uncertainty step by step.

---

## 2. Authorization and Scope

Before performing reconnaissance, confirm what is authorized.

### Scope

Identify:

* Target IP addresses
* Domains
* Subdomains
* Applications
* Networks
* Specific ports/services if restricted
* Testing time window, if applicable
* Activities that are prohibited

### Authorization

Only perform active testing against systems where permission has been provided.

Do not assume that a discovered asset is automatically in scope.

### Scope checklist

```text
[ ] Target is authorized
[ ] Target IP/domain is confirmed
[ ] In-scope assets are known
[ ] Out-of-scope assets are identified
[ ] Testing restrictions are understood
[ ] Evidence/documentation requirements are understood
```

---

# 3. Passive vs Active Reconnaissance

## Passive Reconnaissance

Passive reconnaissance collects information without directly interacting with the target infrastructure.

Examples:

* Search engines
* Public DNS information
* WHOIS/RDAP information
* Certificate transparency records
* Publicly available documentation
* Public repositories
* Publicly exposed information

### Goal

Build an initial picture of the target before direct interaction.

```text
Public information
       ↓
Possible assets
       ↓
Initial attack surface
       ↓
Questions for active reconnaissance
```

---

## Active Reconnaissance

Active reconnaissance involves directly interacting with an authorized target.

Examples:

* Host discovery
* Port scanning
* Service enumeration
* Version detection
* HTTP requests
* DNS queries against authorized infrastructure
* Directory/application discovery where permitted

### Goal

Confirm and expand information about the target.

Active reconnaissance should be controlled and documented.

---

# 4. Asset Discovery

Asset discovery identifies systems and resources belonging to the target.

Possible assets include:

```text
Domain
├── Subdomain
├── Web application
├── API
├── Mail server
├── DNS server
├── VPN
├── Cloud-hosted service
└── Other network hosts
```

### Questions

* What domains are associated with the target?
* Are there subdomains?
* What IP addresses are associated with discovered domains?
* Are multiple applications present?
* Are different services hosted on different systems?
* Are there assets that were not initially obvious?

Do not immediately assume every discovered asset is in scope.

---

# 5. Attack Surface

The attack surface is the collection of exposed interfaces, services, applications, and other points through which a system can be interacted with.

For a simple host:

```text
Host
│
├── 22/tcp → SSH
├── 80/tcp → HTTP
└── 443/tcp → HTTPS
```

For a web application:

```text
Application
│
├── Login
├── Registration
├── Search
├── File upload
├── API
├── Admin interface
└── Other endpoints
```

The attack surface becomes clearer as enumeration progresses.

---

# 6. Host Discovery

Host discovery determines which hosts are reachable or responding.

For an authorized network or lab, the objective is to answer:

```text
Which hosts exist?
Which hosts respond?
Which hosts should I investigate next?
```

Example reasoning:

```text
Network range
     ↓
Host discovery
     ↓
10.10.10.5  → discovered
10.10.10.8  → discovered
10.10.10.12 → discovered
     ↓
Enumerate discovered hosts
```

Record the discovery method and results.

---

# 7. Enumeration

Enumeration goes deeper than simple discovery.

The objective is to identify what is running and gather useful details about exposed services.

Typical information includes:

* Open ports
* Protocols
* Services
* Service versions
* Web servers
* Technologies
* DNS information
* SMB information
* SSH information
* FTP information
* Application endpoints

Example:

```text
Host: 10.10.10.5

22/tcp
└── SSH
    └── Version/details discovered

80/tcp
└── HTTP
    ├── Web server
    ├── Technology
    └── Application endpoints
```

Enumeration should create new questions rather than simply produce a list of ports.

---

# 8. Information Gathering

Information should be organized into useful categories.

## Target Information

```text
Target:
IP:
Domain:
Hostname:
Environment:
Scope:
```

## Network Information

```text
IP addresses:
Open ports:
Protocols:
Services:
Versions:
```

## Web Information

```text
Web server:
Technologies:
Pages:
Directories:
Parameters:
APIs:
Authentication:
Interesting functionality:
```

## Other Services

```text
DNS:
SSH:
FTP:
SMB:
Database:
Other:
```

The objective is to turn raw information into an understandable attack surface.

---

# 9. Note-Taking

Good notes should allow you to reconstruct what happened later.

For every important action, record:

```text
Time
Target
Command/action
Purpose
Result
Evidence
Next question
```

Example:

```text
Target: 10.10.10.5

Action:
Service enumeration

Purpose:
Identify exposed services.

Result:
HTTP and SSH were discovered.

Evidence:
screenshots/10.10.10.5-services.png

Next question:
What web application is running on port 80?
```

Avoid keeping only command lists.

A command without context does not explain your reasoning.

---

# 10. Evidence Collection

Evidence supports your findings and makes your work reproducible.

Useful evidence can include:

* Screenshots
* Command output
* HTTP responses
* URLs
* Relevant headers
* Service information
* DNS results
* Application behavior
* Timestamps

Example structure:

```text
evidence/
├── host-discovery.txt
├── services.txt
├── web/
│   ├── homepage.png
│   └── headers.txt
└── screenshots/
    └── interesting-finding.png
```

Only collect information that is relevant to the authorized assessment.

---

# 11. Recon → Enumeration → Validation

These stages should be treated as a progression.

## Reconnaissance

Find out what exists.

```text
What assets are associated with the target?
```

## Enumeration

Understand what is exposed.

```text
What services, applications, and technologies are present?
```

## Validation

Safely investigate an interesting finding.

```text
Does the suspected issue actually exist?
```

Do not jump directly from:

```text
"Port 80 is open"
```

to:

```text
"Try random exploits"
```

Instead:

```text
Port 80 open
     ↓
Identify web server/application
     ↓
Understand application structure
     ↓
Identify interesting functionality
     ↓
Form a specific hypothesis
     ↓
Safely validate the hypothesis
     ↓
Document result
```

---

# 12. The Unknowns-Driven Approach

At every stage, maintain two lists.

## Known

Information that has been confirmed.

```text
Known:
- Target IP: 10.10.10.5
- Host responds
- Port 22 is open
- Port 80 is open
- HTTP service is present
```

## Unknown

Information that still needs investigation.

```text
Unknown:
- SSH version
- Web server version
- Web technologies
- Application endpoints
- Authentication mechanism
```

Then choose the next action based on the most useful unknown.

```text
Known
  ↓
Unknown
  ↓
Prioritize unknown
  ↓
Investigate
  ↓
New information
  ↓
Update notes
  ↓
Repeat
```

This prevents random tool usage.

---

# 13. Decision-Making During Recon

When you discover something, ask:

### What does this tell me?

Example:

```text
Port 80 is open.
```

This tells you:

```text
A web service may be available.
```

### What does it not tell me?

```text
I don't yet know:
- Which web server?
- Which version?
- Which application?
- Which technologies?
- Which endpoints?
```

### What should I investigate next?

Choose the action that answers one of those questions.

---

# 14. Practical Recon Workflow

```text
1. Confirm authorization
        ↓
2. Define scope
        ↓
3. Passive reconnaissance
        ↓
4. Discover potential assets
        ↓
5. Confirm authorized targets
        ↓
6. Host discovery
        ↓
7. Port discovery
        ↓
8. Service/version enumeration
        ↓
9. Application/technology enumeration
        ↓
10. Map attack surface
        ↓
11. Identify interesting findings
        ↓
12. Form a hypothesis
        ↓
13. Safely validate
        ↓
14. Record evidence
        ↓
15. Update attack-surface map
        ↓
16. Decide the next logical investigation
```

---

# 15. Recon Rules

### Rule 1 — Know the scope

Never assume authorization.

### Rule 2 — Understand before attacking

Enumeration should come before vulnerability validation.

### Rule 3 — Do not blindly run tools

Every command should have a reason.

### Rule 4 — Record important findings immediately

Do not rely on memory.

### Rule 5 — Preserve evidence

Keep useful output and screenshots.

### Rule 6 — Follow the evidence

Let discoveries determine the next investigation.

### Rule 7 — Ask questions

Every discovery should lead to:

```text
What does this tell me?
What does it leave unknown?
What should I investigate next?
```

---

# 16. Week 5 Practical Goal

By the end of this topic, I should be able to take an authorized lab target and independently move through:

```text
Scope
  ↓
Recon
  ↓
Asset Discovery
  ↓
Host Discovery
  ↓
Enumeration
  ↓
Attack Surface
  ↓
Interesting Findings
  ↓
Safe Validation
  ↓
Evidence
  ↓
Documentation
```

The goal is not to memorize a fixed sequence of commands.

The goal is to develop the ability to decide:

> **What do I know?**
> **What don't I know?**
> **What is the next logical thing to investigate?**
