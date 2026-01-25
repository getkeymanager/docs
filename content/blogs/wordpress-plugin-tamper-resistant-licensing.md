---
title: "Building Tamper-Resistant WordPress Plugins with License Validation"
description: "Learn how to implement multi-layered license validation in WordPress plugins to prevent bypass attempts, protect premium features, and ensure proper enforcement across admin hooks, AJAX handlers, REST API endpoints, and cron jobs."
keywords:
  - WordPress plugin security
  - WordPress license validation
  - plugin licensing
  - WordPress security
  - plugin tamper protection
  - WordPress hooks
tags:
  - WordPress
  - PHP
  - Plugin Development
  - Security
  - License Management
category: "Security Integration"
created_at: "2026-01-25"
updated_at: "2026-01-25"
seo_image: "/images/seo/wordpress-plugin-license-security.png"
---

## Introduction

WordPress plugin developers face a unique challenge: the entire codebase is visible and modifiable by site administrators. Unlike compiled applications, PHP plugins can be edited directly from the WordPress admin panel or via FTP.

This transparency means traditional license enforcement strategies fail. A single `if ($licensed)` check in your main plugin file is trivial to bypass—administrators can simply change it to `if (true)` and save.

This guide teaches you how to build **defense-in-depth license validation** for WordPress plugins. You'll learn how to scatter checks across hooks, AJAX handlers, admin pages, shortcodes, REST API endpoints, and cron jobs—making bypass attempts expensive and obvious.

Whether you're building a page builder, SEO tool, e-commerce extension, or membership plugin, these patterns will help you implement license enforcement that withstands real-world tampering.

## Common Mistakes Developers Make

Let's start by understanding why naive integrations fail in WordPress environments.

### Mistake 1: Single Check in Main Plugin File

```php
// my-plugin.php
if (!resolve_authority()) {
    return; // Stop plugin execution
}

// Rest of plugin initialization
```

**Why this fails:** Administrators can edit this file directly from the WordPress admin editor. They'll simply remove the check or change it to `if (true)`. Even if you disable the editor, they can modify files via FTP.

### Mistake 2: Boolean-Based License Checks

```php
$has_authority = verify_authority();

if ($has_authority === true) {
    add_action('admin_menu', 'add_premium_menu');
}
```

**Why this fails:** Searching the plugin directory for `$is_licensed` reveals every check. An attacker can modify the variable once and defeat all checks. Booleans provide no context about *why* validation failed.

### Mistake 3: Transient Caching Without Verification

```php
$authority_granted = get_transient('plugin_authority_granted');

if ($authority_granted === false) {
    $authority_granted = remote_resolve_authority();
    set_transient('plugin_authority_granted', $authority_granted, WEEK_IN_SECONDS);
}
```

**Why this fails:** If attackers modify the transient in the database to always be `true`, validation never runs. Caching is useful for performance but must be combined with real-time checks at critical boundaries.

### Mistake 4: Only Checking in Admin Panel

```php
add_action('admin_init', function() {
    if (!has_authority()) {
        wp_die('Invalid entitlement');
    }
});
```

**Why this fails:** This only protects the admin panel. AJAX handlers, REST API endpoints, shortcodes, and cron jobs remain unprotected. Attackers can call these directly.

### Mistake 5: Storing License Keys in wp_options Unprotected

```php
update_option('my_plugin_entitlement_key', $_POST['entitlement_key']);
```

**Why this fails:** The `wp_options` table is fully readable by plugins and themes. If attackers extract your license key, they can use it on their own sites. Keys should be hashed or encrypted if stored.

### Mistake 6: Hard Errors That Break Sites

```php
if (!has_authority()) {
    die('ENTITLEMENT ERROR: Plugin disabled');
}
```

**Why this fails:** If your validation server is down or the site loses internet connectivity, this hard-crashes the site. Graceful degradation is critical for WordPress plugins.

## Where to Add Enforcement Logic

WordPress plugins have many entry points. Let's cover them systematically:

### 1. Plugin Initialization (Main File)

**Location:** `my-plugin.php` (main plugin file)

