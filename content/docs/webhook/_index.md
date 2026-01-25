# Webhook Integration Guide

![Webhook Placeholder Image](PLACEHOLDER_FOR_IMAGE)

## Overview
Webhooks allow you to receive real-time notifications for key events. The system sends POST requests to your configured URL(s) with event details.

## Supported Events
- License: created, updated, deleted, assigned, activated, deactivated, suspended, expired, revoked
- Activation: created, deleted, failed
- Product: created, updated, deleted
- Contract: created, updated, deleted, suspended

## Configuration
1. Go to Admin Portal > Webhooks
2. Create webhook: name, URL, environment, events, description, secret
3. Save and manage webhooks

## Payload Format
Each webhook POST request contains event details.
