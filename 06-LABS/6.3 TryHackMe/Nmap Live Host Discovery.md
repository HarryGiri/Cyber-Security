# Nmap Live Host Discovery

**Platform:** TryHackMe
**Category:** Nmap / Reconnaissance / Host Discovery
**Difficulty:** Easy
**Status:** Completed

## 🎯 Objective

Learn how Nmap discovers **live hosts** before performing port scanning using:

* ARP
* ICMP
* TCP
* UDP
* Reverse DNS

---

## 🧠 Why Host Discovery?

Before scanning ports, identify which systems are online.

Scanning offline hosts:

* Wastes time
* Generates unnecessary traffic
* Creates additional noise

Nmap can perform host discovery with:

```bash
nmap -sn TARGET
```

`-sn` = **host discovery only**, without port scanning.

---

# 1. Subnets & ARP

A subnet is a logical network with its own IP range.

Common examples:

```text
/16 → 255.255.0.0
/24 → 255.255.255.0
```

### ARP

ARP operates at the **Link Layer** and maps an IP address to a MAC address.

ARP requests are broadcast within the local subnet and **cannot cross routers**.

Therefore:

```text
ARP → Same subnet only
```

### ARP Host Discovery

```bash
sudo nmap -PR -sn 10.200.6.0/24
```

* `-PR` → ARP ping
* `-sn` → host discovery only

Example result:

```text
Nmap done: 256 IP addresses (1 host up) scanned
```

### Key Point

ARP is particularly useful for discovering hosts on the same local network.

---

# 2. Host Discovery Methods

Nmap can use different protocols depending on the network and privileges.

| Layer     | Protocol | Purpose                            |
| --------- | -------- | ---------------------------------- |
| Link      | ARP      | Discover local hosts               |
| Network   | ICMP     | Discover hosts using ICMP          |
| Transport | TCP      | Discover hosts using TCP responses |
| Transport | UDP      | Discover hosts using ICMP errors   |

---

# 3. ICMP Host Discovery

## ICMP Echo

Uses ICMP:

```text
Type 8  → Echo Request
Type 0  → Echo Reply
```

Nmap option:

```bash
nmap -PE -sn TARGET
```

Example:

```bash
sudo nmap -PE -sn 10.200.6.0/24
```

Example result:

```text
10.200.6.1
10.200.6.50
10.200.6.250
```

**3 hosts were discovered.**

### Limitation

Firewalls can block ICMP Echo requests.

---

## ICMP Timestamp

Uses:

```text
Type 13 → Timestamp Request
Type 14 → Timestamp Reply
```

Nmap option:

```bash
nmap -PP -sn TARGET
```

Example:

```bash
nmap -PP -sn 10.200.6.0/24
```

---

## ICMP Address Mask

Uses:

```text
Type 17 → Address Mask Request
Type 18 → Address Mask Reply
```

Nmap option:

```bash
nmap -PM -sn TARGET
```

Example:

```bash
nmap -PM -sn 10.200.6.0/24
```

This may fail if the target or firewall blocks this ICMP type.

---

# 4. TCP Host Discovery

TCP packets can be used when ICMP is blocked.

## TCP SYN Ping

Nmap option:

```bash
-PS
```

Example:

```bash
sudo nmap -PS -sn 10.200.6.0/24
```

Specific ports:

```bash
-PS21
-PS21-25
-PS80,443,8080
```

A response can indicate that the host is online.

### TCP SYN Ping

```text
SYN → Target

Open port   → SYN/ACK
Closed port → RST
```

---

## TCP ACK Ping

Nmap option:

```bash
-PA
```

Example:

```bash
sudo nmap -PA -sn 10.200.6.0/24
```

Specific ports:

```bash
-PA21
-PA21-25
-PA80,443,8080
```

An ACK packet sent to a target can result in:

```text
RST
```

A response indicates that the host is reachable.

### Privileges