**Purpose:** Initialize license state and register the singleton service.

```php
<?php
/**
 * Plugin Name: My Premium Plugin
 * Description: A premium plugin with license validation
 */

if (!defined('ABSPATH')) {
    exit;
}

// Load entitlement service
require_once plugin_dir_path(__FILE__) . 'includes/class-entitlement-service.php';

// Initialize entitlement on plugins_loaded
add_action('plugins_loaded', function() {
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $entitlement->initialize();
});
```

**Why here:** This runs early enough to prepare state but doesn't crash the site if validation fails.

### 2. Admin Menu Registration

**Location:** Admin menu hooks

**Purpose:** Only show premium menu items if licensed.

```php
add_action('admin_menu', function() {
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Always show settings page (for entitlement activation)
    add_menu_page(
        'My Plugin',
        'My Plugin',
        'manage_options',
        'my-plugin',
        'my_plugin_settings_page'
    );
    
    // Only show premium pages if authorized
    if ($state->is_active() && $state->has_feature('premium_reports')) {
        add_submenu_page(
            'my-plugin',
            'Premium Reports',
            'Premium Reports',
            'manage_options',
            'my-plugin-reports',
            'my_plugin_reports_page'
        );
    }
});
```

**Why here:** This prevents unauthorized users from seeing premium features in the admin menu, but doesn't prevent direct URL access (we'll handle that next).

### 3. Admin Page Callbacks

**Location:** Admin page rendering functions

**Purpose:** Verify license at page render time.

```php
function my_plugin_reports_page() {
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Double-check even if menu item was registered
    if (!$state->is_active()) {
        wp_die(
            'This feature requires an active entitlement.',
            'Entitlement Required',
            ['response' => 403]
        );
    }
    
    if (!$state->has_feature('premium_reports')) {
        wp_die(
            'Your entitlement does not include Premium Reports.',
            'Feature Not Available',
            ['response' => 403]
        );
    }
    
    // Render premium page
    include plugin_dir_path(__FILE__) . 'views/reports-page.php';
}
```

**Why here:** Even if someone accesses the page via direct URL, this check blocks rendering.

### 4. AJAX Handlers

**Location:** AJAX action hooks

**Purpose:** Protect AJAX endpoints that execute premium functionality.

```php
add_action('wp_ajax_my_plugin_generate_report', function() {
    // Verify nonce first
    check_ajax_referer('my_plugin_nonce', 'nonce');
    
    // Verify authority
    if (!current_user_can('manage_options')) {
        wp_send_json_error('Insufficient permissions', 403);
    }
    
    // Verify authority
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    if (!$state->can_generate_reports()) {
        wp_send_json_error([
            'message' => 'Report generation requires an active entitlement.',
            'code' => $state->get_reason_code()
        ], 403);
    }
    
    // Process report generation
    $report = generate_report();
    wp_send_json_success($report);
});
```

**Why here:** AJAX handlers are callable via JavaScript, so they must be independently protected.

### 5. REST API Endpoints

**Location:** REST API route registration

**Purpose:** Protect custom REST API endpoints.

```php
add_action('rest_api_init', function() {
    register_rest_route('my-plugin/v1', '/export', [
        'methods' => 'POST',
        'callback' => 'my_plugin_rest_export',
        'permission_callback' => function() {
            // Verify authority permissions
            if (!current_user_can('manage_options')) {
                return false;
            }
            
            // Verify authority
            $entitlement = My_Plugin_Entitlement_Service::instance();
            $state = $entitlement->get_state();
            
            return $state->is_active() && $state->has_feature('export');
        }
    ]);
});

function my_plugin_rest_export($request) {
    // Additional check inside callback
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    if (!$state->can_export()) {
        return new WP_Error(
            'entitlement_required',
            'Export feature not available',
            ['status' => 403]
        );
    }
    
    // Process export
    return ['success' => true, 'data' => $export_data];
}
```

**Why here:** REST API endpoints are publicly accessible and must validate both permissions and license state.

### 6. Shortcodes

**Location:** Shortcode registration

