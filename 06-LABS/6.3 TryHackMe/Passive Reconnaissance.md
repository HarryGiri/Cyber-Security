# Passive Reconnaissance

**Platform:** TryHackMe
**Category:** Recon / OSINT / Networking
**Difficulty:** Easy
**Status:** ✅ Completed

## 🎯 Objective

Learn how to perform passive reconnaissance using publicly available information without directly interacting with the target. The room focused on WHOIS/RDAP, DNS enumeration, passive subdomain discovery, Certificate Transparency logs, DNSDumpster, and Shodan.

## 🔍 What I Did

* Learned the difference between passive and active reconnaissance.
* Used `whois` to gather domain registration information.
* Learned about RDAP as the modern replacement for traditional WHOIS.
* Used `dig` and `nslookup` to query DNS records.
* Identified common DNS records including A, AAAA, CNAME, MX, SOA, and TXT.
* Used DNSDumpster to discover subdomains and related DNS infrastructure.
* Used Certificate Transparency logs through `crt.sh` for passive subdomain discovery.
* Used Shodan to gather information about internet-facing hosts, ports, services, and infrastructure.
* Learned how publicly exposed information can be useful for both attackers and defenders.

## 🛠️ Tools / Commands

```bash
# WHOIS
whois tryhackme.com

# DNS A record
nslookup -type=A tryhackme.com

# DNS MX record
nslookup -type=MX tryhackme.com 1.1.1.1

# DNS TXT record
nslookup -type=TXT tryhackme.com

# DNS A record with dig
dig tryhackme.com A

# DNS MX record using a specific resolver
dig @1.1.1.1 tryhackme.com MX

# DNS TXT record
dig tryhackme.com TXT

# RDAP lookup
curl -s https://rdap.verisign.com/com/v1/domain/tryhackme.com | jq .
```

**Browser-based tools:**

* DNSDumpster — passive DNS and subdomain discovery.
* crt.sh — Certificate Transparency log searches.
* Shodan — search engine for internet-connected devices and exposed services.

## 💡 Key Findings / Concepts

* Standard DNS lookups only resolve domain names or records that are already known; they do not automatically discover hidden or unadvertised subdomains.
* Subdomains can reveal additional attack surface such as development environments, APIs, administration panels, and forgotten applications.
* **DNSDumpster** aggregates publicly available DNS information and can reveal subdomains, hosts, IP addresses, MX/TXT/CNAME records, and relationships between infrastructure.
* **Certificate Transparency (CT) logs** publicly record issued SSL/TLS certificates and can reveal subdomains through certificate SAN entries.
* `crt.sh` can be searched with `%.tryhackme.com` to find certificates associated with subdomains of a domain.
* **Shodan** indexes internet-facing devices and services rather than normal web pages.
* Shodan results can provide information such as IP addresses, ASNs, hosting providers, approximate locations, open ports, service banners, and detected technologies.
* Passive reconnaissance relies on information already available through public sources rather than directly probing the target.
* Passive reconnaissance can help identify forgotten infrastructure and misconfigurations while generating less direct exposure than active reconnaissance.
* Public IP addresses and infrastructure can change over time, so reconnaissance results are not permanent.

## 🧠 What I Learned

I learned that passive reconnaissance goes beyond simply resolving a domain to an IP address. Public sources such as DNS records, Certificate Transparency logs, DNSDumpster, and Shodan can reveal additional infrastructure and subdomains without directly probing the target. I also learned that different sources provide different pieces of information, so cross-referencing them can build a more complete picture of an organisation's public footprint. From a defensive perspective, the same techniques can be used to identify and reduce unintended exposure.

## ⚠️ Mistakes / Things I Didn't Understand

* Initially, I understood DNS lookups mainly as a way to find IP addresses, but learned that different record types reveal different types of infrastructure information.
* Learned that passive subdomain discovery can find domains that are not obvious from standard DNS lookups.
* Needed to understand the difference between traditional WHOIS and modern RDAP.
* Learned that Shodan's data comes from its own internet-wide scanning and indexing, allowing users to search the collected information without directly scanning the target themselves.

## 🔗 Room

https://tryhackme.com/room/passiverecon
