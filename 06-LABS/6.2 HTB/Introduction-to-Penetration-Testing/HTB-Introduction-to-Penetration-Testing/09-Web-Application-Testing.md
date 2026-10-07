# Web Application Testing

## Web Application Architecture

Web applications generally involve interactions between clients,
servers, application logic, databases, APIs, authentication systems, and
other services.

A tester needs to understand how these components communicate and where
security controls are applied.

## Common Web Application Vulnerabilities

### Injection

Injection weaknesses can occur when untrusted input is interpreted as
commands or queries by another component.

### Authentication and Session Management

Testing should examine how users authenticate and how sessions are
created, maintained, and protected.

### Cross-Site Scripting (XSS)

XSS occurs when attacker-controlled content is interpreted as executable
script in a user’s browser.

## Essential Tools and Skills

Web testing requires understanding:

- HTTP requests and responses
- Headers
- Cookies
- Authentication
- Sessions
- Parameters
- APIs
- Application logic

Common testing tools can include an intercepting proxy such as Burp
Suite and other tools appropriate to the authorized assessment.

## Testing Principle

Do not rely only on automated scanning.

Understand how the application works, manually inspect important
functionality, and validate security controls.

## Legal and Ethical Boundaries

Only test web applications that are explicitly authorized.

Stay within:

- Defined scope
- Approved testing methods
- Testing windows
- Data-handling requirements

## Practical Workflow

``` text
Map Application
      ↓
Identify Endpoints
      ↓
Understand Requests / Responses
      ↓
Identify Authentication & Access Controls
      ↓
Test Inputs and Application Logic
      ↓
Validate Findings
      ↓
Collect Evidence
      ↓
Report
```

## Key Takeaway

Effective web application testing requires understanding the
application’s behavior rather than simply running vulnerability
scanners.
