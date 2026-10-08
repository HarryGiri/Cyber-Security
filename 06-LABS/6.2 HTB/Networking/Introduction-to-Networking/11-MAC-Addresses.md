# 11 - MAC Addresses

## MAC Address

A MAC address is a 48-bit (6-octet) address used for Layer-2 network interfaces.

Example formats:

```text
DE:AD:BE:EF:13:37
DE-AD-BE-EF-13-37
DEAD.BEEF.1337
```

## Structure

The first 24 bits are the **Organization Unique Identifier (OUI)**. The remaining portion identifies the individual interface.

## Address Types

### Unicast

Identifies a single destination interface.

### Multicast

Identifies a group of interfaces.

### Broadcast

Uses:

```text
FF:FF:FF:FF:FF:FF
```

and reaches all devices in the local broadcast domain.

## Locally Administered Addresses

The room distinguishes globally assigned OUIs from locally administered MAC addresses.

## ARP

Address Resolution Protocol maps an IPv4 address to a MAC address on a local network.

### ARP Request

A device broadcasts a request asking which MAC address owns a particular IP.

### ARP Reply

The device owning the IP replies with its MAC address.

Example traffic pattern:

```text
Who has 10.129.12.100?
        ↓
10.129.12.100 is at CC:CC:CC:CC:CC:CC
```

## Security Relevance

The room demonstrates that falsified ARP information can associate an attacker's MAC address with another IP, which is the basis of ARP spoofing / poisoning.

## Pentesting Takeaways

- MAC operates at Layer 2.
- ARP is used for local IPv4 address-to-MAC resolution.
- ARP traffic can be inspected with packet-analysis tools.
- Unexpected ARP changes deserve investigation.
