# 19 - Authentication Protocols

## Purpose

Authentication protocols verify the identity of users and devices and can support secure communication between entities.

## Protocol Reference

| Protocol / Technology | Main Use |
|---|---|
| Kerberos | Ticket-based authentication using a KDC |
| SRP | Password-based cryptographic authentication |
| SSL | Older secure-communication protocol terminology |
| TLS | Modern successor to SSL for secure communication |
| OAuth | Delegated authorization |
| OpenID | Federated / decentralized identity |
| SAML | Authentication and authorization data exchange |
| 2FA | Authentication using two factors |
| FIDO | Standards for strong authentication |
| PKI | Public/private-key infrastructure |
| SSO | One login used across multiple applications |
| MFA | Multiple authentication factors |
| PAP | Password transmitted in clear text |
| CHAP | Challenge-based authentication |
| EAP | Framework supporting multiple authentication methods |
| SSH | Secure remote access |
| HTTPS | HTTP protected by TLS |
| LEAP | Cisco wireless authentication protocol with known weaknesses |
| PEAP | EAP-based protected authentication tunnel |

## Stronger Authentication Concepts

### MFA

Uses multiple categories such as:

- Something you know
- Something you have
- Something you are

### SSO

Allows a user to access multiple applications using a single set of credentials.

### PKI

Uses public/private keys for authentication, encryption, and digital signatures.

## Wireless Authentication

The room contrasts older wireless mechanisms such as LEAP with stronger approaches such as EAP-TLS.

## TCP vs UDP

### TCP

- Connection-oriented
- Reliable delivery
- Common for important application data

### UDP

- Connectionless
- Lower overhead
- No built-in guarantee that all data arrives intact

## Pentesting Relevance

When enumerating a service, determine:

```text
What authenticates the user?
What factors are required?
Is the protocol encrypted?
Is a legacy authentication method still enabled?
What trust infrastructure does the service use?
```
