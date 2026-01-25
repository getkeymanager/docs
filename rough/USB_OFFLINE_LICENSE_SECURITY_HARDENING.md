# USB Offline License Security Hardening Guide
## Enterprise-Grade Tamper-Proof Implementation

**Version:** 2.0  
**Last Updated:** 2026-01-23  
**Security Level:** Enterprise-Grade  

---

## ⚠️ CRITICAL SECURITY UPDATE

This document supersedes the configuration approach in the original USB_OFFLINE_LICENSE_GUIDE.md and addresses the critical vulnerability where configuration files (like `config.json`) could be modified by end users.

### The Problem

**INSECURE APPROACH** ❌:
```
USB Drive
├── license.lic (signed)
├── config.json (NOT signed - VULNERABLE!)
│   └── grace_period_days: 365  ← Can be modified!
│   └── features: {...}          ← Can be tampered!
└── public-key.pem
```

**Result:** Users can modify `config.json` to extend grace periods, enable features, or bypass restrictions.

### The Solution

**SECURE APPROACH** ✅:
```
USB Drive
├── license.lic (ALL data signed together)
│   ├── License data
│   ├── Product data
│   ├── Feature flags
│   ├── Grace period
│   ├── Validation rules
│   └── RSA-4096-SHA256 signature ← Covers EVERYTHING
└── public-key.pem (read-only, verification only)
```

**Result:** Any modification to ANY field breaks the cryptographic signature. Tampering is mathematically detectable.

---

## 🔒 1. Core Security Principles

### 1.1 Cryptographic Integrity

All license data MUST be:
- **Signed Together**: All fields in a single signed payload
- **Immutable**: Any change invalidates the signature
- **Verifiable**: Signature checked before trusting any data
- **Non-repudiable**: Only server's private key can create valid signatures

### 1.2 Zero Trust Configuration

**NEVER trust external configuration files**:
- ❌ Separate `config.json` files
- ❌ `.ini` files
- ❌ `.env` files
- ❌ Registry entries set by user
- ❌ Command-line arguments for security parameters

**ONLY trust cryptographically signed data**:
- ✅ Data inside signed license file
- ✅ Signature-verified fields
- ✅ Server-generated timestamps

### 1.3 Defense in Depth

Multiple security layers:
1. **Signature Verification**: Primary defense
2. **Timestamp Validation**: Detect clock manipulation
3. **USB Binding**: Tie license to specific USB serial (optional)
4. **Feature Validation**: Cross-check feature flags
5. **Runtime Monitoring**: Detect tampering attempts

---

## 📄 2. Secure License File Format

### 2.1 Complete Structure

```json
{
  "version": "2.0",
  "license": {
    "key": "XXXXX-XXXXX-XXXXX-XXXXX",
    "status": "active",
    "expires_at": "2025-12-31T23:59:59Z",
    "hardware_id": null,
    "domain": null,
    "features": {
      "premium_support": true,
      "max_users": 100,
      "advanced_analytics": true,
      "api_access": true,
      "custom_branding": false
    },
    "activations_limit": 0,
    "activations_count": 0,
    "metadata": {
      "customer_name": "Acme Corp",
      "purchase_order": "PO-2024-001",
      "support_level": "enterprise"
    }
  },
  "product": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Enterprise Edition",
    "version": "3.0.0"
  },
  "generator": {
    "id": "660e8400-e29b-41d4-a716-446655440001",
    "algorithm": "random",
    "pattern": "XXXXX-XXXXX-XXXXX-XXXXX"
  },
  "validation_rules": {
    "grace_period_days": 30,
    "offline_validation_enabled": true,
    "require_usb_connected": true,
    "max_clock_drift_hours": 24,
    "strict_expiry": false,
    "allow_grace_after_expiry": true
  },
  "security": {
    "signature_algorithm": "RSA-4096-SHA256",
    "issued_by": "License Server v2.0",
    "usb_serial_number": null,
    "anti_tampering_hash": "sha256_of_critical_fields"
  },
  "issued_at": "2024-01-15T10:30:00Z",
  "last_verified_at": "2024-01-15T10:30:00Z",
  "environment": "production",
  "signature": "base64_encoded_rsa_4096_signature"
}
```

### 2.2 Critical Fields (ALL SIGNED)

