---
title: "Random Assign License Keys Queued Endpoint"
description: "API documentation for /api/v1/random-assign-license-keys-queued endpoint."
---

# POST /api/v1/random-assign-license-keys-queued

Queues a bulk license key assignment job for asynchronous processing.

## Request
- **Method:** POST
- **URL:** `/api/v1/random-assign-license-keys-queued`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name         | Type   | Required | Description                                      |
|--------------|--------|----------|--------------------------------------------------|
| api_key      | string | Yes      | API Key                                          |
| product_id   | int    | Yes      | Product ID                                       |
| owner_name   | string | Yes      | Owner Name                                       |
| owner_email  | string | Yes      | Owner email                                      |
| quantity     | int    | Yes      | Number of license keys to generate and assign     |
| validity     | int    | Yes      | Validity period (days)                           |
| activation_limit | int | Yes     | Activation limit per license key                 |

## Responses

### 202 Accepted
- **Job Queued**
  - Code: 900
  - Message: "Bulk license key assignment job queued"
  - Returns: Job ID or status reference

#### Example Success Response
```json
{
  "response": {
    "code": 900,
    "message": "Bulk license key assignment job queued",
    "job_id": "bulk-assign-12345",
    "timestamp": 1732388600
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See Random Assign License Keys for synchronous assignment.