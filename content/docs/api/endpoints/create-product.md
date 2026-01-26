---
title: Create Product
weight: 10
---

# Create Product

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/create-product`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `source` | text | Yes | Required; Product source, can be 'internal' or 'envato' | `internal` |
| `name` | text | Yes | Required; Product name | `API Create Product` |
| `description` | text | Yes | Required; Product description | `API create product` |
| `require_non_expired` | text | Yes | Required; Boolean, can be 1 or 0 | `1` |
| `external_reference` | text | Yes | Optional; External refrence (item ID for Envato products) | `` |
| `status` | text | Yes | Required; Product status, can be 'active' or 'inactive' | `active` |

## Response Examples

This endpoint has **3** documented response example(s) in the Postman collection.

#### Product created

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 750,
    "message": "Product created",
    "product_id": 5,
    "timestamp": 1709002824
  },
  "response_base64": "eyJjb2RlIjo3NTAsIm1lc3NhZ2UiOiJQcm9kdWN0IGNyZWF0ZWQiLCJwcm9kdWN0X2lkIjo1LCJ0aW1lc3RhbXAiOjE3MDkwMDI4MjR9",
  "private_key_used": "global",
  "signature": "QHZ5RTDuJz/MmbDNk9iPYdBc8r5LN4YO8rE1u67Ntm9voWGThuHBLOXxjLwdJB9mk1K3X/u4pR9OhfyJG3cmkQX0n0yMieI31M7YE3gfllxsW75bFWh6AYYK6JB2F5hfUrXKL98gfR7HrXc0NFy1P0GVylZUCzoAbi5ngApsKwLgrkvI4xocedQZTF8+sQ8BHWVX2iQs2x/hLZjlHquntQogDKts39+LPN+7PyWAaJm2feA9aaZ7qJHbp+8nCy/wgslNR+bbc03e0Fr/I++WQYHL2omudTwXXEOTI27DO7tGOUjSEbyPqmSQ49xVUqn6XuYwKmRr4+gdaY1Ri4JfEg=="
}
```

#### Incorrect data found

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 751,
    "message": "Incorrect data found",
    "errors": {
      "name": [
        "The name field is required."
      ],
      "description": [
        "The description field is required."
      ]
    },
    "timestamp": 1709002872
  },
  "response_base64": "eyJjb2RlIjo3NTEsIm1lc3NhZ2UiOiJJbmNvcnJlY3QgZGF0YSBmb3VuZCIsImVycm9ycyI6eyJuYW1lIjpbIlRoZSBuYW1lIGZpZWxkIGlzIHJlcXVpcmVkLiJdLCJkZXNjcmlwdGlvbiI6WyJUaGUgZGVzY3JpcHRpb24gZmllbGQgaXMgcmVxdWlyZWQuIl19LCJ0aW1lc3RhbXAiOjE3MDkwMDI4NzJ9",
  "private_key_used": "global",
  "signature": "WTUPPM1casI4QV6lJLa0Q6ldWBKcrsAysk8IhGSpBYVxkyK6CviinogWmy7irTq/CbA+F/SmtcVvTZnGSVLw3ZeQgOf1+hLXLEm6TQnXEv5vqM55fuZ0xnF4ciV5YCvbontdvAsOEOQ92BXdI3PMTTeOTrxLK85ThmJHpkrvVreQeQrpAuS9VWlyd53ZVO2e0FRwm/qgA58e7mURB04EGLzqSAYYLIKjABrXoHDr4AoKY2kQnnNQxBq6aPkjfvZC3vQfPGYYTy2hsHJdZslCNyxanO9y99H9nXSs1HpMZHh+PXLXvvvkb5suDFX4TdwxiExFPLjdJWmNCYDnI1ZizA=="
}
```

#### Invalid status

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 751,
    "message": "Incorrect data found",
    "errors": {
      "status": [
        "The selected status is invalid."
      ]
    },
    "timestamp": 1709002932
  },
  "response_base64": "eyJjb2RlIjo3NTEsIm1lc3NhZ2UiOiJJbmNvcnJlY3QgZGF0YSBmb3VuZCIsImVycm9ycyI6eyJzdGF0dXMiOlsiVGhlIHNlbGVjdGVkIHN0YXR1cyBpcyBpbnZhbGlkLiJdfSwidGltZXN0YW1wIjoxNzA5MDAyOTMyfQ==",
  "private_key_used": "global",
  "signature": "sIi9cErGHOJIONdETgwDtdPdufYKZuDLqNiuav8Z1yWiJP70df/ezFajFIk40eAusaUR4yY8NcO3o1J5DG9WGdDJc5Tf18u3KLH0hu5Sos0wfDj9VfQtYBbYzUPhGzdjZYyLxN1VjIBZbzdhWetJZeIlg/n/ECdhElnR8RmLrFMaetx7v64y6GPQiPsR3SFHMxtxe2aNOzi9BW8XoWEbujNsqfO8kZlqvQTrc9ysU+ce1QgJeK0iVcyYZ+wnuyFtnWiwOsfGkuaqQIYdEpWmCvctSorXnghNd8UCpvv1LYCXERuWJm/BZzjJDPChicvb3f/5io6sIbY4iP5x7T3hLw=="
}
```
