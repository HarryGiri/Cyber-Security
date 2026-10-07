# Structure of a Penetration Test

A penetration test follows a structured process from planning through
retesting.

## 1. Pre-Engagement

Before technical testing begins:

- Confirm authorization.
- Define scope.
- Agree on rules of engagement.
- Identify testing windows.
- Establish communication procedures.
- Confirm technical information and constraints.

## 2. Information Gathering

### Passive Reconnaissance

Collect information without directly interacting with target systems
where possible.

Examples can include:

- Public information
- DNS information
- Publicly available documents
- Organization and technology information

### Active Reconnaissance

Interact with the target to discover information.

Examples:

- Host discovery
- Port scanning
- Service enumeration
- Application discovery

## 3. Vulnerability Assessment

Analyze discovered systems and services for potential weaknesses.

The goal is to identify issues that may require further validation.

## 4. Exploitation

Safely validate selected vulnerabilities to determine whether they are
actually exploitable.

Testing should remain within the agreed scope and avoid unnecessary
impact.

## 5. Post-Exploitation

If access is obtained, determine the security impact and identify
possible additional attack paths.

The material describes this stage as understanding what an attacker
could achieve after initial compromise.

## 6. Lateral Movement

Where explicitly authorized, assess whether access to one system could
enable movement toward other systems.

## 7. Proof of Concept (PoC)

Evidence should demonstrate the finding clearly without causing
unnecessary harm.

A PoC can include:

- Relevant commands
- Screenshots
- Request/response evidence
- Output
- A concise explanation of the attack path

## 8. Post-Engagement

After testing:

- Organize evidence.
- Analyze findings.
- Prepare the report.
- Communicate results.

## 9. Remediation Support and Retesting

After remediation, retest relevant findings to determine whether they
have been fixed.

## Overall Process

``` text
Pre-Engagement
      ↓
Information Gathering
      ↓
Vulnerability Assessment
      ↓
Exploitation
      ↓
Post-Exploitation
      ↓
Lateral Movement
      ↓
PoC / Evidence
      ↓
Post-Engagement
      ↓
Remediation
      ↓
Retesting
```

## Key Point

A penetration test is a complete engagement lifecycle, not just
exploitation. Planning, scope, evidence, reporting, remediation, and
retesting are equally important parts of professional testing.
