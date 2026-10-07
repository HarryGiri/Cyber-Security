# Types of Penetration Tests

Penetration tests can be classified according to the information
provided to the tester and the perspective from which testing is
performed.

## Classification by Information Provided

### Black Box Testing

The tester starts with little or no internal information about the
target.

**Focus:**

- External reconnaissance
- Attack-surface discovery
- Enumeration
- Discovering weaknesses from an attacker’s perspective

**Advantage:** closely represents an external attacker with limited
knowledge.

**Limitation:** testing can require more time because information must
be discovered during the engagement.

### White Box Testing

The tester receives extensive information about the target, such as
architecture, source code, credentials, or internal documentation.

**Focus:**

- Deep technical analysis
- Internal weaknesses
- Application and architecture review
- More complete coverage

**Advantage:** provides greater visibility and can uncover issues that
are difficult to identify externally.

**Limitation:** does not represent a completely unknown external
attacker.

### Gray Box Testing

The tester receives limited internal information.

It combines aspects of black-box and white-box testing and can represent
a user or attacker who has some legitimate knowledge or access.

### Comparison

| Type      | Tester Knowledge | Main Perspective                 |
|-----------|------------------|----------------------------------|
| Black Box | Little / none    | External attacker                |
| Gray Box  | Limited          | Partially informed attacker/user |
| White Box | Extensive        | Deep/internal assessment         |

## Classification by Testing Perspective

### External Testing

Testing is performed from outside the organization’s trusted
environment.

Typical focus:

- Internet-facing hosts
- Public services
- External applications
- Perimeter security
- Exposed attack surface

### Internal Testing

Testing is performed from inside the organization’s environment.

Typical focus:

- Internal systems
- Internal services
- Access controls
- Segmentation
- Potential attack paths after initial access

### External vs Internal

| External                       | Internal                                  |
|--------------------------------|-------------------------------------------|
| Internet-facing attack surface | Internal attack surface                   |
| External attacker perspective  | Insider/compromised-host perspective      |
| Public services                | Internal services and trust relationships |

## Social Engineering and Physical Testing

Penetration testing can also include human and physical attack paths
when explicitly authorized.

Examples include:

- Social engineering
- Physical access attempts
- Tailgating assessments
- Testing physical security controls

### Tailgating

Tailgating is an attempt to gain access to a restricted area by
following an authorized person through a controlled entrance.

Physical findings can include weaknesses in:

- Entry controls
- Visitor procedures
- Badge systems
- Security awareness
- Physical barriers

## Key Classification Summary

When documenting a penetration test, clearly identify:

- Testing perspective: external or internal.
- Tester knowledge: black, gray, or white box.
- Authorized attack domains.
- Scope and limitations.

The classification affects how realistic the test is for a particular
threat model and how the results should be interpreted.