**Purpose:** Ensure premium shortcodes only work with valid licenses.

```php
add_shortcode('premium_widget', function($atts) {
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    if (!$state->is_active()) {
        return '<!-- Premium Widget: Entitlement inactive -->';
    }
    
    if (!$state->has_feature('premium_widgets')) {
        return '<!-- Premium Widget: Not included in your entitlement -->';
    }
    
    // Render premium widget
    ob_start();
    include plugin_dir_path(__FILE__) . 'views/premium-widget.php';
    return ob_get_clean();
});
```

**Why here:** Shortcodes can be added by any editor, so they need independent validation.

### 7. Cron Jobs

**Location:** Scheduled event callbacks

**Purpose:** Ensure background tasks respect license state.

```php
add_action('my_plugin_daily_sync', function() {
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Verify authority for premium sync
    if (!$state->can_use_premium_sync()) {
        error_log('My Plugin: Daily sync skipped (entitlement inactive)');
        return;
    }
    
    // Perform sync
    my_plugin_sync_data();
});

// Schedule on plugin activation
register_activation_hook(__FILE__, function() {
    if (!wp_next_scheduled('my_plugin_daily_sync')) {
        wp_schedule_event(time(), 'daily', 'my_plugin_daily_sync');
    }
});
```

**Why here:** Cron jobs run in the background and must validate independently.

### 8. Widget Registration

**Location:** Widget classes

**Purpose:** Register premium widgets only when licensed.

```php
add_action('widgets_init', function() {
    $entitlement = My_Plugin_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Always register basic widget
    register_widget('My_Plugin_Basic_Widget');
    
    // Only register premium widgets if authorized
    if ($state->is_active() && $state->has_feature('premium_widgets')) {
        register_widget('My_Plugin_Premium_Widget');
    }
});
```

**Why here:** Prevents premium widgets from appearing in the widget selector for unlicensed users.

## What Data Should Be Passed

When validating licenses in WordPress, provide complete context:

### Domain Name

Always pass the site's domain:

```php
$domain = parse_url(home_url(), PHP_URL_HOST);

$response = $entitlement_client->verify([
    'entitlement_key' => $entitlement_key,
    'identifier' => $domain,
    'product_uuid' => MY_PLUGIN_PRODUCT_UUID
]);
```

**Why:** Domain binding prevents a single license from being used across multiple WordPress installations.

### Server Identifier (For Server-Side Plugins)

For plugins running on managed servers (not shared hosting):

```php
$hwid = My_Plugin_Entitlement_Service::generate_hardware_id();

$response = $entitlement_client->verify([
    'entitlement_key' => $entitlement_key,
    'identifier' => $hwid,
    'product_uuid' => MY_PLUGIN_PRODUCT_UUID
]);
```

**Why:** Hardware identifiers work for VPS/dedicated hosting where the server is stable.

### Product UUID

Always specify your product:

```php
define('MY_PLUGIN_PRODUCT_UUID', 'your-product-uuid-here');

$response = $entitlement_client->verify([
    'entitlement_key' => $entitlement_key,
    'identifier' => $domain,
    'product_uuid' => MY_PLUGIN_PRODUCT_UUID
]);
```

**Why:** If you offer multiple plugins, each needs its own validation scope.

### WordPress Version & PHP Version (Optional)

Pass environment metadata for better support:

```php
$response = $entitlement_client->verify([
    'entitlement_key' => $entitlement_key,
    'identifier' => $domain,
    'metadata' => [
        'wp_version' => get_bloginfo('version'),
        'php_version' => PHP_VERSION,
        'plugin_version' => MY_PLUGIN_VERSION
    ]
]);
```

**Why:** This helps with diagnostics and allows you to enforce minimum version requirements server-side.

### What Must Never Be Stored in Plain Text

❌ Never store in plain text:
- API keys
- License keys (if avoidable)
- Signatures
- Private keys

