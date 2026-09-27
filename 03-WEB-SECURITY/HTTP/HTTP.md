# HTTP

Web request fundamentals for web security testing and HTB labs.

---

## 1. URL Structure

```text
scheme://user:password@host:port/path?query=value#fragment
```

| Component | Example           | Purpose                   |
| --------- | ----------------- | ------------------------- |
| Scheme    | `http://`         | Protocol                  |
| User Info | `admin:password@` | Optional credentials      |
| Host      | `target.com`      | Domain/IP                 |
| Port      | `:80`             | Service port              |
| Path      | `/dashboard.php`  | Requested resource        |
| Query     | `?id=1`           | Parameters sent to server |
| Fragment  | `#status`         | Client-side page location |

Example:

```text
http://admin:password@target.com:80/dashboard.php?id=1#status
```

### Pentesting Relevance

* **Path** → endpoint/resource enumeration
* **Query parameters** → common input points
* **Host** → virtual-host testing
* **Port** → identifies the web service

---

## 2. HTTP Request Flow

```text
Domain
   ↓
DNS / hosts resolution
   ↓
IP address
   ↓
HTTP request
   ↓
Web server
   ↓
HTTP response
   ↓
Browser
```

### `/etc/hosts`

Local hostname mappings:

```text
/etc/hosts
```

Example:

```text
10.10.10.10    target.htb
```

Useful when a lab requires a specific hostname or virtual host.

---

# 3. cURL

`curl` is a command-line tool for sending HTTP requests.

Useful for:

* Request/response testing
* Header inspection
* Authentication testing
* Reproducing browser requests
* Quick enumeration

### Basic Request

```bash
curl http://target.htb
```

### Headers + Response

```bash
curl -i http://target.htb
```

Useful for checking:

* Status code
* Headers
* Cookies
* Content-Type
* Server information

### Verbose Mode

```bash
curl -v http://target.htb
```

Shows detailed request and connection information.

### Save Response

```bash
curl -o page.html http://target.htb/index.html
```

Using remote filename:

```bash
curl -O http://target.htb/index.html
```

### Silent Mode

```bash
curl -s http://target.htb
```

Useful in scripts and automated enumeration.

### Basic Authentication

```bash
curl -u username:password http://target.htb
```

### Custom User-Agent

```bash
curl -A "Mozilla/5.0" http://target.htb
```

### Custom Header

```bash
curl -H "X-Test: test" http://target.htb
```

### POST Data

```bash
curl -d "username=test&password=test" http://target.htb/login
```

### Help

```bash
curl -h
curl --help all
man curl
```

---

# 4. HTTPS

## HTTP vs HTTPS

| HTTP                       | HTTPS                       |
| -------------------------- | --------------------------- |
| Clear-text communication   | TLS-encrypted communication |
| Default port `80`          | Default port `443`          |
| Traffic can be intercepted | Protects data in transit    |
| `http://`                  | `https://`                  |

### Pentesting Relevance

Without HTTPS, sensitive information such as:

* Usernames
* Passwords
* Session data
* Request parameters

may be visible to someone able to capture network traffic.

---

## HTTPS Flow

```text
http://target.htb
       ↓
HTTP request → Port 80
       ↓
301/302 Redirect
       ↓
https://target.htb
       ↓
TLS Handshake
       ↓
Encrypted HTTP communication → Port 443
```

### TLS Handshake — High Level

```text
Client
  ↓
Client Hello
  ↓
Server Hello + Certificate
  ↓
Certificate / Key verification
  ↓
Key exchange
  ↓
Encrypted session
  ↓
HTTP communication over TLS
```

HTTP requests/responses are encrypted after the TLS handshake.

---

## Certificate Validation

cURL validates TLS certificates by default.

An invalid/untrusted certificate may produce:

```text
curl: (60) SSL certificate problem
```

Common in lab environments using self-signed certificates.

### Ignore Certificate Validation

```bash
curl -k https://target.htb
```

`-k` / `--insecure` skips certificate verification.

Use only when appropriate in authorized lab environments.

