---
title: "Protecting WordPress Themes with Multi-Point License Checks"
description: "Learn how to implement robust license validation in WordPress themes through template guards, customizer protection, widget enforcement, and theme mod validation to prevent unauthorized usage."
keywords:
  - WordPress theme security
  - theme license validation
  - WordPress theme protection
  - customizer security
  - theme licensing
  - template protection
tags:
  - WordPress
  - Theme Development
  - PHP
  - Security
  - License Management
category: "Security Integration"
created_at: "2026-01-25"
updated_at: "2026-01-25"
seo_image: "/images/seo/wordpress-theme-license-security.png"
---

## Introduction

WordPress theme developers face an even greater challenge than plugin developers: themes are expected to "just work" visually, and users have less tolerance for licensing barriers that break their site's appearance.

A poorly implemented license check can render a site completely unusable—blank pages, broken layouts, or missing stylesheets. Yet without proper enforcement, premium themes are trivially copied and redistributed.

This guide shows you how to implement **smart, layered license validation** in WordPress themes that protects your intellectual property without destroying the user experience when licenses expire or validation fails.

You'll learn how to validate at theme initialization, protect template files, guard customizer options, secure theme widgets, and implement graceful degradation that maintains basic functionality even when licenses lapse.

## Common Mistakes Developers Make

Let's understand why naive theme licensing implementations fail.

### Mistake 1: Blocking Theme Activation Entirely

```php
// functions.php
if (!resolve_authority()) {
    return; // Stop theme initialization
}
```

**Why this fails:** If validation fails (expired license, network error, server downtime), the theme doesn't load at all. The site becomes a blank page. This is unacceptable for WordPress themes, which must always provide basic functionality.

### Mistake 2: Removing Core Theme Features on Expiry

```php
if (!has_authority()) {
    // Remove all stylesheets
    remove_action('wp_enqueue_scripts', 'theme_enqueue_styles');
}
```

**Why this fails:** Users who paid for the theme expect it to continue working for basic functionality, even if their license expires. Breaking core features creates terrible experiences and negative reviews.

### Mistake 3: Only Checking in functions.php

```php
// functions.php - one check
if (!verify_authority()) {
    add_action('admin_notices', 'show_entitlement_notice');
}
```

**Why this fails:** Users can edit functions.php from the WordPress theme editor or via FTP and remove the check. A single validation point is easily bypassed.

### Mistake 4: Hard-Coding License Keys in Theme Files

```php
define('THEME_ENTITLEMENT_KEY', 'XXXX-XXXX-XXXX-XXXX');
```

**Why this fails:** Hardcoded keys are visible in version control, child themes, and distributed zip files. Anyone can extract and reuse them.

### Mistake 5: Showing Intrusive Notices on Frontend

```php
if (!has_authority()) {
    add_action('wp_footer', function() {
        echo '<div style="position:fixed;top:0;width:100%;background:red;color:white;padding:20px;">
              UNAUTHORIZED THEME
              </div>';
    });
}
```

**Why this fails:** Frontend visitors shouldn't see licensing issues. This reflects poorly on site owners and creates support nightmares. Licensing is an administrative concern, not a visitor concern.

### Mistake 6: Disabling All Premium Features on First Validation Failure

```php
$authority_granted = get_transient('theme_authority_granted');

if ($authority_granted === false) {
    // Disable everything immediately
    return;
}
```

**Why this fails:** Network glitches, server maintenance, or API rate limits shouldn't immediately disable premium features. Grace periods and cached validation prevent false negatives.

## Where to Add Enforcement Logic

WordPress themes have specific entry points where validation should occur:

### 1. Theme Initialization (functions.php)

**Location:** `functions.php`

**Purpose:** Initialize license state singleton.

```php
// functions.php

// Include entitlement service
require_once get_template_directory() . '/inc/class-theme-entitlement-service.php';

// Initialize entitlement on after_setup_theme
add_action('after_setup_theme', function() {
    Theme_Entitlement_Service::instance()->initialize();
}, 1);
```

