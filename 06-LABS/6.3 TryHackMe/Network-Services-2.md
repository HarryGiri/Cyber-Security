# Network Services 2

| Field | Details |
|---|---|
| Platform | TryHackMe |
| Room | Network Services 2 |
| Difficulty | Easy |
| Category | Network Services / Enumeration / Exploitation |
| Status | Completed |

## Objective

Understand how NFS, SMTP, and MySQL work, how to enumerate these services, and how service misconfigurations can expose files, user information, and sensitive database contents.

The room covers network-service discovery, NFS shares and permissions, SMTP server enumeration, MySQL database enumeration, and the security implications of weak configurations and credential reuse.

---

## Task 1 — Get Connected

### What I Learned

This task introduces the room and prepares the environment for the practical exercises.

* Network services provide functionality such as file sharing, email delivery, and database access.
* Misconfigured services can expose sensitive information or provide unauthorized access.
* Enumeration helps identify the services available on a target and understand how they are configured.
* Linux command-line knowledge is useful when investigating network services.
* Practical testing should be performed only against the assigned TryHackMe target or another explicitly authorized environment.

### Environment Preparation

* Connect to the TryHackMe VPN when required by the lab.
* Deploy the target machine and allow it time to initialize.
* Identify the assigned target IP address.
* Use the target address provided by the active lab rather than assuming an address from an earlier session.

### Key Findings

The objective is to understand how network services work and recognize the security issues that can arise when they are exposed or misconfigured.

---

## Task 2 — Understanding NFS

### What I Learned

**NFS stands for Network File System.**

NFS allows a system to access files and directories located on a remote machine as though they were available through its local filesystem.

### How NFS Works

1. An NFS client requests access to a directory exported by a remote server.
2. The server and its export configuration determine whether the client is permitted to access the requested directory.
3. The server provides file handles that identify files and directories.
4. The client accesses remote resources through NFS requests.
5. Access permissions determine which operations the user can perform.

NFS uses Remote Procedure Call (RPC) mechanisms to facilitate communication between clients and servers.

### Important Concepts

* **Mounting:** Connecting a remote filesystem to a directory on the local machine.
* **Export:** A directory made available to NFS clients by the server.
* **File handle:** An identifier used to refer to a file or directory on the remote filesystem.
* **UID:** A user identifier used by the operating system.
* **GID:** A group identifier used by the operating system.
* **RPC:** Remote Procedure Call, a mechanism that allows a program to request operations from another system.

### NFS Compatibility

NFS can be used across different operating systems. For example, Linux, Unix, and macOS systems can access compatible NFS exports, and Windows Server can also provide NFS functionality.

NFS versions differ in their capabilities and security features. The appropriate version depends on the server, client, and environment.

### Key Findings

* NFS is a network-based file-sharing protocol.
* Mounting makes remote files accessible through a local directory.
* File handles identify remote files and directories.
* UID and GID information can influence permission checks.
* Exposing an NFS share too broadly can disclose sensitive files.
* Permissions and export configuration are important parts of NFS security.

---

## Task 3 — Enumerating NFS

### What I Learned

**Enumeration** is the process of gathering detailed information about a target system and its available services.

This may include:

* Open ports.
* Running services and their versions.
* Network shares.
* Accessible directories and files.
* Usernames and other account-related information.
* Configuration weaknesses that require further investigation.

The objective is to understand the available attack surface before deciding which findings need additional validation.

### Tools / Commands

### 1. Scan the target

