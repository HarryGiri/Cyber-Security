# Lab Documentation Guide

Use the appropriate documentation level instead of writing a full report for every lab.

## 🟢 Level 1 — Quick Lab Note

Use for:

- Small TryHackMe rooms
- Simple introductory labs
- Basic exercises
- Labs where the main goal is learning one concept

Include:

- Objective
- What I did
- Important commands
- Key findings
- What I learned
- Mistakes / questions

**Target:** 5–15 minutes.

## 🟡 Level 2 — Technical Lab Write-Up

Use for:

- Important TryHackMe rooms
- Pentesting methodology labs
- Privilege escalation labs
- Enumeration-heavy labs
- Labs that teach multiple techniques

Include:

1. Overview
2. Objective
3. Environment
4. Reconnaissance
5. Enumeration
6. Findings
7. Validation
8. Exploitation where applicable
9. Privilege escalation where applicable
10. Evidence
11. Impact
12. Remediation
13. Lessons learned

## 🔴 Level 3 — Vulnerability Write-Up

Use primarily for:

- PortSwigger
- Important web-security labs
- Web/API vulnerabilities

Focus on:

> **Vulnerability → Root Cause → Testing → Validation → Impact → Remediation**

Avoid simply reproducing the platform's solution.

## 🔵 Level 4 — Assessment-Style Write-Up

Use for:

- HTB machines
- Major practical labs
- Personal security labs
- Larger assessment projects

### Assessment Flow

```text
Scope
  ↓
Recon
  ↓
Enumeration
  ↓
Attack Surface
  ↓
Finding
  ↓
Validation
  ↓
Initial Access
  ↓
Privilege Escalation
  ↓
Impact
  ↓
Remediation
  ↓
Lessons Learned
```

# Platform-Specific Documentation

### TryHackMe

- Small room → Level 1
- Important room → Level 2

### PortSwigger

- Individual lab → Level 3

### HTB Academy

Do NOT create one report per theory section.

Create knowledge notes grouped by:

- Linux
- Windows
- Networking
- Active Directory
- Web
- Enumeration
- Privilege Escalation

### HTB Machines

Use Level 4.

### OverTheWire

Use a short Level 1-style note.