✅ Store securely:
```php
// Use WordPress's built-in encryption (if available)
if (function_exists('wp_hash')) {
    $hashed_key = wp_hash($entitlement_key);
    update_option('my_plugin_entitlement_hash', $hashed_key);
}

// Or use custom encryption
$encrypted_key = openssl_encrypt(
    $entitlement_key,
    'AES-256-CBC',
    wp_salt('auth'),
    0,
    substr(wp_salt('secure_auth'), 0, 16)
);
update_option('my_plugin_entitlement_encrypted', $encrypted_key);
```

## How to Structure Safe Checks

Now let's discuss validation patterns specific to WordPress.

### Use State Objects, Not Booleans

Bad:
```php
$is_valid = resolve_authority(); // Returns true/false
```

Good:
```php
$state = $entitlement->get_state(); // Returns state object

if ($state->is_active()) { }
if ($state->has_feature('export')) { }
if ($state->get_days_until_expiry() <= 7) { }
```

**Why:** State objects provide context. You can ask specific questions and handle different scenarios appropriately.

### Check Response Codes for Specific Handling

```php
$response = $entitlement_client->verify($data);
$code = $response['response']['code'] ?? null;

switch ($code) {
    case 200: // Valid and active
        $this->set_state('active', $response['response']['data']);
        break;
        
    case 202: // No activation found
        $this->set_state('not_activated');
        break;
        
    case 205: // Expired
        $expires_at = $response['response']['data']['expires_at'] ?? null;
        $this->set_state('expired', ['expires_at' => $expires_at]);
        break;
        
    case 204: // Suspended
        $this->set_state('suspended');
        break;
        
    case 210: // Invalid entitlement key
        $this->set_state('invalid');
        break;
        
    default:
        $this->set_state('unknown', ['code' => $code]);
}
```

**Why:** Each response code indicates a specific condition that requires different handling.

### Use Transients for Performance, Not Security

```php
public function get_state() {
    // Try transient first
    $cached_state = get_transient('my_plugin_entitlement_state');
    
    if ($cached_state !== false && $this->is_valid_cache($cached_state)) {
        return $cached_state;
    }
    
    // Resolve authority remotely
    $state = $this->resolve_authority_remotely();
    
    // Cache for 6 hours
    set_transient('my_plugin_entitlement_state', $state, 6 * HOUR_IN_SECONDS);
    
    return $state;
}

private function is_valid_cache($cached_state) {
    // Don't trust cache blindly—verify structure
    return isset($cached_state['status']) 
        && isset($cached_state['timestamp'])
        && (time() - $cached_state['timestamp']) < 6 * HOUR_IN_SECONDS;
}
```

**Why:** Caching reduces API calls but must include validation to prevent manual cache manipulation.

### Scatter Checks Across Multiple Hooks

Don't validate once—validate at every entry point:

```php
// Check 1: Admin page rendering
add_action('admin_init', function() {
    if (isset($_GET['page']) && $_GET['page'] === 'my-plugin-premium') {
        $state = My_Plugin_Entitlement_Service::instance()->get_state();
        if (!$state->is_active()) {
            wp_die('Entitlement required');
        }
    }
});

// Check 2: AJAX handler
add_action('wp_ajax_my_plugin_action', function() {
    $state = My_Plugin_Entitlement_Service::instance()->get_state();
    if (!$state->can_use_feature('ajax_action')) {
        wp_send_json_error('Entitlement required', 403);
    }
    // Process action
});

// Check 3: REST API endpoint
add_action('rest_api_init', function() {
    register_rest_route('my-plugin/v1', '/action', [
        'permission_callback' => function() {
            $state = My_Plugin_Entitlement_Service::instance()->get_state();
            return $state->is_active();
        },
        'callback' => function() {
            // Additional check inside callback
            $state = My_Plugin_Entitlement_Service::instance()->get_state();
            if (!$state->can_use_feature('rest_action')) {
                return new WP_Error('entitlement_required', 'Entitlement required');
            }
            // Process
        }
    ]);
});
```

**Why:** Multiple independent checks mean attackers must bypass multiple locations.

### Implement Grace Periods for Expired Licenses