```bash
nmap -sC -sV -p- -T4 -oA scan <TARGET_IP>
``

This command performs a full TCP port scan, uses Nmap's default scripts, attempts service-version detection, and saves output in multiple formats.

**Options explained:**

| Option | Purpose |
|---|---|
| `-sC` | Runs Nmap's default scripts. |
| `-sV` | Attempts to identify service versions. |
| `-p-` | Scans TCP ports 1–65535. |
| `-T4` | Uses a faster timing profile. |
| `-oA scan` | Saves results in multiple formats using `scan` as the base filename (for example, `.nmap`, `.gnmap`, and `.xml`). |

Replace `<TARGET_IP>` with the address of the assigned lab machine.

### 2. Enumerate NFS exports

```bash
/usr/sbin/showmount -e <TARGET_IP>
```

This command lists NFS exports advertised by the server.

The results help identify which remote directories may be available for mounting. An advertised export does not automatically mean that every client can access it successfully.

### 3. Create a local mount point

```bash
mkdir /tmp/mount
```

This creates a local directory that can serve as the mount point for the remote NFS share.

The `/tmp` directory is temporary, so its contents may not persist after a system restart.

### 4. Mount the NFS share

```bash
sudo mount -t nfs -o nolock <TARGET_IP>:/home /tmp/mount/
```

This command mounts the specified NFS export at the local directory.

| Component | Purpose |
|---|---|
| `sudo` | Runs the command with elevated local privileges. |
| `mount` | Mounts a filesystem. |
| `-t nfs` | Specifies NFS as the filesystem type. |
| `-o nolock` | Disables NLM locking for this mount. |
| `<TARGET_IP>:/home` | Specifies the server and exported directory. |
| `/tmp/mount/` | Specifies the local mount point. |

The export path should match the result observed during enumeration.

### 5. Exposed Private Keys

A private SSH key found in an unexpectedly accessible share is sensitive authentication material. Its exposure should be documented as a security finding in an authorized assessment. Do not copy, use, or disclose private keys unless the activity is explicitly authorized.

The permissions of private-key files should be restricted so that only the intended owner can access them. In an actual assessment, do not copy or use exposed keys unless that activity is explicitly authorized.

### SSH Authentication

SSH provides encrypted remote access. In the lab, the exposed key was discussed in the context of authentication. For this report, the command used to authenticate with the key is omitted; exposed private keys should be treated as sensitive evidence.

### Key Findings

* Full port scanning can identify services running on non-standard ports.
* `showmount` helps identify advertised NFS exports.
* A mounted share exposes remote files through the local filesystem.
* Sensitive files may be exposed if a share includes user home directories.
* SSH private keys must be protected with appropriate filesystem permissions.
* NFS permissions and export settings should be reviewed alongside the files accessible through the share.

---

## Task 4 — Exploiting NFS

### What I Learned

This task demonstrates how insecure NFS configuration can affect the security of the underlying system.

### Root Squashing

**Root squashing** is an NFS security feature that maps remote root-user requests to an unprivileged identity on the server.

Its purpose is to prevent a client-side root user from automatically receiving root-level access to files on the NFS server.

When root squashing is disabled or incorrectly configured, the server may trust client-side ownership or permission changes more than intended.

The exact impact depends on the export configuration, filesystem permissions, server implementation, and available access.

### SUID Permissions

**SUID stands for Set User ID.**

SUID is a special permission associated with executable files. When applicable, it allows a program to execute with the effective user identity of the file's owner rather than simply the identity of the user who launched it.

SUID is not inherently a vulnerability. However, a SUID executable that is incorrectly configured or unnecessarily privileged can create a security risk.

### How the Misconfiguration Connects

The room demonstrates the relationship between several security concepts:

1. An NFS share exposes files to a remote client.
2. The export's configuration affects how file ownership and permissions are handled.
3. Incorrect trust boundaries can allow unintended changes to shared files.
4. An executable with inappropriate ownership and special permissions may introduce a privilege-escalation risk.
5. The overall impact depends on the server configuration and the permissions available to the user.

The practical privilege-escalation commands have been omitted from this report.

### Key Findings

* Root squashing helps restrict remote root privileges on NFS exports.
* SUID changes the effective identity under which an executable runs.
* Writable NFS exports require careful permission and ownership controls.
* A misconfigured NFS export can affect the security of the host, not just the confidentiality of shared files.
* Root access should never be inferred from an NFS configuration alone; the actual impact depends on the complete configuration and execution context.

### Defensive Considerations

* Enable root squashing unless a documented, justified requirement dictates otherwise.
* Restrict exports to trusted clients and required directories.
* Avoid unnecessary write access to shared directories.
* Review ownership and special permissions on files stored in exports.
* Audit SUID executables and remove unnecessary special permissions.
* Monitor changes to sensitive shared files and executable permissions.

---

## Task 5 — Understanding SMTP

### What I Learned

**SMTP stands for Simple Mail Transfer Protocol.**

SMTP is used to send and relay email between clients and mail servers.

An email system commonly uses SMTP for outgoing messages and POP3 or IMAP for receiving or accessing stored messages.

### Responsibilities of an SMTP Server

An SMTP server generally:

* Accepts email submissions or messages from other mail servers.
* Processes and relays outgoing email.
* Communicates with other mail servers to deliver messages.
* Queues messages when a destination server is temporarily unavailable.
* Reports delivery problems when a message cannot be delivered.

### How SMTP Works

The simplified delivery process is:

1. An email client connects to its configured SMTP server.
2. The client and server establish an SMTP session.
3. The client submits the sender, recipient, message body, and any supported attachments.
4. The sending server determines how to route the message.
5. The message is relayed to the recipient's mail server.
6. If the destination is temporarily unavailable, the message may be queued for retry.
7. The recipient accesses the delivered message through the relevant mail service.

### SMTP, POP3, and IMAP

| Protocol | Main Purpose |
|---|---|
| SMTP | Sends or relays email. |
| POP3 | Retrieves email, commonly by downloading messages to a client. |
| IMAP | Provides access to and synchronizes messages stored on a mail server. |

### Default SMTP Port

SMTP commonly uses TCP port 25 for server-to-server mail transfer. Other ports, such as 587 and 465, are commonly used for message submission under different security configurations.

SMTP services can run on Linux and Windows systems.

### Key Findings

* SMTP handles outgoing email and message relay.
* POP3 and IMAP serve different purposes from SMTP.
* Email delivery can involve multiple mail servers.
* Mail queues allow temporary delivery failures to be handled.
* SMTP server configuration and software version can reveal information useful for security assessment.
* Mail servers should be configured to prevent unauthorized relay and unnecessary disclosure of user information.

---

## Task 6 — Enumerating SMTP

### What I Learned

SMTP enumeration involves collecting information about a mail server and understanding what information it reveals to clients.

The room introduces two types of SMTP enumeration.

### 1. Server Information

Identifying the mail-server software and version helps an assessor understand the target's configuration and determine whether further investigation is warranted.

Version information is only a starting point, not proof of a vulnerability. The installed version, patch level, configuration, and relevant security advisories must also be considered.

### 2. User Enumeration

Some SMTP servers support commands such as `VRFY` and `EXPN`, which may reveal information about valid users, aliases, or mailing lists.

Their availability and behavior depend on server configuration. Some servers restrict or disable these commands to reduce information disclosure.

### Tools and Commands Used

### 1. Port Scanning

```bash
nmap -sC -sV -p- <TARGET_IP>
```

Identifies open ports and attempts to determine the services and versions running on the target.

### 2. Start Metasploit

```text
msfconsole
```

Launches the Metasploit Framework console.

### 3. Search for the SMTP Version Module

```text
search smtp_version
```

Searches for a module associated with SMTP version detection.

### 4. Select the Module

```text
use 0
```

Selects module `0` from the search results.

### 5. View Module Options

```text
options
```

Displays the available configuration options and required parameters for the selected module.

### 6. Configure the Target

```text
set rhosts <TARGET_IP>
```

Sets the target IP address using the `RHOSTS` parameter.

### 7. Run the Module

```text
exploit
```

Executes the selected module to retrieve available SMTP server information, such as its mail name.

### 8. Search for the SMTP Enumeration Module

```text
search *smtp_enum*
```

Searches for modules associated with SMTP user enumeration.

### 9. Configure the Username Wordlist

```text
set user_file /usr/share/wordlists/SecLists/Usernames/top-usernames-shortlist.txt
```

Specifies the username wordlist used by the enumeration module.

### 10. Configure the Target

```text
set rhosts <TARGET_IP>
```

Specifies the target system for the SMTP enumeration module.

### 11. Run the Enumeration Module

```text
run
```

Executes the selected module to check whether the SMTP service reveals information about valid usernames.

### Key Findings

- SMTP enumeration can reveal server software, version information, and configuration details.
- Commands such as `VRFY` and `EXPN` may disclose user-related information when supported and permitted by the server.
- Metasploit provides modules for examining SMTP services and testing for user-information disclosure.
- Server banners and version information should be verified before drawing conclusions about vulnerabilities.
- SMTP servers should disclose only the information necessary for their intended function.
- Username enumeration findings can have privacy and account-security implications.

## Task 7 — Exploiting SMTP

### What I Learned

After completing SMTP enumeration, we have gathered information that can help guide further security testing:

1. A username identified during SMTP enumeration.
2. Information about the SMTP server and operating system.
3. Details about other open services discovered during port scanning.

The room uses this information to examine SSH authentication security. Hydra is introduced as a tool for testing network login credentials using password wordlists.

### Tools Used

| Tool | Purpose |
|---|---|
| Hydra | Network authentication testing |
| SSH | Encrypted remote access to a system |
| Kali Linux / Parrot OS | Security testing environments |
| Wordlists | Collections of candidate passwords used in authorized password testing |

### Preparation

Before moving from enumeration to the next stage, exit the Metasploit console and review the information collected during the previous task.

Keeping the discovered username, service information, and target details organized helps maintain a clear assessment workflow.

### Understanding Hydra

Hydra is a network login-testing tool that supports multiple services and protocols, including SSH.

It can perform dictionary-based authentication testing using a supplied username and password list.

Kali Linux and Parrot OS commonly include Hydra and provide wordlists under:

```text
/usr/share/wordlists/
```

Additional wordlists, such as SecLists, provide collections useful for different security-testing activities.

### Understanding the Command Parameters

The room introduces several Hydra parameters:

| Parameter | Purpose |
|---|---|
| `hydra` | Starts the Hydra tool |
| `-t` | Specifies the number of parallel tasks |
| `-l` | Specifies a single username |
| `-P` | Specifies a password-list file |
| `-vV` | Enables detailed output during testing |
| Target IP | Identifies the system being tested |
| `ssh` | Specifies SSH as the target protocol |

These parameters help explain how Hydra is configured for authentication testing. Password-testing activity should only be performed against systems within an explicitly authorized scope.

### Reviewing the SSH Service

SSH provides encrypted remote access to a system. In this task, the SSH service is examined after information has been collected through SMTP enumeration.

The purpose is to understand how information gathered during reconnaissance and enumeration can inform subsequent authentication-security testing.

### Reading the Lab File

After successfully accessing the lab system, the following command is used to display the contents of `smtp.txt`.

```bash
cat smtp.txt
```

**Explanation:** Displays the contents of the specified text file in the terminal.

### Key Findings

- SMTP enumeration can reveal usernames and information about a mail server.
- Enumeration results can help guide later stages of a security assessment.
- Hydra supports authentication testing across multiple network protocols.
- Password wordlists are commonly used in dictionary-based authentication testing.
- SSH provides encrypted remote access and should be protected with strong authentication controls.
- Password reuse can increase risk when credentials are exposed.
- Authentication testing must remain within the authorized assessment scope.
---


---



## 1. What Is MySQL?

MySQL is a **Relational Database Management System (RDBMS)** that uses Structured Query Language (SQL) to manage data.

It is commonly used as the database component of web applications.

### 2. Important Concepts

| Term | Explanation |
|---|---|
| Database | An organized collection of structured data stored for persistent use. |
| RDBMS | Software that creates and manages relational databases. |
| SQL | Structured Query Language, used to interact with relational databases. |
| Table | A structure that stores related data in rows and columns. |
| Primary key | A field used to uniquely identify a record in a table. |
| MySQL server | Processes database requests and returns results. |
| MySQL client | Connects to the server and sends database requests. |

### 3. Client–Server Architecture

MySQL follows a client–server model:

1. The client connects to the MySQL server.
2. The client sends an SQL statement.
3. The server processes the request.
4. The server returns the result to the client.

The server manages the databases, while the client provides an interface for interacting with them.

### 4. MySQL in Web Applications

MySQL is frequently used to store application data, including user information and website content.

It is also part of the **LAMP stack**:

- **L:** Linux
- **A:** Apache
- **M:** MySQL
- **P:** PHP

MySQL can run on both Linux and Windows.

---

### Task 9 — Enumerating MySQL

### 1. Identify the Service

During network enumeration, identify open ports and determine which services are running.

MySQL commonly uses TCP port `3306`. However, the service may be configured to use a different port.

The following command performs service and version detection across all TCP ports on the authorized lab target:

```bash



