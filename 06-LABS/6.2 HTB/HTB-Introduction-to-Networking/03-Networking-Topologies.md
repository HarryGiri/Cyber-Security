# 03 - Networking Topologies

## Definition

A network topology describes the physical or logical arrangement of devices and connections.

### Physical Topology

Describes physical links, cabling, and device placement.

### Logical Topology

Describes how signals and data move through the network.

## Main Components

### Connections

**Wired:** coaxial, fiber, twisted-pair

**Wireless:** Wi-Fi, cellular, satellite

### Nodes

Examples include:

- NICs
- Repeaters
- Hubs
- Bridges
- Switches
- Routers
- Gateways
- Firewalls

## Eight Basic Topologies

| Topology | Main Idea |
|---|---|
| Point-to-Point | Dedicated connection between two hosts |
| Bus | Hosts share a transmission medium |
| Star | Hosts connect through a central component |
| Ring | Hosts form a ring and use a defined direction |
| Mesh | Nodes have multiple paths |
| Tree | Hierarchical arrangement |
| Hybrid | Combination of multiple topologies |
| Daisy Chain | Devices connected sequentially |

## Security Relevance

Topology affects:

- Attack paths
- Segmentation
- Redundancy
- Single points of failure
- Traffic visibility
- Lateral movement

## Pentesting Takeaway

Do not enumerate hosts in isolation. Try to understand the network structure that explains why a host can or cannot reach another host.