**Why here:** Initialize early but don't crash the theme if validation fails.

### 2. Customizer Registration

**Location:** Customizer hook

**Purpose:** Only register premium customizer panels/sections for licensed users.

```php
add_action('customize_register', function($wp_customize) {
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Always register basic customizer options
    $wp_customize->add_section('basic_colors', [
        'title' => 'Basic Colors',
        'priority' => 30,
    ]);
    
    // Only register premium sections if authorized
    if ($state->is_active() && $state->has_feature('premium_customizer')) {
        $wp_customize->add_section('advanced_typography', [
            'title' => 'Advanced Typography',
            'priority' => 35,
        ]);
        
        $wp_customize->add_section('layout_options', [
            'title' => 'Layout Options',
            'priority' => 40,
        ]);
    }
});
```

**Why here:** Prevents unlicensed users from accessing premium customizer features while maintaining basic theme functionality.

### 3. Widget Registration

**Location:** widgets_init hook

**Purpose:** Register premium widgets only for licensed installations.

```php
add_action('widgets_init', function() {
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Always register basic widgets
    register_widget('Theme_Basic_Widget');
    register_widget('Theme_Recent_Posts_Widget');
    
    // Only register premium widgets if authorized
    if ($state->is_active() && $state->has_feature('premium_widgets')) {
        register_widget('Theme_Advanced_Slider_Widget');
        register_widget('Theme_Portfolio_Widget');
        register_widget('Theme_Testimonials_Widget');
    }
});
```

**Why here:** Unlicensed users won't see premium widgets in the widget selector.

### 4. Template Loading (Template Redirect)

**Location:** template_redirect hook

**Purpose:** Validate access to premium template features.

```php
add_action('template_redirect', function() {
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Verify authority if current page uses premium template
    if (is_page_template('templates/premium-landing-page.php')) {
        if (!$state->can_use_premium_templates()) {
            // Fallback to default template
            add_filter('template_include', function($template) {
                return get_page_template();
            });
            
            // Add admin notice (only for admins)
            if (current_user_can('manage_options')) {
                add_action('wp_footer', function() {
                    if (is_user_logged_in() && current_user_can('manage_options')) {
                        echo '<!-- Premium template requires active entitlement -->';
                    }
                });
            }
        }
    }
});
```

**Why here:** Prevents premium templates from rendering for unlicensed users while gracefully falling back to default templates.

### 5. Enqueue Scripts/Styles (wp_enqueue_scripts)

**Location:** wp_enqueue_scripts hook

**Purpose:** Only enqueue premium assets if licensed.

```php
add_action('wp_enqueue_scripts', function() {
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Always enqueue core theme styles
    wp_enqueue_style('theme-core', get_stylesheet_uri());
    
    // Always enqueue basic JavaScript
    wp_enqueue_script('theme-basic', get_template_directory_uri() . '/js/basic.js', ['jquery'], null, true);
    
    // Only enqueue premium assets if authorized
    if ($state->is_active() && $state->has_feature('premium_effects')) {
        wp_enqueue_script('theme-premium', get_template_directory_uri() . '/js/premium.js', ['jquery'], null, true);
        wp_enqueue_style('theme-premium', get_template_directory_uri() . '/css/premium.css');
    }
    
    // Pass entitlement state to JavaScript (for frontend behavior)
    if (current_user_can('manage_options')) {
        wp_localize_script('theme-basic', 'themeEntitlement', [
            'isActive' => $state->is_active(),
            'features' => $state->get_features()
        ]);
    }
});
```

**Why here:** Premium JavaScript and CSS only load when licensed, reducing asset footprint for unlicensed installations.

### 6. Theme Options Page (Admin Menu)

**Location:** admin_menu hook

**Purpose:** Protect premium theme settings.

