---
title: "Assign License Key Endpoint"
description: "API documentation for /api/v1/assign-license-key endpoint."
---

# POST /api/v1/assign-license-key

Assigns a license key to an owner (user/email).

## Request
- **Method:** POST
- **URL:** `/api/v1/assign-license-key`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name         | Type   | Required | Description                                      |
|--------------|--------|----------|--------------------------------------------------|
| api_key      | string | Yes      | API Key                                          |
| license_key  | string | Yes      | License key                                      |
| owner_name   | string | Optional | Owner Name                                       |
| email        | string | Optional | Owner email                                      |

## Responses

### 200 OK
- **License key assigned**
  - Code: 800
  - Message: "License key assigned"
- **Invalid or already assigned license key**
  - Code: 801
  - Message: "Invalid or already assigned license key"

#### Example Success Response
```json
{
  "response": {
    "code": 800,
    "message": "License key assigned",
    "timestamp": 1708999933
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See Activate endpoint for activation process.