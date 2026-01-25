---
title: "CodeIgniter License Integration: Beyond the Bootstrap"
description: "Learn how to implement secure, multi-layered license validation in CodeIgniter 3 and 4 applications using hooks, filters, libraries, and model-based enforcement for robust entitlement management."
keywords:
  - CodeIgniter license validation
  - CodeIgniter security
  - CodeIgniter 4 filters
  - CodeIgniter hooks
  - PHP framework security
tags:
  - CodeIgniter
  - PHP
  - Security
  - License Management
  - Framework
category: "Security Integration"
created_at: "2026-01-25"
updated_at: "2026-01-25"
seo_image: "/images/seo/codeigniter-license-security.png"
---

## Introduction

CodeIgniter developers implementing license validation face a framework-specific challenge: while CodeIgniter provides hooks and filters for cross-cutting concerns, many developers still implement single-point validation that's easily bypassed.

This guide teaches you how to build **layered license enforcement** in CodeIgniter 3 and 4 applications. You'll learn how to use hooks, filters, libraries, and model-based validation to create defense-in-depth protection that works across controllers, APIs, CLI commands, and background tasks.

Whether you're building a SaaS application, admin panel, API server, or e-commerce extension, this guide will help you implement CodeIgniter-native license validation that withstands tampering attempts.

## Common Mistakes Developers Make

### Mistake 1: Single Hook Check

```php
// CodeIgniter 3: config/hooks.php
$hook['post_controller_constructor'] = [
    'class' => 'EntitlementHook',
    'function' => 'verify',
    'filename' => 'EntitlementHook.php',
    'filepath' => 'hooks'
];

// hooks/EntitlementHook.php
class EntitlementHook {
    public function verify() {
        if (!verify_authority()) {
            show_error('Unauthorized', 403);
        }
    }
}
```

**Why this fails:** Disabling hooks in `config.php` or removing the hook definition bypasses all validation. Single hooks are single points of failure.

### Mistake 2: Controller-Level Boolean Checks

```php
// CodeIgniter 4
class PremiumController extends BaseController {
    public function __construct() {
        if (!$this->verify_authority()) {
            throw new \CodeIgniter\Exceptions\PageNotFoundException();
        }
    }
}
```

**Why this fails:** If attackers extend this controller or modify the constructor, they bypass validation. Additionally, booleans provide no context.

### Mistake 3: Only Validating in Web Routes

```php
// Only protecting web controllers, not CLI or API routes
```

**Why this fails:** CLI commands and API endpoints remain unprotected.

## Where to Add Enforcement Logic (CodeIgniter 4)

### 1. Global Filter (Primary Layer)

**Location:** `app/Filters/EntitlementFilter.php`

```php
<?php
namespace App\Filters;

use CodeIgniter\HTTP\RequestInterface;
use CodeIgniter\HTTP\ResponseInterface;
use CodeIgniter\Filters\FilterInterface;

class EntitlementFilter implements FilterInterface {
    public function before(RequestInterface $request, $arguments = null) {
        $entitlementService = service('entitlement');
        $state = $entitlementService->getState();
        
        // Check overall status
        if ($state['status'] === 'EXPIRED') {
            return redirect()->to('/renew')->with('error', 'Your entitlement has expired');
        }
        
        if ($state['status'] === 'SUSPENDED') {
            return redirect()->to('/suspended');
        }
        
        if ($state['status'] !== 'ACTIVE') {
            return redirect()->to('/activate');
        }
        
        // Check specific capability if provided
        if (!empty($arguments)) {
            $capability = $arguments[0] ?? null;
            
            if ($capability && !in_array($capability, $state['features'] ?? [], true)) {
                throw new \CodeIgniter\Exceptions\PageNotFoundException(
                    "Feature '{$capability}' not available"
                );
            }
        }
        
        // Attach state to request
        $request->entitlementState = $state;
    }
    
    public function after(RequestInterface $request, ResponseInterface $response, $arguments = null) {
        // Nothing to do after
    }
}
```

**Register in `app/Config/Filters.php`:**

```php
<?php
namespace Config;

use CodeIgniter\Config\BaseConfig;

class Filters extends BaseConfig {
    public $aliases = [
        'entitlement' => \App\Filters\EntitlementFilter::class,
    ];
    
    public $globals = [
        'before' => [
            // 'entitlement' // Apply globally or selectively
        ],
    ];
    
    public $methods = [];
    
    public $filters = [];
}
```

### 2. Service Layer (Centralized Logic)

**Location:** `app/Libraries/EntitlementService.php`