```php
add_action('admin_menu', function() {
    // Always show basic theme options
    add_theme_page(
        'Theme Settings',
        'Theme Settings',
        'manage_options',
        'theme-settings',
        'render_theme_settings_page'
    );
    
    // Show entitlement status prominently
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    if (!$state->is_active()) {
        add_action('admin_notices', function() use ($state) {
            echo '<div class="notice notice-warning is-dismissible">';
            echo '<p><strong>Theme Entitlement:</strong> ';
            if ($state->is_expired()) {
                echo 'Your entitlement has expired. <a href="' . admin_url('themes.php?page=theme-entitlement') . '">Renew now</a>';
            } elseif ($state->is_not_activated()) {
                echo 'Please activate your entitlement to access premium features. <a href="' . admin_url('themes.php?page=theme-entitlement') . '">Activate</a>';
            }
            echo '</p></div>';
        });
    }
});

function render_theme_settings_page() {
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    ?>
    <div class="wrap">
        <h1>Theme Settings</h1>
        
        <?php if (!$state->is_active()): ?>
            <div class="notice notice-info">
                <p>Some options require an active entitlement. <a href="<?php echo admin_url('themes.php?page=theme-entitlement'); ?>">Activate your entitlement</a></p>
            </div>
        <?php endif; ?>
        
        <form method="post" action="options.php">
            <!-- Basic options always available -->
            <h2>Basic Options</h2>
            <!-- ... basic fields ... -->
            
            <?php if ($state->is_active() && $state->has_feature('advanced_options')): ?>
                <h2>Advanced Options</h2>
                <!-- ... premium fields ... -->
            <?php endif; ?>
            
            <?php submit_button(); ?>
        </form>
    </div>
    <?php
}
```

**Why here:** Guides users to activate licenses while allowing basic theme configuration.

### 7. Template Parts (get_template_part)

**Location:** Template files

**Purpose:** Conditionally load premium template parts.

```php
// In template files (e.g., header.php, footer.php, single.php)

$entitlement = Theme_Entitlement_Service::instance();
$state = $entitlement->get_state();

if ($state->has_feature('premium_header')) {
    get_template_part('template-parts/header', 'premium');
} else {
    get_template_part('template-parts/header', 'basic');
}
```

**Why here:** Provides fallback templates for unlicensed users without breaking the site.

### 8. AJAX Handlers (wp_ajax_*)

**Location:** AJAX action hooks

**Purpose:** Protect theme-specific AJAX endpoints.

```php
add_action('wp_ajax_theme_save_layout', function() {
    check_ajax_referer('theme_layout_nonce', 'nonce');
    
    if (!current_user_can('manage_options')) {
        wp_send_json_error('Insufficient permissions', 403);
    }
    
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    if (!$state->can_save_custom_layouts()) {
        wp_send_json_error([
            'message' => 'Custom layouts require an active entitlement',
            'status' => $state->get_status()
        ], 403);
    }
    
    // Process layout save
    $layout_data = $_POST['layout'] ?? [];
    update_option('theme_custom_layout', $layout_data);
    
    wp_send_json_success(['message' => 'Layout saved']);
});
```

**Why here:** Premium AJAX features are protected even if frontend JavaScript is modified.

## What Data Should Be Passed

When validating theme licenses, provide appropriate context:

### Domain Name

Always validate against the current domain:

```php
$domain = parse_url(home_url(), PHP_URL_HOST);

$response = $entitlement_client->verify([
    'entitlement_key' => $entitlement_key,
    'identifier' => $domain,
    'product_uuid' => THEME_PRODUCT_UUID
]);
```

**Why:** Prevents a single license from being used across multiple sites.

### Theme Version

Pass the current theme version:

```php
$theme = wp_get_theme();

$response = $entitlement_client->verify([
    'entitlement_key' => $entitlement_key,
    'identifier' => $domain,
    'metadata' => [
        'theme_version' => $theme->get('Version'),
        'theme_name' => $theme->get('Name')
    ]
]);
```

