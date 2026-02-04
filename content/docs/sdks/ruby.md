---
title: Ruby SDK
description: Official Ruby SDK for the License Management Platform API.
---

# Ruby SDK

The official Ruby SDK for the License Management Platform provides a robust, enterprise-grade interface for license validation, activation, and management.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/ruby-sdk](https://github.com/getkeymanager/ruby-sdk)

---

## 🚀 Features

- **License Operations**: Online and offline validation, activation, and deactivation.
- **Advanced Management**: Create, update, list, and delete licenses programmatically.
- **Enterprise Security**: RSA-4096-SHA256 signature verification.
- **Resiliency**: Automatic retry with exponential backoff and built-in caching.
- **Full API Coverage**: 100% coverage of all 37 API endpoints including metadata, products, generators, contracts, telemetry, and downloadables.

---

## 📦 Installation

Install via RubyGems:

```bash
gem install getkeymanager
```

Or add to your Gemfile:

```ruby
gem 'getkeymanager'
```

Then run:

```bash
bundle install
```

---

## 🛠️ Usage Example

```ruby
require 'getkeymanager'

client = GetKeyManager::Client.new(
  api_key: 'your-api-key',
  base_url: 'https://api.getkeymanager.com',
  verify_signatures: true,
  public_key_file: '/path/to/public_key.pem'
)

# Validate a license
result = client.validate_license('XXXXX-XXXXX-XXXXX-XXXXX')

response = result['response']
data = response['data']

if data['valid']
  puts "License is valid!"
  license = data['license']
  puts "Status: #{license['status']}"
  puts "Expires: #{license['expires_at'] || 'Never'}"
end
```

---

## 🎯 Core Operations

### License Validation

```ruby
# Validate with hardware binding
result = client.validate_license(
  'XXXXX-XXXXX-XXXXX-XXXXX',
  hardware_id: client.generate_hardware_id
)
```

### License Activation

```ruby
# Activate on current machine
hardware_id = client.generate_hardware_id

result = client.activate_license(
  'XXXXX-XXXXX-XXXXX-XXXXX',
  hardware_id: hardware_id,
  metadata: { app_version: '1.0.0' }
)
```

### License Deactivation

```ruby
# Deactivate from current machine
result = client.deactivate_license(
  'XXXXX-XXXXX-XXXXX-XXXXX',
  hardware_id: client.generate_hardware_id
)
```

---

## 🏢 Management Operations

### Create Licenses

```ruby
# Generate new license keys
result = client.create_license(
  product_id: 'product-uuid',
  generator_id: 'generator-uuid',
  count: 10,
  metadata: { batch: 'Q1-2024' }
)

licenses = result['response']['data']['licenses']
licenses.each do |license|
  puts "Created: #{license['key']}"
end
```

### List Licenses

```ruby
# Get licenses with filters
result = client.list_licenses(
  product_id: 'product-uuid',
  status: 'active',
  page: 1,
  per_page: 50
)
```

### Update License

```ruby
# Update license properties
result = client.update_license(
  'XXXXX-XXXXX-XXXXX-XXXXX',
  status: 'suspended',
  notes: 'Payment overdue'
)
```

---

## 🎛️ Advanced Features

### License Assignment

```ruby
# Assign license to customer
result = client.assign_license_key(
  'XXXXX-XXXXX-XXXXX-XXXXX',
  customer_email: 'customer@example.com',
  customer_name: 'John Doe'
)

# Random assignment
result = client.random_assign_license_keys(
  product_id: 'product-uuid',
  count: 5,
  customer_email: 'customer@example.com'
)
```

### Metadata Management

```ruby
# Add custom metadata to license
client.create_license_key_meta(
  'XXXXX-XXXXX-XXXXX-XXXXX',
  meta_key: 'tier',
  meta_value: 'enterprise'
)

# Add metadata to product
client.create_product_meta(
  product_id: 'product-uuid',
  meta_key: 'support_level',
  meta_value: 'premium'
)
```

### Product Management

```ruby
# Create product
result = client.create_product(
  name: 'Premium Software',
  description: 'Enterprise edition with all features'
)

# List all products
result = client.get_all_products(page: 1, per_page: 50)
```

### Contract Management

```ruby
# Create contract
result = client.create_contract(
  name: 'Enterprise Q1 2024',
  product_id: 'product-uuid',
  generator_id: 'generator-uuid',
  license_count: 1000
)

# List contracts
result = client.get_all_contracts(page: 1, per_page: 50)
```

### Generator Operations

```ruby
# List generators
result = client.get_all_generators(product_id: 'product-uuid')

# Generate licenses using generator
result = client.generate_license_keys(
  product_id: 'product-uuid',
  generator_id: 'generator-uuid',
  count: 100
)
```

### Telemetry

```ruby
# Submit telemetry
client.submit_telemetry(
  'XXXXX-XXXXX-XXXXX-XXXXX',
  event_type: 'app_launch',
  app_version: '1.0.0',
  os: 'macOS'
)

# Retrieve telemetry data
result = client.get_telemetry_data(
  license_key: 'XXXXX-XXXXX-XXXXX-XXXXX',
  page: 1,
  per_page: 50
)
```

### Downloadables

```ruby
# Access downloadable files
result = client.access_downloadables(
  product_id: 'product-uuid',
  license_key: 'XXXXX-XXXXX-XXXXX-XXXXX',
  version: '1.0.0'
)
```

---

## 🔒 Security Features

### Signature Verification

The SDK automatically verifies RSA-4096-SHA256 signatures on all API responses when a public key is provided:

```ruby
client = GetKeyManager::Client.new(
  api_key: 'your-api-key',
  public_key_file: '/path/to/public_key.pem',
  verify_signatures: true  # Enabled by default
)
```

### Hardware ID Generation

```ruby
# Generate unique hardware identifier
hardware_id = client.generate_hardware_id
puts "Hardware ID: #{hardware_id}"
```

---

## ⚙️ Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `api_key` | String | *required* | Your API key |
| `base_url` | String | `https://api.getkeymanager.com` | API base URL |
| `public_key` | String | `nil` | RSA public key (PEM format) |
| `public_key_file` | String | `nil` | Path to public key file |
| `verify_signatures` | Boolean | `true` | Enable signature verification |
| `cache_enabled` | Boolean | `true` | Enable response caching |
| `cache_ttl` | Integer | `300` | Cache TTL in seconds |
| `timeout` | Integer | `30` | Request timeout in seconds |
| `retry_attempts` | Integer | `3` | Number of retry attempts |
| `retry_delay` | Integer | `1000` | Delay between retries (ms) |
| `environment` | String | `nil` | Environment filter |
| `product_id` | String | `nil` | Default product ID |

---

## 🚨 Error Handling

```ruby
begin
  result = client.validate_license('XXXXX-XXXXX-XXXXX-XXXXX')
rescue GetKeyManager::ValidationException => e
  puts "Validation error: #{e.message}"
rescue GetKeyManager::NetworkException => e
  puts "Network error: #{e.message}"
rescue GetKeyManager::SignatureException => e
  puts "Signature verification failed: #{e.message}"
rescue GetKeyManager::RateLimitException => e
  puts "Rate limit exceeded: #{e.message}"
rescue GetKeyManager::LicenseException => e
  puts "License error: #{e.message}"
  puts "Error code: #{e.code}"
end
```

---

## 📋 Requirements

- Ruby 2.7 or higher
- httparty ~> 0.20
- openssl >= 2.2

---

## 📚 Additional Resources

- [Complete API Documentation](/docs/api)
- [SDK Examples](https://github.com/getkeymanager/ruby-sdk/tree/main/examples)
- [Migration Guide](https://github.com/getkeymanager/ruby-sdk/blob/main/MIGRATION.md)

---

## 🤝 Support

- **Documentation**: [https://docs.getkeymanager.com](https://docs.getkeymanager.com)
- **Email**: support@getkeymanager.com
- **Issues**: [GitHub Issues](https://github.com/getkeymanager/ruby-sdk/issues)
