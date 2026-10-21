# W1seGuy

## Lab Overview

| Field | Details |
|---|---|
| Platform | TryHackMe |
| Room | W1seGuy |
| Difficulty | Beginner |
| Category | Cryptography / XOR |
| Status | Completed |

## 1. Learning Objectives

-   Review the provided Python source code before interacting with the
    service.
-   Understand the XOR operation and why XOR can reverse an XOR
    transformation.
-   Connect to a TCP service using Netcat.
-   Recognize hexadecimal-encoded ciphertext.
-   Use known plaintext (`THM{`) to recover part of a repeating XOR key.
-   Use CyberChef to decode and validate the result.
-   Document evidence and verify the result with the TryHackMe room.

## 2. Lab Scope and Setup

This exercise was performed against the TryHackMe W1seGuy room and its
assigned lab machine.

The service listened on TCP port `1337`. 

Connect using the IP shown in your active room session:

``` bash
nc <TARGET_IP> 1337
```

Before connecting, I downloaded and reviewed the Python source file
provided by the room.

## 3. Technical Background

### XOR property

XOR (`⊕`) compares bits and returns `1` when the bits differ and `0`
when they match. XOR is reversible because applying the same key twice
restores the original value:

(P `⊕` K) `⊕` K = P
     

Where:

-   `P` is the plaintext.
-   `K` is the key.
-   `C = P ⊕ K` is the ciphertext.

For a repeating-key XOR cipher, the key bytes repeat across the
ciphertext.

### Known-plaintext clue

The room's flag format begins with the known prefix `THM{`. If the first
four ciphertext bytes are XORed with the bytes for `THM{`, the result
reveals the first four key characters.

## 4. Methodology

### Step 1 --- Download and review the source code

I downloaded and reviewed the Python source file provided in the room to understand how the encryption key was generated and how Flag 1 was XOR-encoded.

### Step 2 --- Connect to the TCP service

I connected to the target using Netcat:

``` bash
nc <TARGET_IP> 1337
```

The service returned a hexadecimal string labelled as the XOR-encoded
first flag and prompted for the encryption key.

**Evidence collected:** terminal output showing the connection and
encoded message. The target IP and ciphertext are session-specific.

### Step 3 --- Identify the ciphertext and known prefix

I treated the supplied message as hexadecimal-encoded bytes. I used the
known flag prefix `THM{` as known plaintext.

For my session, the first four ciphertext bytes were:

``` text
3d1e2a23
```

### Step 4 --- Recover the first four key characters

I XORed the first four ciphertext bytes with the ASCII bytes for `THM{`.
This recovered the first four characters of the key:

``` text
iVgX
```

This was a partial key, not yet the complete key. I needed to determine
the final character and validate the full key against the message.

### Step 5 --- Configure CyberChef

I opened [CyberChef](https://gchq.github.io/CyberChef/) and created a
recipe with these operations in order:

1.  **From Hex** --- converts the hexadecimal input into bytes.
2.  **XOR** --- applies the candidate key using the **Standard** scheme.

I used the ciphertext from my active session as the input. In the XOR
operation, I set the key encoding to **UTF-8** and entered the candidate
key.

The recipe structure was:

``` text
Input (hexadecimal ciphertext)
        |
        v
     From Hex
        |
        v
 XOR (UTF-8 key, Standard scheme)
        |
        v
   Decoded output
```

### Step 6 --- Determine the final key character

Since the first four characters were known, I tested possible fifth
characters from the set:

``` text
a-z, A-Z, 0-9
```

I checked the resulting output for readable plaintext and the expected
flag format. I then validated the candidate by submitting it to the
TryHackMe service.

**Note:** This was a bounded candidate search for the final character in
the assigned lab, not an attempt against an unrelated service.

### Step 7 --- Validate with the room

After submitting the complete key to the active Netcat session, the
service confirmed that the key was correct and returned the second flag.
I also submitted the first flag through the room's answer field and
received confirmation.

Flag values are intentionally omitted from this public-facing write-up.
Keep any required answer values in the TryHackMe room rather than
committing them to a public repository.

## 5. CyberChef Recipe Summary

  Operation    Configuration         Purpose
  ------------ --------------------- -----------------------------------
  From Hex     Delimiter: Auto       Convert the hex string to bytes
  XOR          Key encoding: UTF-8   Apply the candidate repeating key
  XOR scheme   Standard              Use the standard XOR operation

The key field must contain the **complete key** when validating the
final output. The four-character value recovered from the known prefix
is only the starting portion.

## 6. Evidence

The screenshot below is taken from the screenshots attached to my source
document. Visible flag values have been redacted before including it in
this write-up.

![W1seGuy CyberChef and terminal evidence with flag values
redacted](images/w1seguy-evidence-redacted.png)

## 7. Results

-   Reviewed the room-provided Python source code.
-   Connected to the assigned service on TCP port `1337`.
-   Identified the message as hexadecimal ciphertext using repeating-key
    XOR.
-   Used the known prefix `THM{` to recover the first four key
    characters.
-   Configured a CyberChef recipe using **From Hex** followed by
    **XOR**.
-   Tested possible final key characters and checked the decoded output.
-   Validated the key and flag submission with TryHackMe.
-   Completed both flag objectives.

## 8. Key Takeaways

-   XOR is reversible when the same key is applied again.
-   Known plaintext can reveal part of an XOR key.
-   Hexadecimal is a data representation; converting from hex does not
    itself decrypt the data.
-   CyberChef recipes depend on correct operation order and key
    encoding.
-   A plausible decoded string should still be validated against the
    challenge service.
-   Reviewing the source code before testing helps explain the
    challenge's intended logic.
-   Screenshots and concise notes provide useful evidence for a
    practical cybersecurity portfolio.

## 9. Tools and References

-   [TryHackMe --- W1seGuy](https://tryhackme.com/room/w1seguy)
-   [CyberChef](https://gchq.github.io/CyberChef/)
-   Netcat (`nc`)
-   Python source file provided by the room

## 10. Safety and Scope

All interaction described here was performed within the
TryHackMe-provided lab environment. Only connect to targets for which
you have explicit authorization.
