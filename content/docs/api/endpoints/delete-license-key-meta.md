---
title: Delete License Key Meta
weight: 10
---

# Delete License Key Meta

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/delete-license-key-meta`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `3a343c8a-38fe-4b6e-ad77-2222222` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |
| `key` | text | Yes | Required; Meta key | `test-key` |

## Response Examples

This endpoint has **1** documented response example(s) in the Postman collection.

#### Metadata deleted

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 252,
    "message": "Metadata deleted",
    "timestamp": 1709003557
  },
  "response_base64": "eyJjb2RlIjoyNTIsIm1lc3NhZ2UiOiJNZXRhZGF0YSBkZWxldGVkIiwidGltZXN0YW1wIjoxNzA5MDAzNTU3fQ==",
  "private_key_used": "product",
  "signature": "o9rAZGNksnMEnVYW8VRxYqRVm9JX9UbKuHkyTexZgH7ow2AovRkcM3XbVZe/9LwvZWn8spaY9eGmhmzLNegfdI9m89LDpXRbFPLl3p+0CBtAMlQv9ktYsL3VwgKAoEdKpAHH3ITZBVRMIEvwiezMrnIou935QlLLHENB0CEEj/NoxVuan/w5tdunCG6qup6ZpKhMZEWLm1gdAIqFZW1cOp0IY4q6220I/w5nRg0IU79jFot9C9dIQwkg7+nE1rAW6wUML7qGW29UmDGKCW1bPdmd0HltCQC5BIzTBJeYNuRV2O2vc2ryPewJqSVhLgGEDlH9CXwI3pPrICKfpAG/Kw=="
}
```
