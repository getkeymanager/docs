---
title: Create License Keys
weight: 10
---

# Create License Keys

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/create-license-keys`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_keys` | text | Yes | Required; JSON Array; License keys | `["3a343c8a-38fe-4b6e-ad77-444444","3a343c8a-38fe-4b6e-ad77-2222222","3a343c8a-38fe-4b6e-ad77-0078aaf16-333333", "9cc2cc83-4c74-49f9-98f5-f0e1c1eb1541"]` |
| `product_id` | text | Yes | Required; Product ID | `1` |
| `owner_name` | text | Yes | Optional; Owner name | `Test User` |
| `owner_email` | text | Yes | Optional; Owner email | `domain@email.ltdc` |
| `activation_limit` | text | Yes | Required; Activation limit | `0` |
| `validity` | text | Yes | Required; Validity in number of days | `0` |
| `status` | text | Yes | Required; Status, can be 'available', 'assigned', 'reserved', and 'blocked' | `available` |
| `assigned_at` | text | Yes | Optional; Assigned at date will be used to calculate the expiration date | `2024-01-08 00:00:00` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### License keys creation result

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 900,
    "message": "License keys creation result",
    "created": 3,
    "duplicate": 1,
    "timestamp": 1709001673
  },
  "response_base64": "eyJjb2RlIjo5MDAsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleXMgY3JlYXRpb24gcmVzdWx0IiwiY3JlYXRlZCI6MywiZHVwbGljYXRlIjoxLCJ0aW1lc3RhbXAiOjE3MDkwMDE2NzN9",
  "private_key_used": "product",
  "signature": "seZ4pLhzlFADJ7e6S738KV9+Lr3gojb/frGxjEOlefdAP9dzd3HiC9IgtQm7I6mbkjF0pZaAJzh3P7DhgstDiqSRX5br1uvmC+GzLesiVEI5gyKRgEwuMOil85EiMLxmsk3kFqOXrdPMI1DeBK8qGxMd0Oo89LfSEMm2bDlyujxIUgBzQiCBZDXxKOLh5/RDkIBzFNGWJ3tls4RdtU2U2J8VWBw7F7LRIYr4kYSZHgJ5c8Hdkeu2hralhz1u1swMn6yf/gJzIbt5geqizgShLQ1P8tyqMLuk3lZDM8Hu/BgdxFSsVY0PquxZZE30TW6mGjxw0VrSlp44FSeF9y20Gg=="
}
```
