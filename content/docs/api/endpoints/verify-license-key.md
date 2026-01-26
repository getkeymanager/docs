---
title: Verify  License Key
weight: 10
---



## Description

Verify license key

## Endpoint Details

- **Method:** `POST`
- **Path:** `/api/v1/verify`
- **Authentication:** API Key (required)

## Request Headers

None specified in Postman

## Request Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| `api_key` | text | Yes | Required; API Key | `2964c3c9-0b5d-4d89-b3ac-4668f30bc492` |
| `license_key` | text | Yes | Required; License key | `19d4c2a0-b2ee-47a9-9fa7-f8befcc142fd` |
| `identifier` | text | Yes | Required; Identifier | `domain.ltd` |
| `email` | text | Yes | Optional; Owner email; Only saved during Envato purchase code verification, when the purchase code is added to the license manager. | `email@domain.ltd` |

## Response Examples

This endpoint has **2** documented response example(s) in the Postman collection.

#### Invalid license key

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 210,
    "message": "Invalid license key",
    "timestamp": 1708999231
  },
  "response_base64": "eyJjb2RlIjoyMTAsIm1lc3NhZ2UiOiJJbnZhbGlkIGxpY2Vuc2Uga2V5IiwidGltZXN0YW1wIjoxNzA4OTk5MjMxfQ==",
  "private_key_used": "global",
  "signature": "eo8EcwVf2KsWknLXk9/ZYzoIfjmXEy6qJb1r4dAWHFtnWzeImQqEJ+7fHaFIDMy4OVF1Sr6vXtY9uH6fLZVL2cObFTM13VGmZ0QU/9yI0mAs74dUHChPhxgxRw+d55POmt6PeWdmRUzkwfj6YMp//TcNFsSQt+CboDoJiezMCSVQ+np0CGlinOlomUnzY9B7fCN9LM4jfAUFJwYutb5QkVs7/yEf/Y5ZbmnBfgQFnFE4xtmeODUjlJUp3KQ1wezaeS3sPSItTzlK//dEE799Ghcf3g/43TBzqoQjyyxbfETXxSLcYtyL+HznNwQ1djcVMPJbQ7ynvdbbuAp1kD3Fow=="
}
```

#### This license key is not assigned

**HTTP Status:** `200 OK`

**Response Body:**
```json
{
  "response": {
    "code": 201,
    "message": "This license key is not assigned",
    "timestamp": 1708999259
  },
  "response_base64": "eyJjb2RlIjoyMDEsIm1lc3NhZ2UiOiJUaGlzIGxpY2Vuc2Uga2V5IGlzIG5vdCBhc3NpZ25lZCIsInRpbWVzdGFtcCI6MTcwODk5OTI1OX0=",
  "private_key_used": "product",
  "signature": "Lzsf3r2mEuntdvWIJXLjuCXVk5Dvz9wjfd0ryfBOuETLOc1iLqWit9xuer21BNF/ffGnyEeS3GfYHRuWExYQGj4NbLvhOfny2QLuf1caxraYStz3UvN7UFF0FU/oVsjDtdeW1atuALcfi16M5VwdekysqubYPxsfbbnZbx5aJMYqmwqQT1lpZh6E3+rKBaYeotWfOGezMC7GP7tEciqdJaREsF9hbqatlIFs9dkZqOAc0ioPR8tEHUOyFA0q6Cgmj3beWWaqln51B2rWD6i9UGFbd3Gltc5/EA32+EeFbk8oQzU/JKD0xxC0NPdC4XoEoQ6z5qTH2xb+Lq45U3ho9A=="
}
```
