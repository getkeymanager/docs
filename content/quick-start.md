---
title: Quick Start Guide
description: Get up and running with GetKeyManager in less than 5 minutes.
---

# Quick Start Guide

Welcome to GetKeyManager! This guide will walk you through the essential steps to start managing your software licenses.

---

## Step 1: Access the Admin Portal

Log in to your dedicated Admin Portal instance. This is where you will manage your products, customers, and license keys.

*   **URL**: `https://app.getkeymanager.com` (or your private instance URL)
*   **Action**: Familiarize yourself with the [Dashboard]({{< ref "/content/docs/admin-portal/dashboard" >}}).

---

## Step 2: Create Your First Product

Before issuing licenses, you need to define a **Product**.

1.  Navigate to [Products]({{< ref "/content/docs/admin-portal/products" >}}) in the sidebar.
2.  Click **"Create Product"**.
3.  Fill in the name, slug, and environment (choose `development` for now).
4.  Enable **Signature Verification** for maximum security.

---

## Step 3: Generate an API Key

To communicate with the platform via our SDKs or API, you'll need an API Key.

1.  Go to [API Keys]({{< ref "/content/docs/admin-portal/api-keys" >}}).
2.  Create a new key with the necessary permissions.
3.  **Securely save the key**—you won't be able to see it again!

---

## Step 4: Issue a License

Now, let's create a license key for a customer.

1.  Go to [Generators]({{< ref "/content/docs/admin-portal/generators" >}}) or directly to [Licenses]({{< ref "/content/docs/admin-portal/licenses" >}}).
2.  Create a new license for your Product.
3.  Set the state to `assigned` or `available`.

---

## Step 5: Integrate the SDK

Choose the SDK that matches your application framework and follow the installation instructions.

### Popular SDKs:
*   [Laravel SDK]({{< ref "/docs" >}}#laravel)
*   [PHP SDK]({{< ref "/docs" >}}#php)
*   [Node.js SDK]({{< ref "/docs" >}}#nodejs)
*   [React SDK]({{< ref "/docs" >}}#react)

### Example (PHP):
```php
$client = new \GetKeyManager\SDK\LicenseClient([
    'apiKey' => 'your_api_key_here',
    'baseUrl' => 'https://api.getkeymanager.com',
    'verifySignatures' => true,
    'publicKeyFile' => '/path/to/public_key.pem'
]);

$result = $client->validateLicense('XXXXX-XXXXX-XXXXX-XXXXX');

if ($result['success']) {
    echo "License is valid!";
}
```

---

## Next Steps

Now that you've validated your first license, explore more advanced topics:

*   **[License Lifecycle]({{< ref "/content/docs/license-lifecycle" >}})** — Learn about various license states.
*   **[Hardware Binding]({{< ref "/content/docs/usb-offline" >}})** — Lock licenses to specific machines.
*   **[Webhooks]({{< ref "/content/docs/admin-portal/webhooks" >}})** — Automate your workflow with real-time notifications.
*   **[API Endpoints]({{< ref "/content/docs/api/endpoints" >}})** — Explore full automation capabilities.
