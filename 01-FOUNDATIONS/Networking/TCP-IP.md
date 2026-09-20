# TCP/IP

## IPv4
- 32-bit address
- Written as 4 octets
- Example: `192.168.1.10`
- ~4.3 billion addresses

## IPv6
- 128-bit address
- Hexadecimal
- Example: `2001:db8::1`
- Can be compressed like `2001:0db8:85a3:0000:0000:000:0000:0732` =`2001:db8:85a3::732`
- Much larger address space


## TCP vs UDP
### TCP
- Connection-oriented
- Reliable
- Ordered delivery
- ACK + retransmission
- More overhead

### UDP
- Connectionless
- Faster
- No delivery guarantee
- No ordering
- Less overhead


## TCP 3-Way Handshake

1. Client → SYN
2. Server → SYN-ACK
3. Client → ACK

Connection established.


## Common Ports

| Port | Service |
|------|---------|
| 20/21| FTP     |
| 22   | SSH     |
| 25   | SMTP    |
| 53   | DNS     |
| 80   | HTTP    |
| 443  | HTTPS   |
| 445  | SMB     |
| 3389 | RDP     |

### Security
Ports help identify running services during enumeration.