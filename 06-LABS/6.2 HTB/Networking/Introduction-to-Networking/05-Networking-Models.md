# 05 - Networking Models

## Models Covered

The room introduces two layered networking models:

- ISO/OSI
- TCP/IP

## Why Layers Matter

Layering breaks communication into smaller responsibilities so network behavior can be analyzed piece by piece.

## OSI

Seven layers:

```text
7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

## TCP/IP

Four layers:

```text
4 Application
3 Transport
2 Internet
1 Link
```

## Packet Transfer

Data moves down the stack at the sender and up the stack at the receiver.

```text
Sender:   Application → ... → Physical
Receiver: Physical → ... → Application
```

## Encapsulation

Each layer adds information to the data before transmission. The receiver reverses the process.

```text
Data
 ↓
Transport information
 ↓
IP information
 ↓
Frame / Link information
 ↓
Bits
```

## Pentesting Relevance

Use layered thinking to locate where behavior occurs:

- L7: application protocols
- L4: TCP/UDP and ports
- L3: IP and routing
- L2: Ethernet/MAC/ARP
- L1: physical transmission

Both models are useful during packet analysis and troubleshooting.
