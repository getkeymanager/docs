---
title: Create Product Meta
weight: 10
---

# Create Product Meta

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/create-product-meta`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `product_id` | text | Yes | Required; Product ID | `1` |
| `key` | text | Yes | Required; Meta key | `test-key` |
| `value` | text | Yes | Required; Meta value | `test value` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Product not found

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 274,
    "message": "Product not found",
    "timestamp": 1709169490
  },
  "response_base64": "eyJjb2RlIjoyNzQsIm1lc3NhZ2UiOiJQcm9kdWN0IG5vdCBmb3VuZCIsInRpbWVzdGFtcCI6MTcwOTE2OTQ5MH0=",
  "private_key_used": "global",
  "signature": "ijixEhCvzI3s8qsV5206bHb6mBZ1tlbgQ5WTMeUtgQk6Vs99rLUUXR6QjseTiV/nWQrWO6Zd/FFsSu2w3l/Vz38uvfXKKcp3i1DN03HGTOmv5KPJS36PT8LTAFh4GbauCmEeRYUchM7Uh0TOnv/pY+q1Zk5u06vTGjyMvsh1dQ80/qT96T2J7+OTXVUZ+fSyh0D9IwXez8FEOu8iqbjDLKYLaHGB40gcgMXwoy5D7uUNdtNLOe2kZVMXz615+YwDvFlH8sxfw26qSuIXOhn5mtKHZTRGfoAE/uFtQ3skIRN14erslmZ8Drfehg4Ycf+4SMBSGbUWv9jCwM/oxBa/tA=="
}
```

#### Product meta created

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 273,
    "message": "Product meta created",
    "timestamp": 1709169515
  },
  "response_base64": "eyJjb2RlIjoyNzMsIm1lc3NhZ2UiOiJQcm9kdWN0IG1ldGEgY3JlYXRlZCIsInRpbWVzdGFtcCI6MTcwOTE2OTUxNX0=",
  "private_key_used": "product",
  "signature": "KaPY4rCN8vhBK3DCrNhnUTF2O0VkN8grnwPI3nyPwSznexfbLBLPDHt3CUV3FFS7XcdUQ1bXxHgepJoeQPhh6cfsi4jn/23uYicJR3xwmxSInEo1Y8COgDksk/wLJ7XQnmccPpQjOGFwxcnUP7YN3Lu08xit9/hvelf2oEBCsSICpYJKPuyO45J/IUwVNIziYzZi0+A8Q5LSL4q5BlQ4WHHx5m6gtkIq9rbp/nx1cfnNwvsXIqzWqf10ahUe+glV0cBe9Fhy5pxLphk4yO1DmceLXhkPA/68egP1pype8UOBvLntrvk6ZiHsSobt2RD3/wAedvRvhFc1Cb05WGog/g=="
}
```
