# 02 - Network Types

## Common Types

| Type | Meaning |
|---|---|
| WAN | Wide Area Network |
| LAN | Local Area Network |
| WLAN | Wireless LAN |
| VPN | Virtual Private Network |

## WAN

A WAN connects multiple networks across a larger area. The Internet is a major example, but organizations can also operate internal WANs.

## LAN / WLAN

A LAN is a local network such as a home or office network. A WLAN provides similar local connectivity over wireless transmission.

Private IPv4 ranges discussed in the room:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

## VPN Types

### Site-to-Site VPN

Connects complete network ranges, typically through routers or firewalls.

### Remote Access VPN

Creates a virtual interface on a client so it can access a remote network.

The room uses HTB's OpenVPN connection as an example and highlights the routing table created after connecting.

### Split Tunnel

Only selected networks are routed through the VPN. Other Internet traffic uses the normal connection.

### SSL VPN

Provides remote access through a web browser; the room uses browser-delivered applications/desktops such as HTB Pwnbox as an example.

## Additional Terms

| Type | Meaning |
|---|---|
| GAN | Global Area Network |
| MAN | Metropolitan Area Network |
| PAN | Personal Area Network |
| WPAN | Wireless Personal Area Network |

WPAN commonly uses technologies such as Bluetooth and is intended for short-range device communication.

## Pentesting Relevance

During enumeration, identify:

- Private vs public addressing
- Network boundaries
- VPN access
- Remote-access routes
- Wireless connectivity
- Reachable network ranges
