# Get Telemetry Endpoint

**Endpoint:** `GET /api/v1/get-telemetry`

Retrieves telemetry data for a product or license key. The `has_red_flags` option allows you to retrieve records with any red flags without specifying particular ones.

---

## Request

- **Method:** GET
- **URL:** `/api/v1/get-telemetry`
- **Headers:**
  - `Accept: application/json`
- **Query Parameters:**

| Parameter      | Type   | Required | Description                              |
|---------------|--------|----------|------------------------------------------|
| api_key       | string | Yes      | API Key                                  |
| license_key   | string | No       | License key                              |
| has_red_flags | bool   | No       | Retrieve records with any red flags       |

**Example Request:**

```
curl -X GET "https://getKeyManager.local/api/v1/get-telemetry?api_key=2964c3c9-0b5d-4d89-b3ac-4668f30bc492&license_key=65a90cff-8da2-4820-9c9a-a13a041891fd&has_red_flags=true" \
  -H "Accept: application/json"
```

---

## Responses

### 200 OK — Telemetry data retrieved

```
{
    "response": {
        "code": 900,
        "message": "Telemetry data retrieved",
        "data": [
            // ... telemetry records ...
        ],
        "timestamp": 1708999000
    },
    "response_base64": "...",
    "private_key_used": "global",
    "signature": "..."
}
```

---

## Error Codes

| Code | Message                                 |
|------|-----------------------------------------|
| 900  | Telemetry data retrieved                |
| 901  | Invalid API key                         |
| 902  | No telemetry data found                 |

---

## Notes
- The `has_red_flags` parameter is optional and can be used to filter for records with red flags.
- The response includes a digital signature and base64-encoded response for verification.
