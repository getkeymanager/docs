---
title: PHP SDK
description: Official PHP SDK for the License Management Platform API.
---

# PHP SDK

The official PHP SDK for the License Management Platform provides a robust, enterprise-grade interface for license validation, activation, and management.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/php-sdk](https://github.com/getkeymanager/php-sdk)

---

## 🚀 Features

- **License Operations**: Online and offline validation, activation, and deactivation.
- **Advanced Management**: Create, update, list, and delete licenses programmatically.
- **Enterprise Security**: RSA-4096-SHA256 signature verification.
- **Resiliency**: Automatic retry with exponential backoff and built-in caching.
- **Full Coverage**: Metadata management, product management, and contract management.

---

## 📦 Installation

Install via Composer:

```bash
composer require getkeymanager/php-sdk
```

---

## 🛠️ Usage Example

```php
use GetKeyManager\SDK\LicenseClient;

$client = new LicenseClient([
    'apiKey' => 'your-api-key',
    'baseUrl' => 'https://api.getkeymanager.com',
    'verifySignatures' => true,
    'publicKeyFile' => '/path/to/public_key.pem'
]);

// Validate a license
$result = $client->validateLicense('XXXXX-XXXXX-XXXXX-XXXXX');

if ($result['success']) {
    echo "Access Granted!";
}
```

---

## 🆕 New in v2.0

Version 2.0 adds over 30 new methods, including:
- **Product Management**: Manage products directly via API.
- **Generator Support**: Automate license generation.
- **Advanced Telemetry**: Filter and retrieve telemetry data.
- **Public Changelog**: Access updates without authentication.
