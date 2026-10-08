# Testing Domains

Penetration testing can cover multiple technical and physical domains.
The domains can overlap during a real assessment.

## 1. Network Infrastructure Testing

Focuses on network hosts, services, protocols, and infrastructure.

### What Testers Look For

- Exposed services
- Weak configurations
- Vulnerable services
- Authentication weaknesses
- Network segmentation issues
- Insecure protocols

### Common Activities

- Host discovery
- Port scanning
- Service enumeration
- Vulnerability validation
- Configuration review

## 2. Web Application Security Testing

Tests applications exposed through web interfaces and APIs.

### Common Vulnerabilities

- Injection
- Authentication weaknesses
- Session-management issues
- Access-control problems
- Cross-Site Scripting (XSS)
- Insecure application logic

Web testing requires understanding HTTP, application architecture,
authentication, authorization, and how client/server components
interact.

## 3. Mobile Application Security Testing

Assesses mobile applications and their supporting services.

### Areas Examined

- Application behavior
- Authentication
- Data storage
- Communication with backend services
- API interactions
- Client-side security

## 4. Cloud Infrastructure Security Testing

Assesses cloud-hosted infrastructure and services.

Important areas include:

- Identity and Access Management (IAM)
- Storage
- Network controls
- Cloud configuration
- APIs
- Data protection
- Containers and cloud-native applications

Cloud testing requires understanding the cloud provider’s testing
policies and the shared-responsibility model.

## 5. Physical Security Testing

Evaluates physical controls protecting systems and facilities.

Examples:

- Perimeter controls
- Locks
- Access-control systems
- Badge systems
- Visitor procedures
- Physical barriers

## 6. Social Engineering

Tests whether people and organizational processes resist authorized
social-engineering scenarios.

Examples:

- Phishing
- Spear phishing
- Pretexting
- Baiting
- Physical social engineering

These activities require explicit authorization and controlled
scenarios.

## 7. Wireless Network Security Testing

Assesses wireless networks and their security controls.

Areas can include:

- Wireless authentication
- Encryption
- Network configuration
- Access controls
- Exposure of wireless infrastructure

## 8. Software Security Testing

Examines software for security weaknesses.

Testing can involve:

- Code and application behavior
- Input handling
- Authentication and authorization
- Security controls
- Vulnerability validation

## Testing Domains Can Overlap

A single attack path can cross multiple domains.

Example:

``` text
Web Application
      ↓
API
      ↓
Cloud Service
      ↓
Identity / Access Control
      ↓
Internal Network
```

## Key Takeaway

The testing domain should match the organization’s assets, threat model,
and authorized scope. A penetration tester should understand how
different domains interact rather than treating each domain as
completely isolated.