**Command breakdown:**

| Option | Purpose |
|---|---|
| `-sC` | Runs Nmap's default scripts. |
| `-sV` | Attempts to identify service versions. |
| `-p-` | Scans all TCP ports. |

Replace `<TARGET_IP>` with the IP address of your authorized lab machine.

### 2. Install the MySQL Client

On a Debian-based system, the MySQL client can be installed using:

```bash



The client allows you to connect to a MySQL server and interact with databases.

### 3. Connect to MySQL

The general connection syntax is:

```bash



**Parameters:**

| Parameter | Purpose |
|---|---|
| `-h` | Specifies the MySQL server's hostname or IP address. |
| `-u` | Specifies the database username. |
| `-p` | Prompts for the user's password. |

A successful connection depends on valid credentials, network accessibility, and the server's authentication configuration.

### 4. Enumerate the Service

During MySQL enumeration, establish what can be learned from the service and the permissions available to the account.

Useful areas to investigate include:

- MySQL version.
- Accessible databases.
- Database and table structure.
- Account permissions.
- Whether the service exposes information that should be restricted.

MySQL enumeration should remain within the authorized scope of the assessment.

### 5. Query Execution

SQL statements allow clients to request information from a database.

For example, the following query requests the MySQL server version:

```sql



The result can help identify the server version for documentation and follow-up security research.

A Metasploit MySQL SQL-execution module is another method discussed in the room. The important concept is that database queries can be issued through a suitable client or authorized testing tool, depending on the available access and configuration.


### Task 10 — Exploiting MySQL

## 1. Review the Information Collected

Before assessing the security of a MySQL service, organize the information obtained during enumeration:

- Confirmed service and version.
- Authentication requirements.
- Databases visible to the account.
- Available database permissions.
- Potential exposure of sensitive information.

The impact of a database weakness depends on the permissions and data accessible to the account.

### 2. Database Schemas

A **schema** describes the organization of database objects, such as tables and their relationships.

In MySQL, the terms **schema** and **database** are commonly used interchangeably.

Understanding a schema helps an assessor determine how data is organized and identify whether access permissions are appropriate.

### 3. Password Hashes

A hash is produced by applying a hashing function to input data, resulting in a fixed-length output for a given hashing algorithm.

Applications may store password hashes instead of plaintext passwords. However, hashes must still be protected because exposure can create a risk of password recovery or account compromise.

**Important distinction:**

- A password is the original secret used for authentication.
- A password hash is the output of a hashing function.
- A hash is not automatically encrypted data; hashing and encryption are different processes.

### 4. Database Permissions and Sensitive Data

A database account should have only the permissions required for its role.

Excessive permissions can increase the impact of a compromised account. Depending on the account's access, a weakness could expose database structure or sensitive records.

During an authorized assessment, document the permissions and potential impact without unnecessarily collecting or disclosing sensitive information.

### 5. Security Lessons

The MySQL assessment highlights several important security practices:

- Restrict database access to trusted systems and users.
- Use strong, unique credentials.
- Apply the principle of least privilege.
- Avoid reusing passwords across services.
- Protect password hashes and other authentication data.
- Keep MySQL and its supporting software updated.
- Monitor database access and authentication attempts.
- Avoid exposing sensitive database information in reports or public repositories.

### 6. Evidence and Reporting


### Key Takeaways

- MySQL is a relational database management system that uses SQL.
- MySQL commonly listens on TCP port `3306`.
- Nmap can help identify exposed services and their versions.
- The MySQL client provides a way to connect to a database server.
- Enumeration helps establish which information and operations are accessible.
- Database schemas describe the organization of database objects.
- Excessive database permissions and exposed authentication data can create security risks.
- Strong authentication, least privilege, restricted network access, and appropriate monitoring help secure MySQL.

---

## Task 11 — Further Learning

### What I Learned

The final task points toward further reading on security vulnerabilities and system hardening.

The most important concepts from the room are connected:

* **NFS:** Shared filesystem permissions and export configuration can affect host security.
* **SMTP:** Mail-server configuration can reveal information about the service and its users.
* **MySQL:** Database permissions and exposed credentials can put stored information at risk.
* **Enumeration:** Understanding the available services and their configuration helps identify potential security issues.
* **Credential security:** Weak or reused passwords can increase the impact of a compromise.
* **Least privilege:** Services and accounts should receive only the permissions they need.

### Resources From the Room

- [Red Hat Security Guide — Exploits](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/security_guide/ch-exploits)
- [MySQL Server Documentation](https://dev.mysql.com/doc/)
- [Nmap Documentation](https://nmap.org/docs.html)

### Key Findings

The room illustrates why network services must be assessed as part of the broader system rather than in isolation.

An exposed service may disclose information, provide access to files, or allow access to data that should be protected. The actual impact depends on the service configuration, permissions, authentication controls, and the sensitivity of the accessible information.

---

## Main Tools Used

The following tools and clients appear in the attached notes:

| Tool | Purpose |
|---|---|
| Nmap | Port scanning and service/version detection. |
| `showmount` | Listing advertised NFS exports. |
| `mount` | Mounting an NFS share. |
| `chmod` | Changing filesystem permissions. |
| SSH | Encrypted remote administration and authentication. |
| Metasploit Framework | Service-enumeration modules and security testing. |
| MySQL client | Connecting to an authorized MySQL server. |

Some commands from the original document were intentionally excluded because they perform credential guessing, extract sensitive authentication data, or demonstrate privilege escalation.

---

### What I Learned

I learned how NFS, SMTP, and MySQL work and how their configurations can affect system security.

The NFS tasks demonstrated how remote shares expose files and how export permissions, root squashing, and SUID permissions relate to host security.

The SMTP tasks demonstrated how mail servers deliver messages, how server information can be enumerated, and why user-information disclosure and weak authentication controls matter.

The MySQL tasks demonstrated the client-server database model, the purpose of SQL, the role of schemas, and the risks associated with excessive database privileges and exposed password hashes.

The central lesson was that **enumeration provides the context needed to understand and assess a service's security**. Identifying an open port is only the beginning; an assessor must also understand the service, its configuration, its access controls, and the potential impact of any weakness.

## Mistakes / Things I Didn't Understand

* Needed to understand the difference between an NFS export and a local mount point.
* Learned how mounting an NFS share makes remote files accessible through the local filesystem.
* Needed to understand the purpose of file handles, UIDs, and GIDs in NFS.
* Needed to understand how SUID permissions affect executable behavior.
* Learned the difference between SMTP, POP3, and IMAP.
* Needed to understand how SMTP enumeration can disclose service or user information.
* Learned why credentials discovered in one context can pose a risk to other services when reused.


## Room

[TryHackMe — Network Services 2](https://tryhackme.com/room/networkservices2)
