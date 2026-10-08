# 18 - Key Exchange Mechanisms

## Purpose

Key exchange methods allow two parties to establish cryptographic material over an insecure communication channel.

## Diffie-Hellman

Diffie-Hellman allows two parties to establish a shared secret without directly sending that secret across the network.

### Security Concept

The protocol relies on mathematical properties that make the shared secret difficult for an observer to derive from the exchanged public values.

## RSA

RSA is an asymmetric cryptographic algorithm that can be used for encryption and digital signatures.

## ECDH

Elliptic Curve Diffie-Hellman applies the Diffie-Hellman idea using elliptic-curve cryptography.

The room associates it with establishing secure channels such as those used by TLS.

## ECDSA

ECDSA is an elliptic-curve digital-signature algorithm used to authenticate parties / messages through digital signatures.

## Algorithm Summary

| Algorithm | Main Idea |
|---|---|
| Diffie-Hellman | Shared-secret key agreement |
| RSA | Asymmetric encryption / signatures |
| ECDH | Elliptic-curve key agreement |
| ECDSA | Elliptic-curve digital signatures |

## Internet Key Exchange (IKE)

IKE is used with IPsec to negotiate security parameters and establish keys.

The room covers:

### Main Mode

The default IKE mode described by the room. It exchanges information in multiple phases and provides stronger protection of negotiation details than aggressive mode.

### Aggressive Mode

Uses fewer exchanges and exposes more negotiation information.

## Pre-Shared Keys (PSK)

A PSK allows the communicating parties to authenticate using a shared secret.

### Trade-Off

A PSK can strengthen authentication when managed securely, but the shared secret must itself be protected.

## Pentesting Relevance

When assessing VPN or encrypted services, identify:

- Key-exchange method
- Authentication mechanism
- Encryption configuration
- Legacy modes or protocols
- Weak/shared secrets where authorized testing permits validation
