---
title: Delete License Key
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/delete-license-key`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `3a343c8a-38fe-4b6e-ad77-0078aaf16xxxxeb3` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### License key deleted

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 850,
    "message": "License key deleted",
    "timestamp": 1709001887
  },
  "response_base64": "eyJjb2RlIjo4NTAsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleSBkZWxldGVkIiwidGltZXN0YW1wIjoxNzA5MDAxODg3fQ==",
  "private_key_used": "product",
  "signature": "RRToJXLDDiAQRvvNIw6+b4K75R3qZ5Ozig8H7QN8jHYlzPveIH8fHQR0MUtBrcsmuLVp9wdRHJA+tqFwDil2gy6W+uc/aCT1SiDybbqkFpyOeCsL+wkzu8EZDLPxfXA+gMM9vEWZZev8Xk0W4smvhS2s9h3752iuh0OPIQC4vGRXsD2pr/OzzREYi8X25Ibk3TfB92H9/amivklIzXhhQNlOm3o4PZNv4mtjuRh+TlF3fuvUJttH1LDnTvFO/pwk0W3pRBCCxbsdOKtIhM1TtRq5lxVIz8An+1wWqT9V7HEZ/kAIHARNkXzKVYeyzlTEcAahikDFZC0OY2HCzOCoEQ=="
}
```
