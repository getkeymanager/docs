---
title: Generate
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/generate`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `generator_id` | text | Yes | Required; Generator ID | `1` |
| `quantity` | text | Yes | Required; Number of license keys to generate | `10` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### Generate

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 815,
    "message": "Generated license keys",
    "licenseKeys": [
      "95f0b74a-4e73-4232-8197-44ac0986eb44",
      "32b2597b-c3ab-4796-abb4-d20852ba0216",
      "da118e1f-1e3d-4702-b288-ca0ce8e1c752",
      "84337117-143e-478d-b75f-0bbe1aa9d3f8",
      "267478bd-9d02-4945-9263-1494ea5d5ca5",
      "8249fc3c-190f-4b10-b36f-c4a9f6ef7817",
      "bee86a35-7b42-416b-81ac-0210e89be604",
      "9356b053-afb8-4f01-9e03-33e657d95615",
      "19d4c2a0-b2ee-47a9-9fa7-f8befcc142fd",
      "d8696cbb-c702-4ac3-985d-4fd4ee65420b"
    ],
    "timestamp": 1709003415
  },
  "response_base64": "eyJjb2RlIjo4MTUsIm1lc3NhZ2UiOiJHZW5lcmF0ZWQgbGljZW5zZSBrZXlzIiwibGljZW5zZUtleXMiOlsiOTVmMGI3NGEtNGU3My00MjMyLTgxOTctNDRhYzA5ODZlYjQ0IiwiMzJiMjU5N2ItYzNhYi00Nzk2LWFiYjQtZDIwODUyYmEwMjE2IiwiZGExMThlMWYtMWUzZC00NzAyLWIyODgtY2EwY2U4ZTFjNzUyIiwiODQzMzcxMTctMTQzZS00NzhkLWI3NWYtMGJiZTFhYTlkM2Y4IiwiMjY3NDc4YmQtOWQwMi00OTQ1LTkyNjMtMTQ5NGVhNWQ1Y2E1IiwiODI0OWZjM2MtMTkwZi00YjEwLWIzNmYtYzRhOWY2ZWY3ODE3IiwiYmVlODZhMzUtN2I0Mi00MTZiLTgxYWMtMDIxMGU4OWJlNjA0IiwiOTM1NmIwNTMtYWZiOC00ZjAxLTllMDMtMzNlNjU3ZDk1NjE1IiwiMTlkNGMyYTAtYjJlZS00N2E5LTlmYTctZjhiZWZjYzE0MmZkIiwiZDg2OTZjYmItYzcwMi00YWMzLTk4NWQtNGZkNGVlNjU0MjBiIl0sInRpbWVzdGFtcCI6MTcwOTAwMzQxNX0=",
  "private_key_used": "product",
  "signature": "a+ms31dF/DSlbEfbBfvg7D7LuJff43zvR20wAlD8tqZrwy3s1WyfPjYctHUDqCgBHOcNntyKgFihrlJMi7eMbdeEdWLw12CRIzEIV9GvidhpbQYenYGXMbXqnm1vduwI/plsa48HOLmg1byHHCmK6Ko1M7vyuqz3DJke5XXAGSMYWYyQ9fsEKlvRNinHqt5SyRb6ngA8oQ4fRLY9qyZ6/0RHXfAK/zYytSr8MHaIQs5bazFN4K3ciWsv+aU2pYdoBBwyR+ayn7Q1Jh9S8t02/2EqKV8Yguj3tPvbUgbCzC/8gj0nsD75pqQ1o3oah/Y4D1TIJjRkHetzBDCQkMJQXA=="
}
```
