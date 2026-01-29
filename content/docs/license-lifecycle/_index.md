---
title: License Lifecycle & State Machine
weight: 30
---

![License Lifecycle Placeholder Image](placeholder-offline-license.png)

## Purpose & Scope
Defines license states, allowed and forbidden transitions, preconditions, postconditions, side-effects, and explainability rules. Applies to Admin Dashboard, API, Client Portal, offline validation, and SDKs.

## License States
A license key is always in one of these states:
- available
- assigned
- active
- suspended
- expired
- revoked
