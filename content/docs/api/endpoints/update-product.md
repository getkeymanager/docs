---
title: Update Product
weight: 10
---

# Update Product

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/update-product`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `product_id` | text | Yes | Required; Product ID | `5` |
| `source` | text | Yes | Required; Product source, can be 'internal' or 'Envato' | `internal` |
| `name` | text | Yes | Required; Product name | `API Create Product` |
| `description` | text | Yes | Required; Product description | `Test Update` |
| `require_non_expired` | text | Yes | Required; Boolean, can be 1 or 0 | `1` |
| `external_reference` | text | Yes | Optional; External refrence (item ID for Envato products) | `` |
| `status` | text | Yes | Required; Product status, can be 'active' or 'inactive' | `active` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Product Id doesn't exist

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 651,
    "message": "Incorrect data found",
    "errors": {
      "product_id": [
        "The selected product id is invalid."
      ]
    },
    "timestamp": 1709002994
  },
  "response_base64": "eyJjb2RlIjo2NTEsIm1lc3NhZ2UiOiJJbmNvcnJlY3QgZGF0YSBmb3VuZCIsImVycm9ycyI6eyJwcm9kdWN0X2lkIjpbIlRoZSBzZWxlY3RlZCBwcm9kdWN0IGlkIGlzIGludmFsaWQuIl19LCJ0aW1lc3RhbXAiOjE3MDkwMDI5OTR9",
  "private_key_used": "global",
  "signature": "T6yOTueLSUq45yx5i7WeswN9RjAPnUv8199lpOLpiHF1pys2rhaQLxnVRIhHKF4C9RSn2MKZvR7Vht4SH5/ohYnJje5Xlx7RFix7ppgn5SWN6eYD5IhGHmt/7qCivYOjZPKcTVSQB6MY3BYSr+2ZLp/YFG8kmO3yUYCsIJ9qhrjrNzTitZuTiZUE3bC+sqWMyvNA5bfqJv2DwkGzlT8Cen6LxmpgmQ4Udt4BSf2Y4+RS28B45f2uLAoXGo/jPBOTeoFPIVbmT9hXVT9vD6js2uueQ6YssSzQGiYkxaECMi/gtoRo85R/ScfqdKnm8r7Vzy1fgi5v3R9kcNFnSLNxFw=="
}
```

#### Product updated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 650,
    "message": "Product updated",
    "timestamp": 1709003049
  },
  "response_base64": "eyJjb2RlIjo2NTAsIm1lc3NhZ2UiOiJQcm9kdWN0IHVwZGF0ZWQiLCJ0aW1lc3RhbXAiOjE3MDkwMDMwNDl9",
  "private_key_used": "global",
  "signature": "T9B82VNUdO9mSnZZWqqGpeO1axRzliBxbEVtZVN/rO1pCE6rJmxTjwZSEDWhhP2XIO4/LtN9qzimL+SIMUqVvfQZJWx5VytQjwTkmcW2qSkmUqJSScI93Q3ulru51KcbWlmo73msHeFCt9AkqNbQFrJ8lweAhBv1/fpXP4BNLpDVyzyr3I7kbY1kfvY5IOcT6hDrB04cU4wlmkiEVENE7YnAzCq2haXNpn1VRngc89CrLJhMY8cT3vvRZ7Z35s2u8ys0y+qOBScI48kNZUtF8Iy8VO/X1qRkgi7lrP6nPbiVjhfkIX6JsYm8Yd0b608lsKBQ6jIigs+6QJJ266ZTxw=="
}
```