```php
<?php
namespace App\Libraries;

class EntitlementService {
    protected $cache;
    protected $apiKey;
    protected $productUuid;
    protected $apiUrl;
    
    public function __construct() {
        $this->cache = \Config\Services::cache();
        $this->apiKey = getenv('ENTITLEMENT_API_KEY');
        $this->productUuid = getenv('ENTITLEMENT_PRODUCT_UUID');
        $this->apiUrl = getenv('ENTITLEMENT_API_URL') ?: 'https://api.getkeymanager.com/api/v1';
    }
    
    public function resolveAuthority(string $entitlementKey, string $identifier): array {
        $cacheKey = "entitlement:{$entitlementKey}:{$identifier}";
        
        // Check cache first
        if ($cached = $this->cache->get($cacheKey)) {
            return $cached;
        }
        
        try {
            $client = \Config\Services::curlrequest();
            
            $response = $client->post($this->apiUrl . '/verify', [
                'json' => [
                    'entitlement_key' => $entitlementKey,
                    'identifier' => $identifier,
                    'product_uuid' => $this->productUuid
                ],
                'headers' => [
                    'Authorization' => 'Bearer ' . $this->apiKey,
                    'Content-Type' => 'application/json'
                ],
                'timeout' => 10
            ]);
            
            $data = json_decode($response->getBody(), true);
            $state = $this->parseResponse($data);
            
            // Cache for 1 hour
            $this->cache->save($cacheKey, $state, 3600);
            
            return $state;
            
        } catch (\Exception $e) {
            log_message('error', 'Authority resolution failed: ' . $e->getMessage());
            return ['status' => 'DEGRADED', 'features' => []];
        }
    }
    
    private function parseResponse(array $data): array {
        $code = $data['response']['code'] ?? null;
        $responseData = $data['response']['data'] ?? [];
        
        return match($code) {
            200 => [
                'status' => 'ACTIVE',
                'features' => $responseData['features'] ?? [],
                'expires_at' => $responseData['expires_at'] ?? null
            ],
            205 => ['status' => 'EXPIRED', 'expires_at' => $responseData['expires_at'] ?? null],
            204 => ['status' => 'SUSPENDED'],
            202 => ['status' => 'NOT_ACTIVATED'],
            default => ['status' => 'INVALID']
        };
    }
    
    public function getState(): array {
        $session = session();
        
        // Check session cache
        if ($cached = $session->get('entitlement_state')) {
            $expires = $session->get('entitlement_expires');
            if ($expires && time() < $expires) {
                return $cached;
            }
        }
        
        // Resolve authority
        $entitlementKey = getenv('ENTITLEMENT_KEY') ?: $session->get('entitlement_key');
        $identifier = \Config\Services::request()->getServer('HTTP_HOST') ?: 'localhost';
        
        $state = $this->resolveAuthority($entitlementKey, $identifier);
        
        // Cache in session for 1 hour
        $session->set('entitlement_state', $state);
        $session->set('entitlement_expires', time() + 3600);
        
        return $state;
    }
    
    public function hasCapability(array $state, string $capability): bool {
        return $state['status'] === 'ACTIVE' && in_array($capability, $state['features'] ?? [], true);
    }
}
```

**Register as service in `app/Config/Services.php`:**

```php
<?php
namespace Config;

use CodeIgniter\Config\BaseService;

class Services extends BaseService {
    public static function entitlement(bool $getShared = true) {
        if ($getShared) {
            return static::getSharedInstance('entitlement');
        }
        
        return new \App\Libraries\EntitlementService();
    }
}
```

### 3. Controller Validation (Defense in Depth)

```php
<?php
namespace App\Controllers;

class ExportController extends BaseController {
    protected $entitlementService;
    
    public function __construct() {
        $this->entitlementService = service('entitlement');
    }
    
    public function index() {
        // Additional check in controller
        $state = $this->entitlementService->getState();
        
        if (!$this->entitlementService->hasCapability($state, 'export')) {
            throw new \CodeIgniter\Exceptions\PageNotFoundException('Export feature not available');
        }
        
        return view('export/index', [
            'state' => $state
        ]);
    }
    
    public function generate() {
        $state = $this->entitlementService->getState();
        
        if (!$this->entitlementService->hasCapability($state, 'export')) {
            return $this->response->setJSON([
                'error' => 'Export capability not available'
            ])->setStatusCode(403);
        }
        
        $data = $this->performExport();
        
        return $this->response->setJSON([
            'success' => true,
            'data' => $data
        ]);
    }
    
    private function performExport() {
        // Export logic
        return ['records' => []];
    }
}
```

### 4. CLI Commands

