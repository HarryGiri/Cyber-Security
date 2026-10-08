# 10 - Subnetting

## Definition

Subnetting divides an IPv4 range into smaller logical networks.

For a subnet, determine:

- Network address
- Broadcast address
- First host
- Last host
- Number of usable hosts

## Example: /26

Given:

```text
IP:          192.168.12.160
Mask:        255.255.255.192
CIDR:        /26
```

The subnet is:

```text
Network:     192.168.12.128/26
First host:  192.168.12.129
Last host:   192.168.12.190
Broadcast:   192.168.12.191
```

There are 64 addresses in the range and 62 usable host addresses after excluding the network and broadcast addresses.

## Network vs Host Part

The subnet mask acts as a template:

```text
1-bits → Network part
0-bits → Host part
```

Set host bits to `0` to calculate the network address.

Set host bits to `1` to calculate the broadcast address.

## Splitting a Subnet

To divide `192.168.12.128/26` into 4 subnets, extend the prefix by 2 bits:

```text
/26 → /28
```

The four resulting ranges are:

| Subnet | First Host | Last Host | Broadcast |
|---|---|---|---|
| 192.168.12.128/28 | .129 | .142 | .143 |
| 192.168.12.144/28 | .145 | .158 | .159 |
| 192.168.12.160/28 | .161 | .174 | .175 |
| 192.168.12.176/28 | .177 | .190 | .191 |

## Mental Subnetting

Remember the major CIDR boundaries:

```text
/8   /16   /24   /32
```

The room emphasizes identifying which octet changes and working in powers of two rather than trying to memorize every possible subnet.

## Pentesting Relevance

Subnetting affects:

- Which hosts are directly reachable
- Which networks require routing
- Scan ranges
- Attack paths
- Scope interpretation
