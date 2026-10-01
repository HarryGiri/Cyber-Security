# Nmap Basic Port Scans

**Platform:** TryHackMe
**Category:** Nmap / Network Reconnaissance / Port Scanning
**Difficulty:** Easy
**Status:** Completed

## 🎯 Objective

Learn the basic Nmap port-scanning techniques used to identify open TCP and UDP services:

* TCP Connect Scan
* TCP SYN Scan
* UDP Scan
* Port selection
* Scan timing
* Packet rate
* Probe parallelisation

---

# 1. TCP and UDP Ports

A **port** identifies a network service running on a host.

Examples:

| Port | Protocol | Common Service |
| ---: | -------- | -------------- |
|   22 | TCP      | SSH            |
|   53 | UDP      | DNS            |
|   53 | TCP      | DNS            |
|   80 | TCP      | HTTP           |
|  443 | TCP      | HTTPS          |

### Nmap Port States

Nmap considers **6 port states**:

| State              | Meaning                                                   |
| ------------------ | --------------------------------------------------------- |
| `open`             | A service is listening                                    |
| `closed`           | No service is listening, but the port is reachable        |
| `filtered`         | Nmap cannot determine whether it is open or closed        |
| `unfiltered`       | Port is accessible, but Nmap cannot determine open/closed |
| `open\|filtered`   | Cannot determine whether open or filtered                 |
| `closed\|filtered` | Cannot determine whether closed or filtered               |

For a pentester, an **open** port is particularly useful because it indicates an accessible service.

---

# 2. TCP Flags

Important TCP flags:

| Flag  | Purpose                        |
| ----- | ------------------------------ |
| `SYN` | Initiates a TCP connection     |
| `ACK` | Acknowledges received data     |
| `RST` | Resets/terminates a connection |
| `FIN` | Indicates no more data         |
| `PSH` | Pushes data to the application |
| `URG` | Indicates urgent data          |

### TCP 3-Way Handshake

```text
Client                  Server

  SYN  ────────────────>
       <──────── SYN/ACK
  ACK  ────────────────>
```

The first packet uses the **SYN** flag.

---

# 3. TCP Connect Scan

TCP Connect Scan uses the complete TCP 3-way handshake.

Nmap option:

```bash
nmap -sT MACHINE_IP
```

### Process

```text
SYN
 ↓
SYN/ACK
 ↓
ACK
 ↓
Connection established
 ↓
RST/ACK
```

Nmap tears down the connection after confirming the port state.

### Important Point

If the user is **unprivileged**, TCP Connect Scan is the available TCP scanning method.

Example:

```bash
nmap -sT MACHINE_IP
```

Typical output:

```text
PORT   STATE  SERVICE
21/tcp open   ftp
22/tcp open   ssh
53/tcp open   domain
80/tcp open   http
```

---

## Fast Scan

```bash
nmap -F MACHINE_IP
```

`-F` reduces the scan from the default **1000 most common ports** to the **100 most common ports**.

---

## Sequential Port Scanning

By default, Nmap may scan ports in a non-consecutive order.

Use:

```bash
nmap -r MACHINE_IP
```

`-r` → scan ports in consecutive order.

---

# 4. TCP SYN Scan

TCP SYN Scan is Nmap's default TCP scan when running with sufficient privileges.

Option:

```bash
sudo nmap -sS MACHINE_IP
```

### Process

```text
SYN  ────────────────>
     <──────── SYN/ACK
RST  ────────────────>
```

Unlike a TCP Connect Scan, the complete TCP handshake is **not established**.

### Advantages

* Does not complete the TCP connection.
* Generally faster than a full connect scan.
* Produces less connection-level logging than a Connect Scan.

### Example

```bash
nmap -sS 10.10.105.229
```

Example result:

```text
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
53/tcp open  domain
80/tcp open  http
```

---

# 5. UDP Scan

UDP is connectionless and does not use a TCP-style handshake.

Nmap option:

```bash
sudo nmap -sU MACHINE_IP
```

### UDP behaviour

If a UDP port is closed, the target may respond with:

```text
ICMP Type 3
Code 3
Port Unreachable
```

If a UDP port does not respond, Nmap may classify it as:

```text
open|filtered
```

Example:

```bash
sudo nmap -sU --top-ports 10 MACHINE_IP
```

Example result:

```text
PORT     STATE  SERVICE
53/udp   open   domain
67/udp   closed dhcps
123/udp  closed ntp
135/udp  closed msrpc
137/udp  closed netbios-ns
138/udp  closed netbios-dgm
161/udp  closed snmp
445/udp  closed microsoft-ds
631/udp  closed ipp
1434/udp closed ms-sql-m
```

