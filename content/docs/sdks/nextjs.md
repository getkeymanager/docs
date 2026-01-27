---
title: Next.js SDK
description: Official Next.js SDK for the License Management Platform.
---



The official Next.js SDK combined the best of our React hooks and Node.js capabilities to provide a seamless licensing experience for modern web applications.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/nextjs-sdk](https://github.com/getkeymanager/nextjs-sdk)

---

## 🚀 Features

- **Server Components**: Validate licenses directly in Next.js Server Components.
- **API Handler Protection**: Middleware and utilities for API route security.
- **Client Hooks**: Sharing state between client and server effortlessly.
- **Edge Compatible**: Optimized for Next.js Edge Runtime.
- **Full TypeScript**: Comprehensive typing for the whole Next.js lifecycle.

---

## 📦 Installation

```bash
npm install @getkeymanager/nextjs-sdk
```

---

## 🛠️ Usage Example

### Server Component

```typescript
import { getServerLicenseClient } from '@getkeymanager/nextjs-sdk/server';

export default async function Page() {
  const client = getServerLicenseClient();
  const state = await client.resolveLicenseState('XXXXX-XXXXX');

  if (!state.isActive()) {
    return <Unauthorized />;
  }

  return <SecureData />;
}
```

---

## 🆕 New in v2.0

- **Server-Side Hardening**: Intelligent caching with TTL for server environments.
- **Grace Period Support**: 72-hour failover for server-side validation.
- **Middleware Utilities**: Protect entire directory structures with one line of code.
