---
title: Update Product Meta
weight: 10
---

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/update-product-meta`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `product_id` | text | Yes | Required; Product ID | `4` |
| `key` | text | Yes | Required; Meta key | `test-key` |
| `value` | text | Yes | Required; Meta value | `test value` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Meta key doesn't exists

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 372,
    "message": "Meta key doesn't exists",
    "timestamp": 1709169540
  },
  "response_base64": "eyJjb2RlIjozNzIsIm1lc3NhZ2UiOiJNZXRhIGtleSBkb2Vzbid0IGV4aXN0cyIsInRpbWVzdGFtcCI6MTcwOTE2OTU0MH0=",
  "private_key_used": "product",
  "signature": "GefKGxKeaHKzzGMy/NyWjUOjtpFRUm1g0/YserPZrUb30Wuo+PhAyKwSTpDtfee4d3aro71cw/fY+iiIS21/PFHzJ8NwFlW/ahqIQjvSUIvAYGvESIUapf95+VFCuKcXpG+ywe23fwndZbSWyj7BVLnxWwixNxZXGk72jWY3364r+v428ugyFTKZU7pxerjojx98M47polVwQhXePCeyybdzvSfIUDLISYAgzOuXZ2vOVTynKOXmKJbMvpXypIex8irnT/KtNafkGGlVQGXaVSvB82ebOzaGi0KpYyh/cJ1f7jYUPVA6XcA/7vgPfSgiQcqmvlRqrPvSBDntHnJysQ=="
}
```

#### Product meta updated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 373,
    "message": "Product meta updated",
    "timestamp": 1709169556
  },
  "response_base64": "eyJjb2RlIjozNzMsIm1lc3NhZ2UiOiJQcm9kdWN0IG1ldGEgdXBkYXRlZCIsInRpbWVzdGFtcCI6MTcwOTE2OTU1Nn0=",
  "private_key_used": "product",
  "signature": "c3HsM9fpprScfNPJPyqm3c3gLDzF87m64+m5fPoRIwXPpHqWHK/v6wpeEXZkeNRmsWSHJNKVVsCGKsl2NfQvBSk8MaWn1F5OPe1Nekn44vpbinFNGpBiuOjcfUcKnI5vYomliM03cPXH7fTp8UUMkAVY2a4+cESGa/8El7lVW+pAPMsa5sk0LEXpFzezEOTYwFvxqc62OtT1FCozpklHQT6O2oHcSBWBwAZG1QBfltqBy/YWDWueeaXHeyEEm173AfippzZDTMlSJKkeX+HGcCxbY6aoPDefZyF3KeYudJDVtHsUS9IJ4mbvNMY7bVLoA5H9lGYPw1K4SGIWx1Oxvg=="
}
```