| Field | Type | Purpose | Tamper Impact |
|-------|------|---------|---------------|
| `validation_rules.grace_period_days` | int | Offline grace period | Signature breaks |
| `validation_rules.require_usb_connected` | bool | USB enforcement | Signature breaks |
| `license.features` | object | Enabled features | Signature breaks |
| `license.expires_at` | datetime | Expiration date | Signature breaks |
| `security.anti_tampering_hash` | string | Additional integrity check | Signature breaks |

### 2.3 Signature Generation

The signature covers the **entire JSON structure** (minus the signature field itself):

```python
# Pseudo-code for signature generation
def generate_signature(license_data):
    # 1. Remove signature field
    data_to_sign = license_data.copy()
    del data_to_sign['signature']
    
    # 2. Canonical JSON (sorted keys, no whitespace)
    canonical_json = json.dumps(data_to_sign, sort_keys=True, separators=(',', ':'))
    
    # 3. Hash the canonical JSON
    data_hash = SHA256(canonical_json)
    
    # 4. Sign with RSA-4096 private key
    signature = RSA_PRIVATE_KEY.sign(data_hash, padding=PSS, hash_algorithm=SHA256)
    
    # 5. Base64 encode
    return base64.b64encode(signature)
```

**Key Point**: Even a single character change in ANY field (including `grace_period_days`) will cause signature verification to fail.

---

## 🛡️ 3. Client-Side Validation (Required Implementation)

### 3.1 Validation Workflow

```
┌─────────────────────────┐
│  Application Startup    │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  Detect USB Drive       │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  Read license.lic       │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│  Parse JSON                         │
│  STOP: Do NOT trust any data yet!   │
└────────────┬────────────────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│  Verify Signature                   │
│  - Load public key                  │
│  - Reconstruct canonical JSON       │
│  - Verify RSA-4096-SHA256 signature │
└────────────┬────────────────────────┘
             │
         ┌───┴───┐
         │ Valid?│
         └───┬───┘
             │
     ┌───────┴───────┐
     │               │
    NO              YES
     │               │
     ▼               ▼
  REJECT      ┌─────────────────────┐
  LICENSE     │ NOW trust all data: │
  EXIT        │ - grace_period_days │
              │ - features          │
              │ - expiry date       │
              │ - validation rules  │
              └─────────┬───────────┘
                        │
                        ▼
              ┌──────────────────────┐
              │  Validate Constraints│
              │  - Check expiry      │
              │  - Check grace period│
              │  - Check USB presence│
              └─────────┬────────────┘
                        │
                        ▼
              ┌──────────────────────┐
              │  Grant Access        │
              │  Enable Features     │
              └──────────────────────┘
```

### 3.2 Mandatory Checks (Ordered)

#### Check 1: Signature Verification (FIRST!)
```csharp
// .NET Example
public static bool VerifyLicense(string licenseJson, string publicKeyPem)
{
    // 1. Parse JSON
    var licenseData = JsonSerializer.Deserialize<LicenseFile>(licenseJson);
    
    // 2. Extract signature
    string signature = licenseData.Signature;
    
    // 3. Remove signature from data
    licenseData.Signature = null;
    
    // 4. Create canonical JSON (sorted keys, no whitespace)
    var options = new JsonSerializerOptions 
    { 
        PropertyNamingPolicy = JsonNamingPolicy.CamelCase,
        WriteIndented = false,
        DefaultIgnoreCondition = JsonIgnoreCondition.WhenWritingNull
    };
    string canonicalJson = JsonSerializer.Serialize(licenseData, options);
    
    // Sort keys (manual or use library)
    canonicalJson = SortJsonKeys(canonicalJson);
    
    // 5. Load public key
    using var rsa = RSA.Create();
    rsa.ImportFromPem(publicKeyPem);
    
    // 6. Verify signature
    byte[] dataBytes = Encoding.UTF8.GetBytes(canonicalJson);
    byte[] signatureBytes = Convert.FromBase64String(signature);
    
    bool isValid = rsa.VerifyData(
        dataBytes, 
        signatureBytes, 
        HashAlgorithmName.SHA256, 
        RSASignaturePadding.Pkcs1
    );
    
    if (!isValid)
    {
        LogSecurityEvent("TAMPERED LICENSE DETECTED");
        return false;
    }
    
    // 7. NOW trust the data
    return true;
}
```

