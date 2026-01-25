---
title: "Verify Endpoint"
description: "API documentation for /api/v1/verify endpoint."
---

# POST /api/v1/verify

Verifies a license key and API key, returning status and error details.

## Request
- **Method:** POST
- **URL:** `/api/v1/verify`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name           | Type   | Required | Description                                                                 |
|----------------|--------|----------|-----------------------------------------------------------------------------|
| api_key        | string | Yes      | API Key                                                                    |
| license_key    | string | Sometimes| License key (required for license verification)                            |
| identifier     | string | Sometimes| Identifier (required for some checks)                                      |
| email          | string | Optional | Owner email (used in Envato purchase code verification)                    |

## Responses

### 401 Unauthorized
- **Invalid API Key**
  - Code: 100
  - Message: "Invalid API Key"
- **Inactive API Key**
  - Code: 101
  - Message: "Inactive API Key"
- **Permission Required**
  - Code: 102
  - Message: "The used API key doesn't have the required capability to access this endpoint"
- **Wrong IP**
  - Code: 103
  - Message: "API key can't be used from this IP address"

### 403 Forbidden
- **Blocked IP or identifier - Access denied**
  - Code: 150
  - Message: "Access denied"

#### Example Error Response
```json
{
  "response": {
    "code": 100,
    "message": "Invalid API Key",
    "timestamp": 1709381806
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See other endpoint docs for more details.