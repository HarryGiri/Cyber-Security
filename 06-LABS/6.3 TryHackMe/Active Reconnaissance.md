# Active Reconnaissance

**Platform:** TryHackMe
**Category:** Recon / Networking
**Difficulty:** Easy
**Status:** ✅ Completed

## 🎯 Objective

Learn the fundamentals of active reconnaissance by directly interacting with target systems to identify reachable hosts, network paths, open services, and service information. The room focused on browser-based reconnaissance, `ping`, `traceroute`, `telnet`, and `netcat`.

## 🔍 What I Did

* Learned the difference between passive and active reconnaissance.
* Used browser Developer Tools to inspect HTTP headers, JavaScript source files, cookies/storage, and TLS certificates.
* Used `ping` to test host reachability and examine TTL values.
* Used `traceroute` to identify intermediate network hops and understand network paths.
* Compared traceroute results to understand dynamic routing and load balancing.
* Used `telnet` to connect to TCP ports and perform basic banner grabbing.
* Used `netcat (nc)` for TCP connections, banner grabbing, and basic client-server communication.
* Learned why modern tools such as `nc`, `curl`, and SSH are generally preferred over legacy plaintext protocols such as Telnet.

## 🛠️ Tools / Commands

```bash
# Test host reachability
ping -c 5 MACHINE_IP

# IPv4 / IPv6 ping
ping -4 -c 5 MACHINE_IP
ping -6 -c 5 MACHINE_IPV6

# Trace network path
traceroute MACHINE_IP

# Alternative path monitoring
mtr MACHINE_IP

# TCP traceroute
traceroute -T MACHINE_IP

# ICMP traceroute
traceroute -I MACHINE_IP

# Legacy TCP connection / banner grabbing
telnet MACHINE_IP PORT_NUMBER

# Netcat TCP connection
nc MACHINE_IP PORT_NUMBER

# Netcat listener
nc -lvnp PORT_NUMBER

# HTTP headers
curl -I http://MACHINE_IP
curl -I https://MACHINE_IP
```

**Browser Developer Tools:**

* **Network** — inspect requests, responses, headers, cookies, status codes, and timing.
* **Sources** — inspect HTML, JavaScript, and CSS files for exposed endpoints or information.
* **Application** — inspect cookies, Local Storage, and Session Storage.
* **Security** — inspect TLS certificate information and Subject Alternative Names (SANs).

## 💡 Key Findings / Concepts

* **Active reconnaissance** directly interacts with the target and therefore leaves detectable traces such as logs, firewall events, WAF alerts, and IDS alerts.
* Browser Developer Tools can reveal useful information through HTTP headers, JavaScript files, storage, and certificates.
* `ping` uses **ICMP Echo Request/Reply** to determine whether a host is reachable.
* TTL values can provide clues about the target's operating system, although intermediate routers modify the TTL.
* A failed ping does **not necessarily mean a host is offline** because ICMP may be blocked or filtered.
* `traceroute` uses progressively increasing TTL values to identify intermediate network hops.
* Network paths can change because of dynamic routing, load balancing, failover, and anycast infrastructure.
* `*` in traceroute output can indicate that a router did not respond to the probe or suppressed its response.
* **Banner grabbing** can reveal the software and version running on a service.
* Telnet can be used for basic TCP banner grabbing, but it transmits data in plaintext and is unsuitable for secure remote administration.
* `netcat` can operate as both a TCP client and server, making it useful for banner grabbing, connectivity testing, and simple communication.
* Modern HTTPS services require tools capable of handling TLS, such as `curl`, `openssl`, or `ncat --ssl`.
* Active reconnaissance should only be performed against systems where explicit authorization has been provided.

## 🧠 What I Learned

I learned that active reconnaissance provides information that passive sources cannot, but the trade-off is that direct interaction leaves observable traces. `ping` can help determine reachability, while `traceroute` provides information about the network path and intermediate hops. I also learned how browser Developer Tools, Telnet, and Netcat can expose service and application information through direct interaction. These techniques form the foundation for more advanced enumeration and scanning with tools such as Nmap.

## ⚠️ Mistakes / Things I Didn't Understand

* Initially needed to understand why active reconnaissance is more detectable than passive reconnaissance.
* Learned that a failed `ping` does not necessarily indicate that a host is offline.
* Needed to understand how TTL values are affected by intermediate routers before using them for OS fingerprinting.
* Learned that traceroute results can differ between runs because of dynamic routing and load balancing.
* Learned that Telnet is useful for understanding TCP connections and banner grabbing, but should not be used for secure remote administration.

## 🔗 Room

https://tryhackme.com/room/activerecon
