---
title: Blocked IP or identifier - Access denied
weight: 10
---



## Description

Verify license key

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/verify`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `276fac24-3dd1-429f-b8ff-3b74047e0d56` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |
| `email` | text | Yes | Optional; Owner email; Only saved during Envato purchase code verification, when the purchase code is added to the license manager. | `email@domain.ltd` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### Blocked IP or identifier - Access denied

**HTTP Status:** `403 Forbidden`

**Response Body:**
```json
{
  "response": {
    "code": 150,
    "message": "Access denied",
    "timestamp": 1709381942
  },
  "response_base64": "eyJjb2RlIjoxNTAsIm1lc3NhZ2UiOiJBY2Nlc3MgZGVuaWVkIiwidGltZXN0YW1wIjoxNzA5MzgxOTQyfQ==",
  "private_key_used": "global",
  "signature": "H+aaWtx007Vj3BI+bO7dw1Nz/V3qc8XO79cPVNN7QrX8pAqtZIHdvKAZsSKpsp1Vun1Es8uNWJK9kYc7OhdZG1BlG2wTg7qfZstReVb4GRMUmPyX50Rt60CunO/SrfWtRd6GBGkAnmp2n6BMlPFs6P+Tk5gd50x+LcTKjyEhvKtVZ/GWV05LEnsOottUqd/b4uZLUZ0f4YxBvo11plxhUBJ65kGowJl1J/7qf+e2bKGZ6gv0BXhxtsgXzsyToZb/kPmk1sqoUjVf1uu0dwxPwhcqbAE6Q3UsENeMcd4fGF2zugsiW7orPz7Sfk7Xw7pfCpg6H5cOjYUh1ZYO8dx4Fg=="
}
```
