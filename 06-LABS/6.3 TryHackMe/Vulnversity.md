# Vulnversity

## Lab Information

| Field | Details |
|---|---|
| **Platform** | TryHackMe |
| **Category** | Web Application Penetration Testing / Linux Privilege Escalation |
| **Difficulty** | Easy |
| **Status** | Completed |  
| **Write-up (with images)** | https://medium.com/@harrygiri1614/thm-vulnversity-write-up-0204f08b6346?postPublishedType=initial |


## Objective

Complete an authorized, guided assessment of the Vulnversity lab machine. The exercise covers machine deployment, network reconnaissance, web directory enumeration, file-upload security testing, access to the web server, and Linux privilege-escalation analysis.

```text
Machine Deployment
       ↓
Nmap Reconnaissance
       ↓
Gobuster Directory Enumeration
       ↓
File-Upload Testing
       ↓
Web Server Access
       ↓
Linux Privilege Escalation
```

---

# 1. Task 1 — Deploy the Machine 

## Activities

- Started the attacker environment.
- Deployed the Vulnversity lab machine.
- Confirmed that the attacker machine could reach the target through the lab network.


---

# 2. Task 2 — Reconnaissance

## Objective

Identify the services exposed by the target and collect initial information about the system.


### Command Used

```bash
nmap -sV MACHINE_IP
```

The `-sV` option attempts to identify the versions of services running on discovered open ports.

### Useful Nmap Options

| Option | Description |
|---|---|
| `-sV` | Attempts to determine service versions. |
| `-p <port>` | Scans a specific port. |
| `-p-` | Scans all TCP ports. |
| `-Pn` | Skips host discovery and treats the target as online. |
| `-A` | Enables OS detection, version detection, script scanning, and traceroute. |
| `-sC` | Runs Nmap's default script set. |
| `-v` | Enables verbose output. |
| `-sU` | Performs a UDP scan. |
| `-sS` | Performs a TCP SYN scan. |


## Key Findings

- Identified the target's open ports and associated services.
- Used service-version information to understand the exposed network surface.
- Identified the web service and the port on which it was running.
- Collected information that helped form an initial picture of the target operating system.

*Machine-specific answers and flags are intentionally omitted.*

---

# 3. Task 3 — Locating Directories Using Gobuster

## Objective

Discover directories and web resources that are not immediately visible through normal website navigation.


Gobuster is a directory and file discovery tool. It can also be used for DNS subdomain and virtual-host discovery. In this task, it was used for web directory enumeration.
   
### Command Used

```bash
gobuster dir -u http://MACHINE_IP:3333 -w /path/to/wordlist
```

Replace `MACHINE_IP` and the wordlist path with the values appropriate to the assigned lab environment.

### Useful Gobuster Options

| Option | Description |
|---|---|
| `-e` | Prints full URLs in the output. |
| `-u` | Specifies the target URL. |
| `-w` | Specifies the wordlist to use. |
| `-U` | Specifies a username for HTTP Basic Authentication. |
| `-P` | Specifies a password for HTTP Basic Authentication. |
| `-p` | Specifies a proxy to use for requests. |
| `-c` | Specifies cookies to use in requests. |

## Wordlists

A wordlist provides candidate directory or file names for Gobuster to check. Kali Linux includes commonly used wordlists under:

```text
/usr/share/wordlists/
```

The selected wordlist should be appropriate for the target and the scope of the assessment.


## Key Findings

- Used Gobuster to enumerate the web server.
- Identified a directory containing a file-upload form.  
- Discovered paths can expose upload forms, administrative pages, and other areas that require further review.
- Recognized the upload functionality as an important part of the application's attack surface.


---

# 4. Task 4 — Compromise the Web Server

## Objective

Understand how insecure file-upload validation can allow an application to accept executable server-side content.

### Burp suite

Burp Suite is a web application security testing platform. Its Proxy feature can intercept and inspect HTTP requests, while Intruder can automate controlled changes to selected request parameters.

### File-Upload Testing

The lab used Burp Suite Intruder to examine how the upload functionality handled different file extensions.

The extension examples supplied in the room were:

```text
.php
.php3
.php4
.php5
.phtml
```

The purpose of this exercise was to understand whether the server relied on an incomplete extension blocklist.

### Concepts Practised

- Intercepting an upload request using Burp Suite Proxy.
- Sending a captured request to Intruder.
- Identifying the filename extension in the request.
- Understanding how a Sniper-style payload position tests one selected position at a time.
- Comparing the application's responses to different file types.

## Reverse Shell

A reverse shell is a remote command-line connection initiated from the target system back to a listening machine. In this lab, the uploaded server-side file demonstrated how an unsafe upload location and server-side execution could lead to remote command execution.

The listener used during the exercise was:

```bash
nc -lvnp 1234
```

The lab involved configuring the test payload for the authorized lab network, uploading it through the discovered form, and observing the resulting connection.

> **Safety and scope:** Reverse-shell testing should only be performed in an isolated lab or on systems for which explicit authorization has been provided. Do not upload or execute payloads on public or third-party systems.


## Key Findings

