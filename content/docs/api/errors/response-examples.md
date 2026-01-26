---
title: Response Examples
weight: 10
---

# Response Examples

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
| `api_key` | text | Yes | API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |

## Response Examples

This endpoint has **4** documented response example(s) in the Postman collection.

#### Invalid API Key

**HTTP Status:** `401 Unauthorized`

**Response Body:**
```json
{
  "response": {
    "code": 100,
    "message": "Invalid API Key",
    "timestamp": 1709381806
  },
  "response_base64": "eyJjb2RlIjoxMDAsIm1lc3NhZ2UiOiJJbnZhbGlkIEFQSSBLZXkiLCJ0aW1lc3RhbXAiOjE3MDkzODE4MDZ9",
  "private_key_used": "global",
  "signature": "ZLt1XJYlkh+oIlO220aBWgxPYw78b/YFRqv2+cIoPYUoUpK7qkzC3/ZjjdXquQrb1O0jnr1SSGwNUP6i+Yzgx43ss9aN113ULesDw0FU/5s5n9dceeAVDzXim1CCU9K+4ePrd4Fv+GJOcGl2W5BpsO9oZoZ/2O3HtR5y/IiDE56u/MFtoEnjSJq3QqvbBBjzq3iXjO175ZOwC1BHpykbyqwEL7Mn+Lu81r0uFCpKu4EZ9qcVHFrJV66s3PIb2N7FX+vdJNMH0+mB8wbRMlp5xE3s/J3YkO9IcK5oM/SNQfwD0a4GaB6zDMrl6gV4BqaBGnNN7KqGhCk4BYx3uBByXw=="
}
```

#### Accessed From The Wrong IP

**HTTP Status:** `401 Unauthorized`

**Response Body:**
```json
{
  "response": {
    "code": 103,
    "message": "API key can't be used from this IP address",
    "timestamp": 1709381904
  },
  "response_base64": "eyJjb2RlIjoxMDMsIm1lc3NhZ2UiOiJBUEkga2V5IGNhbid0IGJlIHVzZWQgZnJvbSB0aGlzIElQIGFkZHJlc3MiLCJ0aW1lc3RhbXAiOjE3MDkzODE5MDR9",
  "private_key_used": "global",
  "signature": "OYLw8wda4Wx5ki/D75Ng7t9ErM2eXCyHDdo9x+MT4dXzkm9ViibzjxszYELu/7sN8U/EvjE+wdUh+Tn3Tsk8tpVEq91WrQsOQyjsA5Jztq7FMEzJbks0kLPERtTGz6Tud7fR6Rx3S+RPczL/ulQ6+4rZ8Yd8jSVWYwwKDqtMhCYZalh2xLm5kB4VANTdXYyP/kzJV97plo6X4iiS7EeUA8mQzw6wP6w+0aMum21BQEp8/zXRvENkteBUr57S+bZCIFgqPdFTLy95TLPoafP/ooBVwoikBIKPNpApT5WAE01v4e3Jw9TfUPAG/Zq5UNmNnqUpV+NXc+otE5kvELwa3g=="
}
```

#### Inactive API Key

**HTTP Status:** `401 Unauthorized`

**Response Body:**
```json
{
  "response": {
    "code": 101,
    "message": "Inactive API Key",
    "timestamp": 1709381876
  },
  "response_base64": "eyJjb2RlIjoxMDEsIm1lc3NhZ2UiOiJJbmFjdGl2ZSBBUEkgS2V5IiwidGltZXN0YW1wIjoxNzA5MzgxODc2fQ==",
  "private_key_used": "global",
  "signature": "eVCp5nfzpZ6vLXZoIdfFq3DBUxTP+BJpAn10RIb2ZsnOlwLn47z3TP49F2DkvbP+Vri4STgCHfLesBuIgjAm4m4WLjhFgXGUviBd7Zc0t+p1zNr9R36kKvDvrYXij40no2FY/ptDaoMN8R2WCamvhDx/OFPWuA5i5kQnOFpTMamlQRP9+xsZWc/u7Xk3Y0advRu5WkMQhK4tsQn5T/nMpG8ZtIk5WczkXMk1sJ/wRE7OQSH/I/4L4+Z33RUlZtXpgbX+DXYNIAPlHTpbyTbhuiZ0HwX66zKhsH3fqKSkfNtnOxufh8+vXLNgzCRkTetYVSm69MX8hAcbpow+ol14Qg=="
}
```

#### Permission  Required

**HTTP Status:** `401 Unauthorized`

**Response Body:**
```json
{
  "response": {
    "code": 102,
    "message": "The used API key doesn't have the required capability to access this endpoint",
    "timestamp": 1709381852
  },
  "response_base64": "eyJjb2RlIjoxMDIsIm1lc3NhZ2UiOiJUaGUgdXNlZCBBUEkga2V5IGRvZXNuJ3QgaGF2ZSB0aGUgcmVxdWlyZWQgY2FwYWJpbGl0eSB0byBhY2Nlc3MgdGhpcyBlbmRwb2ludCIsInRpbWVzdGFtcCI6MTcwOTM4MTg1Mn0=",
  "private_key_used": "global",
  "signature": "ntfHf95Ba72VTazQqgH3pTSSOT7BTPXnAdo/cQDlNLGAooaaJrqIcb8iDBD6Wn9pdbDahlS/TAINtzr/kjRovrI8fQxw6eG5vgSc5pGMQ1luwlkVkxmQG6+MLHg6GYow14d957Zz9+Dq5kwL5ljjkyVqx8yVbA1OwvCApO+rqZENZwyKpPPnylP9xNgXiJZAG60ncIbjax7gZO8G8MywFRQOUqbFAvwzkRzQ+fAmLm4Z4QUVizqmR9ebkOV7vEOeaGMnzgovEHPjf51X9iFMtVfR/b1IkTRJ6yKW8ZVRZ5y5oUjbcUDV5Cl8vMjqIoGe5U3A+dpiCgNJBqacHlJV+g=="
}
```