### HTTPS with cURL

```bash
curl https://target.htb

curl -i https://target.htb

curl -v https://target.htb

curl -k https://target.htb

curl -ki https://target.htb
```

### Key Takeaways

* Check both ports `80` and `443`.
* HTTP may redirect to HTTPS.
* HTTPS uses TLS encryption.
* Lab certificates may be invalid.
* `-k` can bypass certificate validation during authorized lab testing.
* HTTPS does **not** eliminate application-level vulnerabilities.

---

# 5. HTTP Requests & Responses

## Request Structure

```text
Request Line
Headers
[Optional Body]
```

### Request Line

```text
METHOD /path?query HTTP/version
```

Example:

```http
GET /users/login.html HTTP/1.1
```

| Field   | Example             | Purpose             |
| ------- | ------------------- | ------------------- |
| Method  | `GET`               | Requested operation |
| Path    | `/users/login.html` | Resource            |
| Version | `HTTP/1.1`          | HTTP version        |

Example with query parameter:

```http
GET /users/login.html?username=user HTTP/1.1
```

---

## Request Headers

Headers provide additional information.

Common examples:

```http
Host: target.htb
User-Agent: Mozilla/5.0
Cookie: PHPSESSID=abc123
```

Headers may contain:

* Authentication/session information
* Host information
* Client information
* Application-specific controls

---

## Request Body

Some methods contain a request body.

Example:

```http
POST /login HTTP/1.1
Host: target.htb

username=test&password=test
```

---

# 6. HTTP Response

Response structure:

```text
Status Line
Headers
[Response Body]
```

Example:

```http
HTTP/1.1 200 OK
```

Contains:

```text
HTTP Version + Status Code + Status Message
```

Example:

```http
HTTP/1.1 401 Unauthorized
```

### Response Headers

Examples:

```http
Server: Apache
Content-Type: text/html
Content-Length: 464
Set-Cookie: PHPSESSID=abc123
```

Can reveal:

* Web server/software
* Response type
* Cookies
* Response size
* Application behavior

### Response Body

May contain:

* HTML
* JSON
* JavaScript
* CSS
* Images
* PDF
* Other files

---

# 7. Inspecting Requests

## cURL

```bash
curl -v http://target.htb
```

More verbose:

```bash
curl -vvv http://target.htb
```

Headers + response:

```bash
curl -i http://target.htb
```

---

## Browser DevTools

Open:

```text
F12
```

or:

```text
CTRL + SHIFT + I
```

Go to:

```text
Network → Select Request
```

Inspect:

* HTTP method
* URL/path
* Parameters
* Status code
* Request headers
* Response headers
* Cookies
* Request/response data

### Basic Workflow

```text
Open DevTools
     ↓
Network tab
     ↓
Refresh page
     ↓
Perform action
     ↓
Select interesting request
     ↓
Inspect request + response
```

---

# 8. HTTP Headers

## Header Categories

1. General Headers
2. Entity/Representation Headers
3. Request Headers
4. Response Headers
5. Security Headers

---

## Common Headers

| Header             | Purpose                    |
| ------------------ | -------------------------- |
| `Host`             | Requested hostname         |
| `User-Agent`       | Identifies client          |
| `Referer`          | Indicates request origin   |
| `Accept`           | Accepted response types    |
| `Cookie`           | Sends session/state        |
| `Authorization`    | Authentication information |
| `Content-Type`     | Data type                  |
| `Content-Length`   | Body size                  |
| `Server`           | May reveal server software |
| `Set-Cookie`       | Sets client cookie         |
| `Location`         | Redirect destination       |
| `WWW-Authenticate` | Authentication mechanism   |

### Host

```http
Host: target.htb
```

Useful for virtual-host testing.

### Cookie

```http
Cookie: PHPSESSID=abc123
```

Important during session/authentication testing.

### Authorization

```http
Authorization: Basic dXNlcjpwYXNz
```

Provides authentication information.

---

## Security Headers

### Content-Security-Policy

```http
Content-Security-Policy: script-src 'self'
```