- Tested the upload functionality with different file-extension cases.
- Observed that the application's validation did not adequately account for alternative executable extensions.
- Demonstrated in the lab how unsafe handling of uploaded server-side content can lead to command execution.
- Identified the web-server account context used by the resulting process.  
- Client-side checks are not sufficient; validation must be enforced by the server.
- Uploaded files should not be stored in a location where the web server can execute them.


---

# 5. Task 5 — Privilege Escalation

## Objective

Understand how an incorrectly configured SUID executable can provide an opportunity for local privilege escalation on a Linux system.

## Understanding SUID

SUID stands for **Set User ID**. It is a special permission that can cause an executable to run with the permissions of the file's owner rather than the permissions of the user who launched it.

For example, some system utilities require elevated permissions to perform their intended functions. The `passwd` utility is a common example because changing account credentials involves protected system files.

An unexpected or unnecessary SUID permission on an executable can create a security risk.

## SUID Enumeration

The task involved searching the target system for SUID-enabled files and reviewing the results to identify an unusual executable.

The important part of this process was not simply finding files with the SUID bit, but understanding:

- Which executable had the special permission.
- Whether that permission was expected.
- Which user owned the executable.
- Whether the executable's behaviour could be misused to obtain privileges beyond those intended.

## GTFOBins Research — systemctl

During this task, I identified `/bin/systemctl` as the executable requiring further investigation and consulted GTFOBins to understand the security implications of its configuration.

GTFOBins documents how certain Unix binaries may be abused when they are available with unsafe permissions or in an insecure execution context.

The key learning point was that a privileged utility can become a privilege-escalation path when its permissions and usage are not properly controlled.

## Key Findings

- Enumerated SUID-enabled files on the target.
- Identified `/bin/systemctl` as the unusual executable investigated during the lab.
- Researched its behaviour using GTFOBins.
- Confirmed the privilege-escalation concept within the authorized TryHackMe environment.


---

# 6. Tools Used

| Tool | Purpose |
|---|---|
| **Nmap** | Network scanning, open-port discovery, and service-version detection. |
| **Gobuster** | Web directory and file enumeration. |
| **Burp Suite** | Intercepting and inspecting HTTP requests and testing upload handling. |
| **Netcat** | Observing the lab's reverse connection. |
| **GTFOBins** | Researching the security implications of Unix binaries and permissions. |
| **Linux command-line utilities** | Inspecting the target environment and reviewing system configuration. |

---

# 7. Vulnerabilities and Security Weaknesses Studied

| Area | Security Weakness | Potential Impact |
|---|---|---|
| Network exposure | Unnecessary or insufficiently reviewed open services | Increased attack surface. |
| Web directory exposure | Discoverable application paths | Exposure of functionality that may require additional security review. |
| File upload | Incomplete file-extension validation | Upload of file types that the application did not intend to accept. |
| Server-side file handling | Uploaded executable content stored in an executable web location | Potential server-side code execution. |
| Linux permissions | Risky SUID configuration | Potential local privilege escalation. |
| Privileged utilities | Insecurely configured or exposed system binaries | Possible misuse of elevated execution privileges. |

---

# 8. Remediation and Defensive Recommendations

## Network Services

- Disable services that are not required.
- Restrict exposed services to trusted networks and authorized users.
- Keep network services updated.
- Review scan results and investigate unexpected open ports.

## Web Directory Exposure

- Avoid exposing sensitive administrative or internal resources unnecessarily.
- Enforce authentication and authorization on restricted functionality.
- Review web-server configuration and access controls.
- Monitor for unexpected access to sensitive paths.

## File Upload Security

- Use a strict allowlist of permitted file types.
- Validate file extensions and inspect file content on the server.
- Do not rely on the browser's HTML `accept` attribute as a security control.
- Generate server-side filenames rather than trusting user-supplied names.
- Store uploaded files outside the web root where possible.
- Ensure uploaded files cannot be interpreted as executable server-side code.
- Apply file-size limits and appropriate access controls.

## Linux SUID Configuration

- Audit SUID-enabled executables regularly.
- Remove unnecessary SUID permissions.
- Ensure privileged utilities are owned by trusted system accounts.
- Keep the operating system and installed packages updated.
- Apply least privilege and monitor unexpected privileged execution.

---

# 9. Key Takeaways

- Reconnaissance should be completed before moving into deeper testing.
- Nmap helps identify exposed services and provides useful service-version information.
- Directory enumeration can reveal functionality that is not immediately visible through normal website navigation.
- File-upload functionality requires strict server-side validation.
- Client-side restrictions should never be treated as the only security control.
- Alternative executable file extensions must be considered when designing upload validation.
- Unsafe handling of uploaded files can create a path to server-side code execution.
- Linux privilege escalation requires systematic enumeration of permissions and system configuration.
- SUID permissions should be applied only where they are genuinely required.
- GTFOBins is a useful reference for understanding the security implications of Unix binaries.
- A good penetration-testing report records the methodology, evidence, impact, and remediation—not just the fact that a task was completed.

---



## Lab Direct Link

TryHackMe — Vulnversity: https://tryhackme.com/room/vulnversity
