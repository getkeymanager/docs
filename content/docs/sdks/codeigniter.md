---
title: CodeIgniter SDK
description: Official CodeIgniter 4 SDK for the License Management Platform.
---

# CodeIgniter SDK

The official CodeIgniter 4 SDK provides simple yet powerful license management for PHP developers working in the CI4 ecosystem.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/codeigniter-sdk](https://github.com/getkeymanager/codeigniter-sdk)

---

## 🚀 Features

- **CI4 Native**: Follows CodeIgniter conventions and library patterns.
- **Helper Functions**: Convenient global helpers for status checks.
- **Logging**: Optional integration with CodeIgniter's logging system.
- **State-Based Validation**: Use typed state objects for predictable logic.
- **Grace Period Support**: Built-in 72-hour protection for network failures.

---

## 📦 Installation

Install via Composer:

```bash
composer require getkeymanager/codeigniter-sdk
```

---

## 🛠️ Usage Example

```php
// Load the helper
helper('getkeymanager');

// Resolve the state
$state = resolve_license_state($key);

if ($state->isActive()) {
    // License is valid and active
} elseif ($state->isInGracePeriod()) {
    // API unreachable, but license is still usable
} else {
    // Access denied
}
```

---

## 🆕 New in v2.0

- **Hardened Validation**: Consistent state resolution across all components.
- **RSA-4096 Signatures**: Enterprise-grade security for response verification.
- **Advanced Caching**: Intelligent TTL-based store for validation results.