```php
<?php
namespace App\Commands;

use CodeIgniter\CLI\BaseCommand;
use CodeIgniter\CLI\CLI;

class ReportCommand extends BaseCommand {
    protected $group = 'Reports';
    protected $name = 'reports:generate';
    protected $description = 'Generate automated reports';
    
    public function run(array $params) {
        $entitlementService = service('entitlement');
        $state = $entitlementService->getState();
        
        // Verify authority in CLI command
        if (!$entitlementService->hasCapability($state, 'automated_reports')) {
            CLI::error('Automated reports capability not available');
            return EXIT_ERROR;
        }
        
        CLI::write('Generating report...', 'green');
        
        // Generate report
        $this->generateReport();
        
        CLI::write('Report generated successfully', 'green');
        return EXIT_SUCCESS;
    }
    
    private function generateReport() {
        // Report generation logic
    }
}
```

### 5. API Routes Protection

```php
// app/Config/Routes.php
$routes->group('api', ['namespace' => 'App\Controllers\API', 'filter' => 'entitlement'], function($routes) {
    $routes->post('export', 'ExportAPI::export', ['filter' => 'entitlement:export']);
    $routes->get('analytics', 'AnalyticsAPI::index', ['filter' => 'entitlement:analytics']);
});
```

## Where to Add Enforcement Logic (CodeIgniter 3)

### 1. Hook System

```php
// config/hooks.php
$hook['post_controller_constructor'][] = [
    'class' => 'EntitlementHook',
    'function' => 'verify',
    'filename' => 'EntitlementHook.php',
    'filepath' => 'hooks'
];

// application/hooks/EntitlementHook.php
class EntitlementHook {
    public function verify() {
        $CI =& get_instance();
        $CI->load->library('entitlement_service');
        
        $state = $CI->entitlement_service->get_state();
        
        if ($state['status'] !== 'ACTIVE') {
            show_error('Access denied', 403);
        }
    }
}
```

### 2. Base Controller

```php
// application/core/MY_Controller.php
class MY_Controller extends CI_Controller {
    protected $entitlement_state;
    
    public function __construct() {
        parent::__construct();
        
        $this->load->library('entitlement_service');
        $this->entitlement_state = $this->entitlement_service->get_state();
        
        // Verify authority
        if ($this->entitlement_state['status'] !== 'ACTIVE') {
            redirect('activate');
        }
    }
    
    protected function require_capability($capability) {
        if (!in_array($capability, $this->entitlement_state['features'] ?? [], true)) {
            show_error("Feature '{$capability}' not available", 403);
        }
    }
}

// In controllers
class Export extends MY_Controller {
    public function index() {
        $this->require_capability('export');
        $this->load->view('export/index');
    }
}
```

## Example Integration Flow

### Complete CodeIgniter 4 Setup

**Environment:**
```bash
# .env
ENTITLEMENT_API_KEY=your-api-key
ENTITLEMENT_PRODUCT_UUID=your-product-uuid
ENTITLEMENT_KEY=stored-entitlement-key
```

**Routes with filters:**
```php
// app/Config/Routes.php
$routes->group('dashboard', ['filter' => 'entitlement'], function($routes) {
    $routes->get('/', 'Dashboard::index');
    $routes->get('export', 'Export::index', ['filter' => 'entitlement:export']);
    $routes->get('analytics', 'Analytics::index', ['filter' => 'entitlement:analytics']);
});
```

**Controller:**
```php
<?php
namespace App\Controllers;

class Dashboard extends BaseController {
    public function index() {
        $entitlementService = service('entitlement');
        $state = $entitlementService->getState();
        
        return view('dashboard/index', [
            'hasExport' => $entitlementService->hasCapability($state, 'export'),
            'hasAnalytics' => $entitlementService->hasCapability($state, 'analytics'),
            'expiresAt' => $state['expires_at'] ?? null
        ]);
    }
}
```

## What NOT to Do

### ❌ Single Hook Only
```php
// BAD - Only one hook, easily disabled
$hook['post_controller_constructor'] = ['class' => 'EntitlementHook'];
```

### ❌ No Controller-Level Checks
```php
// BAD - Relying only on hooks/filters
class Premium extends CI_Controller {
    public function feature() {
        // No validation here
    }
}
```

### ❌ Hardcoded Keys
```php
// BAD
$this->entitlement_key = 'XXXX-XXXX-XXXX';
```

### ❌ No CLI Protection
```php
// BAD - CLI commands with no validation
```

## Conclusion

CodeIgniter license validation requires using framework-native features (filters/hooks) combined with controller-level checks. Key principles:

1. **Use filters (CI4) or hooks (CI3)** — Framework-native protection
2. **Validate in controllers** — Defense in depth
3. **Service layer for logic** — Centralized, cacheable
4. **Protect CLI commands** — Independent validation
5. **Capability-based access** — Feature flags, not booleans
6. **Use sessions for caching** — With TTL
7. **Register as service** — Singleton pattern

Build with the assumption that hooks/filters can be disabled, and add controller-level validation as backup.
