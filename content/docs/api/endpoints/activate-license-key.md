---
title: Activate  License Key
weight: 10
---

# Activate  License Key

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/activate`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `CUSTOM-91536fe6-aabf-4ac1-8a60-627830c718b0` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |
| `post_url` | text | Yes | Optional; Remove deactivation Post URL. | `https://domain.ltd/receiver.php?example-getKeyManager-post-url=test` |

## Response Examples

This endpoint has **3** documented response example(s) in the Postman collection.

#### License key activated

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 300,
    "message": "License key activated",
    "timestamp": 1708999677
  },
  "response_base64": "eyJjb2RlIjozMDAsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleSBhY3RpdmF0ZWQiLCJ0aW1lc3RhbXAiOjE3MDg5OTk2Nzd9",
  "private_key_used": "product",
  "signature": "r0QyfdaaoiK0KD+vdTH6IIVxhpViFg7mb/W8ZmGBzFT6TTPtwoFhY0zNkErW7jDS3F1GDF9fzJh/e96IMF/2ZQdSrmsuER1mXfw6u//J54XtHoiFYM+WEkOlLcqJxLPhWgnhqpwfc3YFSqEidavWjhmopYfrJlEB+6g3RQFKSbB59hVh0Oh2JAPnIgdu1PTsiSeaMa7YLOByaBxhBnCrisG/WBbTHny5IFRZOFhYirpfvN/lfnHaHs/1Atj55qyX9oBFiaJq32AKKxZFHzX82sYFF51zyGMDaLiPnMnAR7DaqdMTh1c7xnxfOWccTtLZbpOzFoWw9YW76FHNPTt6zA=="
}
```

#### License key already active

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 301,
    "message": "License key already active",
    "timestamp": 1708999696
  },
  "response_base64": "eyJjb2RlIjozMDEsIm1lc3NhZ2UiOiJMaWNlbnNlIGtleSBhbHJlYWR5IGFjdGl2ZSIsInRpbWVzdGFtcCI6MTcwODk5OTY5Nn0=",
  "private_key_used": "product",
  "signature": "FAL7Nky9qqs2ipfE8JDtEl2fQ3qj0PBGEb5kTSCdaTgbPG6Y7GpE0AaNoZ5E+O0je/JR/kuBECg5dsisHEl9pp+TNxbwePgRFp/SZWUX+5nlvUVqnr33+nBKOfeX6ZUA73oaojppl4SLuSJV/K3ju8K7QsZT5b0/30z7sulkWQbpCXgU/JRo/lGU6P6kcHryr1Bt86ORyXS8fNXvG1shKCmOOeQt2FjSF7UIMyJ2cj4SwhzGfufB211Y5ZVYQMqG4qTUKRUNUOK2HK7F0kBtRxoOBW2nMUWaBLHeBL4GcllprjdClBVhIRnVjIT3XY6oVJw66+oFkmtdIkxgeOrhOQ=="
}
```

#### Identifier is required

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 215,
    "message": "Identifier is required",
    "timestamp": 1708999711
  },
  "response_base64": "eyJjb2RlIjoyMTUsIm1lc3NhZ2UiOiJJZGVudGlmaWVyIGlzIHJlcXVpcmVkIiwidGltZXN0YW1wIjoxNzA4OTk5NzExfQ==",
  "private_key_used": "product",
  "signature": "jjbpVaoe6z3kuL9UUmq5jzTqKbSIbM0VOmJAjNGmfOnVVcC4cVd4C3zmDwv3H6RSGn1jPZGMeAoroIxJqQvKA3u6hzD3n3Sh+yVki3zQFMvYB6aR6Xdp3rR1mLD+0J2t7nC+xdw2EYb3s+QK4GoZOHAKWPq+5Vx2MbKWVk8ioBN8xLY4WJexZCHgzu84VnoWH2sJiJHJPUJDKbaR53DWfQC2ly9miu9Jy35yF4gl+aVmrOnHx6CPTUlfcVCPtZfRUZCfudx57pAyIxCpoErsqtm2C/gJ5CfU8WR/hiEjqmYrmVNeusCY/vX48VLXUov+yaYTjRy/3+QoWzrcxXDmgg=="
}
```
