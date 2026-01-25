---
title: "Get Telemetry Data Endpoint"
description: "API documentation for /api/v1/get-telemetry-data endpoint."
---

# GET /api/v1/get-telemetry-data

Retrieves telemetry data records for analysis and monitoring.

## Request
- **Method:** GET
- **URL:** `/api/v1/get-telemetry-data`
- **Content-Type:** `application/json`

### Query Parameters
| Name                   | Type   | Required | Description                                                                 |
|------------------------|--------|----------|-----------------------------------------------------------------------------|
| api_key                | string | Yes      | API Key                                                                    |
| data_type              | string | Yes      | Data type: 'numeric-xy-axis', 'numeric-single-value', 'text'               |
| data_group             | string | Yes      | Key used to group records together                                         |
| product_id             | string | Optional | Product ID                                                                 |
| user_identifier        | string | Optional | Unique string to identify the software user                                 |
| license_key            | string | Optional | License key                                                                |
| activation_identifier  | string | Optional | Activation identifier                                                      |
| product_version        | string | Optional | Product version                                                            |
| license_key_exists     | string | Optional | License key exists (1/0)                                                   |
| product_exists         | string | Optional | Product exists (1/0)                                                       |
| product_version_exists | string | Optional | Product version exists (1/0)                                               |
| is_correct_format      | string | Optional | Is correct format (1/0)                                                    |
| has_red_flags          | string | Optional | Has red flags (1/0)                                                        |

## Responses

### 200 OK
- **Get Telemetry Data Example**
  - Returns telemetry data records matching the query.

#### Example Response
```json
{
  "response": {
    "code": 200,
    "message": "Success",
    "data": [/* telemetry records */],
    "timestamp": 1708999140
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See Send Telemetry Data for data submission.