**Why:** Helps track which theme versions are in use and enforce minimum version requirements.

### Environment Information

Include WordPress and PHP versions:

```php
$response = $entitlement_client->verify([
    'entitlement_key' => $entitlement_key,
    'identifier' => $domain,
    'metadata' => [
        'wp_version' => get_bloginfo('version'),
        'php_version' => PHP_VERSION,
        'theme_version' => wp_get_theme()->get('Version')
    ]
]);
```

**Why:** Enables better support and diagnostics.

### What Must Never Be Stored in Theme Files

❌ Never hardcode in theme files:
- License keys
- API keys
- Activation identifiers

✅ Store in database options:
```php
// Store encrypted
$encrypted = openssl_encrypt(
    $entitlement_key,
    'AES-256-CBC',
    wp_salt('auth'),
    0,
    substr(wp_salt('secure_auth'), 0, 16)
);
update_option('theme_entitlement_encrypted', $encrypted);
```

## How to Structure Safe Checks

Themes require special validation patterns to maintain usability:

### Always Provide Fallbacks

Bad:
```php
if ($entitlement->isAuthorized()) {
    // Show premium feature
} else {
    // Show nothing - breaks site
}
```

Good:
```php
if ($state->has_feature('premium_slider')) {
    get_template_part('template-parts/slider', 'premium');
} else {
    // Always show something - basic slider
    get_template_part('template-parts/slider', 'basic');
}
```

**Why:** Themes must always render something. Never leave empty spaces.

### Use Feature Flags, Not Global Booleans

```php
// Bad
if ($has_authority) {
    show_all_premium_features();
}

// Good
if ($state->has_feature('advanced_typography')) {
    load_typography_options();
}

if ($state->has_feature('custom_layouts')) {
    enable_layout_builder();
}

if ($state->has_feature('premium_widgets')) {
    register_premium_widgets();
}
```

**Why:** Enables tiered licensing (Basic, Pro, Agency) with granular feature control.

### Cache Wisely with Validation

```php
public function get_state() {
    // Try cache
    $cached = get_transient('theme_entitlement_state');
    
    if ($cached !== false && $this->is_cache_valid($cached)) {
        return new Entitlement_State($cached);
    }
    
    // Resolve authority remotely
    $state = $this->resolve_authority_remotely();
    
    // Cache for 12 hours (shorter than plugins due to theme's critical nature)
    set_transient('theme_entitlement_state', $state, 12 * HOUR_IN_SECONDS);
    
    return new Entitlement_State($state);
}

private function is_cache_valid($cached) {
    // Verify cache structure and age
    if (!isset($cached['status']) || !isset($cached['timestamp'])) {
        return false;
    }
    
    $age = time() - $cached['timestamp'];
    return $age < 12 * HOUR_IN_SECONDS;
}
```

**Why:** Shorter cache times for themes prevent long delays in license updates while maintaining performance.

### Implement Extended Grace Periods for Themes

```php
public function get_state() {
    $state = $this->validate_remotely();
    
    if ($state['status'] === 'expired') {
        $expired_at = strtotime($state['expires_at'] ?? 'now');
        $days_expired = floor((time() - $expired_at) / DAY_IN_SECONDS);
        
        if ($days_expired <= 14) {
            // Longer grace period for themes (14 days vs 7 for plugins)
            add_action('admin_notices', function() use ($days_expired) {
                echo '<div class="notice notice-warning">';
                echo '<p><strong>Theme License Expired:</strong> ';
                echo 'Your license expired ' . $days_expired . ' days ago. ';
                echo 'Premium features will be disabled in ' . (14 - $days_expired) . ' days. ';
                echo '<a href="' . admin_url('themes.php?page=theme-license') . '">Renew now</a></p>';
                echo '</div>';
            });
            
            // Treat as active with warning
            $state['status'] = 'active';
            $state['grace_period'] = true;
            $state['grace_days_remaining'] = 14 - $days_expired;
        }
    }
    
    return $state;
}
```

