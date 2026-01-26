---
title: Update License Key Meta
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/update-license-key-meta`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `3a343c8a-38fe-4b6e-ad77-2222222` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |
| `key` | text | Yes | Required; Meta key | `test` |
| `value` | text | Yes | Required; Meta value | `test value` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Metadata updated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 353,
    "message": "Metadata updated",
    "meta_id": 1,
    "timestamp": 1709003499
  },
  "response_base64": "eyJjb2RlIjozNTMsIm1lc3NhZ2UiOiJNZXRhZGF0YSB1cGRhdGVkIiwibWV0YV9pZCI6MSwidGltZXN0YW1wIjoxNzA5MDAzNDk5fQ==",
  "private_key_used": "product",
  "signature": "qEjrQI+vaomtqaRv28Jm2+4l61zKbpb/UNb0PnJwJuB0Uzb+lVh3AeTAfoUAABz3AfFQ6o/fO7ot+Y9F33ywPbYIYZLvPiPurccoUFVWP7RV5Owzxmr1BpHliRDl5qhaMQ6fVt6C80ShCDcUgQi8v0vGCYZT5T6d5UOHsU9BM3SvHaWhi3xRWsCwMg91VlqxNGBf6WdOu5FlSnzHEqR+zzQnZ8jRVi6YeAZOGTQ2E/s3SWLQsHJjQ0Dgid7XJtiio+XNehz51bJW7DjxmIAA7WFgg+8TRmBSotBH0Go9Kip4F4vqFu+iB+zECpsF0U29EUGdKtVPMmtRuhjLJI2bdw=="
}
```

#### Meta key doesn't exist

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 352,
    "message": "Meta key doesn't exist",
    "timestamp": 1709003526
  },
  "response_base64": "eyJjb2RlIjozNTIsIm1lc3NhZ2UiOiJNZXRhIGtleSBkb2Vzbid0IGV4aXN0IiwidGltZXN0YW1wIjoxNzA5MDAzNTI2fQ==",
  "private_key_used": "product",
  "signature": "EKzwQc/aHyZ1azHutRXoE4tKXaimEFKrDknEirXaQAGZNUh/VzIeV7/hLULUVyBtOEdVhhirsyvH0IAPblscFG6++px75KmyTDda/b1bxUgmUrm/OIrmrT2nwh85aCQ4I8vRtIykCigXf1f9WhMpN+PlkLCttPN51erXlEkrYISzsICN7wd4rkUrHjChhxKBYHsl7LvC4Ua9jv5glTEQ+0oyozig62mW8uWKPyC/HKWcCBR1cEluTJPjBFCepj1Oiunw9aHPKPH18bU8JbSFVznOnCm7vSlI3sojV6w1GMsjaQJ4pfUESUE2WQrFO3Qnlker89whmV1gSs+hA3VtGQ=="
}
```
