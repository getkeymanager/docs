---
title: API Keys
weight: 100
---

# API Keys

The API Keys page is the control center for programmatic access to the platform. It allows administrators to generate, manage, and secure the credentials used by external applications, scripts, and integrations.

---

## What Is This Page?

API Keys provide a secure way to authenticate requests to the platform's public API without requiring a username or password. Each key is tightly controlled through environment scoping, granular permissions, and rate limiting to ensure that automation remains secure and predictable.

---

## Key Features

### 1. Environment Scoping
API Keys are strictly bound to one of the following environments:
- **Production**: Active for real-world operations.
- **Staging**: Used for testing integrations with realistic data.
- **Development**: Isolated environment for initial coding and experimentation.
*Cross-environment access is strictly forbidden by the platform core.*

### 2. Granular Permissions
Each key can be assigned a specific set of permissions. You can see a summary of these permissions (e.g., `License Management`, `Customer Read`, `Telemetry Write`) directly in the main list. This follows the principle of least privilege—only granting the exact access needed for a specific integration.

### 3. Lifecycle Management
- **Status Monitoring**: Instantly see if a key is `Active`, `Inactive`, or `Expired`.
- **Last Used Tracking**: Monitor exactly when a key was last used to identify orphaned or underutilized integrations.
- **Revocation**: If a key is compromised or no longer needed, it can be revoked immediately, cutting off all future access without deleting the historical data associated with it.

---

## Using API Keys

### Generating a New Key
1. Click **Create API Key**.
2. Give the key a descriptive **Name** (e.g., "Main Website Integration").
3. Select the **Environment**.
4. Configure **Permissions** and **Rate Limits**.
5. **CRITICAL**: Copy your API key immediately. For security reasons, the full key is only displayed once.

### Rotation & Security
If a key is accidentally exposed or needs to be rotated as part of a security policy:
- **Regenerate**: This action generates a new random string while keeping the same name, permissions, and configuration. The old key will stop working immediately.
- **Revoke**: Use this to temporarily disable a key without deleting it.

---

## Troubleshooting

- **401 Unauthorized**: 
    - Verify that the key is **Active** and hasn't **Expired**.
    - Ensure the key is being used against the correct environment endpoint (e.g., using a "Staging" key on the "Production" API will fail).
- **429 Too Many Requests**: Check the **Rate Limits** column. If your integration is hitting limits, you may need to increase the threshold in the key's settings.
- **Permission Denied (403)**: Ensure the key has the specific permission required for the endpoint you are calling. You can verify active permissions in the "Permissions" column.

---

## Related Pages

- [Logs](../logs) - View detailed API request/response logs.
- [Background Jobs](../background-jobs) - Monitor jobs triggered via the API.
- [Customers](../customers) - API keys can be scoped to specific customers for restricted access.
