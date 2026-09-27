# OhSINT

**Platform:** TryHackMe
**Category:** OSINT
**Difficulty:** Easy
**Status:** Completed

---

## 🎯 Objective

Use **Open Source Intelligence (OSINT)** techniques to extract information about a person from a single image.

The investigation involved:

* Extracting image metadata
* Identifying the image owner
* Searching public sources
* Correlating information across multiple websites
* Using WiGLE to investigate Wi-Fi information
* Inspecting website source code

---

## 🔍 What I Did

### 1. Extracted Image Metadata

The provided image was analyzed using **ExifTool**.

```bash
exiftool image.jpg
```

Important metadata discovered:

```text
File Type       : JPEG
Image Width     : 1920
Image Height    : 1080
Copyright       : OWoodflint
GPS Latitude    : 54.2947963
GPS Longitude   : -2.2503684
GPS Position    : 54.2947963 -2.2503684
```

The `Copyright` field revealed the possible username:

```text
OWoodflint
```

The GPS coordinates also provided a useful starting point for identifying the person's location.

---

### 2. Identified the User

I searched for:

```text
OWoodflint
```

using search engines and public websites.

Information related to the username was scattered across several platforms, including:

* GitHub
* X / Twitter
* WordPress

The same username was used to correlate information between these sources.

---

### 3. Investigated Social Media

The user's social media presence provided additional information that could be correlated with the other OSINT findings.

This helped identify information such as:

* Avatar
* Location
* Wi-Fi information
* Other publicly available details

---

### 4. Used WiGLE

I used **WiGLE** to investigate the wireless network information associated with the location.

The Wi-Fi information helped identify the **SSID of the WAP** the user had connected to as it was provided in one of his X tweet

---

### 5. Investigated WordPress

A WordPress website associated with the username contained additional information.

I inspected the website's source code because some information was not immediately visible on the rendered page.

The person's password was present in the source code and had been made difficult to notice by changing the text colour to white.

This demonstrates why inspecting **HTML/source code** can sometimes reveal information that is hidden from normal visual inspection.

---

## 🛠️ Tools Used

| Tool                                  | Purpose                                        |
| ------------------------------------- | ---------------------------------------------- |
| ExifTool                              | Extract image metadata and GPS information     |
| Google/Search Engine                  | Search for usernames and public information    |
| GitHub                                | Investigate username and public repositories   |
| X/Twitter                             | Investigate social media information           |
| WordPress                             | Discover additional information                |
| WiGLE                                 | Investigate wireless networks/SSID information |
| Browser Developer Tools / View Source | Inspect webpage source code                    |

---

## 📍 Important Findings

### Image Metadata

```text
Copyright : OWoodflint

GPS:
Latitude  : 54.2947963
Longitude : -2.2503684
```

The metadata provided the first major lead.

### Username

```text
OWoodflint
```

This username was then searched across multiple public platforms.

### OSINT Correlation

The investigation followed this general process:

```text
Image
  ↓
ExifTool
  ↓
Metadata
  ↓
OWoodflint
  ↓
Search Engines
  ↓
GitHub / X / WordPress
  ↓
Cross-reference information
  ↓
WiGLE
  ↓
SSID / Location
  ↓
Additional OSINT findings
```

---

## 📝 Room Answers

> Replace the placeholders below with the exact answers you recovered from the room.

## 📝 Room Questions

| Question | Result |
|---|---|
| What is this user's avatar of? | Found on X|
| What city is this person in? | Found using OSINT correlation |
| What is the SSID of the WAP he connected to? | Found using WiGLE |
| What is his personal email address? | Found  |
| What site did you find his email address on? | Identified |
| Where has he gone on holiday? | Found |
| What is the person's password? | Found by inspecting page source |

---

## 🧠 What I Learned

* Image metadata can contain valuable OSINT information.
* **ExifTool** can reveal GPS coordinates and other metadata.
* Usernames can be used as identifiers across different platforms.
* OSINT often requires **correlating small pieces of information** from multiple sources.
* WiGLE can be useful when investigating wireless networks.
* Website source code should not be ignored during OSINT investigations.
* Information that is visually hidden on a webpage may still exist in the HTML/source.
* A single image can provide enough information to begin building a larger intelligence picture.

---

## ⚠️ Important Takeaways

The most important part of this room was not a particular tool, but the **investigation methodology**:

```text
Find a clue
   ↓
Identify a username/person
   ↓
Search multiple sources
   ↓
Correlate information
   ↓
Validate findings
   ↓
Follow new leads
   ↓
Extract the required information
```

OSINT is largely about connecting seemingly unrelated pieces of publicly available information.

---

## 🔗 Room

[TryHackMe — OhSINT](https://tryhackme.com/room/ohsint)
