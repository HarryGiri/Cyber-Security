# 14 - Common Protocols

## Protocol Quick Reference

| Protocol | Port | Transport | Main Purpose |
|---|---:|---|---|
| SSH | 22 | TCP | Secure remote login |
| Telnet | 23 | TCP | Remote login |
| DNS | 53 | TCP/UDP | Name resolution |
| FTP | 20-21 | TCP | File transfer |
| TFTP | 69 | UDP | Simple file transfer |
| DHCP | 67-68 | UDP | IP configuration |
| HTTP | 80 | TCP | Web communication |
| HTTPS | 443 | TCP | Secure web communication |
| SMTP | 25 | TCP | Email transfer |
| POP3 | 110 | TCP | Email retrieval |
| IMAP | 143 | TCP | Email access |
| SMB | 445 | TCP | File/resource sharing |
| NFS | 111, 2049 | TCP/UDP | Remote filesystem access |
| Kerberos | 88 | TCP/UDP | Authentication / authorization |
| LDAP | 389 | TCP/UDP | Directory services |
| RDP | 3389 | TCP | Remote desktop |
| RPC | 135, 137-139 | TCP/UDP | Remote procedure calls |
| SNMP | 161-162 | UDP | Network management |
| NTP | 123 | UDP | Time synchronization |
| SIP | 5060 | UDP/TCP | VoIP sessions |
| OSPF | 89 | IP protocol | Routing |
| PPTP | 1723 | TCP | VPN tunneling |

## TCP

TCP is connection-oriented and designed to provide reliable delivery.

Common examples from the room include web pages and email.

## UDP

UDP is connectionless and emphasizes lower overhead / speed over delivery guarantees.

Common examples include streaming, gaming, DNS, and other services where latency matters.

## ICMP

ICMP is used for control and troubleshooting messages.

The room also discusses different ICMP request/message types and how network tools use ICMP behavior.

## Pentesting Relevance

Port and service enumeration becomes more useful when the tester knows what a protocol is normally used for and whether it runs over TCP or UDP.
