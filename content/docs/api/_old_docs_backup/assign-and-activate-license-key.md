---
title: "Assign and Activate License Key Endpoint"
description: "API documentation for /api/v1/assign-and-activate-license-key endpoint."
---

# POST /api/v1/assign-and-activate-license-key

Assigns and activates a license key for an owner and identifier.

## Request
- **Method:** POST
- **URL:** `/api/v1/assign-and-activate-license-key`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name         | Type   | Required | Description                                      |
|--------------|--------|----------|--------------------------------------------------|
| api_key      | string | Yes      | API Key                                          |
| license_key  | string | Yes      | License key                                      |
| identifier   | string | Yes      | Identifier (domain, device, etc.)                |
| post_url     | string | Optional | Deactivation Post URL (for callbacks, if needed) |
| owner_email  | string | Yes      | Owner email                                      |
| owner_name   | string | Yes      | Owner name                                       |

## Responses

### 200 OK
- **License key activated**
  - Code: 300
  - Message: "License key activated"

#### Example Success Response
```json
{
  "response": {
    "code": 300,
    "message": "License key activated",
    "timestamp": 1708999677
  },
  "response_base64": "...",
  "private_key_used": "product",
  "signature": "..."
}
```

---

See Assign License Key and Activate endpoints for related actions.