**Why:** Themes affect site appearance directly. Longer grace periods prevent sudden visual breakage.

## Example Integration Flow

Here's a complete theme integration:

### Step 1: License Service Class

```php
// inc/class-theme-entitlement-service.php

class Theme_Entitlement_Service {
    private static $instance = null;
    private $state = null;
    private $client = null;
    
    public static function instance() {
        if (self::$instance === null) {
            self::$instance = new self();
        }
        return self::$instance;
    }
    
    private function __construct() {
        require_once get_template_directory() . '/inc/class-entitlement-client.php';
        $this->client = new Theme_Entitlement_Client([
            'api_key' => defined('THEME_API_KEY') ? THEME_API_KEY : '',
            'product_uuid' => defined('THEME_PRODUCT_UUID') ? THEME_PRODUCT_UUID : ''
        ]);
    }
    
    public function initialize() {
        $this->state = $this->load_state();
        
        // Add admin notices for entitlement issues (admin only)
        if (is_admin() && current_user_can('manage_options')) {
            add_action('admin_notices', [$this, 'show_entitlement_notices']);
        }
    }
    
    private function load_state() {
        // Try cache
        $cached = get_transient('theme_entitlement_state');
        if ($cached !== false && $this->is_cache_valid($cached)) {
            return $cached;
        }
        
        // Resolve authority remotely
        return $this->resolve_authority_remotely();
    }
    
    private function resolve_authority_remotely() {
        $entitlement_key = get_option('theme_entitlement_key', '');
        
        if (empty($entitlement_key)) {
            return $this->create_state('not_activated');
        }
        
        try {
            $domain = parse_url(home_url(), PHP_URL_HOST);
            $theme = wp_get_theme();
            
            $response = $this->client->verify([
                'entitlement_key' => $entitlement_key,
                'identifier' => $domain,
                'product_uuid' => THEME_PRODUCT_UUID,
                'metadata' => [
                    'theme_version' => $theme->get('Version'),
                    'wp_version' => get_bloginfo('version')
                ]
            ]);
            
            $code = $response['response']['code'] ?? null;
            $data = $response['response']['data'] ?? [];
            
            $state = $this->map_response_to_state($code, $data);
            
            // Cache for 12 hours
            set_transient('theme_entitlement_state', $state, 12 * HOUR_IN_SECONDS);
            
            return $state;
            
        } catch (Exception $e) {
            error_log('Theme entitlement validation error: ' . $e->getMessage());
            
            // Use backup cache or degraded mode
            $backup = get_transient('theme_entitlement_backup');
            if ($backup !== false) {
                return $backup;
            }
            
            return $this->create_state('degraded');
        }
    }
    
    private function map_response_to_state($code, $data) {
        switch ($code) {
            case 200:
                return [
                    'status' => 'active',
                    'features' => $data['features'] ?? [],
                    'expires_at' => $data['expires_at'] ?? null,
                    'timestamp' => time()
                ];
                
            case 205:
                // Handle grace period
                $expires_at = strtotime($data['expires_at'] ?? 'now');
                $days_expired = floor((time() - $expires_at) / DAY_IN_SECONDS);
                
                if ($days_expired <= 14) {
                    return [
                        'status' => 'active',
                        'grace_period' => true,
                        'days_expired' => $days_expired,
                        'features' => $data['features'] ?? [],
                        'expires_at' => $data['expires_at'],
                        'timestamp' => time()
                    ];
                }
                
                return [
                    'status' => 'expired',
                    'expires_at' => $data['expires_at'],
                    'timestamp' => time()
                ];
                
            case 204:
                return ['status' => 'suspended', 'timestamp' => time()];
                
            case 202:
                return ['status' => 'not_activated', 'timestamp' => time()];
                
            default:
                return ['status' => 'invalid', 'code' => $code, 'timestamp' => time()];
        }
    }
    
    private function create_state($status, $data = []) {
        return array_merge(['status' => $status, 'timestamp' => time()], $data);
    }
    
    public function get_state() {
        if ($this->state === null) {
            $this->initialize();
        }
        return new Theme_Entitlement_State($this->state);
    }
    
    public function show_entitlement_notices() {
        $state = $this->get_state();
        
        if ($state->is_in_grace_period()) {
            $days = $state->get_grace_days_remaining();
            echo '<div class="notice notice-warning is-dismissible">';
            echo '<p><strong>Theme Entitlement Expired:</strong> ';
            echo 'Your entitlement expired. Premium features will be disabled in ' . $days . ' days. ';
            echo '<a href="' . admin_url('themes.php?page=theme-entitlement') . '">Renew now</a></p>';
            echo '</div>';
        } elseif ($state->is_expired()) {
            echo '<div class="notice notice-error">';
            echo '<p><strong>Theme Entitlement Expired:</strong> ';
            echo 'Premium features are disabled. <a href="' . admin_url('themes.php?page=theme-entitlement') . '">Renew now</a></p>';
            echo '</div>';
        } elseif ($state->is_not_activated()) {
            echo '<div class="notice notice-info is-dismissible">';
            echo '<p><strong>Theme Entitlement:</strong> ';
            echo 'Activate your entitlement to access premium features. <a href="' . admin_url('themes.php?page=theme-entitlement') . '">Activate</a></p>';
            echo '</div>';
        }
    }
}
```

