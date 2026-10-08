# 12 - IPv6 Addresses

## IPv6 Basics

IPv6 is the successor to IPv4 and uses **128-bit** addresses.

Example:

```text
fe80:0000:0000:0000:dd80:b1a9:6687:2d3b/64
```

Shortened form:

```text
fe80::dd80:b1a9:6687:2d3b/64
```

## IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address length | 32-bit | 128-bit |
| Representation | Decimal | Hexadecimal |
| Dynamic addressing | DHCP | SLAAC / DHCPv6 |
| IPsec | Optional | Supported as part of IPv6 design |
| Example prefix | `10.10.10.0/24` | `fe80::/64` |

## IPv6 Address Types

| Type | Meaning |
|---|---|
| Unicast | One interface |
| Anycast | Multiple interfaces; one receives the packet |
| Multicast | Multiple interfaces; all receive the packet |

## IPv6 Structure

An IPv6 address consists of:

```text
Network Prefix | Interface Identifier
```

## Hexadecimal

IPv6 uses hexadecimal because it represents binary more compactly.

```text
Decimal → Hex
10 → A
11 → B
12 → C
13 → D
14 → E
15 → F
```

## IPv6 Compression Rules

The room references RFC 5952 notation rules:

- Use lowercase hexadecimal letters.
- Remove leading zeros in each block.
- Replace one or more consecutive zero blocks with `::`.
- Use `::` only once in an address.

## Pentesting Relevance

IPv6 should not be ignored during enumeration. A network can expose hosts and services through IPv6 even when the tester is primarily looking at IPv4.
