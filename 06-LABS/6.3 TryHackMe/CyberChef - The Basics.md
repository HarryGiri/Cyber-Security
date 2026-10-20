# TryHackMe — CyberChef: The Basics

## Lab Overview

| Field | Details |
|---|---|
| Platform | TryHackMe |
| Room | CyberChef: The Basics |
| Difficulty | Beginner |
| Category | Data Encoding, Decoding, Data Extraction |
| Status | Completed — 100% |

## 1. Learning Objectives

- Understand CyberChef and its purpose.
- Navigate the four main interface areas.
- Build and execute recipes.
- Extract useful information from text.
- Encode, decode, and transform data.
- Convert between common data representations.

## 2. What Is CyberChef?

[CyberChef](https://gchq.github.io/CyberChef/) is a browser-based tool for analyzing and transforming data using individual operations arranged into a **recipe**.

Common uses include:

- Decoding Base64 and Base85.
- URL encoding and decoding.
- Converting between text, binary, hexadecimal, and decimal.
- Extracting IP addresses, URLs, and email addresses.
- Converting Unix timestamps.
- Performing basic cryptographic transformations.

CyberChef is useful during security investigations when data appears encoded, transformed, or difficult to interpret.

**Access options:**
- Online: https://gchq.github.io/CyberChef
- Local/offline: [CyberChef releases on GitHub](https://github.com/gchq/CyberChef/releases)

Avoid pasting confidential or sensitive data into an online tool unless its handling is appropriate for your environment. A local copy may be preferable for sensitive investigations.

## 3. Understanding the Interface

CyberChef has four main areas:

| Area | Purpose |
|---|---|
| Operations | Search for and select available transformations |
| Recipe | Arrange operations in the order they should run |
| Input | Paste text or provide files to process |
| Output | Inspect, copy, or save the result |

### Recipe controls

- **Save Recipe:** Save the current sequence of operations.
- **Load Recipe:** Load a previously saved recipe.
- **Clear Recipe:** Remove the selected operations.
- **BAKE!:** Run the recipe manually.
- **Auto Bake:** Re-run the recipe when input or operations change.

### General workflow

1. Define the objective.
2. Paste or upload the input data.
3. Select suitable operations and configure their parameters.
4. Inspect the output and determine whether it meets the objective.
5. If necessary, revise the recipe and try again.

**Key principle:** Choose operations based on evidence and the expected data format, not by randomly applying every available transformation.

## 4. Common CyberChef Operations

### Data extraction

These operations identify useful information embedded in larger input strings.

| Operation | Purpose |
|---|---|
| Extract IP addresses | Find IPv4 and IPv6 addresses |
| Extract URLs | Identify URLs in the input |
| Extract email addresses | Identify email addresses |

These are especially useful when reviewing logs, copied text, configuration files, or investigation artifacts.

### Data format and encoding

| Operation | Purpose | Example |
|---|---|---|
| From Base64 | Decode Base64 data | `V2VsY29tZQ==` → `Welcome` |
| To Base64 | Encode data as Base64 | `THM` → `VEhN` |
| URL Decode | Convert percent-encoded characters back to their original representation | `%3A` → `:` |
| URL Encode | Percent-encode characters | `:` → `%3A` |
| From Base85 | Decode Base85-encoded data | Depends on input and variant |
| From Base58 | Decode Base58 data | Depends on input |
| To Base62 | Encode data using Base62 | Depends on input and implementation |
| To Hex | Convert bytes to hexadecimal | `A` → `41` |
| To Decimal | Represent bytes as decimal values | `A` → `65` |
| From Morse Code | Convert Morse code into text | `- .... .` → `THE` |
| ROT13 | Rotate alphabetic characters by 13 positions | `ABC` → `NOP` |

**Important distinction:** Encoding is not encryption. Base64, hexadecimal, and URL encoding do not provide confidentiality; their output can generally be reversed without a secret key.

### Date and time

| Operation | Purpose |
|---|---|
| From UNIX Timestamp | Convert a Unix timestamp to a readable date/time |
| To UNIX Timestamp | Convert a date/time into a Unix timestamp |

A Unix timestamp counts seconds from the Unix epoch: `1970-01-01 00:00:00 UTC`.

When interpreting timestamps, check whether the result is shown in UTC or another time zone.

## 5. Base64 Fundamentals

Base64 converts binary data into a text representation using a 64-character alphabet. It is commonly used to represent data in systems that expect text.

### Example: Encode `THM`

ASCII bytes:

| Character | Decimal | 8-bit binary |
|---|---:|---|
| T | 84 | `01010100` |
| H | 72 | `01001000` |
| M | 77 | `01001101` |

Concatenate the binary values:

```text
010101000100100001001101
```

Split into six-bit groups:

```text
010101 000100 100001 001101
```

Convert each group to decimal:

```text
21 4 33 13
```

Map the values to the Base64 alphabet:

```text
21 -> V
 4 -> E
33 -> h
13 -> N
```

Final Base64 representation:

```text
VEhN
```

### Practical notes

- Base64 uses groups of six bits to select characters from its alphabet.
- Padding characters such as `=` may appear at the end.
- Decoding Base64 does not require a secret key.
- Base64 is not a secure way to hide passwords or other sensitive information.

## 6. URL Encoding and Decoding

URL encoding represents certain characters using percent-encoded byte values.

Examples:

| Character | Encoded representation |
|---|---|
| `:` | `%3A` |
| `/` | `%2F` |
| `.` | `%2E` |
| `=` | `%3D` |
| `#` | `%23` |

Example:

```text
Encoded:
https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics

Decoded:
https://tryhackme.com/r/room/cyberchefbasics
```

URL encoding is a representation technique, not encryption.

## 7. Practical Exercises — Room Answers

### Task 5: Practice

| Question | Answer |
|---|---|
| Hidden email address | `hidden@hotmail.com` |
| Hidden IP ending in `.232` | `102.20.11.232` |
| Domain beginning with `T` | `TryHackMe.com` |
| Binary value of decimal `78` | `01001110` |
| URL-encoded careers URL | `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Fcareers` |

### Task 6: Your First Official Cook

| Question | Answer |
|---|---|
| IP that starts and ends with `10` | Completed |
| Base64 encoding of `Nice Room!` | Completed |
| Decode the supplied CyberChef Basics URL | Completed |
| Unix timestamp `1725151258` | Completed |
| Base85 decoded string | Completed |

## 8. Recommended Investigation Workflow

When you encounter an unknown string during a lab or authorized investigation:

1. **Preserve the original input.** Keep a copy so transformations do not destroy your evidence.
2. **Identify clues.** Look for character sets, padding, prefixes, separators, and recognizable patterns.
3. **Choose an operation.** Use Base64 decoding for likely Base64 data, URL decoding for percent escapes, or extraction operations for indicators.
4. **Build a recipe.** Apply multiple operations only when the evidence supports the sequence.
5. **Validate the output.** Check whether the result is readable and consistent with the expected format.
6. **Document the result.** Record the input, operations, relevant settings, and verified output.

## 9. Key Takeaways

- CyberChef is a versatile tool for data transformation and investigation.
- Operations are chained together through recipes.
- The four interface areas are Operations, Recipe, Input, and Output.
- Extraction tools help locate indicators such as IP addresses, URLs, and email addresses.
- Base64 and URL encoding are reversible representations, not encryption.
- Unix timestamps can help correlate events during log analysis.
- Always validate decoded output and preserve original evidence.
