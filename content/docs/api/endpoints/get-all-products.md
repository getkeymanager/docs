---
title: Get All Products
weight: 10
---

# Get All Products

## Endpoint Details

- **Method:** `GET`
- **Path:** `/api/v1/get-all-products`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

None

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### All products

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 810,
    "message": "All products",
    "products": [
      {
        "id": 1,
        "external_reference": "",
        "source": "internal",
        "name": "Test Product",
        "post_url": "",
        "description": "Test product that has it's own private key",
        "status": "active",
        "require_non_expired": 0,
        "created_at": "2024-02-24T16:57:17.000000Z",
        "updated_at": "2024-02-24T18:36:00.000000Z",
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
      {
        "id": 2,
        "external_reference": "",
        "source": "internal",
        "name": " Deski Support",
        "post_url": "",
        "description": " WordPress HelpDesk & Support Ticketing Plugin",
        "status": "active",
        "require_non_expired": 0,
        "created_at": "2024-02-24T20:50:57.000000Z",
        "updated_at": "2024-02-24T20:50:57.000000Z",
        "meta_data": []
      },
      {
        "id": 3,
        "external_reference": "",
        "source": "internal",
        "name": "Example Product",
        "post_url": "",
        "description": "Inactive product example",
        "status": "active",
        "require_non_expired": 0,
        "created_at": "2024-02-24T20:51:47.000000Z",
        "updated_at": "2024-03-03T08:47:49.000000Z",
        "meta_data": []
      },
      {
        "id": 4,
        "external_reference": "",
        "source": "internal",
        "name": "Nanosoft Doors",
        "post_url": "",
        "description": "Desktop operation system",
        "status": "active",
        "require_non_expired": 1,
        "created_at": "2024-02-24T20:53:41.000000Z",
        "updated_at": "2024-02-24T20:53:41.000000Z",
        "meta_data": []
      }
    ],
    "timestamp": 1709534400
  },
  "response_base64": "eyJjb2RlIjo4MTAsIm1lc3NhZ2UiOiJBbGwgcHJvZHVjdHMiLCJwcm9kdWN0cyI6W3siaWQiOjEsImV4dGVybmFsX3JlZmVyZW5jZSI6IiIsInNvdXJjZSI6ImludGVybmFsIiwibmFtZSI6IlRlc3QgUHJvZHVjdCIsInBvc3RfdXJsIjoiIiwiZGVzY3JpcHRpb24iOiJUZXN0IHByb2R1Y3QgdGhhdCBoYXMgaXQncyBvd24gcHJpdmF0ZSBrZXkiLCJzdGF0dXMiOiJhY3RpdmUiLCJyZXF1aXJlX25vbl9leHBpcmVkIjowLCJjcmVhdGVkX2F0IjoiMjAyNC0wMi0yNFQxNjo1NzoxNy4wMDAwMDBaIiwidXBkYXRlZF9hdCI6IjIwMjQtMDItMjRUMTg6MzY6MDAuMDAwMDAwWiIsIm1ldGFfZGF0YSI6W3sia2V5IjoidGVzdC1rZXkiLCJ2YWx1ZSI6InRlc3QgdmFsdWUgeCJ9LHsia2V5IjoidGVzdC1rZXktMiIsInZhbHVlIjoidGVzdCB2YWx1ZSB4MiJ9XX0seyJpZCI6MiwiZXh0ZXJuYWxfcmVmZXJlbmNlIjoiIiwic291cmNlIjoiaW50ZXJuYWwiLCJuYW1lIjoiIERlc2tpIFN1cHBvcnQiLCJwb3N0X3VybCI6IiIsImRlc2NyaXB0aW9uIjoiIFdvcmRQcmVzcyBIZWxwRGVzayAmIFN1cHBvcnQgVGlja2V0aW5nIFBsdWdpbiIsInN0YXR1cyI6ImFjdGl2ZSIsInJlcXVpcmVfbm9uX2V4cGlyZWQiOjAsImNyZWF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIwOjUwOjU3LjAwMDAwMFoiLCJ1cGRhdGVkX2F0IjoiMjAyNC0wMi0yNFQyMDo1MDo1Ny4wMDAwMDBaIiwibWV0YV9kYXRhIjpbXX0seyJpZCI6MywiZXh0ZXJuYWxfcmVmZXJlbmNlIjoiIiwic291cmNlIjoiaW50ZXJuYWwiLCJuYW1lIjoiRXhhbXBsZSBQcm9kdWN0IiwicG9zdF91cmwiOiIiLCJkZXNjcmlwdGlvbiI6IkluYWN0aXZlIHByb2R1Y3QgZXhhbXBsZSIsInN0YXR1cyI6ImFjdGl2ZSIsInJlcXVpcmVfbm9uX2V4cGlyZWQiOjAsImNyZWF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIwOjUxOjQ3LjAwMDAwMFoiLCJ1cGRhdGVkX2F0IjoiMjAyNC0wMy0wM1QwODo0Nzo0OS4wMDAwMDBaIiwibWV0YV9kYXRhIjpbXX0seyJpZCI6NCwiZXh0ZXJuYWxfcmVmZXJlbmNlIjoiIiwic291cmNlIjoiaW50ZXJuYWwiLCJuYW1lIjoiTmFub3NvZnQgRG9vcnMiLCJwb3N0X3VybCI6IiIsImRlc2NyaXB0aW9uIjoiRGVza3RvcCBvcGVyYXRpb24gc3lzdGVtIiwic3RhdHVzIjoiYWN0aXZlIiwicmVxdWlyZV9ub25fZXhwaXJlZCI6MSwiY3JlYXRlZF9hdCI6IjIwMjQtMDItMjRUMjA6NTM6NDEuMDAwMDAwWiIsInVwZGF0ZWRfYXQiOiIyMDI0LTAyLTI0VDIwOjUzOjQxLjAwMDAwMFoiLCJtZXRhX2RhdGEiOltdfV0sInRpbWVzdGFtcCI6MTcwOTUzNDQwMH0=",
  "private_key_used": "global",
  "signature": "UtcMnR8u/IuJs8Icn13L/g8ABS5pwn2mxGwJ32+8vJ8CxNhYciK2CU+eD46KvC9AE1dvCdEZTGozWQVyILvlSRtzru6oqb7jzHr6VusDEn4EFtdYuZAGXcGZ1LZRwSxnBHvLAmRDG9uvpJbbIc6gVsQCW9GR+8EMKzx0V2M6JZCzg2H3X0K49vi+w+HkMvS+ecPi2B+C3BQv1jBoD0bU5sQbFO9fyfKDDOp0eoI6UI6jIgOcaRc0EjKvbdSKxt0+sIRummEyds/VJbhZqb9XFEN3yy79c4u3IxiLxebmdq1IW02v2YXp2iVraa3eZVuqSvYSgRIAc/H2ltbrjq/QaA=="
}
```
