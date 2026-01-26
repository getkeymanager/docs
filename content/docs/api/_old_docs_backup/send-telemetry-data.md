---
title: "Send Telemetry Data Endpoint"
description: "API documentation for /api/v1/send-telemetry-data endpoint."
---

# POST /api/v1/send-telemetry-data

Sends telemetry data from your software to the platform for analysis and monitoring.

## Request
- **Method:** POST
- **URL:** `/api/v1/send-telemetry-data`
- **Content-Type:** `application/x-www-form-urlencoded`

### Parameters
| Name                   | Type   | Required | Description                                                                 |
|------------------------|--------|----------|-----------------------------------------------------------------------------|
| api_key                | string | Yes      | API Key                                                                    |
| data_type              | string | Yes      | Data type: 'numeric-xy-axis', 'numeric-single-value', 'text'               |
| numeric_data_single_value | string | Cond. | Required if data_type is 'numeric-single-value'                             |
| numeric_data_x         | string | Cond.    | Required if data_type is 'numeric-xy-axis'                                 |
| numeric_data_y         | string | Cond.    | Required if data_type is 'numeric-xy-axis'                                 |
| text_data              | string | Cond.    | Required if data_type is 'text'                                            |
| product_id             | string | Optional | Product ID                                                                 |
| user_identifier        | string | Optional | Unique string to identify the software user                                 |
| license_key            | string | Optional | License key                                                                |
| activation_identifier  | string | Optional | Activation identifier                                                      |
| product_version        | string | Optional | Product version                                                            |
| data_group             | string | Yes      | Key used to group records together                                         |

## Responses

### 200 OK
- **Correct format data saved**
  - Code: 830
  - Message: "Correct format data saved"
- **Incorrect format data saved - With Errors**
  - Code: 831
  - Message: "Incorrect format data saved"
  - Errors: Field-specific validation errors

#### Example Success Response
```json
{
  "response": {
    "code": 830,
    "message": "Correct format data saved",
    "errors": [],
    "timestamp": 1708999140
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

#### Example Error Response
```json
{
  "response": {
    "code": 831,
    "message": "Incorrect format data saved",
    "errors": {
      "product_id": ["The selected product id is invalid."],
      "user_identifier": ["The user identifier field is required."],
      "license_key": ["The license key field is required."],
      "activation_identifier": ["The activation identifier field is required."],
      "product_version": ["The product version field is required."],
      "data_type": ["The data type field is required."],
      "data_group": ["The data group field is required."]
    },
    "timestamp": 1708999057
  },
  "response_base64": "...",
  "private_key_used": "global",
  "signature": "..."
}
```

---

See Get Telemetry Data for retrieval.