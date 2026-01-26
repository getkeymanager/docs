---
title: Deactivate  License Key
weight: 10
---



## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/deactivate`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `9cc2cc83-4c74-49f9-98f5-f0e1c1eb1541` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### License key deactivated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": "400",
    "message": "License key deactivated",
    "timestamp": 1709000040
  },
  "response_base64": "eyJjb2RlIjoiNDAwIiwibWVzc2FnZSI6IkxpY2Vuc2Uga2V5IGRlYWN0aXZhdGVkIiwidGltZXN0YW1wIjoxNzA5MDAwMDQwfQ==",
  "private_key_used": "global",
  "signature": "dCZV/qUWm1gmo/2w9moIuY7DpIApgO1c77NqKD3Ns9MBoyNr/Jce+QpADfv+eR+zkP0Ak++HzgNyfdrhmupWs8bmmMElkZj0XL9tnhZ2b9ZmdU7Zn4CAkqclkCAC3IDQCPZClVzbW7i8w+6yRUv03UimKlbSO/7T3iSv66aJz06m7qvw50oHPZAQDXu7vETjxJigw5X1L4/VxP1fcq7MiCY6dFOCj18J8in58FEbM6/ycKf+JTbjvVXQO4yEqPP/YoE3csfsQ6kez5hsQ2zlFY2J214st+MQMwchRdGiqbAVAN8Cjr/mPxhr530/ORyPxz9LgJV5Z33paybTSoQ8ZA=="
}
```

#### License key already inactive

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 401,
    "message": "License key already inactive",
    "timestamp": 1709000060
  },
  "response_base64": "eyJjb2RlIjo0MDEsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleSBhbHJlYWR5IGluYWN0aXZlIiwidGltZXN0YW1wIjoxNzA5MDAwMDYwfQ==",
  "private_key_used": "product",
  "signature": "BWeEo4YmC5/w3oigJsUZCgH80wxcF4rv9lHf7v9pK8jxkYMeDRgplkKuY4JbNKU9ghAVKLcjUi6PUB77L3iYeL3uNqa5MZj+j4KsYqhsgoK7zptD7i7BfO5RuBoAvY0H8g1csCR9B9Ur70C+qydSne/B6I3CVrHHWFQiamusSLwtglIIMqUBK479IvMqlvoSE2JM9zXSnS6nwDR1pM36qE3poxyzGVvn6NzgLKS/1TAtow8+ErDBrQAr7FA4BwN0FWps5AiNhzWTBUAsV3Nwi4E+m3Ur6eTutfe50wEgoiXCwpBcznbmqZ4pDg80lKOrYyTos4wBN2aKlsC+uXc/Kg=="
}
```