#### Check 2: Expiry Validation
```csharp
public static bool IsLicenseExpired(LicenseFile license)
{
    if (license.License.ExpiresAt == null)
        return false; // Perpetual license
    
    DateTime expiryDate = license.License.ExpiresAt.Value;
    DateTime now = DateTime.UtcNow;
    
    // Check if expired
    if (now > expiryDate)
    {
        // Check grace period (from SIGNED data)
        int gracePeriodDays = license.ValidationRules.GracePeriodDays;
        DateTime graceEndDate = expiryDate.AddDays(gracePeriodDays);
        
        if (now > graceEndDate)
        {
            LogSecurityEvent("LICENSE EXPIRED (grace period ended)");
            return true; // Expired beyond grace
        }
        
        LogSecurityEvent($"LICENSE IN GRACE PERIOD ({(graceEndDate - now).Days} days remaining)");
        return false; // Still in grace period
    }
    
    return false; // Not expired
}
```

#### Check 3: Feature Validation
```csharp
public static bool IsFeatureEnabled(LicenseFile license, string featureName)
{
    // CRITICAL: Only use features from SIGNED license file
    if (license.License.Features.TryGetValue(featureName, out var value))
    {
        if (value is bool boolValue)
            return boolValue;
        if (value is int intValue)
            return intValue > 0;
    }
    
    return false; // Feature not found or disabled
}
```

#### Check 4: USB Presence (Optional but Recommended)
```csharp
public static bool IsUSBConnected(LicenseFile license, string usbPath)
{
    if (!license.ValidationRules.RequireUsbConnected)
        return true; // Not required
    
    // Check if USB is accessible
    if (!Directory.Exists(usbPath))
    {
        LogSecurityEvent("USB DRIVE NOT CONNECTED");
        return false;
    }
    
    // Optionally check USB serial number
    if (!string.IsNullOrEmpty(license.Security.UsbSerialNumber))
    {
        string currentSerial = GetUSBSerialNumber(usbPath);
        if (currentSerial != license.Security.UsbSerialNumber)
        {
            LogSecurityEvent("USB DRIVE MISMATCH (different serial)");
            return false;
        }
    }
    
    return true;
}
```

---

## 🚨 4. Attack Scenarios & Mitigations

### 4.1 Attack: Modify grace_period_days

**Attack:**
```json
// Attacker changes:
"validation_rules": {
  "grace_period_days": 9999  // Extended to 27 years!
}
```

**Detection:**
- Signature verification FAILS immediately
- Application rejects license before reading any data
- Attack detected and logged

**Mitigation:**
```csharp
if (!VerifyLicense(licenseJson, publicKey))
{
    LogSecurityEvent("TAMPERED LICENSE - SIGNATURE INVALID");
    Application.Exit(1); // Terminate immediately
}
```

### 4.2 Attack: Enable Premium Features

**Attack:**
```json
"features": {
  "premium_support": true,  // Changed from false
  "max_users": 999999       // Changed from 100
}
```

**Detection:**
- Signature verification FAILS
- No feature data is trusted until signature passes
- Attack logged

**Mitigation:**
- Same as 4.1 - signature verification is the primary defense
- Features are only read AFTER signature validation

### 4.3 Attack: Extend Expiry Date

**Attack:**
```json
"license": {
  "expires_at": "2099-12-31T23:59:59Z"  // Extended 75 years!
}
```

**Detection:**
- Signature verification FAILS
- Application never reaches expiry check logic
- Attack logged

**Mitigation:**
- Signature covers `expires_at`
- Tampering breaks signature
- License rejected before expiry is checked

### 4.4 Attack: Replace Signature

**Attack:**
```json
// Attacker modifies data AND tries to generate new signature
"grace_period_days": 9999,
"signature": "attacker_generated_signature"
```

