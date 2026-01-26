---
title: "Random Assign License Keys Endpoint"
description: "API documentation for /api/v1/random-assign-license-keys endpoint."
---

# POST /api/v1/random-assign-license-keys

Generates and assigns multiple license keys to a user or owner in bulk.

## Request
- **Method:** POST
- **URL:** `/api/v1/random-assign-license-keys`
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

### 200 OK
- **License keys assigned**
  - Code: 803
  - Message: "License keys assigned"
  - Returns: Array of assigned license key objects with details (product_id, license_key, activation_limit, validity, status, owner_name, owner_email, assigned_at, etc.)
- **Product not found**
  - Code: 805
  - Message: "Product not found"

#### Example Success Response
```json
{
  "response": {
    "code": 803,
    "message": "License keys assigned",
    "license_keys": [
      {
        "product_id": 1,
        "license_key": "1de7d049-3160-44c2-b260-fc12b2b7e702",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.829115Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 213,
        "meta_data": []
      }
      // ...more license keys
    ],
    "timestamp": 1732388528
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

#### Example Error Response
```json
{
  "response": {
    "code": 805,
    "message": "Product not found",
    "timestamp": 1732388563
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See Assign License Key for single assignment.