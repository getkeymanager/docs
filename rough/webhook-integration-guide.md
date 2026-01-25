# Webhook Integration Guide

This guide explains how to use webhooks in the License Management Platform.

## Overview
Webhooks allow you to receive real-time notifications for key events in your account. When an event occurs, the system sends a POST request to your configured URL(s) with event details.

## Supported Events
You can subscribe to any of the following events:

**License Events**
- license.created
- license.updated
- license.deleted
- license.assigned
- license.activated
- license.deactivated
- license.suspended
- license.expired
- license.revoked

**Activation Events**
- activation.created
- activation.deleted
- activation.failed

**Product Events**
- product.created
- product.updated
- product.deleted

**Contract Events**
- contract.created
- contract.updated
- contract.deleted
- contract.suspended

## How to Configure Webhooks
1. Go to the Admin Portal > Webhooks section.
2. Click "Create Webhook" and fill in:
   - Name
   - URL (where notifications will be sent)
   - Environment (production, staging, development)
   - Events to subscribe to
   - Description (optional)
   - Secret (auto-generated)
3. Save the webhook. You can edit or disable it anytime.

## Payload Format
Each webhook POST request contains:
```json
{
  "event": "event.name",
  "payload": { ... },
  "webhook_id": "webhook-uuid"
}
```
- `event`: The event name (e.g., license.created)
- `payload`: The event data (varies by event)
- `webhook_id`: The UUID of your webhook

## Security
- Each webhook includes a secret for verification.
- Use HTTPS for your endpoint.
- Validate the secret and event name in your handler.

## Retry & Delivery
- Only active webhooks receive events.
- Delivery is attempted once per event.
- Failed deliveries are logged.

## Example Handler
```php
// Example: Laravel controller
public function handleWebhook(Request $request) {
    $event = $request->input('event');
    $payload = $request->input('payload');
    $webhookId = $request->input('webhook_id');
    // Validate and process
}
```

## Troubleshooting
- Check your endpoint logs for incoming requests.
- Ensure your endpoint responds with HTTP 200.
- Use the Admin Portal to view webhook logs and status.

## Audit & Governance
- All webhook deliveries are logged and auditable.
- Only permitted events and environments are delivered.

For more details, see the Admin Portal or contact support.
