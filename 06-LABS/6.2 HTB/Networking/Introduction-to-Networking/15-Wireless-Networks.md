# 15 - Wireless Networks

## Wireless Basics

Wireless networks use radio-frequency (RF) communication between wireless interfaces and access points / WAPs.

A client generally needs to be within range and have appropriate network configuration such as the network name and credentials.

## Wireless Security Features

The room groups wireless security around:

- Encryption
- Access control
- Firewalls
- Authentication

## WEP

WEP is an older wireless security mechanism with known weaknesses.

The room covers its challenge-response process and explains that flaws in the design of the integrity/encryption mechanism can allow attacks against WEP.

WEP variants discussed include:

```text
WEP-40 / WEP-64
WEP-104
```

Both use a 24-bit IV; the room describes differences in the associated secret-key sizes.

## WPA

WPA was introduced as an improvement over WEP.

The room distinguishes:

- WPA-Personal
- WPA-Enterprise

## Authentication

The section discusses EAP-based authentication and TACACS+ in the context of wireless/network access.

## Disassociation Attack

A disassociation attack attempts to disrupt communication by causing clients to disconnect from the wireless network.

## Wireless Hardening

The room recommends considering:

- Stronger Wi-Fi security such as WPA.
- WPA-Enterprise where appropriate.
- MAC filtering as an additional control.
- EAP-TLS for certificate-based authentication.
- Carefully configured access controls.
- Appropriate network segmentation.

## Pentesting Relevance

Wireless assessments should examine:

- Authentication method
- Encryption/security protocol
- Access controls
- Network segmentation
- Client/AP behavior
- Wireless attack exposure
