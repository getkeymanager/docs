---
title: Get All Generators
weight: 10
---

## Endpoint Details

- **Method:** `GET`
- **Path:** `/api/v1/get-all-generators`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

None

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### All generators

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 820,
    "message": "All generators",
    "products": [
      {
        "id": 1,
        "product_id": 1,
        "method": "uuid",
        "prefix": "",
        "suffix": "",
        "function_name": "",
        "number_of_chunks": 4,
        "chunk_length": 4,
        "activation_limit": 1,
        "validity": 365,
        "status": 1,
        "charset": "0123456789ABCDEF",
        "created_at": "2024-02-24T20:54:16.000000Z",
        "updated_at": "2024-02-24T20:54:16.000000Z"
      },
      {
        "id": 2,
        "product_id": 2,
        "method": "chunk-system",
        "prefix": "",
        "suffix": "",
        "function_name": "",
        "number_of_chunks": 4,
        "chunk_length": 4,
        "activation_limit": 1,
        "validity": 365,
        "status": 0,
        "charset": "0123456789ABCDEF",
        "created_at": "2024-02-24T20:54:28.000000Z",
        "updated_at": "2024-02-24T20:54:28.000000Z"
      },
      {
        "id": 3,
        "product_id": 4,
        "method": "custom",
        "prefix": "",
        "suffix": "",
        "function_name": "testFunction",
        "number_of_chunks": 4,
        "chunk_length": 4,
        "activation_limit": 1,
        "validity": 0,
        "status": 0,
        "charset": "0123456789ABCDEF",
        "created_at": "2024-02-24T20:55:28.000000Z",
        "updated_at": "2024-02-24T20:55:28.000000Z"
      }
    ],
    "timestamp": 1709003381
  },
  "response_base64": "eyJjb2RlIjo4MjAsIm1lc3NhZ2UiOiJBbGwgZ2VuZXJhdG9ycyIsInByb2R1Y3RzIjpbeyJpZCI6MSwicHJvZHVjdF9pZCI6MSwibWV0aG9kIjoidXVpZCIsInByZWZpeCI6IiIsInN1ZmZpeCI6IiIsImZ1bmN0aW9uX25hbWUiOiIiLCJudW1iZXJfb2ZfY2h1bmtzIjo0LCJjaHVua19sZW5ndGgiOjQsImFjdGl2YXRpb25fbGltaXQiOjEsInZhbGlkaXR5IjozNjUsInN0YXR1cyI6MSwiY2hhcnNldCI6IjAxMjM0NTY3ODlBQkNERUYiLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMDo1NDoxNi4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjRUMjA6NTQ6MTYuMDAwMDAwWiJ9LHsiaWQiOjIsInByb2R1Y3RfaWQiOjIsIm1ldGhvZCI6ImNodW5rLXN5c3RlbSIsInByZWZpeCI6IiIsInN1ZmZpeCI6IiIsImZ1bmN0aW9uX25hbWUiOiIiLCJudW1iZXJfb2ZfY2h1bmtzIjo0LCJjaHVua19zZW5ndGgiOjQsImFjdGl2YXRpb25fbGltaXQiOjEsInZhbGlkaXR5IjozNjUsInN0YXR1cyI6MCwiY2hhcnNldCI6IjAxMjM0NTY3ODlBQkNERUYiLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMDo1NDoyOC4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjRUMjA6NTQ6MjguMDAwMDAwWiJ9LHsiaWQiOjMsInByb2R1Y3RfaWQiOjQsIm1ldGhvZCI6ImN1c3RvbSIsInByZWZpeCI6IiIsInN1ZmZpeCI6IiIsImZ1bmN0aW9uX25hbWUiOiJ0ZXN0RnVuY3Rpb24iLCJudW1iZXJfb2ZfY2h1bmtzIjo0LCJjaHVua19zZW5ndGgiOjQsImFjdGl2YXRpb25fbGltaXQiOjEsInZhbGlkaXR5IjowLCJzdGF0dXMiOjAsImNoYXJzZXQiOiIwMTIzNDU2Nzg5QUJDREVGIiwiY3JlYXRlZF9hdCI6IjIwMjQtMDItMjRUMjA6NTU6MjguMDAwMDAwWiIsInVwZGF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIwOjU1OjI4LjAwMDAwMFoifV0sInRpbWVzdGFtcCI6MTcwOTAwMzM4MX0=",
  "private_key_used": "global",
  "signature": "k/5qRBe9iHPFfO1Y3G1Qo9tHGqHc5Se4pG3aVnNPU5lAuROMEl16dJzMcLZ9Plwfx/SZ+rBIT0d8ngVN+QWwIqVkkCyGTyrvjXKI7vlzaSYX7GFMe703e2yJQadOSv2owvjpCY0Nwrqfgfms3GZM7Bt22MMyv/CljxN0YZMly60I874+jApcX9TqDI9zLUndrE4oKcscOyQyjmGRG5E1NYXXv//z9nQQbygtUD+NhPzMRKuWa7a01H+YzDLcFGx6d2BcpBpcrB2Z5Ewu8f7MnH9m8EUu7z+nWERBLldSLDTtCIGSWyb8QGkOIKKph1ui4scZMFwDBpKRKshlzH4BYw=="
}
```
