---
title: Random Assign License Keys Queued
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/random-assign-license-keys-queued`
- **Authentication:** API Key (required)

## Request Headers

| Header | Value | Description |
|--------|-------|-------------|
| `Accept` | `application/json` | N/A |

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `product_id` | text | Yes | Required; Product ID | `1` |
| `owner_name` | text | Yes | Optional; Owner Name | `Test User` |
| `owner_email` | text | Yes | N/A | `email@domain.ltd` |
| `quantity` | text | Yes | N/A | `7` |
| `generate` | text | Yes | N/A | `1` |
| `webhook_url` | text | Yes | N/A | `https://demo.getKeyManager.com/woocommerce-integration?getKeyManager-webhook=demo-webhook-key` |
| `identifier` | text | Yes | Example: Order ID; Will be added to the data sent to the webhook URL when the queue is processed. | `31` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### Request Queued

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 807,
    "message": "Request Queued",
    "timestamp": 1732487985
  },
  "response_base64": "eyJjb2RlIjo4MDcsIm1lc3NhZ2UiOiJSZXF1ZXN0IFF1ZXVlZCIsInRpbWVzdGFtcCI6MTczMjQ4Nzk4NX0=",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```
