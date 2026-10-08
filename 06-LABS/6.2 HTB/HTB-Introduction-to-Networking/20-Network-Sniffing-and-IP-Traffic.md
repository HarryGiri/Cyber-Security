# 20 - Network Sniffing and IP Traffic

## IP Packet

An IP packet contains a header and payload.

The header provides information needed for routing and packet processing.

## Important IP Header Fields

| Field | Purpose |
|---|---|
| Version | IPv4 / IPv6 version |
| Internet Header Length | Header size |
| Class of Service | Traffic priority / service information |
| Total Length | Packet size |
| Identification | Identifies fragmented packets |
| Flags | Fragmentation controls |
| Fragment Offset | Position of a fragment |
| TTL | Limits packet lifetime |
| Protocol | Identifies the upper-layer protocol, such as TCP/UDP |
| Checksum | Detects header errors |
| Source / Destination | Sender and receiver addresses |
| Options | Optional information |

## IP Identification Field

The room shows that packet IDs can provide clues when analyzing traffic from systems with multiple IP addresses.

Example observed sequence:

```text
10.129.1.100 → 10.129.1.1   id 1337
10.129.1.100 → 10.129.1.1   id 1338
10.129.2.200 → 10.129.1.1   id 1340
```

A continuous sequence can suggest that multiple addresses belong to the same underlying host.

## Record Route

The room demonstrates the IP Record-Route option with:

```bash
ping -c 1 -R 10.129.143.158
```

The output can show intermediate IP addresses observed along the path.

## Traceroute Concept

The room explains TTL-based route discovery:

1. Send a packet with a small TTL.
2. A router decrements the TTL.
3. When TTL reaches zero, an ICMP Time-Exceeded response identifies the router.
4. Increase TTL and repeat.
5. Continue until the destination responds.

## IP Payload

The payload contains upper-layer data such as TCP or UDP information.

## TCP Segment

TCP data is carried inside IP packets. The TCP header includes fields such as source port, destination port, and sequence information.

## UDP Datagram

UDP sends connectionless datagrams without establishing a connection first.

When UDP is used with traceroute, a destination can return an ICMP Port Unreachable response when the probe reaches it.

## Blind Spoofing

The room defines blind spoofing as sending forged information without being able to observe the target's responses. It involves manipulating packet-header information.

The material describes this as a technique that can affect the integrity of network connections.

## Pentesting Relevance

Packet analysis can help answer:

```text
Who is communicating?
What protocol is being used?
Where did the packet travel?
What routes are visible?
Are there multiple addresses associated with one host?
What does the packet header reveal?
```
