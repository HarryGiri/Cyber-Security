# Networking Basics

## OSI Model
7 layers:

1. Physical       → Bits, cables, signals
2. Data Link      → Frames, MAC
3. Network        → Packets, IP, routing
4. Transport      → TCP, UDP, ports
5. Session        → Sessions
6. Presentation   → Encryption, encoding
7. Application    → HTTP, DNS, FTP, SSH

### Order
Physical → Data Link → Network → Transport → Session → Presentation → Application


## TCP/IP Model
4 layers:

1. Network Access   → Ethernet, MAC
2. Internet         → IP, ICMP
3. Transport        → TCP, UDP
4. Application      → HTTP, DNS, SSH, FTP



## MAC vs IP
### MAC
- Hardware address
- Layer 2
- Used inside local network
- Example: `00:1A:2B:3C:4D:5E`

### IP
- Logical address
- Layer 3
- Used to identify/reach devices across networks
- IPv4 / IPv6


## Ports & Sockets
### Port
- Identifies a service/process
- Range: `0–65535`
- 0–1023	    Well-known	Major/common services
- 1024–49151	Registered	Applications/services
- 49152–65535	Dynamic/Ephemeral	Temporary client-side connections

### Socket
- A socket is an endpoint used for communication between two devices/processes over a network.
- IP + Port
- Example: `192.168.1.10:80`


## Routing
- Process of sending packets between networks
- Router decides where packets should go
- Routing table → contains available routes



## NAT

NAT = Network Address Translation
- Converts private IP ↔ public IP
- Allows multiple devices to share one public IP
- Common in home routers

Private ranges:
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

# Common Services

## HTTP
- Port: `80`
- Web traffic
- Not encrypted

## HTTPS
- Port: `443`
- HTTP + TLS
- Encrypted web traffic

## DNS
- Port: `53`
- Domain → IP
- UDP/TCP

## SSH
- Port: `22`
- Secure remote access
- Encrypted

## FTP
- Ports: `20/21`
- File transfer
- Not encrypted by default

## SMB
- Port: `445`
- File/printer sharing
- Common in Windows networks

## Security Relevance

During enumeration:
- Find open ports
- Identify services
- Identify versions
- Check for misconfigurations/vulnerabilities