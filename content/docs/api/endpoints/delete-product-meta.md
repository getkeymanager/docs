---
title: Delete Product Meta
weight: 10
---

# Delete Product Meta

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/delete-product-meta`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `product_id` | text | Yes | Required; Product ID | `4` |
| `key` | text | Yes | Required; Meta key | `test-key` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### Product meta deleted

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 482,
    "message": "Product meta deleted",
    "timestamp": 1709169577
  },
  "response_base64": "eyJjb2RlIjo0ODIsIm1lc3NhZ2UiOiJQcm9kdWN0IG1ldGEgZGVsZXRlZCIsInRpbWVzdGFtcCI6MTcwOTE2OTU3N30=",
  "private_key_used": "product",
  "signature": "NTOWJ0iY+q+q6c6GwQOHWzkS8EX9z7PLexgunQlj7/t0An5h9Z4I4j2eyafKuinlHJWZUONX2GUqu8zdIsMq5F3JJKT12ymEJpqXypNvP5BNG0hwuclItalKNNbrwGjrXcH7hsuJ5+W6gLCvb2Im13Oqa9tH8HihEgAM1H17CGCxHHnMYeNNsydlCkHKVy3MRAFK0UgI3jhJyTGlV6iKqIAZB6JVJvt88Y077gOwl3DmVPyM5w/cUk0vO3MCSf9GfSnZ841cn67/BMHmPtkaUqlIAoINgGSdZiAT1SB7WGRfVXovyp6/pjSq0zJ16MZKIKzzREsjFv029CMwW/9xuA=="
}
```
