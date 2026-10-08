# 06 - OSI Model

## Seven Layers

| Layer | Name | Main Function |
|---:|---|---|
| 7 | Application | Application-level input/output and services |
| 6 | Presentation | Data representation / translation |
| 5 | Session | Logical communication sessions |
| 4 | Transport | End-to-end data transport, segmentation, flow control |
| 3 | Network | Addressing and routing |
| 2 | Data Link | Frames and transmission over the local medium |
| 1 | Physical | Signals and transmission media |

## Data Direction

Sender:

```text
L7 → L6 → L5 → L4 → L3 → L2 → L1
```

Receiver:

```text
L1 → L2 → L3 → L4 → L5 → L6 → L7
```

## Pentesting Perspective

Use the model as a troubleshooting and analysis map rather than only memorizing the layer names.

Example:

```text
Web issue        → Layer 7
TCP/UDP issue    → Layer 4
Routing issue    → Layer 3
ARP/MAC issue    → Layer 2
Physical link    → Layer 1
```
