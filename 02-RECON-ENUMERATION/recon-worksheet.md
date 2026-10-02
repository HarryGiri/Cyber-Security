# Reconnaissance Worksheet

> Use this worksheet only for authorized labs, systems, and assessments.

---

# 1. Assessment Information

| Field           | Details |
| --------------- | ------- |
| Target / Lab    |         |
| Date            |         |
| Tester          |         |
| Assessment Type |         |
| Authorization   |         |
| Scope           |         |
| Out of Scope    |         |
| Time Window     |         |

---

# 2. Scope

## In-Scope Targets

```text
IP addresses:
Domains:
Subdomains:
Applications:
Networks:
Other:
```

## Out-of-Scope Targets

```text
-
-
-
```

## Restrictions

```text
-
-
-
```

---

# 3. Initial Questions

Before starting, record what is already known.

### What do I know?

```text
-
-
-
```

### What don't I know?

```text
-
-
-
```

### What do I need to discover first?

```text
-
-
-
```

---

# 4. Passive Reconnaissance

## Information Sources

| Source | Information Found | Relevant? | Evidence |
| ------ | ----------------- | --------- | -------- |
|        |                   |           |          |
|        |                   |           |          |
|        |                   |           |          |

## Discovered Assets

| Asset | Type | Source | In Scope? | Notes |
| ----- | ---- | ------ | --------- | ----- |
|       |      |        |           |       |
|       |      |        |           |       |
|       |      |        |           |       |

### Passive Recon Notes

```text
-
-
-
```

---

# 5. Asset Inventory

| Asset | IP / Domain | Type | Status | Notes |
| ----- | ----------- | ---- | ------ | ----- |
|       |             |      |        |       |
|       |             |      |        |       |
|       |             |      |        |       |

### Questions

```text
What assets are confirmed?

-

What assets still need confirmation?

-

Are there any potentially related assets?

-
```

---

# 6. Host Discovery

## Method / Command

```text
Command:
```

### Results

| Host | Status | Notes |
| ---- | ------ | ----- |
|      |        |       |
|      |        |       |
|      |        |       |

### Evidence

```text
Evidence file:
Screenshot:
Output:
```

### New Questions

```text
-
-
-
```

---

# 7. Port & Service Enumeration

## Target

```text
IP / Hostname:
```

## Results

| Port | Protocol | Service | Version / Details | Notes |
| ---- | -------- | ------- | ----------------- | ----- |
|      |          |         |                   |       |
|      |          |         |                   |       |
|      |          |         |                   |       |

### Command / Method

```text
```

### Evidence

```text
-
-
```

---

# 8. Service-Specific Enumeration

## HTTP / HTTPS

```text
URL:
Web server:
Version:
Technology:
Title:
Interesting endpoints:
Parameters:
Authentication:
Other findings:
```

### Questions

```text
-
-
-
```

---

## DNS

```text
Domain:
Nameservers:
Records:
Subdomains:
Other findings:
```

### Questions

```text
-
-
-
```

---

## SSH

```text
Port:
Version:
Authentication information:
Other findings:
```

### Questions

```text
-
-
-
```

---

## FTP

```text
Port:
Version:
Anonymous access:
Interesting files:
Other findings:
```

### Questions

```text
-
-
-
```

---

## SMB

```text
Port:
Version:
Shares:
Users:
Other findings:
```

### Questions

```text
-
-
-
```

---

## Other Service

```text
Service:
Port:
Version:
Information:
Interesting findings:
```

---

# 9. Attack Surface Map

Update this as new information is discovered.

```text
TARGET
│
├── Host:
│   ├── Port:
│   │   └── Service:
│   │       └── Interesting information:
│   │
│   └── Port:
│       └── Service:
│           └── Interesting information:
│
└── Other assets:
    ├──
    └──
```

---

# 10. Known vs Unknown

## What I Know

```text
1.
2.
3.
4.
5.
```

## What I Don't Know

```text
1.
2.
3.
4.
5.
```

## Next Logical Questions

```text
1.
2.
3.
4.
5.
```

---

# 11. Interesting Findings

Record findings that deserve further investigation.

| Finding | Why Interesting? | Evidence | Next Step |
| ------- | ---------------- | -------- | --------- |
|         |                  |          |           |
|         |                  |          |           |
|         |                  |          |           |

Do not automatically treat an interesting finding as a vulnerability.

---

# 12. Hypothesis

For each interesting finding:

### Observation

```text
What did I observe?

-
```

### Hypothesis

```text
What do I think might be happening?

-
```

### Reasoning

```text
Why do I think this?

-
```

### Validation

```text
What authorized, safe test can confirm or reject the hypothesis?

-
```

### Result

```text
Confirmed / Not confirmed / Inconclusive

Details:
-
```

---

# 13. Evidence Log

| Evidence ID | Type | Description | Location |
| ----------- | ---- | ----------- | -------- |
| E-001       |      |             |          |
| E-002       |      |             |          |
| E-003       |      |             |          |
| E-004       |      |             |          |

### Evidence Naming

Use clear names such as:

```text
E-001-host-discovery.txt
E-002-service-enumeration.txt
E-003-web-homepage.png
E-004-interesting-finding.png
```

---

# 14. Command Log

| # | Time | Target | Command / Action | Purpose | Result |
| - | ---- | ------ | ---------------- | ------- | ------ |
| 1 |      |        |                  |         |        |
| 2 |      |        |                  |         |        |
| 3 |      |        |                  |         |        |
| 4 |      |        |                  |         |        |

Avoid recording commands without explaining why they were used.

---

# 15. Investigation Log

Use this to track the reasoning process.

| Step | What I Know | What I Don't Know | Next Action | Result |
| ---- | ----------- | ----------------- | ----------- | ------ |
| 1    |             |                   |             |        |
| 2    |             |                   |             |        |
| 3    |             |                   |             |        |
| 4    |             |                   |             |        |
| 5    |             |                   |             |        |

---

# 16. Findings Summary

## Confirmed Information

```text
-
-
-
```

## Potential Findings

```text
-
-
-
```

## Validated Findings

```text
-
-
-
```

## Inconclusive Findings

```text
-
-
-
```

---

# 17. Final Attack Surface

```text
Target
│
├── Host(s)
│   ├── Service(s)
│   │   ├── Version
│   │   └── Interesting information
│   │
│   └── Web/Application
│       ├── Endpoint
│       ├── Functionality
│       └── Interesting finding
│
└── Other discovered assets
```

---

# 18. Final Questions

Before finishing the reconnaissance phase:

```text
[ ] Did I confirm the scope?
[ ] Did I document the authorized target?
[ ] Did I identify relevant assets?
[ ] Did I identify reachable hosts?
[ ] Did I enumerate exposed services?
[ ] Did I identify relevant technologies?
[ ] Did I map the attack surface?
[ ] Did I record interesting findings?
[ ] Did I preserve useful evidence?
[ ] Did I document my reasoning?
[ ] Did I distinguish observations from assumptions?
[ ] Did I validate findings safely?
[ ] Do I know what remains unknown?
[ ] Did I identify the next logical investigation?
```

---

# 19. Final Mental Check

```text
What do I know?
        ↓
What don't I know?
        ↓
Why does that unknown matter?
        ↓
What is the safest/logical way to investigate it?
        ↓
What did I discover?
        ↓
What evidence supports it?
        ↓
What should I investigate next?
```

> **Good reconnaissance is not about running more tools.**
>
> **It is about asking better questions and reducing uncertainty systematically.**
