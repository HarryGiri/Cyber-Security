# CIDR & Subnetting

## CIDR
CIDR = Classless Inter-Domain Routing

Example:

`192.168.1.0/24`

- `/24` = network prefix
- Remaining bits = host portion

### Common CIDR

| CIDR| Addresses |
|-----|-----|
| /24 | 256 |
| /25 | 128 |
| /26 | 64  |
| /27 | 32  |
| /28 | 16  |
| /29 | 8   |
| /30 | 4   |

Usable hosts usually:
`Total addresses - 2`


## Subnetting
- Dividing one network into smaller networks
- Helps with:
  - IP management
  - Network organization
  - Reducing broadcast traffic
  - Network segmentation

