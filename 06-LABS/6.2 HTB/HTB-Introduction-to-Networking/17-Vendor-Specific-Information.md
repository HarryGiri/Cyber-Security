# 17 - Vendor-Specific Information

## Cisco IOS

Cisco IOS is the operating system used by Cisco network devices such as routers and switches.

The room highlights capabilities including:

- IPv6 support
- Quality of Service (QoS)
- Security features such as encryption and authentication
- Virtual Routing and Forwarding (VRF)
- VLAN-related functionality

## Routing Protocols

The room mentions:

- OSPF
- BGP

These protocols are important when understanding how network traffic is routed.

## Cisco Access

Cisco devices can support remote access through SSH or Telnet.

Example from the room:

```text
$ telnet 10.129.10.2
Trying 10.129.10.2...
Connected to 10.129.10.2.
User Access Verification
Password:
```

The response can reveal that a device is running Cisco IOS.

## VLANs

A VLAN is a logical grouping of network endpoints that creates a separate broadcast domain.

Example from the room:

| Department | VLAN | Subnet |
|---|---:|---|
| Servers | 10 | 192.168.1.0/24 |
| C-Level | 20 | 192.168.2.0/24 |
| Finance | 30 | 192.168.3.0/24 |
| HR | 40 | 192.168.4.0/24 |
| Marketing | 50 | 192.168.5.0/24 |
| Support | 60 | 192.168.6.0/24 |

## VLAN Concepts

The room covers:

- VLAN memberships
- Access ports
- Trunk ports
- VLAN identification
- ISL
- IEEE 802.1Q
- VLAN-capable NICs

## Linux VLAN Interface

The room shows loading the 802.1Q module:

```bash
sudo modprobe 8021q
lsmod | grep 8021
```

Create a VLAN interface with `ip`:

```bash
sudo ip link add link eth0 name eth0.20 type vlan id 20
```

Assign an address and bring it up:

```bash
sudo ip addr add 192.168.1.1/24 dev eth0.20
sudo ip link set up eth0.20
ip a | grep eth0.20
```

## Windows VLAN Configuration

The room also demonstrates Windows PowerShell commands for checking adapter properties and setting a VLAN ID:

```powershell
Get-NetAdapter | Format-Table -AutoSize
Get-NetAdapterAdvancedProperty -DisplayName "vlan id"
Set-NetAdapter -Name "Ethernet 2" -VlanID 10
```

## VLAN Traffic Analysis

VLAN-tagged traffic can be examined in packet captures. The room shows using `tshark` to enumerate observed VLAN IDs.

## VLAN Security

The room discusses:

- VLAN hopping
- Double-tagging attacks

These attacks exploit VLAN/trunk configuration weaknesses.

## VXLAN

VXLAN is discussed as a technology for extending Layer-2 networks over Layer-3 infrastructure.

## Cisco Discovery Protocol (CDP)

CDP can reveal information about Cisco network devices.

Example information visible in CDP traffic can include:

- Device name
- IP address
- Port ID
- Device role/capabilities
- IOS/software information
- Hardware platform

## Pentesting Relevance

Vendor-specific enumeration can expose useful architecture information and reveal segmentation technologies, device types, management interfaces, and routing/switching details.
