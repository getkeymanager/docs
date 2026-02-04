---
title: Go SDK
description: Official Go SDK for the License Management Platform API.
---

# Go SDK

The official Go SDK for the License Management Platform provides a robust, enterprise-grade interface for license validation, activation, and management.

---

## 🔗 Repository

**GitHub**: [https://github.com/getkeymanager/go-sdk](https://github.com/getkeymanager/go-sdk)

---

## 🚀 Features

- **License Operations**: Online and offline validation, activation, and deactivation.
- **Advanced Management**: Create, update, list, and delete licenses programmatically.
- **Enterprise Security**: RSA-4096-SHA256 signature verification.
- **Resiliency**: Automatic retry with exponential backoff and built-in caching.
- **Full API Coverage**: 100% coverage of all 37 API endpoints including metadata, products, generators, contracts, telemetry, and downloadables.
- **Zero Dependencies**: Uses only Go standard library.

---

## 📦 Installation

Install via go get:

```bash
go get github.com/getkeymanager/go-sdk/getkeymanager
```

---

## 🛠️ Usage Example

```go
package main

import (
    "fmt"
    "log"
    "os"
    
    "github.com/getkeymanager/go-sdk/getkeymanager"
)

func main() {
    publicKey, _ := os.ReadFile("/path/to/public_key.pem")
    
    client, err := getkeymanager.NewClient(map[string]interface{}{
        "api_key":           "your-api-key",
        "base_url":          "https://api.getkeymanager.com",
        "verify_signatures": true,
        "public_key":        string(publicKey),
    })
    
    if err != nil {
        log.Fatal(err)
    }
    
    // Validate a license
    result, err := client.ValidateLicense("XXXXX-XXXXX-XXXXX-XXXXX", map[string]interface{}{})
    if err != nil {
        log.Fatal(err)
    }
    
    response := result["response"].(map[string]interface{})
    data := response["data"].(map[string]interface{})
    
    if valid, ok := data["valid"].(bool); ok && valid {
        fmt.Println("License is valid!")
        license := data["license"].(map[string]interface{})
        fmt.Printf("Status: %v\n", license["status"])
        fmt.Printf("Expires: %v\n", license["expires_at"])
    }
}
```

---

## 🎯 Core Operations

### License Validation

```go
// Validate with hardware binding
hardwareID := client.GenerateHardwareID()

result, err := client.ValidateLicense("XXXXX-XXXXX-XXXXX-XXXXX", map[string]interface{}{
    "hardware_id": hardwareID,
})
```

### License Activation

```go
// Activate on current machine
hardwareID := client.GenerateHardwareID()

result, err := client.ActivateLicense("XXXXX-XXXXX-XXXXX-XXXXX", map[string]interface{}{
    "hardware_id": hardwareID,
    "metadata": map[string]interface{}{
        "app_version": "1.0.0",
    },
})
```

### License Deactivation

```go
// Deactivate from current machine
result, err := client.DeactivateLicense("XXXXX-XXXXX-XXXXX-XXXXX", map[string]interface{}{
    "hardware_id": client.GenerateHardwareID(),
})
```

---

## 🏢 Management Operations

### Create Licenses

```go
// Generate new license keys
result, err := client.CreateLicense(map[string]interface{}{
    "product_id":   "product-uuid",
    "generator_id": "generator-uuid",
    "count":        10,
    "metadata": map[string]interface{}{
        "batch": "Q1-2024",
    },
})

response := result["response"].(map[string]interface{})
licenses := response["data"].(map[string]interface{})["licenses"].([]interface{})

for _, l := range licenses {
    license := l.(map[string]interface{})
    fmt.Printf("Created: %v\n", license["key"])
}
```

### List Licenses

```go
// Get licenses with filters
result, err := client.ListLicenses(map[string]interface{}{
    "product_id": "product-uuid",
    "status":     "active",
    "page":       1,
    "per_page":   50,
})
```

### Update License

```go
// Update license properties
result, err := client.UpdateLicense("XXXXX-XXXXX-XXXXX-XXXXX", map[string]interface{}{
    "status": "suspended",
    "notes":  "Payment overdue",
})
```

---

## 🎛️ Advanced Features

### License Assignment

```go
// Assign license to customer
result, err := client.AssignLicenseKey("XXXXX-XXXXX-XXXXX-XXXXX", "customer@example.com", map[string]interface{}{
    "customer_name": "John Doe",
})

// Random assignment
result, err := client.RandomAssignLicenseKeys(map[string]interface{}{
    "product_id":     "product-uuid",
    "count":          5,
    "customer_email": "customer@example.com",
})
```

### Metadata Management

```go
// Add custom metadata to license
client.CreateLicenseKeyMeta("XXXXX-XXXXX-XXXXX-XXXXX", "tier", "enterprise")

// Add metadata to product
client.CreateProductMeta("product-uuid", "support_level", "premium")
```

### Product Management

```go
// Create product
result, err := client.CreateProduct(map[string]interface{}{
    "name":        "Premium Software",
    "description": "Enterprise edition with all features",
})

// List all products
result, err := client.GetAllProducts(map[string]interface{}{
    "page":     1,
    "per_page": 50,
})
```

### Contract Management

```go
// Create contract
result, err := client.CreateContract(map[string]interface{}{
    "name":          "Enterprise Q1 2024",
    "product_id":    "product-uuid",
    "generator_id":  "generator-uuid",
    "license_count": 1000,
})

// List contracts
result, err := client.GetAllContracts(map[string]interface{}{
    "page":     1,
    "per_page": 50,
})
```

### Generator Operations

```go
// List generators
result, err := client.GetAllGenerators(map[string]interface{}{
    "product_id": "product-uuid",
})

// Generate licenses using generator
result, err := client.GenerateLicenseKeys(map[string]interface{}{
    "product_id":   "product-uuid",
    "generator_id": "generator-uuid",
    "count":        100,
})
```

### Telemetry

```go
// Submit telemetry
client.SubmitTelemetry("XXXXX-XXXXX-XXXXX-XXXXX", map[string]interface{}{
    "event_type":  "app_launch",
    "app_version": "1.0.0",
    "os":          "Linux",
})

// Retrieve telemetry data
result, err := client.GetTelemetryData(map[string]interface{}{
    "license_key": "XXXXX-XXXXX-XXXXX-XXXXX",
    "page":        1,
    "per_page":    50,
})
```

### Downloadables

```go
// Access downloadable files
result, err := client.AccessDownloadables(map[string]interface{}{
    "product_id":  "product-uuid",
    "license_key": "XXXXX-XXXXX-XXXXX-XXXXX",
    "version":     "1.0.0",
})
```

---

## 🔒 Security Features

### Signature Verification

The SDK automatically verifies RSA-4096-SHA256 signatures on all API responses when a public key is provided:

```go
publicKey, _ := os.ReadFile("/path/to/public_key.pem")

client, err := getkeymanager.NewClient(map[string]interface{}{
    "api_key":           "your-api-key",
    "public_key":        string(publicKey),
    "verify_signatures": true,  // Enabled by default
})
```

### Hardware ID Generation

```go
// Generate unique hardware identifier
hardwareID := client.GenerateHardwareID()
fmt.Printf("Hardware ID: %s\n", hardwareID)
```

---

## ⚙️ Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `api_key` | string | *required* | Your API key |
| `base_url` | string | `https://api.getkeymanager.com` | API base URL |
| `public_key` | string | `""` | RSA public key (PEM format) |
| `public_key_file` | string | `""` | Path to public key file |
| `verify_signatures` | bool | `true` | Enable signature verification |
| `cache_enabled` | bool | `true` | Enable response caching |
| `cache_ttl` | int | `300` | Cache TTL in seconds |
| `timeout` | int | `30` | Request timeout in seconds |
| `retry_attempts` | int | `3` | Number of retry attempts |
| `retry_delay` | int | `1000` | Delay between retries (ms) |
| `environment` | string | `""` | Environment filter |
| `product_id` | string | `""` | Default product ID |

---

## 🚨 Error Handling

```go
result, err := client.ValidateLicense("XXXXX-XXXXX-XXXXX-XXXXX", nil)
if err != nil {
    switch e := err.(type) {
    case *getkeymanager.ValidationException:
        fmt.Printf("Validation error: %v\n", e)
    case *getkeymanager.NetworkException:
        fmt.Printf("Network error: %v\n", e)
    case *getkeymanager.SignatureException:
        fmt.Printf("Signature verification failed: %v\n", e)
    case *getkeymanager.RateLimitException:
        fmt.Printf("Rate limit exceeded: %v\n", e)
    case *getkeymanager.LicenseException:
        fmt.Printf("License error: %v (Code: %d)\n", e.Message, e.Code)
    default:
        fmt.Printf("Error: %v\n", err)
    }
    return
}
```

---

## 📋 Requirements

- Go 1.19 or higher
- No external dependencies (uses only standard library)

---

## 📚 Additional Resources

- [Complete API Documentation](/docs/api)
- [SDK Examples](https://github.com/getkeymanager/go-sdk/tree/main/examples)
- [Migration Guide](https://github.com/getkeymanager/go-sdk/blob/main/MIGRATION.md)

---

## 🤝 Support

- **Documentation**: [https://docs.getkeymanager.com](https://docs.getkeymanager.com)
- **Email**: support@getkeymanager.com
- **Issues**: [GitHub Issues](https://github.com/getkeymanager/go-sdk/issues)
