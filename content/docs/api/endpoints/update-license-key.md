---
title: Update License Key
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/update-license-key`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `9cc2cc83-4c74-49f9-98f5-f0e1c1eb1541` |
| `product_id` | text | Yes | Required; Product ID | `1` |
| `owner_name` | text | Yes | Optional; Owner name | `Test Userx` |
| `owner_email` | text | Yes | Optional; Owner email | `email@domain.ltd` |
| `activation_limit` | text | Yes | Required; Activation limit | `0` |
| `validity` | text | Yes | Required; Validity in number of days | `0` |
| `status` | text | Yes | Required; Status, can be 'available', 'assigned', 'reserved', and 'blocked' | `assigned` |
| `assigned_at` | text | Yes | Optional; Assigned at date will be used to calculate the expiration date | `2024-01-08 21:17:32` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### License keys updated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 950,
    "message": "License keys updated",
    "timestamp": 1709001862
  },
  "response_base64": "eyJjb2RlIjo5NTAsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleXMgdXBkYXRlZCIsInRpbWVzdGFtcCI6MTcwOTAwMTg2Mn0=",
  "private_key_used": "product",
  "signature": "D0sIFnnZk2mdTDrX4FXpkK5F15RPJH0atOP3aOSi2cSF2H4KJ+EFl1PXzKJLzXwl6i3svQMQ+w7zeZCcS8diJW1JUxMj6fnD17+maza6eH1+4sBq9/TOW6nQLYvpmkEXWr265hGKh6gPAiLX+SZLKWDhwZEoR9ZaoI7UV6RJSodSTqZtNoeYpOT3Nlgbovb1zrPZoeCzOJ0Vao/bexV6v1DhcHuohTXiZt6YBeKxSNPLgmf3uvXYgW0ROhpsG22QlCdbJRqbBVBSQtESynMxMX6dm9VVSWpF7X7eUY3Zmb3jU6SdQI4RLmnIN4YJ2oQZ9lB1e9gHfvaxK/yVzmLwtQ=="
}
```
