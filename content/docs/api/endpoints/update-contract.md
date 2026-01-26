---
title: Update Contract
weight: 10
---

# Update Contract

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/update-contract`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | N/A | `bd494175-4582-43dd-9c32-c58f45e2ec91` |
| `contract_id` | text | Yes | N/A | `8` |
| `contract_key` | text | Yes | N/A | `d375f538-9c96-11ef-b499-c87f5451677f-123456789` |
| `contract_name` | text | Yes | N/A | `Test Contract` |
| `contract_information` | text | Yes | N/A | `Test information` |
| `product_id` | text | Yes | N/A | `1` |
| `license_keys_quantity` | text | Yes | N/A | `65` |
| `status` | text | Yes | N/A | `active` |
| `can_get_info` | text | Yes | N/A | `1` |
| `can_generate` | text | Yes | N/A | `1` |
| `can_destroy` | text | Yes | N/A | `1` |
| `can_destroy_all` | text | Yes | N/A | `1` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Incorrect data found

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 825,
    "message": "Incorrect data found",
    "errors": {
      "contract_key": "Contract key is required and must be unique.",
      "contract_name": "Contract name is required.",
      "contract_information": "Contract information is required.",
      "product_id": "Product Id must be a valid product Id.",
      "license_keys_quantity": "License keys quantity must be 1 or more.",
      "status": "Status must be active or inactive",
      "can_get_info": "Can get info must be 1 for true or 0 for false",
      "can_generate": "Can generate must be 1 for true or 0 for false",
      "can_destroy": "Can destroy must be 1 for true or 0 for false",
      "can_destroy_all": "Can destroy all must be 1 for true or 0 for false"
    },
    "timestamp": 1731204923
  },
  "response_base64": "eyJjb2RlIjo4MjUsIm1lc3NhZ2UiOiJJbmNvcnJlY3QgZGF0YSBmb3VuZCIsImVycm9ycyI6eyJjb250cmFjdF9rZXkiOiJDb250cmFjdCBrZXkgaXMgcmVxdWlyZWQgYW5kIG11c3QgYmUgdW5pcXVlLiIsImNvbnRyYWN0X25hbWUiOiJDb250cmFjdCBuYW1lIGlzIHJlcXVpcmVkLiIsImNvbnRyYWN0X2luZm9ybWF0aW9uIjoiQ29udHJhY3QgaW5mb3JtYXRpb24gaXMgcmVxdWlyZWQuIiwicHJvZHVjdF9pZCI6IlByb2R1Y3QgSWQgbXVzdCBiZSBhIHZhbGlkIHByb2R1Y3QgSWQuIiwibGljZW5zZV9rZXlzX3F1YW50aXR5IjoiTGljZW5zZSBrZXlzIHF1YW50aXR5IG11c3QgYmUgMSBvciBtb3JlLiIsInN0YXR1cyI6IlN0YXR1cyBtdXN0IGJlIGFjdGl2ZSBvciBpbmFjdGl2ZSIsImNhbl9nZXRfaW5mbyI6IkNhbiBnZXQgaW5mbyBtdXN0IGJlIDEgZm9yIHRydWUgb3IgMCBmb3IgZmFsc2UiLCJjYW5fZ2VuZXJhdGUiOiJDYW4gZ2VuZXJhdGUgbXVzdCBiZSAxIGZvciB0cnVlIG9yIDAgZm9yIGZhbHNlIiwiY2FuX2Rlc3Ryb3kiOiJDYW4gZGVzdHJveSBtdXN0IGJlIDEgZm9yIHRydWUgb3IgMCBmb3IgZmFsc2UiLCJjYW5fZGVzdHJveV9hbGwiOiJDYW4gZGVzdHJveSBhbGwgbXVzdCBiZSAxIGZvciB0cnVlIG9yIDAgZm9yIGZhbHNlIn0sInRpbWVzdGFtcCI6MTczMTIwNDkyM30=",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```

#### Contract updated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 842,
    "message": "contract updated",
    "contract": {
      "id": 8,
      "name": "Test Contract",
      "information": "Test information",
      "contract_key": "d375f538-9c96-11ef-b499-c87f5451677f-123456789",
      "license_keys_quantity": "65",
      "product_id": "1",
      "can_get_info": "1",
      "can_generate": "1",
      "can_destroy": "1",
      "can_destroy_all": "1",
      "status": "active",
      "created_at": "2024-11-10T00:08:51.000000Z",
      "updated_at": "2024-11-10T02:46:58.000000Z",
      "license_keys_count": 0
    },
    "timestamp": 1731206818
  },
  "response_base64": "eyJjb2RlIjo4NDEsIm1lc3NhZ2UiOiJjb250cmFjdCBjcmVhdGVkIiwiY29udHJhY3QiOnsiaWQiOjgsIm5hbWUiOiJUZXN0IENvbnRyYWN0IiwiaW5mb3JtYXRpb24iOiJUZXN0IGluZm9ybWF0aW9uIiwiY29udHJhY3Rfa2V5IjoiZDM3NWY1MzgtOWM5Ni0xMWVmLWI0OTktYzg3ZjU0NTE2NzdmLTEyMzQ1Njc4OSIsImxpY2Vuc2Vfa2V5c19xdWFudGl0eSI6IjY1IiwicHJvZHVjdF9pZCI6IjEiLCJjYW5fZ2V0X2luZm8iOiIxIiwiY2FuX2dlbmVyYXRlIjoiMSIsImNhbl9kZXN0cm95IjoiMSIsImNhbl9kZXN0cm95X2FsbCI6IjEiLCJzdGF0dXMiOiJhY3RpdmUiLCJjcmVhdGVkX2F0IjoiMjAyNC0xMS0xMFQwMDowODo1MS4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMTBUMDI6NDY6NTguMDAwMDAwWiIsImxpY2Vuc2Vfa2V5c19jb3VudCI6MH0sInRpbWVzdGFtcCI6MTczMTIwNjgxOH0=",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```
