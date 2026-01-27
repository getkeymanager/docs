---
title: React SDK
description: Official React SDK for the License Management Platform.
---



The official React SDK provides hooks and utilities for integrating license management directly into your React applications with state-based awareness.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/react-sdk](https://github.com/getkeymanager/react-sdk)

---

## 🚀 Features

- **Custom Hooks**: `useLicenseState`, `useIsLicenseActive`, `useFeatureAllowed`.
- **Grace Period Support**: Built-in awareness of temporary network failover states.
- **Zero Dependencies**: Lightweight and self-contained.
- **SSR Ready**: Works with Next.js, Remix, and other SSR frameworks.
- **Type Safe**: First-class TypeScript support.

---

## 📦 Installation

```bash
npm install @getkeymanager/react-sdk
```

---

## 🛠️ Usage Example

```jsx
import { useLicenseState } from '@getkeymanager/react-sdk';

function PremiumWidget() {
  const { state, isLoading } = useLicenseState('XXXXX-XXXXX');

  if (isLoading) return <Loading />;

  if (state.isActive()) {
    return <PremiumContent />;
  }

  return <UpgradePrompt />;
}
```

---

## 🆕 New in v2.0

- **State-Based Core**: Intelligent hooks that handle grace periods and caching automatically.
- **Enterprise Hardening**: RSA signature verification integrated into the hook lifecycle.
- **Feature Gating**: Simplified boolean checks for license-dependent features.
    - `useFeatureAllowed('premium_analytics')`
