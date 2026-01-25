---
title: "Access Restrictions Endpoint"
description: "API documentation for access restriction errors and responses."
---

# Access Restrictions

Describes error responses for blocked IPs, identifiers, or other access restrictions.

## Request Example
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

### 403 Forbidden
- **Blocked IP or identifier - Access denied**
  - Code: 150
  - Message: "Access denied"

#### Example Error Response
```json
{
  "response": {
    "code": 150,
    "message": "Access denied",
    "timestamp": 1709381942
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See Verify endpoint for more details.