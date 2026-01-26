---
title: Send Telemetry
weight: 10
---

# Send Telemetry

## Description

Your software should consistently send accurate data. Data flagged with red flags is presumed to originate from a tampered or pirated version.

For instance, it's imperative that your software consistently transmits a valid license key within the request. Illegitimate copies often attempt to bypass activation, resulting in requests being sent with invalid license keys.

Data collection requests should not be put behind valid activation logic; the data should be sent regardless of activation status.

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/send-telemetry-data`
- **Authentication:** API Key (required)

## Request Headers

| Header | Value | Description |
|--------|-------|-------------|
| `Accept` | `application/json` | N/A |

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `data_type` | text | Yes | Required; Data type, can be 'numeric-xy-axis', 'numeric-single-value', 'text' | `numeric-single-value` |
| `numeric_data_single_value` | text | Yes | Required if data type is 'numeric-single-value' | `50` |
| `numeric_data_x` | text | No | Required if data type is 'numeric-xy-axis' | `1` |
| `numeric_data_y` | text | No | Required if data type is 'numeric-xy-axis' | `2` |
| `text_data` | text | No | Required if data type is 'text' | `text value` |
| `product_id` | text | Yes | Optional; Product ID | `1` |
| `user_identifier` | text | Yes | Optional; User identifier, a distinctive string designed to identify the present software user, irrespective of their activation location or whether they possess a valid license or not. | `554dddsqfqs4dqd5qsd74q` |
| `license_key` | text | Yes | Optional; License key | `9cc2cc83-4c74-49f9-98f5-f0e1c1eb1541` |
| `activation_identifier` | text | Yes | Optional; Activaton identifier | `12135644` |
| `product_version` | text | Yes | Optional; Product verssion | `1.0.1` |
| `data_group` | text | Yes | Required; Key used to group records together | `test_group` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Incorrect format data saved - With Errors

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 831,
    "message": "Incorrect format data saved",
    "errors": {
      "product_id": [
        "The selected product id is invalid."
      ],
      "user_identifier": [
        "The user identifier field is required."
      ],
      "license_key": [
        "The license key field is required."
      ],
      "activation_identifier": [
        "The activation identifier field is required."
      ],
      "product_version": [
        "The product version field is required."
      ],
      "data_type": [
        "The data type field is required."
      ],
      "data_group": [
        "The data group field is required."
      ]
    },
    "timestamp": 1708999057
  },
  "response_base64": "eyJjb2RlIjo4MzEsIm1lc3NhZ2UiOiJJbmNvcnJlY3QgZm9ybWF0IGRhdGEgc2F2ZWQiLCJlcnJvcnMiOnsicHJvZHVjdF9pZCI6WyJUaGUgc2VsZWN0ZWQgcHJvZHVjdCBpZCBpcyBpbnZhbGlkLiJdLCJ1c2VyX2lkZW50aWZpZXIiOlsiVGhlIHVzZXIgaWRlbnRpZmllciBmaWVsZCBpcyByZXF1aXJlZC4iXSwibGljZW5zZV9rZXkiOlsiVGhlIGxpY2Vuc2Uga2V5IGZpZWxkIGlzIHJlcXVpcmVkLiJdLCJhY3RpdmF0aW9uX2lkZW50aWZpZXIiOlsiVGhlIGFjdGl2YXRpb24gaWRlbnRpZmllciBmaWVsZCBpcyByZXF1aXJlZC4iXSwicHJvZHVjdF92ZXJzaW9uIjpbIlRoZSBwcm9kdWN0IHZlcnNpb24gZmllbGQgaXMgcmVxdWlyZWQuIl0sImRhdGFfdHlwZSI6WyJUaGUgZGF0YSB0eXBlIGZpZWxkIGlzIHJlcXVpcmVkLiJdLCJkYXRhX2dyb3VwIjpbIlRoZSBkYXRhIGdyb3VwIGZpZWxkIGlzIHJlcXVpcmVkLiJdfSwidGltZXN0YW1wIjoxNzA4OTk5MDU3fQ==",
  "private_key_used": "global",
  "signature": "FwhAVWpM2X0u2bGKZrcqfGmhgW4phpMYZm/c8MVFZZjrbJJpHHKn7HxiYKGykmE13K8Qe0y8HD/X8YTs6gnGTjTS+raKH7q58Cv7jjR61Jc9nuja5fgI8UMrY11AwTmgjFcchQgBdmxqaLCuQzAEUaPxpWtk5OQb4MBUFR9DMHzC82uqTTgkOBurzlLotLgTOvz0x7wSgGpC46oXHvy29hRdm46SagKAIjk46COd3JOn6cL/Us+JTKYPn5Upi6HV1sj/kTS/k1eOyd8fttnQEjXIAZxHfWBj5KqnKpC0IrnqJfpSZkLGDUPAqcyLlFAvoJfs4WCTKiCWNr9hhPEw8g=="
}
```

#### Correct format data saved

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 830,
    "message": "Correct format data saved",
    "errors": [],
    "timestamp": 1708999140
  },
  "response_base64": "eyJjb2RlIjo4MzAsIm1lc3NhZ2UiOiJDb3JyZWN0IGZvcm1hdCBkYXRhIHNhdmVkIiwiZXJyb3JzIjpbXSwidGltZXN0YW1wIjoxNzA4OTk5MTQwfQ==",
  "private_key_used": "global",
  "signature": "KdJsqHq3QQj7ekAd9+BOr8GI63Y/YAqo80qCZrAnuVaynpgPepvEsiQCAGxNAnyJESu7teLisvO+ts5Mu3q+9CMqtGYyxW6vOHLbpwU0eXWaqUUsHhLk2ZYFqd6kt0bBGyo4a09+58B4Z3zYI3nMqURaEHLbQON2z+J5KEjNkwPNxdq7AmJ9G3rSpeylQdykgpxqbuzTA7NLg5o+hnfkw/ssMViPGJ5N9OJ22OoXsj0kpEUWBajdDD/q+U/oG05TdJH8ekvRX2S198JbXyQzFtXFu+faUGTFPUzViUxn+QWwEK7VY7lftx1ZysJ+AyfWX3uCD8J2G+pbOB38pinH5g=="
}
```
