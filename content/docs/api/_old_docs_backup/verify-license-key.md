---
title: "Verify License Key Endpoint"
description: "API documentation for verifying a license key."
---

# POST /api/v1/verify (License Key)

Verifies a license key for validity and assignment.

## Request
- **Method:** POST
- **URL:** `/api/v1/verify`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name         | Type   | Required | Description                                      |
|--------------|--------|----------|--------------------------------------------------|
| api_key      | string | Yes      | API Key                                          |
| license_key  | string | Yes      | License key                                      |
| identifier   | string | Yes      | Identifier (domain, device, etc.)                |
| email        | string | Optional | Owner email (Envato purchase code verification)  |

## Responses

### 200 OK
- **Invalid license key**
  - Code: 210
  - Message: "Invalid license key"
- **License key not assigned**
  - Code: 201
  - Message: "This license key is not assigned"

#### Example Error Response
```json
{
  "response": {
    "code": 210,
    "message": "Invalid license key",
    "timestamp": 1708999231
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See Activate endpoint for activation process.