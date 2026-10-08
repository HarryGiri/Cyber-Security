# 09 - IP Addresses

## MAC vs IP

- **MAC** identifies a network interface on the local network.
- **IP** provides logical addressing used to reach hosts across networks.

## IPv4

IPv4 is 32 bits and is written as four octets:

```text
192.168.10.39
```

Each octet ranges from `0-255`.

### Binary Values

```text
128 64 32 16 8 4 2 1
```

Example:

```text
192 = 11000000
```

## Network and Host Parts

An IPv4 address is divided into a network part and a host part. The subnet mask determines the split.

## Subnet Mask

```text
255.255.255.0
```

Binary:

```text
11111111.11111111.11111111.00000000
```

## CIDR

CIDR expresses the number of network bits.

```text
192.168.10.39/24
```

`/24` means 24 bits represent the network portion.

## Network and Broadcast Addresses

- Network address: host bits are all `0`.
- Broadcast address: host bits are all `1`.

## Default Gateway

The default gateway is the router used to reach other networks.

## Pentesting Relevance

IP knowledge is fundamental to:

- Scope validation
- Host discovery
- Port scanning
- Subnet analysis
- Route analysis
- Network segmentation

> Verify the actual subnet instead of assuming `/24`.
