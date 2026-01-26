---
title: Random Assign License Keys
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/random-assign-license-keys`
- **Authentication:** API Key (required)

## Request Headers

| Header | Value | Description |
|--------|-------|-------------|
| `Accept` | `application/json` | N/A |

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `product_id` | text | Yes | Required; Product ID | `1` |
| `owner_name` | text | Yes | Optional; Owner Name | `Test User` |
| `owner_email` | text | Yes | N/A | `email@domain.ltd` |
| `quantity` | text | Yes | N/A | `7` |
| `generate` | text | Yes | N/A | `0` |

## Response Examples

This endpoint has **4** documented response example(s) in the Postman collection.

#### License keys generated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 803,
    "message": "License keys assigned",
    "license_keys": [
      {
        "product_id": 1,
        "license_key": "1de7d049-3160-44c2-b260-fc12b2b7e702",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.829115Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 213,
        "meta_data": []
      },
      {
        "product_id": 1,
        "license_key": "5872476e-ff56-4ac2-99ef-2ceb86c64e89",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.830500Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 214,
        "meta_data": []
      },
      {
        "product_id": 1,
        "license_key": "bca4e747-e66b-40ce-b779-fa0210d9d78a",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.831818Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 215,
        "meta_data": []
      },
      {
        "product_id": 1,
        "license_key": "185a58da-1272-4163-be16-9fc75d108a0b",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.833101Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 216,
        "meta_data": []
      },
      {
        "product_id": 1,
        "license_key": "4a8337d8-472a-433e-b7b9-90cdb899b591",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.834370Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 217,
        "meta_data": []
      },
      {
        "product_id": 1,
        "license_key": "a4c4465a-85d7-4828-9914-9c817fa61679",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.835808Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 218,
        "meta_data": []
      },
      {
        "product_id": 1,
        "license_key": "6e3f88a4-17b7-46a7-81ee-09447e947939",
        "activation_limit": 1,
        "validity": 365,
        "status": "assigned",
        "owner_name": "Test User",
        "owner_email": "email@domain.ltd",
        "assigned_at": "2024-11-23T19:02:08.837173Z",
        "contract_id": null,
        "updated_at": "2024-11-23T19:02:08.000000Z",
        "created_at": "2024-11-23T19:02:08.000000Z",
        "id": 219,
        "meta_data": []
      }
    ],
    "timestamp": 1732388528
  },
  "response_base64": "eyJjb2RlIjo4MDMsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleXMgYXNzaWduZWQiLCJsaWNlbnNlX2tleXMiOlt7InByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiMWRlN2QwNDktMzE2MC00NGMyLWIyNjAtZmMxMmIyYjdlNzAyIiwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwic3RhdHVzIjoiYXNzaWduZWQiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYXNzaWduZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjgyOTExNVoiLCJjb250cmFjdF9pZCI6bnVsbCwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMjNUMTk6MDI6MDguMDAwMDAwWiIsImNyZWF0ZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjAwMDAwMFoiLCJpZCI6MjEzLCJtZXRhX2RhdGEiOltdfSx7InByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiNTg3MjQ3NmUtZmY1Ni00YWMyLTk5ZWYtMmNlYjg2YzY0ZTg5IiwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwic3RhdHVzIjoiYXNzaWduZWQiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYXNzaWduZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjgzMDUwMFoiLCJjb250cmFjdF9pZCI6bnVsbCwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMjNUMTk6MDI6MDguMDAwMDAwWiIsImNyZWF0ZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjAwMDAwMFoiLCJpZCI6MjE0LCJtZXRhX2RhdGEiOltdfSx7InByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiYmNhNGU3NDctZTY2Yi00MGNlLWI3NzktZmEwMjEwZDlkNzhhIiwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwic3RhdHVzIjoiYXNzaWduZWQiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYXNzaWduZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjgzMTgxOFoiLCJjb250cmFjdF9pZCI6bnVsbCwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMjNUMTk6MDI6MDguMDAwMDAwWiIsImNyZWF0ZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjAwMDAwMFoiLCJpZCI6MjE1LCJtZXRhX2RhdGEiOltdfSx7InByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiMTg1YTU4ZGEtMTI3Mi00MTYzLWJlMTYtOWZjNzVkMTA4YTBiIiwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwic3RhdHVzIjoiYXNzaWduZWQiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYXNzaWduZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjgzMzEwMVoiLCJjb250cmFjdF9pZCI6bnVsbCwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMjNUMTk6MDI6MDguMDAwMDAwWiIsImNyZWF0ZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjAwMDAwMFoiLCJpZCI6MjE2LCJtZXRhX2RhdGEiOltdfSx7InByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiNGE4MzM3ZDgtNDcyYS00MzNlLWI3YjktOTBjZGI4OTliNTkxIiwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwic3RhdHVzIjoiYXNzaWduZWQiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYXNzaWduZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjgzNDM3MFoiLCJjb250cmFjdF9pZCI6bnVsbCwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMjNUMTk6MDI6MDguMDAwMDAwWiIsImNyZWF0ZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjAwMDAwMFoiLCJpZCI6MjE3LCJtZXRhX2RhdGEiOltdfSx7InByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiYTRjNDQ2NWEtODVkNy00ODI4LTk5MTQtOWM4MTdmYTYxNjc5IiwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwic3RhdHVzIjoiYXNzaWduZWQiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYXNzaWduZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjgzNTgwOFoiLCJjb250cmFjdF9pZCI6bnVsbCwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMjNUMTk6MDI6MDguMDAwMDAwWiIsImNyZWF0ZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjAwMDAwMFoiLCJpZCI6MjE4LCJtZXRhX2RhdGEiOltdfSx7InByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiNmUzZjg4YTQtMTdiNy00NmE3LTgxZWUtMDk0NDdlOTQ3OTM5IiwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwic3RhdHVzIjoiYXNzaWduZWQiLCJvd25lcl9uYW1lIjoiVGVzdCBVc2VyIiwib3duZXJfZW1haWwiOiJlbWFpbEBkb21haW4ubHRkIiwiYXNzaWduZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjgzNzE3M1oiLCJjb250cmFjdF9pZCI6bnVsbCwidXBkYXRlZF9hdCI6IjIwMjQtMTEtMjNUMTk6MDI6MDguMDAwMDAwWiIsImNyZWF0ZWRfYXQiOiIyMDI0LTExLTIzVDE5OjAyOjA4LjAwMDAwMFoiLCJpZCI6MjE5LCJtZXRhX2RhdGEiOltdfV0sInRpbWVzdGFtcCI6MTczMjM4ODUyOH0=",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```

#### Product not found

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 805,
    "message": "Product not found",
    "timestamp": 1732388563
  },
  "response_base64": "eyJjb2RlIjo4MDUsIm1lc3NhZ2UiOiJQcm9kdWN0IG5vdCBmb3VuZCIsInRpbWVzdGFtcCI6MTczMjM4ODU2M30=",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```

#### Generator not found

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 806,
    "message": "Generator not found",
    "timestamp": 1732388605
  },
  "response_base64": "eyJjb2RlIjo4MDYsIm1lc3NhZ2UiOiJHZW5lcmF0b3Igbm90IGZvdW5kIiwidGltZXN0YW1wIjoxNzMyMzg4NjA1fQ==",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```

#### Insufficient license keys

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 802,
    "message": "Insufficient license keys",
    "available_quantity": 5,
    "timestamp": 1732388664
  },
  "response_base64": "eyJjb2RlIjo4MDIsIm1lc3NhZ2UiOiJJbnN1ZmZpY2llbnQgbGljZW5zZSBrZXlzIiwiYXZhaWxhYmxlX3F1YW50aXR5Ijo1LCJ0aW1lc3RhbXAiOjE3MzIzODg2NjR9",
  "private_key_used": "global",
  "signature": "Private key not set"
}
```
