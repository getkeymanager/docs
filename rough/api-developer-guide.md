# API Developer Guide  
## License Management Platform – v1.0

---

## 1. Introduction

This document describes **all public APIs**, request/response formats, security rules, and response codes for the License Management Platform.

The API is designed to be:
- Deterministic
- Cryptographically verifiable
- Offline-friendly
- Idempotent
- Backward compatible

This guide is **authoritative**.  
If implementation or SDK behavior differs from this document, the implementation is incorrect.

---

## 2. API Fundamentals

### 2.1 Base URL & Versioning

All APIs are versioned.

```

/api/v1/*

```

Breaking changes will only be introduced in a new version.

---

## 3. Authentication & Authorization

### 3.1 API Keys

All API requests require an API key.

**Header**

```

Authorization: Bearer {API_KEY}

```

### API Key Controls
- Environment scoped (production / staging / development)
- IP allowlisting
- Endpoint-level permission matrix
- Rate-limited

---

## 4. Idempotency (CRITICAL)

Endpoints that mutate state MUST support idempotency.

**Header**

```

Idempotency-Key: <unique-client-generated-key>

````

### Idempotent Operations
- License creation
- Activation
- Assignment
- Random assignment
- Contract generation

**Rule**
> Same Idempotency-Key + same request payload → same response, no duplicate side effects.

---

## 5. API Response Format (Canonical)

All responses follow the same structure.

```json
{
  "response": {
    "code": 300,
    "message": "License key activated",
    "errors": [],
    "data": {},
    "timestamp": 1708999677
  },
  "response_base64": "BASE64_PAYLOAD",
  "private_key_used": "product|global",
  "signature": "RSA_SIGNATURE"
}
````

### Response Guarantees

* Responses are signed (RSA)
* `response.code` is authoritative
* HTTP status may be `200` even for logical errors

---

## 6. Response Codes (Complete Reference)

### 6.1 API Key & Authentication (100–103)

| Code | Meaning                          |
| ---- | -------------------------------- |
| 100  | Invalid API key                  |
| 101  | Inactive API key                 |
| 102  | API key lacks permission         |
| 103  | API key IP restriction violation |

---

### 6.2 Access Restrictions (150)

| Code | Meaning       |
| ---- | ------------- |
| 150  | Access denied |

---

### 6.3 License Verification (200–215)

| Code | Meaning                     |
| ---- | --------------------------- |
| 200  | Valid license key           |
| 201  | License not assigned        |
| 202  | No activation found         |
| 203  | Product inactive or missing |
| 204  | License blocked             |
| 205  | License expired             |
| 206  | Envato purchase code added  |
| 210  | Invalid license key         |
| 215  | Identifier required         |

---

### 6.4 Activation (300–302)

| Code | Meaning                  |
| ---- | ------------------------ |
| 300  | License activated        |
| 301  | License already active   |
| 302  | Activation limit reached |

---

### 6.5 Deactivation (400–401)

| Code | Meaning                  |
| ---- | ------------------------ |
| 400  | License deactivated      |
| 401  | License already inactive |

---

### 6.6 License Details (500)

| Code | Meaning                  |
| ---- | ------------------------ |
| 500  | Active license key found |

---

### 6.7 Downloadables (600–701)

| Code | Meaning             |
| ---- | ------------------- |
| 600  | Downloads available |
| 700  | File not found      |
| 701  | Permission denied   |

---

### 6.8 Assignment & Generation (800–807)

| Code | Meaning                     |
| ---- | --------------------------- |
| 800  | License assigned            |
| 801  | Invalid or already assigned |
| 802  | Insufficient licenses       |
| 803  | Licenses assigned           |
| 805  | Product not found           |
| 806  | Generator not found         |
| 807  | Request queued              |

---

### 6.9 License CRUD (900–952)

| Code | Meaning             |
| ---- | ------------------- |
| 900  | Licenses created    |
| 901  | Incorrect data      |
| 902  | No licenses created |
| 950  | License updated     |
| 951  | Incorrect data      |
| 952  | License not found   |

---

### 6.10 Product CRUD (650–751)

| Code | Meaning           |
| ---- | ----------------- |
| 750  | Product created   |
| 751  | Incorrect data    |
| 650  | Product updated   |
| 651  | Incorrect data    |
| 550  | Product deleted   |
| 551  | Product not found |

---

### 6.11 Metadata APIs (250–483)

Used for both license & product metadata.

Examples:

* 453 → Metadata created
* 353 → Metadata updated
* 252 → Metadata deleted

---

### 6.12 Telemetry (830–970)

| Code | Meaning                |
| ---- | ---------------------- |
| 830  | Correct format saved   |
| 831  | Incorrect format saved |
| 970  | Telemetry data found   |

---

### 6.13 Contracts (1200–1501)

| Code | Meaning                     |
| ---- | --------------------------- |
| 1200 | Contract not found          |
| 1204 | Contract found              |
| 1205 | License limit reached       |
| 1300 | Contract licenses generated |
| 1400 | License deleted             |
| 1500 | Licenses deleted            |

---

## 7. Endpoint Reference

### 7.1 Verify License

**POST**

```
/api/v1/verify
```

**Payload**

```json
{
  "license_key": "XXXX-XXXX-XXXX",
  "identifier": "HWID_OR_DOMAIN",
  "product_uuid": "uuid"
}
```

**Responses**

* `200` Valid
* `202` No activation
* `205` Expired
* `210` Invalid

---

### 7.2 Activate License

**POST**

```
/api/v1/activate
```

**Payload**

```json
{
  "license_key": "XXXX",
  "identifier": "HWID",
  "product_uuid": "uuid"
}
```

**Responses**

* `300` Activated
* `301` Already active
* `302` Limit reached

---

### 7.3 Deactivate License

**POST**

```
/api/v1/deactivate
```

**Payload**

```json
{
  "license_key": "XXXX",
  "identifier": "HWID"
}
```

**Responses**

* `400` Deactivated
* `401` Already inactive

---

### 7.4 Access Downloadables

**GET**

```
/api/v1/access-downloadables
```

Returns signed URLs if allowed.

---

### 7.5 Create Licenses

**POST**

```
/api/v1/create-license-keys
```

Supports bulk creation and idempotency.

---

### 7.6 Assign License

**POST**

```
/api/v1/assign-license-key
```

---

### 7.7 Random Assign Licenses

**POST**

```
/api/v1/random-assign-license-keys
```

May return `807` if queued.

---

### 7.8 Send Telemetry

**POST**

```
/api/v1/send-telemetry-data
```

Malformed data is accepted and flagged.

---

### 7.9 Contracts API

**GET**

```
/api/v1/contracts/get-info
```

**POST**

```
/api/v1/contracts/generate
```

**POST**

```
/api/v1/contracts/destroy
```

---

## 8. Rate Limiting

Applied per:

* API key
* IP
* License key
* Contract

Violations return access-denied responses.

---

## 9. Security Notes

* All responses are signed
* Private keys are never exposed
* Offline behavior mirrors online rules
* UUIDs only for external references

---

## 10. Best Practices

* Always use Idempotency-Key
* Cache verification responses briefly
* Never hard-code license logic
* Handle all response codes explicitly
* Verify signatures in SDKs

---

## 11. Summary

This API enables:

* Secure license verification
* Deterministic activation
* Enterprise automation
* Offline validation
* Reseller workflows

It is designed to be stable, predictable, and auditable.

---

END OF API DEVELOPER GUIDE