| Scan                 | Privileged account required? |
| -------------------- | ---------------------------- |
| TCP SYN Ping (`-PS`) | No                           |
| TCP ACK Ping (`-PA`) | Yes                          |

---

# 5. UDP Host Discovery

UDP can also be used to identify live hosts.

Nmap option:

```bash
-PU
```

Example:

```bash
sudo nmap -PU -sn 10.200.6.0/24
```

A UDP packet sent to a **closed UDP port** can trigger:

```text
ICMP Destination Unreachable
Port Unreachable
```

This response indicates that the host is online.

---

# 6. Target Specification

Nmap supports several target formats.

### Individual targets

```bash
nmap 10.10.10.1
```

### Multiple targets

```bash
nmap 10.10.10.1 10.10.10.2 example.com
```

### IP range

```bash
nmap 10.10.10.15-20
```

### Subnet

```bash
nmap 10.10.10.0/24
```

### Targets from a file

```bash
nmap -iL list_of_hosts.txt
```

### List targets without scanning

```bash
nmap -sL TARGETS
```

Disable DNS resolution:

```bash
nmap -sL -n TARGETS
```

---

# 7. Reverse DNS

Reverse DNS resolves:

```text
IP → Hostname
```

Example:

```text
10.200.6.15 → hostname
```

### Force reverse DNS for all hosts

```bash
nmap -R TARGET
```

### Disable DNS lookups

```bash
nmap -n TARGET
```

### Use a specific DNS server

```bash
nmap --dns-servers DNS_SERVER TARGET
```

Reverse DNS can provide useful information about host roles and network structure, but records may be missing or inaccurate.

---

# 8. Important Nmap Options

| Option          | Purpose                       |
| --------------- | ----------------------------- |
| `-sn`           | Host discovery only           |
| `-PR`           | ARP discovery                 |
| `-PE`           | ICMP Echo                     |
| `-PP`           | ICMP Timestamp                |
| `-PM`           | ICMP Address Mask             |
| `-PS`           | TCP SYN Ping                  |
| `-PA`           | TCP ACK Ping                  |
| `-PU`           | UDP Ping                      |
| `-R`            | Reverse DNS for all hosts     |
| `-n`            | Disable DNS lookup            |
| `--dns-servers` | Specify DNS server            |
| `-sL`           | List targets without scanning |
| `-iL`           | Read targets from a file      |

---

# 9. Host Discovery Summary

```text
                 Nmap Host Discovery
                         │
       ┌─────────────────┼─────────────────┐
       │                 │                 │
      ARP              ICMP              TCP/UDP
       │                 │                 │
      -PR          -PE / -PP / -PM     -PS / -PA / -PU
       │
 Same subnet
```

### Practical commands

```bash
# ARP
sudo nmap -PR -sn TARGET

# ICMP Echo
sudo nmap -PE -sn TARGET

# ICMP Timestamp
sudo nmap -PP -sn TARGET

# ICMP Address Mask
sudo nmap -PM -sn TARGET

# TCP SYN
sudo nmap -PS80,443 -sn TARGET

# TCP ACK
sudo nmap -PA80,443 -sn TARGET

# UDP
sudo nmap -PU53,161 -sn TARGET
```

---

# 🧠 What I Learned

* Host discovery should generally come before detailed port scanning.
* ARP discovery works within the local subnet because ARP operates at Layer 2.
* ICMP Echo is simple but can be blocked by firewalls.
* ICMP Timestamp and Address Mask provide alternative discovery methods.
* TCP SYN and ACK packets can identify reachable hosts when ICMP is unavailable.
* UDP discovery can use ICMP Port Unreachable responses to identify live systems.
* `-sn` prevents Nmap from continuing into port scanning.
* Reverse DNS can reveal useful hostnames and possible system roles.
* Different discovery techniques should be combined when one method is blocked.

---

## 🔗 Related Nmap Topics

Next: **Nmap Basic Port Scans**

This room is part of the Nmap learning series and focuses specifically on **discovering live hosts before port scanning**.