```php
public function get_state() {
    $state = $this->resolve_authority_remotely();
    
    if ($state['status'] === 'expired') {
        $expired_at = strtotime($state['expires_at'] ?? 'now');
        $days_expired = floor((time() - $expired_at) / DAY_IN_SECONDS);
        
        if ($days_expired <= 7) {
            // Grace period: allow access with warning
            add_action('admin_notices', function() use ($days_expired) {
                echo '<div class="notice notice-warning">';
                echo '<p><strong>Entitlement Expired:</strong> ';
                echo 'Your entitlement expired ' . $days_expired . ' days ago. ';
                echo 'Please renew to continue receiving updates.</p>';
                echo '</div>';
            });
            
            // Treat as active during grace period
            $state['status'] = 'active';
            $state['grace_period'] = true;
        }
    }
    
    return $state;
}
```

**Why:** Grace periods prevent abrupt lockouts and improve user experience without sacrificing long-term enforcement.

## Example Integration Flow

Here's a complete example demonstrating all concepts:

### Step 1: License Service Class

```php
// includes/class-entitlement-service.php

class My_Plugin_Entitlement_Service {
    private static $instance = null;
    private $state = null;
    private $client = null;
    
    public static function instance() {
        if (self::$instance === null) {
            self::$instance = new self();
        }
        return self::$instance;
    }
    
    public function __construct() {
        require_once plugin_dir_path(__FILE__) . 'class-entitlement-client.php';
        $this->client = new My_Plugin_Entitlement_Client([
            'api_key' => defined('MY_PLUGIN_API_KEY') ? MY_PLUGIN_API_KEY : '',
            'product_uuid' => defined('MY_PLUGIN_PRODUCT_UUID') ? MY_PLUGIN_PRODUCT_UUID : ''
        ]);
    }
    
    public function initialize() {
        // Load state on initialization
        $this->state = $this->load_state();
    }
    
    private function load_state() {
        // Try cache first
        $cached = get_transient('my_plugin_entitlement_state');
        if ($cached !== false && $this->is_valid_cache($cached)) {
            return $cached;
        }
        
        // Resolve authority remotely
        return $this->resolve_authority_remotely();
    }
    
    private function resolve_authority_remotely() {
        $entitlement_key = get_option('my_plugin_entitlement_key', '');
        
        if (empty($entitlement_key)) {
            return $this->create_state('not_activated');
        }
        
        try {
            $domain = parse_url(home_url(), PHP_URL_HOST);
            
            $response = $this->client->verify([
                'entitlement_key' => $entitlement_key,
                'identifier' => $domain,
                'product_uuid' => MY_PLUGIN_PRODUCT_UUID
            ]);
            
            $code = $response['response']['code'] ?? null;
            $data = $response['response']['data'] ?? [];
            
            return $this->map_response_to_state($code, $data);
            
        } catch (Exception $e) {
            error_log('Entitlement validation error: ' . $e->getMessage());
            return $this->create_state('degraded');
        }
    }
    
    private function map_response_to_state($code, $data) {
        $state = [];
        
        switch ($code) {
            case 200:
                $state = [
                    'status' => 'active',
                    'features' => $data['features'] ?? [],
                    'expires_at' => $data['expires_at'] ?? null,
                    'activations_count' => $data['activations_count'] ?? 0
                ];
                break;
                
            case 205:
                $state = [
                    'status' => 'expired',
                    'expires_at' => $data['expires_at'] ?? null
                ];
                break;
                
            case 204:
                $state = ['status' => 'suspended'];
                break;
                
            case 202:
                $state = ['status' => 'not_activated'];
                break;
                
            default:
                $state = ['status' => 'invalid', 'code' => $code];
        }
        
        $state['timestamp'] = time();
        
        // Cache for 6 hours
        set_transient('my_plugin_entitlement_state', $state, 6 * HOUR_IN_SECONDS);
        
        return $state;
    }
    
    private function create_state($status, $data = []) {
        return array_merge(['status' => $status, 'timestamp' => time()], $data);
    }
    
    public function get_state() {
        if ($this->state === null) {
            $this->initialize();
        }
        return new My_Plugin_Entitlement_State($this->state);
    }
}
```

