# 21 - Cryptography

## Purpose

Cryptography protects information from unauthorized access and helps provide confidentiality, integrity, authentication, and related security properties.

## Symmetric Encryption

Symmetric encryption uses the same secret key to encrypt and decrypt data.

```text
Plaintext
   ↓
[Secret Key]
   ↓
Ciphertext
   ↓
[Same Secret Key]
   ↓
Plaintext
```

### Key Consideration

Both parties need access to the same secret key, so secure key distribution is important.

## Asymmetric Encryption

Asymmetric cryptography uses a key pair:

- Public key
- Private key

The keys have different roles and allow secure communication without sharing one common secret in the same way as symmetric encryption.

## Public-Key Encryption

Public-key systems can support:

- Encryption
- Authentication
- Digital signatures
- Secure key exchange

## DES

Data Encryption Standard (DES) is an older symmetric encryption algorithm.

## AES

Advanced Encryption Standard (AES) is a modern symmetric encryption algorithm and is widely used for protecting data.

## Cipher Modes

The room introduces different block-cipher modes and their role in determining how plaintext blocks are transformed.

Examples discussed include:

| Mode | Key Idea |
|---|---|
| ECB | Encrypts blocks independently |
| CBC | Chains each block with the previous ciphertext block |
| CTR | Uses a counter to produce a keystream |

## Pentesting Relevance

When assessing encrypted services, understand:

- Which cryptographic protocol is used.
- Whether legacy algorithms are enabled.
- How keys are exchanged.
- How authentication is implemented.
- Whether data is protected in transit.

## Key Takeaway

Do not treat "encrypted" as automatically secure. The algorithm, key exchange, authentication, configuration, and implementation all matter.
