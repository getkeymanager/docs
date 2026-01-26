---
title: Delete Product
weight: 10
---

# Delete Product

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/delete-product`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `product_id` | text | Yes | Required; Product ID | `5` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### Product deleted

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 550,
    "message": "Product deleted",
    "timestamp": 1709003069
  },
  "response_base64": "eyJjb2RlIjo1NTAsIm1lc3NhZ2UiOiJQcm9kdWN0IGRlbGV0ZWQiLCJ0aW1lc3RhbXAiOjE3MDkwMDMwNjl9",
  "private_key_used": "global",
  "signature": "dmhFXoEwt655+bVyG77mJ/W+rn7KYBIEfl9oPhhrU5X83zrOBJAt3s/NrKqH+29bocWeE6LHVsEp3RLefEI4Sy5RfxhySCn293ydi78lU4C398ZOp//0jlkkImKJZhy/1LGZw9pGFs3zwspTmzyG+y5a3mMmp46w5YSIatFPCnwVHqIGiR8/qhKpn3NIIbEa7USBTlaVmbzBSDq2TvvtGndyFoFmi9+U3v2Iy9FETO4Qslk7As0WcUbKQiO7d4Ex0CiC/+6EJSY6p4a3hoY47S3WGbj6gIrjefBox/JJ/d6ComSY6rKj+dbm5/sag+END2lujKXH+LKXeYF6wHYxRA=="
}
```
