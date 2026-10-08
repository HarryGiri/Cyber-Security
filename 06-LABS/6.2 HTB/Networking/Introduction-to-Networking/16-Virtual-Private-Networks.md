# 16 - Virtual Private Networks

## Definition

A VPN creates a secure, encrypted connection between a remote device and a private network.

Typical use cases include:

- Remote employees
- Remote administration
- Access to internal resources
- Connecting separate networks

## Why Organizations Use VPNs

VPNs can provide secure remote connectivity and help protect traffic crossing untrusted networks.

## IPsec

The room introduces IPsec as a common VPN security technology.

It provides mechanisms for confidentiality and authentication of IP traffic.

### IPsec Modes

| Mode | General Idea |
|---|---|
| Transport | Protects the payload of IP packets |
| Tunnel | Protects the original packet and carries it inside a new IP packet |

## Protocols / Components

The room discusses:

- ESP (Encapsulating Security Payload)
- IKE (Internet Key Exchange)
- PPTP

## PPTP

The room notes that PPTP has known security weaknesses and is no longer considered secure.

## Pentesting Relevance

When assessing VPNs, identify:

- VPN technology
- Authentication method
- Encryption configuration
- Reachable internal networks
- Split/full tunneling behavior
- Legacy or insecure protocols