### Step 2: State Object

```php
// includes/class-entitlement-state.php

class My_Plugin_Entitlement_State {
    private $data;
    
    public function __construct($data) {
        $this->data = $data;
    }
    
    public function is_active() {
        return isset($this->data['status']) && $this->data['status'] === 'active';
    }
    
    public function is_expired() {
        return isset($this->data['status']) && $this->data['status'] === 'expired';
    }
    
    public function is_suspended() {
        return isset($this->data['status']) && $this->data['status'] === 'suspended';
    }
    
    public function is_degraded() {
        return isset($this->data['status']) && $this->data['status'] === 'degraded';
    }
    
    public function has_feature($feature) {
        return $this->is_active() && in_array($feature, $this->data['features'] ?? [], true);
    }
    
    public function can_generate_reports() {
        return $this->has_feature('premium_reports');
    }
    
    public function can_export() {
        return $this->has_feature('export');
    }
    
    public function get_status() {
        return $this->data['status'] ?? 'unknown';
    }
    
    public function get_reason_code() {
        return $this->data['code'] ?? null;
    }
}
```

### Step 3: Admin Page with Validation

```php
// admin/reports-page.php

add_action('admin_menu', function() {
    $state = My_Plugin_Entitlement_Service::instance()->get_state();
    
    if ($state->is_active() && $state->can_generate_reports()) {
        add_submenu_page(
            'my-plugin',
            'Premium Reports',
            'Premium Reports',
            'manage_options',
            'my-plugin-reports',
            'my_plugin_render_reports_page'
        );
    }
});

function my_plugin_render_reports_page() {
    // Verify authority again at render time
    $state = My_Plugin_Entitlement_Service::instance()->get_state();
    
    if (!$state->can_generate_reports()) {
        wp_die(
            'This feature requires an active entitlement with Premium Reports.',
            'Feature Not Available',
            ['response' => 403]
        );
    }
    
    ?>
    <div class="wrap">
        <h1>Premium Reports</h1>
        <div id="reports-container">
            <!-- Report UI -->
        </div>
    </div>
    <?php
}
```

### Step 4: AJAX Handler with Validation

```php
// includes/ajax-handlers.php

add_action('wp_ajax_my_plugin_generate_report', function() {
    check_ajax_referer('my_plugin_reports', 'nonce');
    
    if (!current_user_can('manage_options')) {
        wp_send_json_error('Insufficient permissions', 403);
    }
    
    $state = My_Plugin_Entitlement_Service::instance()->get_state();
    
    if (!$state->can_generate_reports()) {
        wp_send_json_error([
            'message' => 'Premium Reports feature not available',
            'status' => $state->get_status(),
            'reason_code' => $state->get_reason_code()
        ], 403);
    }
    
    // Generate report
    $report = my_plugin_generate_report_data();
    
    wp_send_json_success([
        'report' => $report,
        'generated_at' => current_time('mysql')
    ]);
});
```

### Step 5: Graceful Degradation

```php
public function get_state() {
    if ($this->state === null) {
        $this->state = $this->load_state();
    }
    
    // If degraded (network error), allow limited access
    if ($this->state['status'] === 'degraded') {
        add_action('admin_notices', function() {
            echo '<div class="notice notice-warning is-dismissible">';
            echo '<p><strong>Entitlement Verification Warning:</strong> ';
            echo 'Unable to verify entitlement status. Running in limited mode.</p>';
            echo '</div>';
        });
    }
    
    return new My_Plugin_Entitlement_State($this->state);
}
```

## Debugging & Error Handling

WordPress plugins should never use `die()` or `exit()` outside of controlled contexts. Here's how to debug properly:

### Use error_log() Instead of var_dump()

```php
// Bad
var_dump($license_state);

// Good
error_log('License state: ' . print_r($license_state, true));
```

**Why:** Logging doesn't break the site and creates audit trails.

### Enable WP_DEBUG During Development

