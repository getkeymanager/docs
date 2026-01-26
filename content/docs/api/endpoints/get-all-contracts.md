---
title: Get All Contracts
weight: 10
---

## Endpoint Details

- **Method:** `GET`
- **Path:** `/api/v1/get-all-contracts`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

None

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Product doesn't exist

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 740,
    "message": "Product doesn't exist",
    "timestamp": 1710446875
  },
  "response_base64": "eyJjb2RlIjo3NDAsIm1lc3NhZ2UiOiJQcm9kdWN0IGRvZXNuJ3QgZXhpc3QiLCJ0aW1lc3RhbXAiOjE3MTA0NDY4NzV9",
  "private_key_used": "global",
  "signature": "FN5Cqf4UC/NLGucCI16vFMlb4jRA011o1TYHCZf/NDcJXeK0xfyDeZeJFKWB2/jQ2royyEFpX/HBEpeVYt5re5vBk/F9vGX0g+y9a0zxjwFbJTRcRWxuUm1++map44l7B08lrysfBDZKDlKI0yI3OI3uPJ6/Rj8MR7frnSv/eW/APofKAz5J5czlCWcRDI0pzMXJrJrO2zFTzRDqNN/LEcmKzK0nlr3UgKMj3moT6k/vrJ7LZaLaq3JGZ4SJYMbPNbzX1yqOIeKevKExkYqBdjGyLGOQg+64/1B97YFutdcrLriTwcQYMXvFcHwO2TP4AELOqM4bBKDRLifxdm7HAQ=="
}
```

#### All contracts

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 846,
    "message": "All contracts",
    "contracts": [
      {
        "id": 10,
        "name": "Test Contract",
        "information": "Test information",
        "contract_key": "6dabe9fa-3512-49b4-beb5-7f837b510ec3-1234",
        "license_keys_quantity": 65,
        "product_id": 1,
        "can_get_info": 1,
        "can_generate": 1,
        "can_destroy": 1,
        "can_destroy_all": 1,
        "status": "active",
        "created_at": "2024-11-10T02:13:10.000000Z",
        "updated_at": "2024-11-10T02:13:10.000000Z",
        "license_keys_count": 0
      }
    ],
    "timestamp": 1731207615
  },
  "response_base64": "eyJjb2RlIjo4NDYsIm1lc3NhZ2UiOiJBbGwgY29udHJhY3RzIiwiY29udHJhY3RzIjpbeyJpZCI6MTAsIm5hbWUiOiJUZXN0IENvbnRyYWN0IiwiaW5mb3JtYXRpb24iOiJUZXN0IGluZm9ybWF0aW9uIiwiY29udHJhY3Rfa2V5IjoiNmRhYmU5ZmEtMzUxMi00OWI0LWJlYjUtN2Y4MzdiNTEwZWMzLTEyMzQiLCJsaWNlbnNlX2tleXNfcXVhbnRpdHkiOjY1LCJwcm9kdWN0X2lkIjoxLCJjYW5fZ2V0X2luZm8iOjEsImNhbl9nZW5lcmF0ZSI6MSwiY2FuX2Rlc3Ryb3kiOjEsImNhbl9kZXN0cm95X2FsbCI6MSwic3RhdHVzIjoiYWN0aXZlIiwiY3JlYXRlZF9hdCI6IjIwMjQtMTEtMTBUMDI6MTM6MTAuMDAwMDAwWiIsInVwZGF0ZWRfYXQiOiIyMDI0LTExLTEwVDAyOjEzOjEwLjAwMDAwMFoiLCJsaWNlbnNlX2tleXNfY291bnQiOjB9XSwidGltZXN0YW1wIjoxNzMxMjA3NjE1fQ==",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```
