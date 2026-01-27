---
title: Laravel SDK
description: Official Laravel SDK for the License Management Platform.
---



The official Laravel SDK provides elegant license validation, activation, and management with native Laravel support, including service providers, facades, and middleware.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/laravel-sdk](https://github.com/getkeymanager/laravel-sdk)

---

## 🚀 Features

- **Facade Support**: Use the `GetKeyManager` facade for simple calls.
- **Route Middleware**: Protect routes with `licensed` or `feature:` middleware.
- **Artisan Commands**: Manage licenses and products from the terminal.
- **Auto-Discovery**: Zero-configuration setup for Laravel 10, 11, and 12.
- **Session Caching**: Automatic session-based caching for performance.

---

## 📦 Installation

Install via Composer:

```bash
composer require getkeymanager/laravel-sdk
```

---

## 🛠️ Usage Example

### Protecting a Route

```php
Route::get('/premium-feature', function () {
    //
})->middleware('licensed');
```

### Using the Facade

```php
use GetKeyManager;

$result = GetKeyManager::validate('XXXXX-XXXXX-XXXXX-XXXXX');

if ($result['success']) {
    //
}
```

---

## 🆕 New in v2.0

Version 2.0 introduces **Hardened State Management**:
- **`resolveState()`**: Transforms API responses into intelligent state objects.
- **Grace Period**: Automatic 72-hour failover protection.
- **Enhanced Verification**: Advanced RSA signature validation.
