
# API Developer Guide

## Introduction
This guide describes all public APIs, request/response formats, security rules, and response codes for the License Management Platform. The API is deterministic, cryptographically verifiable, offline-friendly, idempotent, and backward compatible.

## API Fundamentals
- All APIs are versioned: `/api/v1/*`
- Breaking changes only in new versions

## Authentication & Authorization
- All API requests require an API key
- Use header: `Authorization: Bearer {API_KEY}`

## API Endpoints Documentation


## API Endpoint Documentation Status

| Endpoint Name                                 | File Link                                         | Status  |
|-----------------------------------------------|---------------------------------------------------|---------|
| Verify Endpoint                              | [verify.md](verify.md)                            | Done    |
| Send Telemetry Data Endpoint                  | [send-telemetry-data.md](send-telemetry-data.md)  | Done    |
| Get Telemetry Data Endpoint                   | [get-telemetry-data.md](get-telemetry-data.md)    | Done    |
| Activate License Key Endpoint                 | [activate.md](activate.md)                        | Done    |
| Verify License Key Endpoint                   | [verify-license-key.md](verify-license-key.md)     | Done    |
| Assign License Key Endpoint                   | [assign-license-key.md](assign-license-key.md)     | Done    |
| Assign and Activate License Key Endpoint      | [assign-and-activate-license-key.md](assign-and-activate-license-key.md) | Done |
| Random Assign License Keys Endpoint           | [random-assign-license-keys.md](random-assign-license-keys.md) | Done |
| Get Telemetry Endpoint                       | [get-telemetry.md](get-telemetry.md)              | Done    |
| Random Assign License Keys Queued Endpoint    | [random-assign-license-keys-queued.md](random-assign-license-keys-queued.md) | Done |
| Deactivate License Key Endpoint               | [deactivate.md](deactivate.md)                    | Done    |
| Access Restrictions                          | [access-restrictions.md](access-restrictions.md)  | Done    |

**Legend:**
- **Done**: Documentation file exists and is referenced here.
- **Pending**: Documentation file missing or incomplete (add row if new endpoint is found).

Each endpoint document includes request/response formats, required parameters, and example responses.
