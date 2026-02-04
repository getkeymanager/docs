---
title: Python SDK
description: Official Python SDK for the License Management Platform API.
---

# Python SDK

The official Python SDK for the License Management Platform provides a robust, enterprise-grade interface for license validation, activation, and management.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/python-sdk](https://github.com/getkeymanager/python-sdk)

---

## 🚀 Features

- **License Operations**: Online and offline validation, activation, and deactivation.
- **Advanced Management**: Create, update, list, and delete licenses programmatically.
- **Enterprise Security**: RSA-4096-SHA256 signature verification.
- **Resiliency**: Automatic retry with exponential backoff and built-in caching.
- **Full API Coverage**: 100% coverage of all 37 API endpoints including metadata, products, generators, contracts, telemetry, and downloadables.

---

## 📦 Installation

Install via pip:

```bash
pip install getkeymanager-sdk
```

---

## 🛠️ Usage Example

```python
from getkeymanager import LicenseClient

client = LicenseClient({
    'api_key': 'your-api-key',
    'base_url': 'https://api.getkeymanager.com',
    'verify_signatures': True,
    'public_key_file': '/path/to/public_key.pem'
})

# Validate a license
result = client.validate_license('XXXXX-XXXXX-XXXXX-XXXXX')

if result['response']['data']['valid']:
    print("License is valid!")
    license = result['response']['data']['license']
    print(f"Status: {license['status']}")
    print(f"Expires: {license.get('expires_at', 'Never')}")
```

---

## 🎯 Core Operations

### License Validation

```python
# Validate with hardware binding
result = client.validate_license(
    'XXXXX-XXXXX-XXXXX-XXXXX',
    hardware_id=client.generate_hardware_id()
)
```

### License Activation

```python
# Activate on current machine
hardware_id = client.generate_hardware_id()

result = client.activate_license(
    'XXXXX-XXXXX-XXXXX-XXXXX',
    hardware_id=hardware_id,
    metadata={'app_version': '1.0.0'}
)
```

### License Deactivation

```python
# Deactivate from current machine
result = client.deactivate_license(
    'XXXXX-XXXXX-XXXXX-XXXXX',
    hardware_id=client.generate_hardware_id()
)
```

---

## 🏢 Management Operations

### Create Licenses

```python
# Generate new license keys
result = client.create_license(
    product_id='product-uuid',
    generator_id='generator-uuid',
    count=10,
    metadata={'batch': 'Q1-2024'}
)

licenses = result['response']['data']['licenses']
for license in licenses:
    print(f"Created: {license['key']}")
```

### List Licenses

```python
# Get licenses with filters
result = client.list_licenses(
    product_id='product-uuid',
    status='active',
    page=1,
    per_page=50
)
```

### Update License

```python
# Update license properties
result = client.update_license(
    'XXXXX-XXXXX-XXXXX-XXXXX',
    {'status': 'suspended', 'notes': 'Payment overdue'}
)
```

---

## 🎛️ Advanced Features

### License Assignment

```python
# Assign license to customer
result = client.assign_license_key(
    'XXXXX-XXXXX-XXXXX-XXXXX',
    customer_email='customer@example.com',
    customer_name='John Doe'
)

# Random assignment
result = client.random_assign_license_keys(
    product_id='product-uuid',
    count=5,
    customer_email='customer@example.com'
)
```

### Metadata Management

```python
# Add custom metadata to license
client.create_license_key_meta(
    'XXXXX-XXXXX-XXXXX-XXXXX',
    meta_key='tier',
    meta_value='enterprise'
)

# Add metadata to product
client.create_product_meta(
    product_id='product-uuid',
    meta_key='support_level',
    meta_value='premium'
)
```

### Product Management

```python
# Create product
result = client.create_product(
    name='Premium Software',
    description='Enterprise edition with all features'
)

# List all products
result = client.get_all_products(page=1, per_page=50)
```

### Contract Management

```python
# Create contract
result = client.create_contract(
    name='Enterprise Q1 2024',
    product_id='product-uuid',
    generator_id='generator-uuid',
    license_count=1000
)

# List contracts
result = client.get_all_contracts(page=1, per_page=50)
```

### Generator Operations

```python
# List generators
result = client.get_all_generators(product_id='product-uuid')

# Generate licenses using generator
result = client.generate_license_keys(
    product_id='product-uuid',
    generator_id='generator-uuid',
    count=100
)
```

### Telemetry

```python
# Submit telemetry
client.submit_telemetry(
    'XXXXX-XXXXX-XXXXX-XXXXX',
    {
        'event_type': 'app_launch',
        'app_version': '1.0.0',
        'os': 'Windows 10'
    }
)

# Retrieve telemetry data
result = client.get_telemetry_data(
    license_key='XXXXX-XXXXX-XXXXX-XXXXX',
    page=1,
    per_page=50
)
```

### Downloadables

```python
# Access downloadable files
result = client.access_downloadables(
    product_id='product-uuid',
    license_key='XXXXX-XXXXX-XXXXX-XXXXX',
    version='1.0.0'
)
```

---

## 🔒 Security Features

### Signature Verification

The SDK automatically verifies RSA-4096-SHA256 signatures on all API responses when a public key is provided:

```python
client = LicenseClient({
    'api_key': 'your-api-key',
    'public_key_file': '/path/to/public_key.pem',
    'verify_signatures': True  # Enabled by default
})
```

### Hardware ID Generation

```python
# Generate unique hardware identifier
hardware_id = client.generate_hardware_id()
print(f"Hardware ID: {hardware_id}")
```

---

## ⚙️ Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `api_key` | string | *required* | Your API key |
| `base_url` | string | `https://api.getkeymanager.com` | API base URL |
| `public_key` | string | `None` | RSA public key (PEM format) |
| `public_key_file` | string | `None` | Path to public key file |
| `verify_signatures` | bool | `True` | Enable signature verification |
| `cache_enabled` | bool | `True` | Enable response caching |
| `cache_ttl` | int | `300` | Cache TTL in seconds |
| `timeout` | int | `30` | Request timeout in seconds |
| `retry_attempts` | int | `3` | Number of retry attempts |
| `retry_delay` | int | `1000` | Delay between retries (ms) |
| `environment` | string | `None` | Environment filter |
| `product_id` | string | `None` | Default product ID |

---

## 🚨 Error Handling

```python
from getkeymanager import (
    LicenseException,
    ValidationException,
    NetworkException,
    SignatureException,
    RateLimitException
)

try:
    result = client.validate_license('XXXXX-XXXXX-XXXXX-XXXXX')
except ValidationException as e:
    print(f"Validation error: {e}")
except NetworkException as e:
    print(f"Network error: {e}")
except SignatureException as e:
    print(f"Signature verification failed: {e}")
except RateLimitException as e:
    print(f"Rate limit exceeded: {e}")
except LicenseException as e:
    print(f"License error: {e}")
    print(f"Error code: {e.code}")
```

---

## 📋 Requirements

- Python 3.7 or higher
- requests >= 2.25.0
- cryptography >= 3.4.0

---

## 📚 Additional Resources

- [Complete API Documentation](/docs/api)
- [SDK Examples](https://github.com/getkeymanager/python-sdk/tree/main/examples)
- [Migration Guide](https://github.com/getkeymanager/python-sdk/blob/main/MIGRATION.md)

---

## 🤝 Support

- **Documentation**: [https://docs.getkeymanager.com](https://docs.getkeymanager.com)
- **Email**: support@getkeymanager.com
- **Issues**: [GitHub Issues](https://github.com/getkeymanager/python-sdk/issues)
