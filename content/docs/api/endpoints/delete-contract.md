---
title: Delete Contract
weight: 10
---

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/delete-contract`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | N/A | `bd494175-4582-43dd-9c32-c58f45e2ec91` |
| `contract_id` | text | Yes | N/A | `9` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Contract not found

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 844,
    "message": "Contract not found",
    "timestamp": 1731207335
  },
  "response_base64": "eyJjb2RlIjo4NDQsIm1lc3NhZ2UiOiJDb250cmFjdCBub3QgZm91bmQiLCJ0aW1lc3RhbXAiOjE3MzEyMDczMzV9",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```

#### Contract deleted

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 843,
    "message": "contract deleted",
    "timestamp": 1731207382
  },
  "response_base64": "eyJjb2RlIjo4NDMsIm1lc3NhZ2UiOiJjb250cmFjdCBkZWxldGVkIiwidGltZXN0YW1wIjoxNzMxMjA3MzgyfQ==",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```
