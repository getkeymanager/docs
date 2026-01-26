---
title: Destroy Contract License (Legacy)
weight: 10
---

# Destroy Contract License (Legacy)

## Description

Legacy endpoint for destroying a single contract license. Kept for backward compatibility.

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/contracts/destroy`
- **Authentication:** API Key (required)

## Request Headers

| Header | Value | Description |
|--------|-------|-------------|
| `Authorization` | `Bearer {{api_key}}` | N/A |
| `Idempotency-Key` | `{{$guid}}` | N/A |
| `Content-Type` | `application/json` | N/A |

## Request Parameters

```json
{
  "license_key": "XXXX-XXXX-XXXX"
}
```

## Response Examples

⚠️ **No response examples** are documented in the Postman collection for this endpoint.
