---
title: Get License Keys
weight: 10
---

# Get License Keys

## Endpoint Details

- **Method:** `GET`
- **Path:** `/api/v1/get-license-keys`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

None

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### License keys

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 730,
    "message": "License keys",
    "license_keys": [
      {
        "id": 944516,
        "product_id": 1,
        "license_key": "2f09f12d-7040-4bc6-a506-23f372d09a25",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944517,
        "product_id": 1,
        "license_key": "85940963-97bd-4ba7-9f60-5d431662079a",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944518,
        "product_id": 1,
        "license_key": "270d342e-8e95-4607-b932-7d79be520976",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944519,
        "product_id": 1,
        "license_key": "880a351d-c100-409a-bcde-7bc6cb97c8c1",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944520,
        "product_id": 1,
        "license_key": "1416b187-2b55-4bc7-b0c8-9df2fba9d8cd",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944521,
        "product_id": 1,
        "license_key": "24d16e40-c343-40fb-9fbf-3555e0543ae1",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944522,
        "product_id": 1,
        "license_key": "dc2d70c5-85c7-4838-ac20-cefb9d9e6e7f",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944523,
        "product_id": 1,
        "license_key": "4c16b3ad-dd0a-45bd-9072-4d613577a112",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944524,
        "product_id": 1,
        "license_key": "9e003e21-dcbe-475e-82ad-238305c723a0",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      },
      {
        "id": 944525,
        "product_id": 1,
        "license_key": "0b9c5c36-813f-4f4c-9cf3-ce2d291089f8",
        "owner_name": null,
        "owner_email": null,
        "activation_limit": 1,
        "validity": 365,
        "assigned_at": null,
        "status": "available",
        "created_at": "2024-02-24T21:21:24.000000Z",
        "updated_at": "2024-02-24T21:21:24.000000Z"
      }
    ],
    "timestamp": 1709003445
  },
  "response_base64": "eyJjb2RlIjo3MzAsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleXMiLCJsaWNlbnNlX2tleXMiOlt7ImlkIjo5NDQ1MTYsInByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiMmYwOWYxMmQtNzA0MC00YmM2LWE1MDYtMjNmMzcyZDA5YTI1Iiwib3duZXJfbmFtZSI6bnVsbCwib3duZXJfZW1haWwiOm51bGwsImFjdGl2YXRpb25fbGltaXQiOjEsInZhbGlkaXR5IjozNjUsImFzc2lnbmVkX2F0IjpudWxsLCJzdGF0dXMiOiJhdmFpbGFibGUiLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMToyMToyNC4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjRUMjE6MjE6MjQuMDAwMDAwWiJ9LHsiaWQiOjk0NDUxNywicHJvZHVjdF9pZCI6MSwibGljZW5zZV9rZXkiOiI4NTk0MDk2My05N2JkLTRiYTctOWY2MC01ZDQzMTY2MjA3OWEiLCJvd25lcl9uYW1lIjpudWxsLCJvd25lcl9lbWFpbCI6bnVsbCwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwiYXNzaWduZWRfYXQiOm51bGwsInN0YXR1cyI6ImF2YWlsYWJsZSIsImNyZWF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIxOjIxOjI0LjAwMDAwMFoiLCJ1cGRhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMToyMToyNC4wMDAwMDBaIn0seyJpZCI6OTQ0NTE4LCJwcm9kdWN0X2lkIjoxLCJsaWNlbnNlX2tleSI6IjI3MGQzNDJlLThlOTUtNDYwNy1iOTMyLTdkNzliZTUyMDk3NiIsIm93bmVyX25hbWUiOm51bGwsIm93bmVyX2VtYWlsIjpudWxsLCJhY3RpdmF0aW9uX2xpbWl0IjoxLCJ2YWxpZGl0eSI6MzY1LCJhc3NpZ25lZF9hdCI6bnVsbCwic3RhdHVzIjoiYXZhaWxhYmxlIiwiY3JlYXRlZF9hdCI6IjIwMjQtMDItMjRUMjE6MjE6MjQuMDAwMDAwWiIsInVwZGF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIxOjIxOjI0LjAwMDAwMFoifSx7ImlkIjo5NDQ1MTksInByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiODgwYTM1MWQtYzEwMC00MDlhLWJjZGUtN2JjNmNiOTdjOGMxIiwib3duZXJfbmFtZSI6bnVsbCwib3duZXJfZW1haWwiOm51bGwsImFjdGl2YXRpb25fbGltaXQiOjEsInZhbGlkaXR5IjozNjUsImFzc2lnbmVkX2F0IjpudWxsLCJzdGF0dXMiOiJhdmFpbGFibGUiLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMToyMToyNC4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjRUMjE6MjE6MjQuMDAwMDAwWiJ9LHsiaWQiOjk0NDUyMCwicHJvZHVjdF9pZCI6MSwibGljZW5zZV9rZXkiOiIxNDE2YjE4Ny0yYjU1LTRiYzctYjBjOC05ZGYyZmJhOWQ4Y2QiLCJvd25lcl9uYW1lIjpudWxsLCJvd25lcl9lbWFpbCI6bnVsbCwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwiYXNzaWduZWRfYXQiOm51bGwsInN0YXR1cyI6ImF2YWlsYWJsZSIsImNyZWF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIxOjIxOjI0LjAwMDAwMFoiLCJ1cGRhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMToyMToyNC4wMDAwMDBaIn0seyJpZCI6OTQ0NTIxLCJwcm9kdWN0X2lkIjoxLCJsaWNlbnNlX2tleSI6IjI0ZDE2ZTQwLWMzNDMtNDBmYi05ZmJmLTM1NTVlMDU0M2FlMSIsIm93bmVyX25hbWUiOm51bGwsIm93bmVyX2VtYWlsIjpudWxsLCJhY3RpdmF0aW9uX2xpbWl0IjoxLCJ2YWxpZGl0eSI6MzY1LCJhc3NpZ25lZF9hdCI6bnVsbCwic3RhdHVzIjoiYXZhaWxhYmxlIiwiY3JlYXRlZF9hdCI6IjIwMjQtMDItMjRUMjE6MjE6MjQuMDAwMDAwWiIsInVwZGF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIxOjIxOjI0LjAwMDAwMFoifSx7ImlkIjo5NDQ1MjIsInByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiZGMyZDcwYzUtODVjNy00ODM4LWFjMjAtY2VmYjlkOWU2ZTdmIiwib3duZXJfbmFtZSI6bnVsbCwib3duZXJfZW1haWwiOm51bGwsImFjdGl2YXRpb25fbGltaXQiOjEsInZhbGlkaXR5IjozNjUsImFzc2lnbmVkX2F0IjpudWxsLCJzdGF0dXMiOiJhdmFpbGFibGUiLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMToyMToyNC4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjRUMjE6MjE6MjQuMDAwMDAwWiJ9LHsiaWQiOjk0NDUyMywicHJvZHVjdF9pZCI6MSwibGljZW5zZV9rZXkiOiI0YzE2YjNhZC1kZDBhLTQ1YmQtOTA3Mi00ZDYxMzU3N2ExMTIiLCJvd25lcl9uYW1lIjpudWxsLCJvd25lcl9lbWFpbCI6bnVsbCwiYWN0aXZhdGlvbl9saW1pdCI6MSwidmFsaWRpdHkiOjM2NSwiYXNzaWduZWRfYXQiOm51bGwsInN0YXR1cyI6ImF2YWlsYWJsZSIsImNyZWF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIxOjIxOjI0LjAwMDAwMFoiLCJ1cGRhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMToyMToyNC4wMDAwMDBaIn0seyJpZCI6OTQ0NTI0LCJwcm9kdWN0X2lkIjoxLCJsaWNlbnNlX2tleSI6IjllMDAzZTIxLWRjYmUtNDc1ZS04MmFkLTIzODMwNWM3MjNhMCIsIm93bmVyX25hbWUiOm51bGwsIm93bmVyX2VtYWlsIjpudWxsLCJhY3RpdmF0aW9uX2xpbWl0IjoxLCJ2YWxpZGl0eSI6MzY1LCJhc3NpZ25lZF9hdCI6bnVsbCwic3RhdHVzIjoiYXZhaWxhYmxlIiwiY3JlYXRlZF9hdCI6IjIwMjQtMDItMjRUMjE6MjE6MjQuMDAwMDAwWiIsInVwZGF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIxOjIxOjI0LjAwMDAwMFoifSx7ImlkIjo5NDQ1MjUsInByb2R1Y3RfaWQiOjEsImxpY2Vuc2Vfa2V5IjoiMGI5YzVjMzYtODEzZi00ZjRjLTljZjMtY2UyZDI5MTA4OWY4Iiwib3duZXJfbmFtZSI6bnVsbCwib3duZXJfZW1haWwiOm51bGwsImFjdGl2YXRpb25fbGltaXQiOjEsInZhbGlkaXR5IjozNjUsImFzc2lnbmVkX2F0IjpudWxsLCJzdGF0dXMiOiJhdmFpbGFibGUiLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMToyMToyNC4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjRUMjE6MjE6MjQuMDAwMDAwWiJ9XSwidGltZXN0YW1wIjoxNzA5MDAzNDQ1fQ==",
  "private_key_used": "global",
  "signature": "FnpuID8U+2gGke5Bbxw44QDHhiohWCH+GJViCpA22OrHclbRo/K4N4V8gpUBik8zcnQV3mYjaNVOLcNj46Aqh5cPg2Bd0knw71D5JzgZa+xDGXaYY1bywIGUHCS2Irj0ptAqh6CK+nMU0Gp9SIOD2rukjOGcFWQQFtsdY0JDiogsFEOrRHXWj+QLuEPGAx5Tf5UMLd5fqf+Ia3F/8mAJ59g9W5mh8WBfIaZAt8sO0MnTtVvv6C2l4h9kesK7u2mL9qI88cUTyW9rVBl8UwnswudbBL/vfYz7PjrHKE3pLjJjyP6OC72NOVUfTo/hQNED3WfUXY+v+WyJFC8e4ghz1A=="
}
```
