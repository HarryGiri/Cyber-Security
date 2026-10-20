# Cryptography Basics

## Lab Overview

| Field | Details |
|---|---|
| Platform | TryHackMe |
| Room | Cryptography Basics |
| Difficulty | Introductory |
| Category | Cryptography, Encryption, Basic Mathematics |
| Status | Completed |

## 1. Learning Objectives

- Understand essential cryptography terminology.
- Explain why cryptography is necessary.
- Work with the Caesar cipher.
- Compare symmetric and asymmetric encryption.
- Understand XOR and modulo operations.

## 2. Importance of Cryptography

Cryptography enables secure communication in the presence of potential adversaries. It supports confidentiality, integrity, and authentication.

### Common applications

- HTTPS protects data exchanged between browsers and web servers.
- SSH establishes an encrypted remote-access session.
- Digital certificates help verify server identity.
- Cryptographic hashes help verify data integrity.
- Encryption protects sensitive information stored on devices and transmitted over networks.

**Payment card security standard:** PCI DSS (Payment Card Industry Data Security Standard).

### Key security goals

| Goal | Meaning |
|---|---|
| Confidentiality | Prevent unauthorized parties from reading data |
| Integrity | Detect unauthorized changes to data |
| Authentication | Verify the identity of a user, device, or service |

## 3. Cryptography Terminology

| Term | Definition |
|---|---|
| Plaintext | Original readable message or data |
| Ciphertext | Encrypted, unintelligible representation of data |
| Cipher | Algorithm used to encrypt or decrypt data |
| Key | Value used by a cryptographic algorithm |
| Encryption | Conversion of plaintext into ciphertext |
| Decryption | Recovery of plaintext from ciphertext using the appropriate key |

A simplified encryption model:

\[
C = E_K(P)
\]

Where \(P\) is plaintext, \(K\) is the key, \(E\) is the encryption function, and \(C\) is ciphertext.

Decryption reverses the process:

\[
P = D_K(C)
\]

## 4. Historical Ciphers — Caesar Cipher

The Caesar cipher shifts each letter by a fixed number of positions in the alphabet.

Example:

- Plaintext: `TRYHACKME`
- Key: `3`
- Direction: Right
- Ciphertext: `WUBKDFNPH`

To decrypt, shift each letter left by three positions.

### Important characteristics

- It is a substitution cipher.
- The key is the shift value.
- There are only 25 non-trivial shifts for the English alphabet.
- An attacker can try every possible shift in a brute-force attack.
- It is insecure for protecting modern sensitive information.

### Python implementation

```python
def caesar_cipher(text, shift):
    result = ""

    for char in text:
        if char.isalpha():
            base = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - base + shift) % 26 + base)
        else:
            result += char

    return result

print(caesar_cipher("TRYHACKME", 3))
print(caesar_cipher("WUBKDFNPH", -3))
```

**Key lesson:** A cipher with a small key space is vulnerable to brute force.

## 5. Types of Encryption

### Symmetric encryption

Symmetric encryption uses the **same secret key** for encryption and decryption.

Examples:

- DES — Data Encryption Standard
- 3DES — Triple DES
- AES — Advanced Encryption Standard

| Algorithm | Key information | Security notes |
|---|---|---|
| DES | 56-bit key | Insecure; do not trust for modern protection |
| 3DES | Commonly described as 168-bit nominal keying, with about 112-bit effective security | Deprecated; avoid for new systems |
| AES | 128-, 192-, or 256-bit keys | Widely used modern symmetric cipher |

**Main challenge:** The communicating parties must securely share and protect the secret key.

### Asymmetric encryption

Asymmetric cryptography uses a pair of mathematically related keys:

- **Public key:** Can be shared with others.
- **Private key:** Must be kept secret.

For confidentiality, a sender can encrypt data using the recipient's public key; the recipient decrypts it with their private key.

Examples include:

- RSA
- Diffie–Hellman key exchange
- Elliptic Curve Cryptography (ECC)

**Important distinction:** Diffie–Hellman is primarily a key-agreement method, rather than a direct message-encryption algorithm. Digital signatures also use asymmetric cryptography, but their purpose is to support authenticity and integrity rather than confidentiality.

Asymmetric operations are generally slower than symmetric encryption. Secure protocols commonly use asymmetric cryptography to establish or agree on keys, then use symmetric encryption for bulk data.

### Symmetric vs. asymmetric

| Property | Symmetric | Asymmetric |
|---|---|---|
| Keys | One shared secret key | Public/private key pair |
| Main challenge | Securely sharing the secret | Protecting the private key and authenticating public keys |
| Typical performance | Faster | Generally slower |
| Examples | AES | RSA, ECC-based systems |

## 6. Basic Mathematics

### XOR operation

XOR means *exclusive OR*. It returns `1` when two input bits differ and `0` when they match.

| A | B | A XOR B |
|---:|---:|---:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Example:

```text
  1010
⊕ 1100
------
  0110
```

Useful properties:

- \(A \oplus A = 0\)
- \(A \oplus 0 = A\)
- \(A \oplus B = B \oplus A\)
- \((A \oplus B) \oplus B = A\)

A simple XOR-based transformation is:

\[
C = P \oplus K
\]

Since XORing with the same key again reverses the operation:

\[
P = C \oplus K
\]

This illustrates a mathematical property, **not a recommendation to design your own encryption**. Secure cryptographic systems require appropriate algorithms, key management, and additional protections.

### Modulo operation

Modulo returns the remainder after division.

Examples:

| Expression | Result |
|---|---:|
| \(25 \bmod 5\) | 0 |
| \(23 \bmod 6\) | 5 |
| \(23 \bmod 7\) | 2 |
| \(60 \bmod 12\) | 0 |

For a positive modulus \(n\), the remainder is in the range \(0\) through \(n-1\).

Modulo arithmetic is useful in cryptography for operations involving large integers, modular exponentiation, and number-theoretic algorithms.

### Python examples

```python
# XOR
print(0b1001 ^ 0b1010)

# Modulo
print(118613842 % 9091)
print(60 % 12)
```



## 7. Key Takeaways

- Cryptography helps protect confidentiality, integrity, and authenticity.
- Plaintext is transformed into ciphertext through encryption.
- Caesar cipher is a historical cipher that can be brute-forced easily.
- Symmetric encryption uses a shared secret key; asymmetric cryptography uses a public/private key pair.
- DES is insecure, while AES remains widely used.
- XOR has reversible properties when the same key is applied again.
- Modulo arithmetic is fundamental to many cryptographic algorithms.

