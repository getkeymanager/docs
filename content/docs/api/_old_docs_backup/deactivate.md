---
title: "Deactivate License Key Endpoint"
description: "API documentation for /api/v1/deactivate endpoint."
---

# POST /api/v1/deactivate

Deactivates a license key for a specific identifier.

## Request
- **Method:** POST
- **URL:** `/api/v1/deactivate`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name        | Type   | Required | Description                   |
|-------------|--------|----------|-------------------------------|
| api_key     | string | Yes      | API Key                       |
| license_key | string | Yes      | License key                   |
| identifier  | string | Yes      | Identifier (domain, device)   |

## Responses

### 200 OK
- **License key deactivated**
  - Code: 400
  - Message: "License key deactivated"

- **License key already inactive**
  - Code: 401
  - Message: "License key already inactive"

#### Example Success Response
```json
{
  "response": {
    "code": 400,
    "message": "License key deactivated",
    "timestamp": 1709000040
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

#### Example Already Inactive Response
```json
{
  "response": {
    "code": 401,
    "message": "License key already inactive",
    "timestamp": 1709000060
  },
  "response_base64": "...",
  "private_key_used": "product",
  "signature": "..."
}
```

---

See Activate License Key for related actions.