**Detection:**
- Signature verification FAILS (attacker doesn't have private key)
- RSA-4096 is computationally infeasible to break
- Attack logged

**Mitigation:**
```csharp
// Public key verification ensures only server can sign
bool isValid = rsa.VerifyData(data, signature, ...);
// Will return false because attacker can't create valid signature
```

### 4.5 Attack: Replace Entire License File

**Attack:**
```
// Attacker replaces license.lic with a different signed license
// (e.g., from another customer)
```

**Detection:**
- Signature is valid (it's a real license)
- BUT license key doesn't match expected key
- OR hardware_id doesn't match machine
- OR USB serial doesn't match

**Mitigation:**
```csharp
// Check license key matches expected
if (license.License.Key != expectedLicenseKey)
{
    LogSecurityEvent("LICENSE KEY MISMATCH");
    return false;
}

// Check hardware binding
if (!string.IsNullOrEmpty(license.License.HardwareId))
{
    string currentHWID = GenerateHardwareId();
    if (currentHWID != license.License.HardwareId)
    {
        LogSecurityEvent("HARDWARE MISMATCH");
        return false;
    }
}
```

### 4.6 Attack: Clock Manipulation

**Attack:**
```bash
# Attacker sets system clock back to extend grace period
sudo date -s "2020-01-01"
```

**Detection:**
- `last_verified_at` timestamp tracking
- Detect time going backwards
- Grace period calculation still uses real elapsed time

**Mitigation:**
```csharp
public static bool DetectClockTampering(LicenseFile license)
{
    DateTime lastVerified = license.LastVerifiedAt;
    DateTime now = DateTime.UtcNow;
    
    // Time should only move forward
    if (now < lastVerified)
    {
        // Clock moved backwards!
        TimeSpan drift = lastVerified - now;
        
        if (drift.TotalHours > license.ValidationRules.MaxClockDriftHours)
        {
            LogSecurityEvent($"CLOCK TAMPERING DETECTED (backwards {drift.TotalDays} days)");
            return true;
        }
    }
    
    // Update last_verified_at (write back to file if allowed)
    // Note: This write is NOT signed, but drift detection still works
    license.LastVerifiedAt = now;
    
    return false;
}
```

### 4.7 Attack: Remove USB Requirement

**Attack:**
```json
"validation_rules": {
  "require_usb_connected": false  // Changed from true
}
```

**Detection:**
- Signature verification FAILS
- Setting is never trusted
- Attack logged

**Mitigation:**
- `require_usb_connected` is inside signed data
- Cannot be changed without breaking signature

---

## 🔐 5. Server-Side License Generation

### 5.1 Secure Generation Process

```php
// PHP Example (Laravel)
class OfflineLicenseGenerator
{
    public function generateUSBLicense(License $license, array $options = [])
    {
        // 1. Build license data structure
        $licenseData = [
            'version' => '2.0',
            'license' => [
                'key' => $license->key,
                'status' => $license->status,
                'expires_at' => $license->expires_at?->toIso8601String(),
                'hardware_id' => null, // USB license - no HWID
                'domain' => null,
                'features' => $license->feature_flags,
                'activations_limit' => 0, // USB = unlimited
                'activations_count' => 0,
                'metadata' => $license->metadata
            ],
            'product' => [
                'id' => $license->product->uuid,
                'name' => $license->product->name,
                'version' => $options['product_version'] ?? null
            ],
            'generator' => [
                'id' => $license->generator->uuid,
                'algorithm' => $license->generator->algorithm,
                'pattern' => $license->generator->pattern
            ],
            'validation_rules' => [
                'grace_period_days' => $options['grace_period_days'] ?? 30,
                'offline_validation_enabled' => true,
                'require_usb_connected' => $options['require_usb'] ?? true,
                'max_clock_drift_hours' => 24,
                'strict_expiry' => false,
                'allow_grace_after_expiry' => true
            ],
            'security' => [
                'signature_algorithm' => 'RSA-4096-SHA256',
                'issued_by' => 'License Server v2.0',
                'usb_serial_number' => $options['usb_serial'] ?? null,
                'anti_tampering_hash' => null // Computed below
            ],
            'issued_at' => now()->toIso8601String(),
            'last_verified_at' => now()->toIso8601String(),
            'environment' => $license->environment
        ];
        
        // 2. Compute anti-tampering hash (additional layer)
        $licenseData['security']['anti_tampering_hash'] = $this->computeAntiTamperingHash($licenseData);
        
        // 3. Generate signature
        $signature = $this->signLicenseData($licenseData);
        
        // 4. Add signature
        $licenseData['signature'] = $signature;
        
        // 5. Return JSON
        return json_encode($licenseData, JSON_PRETTY_PRINT | JSON_UNESCAPED_SLASHES);
    }
    
    private function signLicenseData(array $data): string
    {
        // 1. Create canonical JSON (sorted keys, no whitespace)
        $canonicalJson = json_encode($data, JSON_UNESCAPED_SLASHES | JSON_UNESCAPED_UNICODE);
        $canonicalJson = $this->sortJsonKeys($canonicalJson);
        
        // 2. Load private key
        $privateKey = openssl_pkey_get_private(
            config('licensing.private_key'),
            config('licensing.private_key_password')
        );
        
        if (!$privateKey) {
            throw new \Exception('Failed to load private key');
        }
        
        // 3. Sign data
        $signature = '';
        $success = openssl_sign(
            $canonicalJson,
            $signature,
            $privateKey,
            OPENSSL_ALGO_SHA256
        );
        
        if (!$success) {
            throw new \Exception('Failed to sign license data');
        }
        
        // 4. Base64 encode
        return base64_encode($signature);
    }
    
    private function computeAntiTamperingHash(array $data): string
    {
        // Hash critical fields (additional integrity check)
        $criticalFields = [
            $data['license']['key'],
            $data['license']['expires_at'],
            $data['validation_rules']['grace_period_days'],
            $data['license']['features']
        ];
        
        $concatenated = json_encode($criticalFields, JSON_UNESCAPED_SLASHES);
        return hash('sha256', $concatenated);
    }
}
```

### 5.2 Admin Portal Updates

**Required Changes to `/admin/licenses/{uuid}/offline-file` page:**

1. **Remove separate config.json generation**
2. **Embed all config in license.lic**
3. **Add USB-specific options form:**

```blade
<div class="space-y-4">
    <h3>USB License Configuration</h3>
    
    <div class="form-group">
        <label>Grace Period (Days)</label>
        <input type="number" wire:model="gracePeriodDays" value="30" min="0" max="365">
        <p class="text-sm text-gray-500">Offline validation grace period after expiry</p>
    </div>
    
    <div class="form-group">
        <label>
            <input type="checkbox" wire:model="requireUSBConnected" checked>
            Require USB Connected During Runtime
        </label>
        <p class="text-sm text-gray-500">Force USB to remain connected</p>
    </div>
    
    <div class="form-group">
        <label>USB Serial Number (Optional)</label>
        <input type="text" wire:model="usbSerialNumber" placeholder="Leave empty for any USB">
        <p class="text-sm text-gray-500">Bind license to specific USB drive</p>
    </div>
    
    <div class="form-group">
        <label>
            <input type="checkbox" wire:model="allowGraceAfterExpiry" checked>
            Allow Grace Period After Expiry
        </label>
    </div>
</div>
```

---

## 📚 6. Updated Platform Implementations

### 6.1 .NET/C# (Complete Secure Implementation)

```csharp
using System;
using System.IO;
using System.Text;
using System.Text.Json;
using System.Security.Cryptography;
using System.Linq;

public class SecureUSBLicenseValidator
{
    private const string LICENSE_FILENAME = "license.lic";
    private const string PUBLIC_KEY_FILENAME = "public-key.pem";
    
    public class ValidationResult
    {
        public bool IsValid { get; set; }
        public string ErrorMessage { get; set; }
        public LicenseFile License { get; set; }
        public Dictionary<string, object> EnabledFeatures { get; set; }
    }
    
    public static ValidationResult ValidateLicense(string usbDrivePath, string expectedLicenseKey = null)
    {
        var result = new ValidationResult { IsValid = false, EnabledFeatures = new Dictionary<string, object>() };
        
        try
        {
            // Step 1: Find license file
            string licensePath = Path.Combine(usbDrivePath, LICENSE_FILENAME);
            string publicKeyPath = Path.Combine(usbDrivePath, PUBLIC_KEY_FILENAME);
            
            if (!File.Exists(licensePath))
            {
                result.ErrorMessage = "License file not found on USB drive";
                return result;
            }
            
            if (!File.Exists(publicKeyPath))
            {
                result.ErrorMessage = "Public key not found on USB drive";
                return result;
            }
            
            // Step 2: Read files
            string licenseJson = File.ReadAllText(licensePath);
            string publicKeyPem = File.ReadAllText(publicKeyPath);
            
            // Step 3: Parse JSON (but don't trust yet!)
            var license = JsonSerializer.Deserialize<LicenseFile>(licenseJson);
            
            // Step 4: VERIFY SIGNATURE FIRST (critical!)
            if (!VerifySignature(license, publicKeyPem))
            {
                LogSecurityEvent("TAMPERED LICENSE DETECTED - Invalid signature");
                result.ErrorMessage = "License signature verification failed. File may be tampered.";
                return result;
            }
            
            // Step 5: NOW trust the data - signature is valid
            result.License = license;
            
            // Step 6: Check license key match (if expected)
            if (!string.IsNullOrEmpty(expectedLicenseKey) && license.License.Key != expectedLicenseKey)
            {
                LogSecurityEvent($"LICENSE KEY MISMATCH: expected={expectedLicenseKey}, got={license.License.Key}");
                result.ErrorMessage = "License key does not match expected value";
                return result;
            }
            
            // Step 7: Check expiry (using signed grace_period_days)
            if (IsExpired(license))
            {
                result.ErrorMessage = $"License expired on {license.License.ExpiresAt}";
                return result;
            }
            
            // Step 8: Check USB presence requirement (using signed rule)
            if (license.ValidationRules.RequireUsbConnected)
            {
                if (!IsUSBConnected(usbDrivePath))
                {
                    result.ErrorMessage = "USB drive must remain connected";
                    return result;
                }
            }
            
            // Step 9: Check clock tampering
            if (DetectClockTampering(license))
            {
                result.ErrorMessage = "System clock tampering detected";
                return result;
            }
            
            // Step 10: Extract enabled features (from signed data)
            result.EnabledFeatures = license.License.Features;
            
            // Step 11: All checks passed!
            result.IsValid = true;
            
            // Step 12: Update last_verified_at (optional, for drift detection)
            UpdateLastVerified(licensePath, license);
            
            return result;
        }
        catch (Exception ex)
        {
            LogSecurityEvent($"LICENSE VALIDATION ERROR: {ex.Message}");
            result.ErrorMessage = $"License validation error: {ex.Message}";
            return result;
        }
    }
    
    private static bool VerifySignature(LicenseFile license, string publicKeyPem)
    {
        try
        {
            // 1. Extract signature
            string signature = license.Signature;
            
            // 2. Clone object and remove signature
            var dataToVerify = JsonSerializer.Deserialize<LicenseFile>(
                JsonSerializer.Serialize(license)
            );
            dataToVerify.Signature = null;
            
            // 3. Create canonical JSON (sorted keys)
            var options = new JsonSerializerOptions
            {
                WriteIndented = false,
                PropertyNamingPolicy = JsonNamingPolicy.CamelCase,
                DefaultIgnoreCondition = System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingNull
            };
            string canonicalJson = JsonSerializer.Serialize(dataToVerify, options);
            canonicalJson = SortJsonKeys(canonicalJson);
            
            // 4. Load public key
            using var rsa = RSA.Create();
            rsa.ImportFromPem(publicKeyPem);
            
            // 5. Verify signature
            byte[] dataBytes = Encoding.UTF8.GetBytes(canonicalJson);
            byte[] signatureBytes = Convert.FromBase64String(signature);
            
            bool isValid = rsa.VerifyData(
                dataBytes,
                signatureBytes,
                HashAlgorithmName.SHA256,
                RSASignaturePadding.Pkcs1
            );
            
            return isValid;
        }
        catch (Exception ex)
        {
            LogSecurityEvent($"SIGNATURE VERIFICATION ERROR: {ex.Message}");
            return false;
        }
    }
    
    private static bool IsExpired(LicenseFile license)
    {
        if (license.License.ExpiresAt == null)
            return false; // Perpetual
        
        DateTime expiryDate = license.License.ExpiresAt.Value;
        DateTime now = DateTime.UtcNow;
        
        if (now <= expiryDate)
            return false; // Not expired
        
        // Check grace period (from SIGNED data)
        if (license.ValidationRules.AllowGraceAfterExpiry)
        {
            DateTime graceEndDate = expiryDate.AddDays(license.ValidationRules.GracePeriodDays);
            if (now <= graceEndDate)
            {
                LogSecurityEvent($"LICENSE IN GRACE PERIOD ({(graceEndDate - now).Days} days remaining)");
                return false; // Still in grace
            }
        }
        
        return true; // Expired
    }
    
    private static bool IsUSBConnected(string usbPath)
    {
        return Directory.Exists(usbPath) && File.Exists(Path.Combine(usbPath, LICENSE_FILENAME));
    }
    
    private static bool DetectClockTampering(LicenseFile license)
    {
        DateTime lastVerified = license.LastVerifiedAt;
        DateTime now = DateTime.UtcNow;
        
        if (now < lastVerified)
        {
            TimeSpan drift = lastVerified - now;
            if (drift.TotalHours > license.ValidationRules.MaxClockDriftHours)
            {
                LogSecurityEvent($"CLOCK TAMPERING: Time moved backwards {drift.TotalDays:F1} days");
                return true;
            }
        }
        
        return false;
    }
    
    private static void UpdateLastVerified(string licensePath, LicenseFile license)
    {
        try
        {
            // Update last_verified_at timestamp
            // Note: This write is NOT signed, but it's only used for drift detection
            license.LastVerifiedAt = DateTime.UtcNow;
            
            var options = new JsonSerializerOptions { WriteIndented = true };
            string updatedJson = JsonSerializer.Serialize(license, options);
            
            File.WriteAllText(licensePath, updatedJson);
        }
        catch
        {
            // Ignore write errors (USB might be read-only)
        }
    }
    
    private static string SortJsonKeys(string json)
    {
        // Simple key sorting (production should use proper library)
        var obj = JsonSerializer.Deserialize<Dictionary<string, object>>(json);
        var sorted = obj.OrderBy(kv => kv.Key).ToDictionary(kv => kv.Key, kv => kv.Value);
        return JsonSerializer.Serialize(sorted);
    }
    
    private static void LogSecurityEvent(string message)
    {
        // Log to file, SIEM, or monitoring system
        Console.WriteLine($"[SECURITY] {DateTime.UtcNow:O} - {message}");
        
        // In production:
        // - Write to secure log file
        // - Send to monitoring system
        // - Alert security team if critical
    }
}

// Model classes
public class LicenseFile
{
    public string Version { get; set; }
    public LicenseData License { get; set; }
    public ProductData Product { get; set; }
    public GeneratorData Generator { get; set; }
    public ValidationRules ValidationRules { get; set; }
    public SecurityData Security { get; set; }
    public DateTime IssuedAt { get; set; }
    public DateTime LastVerifiedAt { get; set; }
    public string Environment { get; set; }
    public string Signature { get; set; }
}

public class LicenseData
{
    public string Key { get; set; }
    public string Status { get; set; }
    public DateTime? ExpiresAt { get; set; }
    public string HardwareId { get; set; }
    public string Domain { get; set; }
    public Dictionary<string, object> Features { get; set; }
    public int ActivationsLimit { get; set; }
    public int ActivationsCount { get; set; }
    public Dictionary<string, object> Metadata { get; set; }
}

public class ProductData
{
    public string Id { get; set; }
    public string Name { get; set; }
    public string Version { get; set; }
}

public class GeneratorData
{
    public string Id { get; set; }
    public string Algorithm { get; set; }
    public string Pattern { get; set; }
}

public class ValidationRules
{
    public int GracePeriodDays { get; set; }
    public bool OfflineValidationEnabled { get; set; }
    public bool RequireUsbConnected { get; set; }
    public int MaxClockDriftHours { get; set; }
    public bool StrictExpiry { get; set; }
    public bool AllowGraceAfterExpiry { get; set; }
}

public class SecurityData
{
    public string SignatureAlgorithm { get; set; }
    public string IssuedBy { get; set; }
    public string UsbSerialNumber { get; set; }
    public string AntiTamperingHash { get; set; }
}
```

### 6.2 Usage Example

```csharp
// Application startup
class Program
{
    static void Main(string[] args)
    {
        // 1. Detect USB drive
        string usbPath = DetectUSBDrive();
        if (usbPath == null)
        {
            Console.WriteLine("ERROR: USB license drive not found");
            Environment.Exit(1);
        }
        
        // 2. Validate license (with signature verification)
        var result = SecureUSBLicenseValidator.ValidateLicense(usbPath, "XXXXX-XXXXX-XXXXX-XXXXX");
        
        if (!result.IsValid)
        {
            Console.WriteLine($"LICENSE ERROR: {result.ErrorMessage}");
            Environment.Exit(1);
        }
        
        // 3. License is valid - check features
        bool hasPremiumSupport = result.EnabledFeatures.ContainsKey("premium_support") &&
                                 (bool)result.EnabledFeatures["premium_support"];
        
        int maxUsers = result.EnabledFeatures.ContainsKey("max_users") ?
                       Convert.ToInt32(result.EnabledFeatures["max_users"]) : 1;
        
        Console.WriteLine("LICENSE VALID");
        Console.WriteLine($"Product: {result.License.Product.Name}");
        Console.WriteLine($"Expires: {result.License.License.ExpiresAt?.ToString() ?? "Never"}");
        Console.WriteLine($"Premium Support: {hasPremiumSupport}");
        Console.WriteLine($"Max Users: {maxUsers}");
        
        // 4. Start application with enabled features
        StartApplication(result.EnabledFeatures);
    }
    
    static string DetectUSBDrive()
    {
        foreach (var drive in DriveInfo.GetDrives())
        {
            if (drive.DriveType == DriveType.Removable && drive.IsReady)
            {
                string licensePath = Path.Combine(drive.RootDirectory.FullName, "license.lic");
                if (File.Exists(licensePath))
                {
                    return drive.RootDirectory.FullName;
                }
            }
        }
        return null;
    }
}
```

---

## ✅ 7. Security Checklist

### For Administrators

- [ ] **Never** create separate `config.json` files
- [ ] **Always** embed all configuration in signed license file
- [ ] **Use** strong grace periods (30-90 days recommended)
- [ ] **Set** `require_usb_connected: true` for high-security scenarios
- [ ] **Bind** to USB serial number for maximum security
- [ ] **Protect** private key with hardware security module (HSM)
- [ ] **Rotate** signing keys annually
- [ ] **Monitor** license generation logs

### For Developers

- [ ] **Verify** signature BEFORE reading ANY data
- [ ] **Never** trust unsigned configuration files
- [ ] **Use** all validation functions (signature, expiry, features)
- [ ] **Log** security events to monitoring system
- [ ] **Implement** clock tampering detection
- [ ] **Test** with tampered licenses to verify rejection
- [ ] **Handle** errors gracefully (fail closed)
- [ ] **Update** `last_verified_at` for drift detection

### For Security Teams

- [ ] **Audit** license generation process
- [ ] **Review** signature verification implementation
- [ ] **Test** tampering scenarios
- [ ] **Monitor** security event logs
- [ ] **Investigate** failed validation attempts
- [ ] **Plan** key rotation procedures
- [ ] **Document** incident response procedures

---

## 📖 8. Migration from v1.0

### 8.1 Breaking Changes

| Change | Impact | Action Required |
|--------|--------|-----------------|
| Removed `config.json` | Medium | Regenerate all USB licenses |
| Added `validation_rules` | Low | Use default values |
| Added `security` section | Low | Auto-generated |
| Signature includes all fields | High | Regenerate licenses |

### 8.2 Migration Steps

1. **Backup** existing USB drives
2. **Update** server to v2.0 (includes new generator)
3. **Regenerate** all USB license files
4. **Update** client applications with new validator code
5. **Test** with regenerated licenses
6. **Distribute** new USB drives to customers
7. **Decommission** old licenses (set grace period)

### 8.3 Compatibility

- **v2.0 validator** can read v1.0 licenses (backward compatible)
- **v1.0 validator** cannot read v2.0 licenses (forward incompatible)
- Recommendation: Upgrade all clients before distributing v2.0 licenses

---

## 🎯 9. Summary

### What Changed

❌ **OLD (INSECURE)**:
- Separate `config.json` file (unprotected)
- User could modify grace periods and features
- No tamper detection

✅ **NEW (SECURE)**:
- All data in signed license file
- RSA-4096-SHA256 signature over everything
- Tampering mathematically detectable
- Enterprise-grade security

### Key Takeaways

1. **ALL configuration MUST be signed**
2. **Verify signature BEFORE reading data**
3. **Never trust external configuration**
4. **Log all security events**
5. **Test with tampered licenses**

### Result

**Enterprise-grade, tamper-proof, cryptographically secure offline licensing.**

---

**END OF SECURITY HARDENING GUIDE**
