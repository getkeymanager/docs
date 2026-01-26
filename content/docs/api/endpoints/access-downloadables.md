---
title: Access Downloadables
weight: 10
---

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/access-downloadables`
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

This endpoint has **1** documented response example(s) in the Postman collection.

#### Downloads

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 600,
    "message": "Downloads",
    "downloadables": [
      {
        "id": 2,
        "product_id": 1,
        "numeric_version": 102,
        "version": "1.0.2",
        "update_summary": "Bugfixes",
        "changelog": "Bugfixes",
        "published": 1,
        "release_date": "2024-02-27 00:00:00",
        "download_counter": 0,
        "url": "https://getKeyManager.local/api/v1/download/2964c3c9-0b5d-4d89-b3ac-4668f30bc492/65a90cff-8da2-4820-9c9a-a13a041891fd/ZG9tYWluLmx0ZA%3D%3D/102"
      },
      {
        "id": 1,
        "product_id": 1,
        "numeric_version": 101,
        "version": "1.0.1",
        "update_summary": "Bugfixes",
        "changelog": "Minor bug fixes",
        "published": 1,
        "release_date": "2024-02-27 00:00:00",
        "download_counter": 0,
        "url": "https://getKeyManager.local/api/v1/download/2964c3c9-0b5d-4d89-b3ac-4668f30bc492/65a90cff-8da2-4820-9c9a-a13a041891fd/ZG9tYWluLmx0ZA%3D%3D/101"
      }
    ],
    "timestamp": 1709001214
  },
  "response_base64": "eyJjb2RlIjo2MDAsIm1lc3NhZ2UiOiJMaUNlbnNlIGtleSBmb3VuZCIsImRvd25sb2FkYWJsZXMiOlt7ImlkIjoyLCJwcm9kdWN0X2lkIjoxLCJudW1lcmljX3ZlcnNpb24iOjEwMiwidmVyc2lvbiI6IjEuMC4yIiwidXBkYXRlX3N1bW1hcnkiOiJCdWdmaXhlcyIsImNoYW5nZWxvZyI6IkJ1Z2ZpeGVzIiwicHVibGlzaGVkIjoxLCJyZWxlYXNlX2RhdGUiOiIyMDI0LTAyLTI3IDAwOjAwOjAwIiwiZG93bmxvYWRfY291bnRlciI6MCwidXJsIjoiaHR0cHM6XC9cL2tlZXZhdWx0LmxvY2FsXC9hcGlcL3YxXC9kb3dubG9hZFwvMjk2NGMzYzktMGI1ZC00ZDg5LWIzYWMtNDY2OGYzMGJjNDkyXC82NWE5MGNmZi04ZGEyLTQ4MjAtOWM5YS1hMTNhMDQxODkxZmRcL1pHOXRZV2x1TG14MFpBJTNEJTNEXC8xMDIifSx7ImlkIjoxLCJwcm9kdWN0X2lkIjoxLCJudW1lcmljX3ZlcnNpb24iOjEwMSwidmVyc2lvbiI6IjEuMC4xIiwidXBkYXRlX3N1bW1hcnkiOiJCdWdmaXhlcyIsImNoYW5nZWxvZyI6Ik1pbm9yIGJ1ZyBmaXhlcyIsInB1Ymxpc2hlZCI6MSwicmVsZWFzZV9kYXRlIjoiMjAyNC0wMi0yNyAwMDowMDowMCIsImRvd25sb2FkX2NvdW50ZXIiOjAsInVybCI6Imh0dHBzOlwvXC9rZWV2YXVsdC5sb2NhbFwvYXBpXC92MVwvZG93bmxvYWRcLzI5NjRjM2M5LTBiNWQtNGQ4OS1iM2FjLTQ2NjhmMzBiYzQ5MlwvNjVhOTBjZmYtOGRhMi00ODIwLTljOWEtYTEzYTA0MTg5MWZkXC9aRzl0WVdsdUxteDBaQSUzRCUzRFwvMTAxIn1dLCJ0aW1lc3RhbXAiOjE3MDkwMDEyMTR9",
  "private_key_used": "product",
  "signature": "OnKB1KO7hlPVHK500ykyucQjBPmef2W1vTLaUAXh/AzCI6XNwK7TbxQj1lspdbovaeXzonQsOrL/Lx9jyT0s9uz8dC7P00dSOPM1zj0AnPOtn04BtnZKkH4VLT+0/xvYtsn0GMQ6slsL3jhruxb59G7Bv4Gq3zEG6dnCRcQDnH7SxAYNwXUXLglZ2CggCe/5pk1JCF5hijRnQjELJ5Uhr2Ut1m/7FjTxbNN8TXlTgDe0nbtJ+kUOCaPrvH7M+vbTJf2gy6/bc1aQDmZV4S0rAk/VEaBrVAcTXswJJ3xB/3JN+1fNWBpPAtcFqUL3dyNp56/fcpDVi4yEzwzYWsDBgQ=="
}
```
