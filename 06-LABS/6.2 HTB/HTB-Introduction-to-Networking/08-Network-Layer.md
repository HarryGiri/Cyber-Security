# 08 - Network Layer

## Layer 3

The Network Layer is responsible for moving packets between networks.

### Core Functions

- Logical addressing
- Routing

## Protocols Mentioned

- IPv4
- IPv6
- IPsec
- ICMP
- IGMP
- RIP
- OSPF

## Routing Between Subnets

Same subnet:

```text
Host A → Host B
```

Different subnets:

```text
Host A → Default Gateway → Router(s) → Host B
```

Routers use addressing and routing information to forward packets.

## Pentesting Relevance

Layer-3 understanding helps with:

- Subnet discovery
- Gateway identification
- Route analysis
- Reachability testing
- Segmentation analysis

## Questions to Ask

```text
What subnet am I on?
What is my gateway?
Is the destination local or remote?
What route does traffic take?
```