### Step 2: State Object

```php
// inc/class-theme-entitlement-state.php

class Theme_Entitlement_State {
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
    
    public function is_not_activated() {
        return isset($this->data['status']) && $this->data['status'] === 'not_activated';
    }
    
    public function is_in_grace_period() {
        return isset($this->data['grace_period']) && $this->data['grace_period'] === true;
    }
    
    public function get_grace_days_remaining() {
        if (!$this->is_in_grace_period()) {
            return 0;
        }
        
        $days_expired = $this->data['days_expired'] ?? 0;
        return max(0, 14 - $days_expired);
    }
    
    public function has_feature($feature) {
        if (!$this->is_active()) {
            return false;
        }
        
        $features = $this->data['features'] ?? [];
        return in_array($feature, $features, true);
    }
    
    public function can_use_premium_templates() {
        return $this->has_feature('premium_templates');
    }
    
    public function can_save_custom_layouts() {
        return $this->has_feature('custom_layouts');
    }
    
    public function get_status() {
        return $this->data['status'] ?? 'unknown';
    }
    
    public function get_features() {
        return $this->data['features'] ?? [];
    }
}
```

### Step 3: Functions.php Integration

```php
// functions.php

// Define constants
define('THEME_PRODUCT_UUID', 'your-product-uuid');

// Include entitlement service
require_once get_template_directory() . '/inc/class-theme-entitlement-service.php';
require_once get_template_directory() . '/inc/class-theme-entitlement-state.php';

// Initialize on after_setup_theme
add_action('after_setup_theme', function() {
    Theme_Entitlement_Service::instance()->initialize();
}, 1);

// Conditionally register premium features
add_action('after_setup_theme', function() {
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Always register basic theme support
    add_theme_support('post-thumbnails');
    add_theme_support('title-tag');
    add_theme_support('custom-logo');
    
    // Only register premium features if authorized
    if ($state->has_feature('custom_headers')) {
        add_theme_support('custom-header');
    }
    
    if ($state->has_feature('custom_backgrounds')) {
        add_theme_support('custom-background');
    }
});

// Enqueue assets conditionally
add_action('wp_enqueue_scripts', function() {
    $entitlement = Theme_Entitlement_Service::instance();
    $state = $entitlement->get_state();
    
    // Always load core styles
    wp_enqueue_style('theme-style', get_stylesheet_uri());
    
    // Only load premium assets if authorized
    if ($state->is_active() && $state->has_feature('premium_effects')) {
        wp_enqueue_script('theme-premium', get_template_directory_uri() . '/js/premium.js', ['jquery'], null, true);
    }
});
```

