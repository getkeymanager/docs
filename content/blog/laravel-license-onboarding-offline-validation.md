---
title: "Laravel License Onboarding, Activation, and Offline Validation"
description: "Step-by-step guide to onboarding users with the GetKeyManager Laravel SDK: assign and activate licenses, store .lic files, parse offline license files, and enforce licensing across routes, middleware, queues, and commands."
keywords:
  - Laravel license activation
  - Laravel SDK onboarding
  - offline license validation
  - license key assignment
  - license telemetry
  - GetKeyManager Laravel SDK
  - license enforcement Laravel
  - license middleware
  - license queue jobs
  - license console commands
tags:
  - Laravel
  - PHP
  - SDK
  - License Management
  - Offline Validation
category: "SDK Integration"
created_at: "2026-02-03"
updated_at: "2026-02-03"
seo_image: "/images/seo/laravel-license-onboarding.png"
---

## Overview

This walkthrough shows a complete, production-safe flow for Laravel:

1. Install `getkeymanager/laravel-sdk`.
2. Configure `config/getkeymanager.php`.
3. Add a license capture page with controller + route + Blade view.
4. Assign and activate the license using the request domain + IP.
5. Save the returned `.lic` file and related metadata.
6. Parse the `.lic` file offline using `parseLicenseFile`.
7. Enforce licensing in routes, middleware, jobs, queues, and commands.
8. Send telemetry data to keep usage visibility and security signals.

> **Goal:** keep licensing server-side, deterministic, and tamper-resistant—without blocking your app during temporary API outages.

---

## 1) Install the SDK

```bash
composer require getkeymanager/laravel-sdk
```

Optional config publish:

```bash
php artisan vendor:publish --tag=getkeymanager-config
```

---

## 2) Configure `config/getkeymanager.php`

Update `.env`:

```env
LICENSE_MANAGER_API_KEY=your-api-key-here
LICENSE_MANAGER_BASE_URL=https://api.getkeymanager.com
LICENSE_MANAGER_ENVIRONMENT=production
LICENSE_MANAGER_VERIFY_SIGNATURES=true
LICENSE_MANAGER_PUBLIC_KEY_FILE=storage_path:app/keys/product_public.pem
```

Then in `config/getkeymanager.php` ensure the keys match:

```php
return [
    'api_key' => env('LICENSE_MANAGER_API_KEY'),
    'base_url' => env('LICENSE_MANAGER_BASE_URL', 'https://api.getkeymanager.com'),
    'environment' => env('LICENSE_MANAGER_ENVIRONMENT', 'production'),
    'verify_signatures' => env('LICENSE_MANAGER_VERIFY_SIGNATURES', true),
    'public_key_file' => env('LICENSE_MANAGER_PUBLIC_KEY_FILE'),
    'timeout' => env('LICENSE_MANAGER_TIMEOUT', 30),
    'cache_enabled' => env('LICENSE_MANAGER_CACHE_ENABLED', true),
    'cache_ttl' => env('LICENSE_MANAGER_CACHE_TTL', 300),

    'middleware' => [
        'redirect_to' => '/license-required',
        'cache_in_session' => true,
        'session_key' => 'license_validation',
    ],
];
```

---

## 3) Create a license capture page (controller + route + Blade)

### Route

```php
// routes/web.php
use App\Http\Controllers\LicenseController;

Route::get('/license', [LicenseController::class, 'show']);
Route::post('/license', [LicenseController::class, 'store']);
```

### Controller

```php
// app/Http/Controllers/LicenseController.php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Storage;
use GetKeyManager\Laravel\Facades\GetKeyManager;

class LicenseController extends Controller
{
    public function show()
    {
        return view('license');
    }

    public function store(Request $request)
    {
        $request->validate([
            'license_key' => ['required', 'string'],
            'email' => ['required', 'email'],
        ]);

        $licenseKey = $request->input('license_key');
        $email = $request->input('email');

        // Domain + IP from the request
        $domain = $request->getHost();
        $ip = $request->ip();

        // 1) Assign license to the customer
        $assign = GetKeyManager::assignLicenseKey($licenseKey, $email);

        // 2) Activate the license with domain + IP metadata
        $activation = GetKeyManager::activateLicense($licenseKey, [
            'domain' => $domain,
            'ip' => $ip,
        ]);

        // 3) Store the .lic file if returned
        $licContent = $activation['response']['data']['licFileContent'] ?? null;
        if ($licContent) {
            $path = "licenses/{$licenseKey}.lic";
            Storage::disk('local')->put($path, $licContent);
        }

        // Optional: store the activation metadata for internal auditing
        $metaPath = "licenses/{$licenseKey}.json";
        Storage::disk('local')->put($metaPath, json_encode([
            'license_key' => $licenseKey,
            'email' => $email,
            'domain' => $domain,
            'ip' => $ip,
            'activation' => $activation,
        ], JSON_PRETTY_PRINT));

        return redirect('/license')->with('status', 'License activated successfully.');
    }
}
```

### Blade view

