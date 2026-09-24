# Nmap

**Platform:** TryHackMe
**Category:** Recon / Networking / Enumeration
**Difficulty:** Easy
**Status:** ✅ Completed

## 🎯 Objective

Learn the fundamentals of Nmap for port scanning, service enumeration, host discovery, NSE scripting, firewall evasion, and different TCP/UDP scanning techniques.

## 🔍 What I Did

* Learned why port scanning is an important first step in network enumeration.
* Learned how ports are used to direct network traffic to services.
* Performed TCP Connect, SYN, UDP, NULL, FIN, and Xmas scans.
* Learned how Nmap determines whether ports are open, closed, or filtered.
* Learned how UDP scanning differs from TCP scanning.
* Performed host discovery using ping sweeps.
* Learned about Nmap timing templates and scan performance.
* Used NSE scripts for automated enumeration.
* Learned how to search for installed NSE scripts.
* Learned about firewall evasion techniques such as `-Pn`.
* Used service/version and OS detection options.
* Practiced saving scan results in different formats.
* Used Wireshark to understand TCP Connect scan traffic.
* Used the `ftp-anon` NSE script to test anonymous FTP access.

## 🛠️ Tools / Commands

```bash
# Basic scan
nmap MACHINE_IP

# TCP Connect scan
nmap -sT MACHINE_IP

# SYN scan
sudo nmap -sS MACHINE_IP

# UDP scan
sudo nmap -sU MACHINE_IP

# NULL scan
sudo nmap -sN MACHINE_IP

# FIN scan
sudo nmap -sF MACHINE_IP

# Xmas scan
sudo nmap -sX MACHINE_IP

# Host discovery / ping sweep
nmap -sn 172.16.0.0/16

# Skip host discovery
nmap -Pn MACHINE_IP

# OS detection
sudo nmap -O MACHINE_IP

# Service/version detection
nmap -sV MACHINE_IP

# Verbosity
nmap -v MACHINE_IP
nmap -vv MACHINE_IP

# Save results in 3 formats
nmap MACHINE_IP -oA scan

# Normal output
nmap MACHINE_IP -oN scan.txt

# Grepable output
nmap MACHINE_IP -oG scan.txt

# Aggressive scan
nmap -A MACHINE_IP

# Timing
nmap -T5 MACHINE_IP

# Specific port
nmap -p 80 MACHINE_IP

# Port range
nmap -p 5000-5500 MACHINE_IP

# All ports
nmap -p- MACHINE_IP

# Top UDP ports
nmap -sU --top-ports 20 MACHINE_IP

# NSE script
nmap --script <script-name> MACHINE_IP

# Vulnerability scripts
nmap --script vuln MACHINE_IP

# FTP anonymous login check
nmap --script ftp-anon -p 21 MACHINE_IP

# Minimum parallel probes
nmap --min-parallelism 64 MACHINE_IP

# Append random data
nmap --data-length <number> MACHINE_IP
```

## 💡 Key Findings / Concepts

* A computer has **65,535 TCP/UDP ports** available.
* Ports allow multiple network services to operate on the same host.
* Common services are often associated with standard ports, but services can run on non-standard ports.
* **TCP Connect (`-sT`)** completes the TCP three-way handshake.
* **SYN (`-sS`)** performs a half-open scan and does not complete the full handshake.
* **UDP (`-sU`)** is slower and more difficult to identify because UDP is connectionless.
* A UDP port with no response is generally reported as `open|filtered`.
* Closed UDP ports commonly respond with an **ICMP port unreachable** message.
* NULL, FIN, and Xmas scans manipulate TCP flags and can sometimes help with firewall evasion.
* Xmas scans use the **FIN, PSH and URG** flags.
* `-sn` performs host discovery without a port scan.
* `-Pn` tells Nmap to skip host discovery and treat the target as alive.
* NSE scripts extend Nmap beyond basic port scanning.
* NSE scripts are written in **Lua**.
* NSE categories include `safe`, `intrusive`, `vuln`, `exploit`, `auth`, `brute`, and `discovery`.
* `-sV` identifies services and their versions.
* `-O` attempts operating-system detection.
* `-A` enables several advanced enumeration features together.
* `-oA` saves results in three major formats.
* Increasing verbosity with `-vv` provides more useful information during enumeration.

## 🧪 Practical Results

```text
ICMP Response:
N

Xmas Scan:
999 ports → open|filtered

Reason:
No response

TCP SYN Scan:
5 open ports

FTP Anonymous Login:
Y
```

## 🧠 What I Learned

I learned that Nmap is not simply a tool for finding open ports. It provides a complete framework for initial network enumeration, including host discovery, port scanning, service/version detection, OS detection, scripting, and output management.

The different scan types behave differently at the TCP/IP level. Understanding these differences helps explain why Nmap can classify ports differently depending on the scan being used.

I also learned that enumeration should come before exploitation because identifying available services gives a clearer understanding of the target's attack surface.

## ⚠️ Mistakes / Things I Didn't Understand

* Initially thought Nmap was mainly a port scanner, but learned that it can perform much broader enumeration.
* Needed to understand the difference between TCP Connect and SYN scans.
* Needed to understand why UDP scanning is slower than TCP scanning.
* Initially found `open|filtered` confusing and learned that it means Nmap cannot determine whether the port is open or filtered.
* Needed to understand the purpose of NULL, FIN, and Xmas scans.
* Learned that `-Pn` is useful when ICMP/host discovery is blocked.
* Needed to understand how NSE categories differ and why `intrusive` scripts should be treated carefully.
* Learned that scan results should be saved for later analysis and reporting.

## 🔗 Room

https://tryhackme.com/room/nmap
