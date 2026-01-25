---
title: "Activate License Key Endpoint"
description: "API documentation for /api/v1/activate endpoint."
---

# POST /api/v1/activate

Activates a license key for a specific identifier (e.g., domain, device).

## Request
- **Method:** POST
- **URL:** `/api/v1/activate`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name         | Type   | Required | Description                                      |
|--------------|--------|----------|--------------------------------------------------|
| api_key      | string | Yes      | API Key                                          |
| license_key  | string | Yes      | License key                                      |
| identifier   | string | Yes      | Identifier (domain, device, etc.)                |
| post_url     | string | Optional | Deactivation Post URL (for callbacks, if needed) |

## Responses

### 200 OK
- **License key activated**
  - Code: 300
  - Message: "License key activated"
- **License key already active**
  - Code: 301
  - Message: "License key already active"

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

See Deactivate endpoint for deactivation process.