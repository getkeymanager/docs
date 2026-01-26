---
title: Get License Key Details
weight: 10
---

# Get License Key Details

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/get-license-key-details`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `19d4c2a0-b2ee-47a9-9fa7-f8befcc142fd` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### No activation found for this license key/identifier combination

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 202,
    "message": "No activation found for this license key/identifier combination",
    "timestamp": 1709000147
  },
  "response_base64": "eyJjb2RlIjoyMDIsIm1lc3NhZ2UiOiJObyBhY3RpdmF0aW9uIGZvdW5kIGZvciB0aGlzIGxpY2Vuc2Uga2V5XC9pZGVudGlmaWVyIGNvbWJpbmF0aW9uIiwidGltZXN0YW1wIjoxNzA5MDAwMTQ3fQ==",
  "private_key_used": "product",
  "signature": "lh009dD7UycTldpwdUQv8FLBofnaP8e+CfxS6i4bdoRXKE3lLZVOVzw91M58iKzZ6nzlYtsF2e4OcYbmtPl2S2CtpBgfG+yn2v6iZXNIbp2HnWZBQUNHpp5AbLx6wLVEueeWzyQ8fMI3mKQaVZo6TxC0WdMYoXaE+c1q7WpqL7VQAQL9aC/EmGyoTSFIe3mo1bhopm6/sSQE4+PVHS5R091qXngruF+h3ZII2CzJ2pwyV7uLdjull/uHaoKxRqIzvV9tvGb3GJ18lVC0/0+ROVeMv3RhDWEO1nu5JUijTT7P2C8sJmH08qznbrxliqg/G856h3a3cMX5agdxIjqcyg=="
}
```

#### Active license key found

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 500,
    "message": "Active license key found",
    "licenseKey": {
      "id": 1034773,
      "license_key": "3a343c8a-38fe-4b6e-ad77-2222222",
      "owner_name": "Test User",
      "owner_email": "email@domain.ltd",
      "activation_limit": 0,
      "validity": 0,
      "assigned_at": "2024-02-27 03:05:31",
      "meta_data": [
        {
          "key": "test-key",
          "value": "test value y"
        },
        {
          "key": "test-key-2",
          "value": "test value y2"
        }
      ],
      "expires_at": false
    },
    "product": {
      "id": 1,
      "external_reference": "",
      "source": "internal",
      "name": "Test Product",
      "post_url": "",
      "description": "Test product that has it's own private key",
      "meta_data": [
        {
          "key": "test-key",
          "value": "test value x"
        },
        {
          "key": "test-key-2",
          "value": "test value x2"
        }
      ]
    },
    "timestamp": 1709534415
  },
  "response_base64": "eyJjb2RlIjo1MDAsIm1lc3NhZ2UiOiJBY3RpdmUgbGljZW5zZSBrZXkgZm91bmQiLCJsaWNlbnNlS2V5Ijp7ImlkIjoxMDM0NzczLCJsaWNlbnNlX2tleSI6IjNhMzQzYzhhLTM4ZmUtNGI2ZS1hZDc3LTIyMjIyMjIiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYWN0aXZhdGlvbl9saW1pdCI6MCwidmFsaWRpdHkiOjAsImFzc2lnbmVkX2F0IjoiMjAyNC0wMi0yNyAwMzowNTozMSIsIm1ldGFfZGF0YSI6W3sia2V5IjoidGVzdC1rZXkiLCJ2YWx1ZSI6InRlc3QgdmFsdWUgeSJ9LHsia2V5IjoidGVzdC1rZXktMiIsInZhbHVlIjoidGVzdCB2YWx1ZSB5MiJ9XSwiZXhwaXJlc19hdCI6ZmFsc2V9LCJwcm9kdWN0Ijp7ImlkIjoxLCJleHRlcm5hbF9yZWZlcmVuY2UiOiIiLCJzb3VyY2UiOiJpbnRlcm5hbCIsIm5hbWUiOiJUZXN0IFByb2R1Y3QiLCJwb3N0X3VybCI6IiIsImRlc2NyaXB0aW9uIjoiVGVzdCBwcm9kdWN0IHRoYXQgaGFzIGl0J3Mgb3duIHByaXZhdGUga2V5IiwibWV0YV9kYXRhIjpbeyJrZXkiOiJ0ZXN0LWtleSIsInZhbHVlIjoidGVzdCB2YWx1ZSB4In0seyJrZXkiOiJ0ZXN0LWtleS0yIiwidmFsdWUiOiJ0ZXN0IHZhbHVlIHgyIn1dfSwidGltZXN0YW1wIjoxNzA5NTM0NDE1fQ==",
  "private_key_used": "product",
  "signature": "rKceBFV5ySsPy9wKs53c2e35/vJedvf7tjrT7oP/CtkfJbLMGwjA50AV7t5eA5UDFjT77FvU4vDEJUpt8Adq5sogNUkG9S9NH0mYNeDdW/JwYL5cWCFpv3972EopMYiFHNavThl4rTgbtby2gpGRBrBMDbXr4AVLc3Hn5kXWleQ3IFgPFu0I1PNDw+L2TTeVxuY7zq3BvrwuDEv5WXgdW8tbvOs3tyKakU3YLAJKsir0Hk+Ez0p6bKKO3Xwfaed5A3vj/eQXTQJYOzhr9+bDBhIYHScOC31aTfBtg30h/fimI+a9m9MwqxiaD/IxnyYYS5o84M0VKvEBKIYzi/Rc0w=="
}
```
