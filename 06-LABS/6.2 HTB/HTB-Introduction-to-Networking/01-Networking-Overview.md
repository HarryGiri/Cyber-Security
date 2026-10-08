# 01 - Networking Overview

## Core Idea

A network allows computers and other devices to communicate using different protocols, media, and topologies.

For security work, networking knowledge matters because an incorrect understanding of the network can lead to missed hosts, incorrect scope assumptions, and wrong conclusions during a penetration test.

## Segmentation

A large flat network is easier to build but provides fewer security boundaries. Dividing the environment into smaller networks adds defensive layers.

Common controls include:

- Access Control Lists (ACLs)
- Firewalls
- Host-based firewall rules
- Intrusion Detection Systems (IDS)
- Network monitoring

## Pentesting Lesson: Never Assume /24

The room gives an example where a `/25` network was split into two separate ranges:

```text
Server Gateway:      10.20.0.1/25
Domain Controller:   10.20.0.10/25
Client Gateway:      10.20.0.129/25
Client Workstation:  10.20.0.200/25
Pentester IP:        10.20.0.252/24
```

The tester could communicate with the client network but failed to understand that other valuable systems were on a different subnet.

## Secure Network Placement

The room recommends considering separate networks for:

| Asset | Suggested Placement |
|---|---|
| Public web server | DMZ |
| Workstations | Separate network |
| Switches / routers | Administration network |
| IP phones | Separate network |
| Printers | Separate network |

## Why Segmentation Matters

Segmentation can reduce unnecessary communication and make lateral movement harder.

Useful questions during assessment:

```text
Why can this host communicate with that host?
Should this system reach the Internet?
Should workstations communicate with each other?
Which subnet contains the high-value systems?
```

## FQDN vs URL

An FQDN identifies a host, while a URL can identify a more specific resource.

```text
FQDN:
www.hackthebox.eu

URL:
https://www.hackthebox.eu/example?floor=2&office=dev&employee=17
```

## Basic Traffic Flow

```text
Client
  ↓
Router
  ↓
ISP
  ↓
DNS resolution
  ↓
Destination network
  ↓
Server
  ↓
Response
```

## Pentesting Takeaways

- Identify the real subnet and gateway before scanning.
- Do not blindly configure a `/24` mask.
- Understand network segmentation and routing boundaries.
- Treat unexpected inter-network communication as a finding worth investigating.