```blade
<!-- resources/views/license.blade.php -->
@extends('layouts.app')

@section('content')
<div class="container">
    <h1>Activate Your License</h1>

    @if (session('status'))
        <div class="alert alert-success">{{ session('status') }}</div>
    @endif

    <form method="POST" action="/license">
        @csrf

        <div class="mb-3">
            <label class="form-label">License Key</label>
            <input name="license_key" class="form-control" required>
        </div>

        <div class="mb-3">
            <label class="form-label">Email Address</label>
            <input name="email" type="email" class="form-control" required>
        </div>

        <button class="btn btn-primary">Activate</button>
    </form>
</div>
@endsection
```

---

## 4) Parse the `.lic` file offline with `parseLicenseFile`

Once the `.lic` file is stored, you can parse it offline with the PHP SDK validator. This is ideal for **offline verification**, **forensic checks**, and **server-side audits**.

```php
use GetKeyManager\SDK\Config\Configuration;
use GetKeyManager\SDK\Cache\CacheManager;
use GetKeyManager\SDK\Http\HttpClient;
use GetKeyManager\SDK\SignatureVerifier;
use GetKeyManager\SDK\StateResolver;
use GetKeyManager\SDK\StateStore;
use GetKeyManager\SDK\Validation\LicenseValidator;

$publicKey = file_get_contents(storage_path('app/keys/product_public.pem'));
$licContent = file_get_contents(storage_path('app/licenses/LIC-XXXX.lic'));

$config = new Configuration([
    'apiKey' => config('getkeymanager.api_key'),
    'baseUrl' => config('getkeymanager.base_url'),
    'environment' => config('getkeymanager.environment'),
    'verifySignatures' => true,
    'publicKey' => $publicKey,
    'cacheEnabled' => false,
    'cacheTtl' => 0,
]);

$verifier = new SignatureVerifier($publicKey);
$stateResolver = new StateResolver($verifier, $config->getEnvironment(), $config->getProductId());
$stateStore = new StateStore($verifier, 3600);
$cache = new CacheManager(false, 0);
$httpClient = new HttpClient($config, $verifier, $stateResolver);

$validator = new LicenseValidator(
    $config,
    $httpClient,
    $cache,
    $stateStore,
    $stateResolver,
    $verifier
);

$licenseData = $validator->parseLicenseFile($licContent, $publicKey);

// $licenseData now contains decrypted fields like license_key, expires_at, features, etc.
```

> If you want full offline validation (signature + expiry + hardware checks), use:
> 
> ```php
> $result = GetKeyManager::validateOfflineLicense($licenseData, [
>     'publicKey' => $publicKey,
>     'hardwareId' => GetKeyManager::generateHardwareId(),
> ]);
> ```

---

## 5) Protect routes, middleware, jobs, and commands

### Route guards

```php
Route::middleware(['license.validate'])->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index']);
});
```

### Middleware enforcement

```php
// app/Http/Middleware/RequireLicense.php
public function handle($request, Closure $next)
{
    $licenseKey = $request->header('X-License-Key');

    $result = GetKeyManager::validateLicense($licenseKey, [
        'domain' => $request->getHost(),
    ]);

    if (!($result['response']['data']['valid'] ?? false)) {
        return redirect('/license');
    }

    return $next($request);
}
```

### Console commands

```php
// app/Console/Commands/GenerateReports.php
public function handle()
{
    $licenseKey = config('app.license_key');
    $state = GetKeyManager::resolveLicenseState($licenseKey);

    if (!$state->isValid()) {
        $this->error('License is not active.');
        return 1;
    }

    // Run command
}
```

### Jobs and queues

```php
// app/Jobs/ProcessReport.php
public function handle()
{
    $licenseKey = config('app.license_key');
    $state = GetKeyManager::resolveLicenseState($licenseKey);

    if (!$state->allows('reporting')) {
        $this->release(30);
        return;
    }

    // Process job
}
```

---

## 6) Send telemetry data

Telemetry helps you spot misuse, suspicious activity, and feature adoption.

```php
GetKeyManager::sendTelemetry($licenseKey, [
    'event' => 'feature_used',
    'feature' => 'pdf_export',
    'domain' => request()->getHost(),
    'ip' => request()->ip(),
    'timestamp' => now()->toIso8601String(),
]);
```

---

## Security tips for Laravel apps

- **Never trust the client** for license state; always validate server-side.
- **Use domain binding** for web apps (`$request->getHost()`), and hardware IDs for on-prem installs.
- **Cache license state** for short periods to reduce API calls without going stale.
- **Enforce in multiple layers**: middleware + controllers + service classes + queues.
- **Store .lic files securely** (private storage, not public web directories).
- **Log activation results** to your audit trail for support and forensics.

---

## Next steps

- Add feature-gate checks with `GetKeyManager::checkFeature()`.
- Use `assignAndActivateLicenseKey()` for single-step onboarding.
- Rotate keys safely by updating `public_key_file` and refreshing cached state.

If you need help integrating, reach out to support or explore the SDK examples folder for a full project scaffold.