```php
// wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

Then log validation details:

```php
if (defined('WP_DEBUG') && WP_DEBUG) {
    error_log('My Plugin - Entitlement validation response:');
    error_log(print_r($response, true));
}
```

### Show Admin Notices for License Issues

```php
add_action('admin_notices', function() {
    $state = My_Plugin_Entitlement_Service::instance()->get_state();
    
    if ($state->is_expired()) {
        echo '<div class="notice notice-error">';
        echo '<p><strong>Entitlement Expired:</strong> ';
        echo 'Your entitlement has expired. <a href="' . admin_url('admin.php?page=my-plugin-entitlement') . '">Renew now</a></p>';
        echo '</div>';
    } elseif ($state->is_suspended()) {
        echo '<div class="notice notice-error">';
        echo '<p><strong>Entitlement Suspended:</strong> ';
        echo 'Your entitlement has been suspended. Please contact support.</p>';
        echo '</div>';
    }
});
```

### Handle Network Failures Gracefully

```php
try {
    $response = $this->client->verify($data);
    $state = $this->parse_response($response);
} catch (Exception $e) {
    // Don't crash—use cached state
    $cached_state = get_transient('my_plugin_entitlement_state_backup');
    
    if ($cached_state !== false) {
        error_log('My Plugin: Using backup cache due to network error');
        $state = $cached_state;
    } else {
        error_log('My Plugin: Network error and no cache, entering degraded mode');
        $state = ['status' => 'degraded'];
    }
    
    // Store backup cache for 7 days
    set_transient('my_plugin_entitlement_state_backup', $state, 7 * DAY_IN_SECONDS);
}
```

## What NOT to Do

Let's be explicit about WordPress-specific anti-patterns:

### ❌ Single Check in Main Plugin File

```php
// BAD
if (!resolve_authority()) {
    return;
}
```

**Why wrong:** Easily bypassed by editing one file.

### ❌ Trusting Transients Completely

```php
// BAD
if (get_transient('authority_granted') === true) {
    // Grant access
}
```

**Why wrong:** Transients are stored in the database and can be manipulated.

### ❌ Only Protecting Admin Pages

```php
// BAD
add_action('admin_init', function() {
    if (!has_authority()) die();
});
```

**Why wrong:** Leaves AJAX, REST API, shortcodes, and cron unprotected.

### ❌ Hard Crashes

```php
// BAD
die('Entitlement invalid!');
```

**Why wrong:** Breaks the entire site. No recovery path.

### ❌ Storing Unencrypted Keys in Database

```php
// BAD
update_option('my_plugin_entitlement_key', $_POST['entitlement']);
```

**Why wrong:** Keys are easily extracted from database exports.

### ❌ Ignoring Response Codes

```php
// BAD
if ($response['success']) { }
```

**Why wrong:** Misses critical details like expiry, suspension, or activation limits.

### ❌ Infinite Caching

```php
// BAD
set_transient('entitlement_state', $state, YEAR_IN_SECONDS);
```

**Why wrong:** If license is revoked, plugin never knows.

## Conclusion

Building tamper-resistant WordPress plugins requires **defense-in-depth**: multiple checks at multiple entry points, state-based validation, graceful degradation, and proper error handling.

Key principles for WordPress plugins:

1. **Never rely on a single check** — Validate at admin pages, AJAX handlers, REST endpoints, shortcodes, and cron jobs
2. **Use state objects, not booleans** — Ask specific questions like "Can this feature be used?"
3. **Check response codes** — 200, 202, 205, etc. provide precise failure reasons
4. **Cache for performance, not security** — Always validate cache integrity
5. **Handle failures gracefully** — Use grace periods, degraded modes, and admin notices
6. **Never crash the site** — Use warnings and limited functionality, not hard stops
7. **Protect all entry points** — Admin, AJAX, REST, shortcodes, widgets, and cron

Remember: WordPress plugins are open source by nature. Your goal isn't to make bypass impossible—it's to make it expensive, obvious, and not worth the effort.

Build with the assumption that administrators can modify your code, and design your validation logic to scatter checks across enough locations that removing them all becomes tedious and error-prone.
