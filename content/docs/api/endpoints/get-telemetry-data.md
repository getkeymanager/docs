---
title: Get Telemetry
weight: 10
---



## Description

StartFragmeStartFragment

The 'has_red_flags' option allows you to retrieve records with any red flags without specifying particular ones.

## Endpoint Details

- **Method:** `GET`
- **Path:** `/api/v1/get-telemetry-data`
- **Authentication:** API Key (required)

## Request Headers

| Header | Value | Description |
|--------|-------|-------------|
| `Accept` | `application/json` | N/A |

## Request Parameters

None

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### Get Telemetry Data Example

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 970,
    "message": "Telemetry data found",
    "data": [
      {
        "id": 1,
        "user_identifier": "554dddsqfqs4dqd5qsd74q",
        "license_key": "755aed85-409d-490b-a170-e40988c12f5c",
        "activation_identifier": "12135644",
        "product_id": 100,
        "product_version": "5.2.5",
        "data_type": "numeric-single-value",
        "data_group": "test_group",
        "data": "50",
        "is_correct_format": 0,
        "license_key_exists": 0,
        "product_exists": 0,
        "product_version_exists": 0,
        "has_red_flags": 1,
        "created_at": "2024-02-27T01:57:24.000000Z",
        "updated_at": "2024-02-27T01:57:24.000000Z"
      },
      {
        "id": 3,
        "user_identifier": "554dddsqfqs4dqd5qsd74q",
        "license_key": "755aed85-409d-490b-a170-e40988c12f5c",
        "activation_identifier": "12135644",
        "product_id": 100,
        "product_version": "5.2.5",
        "data_type": "numeric-single-value",
        "data_group": "test_group",
        "data": "50",
        "is_correct_format": 0,
        "license_key_exists": 0,
        "product_exists": 0,
        "product_version_exists": 0,
        "has_red_flags": 1,
        "created_at": "2024-02-27T01:58:42.000000Z",
        "updated_at": "2024-02-27T01:58:42.000000Z"
      }
    ],
    "timestamp": 1708999204
  },
  "response_base64": "eyJjb2RlIjo5NzAsIm1lc3NhZ2UiOiJUZWxlbWV0cnkgZGF0YSBmb3VuZCIsImRhdGEiOlt7ImlkIjoxLCJ1c2VyX2lkZW50aWZpZXIiOiI1NTRkZGRzcWZxczRkcWQ1cXNkNzRxIiwibGljZW5zZV9rZXkiOiI3NTVhZWQ4NS00MDlkLTQ5MGItYTE3MC1lNDA5ODhjMTJmNWMiLCJhY3RpdmF0aW9uX2lkZW50aWZpZXIiOiIxMjEzNTY0NCIsInByb2R1Y3RfaWQiOjEwMCwicHJvZHVjdF92ZXJzaW9uIjoiNS4yLjUiLCJkYXRhX3R5cGUiOiJudW1lcmljLXNpbmdsZS12YWx1ZSIsImRhdGFfZ3JvdXAiOiJ0ZXN0X2dyb3VwIiwiZGF0YSI6IjUwIiwiaXNfY29ycmVjdF9mb3JtYXQiOjAsImxpY2Vuc2Vfa2V5X2V4aXN0cyI6MCwicHJvZHVjdF9leGlzdHMiOjAsInByb2R1Y3RfdmVyc2lvbl9leGlzdHMiOjAsImhhc19yZWRfZmxhZ3MiOjEsImNyZWF0ZWRfYXQiOiIyMDI0LTAyLTI3VDAxOjU3OjI0LjAwMDAwMFoiLCJ1cGRhdGVkX2F0IjoiMjAyNC0wMi0yN1QwMTo1NzoyNC4wMDAwMDBaIn0seyJpZCI6MywidXNlcl9pZGVudGlmaWVyIjoiNTU0ZGRkc3FmcXM0ZHFkNXFzZDc0cSIsImxpY2Vuc2Vfa2V5IjoiNzU1YWVkODUtNDA5ZC00OTBiLWExNzAtZTQwOTg4YzEyZjVjIiwiYWN0aXZhdGlvbl9pZGVudGlmaWVyIjoiMTIxMzU2NDQiLCJwcm9kdWN0X2lkIjoxMDAsInByb2R1Y3RfdmVyc2lvbiI6IjUuMi41IiwiZGF0YV90eXBlIjoibnVtZXJpYy1zaW5nbGUtdmFsdWUiLCJkYXRhX2dyb3VwIjoidGVzdF9ncm91cCIsImRhdGEiOiI1MCIsImlzX2NvcnJlY3RfZm9ybWF0IjowLCJsaWNlbnNlX2tleV9leGlzdHMiOjAsInByb2R1Y3RfZXhpc3RzIjowLCJwcm9kdWN0X3ZlcnNpb25fZXhpc3RzIjowLCJoYXNfcmVkX2ZsYWdzIjoxLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yN1QwMTo1ODo0Mi4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjdUMDE6NTg6NDIuMDAwMDAwWiJ9XSwidGltZXN0YW1wIjoxNzA4OTk5MjA0fQ==",
  "private_key_used": "global",
  "signature": "a6tbieNP65lHeVCTXNBqIMHYBpajgFgcTb1dYB6ChNtwh+eq9S3uiphXCIOkheTegVod5d7fE8my5z/FTvtOWj4IUGEWsQrYxn3vlahxLkWlUdxJD8xH+U1+/5qijibQcueWl6Tlpvi0yTBhoEeQ1ZQ6W3zE+D2QHoyhzzCtFraFRYYl7BSqzMcujtz8Dy/tftOItbJRk1LdCfWt48az/MKd5NcKW6nU819u09KoD0ddgxxK3KMueV1Ruv11091Eqba1oYQvtrGWGZFh30/h2xHjKZLq1f7/Ln+vnxEYlSHXTFdBDBgJqdXi44OVUftkZt3AL/GmART95o+/CC3EZA=="
}
```
