---
title: Assign And Activate License Key
weight: 10
---

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/assign-and-activate-license-key`
- **Authentication:** API Key (required)

## Request Headers

| Header | Value | Description |
|--------|-------|-------------|
| `Accept` | `application/json` | N/A |

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `19d4c2a0-b2ee-47a9-9fa7-f8befcc142fd` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |
| `post_url` | text | Yes | Optional; Remove deactivation Post URL. | `https://domain.ltd/receiver.php?example-getKeyManager-post-url=test` |
| `owner_email` | text | Yes | Required; Owner email | `email@domain.ltd` |
| `owner_name` | text | Yes | Required; Owner name | `Test User` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### License key activated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 300,
    "message": "License key activated",
    "timestamp": 1708999987
  },
  "response_base64": "eyJjb2RlIjozMDAsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleSBhY3RpdmF0ZWQiLCJ0aW1lc3RhbXAiOjE3MDg5OTk5ODd9",
  "private_key_used": "product",
  "signature": "VKofkoqjrqOQQTxwkfqGY4xmvZZE2cxMIfrc3elOjN0C1zieN2655Vx8CMGQkn8v+M1lP+P+eAz2lump1a9wA8MHbXIlWGuLVrCMkQgpMRb1zkeGbVG1K9F4s1IZ0OWHBIyBaWNel93acabIckMggXoImbZH76uC+WSEfZSsGpZ4Moe5LHukYmzob1WGfw2PFaCtM4UGedmTygf8dv8YKcvSRV2oW/TH/M89I7QVkIxKd8g6pO9mWoA1di86k80rAC70jpZTHD0PhI76sAC+RtIxMsDggIer2GmBm9PosjqlEXbPOaVFyO/dizywYUA/3j7zcGV+bE7rzDBZ+X4yTQ=="
}
```
