# 07 - TCP/IP Model

## Four Layers

| Layer | Name | Main Function |
|---:|---|---|
| 4 | Application | Application protocols and services |
| 3 | Transport | TCP sessions and UDP datagrams |
| 2 | Internet | IP addressing and routing |
| 1 | Link | Transmission over the network medium |

## Important Responsibilities

| Task | Protocol | Role |
|---|---|---|
| Logical addressing | IP | Addresses networks and hosts |
| Routing | IP | Moves packets toward the destination |
| Error / control flow | TCP | Maintains reliable connections |
| Application support | TCP / UDP | Ports distinguish application communication |
| Name resolution | DNS | Resolves names to IP addresses |

## OSI Mapping

```text
OSI                         TCP/IP
Application                 Application
Presentation             ┐
Session                  ├→ Application
Transport                  Transport
Network                    Internet
Data Link                ┐
Physical                 ┘→ Link
```

## Pentesting Relevance

The model helps connect practical observations to the correct layer:

```text
Application → Port → IP / Route → Link
```