Controls allowed resource/script sources.

### Strict-Transport-Security

```http
Strict-Transport-Security: max-age=31536000
```

Forces browsers to use HTTPS.

### Referrer-Policy

```http
Referrer-Policy: origin
```

Controls information sent through the `Referer` header.

---

## cURL Header Commands

Headers only:

```bash
curl -I https://target.htb
```

Headers + body:

```bash
curl -i https://target.htb
```

Full request/response:

```bash
curl -v https://target.htb
```

Custom User-Agent:

```bash
curl -A "Mozilla/5.0" https://target.htb
```

Custom header:

```bash
curl -H "X-Test: test" https://target.htb
```

### `-I` vs `-i`

```text
-I → Headers only / HEAD request
-i → Headers + response body
```

---

# 9. HTTP Methods

HTTP methods tell the server what operation is being requested.

| Method    | Purpose                 | Pentesting Relevance                     |
| --------- | ----------------------- | ---------------------------------------- |
| `GET`     | Retrieve resource       | Identify input points                    |
| `POST`    | Submit data             | Test submitted data                      |
| `HEAD`    | Headers only            | Inspect resource information             |
| `PUT`     | Create/replace resource | Check unauthorized creation/modification |
| `DELETE`  | Delete resource         | Check authorization                      |
| `OPTIONS` | Supported methods       | Identify available methods               |
| `PATCH`   | Partial modification    | Relevant to APIs                         |

### Quick Commands

```bash
# GET
curl http://target.htb/

# HEAD
curl -I http://target.htb/

# OPTIONS
curl -X OPTIONS -i http://target.htb/

# POST
curl -X POST -d "username=test&password=test" http://target.htb/

# PUT
curl -X PUT -d "data=test" http://target.htb/resource

# DELETE
curl -X DELETE http://target.htb/resource
```

> Only test methods that create, modify, or delete resources in explicitly authorized environments.

---

# 10. HTTP Status Codes

| Class | Meaning              |
| ----- | -------------------- |
| `1xx` | Informational        |
| `2xx` | Success              |
| `3xx` | Redirection          |
| `4xx` | Client/request error |
| `5xx` | Server error         |

## Important Codes

| Code  | Meaning               | Pentesting Relevance       |
| ----- | --------------------- | -------------------------- |
| `200` | OK                    | Successful response        |
| `302` | Found/Redirect        | Login/dashboard redirects  |
| `400` | Bad Request           | Request formatting         |
| `401` | Unauthorized          | Authentication required    |
| `403` | Forbidden             | Access-control testing     |
| `404` | Not Found             | Endpoint enumeration       |
| `500` | Internal Server Error | Application/error behavior |

### Key Concept

```text
HTTP Method → What operation is requested

Status Code → What happened

Response → What the server returned
```

---

# 11. GET Requests

Browsers commonly use `GET` to request resources.

A page may trigger additional requests.

### DevTools Workflow

```text
Open page
   ↓
Network tab
   ↓
Clear requests
   ↓
Perform action
   ↓
Identify new request
   ↓
Inspect URL, method, parameters, headers, response
```

---

# 12. HTTP Basic Authentication

Basic Authentication is handled by the web server to protect a resource.

Example response:

```http
HTTP/1.1 401 Authorization Required
WWW-Authenticate: Basic realm="Access denied"
```

### Identify Basic Auth

A response containing:

```text
401
WWW-Authenticate: Basic
```

indicates that Basic Authentication is being requested.

### cURL

```bash
curl -u admin:admin http://<SERVER_IP>:<PORT>/
```

Credentials can also appear in the URL:

```bash
curl http://admin:admin@<SERVER_IP>:<PORT>/
```

---

## Authorization Header

Basic Auth uses:

```http
Authorization: Basic <base64-value>
```

Example:

```http
Authorization: Basic YWRtaW46YWRtaW4=
```

Base64 is **encoding, not encryption**.

### Manually Set Header

```bash
curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' \
http://<SERVER_IP>:<PORT>/
```

