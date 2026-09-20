# HTTP / HTTPS

## HTTP
- Application-layer protocol
- Used for web communication (Request <--> Server)
- Port `80`

## HTTP Request

Contains:
- Method
- URL/path
- Headers
- Body (optional)

Common methods:
- GET
- POST
- PUT
- PATCH
- DELETE

## HTTP Response

Contains:
- Status code
- Headers
- Body

Common status codes:
- 200 → OK
- 301/302 → Redirect
- 400 → Bad Request
- 401 → Unauthorized
- 403 → Forbidden
- 404 → Not Found
- 500 → Server Error


## HTTPS
HTTPS = HTTP + TLS

- Encrypts communication
- Protects confidentiality
- Helps verify server identity
- Port `443`

### TLS
Provides:
- Encryption
- Integrity
- Authentication