---
title: JavaScript SDK
description: Official JavaScript/Node.js SDK for the License Management Platform.
---

# JavaScript SDK

The official JavaScript/Node.js SDK provides a modern, promise-based interface for managing licenses in both browser and server-side environments.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/javascript-sdk](https://github.com/getkeymanager/javascript-sdk)

---

## 🚀 Features

- **Platform Agnostic**: Works in Node.js, Browsers, and Edge environments.
- **Modern Syntax**: Clean, ES6+ promise-based API.
- **TypeScript Support**: Full type definitions included.
- **Offline Validation**: Support for signed offline license files.
- **Telemetry**: Built-in support for usage tracking and piracy detection.

---

## 📦 Installation

```bash
npm install @getkeymanager/js-sdk
```

---

## 🛠️ Usage Example

```javascript
import { LicenseClient } from '@getkeymanager/js-sdk';

const client = new LicenseClient({
  apiKey: 'your-api-key',
  verifySignatures: true,
  publicKey: '...'
});

const result = await client.validateLicense('XXXXX-XXXXX-XXXXX-XXXXX');

if (result.success) {
  console.log('License valid:', result.data.status);
}
```

---

## 🆕 New in v2.0

- **State-Based Core**: Intelligent state resolver and store.
- **Comprehensive API**: Methods for managing products, contracts, and generators.
- **Enhanced Security**: Hardened signature verification logic.
