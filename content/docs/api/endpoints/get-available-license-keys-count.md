---
title: Get Available License Keys Count
weight: 10
---

## Endpoint Details

- **Method:** `GET`
- **Path:** `/api/v1/get-available-license-keys-count`
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

#### Available license keys count

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 741,
    "message": "Available license keys count",
    "count": 696,
    "timestamp": 1710446966
  },
  "response_base64": "eyJjb2RlIjo3NDEsIm1lc3NhZ2UiOiJBdmFpbGFibGUgbGljZW5zZSBrZXlzIGNvdW50IiwiY291bnQiOjY5NiwidGltZXN0YW1wIjoxNzEwNDQ2OTY2fQ==",
  "private_key_used": "global",
  "signature": "eYfU5zWZa/ZKGqPr2RV7wiMyVeGOrIHQhhCrszUVk0kdpElLee27ngQnIEMQ+p6p4NNW+PxMcVYuM0tx9c760UyTmzgfCxXaiiyrwIMCWlIqemE0z/WWxF6qERS2x07u6XAvdEPKFFa4nxMSDR9dAG544s3sigvLXB0rD/pA4IX/QXiuf3ZjJGdOV7M8t1zrNfVwnq+cFn6QKIry4GZBS0OvGkfySF/l96x1I8pR9t5p76XpVGhX7v5A0K3va+r5Cu8qpMFkZqwVtMlNtsmYMlGUcuZ1XEhWB/nLvwPTWlTI9qL8VU/aBzRz1NJwzoTGBNu83OHSZXvpOpfYpIF7qA=="
}
```
