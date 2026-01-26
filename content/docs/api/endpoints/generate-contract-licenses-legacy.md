---
title: Generate Contract Licenses (Legacy)
weight: 10
---

# Generate Contract Licenses (Legacy)

## Description

Legacy endpoint for generating contract licenses. Kept for backward compatibility.

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/contracts/generate`
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
  "contract_uuid": "{{contract_uuid}}",
  "quantity": 1
}
```

## Response Examples

⚠️ **No response examples** are documented in the Postman collection for this endpoint.