### Important Finding

```text
161/udp → closed
Service → SNMP
```

---

# 6. Selecting Ports

### Specific ports

```bash
nmap -p22,80,443 MACHINE_IP
```

### Port range

```bash
nmap -p1-1023 MACHINE_IP
```

### Custom range

```bash
nmap -p5000-5500 MACHINE_IP
```

### All 65535 ports

```bash
nmap -p- MACHINE_IP
```

### Top 100 ports

```bash
nmap -F MACHINE_IP
```

### Top N ports

```bash
nmap --top-ports 10 MACHINE_IP
```

---

# 7. Scan Timing

Nmap provides six timing templates:

| Option | Name       | Speed     |
| ------ | ---------- | --------- |
| `-T0`  | Paranoid   | Slowest   |
| `-T1`  | Sneaky     | Very slow |
| `-T2`  | Polite     | Slow      |
| `-T3`  | Normal     | Default   |
| `-T4`  | Aggressive | Fast      |
| `-T5`  | Insane     | Fastest   |

Example:

```bash
nmap -T4 MACHINE_IP
```

Very slow/paranoid scan:

```bash
nmap -T0 MACHINE_IP
```

`-T5` is faster but can increase packet loss and potentially affect accuracy.

---

# 8. Packet Rate

Nmap can control the number of packets sent per second.

### Minimum rate

```bash
nmap --min-rate 15 MACHINE_IP
```

Ensures Nmap sends at least approximately 15 packets/sec when possible.

### Maximum rate

```bash
nmap --max-rate 50 MACHINE_IP
```

Limits the packet rate to approximately 50 packets/sec.

---

# 9. Probe Parallelisation

Nmap can control how many probes run simultaneously.

### Minimum parallel probes

```bash
nmap --min-parallelism=64 MACHINE_IP
```

Example:

```bash
nmap --min-parallelism=100 MACHINE_IP
```

This controls the minimum number of probes Nmap attempts to maintain in parallel.

---

# 10. Important Commands

```bash
# TCP Connect Scan
nmap -sT MACHINE_IP

# TCP SYN Scan
sudo nmap -sS MACHINE_IP

# UDP Scan
sudo nmap -sU MACHINE_IP

# Fast scan
nmap -F MACHINE_IP

# All ports
nmap -p- MACHINE_IP

# Specific ports
nmap -p22,80,443 MACHINE_IP

# Port range
nmap -p1-1023 MACHINE_IP

# Scan sequentially
nmap -r MACHINE_IP

# Top 10 ports
nmap --top-ports 10 MACHINE_IP

# Slow/paranoid
nmap -T0 MACHINE_IP

# Fast/aggressive
nmap -T4 MACHINE_IP

# Minimum packet rate
nmap --min-rate 15 MACHINE_IP

# Maximum packet rate
nmap --max-rate 50 MACHINE_IP

# Minimum parallel probes
nmap --min-parallelism=100 MACHINE_IP
```

---

# 🧠 TCP Connect vs SYN Scan

| Feature                    | TCP Connect           | TCP SYN             |
| -------------------------- | --------------------- | ------------------- |
| Option                     | `-sT`                 | `-sS`               |
| Full handshake             | Yes                   | No                  |
| Privileged user            | Not required          | Required            |
| Final action after SYN/ACK | `ACK` then teardown   | `RST`               |
| Common use                 | Unprivileged scanning | Privileged scanning |

---

# 🧠 What I Learned

* A port identifies a network service on a host.
* Nmap has six possible port states.
* TCP Connect Scan completes the TCP 3-way handshake.
* TCP SYN Scan detects open ports without completing the handshake.
* SYN scanning requires a privileged account.
* UDP does not use a connection-oriented handshake.
* Closed UDP ports can respond with ICMP Port Unreachable.
* `-p-` scans all 65,535 TCP ports.
* `-F` scans the 100 most common ports.
* `--top-ports` allows scanning a chosen number of common ports.
* `-T0` is the slowest/paranoid timing template.
* `--min-rate` and `--max-rate` control packet transmission rate.
* `--min-parallelism` controls the minimum number of parallel probes.

---

## 📌 Key Takeaway

The basic Nmap port-scanning workflow is:

```text
Target
  ↓
Host Discovery
  ↓
Port Scanning
  ↓
Identify Open Ports
  ↓
Identify Services
  ↓
Further Enumeration
```

This room builds directly on **Nmap Live Host Discovery** and prepares for **Nmap Advanced Port Scans**.
