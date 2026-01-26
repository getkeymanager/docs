---
title: Assign License Key
weight: 10
---

# Assign License Key

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/assign-license-key`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `bb7ffb6f-2d8e-4977-b2fa-8d43ea58aa0d` |
| `owner_name` | text | Yes | Optional; Owner Name | `Test User` |
| `email` | text | Yes | Optional; Owner email | `email@domain.ltd` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Invalid or already assigned license key

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 801,
    "message": "Invalid or already assigned license key",
    "timestamp": 1708999873
  },
  "response_base64": "eyJjb2RlIjo4MDEsIm1lc3NhZ2UiOiJJbnZhbGlkIG9yIGFscmVhZHkgYXNzaWduZWQgbGljZW5zZSBrZXkiLCJ0aW1lc3RhbXAiOjE3MDg5OTk4NzN9",
  "private_key_used": "global",
  "signature": "XosNwfSXTgkJlG5IK+GaTt7bQea0qJC1/J+cZ9+/XioLwbYPlLYCGV+y6YvcMebZfH2Nz3pRfiuobnfQ2rBfGRugbCsOFs8rnUr/IW43PYqzPkeLZSfFTZCWIxYPUy2he8Y8PfisHhMG2g+SRXE/YrgcBwX8P8+iv1KYaUrULWXSzspzdSxEKYGOaDCe5KQx1W2WOctbpIBLKHKK7QPQQd7dZBABxrPrKJHMgnTy4rO9SFM0rbznLn+kCLBHgqi5GyVxcS2VNuBW6XIFQZzBF9qFjIYZ4Tgq1s0lBR6M/VHRzQ+dOmIqQ+7GzQLhi0doplIDFWX4OKmlY4fwPirEvw=="
}
```

#### License key assigned

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 800,
    "message": "License key assigned",
    "timestamp": 1708999933
  },
  "response_base64": "eyJjb2RlIjo4MDAsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleSBhc3NpZ25lZCIsInRpbWVzdGFtcCI6MTcwODk5OTkzM30=",
  "private_key_used": "global",
  "signature": "Q5aCPpbdb2luJrTHw5cgc3QMIFI/Chx+YKQpE8LqppOBLLtrztsq5Of3x+iF9HlusBxvyq/HmSNotfR4a+90ororZuHeMV6lGnzn12/yMXhMdKTIZ9SHE1TTzMOKBEITiTMHNZsD3vSTv4bNGIQe44jq853o0V1G/m6j4V/4rX+ImDFI8/Wmx6Q6kbr53PC8jFsDxQthWCn1bYQR42gVtydXGpoLLoUJQnhhVOfW7FIV7z08dMWfkoyqyjH8f3kfEClIGI3GuN9MNmfkMRqj3usAtjiaJj1BOEFHFdeltJY6oKTFpnDzqy6MfGgCi0OePbOu9UKwhS+/1kD3B5ADBg=="
}
```
