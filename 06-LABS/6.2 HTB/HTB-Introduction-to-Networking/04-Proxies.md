# 04 - Proxies

## Definition

A proxy is a device or service that sits between two endpoints and acts as a mediator for a connection.

## Forward Proxy

A forward proxy handles requests made by clients:

```text
Client → Forward Proxy → Internet
```

Common uses include web filtering and controlling outbound access.

## Reverse Proxy

A reverse proxy handles incoming traffic before it reaches backend systems:

```text
Internet → Reverse Proxy → Web Server
```

Common uses include:

- Traffic filtering
- Hiding backend systems
- WAF functionality
- DDoS protection

The room mentions Cloudflare and ModSecurity as examples.

## Transparent Proxy

The client does not explicitly know the proxy is present.

## Non-Transparent Proxy

The client or application is configured to communicate through the proxy.

## Pentesting Relevance

Understanding proxies helps explain:

- Where traffic is inspected.
- Which system is actually receiving a request.
- Why backend systems may not be directly exposed.
- Where security controls such as WAFs are placed.

## Practical Mental Model

```text
Client
  ↓
Proxy / WAF
  ↓
Backend
```