Other authorization schemes include:

```text
Basic <base64-credentials>
Bearer <token>
```

---

# 13. GET Parameters

GET parameters appear in the URL.

Example:

```text
/search.php?search=le
```

Breakdown:

```text
Path       → /search.php
Parameter  → search
Value      → le
```

### Finding Parameters

```text
Browser
   ↓
DevTools → Network
   ↓
Clear requests
   ↓
Perform action
   ↓
Select request
   ↓
Inspect Request URL
```

---

## Reproduce GET Request

```bash
curl 'http://<SERVER_IP>:<PORT>/search.php?search=le' \
-H 'Authorization: Basic YWRtaW46YWRtaW4='
```

### Copy as cURL

```text
Network
→ Right-click request
→ Copy
→ Copy as cURL
```

Useful for reproducing the exact browser request.

Remove unnecessary headers when manually testing, while keeping required authentication/session headers.

### Copy as Fetch

```text
Network
→ Right-click request
→ Copy
→ Copy as Fetch
→ Console
→ Paste & execute
```

---

# 14. POST Requests

`POST` sends data in the request body.

### GET vs POST

```text
GET

/search.php?search=london
        ↓
Parameter in URL


POST

/search.php

Body:
{"search":"london"}
        ↓
Parameter in request body
```

### Form POST

```bash
curl -X POST \
-d 'username=admin&password=admin' \
http://<SERVER_IP>:<PORT>/
```

### Follow Redirects

```bash
curl -L -X POST \
-d 'username=admin&password=admin' \
http://<SERVER_IP>:<PORT>/
```

`-L` follows redirects.

---

# 15. Cookies & Sessions

After successful login, the server may return:

```http
Set-Cookie: PHPSESSID=<session_value>; path=/
```

The browser stores the cookie and sends it with subsequent requests.

### View Cookie

```bash
curl -i -X POST \
-d 'username=admin&password=admin' \
http://<SERVER_IP>:<PORT>/
```

Look for:

```http
Set-Cookie: PHPSESSID=<session_value>
```

### Send Cookie

```bash
curl -b 'PHPSESSID=<session_value>' \
http://<SERVER_IP>:<PORT>/
```

Or:

```bash
curl -H 'Cookie: PHPSESSID=<session_value>' \
http://<SERVER_IP>:<PORT>/
```

### Browser

```text
DevTools
→ Storage
→ Cookies
→ Target website
```

---

# 16. JSON Data

Web applications and APIs may send JSON.

Example:

```json
{
  "search": "london"
}
```

The request should specify:

```http
Content-Type: application/json
```

Example:

```http
POST /search.php HTTP/1.1
Content-Type: application/json
Cookie: PHPSESSID=<session_value>
```

### JSON POST with cURL

```bash
curl -X POST \
-d '{"search":"london"}' \
-b 'PHPSESSID=<session_value>' \
-H 'Content-Type: application/json' \
http://<SERVER_IP>:<PORT>/search.php
```

---

# 17. DevTools → cURL Workflow

For an unknown POST request:

```text
Network
   ↓
Clear requests
   ↓
Perform action
   ↓
Select POST request
   ↓
Inspect Request / Payload / Headers
   ↓
Copy → Copy as cURL
   ↓
Run in terminal
   ↓
Modify parameters
   ↓
Test
```

Identify:

* Endpoint
* HTTP method
* Request body
* `Content-Type`
* Authentication/session cookie
* Response

---

# 18. CRUD APIs

APIs commonly expose entities through URL paths.

Example:

```text
/api.php/city/london
```

```text
city     → entity
london   → specific entity
```

## CRUD

| Operation | Method   | Purpose     |
| --------- | -------- | ----------- |
| Create    | `POST`   | Add data    |
| Read      | `GET`    | Read data   |
| Update    | `PUT`    | Modify data |
| Delete    | `DELETE` | Remove data |

---

## READ — GET

Specific entry:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
```

Search:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/le | jq
```