### Step 4: Template File with Fallback

```php
// header.php

$entitlement = Theme_Entitlement_Service::instance();
$state = $entitlement->get_state();
?>

<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
    <meta charset="<?php bloginfo('charset'); ?>">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <?php wp_head(); ?>
</head>

<body <?php body_class(); ?>>
<?php wp_body_open(); ?>

<header class="site-header">
    <?php if ($state->has_feature('premium_header')): ?>
        <!-- Premium header with advanced options -->
        <?php get_template_part('template-parts/header', 'premium'); ?>
    <?php else: ?>
        <!-- Basic header -->
        <?php get_template_part('template-parts/header', 'basic'); ?>
    <?php endif; ?>
</header>
```

## Debugging & Error Handling

For themes, debugging must be especially careful to avoid breaking the frontend:

### Never Use die() or exit() in Theme Files

```php
// BAD
if (!has_authority()) {
    die('Theme not authorized');
}

// GOOD
if (!$state->is_active()) {
    // Log the issue
    error_log('Theme entitlement not active, using fallback features');
    
    // Show admin notice (backend only)
    if (is_admin() && current_user_can('manage_options')) {
        add_action('admin_notices', function() {
            echo '<div class="notice notice-warning"><p>Theme entitlement inactive.</p></div>';
        });
    }
    
    // Continue with basic functionality
}
```

### Use Template Fallbacks

```php
public function load_template($template_name) {
    $state = $this->get_state();
    
    if ($state->has_feature('premium_templates')) {
        $premium_template = locate_template("template-parts/{$template_name}-premium.php");
        if ($premium_template) {
            return $premium_template;
        }
    }
    
    // Always have a fallback
    return locate_template("template-parts/{$template_name}-basic.php");
}
```

### Log Validation Errors

```php
if (defined('WP_DEBUG') && WP_DEBUG) {
    add_action('theme_entitlement_validation_failed', function($error) {
        error_log('Theme Entitlement Validation Failed: ' . print_r($error, true));
    });
}
```

## What NOT to Do

Theme-specific anti-patterns:

### ❌ Breaking the Frontend

```php
// BAD - Breaks site appearance
if (!has_authority()) {
    return; // Stops theme loading
}
```

### ❌ Showing Licensing Issues to Visitors

```php
// BAD - Visitors shouldn't see this
if (!has_authority()) {
    echo '<div class="entitlement-warning">UNAUTHORIZED THEME</div>';
}
```

### ❌ Disabling Core Styles

```php
// BAD - Makes site unusable
if (!has_authority()) {
    remove_action('wp_enqueue_scripts', 'theme_enqueue_styles');
}
```

### ❌ No Fallback Templates

```php
// BAD - May show blank areas
if ($entitlement->has_premium()) {
    get_template_part('slider');
}
// No else clause - shows nothing if not authorized
```

### ❌ Hard-Coding Keys

```php
// BAD
define('THEME_ENTITLEMENT', 'XXXX-XXXX-XXXX');
```

## Conclusion

WordPress theme licensing requires careful balance: protect your work without breaking user sites. Key principles:

1. **Always provide fallbacks** — Basic functionality must always work
2. **Never break the frontend** — Visitors shouldn't see licensing issues
3. **Use extended grace periods** — 14+ days for themes vs 7 for plugins
4. **Show admin notices, not frontend banners** — Communicate with site owners, not visitors
5. **Feature-based restrictions** — Disable premium features, not core functionality
6. **Cache with shorter TTLs** — 12 hours for themes vs 24+ for plugins
7. **Test degraded modes** — Ensure theme looks acceptable even without premium features

Build themes that gracefully degrade, communicate clearly with administrators, and maintain professional appearance regardless of license status.
