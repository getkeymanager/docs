---
title: Create License Key Meta
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/create-license-key-meta`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `3a343c8a-38fe-4b6e-ad77-2222222` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |
| `key` | text | Yes | Required; Meta key | `test-key` |
| `value` | text | Yes | Required; Meta value | `test value` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### This license key is not assigned

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 201,
    "message": "This license key is not assigned",
    "timestamp": 1709003106
  },
  "response_base64": "eyJjb2RlIjoyMDEsIm1lc3NhZ2UiOiJUaGlzIGxpY2Vuc2Uga2V5IGlzIG5vdCBhc3NpZ25lZCIsInRpbWVzdGFtcCI6MTcwOTAwMzEwNn0=",
  "private_key_used": "product",
  "signature": "Jegog7vXkmKk93fC6nfQ4djbLp04xN8fqQvpaXs13VW3LlwJnAyYwBr9k935Rg0apHQLs+XFHwqQe/zv6mswC7Ab4FWJH/dFtkKlqgnuexABM3MUHidKnCbqnRKyhXQcFyp/9XEIkeJcIccKuezYcnzXfcYa1f/2LibxmMPIzuwO/L6gyrkF9L5hMlgc7QG64AjAH+jP8Gpa+ogxOYnAWkMwpu4O0LTbGlVh9tZNv8lh0C8+cXZWnIjnWU8i1TKuQ4JYwsMda/50H1IhrRJHOwU8nRMtUkjLTLpMe1+bNr66o7UrypTneBzUjAmiz2ptmJZeg/zLT038Ul9ii39VLQ=="
}
```

#### Metadata created

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 453,
    "message": "Metadata created",
    "meta_id": 1,
    "timestamp": 1709003135
  },
  "response_base64": "eyJjb2RlIjo0NTMsIm1lc3NhZ2UiOiJNZXRhZGF0YSBjcmVhdGVkIiwibWV0YV9pZCI6MSwidGltZXN0YW1wIjoxNzA5MDAzMTM1fQ==",
  "private_key_used": "product",
  "signature": "Xka7Ix9BHnScdGxCXkzMtuTsyiS7C3XLqF6ugdqCNOLJWAGsk7/oACg+AbRLwKBbQ/lz+HGf1aRB2npKyXKP7cnhbm46sv49Z2qSG2YlwnvLC28ZdKAP4idd64Ycgv2lJKJ35+lJoBr6gZ9L6HhIaQ3M+e2AgJEl2S3MYM4QaIaVZceXSdVaKjfY4c49hKkzfpYKryYKGCvui5SgBB5qwDu2kHZXhx29JTEkZJ/VKp16LIOBXosVDAA8pVk4SgOxbnlWHCPjo9HuB4/HSk0oLhklXL+dYsCE/xRP2OMO8LqPTGD2oT28nAAVHqpqRxrbnHke4tsEvY4cxYjPqWiY6A=="
}
```