All entries:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/ | jq
```

Useful:

```text
-s   → Silent mode
| jq → Format JSON
```

---

## CREATE — POST

```bash
curl -X POST \
http://<SERVER_IP>:<PORT>/api.php/city/ \
-d '{"city_name":"HTB_City","country_name":"HTB"}' \
-H 'Content-Type: application/json'
```

Verify:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/HTB_City | jq
```

Pattern:

```text
POST
+
JSON body
+
Content-Type: application/json
```

---

## UPDATE — PUT

```bash
curl -X PUT \
http://<SERVER_IP>:<PORT>/api.php/city/london \
-d '{"city_name":"New_HTB_City","country_name":"HTB"}' \
-H 'Content-Type: application/json'
```

Verify:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq

curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq
```

### PUT vs PATCH

```text
PUT   → Update/replace resource
PATCH → Partially update resource
```

### OPTIONS

```bash
curl -X OPTIONS http://<SERVER_IP>:<PORT>/api.php/city/
```

---

## DELETE

```bash
curl -X DELETE \
http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
```

Verify:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq
```

---

# 19. API Testing Workflow

When discovering an API:

```text
Identify API endpoint
        ↓
Identify entity / identifier
        ↓
Test GET
        ↓
Test search/filter behavior
        ↓
Check supported methods
        ↓
Test POST if permitted
        ↓
Test PUT/PATCH if permitted
        ↓
Test DELETE if permitted
        ↓
Check authentication
        ↓
Check authorization
```

---

# 20. API Security Relevance

During authorized API testing, check whether the current user can:

* Read data they should not access
* Create unauthorized entries
* Modify unauthorized entries
* Delete unauthorized entries

Common authentication mechanisms:

```text
Cookie
Authorization header
JWT
```

### Pentesting Focus

```text
API endpoint
     ↓
HTTP method
     ↓
Entity / identifier
     ↓
Authentication
     ↓
Authorization
     ↓
Allowed CRUD operation
```

---

# 21. HTB Web Testing Workflow

Use this general process when approaching an unfamiliar web target:

```text
Identify Web Service
        ↓
Check HTTP / HTTPS
        ↓
Inspect Response
        ↓
Identify Paths / Endpoints
        ↓
Identify Parameters
        ↓
Inspect Methods
        ↓
Inspect Headers
        ↓
Inspect Cookies / Authentication
        ↓
Reproduce Requests
        ↓
Test Application Behavior
        ↓
Move Interesting Requests to Burp Suite
```

---

# 22. Quick Reference

## cURL

```bash
# Basic request
curl http://target.htb

# Headers + body
curl -i http://target.htb

# Verbose
curl -v http://target.htb

# Headers only
curl -I http://target.htb

# HTTPS
curl https://target.htb

# Ignore invalid certificate
curl -k https://target.htb

# Basic authentication
curl -u user:password http://target.htb

# Custom User-Agent
curl -A "Mozilla/5.0" http://target.htb

# Custom header
curl -H "X-Test: test" http://target.htb

# POST form data
curl -X POST -d "username=test&password=test" http://target.htb/login

# Follow redirects
curl -L http://target.htb

# Send cookie
curl -b 'PHPSESSID=<value>' http://target.htb

# JSON POST
curl -X POST \
-H 'Content-Type: application/json' \
-d '{"search":"test"}' \
http://target.htb/search.php

# OPTIONS
curl -X OPTIONS -i http://target.htb
```

## Browser

```text
F12
CTRL + SHIFT + I

Network
→ Select request
→ Headers
→ Payload
→ Response
→ Cookies
```

## Request Analysis

```text
Method
Path
Parameters
Headers
Cookies
Body
Status Code
Response
```

---

# Key Takeaways

```text
URL
 ↓
Request
 ↓
Method + Path + Parameters
 ↓
Headers + Cookies + Body
 ↓
Server
 ↓
Status Code + Response
 ↓
Understand application behavior
 ↓
Identify interesting attack surface
```

For practical web testing, focus on understanding **what request the browser sends, why it sends it, what the server does with it, and how the response changes when inputs are modified**.
