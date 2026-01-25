# USB-Based Offline License Management Guide
## Complete Implementation & Deployment Strategy

**Version:** 1.0  
**Last Updated:** 2026-01-23

---

## 📋 Table of Contents

1. [Overview](#1-overview)
2. [Architecture & Workflow](#2-architecture--workflow)
3. [USB Drive Setup](#3-usb-drive-setup)
4. [License File Generation](#4-license-file-generation)
5. [Application Integration](#5-application-integration)
6. [Platform-Specific Implementation](#6-platform-specific-implementation)
7. [Security Considerations](#7-security-considerations)
8. [Troubleshooting](#8-troubleshooting)
9. [Best Practices](#9-best-practices)

---

## 1. Overview

### 1.1 Purpose

This guide explains how to implement **USB stick-based offline license management** where:

- License files are stored on a USB drive
- USB drive must remain connected during application runtime
- Works with any application (.NET, Python, Go, PHP, Electron, etc.)
- Supports Windows and Linux environments
- Provides tamper-proof, cryptographically signed licenses

### 1.2 Use Cases

- **Air-gapped systems**: Environments without internet access
- **Industrial control systems**: Manufacturing floors, critical infrastructure
- **Secure facilities**: Government, military, healthcare
- **Field deployments**: Remote locations, temporary installations
- **Multi-machine licenses**: One USB for multiple authorized devices

### 1.3 Key Benefits

✅ **No Internet Required**: Complete offline operation  
✅ **Physical Control**: License tied to physical USB device  
✅ **Portable**: Move license between authorized machines  
✅ **Secure**: RSA-4096 cryptographic signatures  
✅ **Simple**: Easy deployment and updates  

---

## 2. Architecture & Workflow

### 2.1 System Components

```
┌─────────────────────┐
│   Admin Portal      │
│  (getkeymanager)    │
└──────────┬──────────┘
           │ Generate
           │ .lic file
           ▼
┌─────────────────────┐
│    USB Drive        │
│  license.lic        │
│  public-key.pem     │
│  app-config.json    │
└──────────┬──────────┘
           │ USB stays
           │ connected
           ▼
┌─────────────────────┐
│  Client Application │
│  (.NET/Python/Go/   │
│   PHP/Electron/etc) │
└─────────────────────┘
```

### 2.2 Workflow Steps

1. **Admin**: Generate offline license file via Admin Portal
2. **Admin**: Copy license file + public key to USB drive
3. **Admin**: Provide USB drive to customer
4. **Customer**: Insert USB drive into target machine
5. **Customer**: Configure application to read from USB path
6. **Application**: Validates license on startup and periodically
7. **Application**: Monitors USB presence (optional)
8. **Application**: Operates with validated features

### 2.3 License Validation Flow

```
Application Startup
    ↓
Detect USB Drive
    ↓
Read license.lic
    ↓
Verify RSA Signature ──→ FAIL → Application Exits
    ↓ PASS
Check Expiration ──→ FAIL → Application Exits
    ↓ PASS
Verify Hardware ID (optional) ──→ FAIL → Application Exits
    ↓ PASS
Load Feature Flags
    ↓
Application Runs with Licensed Features
    ↓
Periodic Re-validation (every 1-24 hours)
```

---

## 3. USB Drive Setup

### 3.1 Recommended USB Drive Specifications

| Specification | Recommendation | Notes |
|--------------|----------------|-------|
| **Capacity** | 1-4 GB | License files are < 10 KB |
| **Format** | FAT32 or exFAT | Cross-platform compatibility |
| **Speed** | USB 2.0+ | USB 3.0 for faster reads |
| **Write Protection** | Optional | Prevent customer tampering |
| **Branding** | Custom | Company logo/colors |

### 3.2 USB Drive Structure

```
USB:/
├── license.lic           # Offline license file
├── public-key.pem        # RSA public key for verification
├── config.json           # Application-specific configuration
├── README.txt            # User instructions
└── logs/                 # Optional: Validation logs
    └── .gitkeep
```

### 3.3 Creating the USB Drive

#### Windows

```batch
REM Format USB (drive letter E:)
format E: /FS:FAT32 /Q /V:LICENSE

REM Copy files
copy license.lic E:\
copy public-key.pem E:\
copy config.json E:\
copy README.txt E:\
mkdir E:\logs
```

#### Linux

```bash
# Format USB (device /dev/sdb1)
sudo mkfs.vfat -F 32 -n LICENSE /dev/sdb1

# Mount
sudo mount /dev/sdb1 /mnt/usb

# Copy files
sudo cp license.lic /mnt/usb/
sudo cp public-key.pem /mnt/usb/
sudo cp config.json /mnt/usb/
sudo cp README.txt /mnt/usb/
sudo mkdir /mnt/usb/logs

# Unmount
sudo umount /mnt/usb
```

### 3.4 Sample config.json

```json
{
  "version": "1.0",
  "application": {
    "name": "YourApp",
    "version": "3.0.0"
  },
  "license_file": "license.lic",
  "public_key_file": "public-key.pem",
  "validation": {
    "check_on_startup": true,
    "check_interval_hours": 24,
    "require_hardware_binding": false,
    "grace_period_days": 30
  },
  "logging": {
    "enabled": true,
    "path": "logs/validation.log",
    "level": "info"
  }
}
```

### 3.5 Sample README.txt

```text
LICENSE USB DRIVE
=================

This USB drive contains your software license.

IMPORTANT INSTRUCTIONS:
1. Keep this USB drive connected while using the software
2. Do not modify, delete, or copy files from this drive
3. Store safely when not in use
4. Contact support if license validation fails

FILES:
- license.lic: Your license file (DO NOT EDIT)
- public-key.pem: Verification key (DO NOT EDIT)
- config.json: Configuration (may be edited by admin)
- README.txt: This file

SUPPORT:
Email: support@yourcompany.com
Phone: +1-555-123-4567

License Key: XXXXX-XXXXX-XXXXX-XXXXX
Issued: 2024-01-20
Expires: 2025-12-31
```

---

## 4. License File Generation

### 4.1 Admin Portal Steps

1. Navigate to **License Keys** in Admin Portal
2. Select the license to export
3. Click **Actions** → **Generate Offline License**
4. Configure options:
   - **Hardware Binding**: Enable if license is device-specific
   - **Domain Binding**: Leave empty for USB-based licenses
   - **Grace Period**: Set to 30-90 days
   - **Environment**: Match your deployment environment
5. Click **Generate**
6. Download `license.lic` file

### 4.2 API-Based Generation

```bash
curl -X POST https://your-domain.com/api/v1/licenses/{license_key}/offline-file \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "hardware_id": null,
    "domain": null,
    "grace_period_days": 30,
    "environment": "production"
  }' \
  -o license.lic
```

### 4.3 License File Structure

See [OFFLINE_LICENSE_FORMAT.md](./OFFLINE_LICENSE_FORMAT.md) for complete specifications.

**Key fields for USB deployment:**

```json
{
  "version": "1.0",
  "license": {
    "key": "XXXXX-XXXXX-XXXXX-XXXXX",
    "status": "active",
    "expires_at": "2025-12-31T23:59:59Z",
    "hardware_id": null,
    "domain": null,
    "features": {
      "max_users": 100,
      "modules": ["crm", "analytics"]
    },
    "activations_limit": 0,
    "activations_count": 0
  },
  "grace_period_days": 30,
  "last_verified_at": "2024-01-20T10:00:00Z",
  "signature": "BASE64_RSA_SIGNATURE"
}
```

**Note:** Set `hardware_id` to `null` and `activations_limit` to `0` for USB-based licenses.

---

## 5. Application Integration

### 5.1 License Validation Library

All platforms should use the appropriate SDK:

- **PHP**: `sdks/php/LicenseClient.php`
- **JavaScript/Node**: `sdks/javascript/license-client.js`
- **.NET**: Community SDK (see SDK_TELEMETRY_UPDATE_GUIDE.md)
- **Python**: Community SDK
- **Go**: Community SDK

### 5.2 USB Detection

#### Finding USB Drive

**Windows (PowerShell):**
```powershell
# Find USB drive by volume label
$usbDrive = Get-WmiObject Win32_LogicalDisk | 
    Where-Object { $_.DriveType -eq 2 -and $_.VolumeName -eq "LICENSE" }

if ($usbDrive) {
    $licensePath = Join-Path $usbDrive.DeviceID "license.lic"
    Write-Host "License found at: $licensePath"
}
```

**Linux (Bash):**
```bash
# Find USB drive by label
USB_MOUNT=$(findmnt -n -o TARGET LABEL=LICENSE)

if [ -n "$USB_MOUNT" ]; then
    LICENSE_PATH="$USB_MOUNT/license.lic"
    echo "License found at: $LICENSE_PATH"
fi
```

**Cross-Platform (Python):**
```python
import os
import platform

def find_license_usb():
    """Find USB drive with license file"""
    system = platform.system()
    
    if system == "Windows":
        # Check all drive letters
        for drive in "DEFGHIJKLMNOPQRSTUVWXYZ":
            path = f"{drive}:\\license.lic"
            if os.path.exists(path):
                return path
    elif system == "Linux":
        # Check common mount points
        mount_points = [
            "/media",
            "/mnt",
            "/run/media/$USER"
        ]
        for mount in mount_points:
            if os.path.exists(mount):
                for device in os.listdir(mount):
                    path = os.path.join(mount, device, "license.lic")
                    if os.path.exists(path):
                        return path
    return None
```

### 5.3 Continuous USB Monitoring (Optional)

Monitor USB presence during runtime to ensure license isn't removed:

**Python Example:**
```python
import os
import time
import sys

class USBLicenseMonitor:
    def __init__(self, license_path, check_interval=60):
        self.license_path = license_path
        self.check_interval = check_interval
        self.running = True
    
    def start(self):
        """Start monitoring in background thread"""
        import threading
        thread = threading.Thread(target=self._monitor_loop)
        thread.daemon = True
        thread.start()
    
    def _monitor_loop(self):
        """Continuous monitoring loop"""
        while self.running:
            if not os.path.exists(self.license_path):
                print("ERROR: License USB removed!")
                print("Please reinsert the USB drive to continue.")
                # Pause application or exit
                sys.exit(1)
            time.sleep(self.check_interval)
    
    def stop(self):
        self.running = False

# Usage
monitor = USBLicenseMonitor("/path/to/license.lic", check_interval=30)
monitor.start()
```

---

## 6. Platform-Specific Implementation

### 6.1 .NET / C# Application

```csharp
using System;
using System.IO;
using System.Linq;
using LicenseManager.SDK;

public class USBLicenseValidator
{
    private string licensePath;
    private LicenseClient client;
    
    public USBLicenseValidator()
    {
        // Find USB drive
        var drives = DriveInfo.GetDrives()
            .Where(d => d.DriveType == DriveType.Removable)
            .Where(d => File.Exists(Path.Combine(d.RootDirectory.FullName, "license.lic")));
        
        var usbDrive = drives.FirstOrDefault();
        if (usbDrive == null)
        {
            throw new Exception("License USB drive not found!");
        }
        
        licensePath = Path.Combine(usbDrive.RootDirectory.FullName, "license.lic");
        string publicKeyPath = Path.Combine(usbDrive.RootDirectory.FullName, "public-key.pem");
        
        // Initialize client
        client = new LicenseClient(new LicenseClientConfig
        {
            ApiKey = "not-used-offline",
            PublicKey = File.ReadAllText(publicKeyPath)
        });
    }
    
    public LicenseValidationResult Validate()
    {
        string licenseContent = File.ReadAllText(licensePath);
        
        var result = client.ValidateOfflineLicense(licenseContent, new ValidateOptions
        {
            HardwareId = null // Or generate if needed
        });
        
        if (!result.Valid)
        {
            throw new Exception($"License validation failed: {string.Join(", ", result.Errors)}");
        }
        
        return result;
    }
    
    public void StartMonitoring(Action onUSBRemoved)
    {
        var watcher = new FileSystemWatcher(Path.GetDirectoryName(licensePath))
        {
            NotifyFilter = NotifyFilters.FileName | NotifyFilters.DirectoryName
        };
        
        watcher.Deleted += (sender, e) =>
        {
            if (e.FullPath == licensePath)
            {
                onUSBRemoved?.Invoke();
            }
        };
        
        watcher.EnableRaisingEvents = true;
    }
}

// Usage in Main()
class Program
{
    static void Main(string[] args)
    {
        try
        {
            var validator = new USBLicenseValidator();
            var result = validator.Validate();
            
            Console.WriteLine($"License valid for: {result.License.Key}");
            Console.WriteLine($"Features: {string.Join(", ", result.License.Features.Keys)}");
            
            // Start monitoring
            validator.StartMonitoring(() =>
            {
                Console.WriteLine("USB removed! Exiting...");
                Environment.Exit(1);
            });
            
            // Run application
            RunApplication(result.License);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"License error: {ex.Message}");
            Environment.Exit(1);
        }
    }
    
    static void RunApplication(License license)
    {
        Console.WriteLine("Application running...");
        // Your application logic here
        Console.ReadLine();
    }
}
```

### 6.2 Python Application

```python
#!/usr/bin/env python3
import os
import sys
import json
import time
from pathlib import Path

# Assuming you have the Python SDK
from licensemanager import LicenseClient

class USBLicenseManager:
    def __init__(self):
        self.license_path = self.find_license_usb()
        if not self.license_path:
            raise Exception("License USB drive not found!")
        
        self.usb_root = Path(self.license_path).parent
        self.public_key_path = self.usb_root / "public-key.pem"
        self.config_path = self.usb_root / "config.json"
        
        # Load config
        with open(self.config_path) as f:
            self.config = json.load(f)
        
        # Initialize client
        self.client = LicenseClient({
            'apiKey': 'not-used-offline',
            'publicKey': open(self.public_key_path).read()
        })
    
    def find_license_usb(self):
        """Find USB drive containing license file"""
        # Linux
        if sys.platform.startswith('linux'):
            for root in ['/media', '/mnt', f'/run/media/{os.getenv("USER")}']:
                if os.path.exists(root):
                    for device in os.listdir(root):
                        license_path = os.path.join(root, device, 'license.lic')
                        if os.path.exists(license_path):
                            return license_path
        
        # Windows
        elif sys.platform == 'win32':
            import string
            for drive in string.ascii_uppercase:
                license_path = f'{drive}:\\license.lic'
                if os.path.exists(license_path):
                    return license_path
        
        return None
    
    def validate(self):
        """Validate license from USB"""
        with open(self.license_path) as f:
            license_data = f.read()
        
        result = self.client.validate_offline_license(license_data)
        
        if not result['valid']:
            raise Exception(f"License validation failed: {', '.join(result['errors'])}")
        
        return result
    
    def monitor_usb(self, check_interval=30):
        """Monitor USB presence"""
        while True:
            if not os.path.exists(self.license_path):
                print("ERROR: License USB removed!")
                sys.exit(1)
            time.sleep(check_interval)

# Usage
if __name__ == '__main__':
    try:
        manager = USBLicenseManager()
        result = manager.validate()
        
        print(f"✓ License valid: {result['license']['key']}")
        print(f"✓ Expires: {result['license']['expires_at']}")
        print(f"✓ Features: {', '.join(result['license']['features'].keys())}")
        
        # Start USB monitoring in background
        import threading
        monitor_thread = threading.Thread(target=manager.monitor_usb)
        monitor_thread.daemon = True
        monitor_thread.start()
        
        # Run application
        print("\nApplication running...")
        print("Press Ctrl+C to exit")
        
        while True:
            time.sleep(1)
            # Your application logic here
    
    except KeyboardInterrupt:
        print("\nExiting...")
        sys.exit(0)
    except Exception as e:
        print(f"ERROR: {e}")
        sys.exit(1)
```

### 6.3 Go Application

```go
package main

import (
    "encoding/json"
    "fmt"
    "io/ioutil"
    "os"
    "path/filepath"
    "time"
    
    "github.com/yourorg/licensemanager-go"
)

type USBLicenseManager struct {
    LicensePath string
    PublicKeyPath string
    Client *licensemanager.Client
}

func NewUSBLicenseManager() (*USBLicenseManager, error) {
    // Find USB drive
    licensePath, err := findLicenseUSB()
    if err != nil {
        return nil, err
    }
    
    usbRoot := filepath.Dir(licensePath)
    publicKeyPath := filepath.Join(usbRoot, "public-key.pem")
    
    // Read public key
    publicKey, err := ioutil.ReadFile(publicKeyPath)
    if err != nil {
        return nil, fmt.Errorf("failed to read public key: %w", err)
    }
    
    // Initialize client
    client := licensemanager.NewClient(licensemanager.Config{
        APIKey: "not-used-offline",
        PublicKey: string(publicKey),
    })
    
    return &USBLicenseManager{
        LicensePath: licensePath,
        PublicKeyPath: publicKeyPath,
        Client: client,
    }, nil
}

func findLicenseUSB() (string, error) {
    // Check Windows drives
    if runtime.GOOS == "windows" {
        for drive := 'D'; drive <= 'Z'; drive++ {
            path := fmt.Sprintf("%c:\\license.lic", drive)
            if _, err := os.Stat(path); err == nil {
                return path, nil
            }
        }
    }
    
    // Check Linux mount points
    if runtime.GOOS == "linux" {
        mountPoints := []string{"/media", "/mnt"}
        for _, mount := range mountPoints {
            filepath.Walk(mount, func(path string, info os.FileInfo, err error) error {
                if err == nil && info.Name() == "license.lic" {
                    return filepath.SkipDir
                }
                return nil
            })
        }
    }
    
    return "", fmt.Errorf("license USB not found")
}

func (m *USBLicenseManager) Validate() (*licensemanager.ValidationResult, error) {
    // Read license file
    licenseData, err := ioutil.ReadFile(m.LicensePath)
    if err != nil {
        return nil, fmt.Errorf("failed to read license: %w", err)
    }
    
    // Validate
    result, err := m.Client.ValidateOfflineLicense(string(licenseData), nil)
    if err != nil {
        return nil, err
    }
    
    if !result.Valid {
        return nil, fmt.Errorf("validation failed: %v", result.Errors)
    }
    
    return result, nil
}

func (m *USBLicenseManager) MonitorUSB(interval time.Duration, onRemoved func()) {
    ticker := time.NewTicker(interval)
    defer ticker.Stop()
    
    for range ticker.C {
        if _, err := os.Stat(m.LicensePath); os.IsNotExist(err) {
            fmt.Println("ERROR: License USB removed!")
            if onRemoved != nil {
                onRemoved()
            }
            os.Exit(1)
        }
    }
}

func main() {
    // Initialize
    manager, err := NewUSBLicenseManager()
    if err != nil {
        fmt.Printf("License error: %v\n", err)
        os.Exit(1)
    }
    
    // Validate
    result, err := manager.Validate()
    if err != nil {
        fmt.Printf("Validation error: %v\n", err)
        os.Exit(1)
    }
    
    fmt.Printf("✓ License valid: %s\n", result.License.Key)
    fmt.Printf("✓ Expires: %s\n", result.License.ExpiresAt)
    
    // Start monitoring
    go manager.MonitorUSB(30*time.Second, func() {
        fmt.Println("USB removed, exiting...")
    })
    
    // Run application
    fmt.Println("Application running...")
    select {} // Run forever
}
```

### 6.4 PHP Application

```php
<?php
require 'vendor/autoload.php';

use LicenseManager\SDK\LicenseClient;

class USBLicenseManager
{
    private $licensePath;
    private $publicKeyPath;
    private $client;
    
    public function __construct()
    {
        // Find USB drive
        $this->licensePath = $this->findLicenseUSB();
        if (!$this->licensePath) {
            throw new Exception("License USB drive not found!");
        }
        
        $usbRoot = dirname($this->licensePath);
        $this->publicKeyPath = $usbRoot . '/public-key.pem';
        
        // Initialize client
        $this->client = new LicenseClient([
            'apiKey' => 'not-used-offline',
            'publicKey' => file_get_contents($this->publicKeyPath)
        ]);
    }
    
    private function findLicenseUSB()
    {
        // Windows
        if (strtoupper(substr(PHP_OS, 0, 3)) === 'WIN') {
            foreach (range('D', 'Z') as $drive) {
                $path = "{$drive}:\\license.lic";
                if (file_exists($path)) {
                    return $path;
                }
            }
        }
        
        // Linux
        else {
            $mountPoints = ['/media', '/mnt', '/run/media/' . get_current_user()];
            foreach ($mountPoints as $mount) {
                if (!is_dir($mount)) continue;
                
                foreach (scandir($mount) as $device) {
                    if ($device === '.' || $device === '..') continue;
                    
                    $path = "{$mount}/{$device}/license.lic";
                    if (file_exists($path)) {
                        return $path;
                    }
                }
            }
        }
        
        return null;
    }
    
    public function validate()
    {
        $licenseData = file_get_contents($this->licensePath);
        
        $result = $this->client->validateOfflineLicense($licenseData);
        
        if (!$result['valid']) {
            throw new Exception("License validation failed: " . implode(', ', $result['errors']));
        }
        
        return $result;
    }
    
    public function monitorUSB($interval = 30, $onRemoved = null)
    {
        while (true) {
            if (!file_exists($this->licensePath)) {
                echo "ERROR: License USB removed!\n";
                if ($onRemoved) {
                    call_user_func($onRemoved);
                }
                exit(1);
            }
            sleep($interval);
        }
    }
}

// Usage
try {
    $manager = new USBLicenseManager();
    $result = $manager->validate();
    
    echo "✓ License valid: {$result['license']['key']}\n";
    echo "✓ Expires: {$result['license']['expires_at']}\n";
    echo "✓ Features: " . implode(', ', array_keys($result['license']['features'])) . "\n";
    
    // Start monitoring in background (requires pcntl extension)
    if (extension_loaded('pcntl')) {
        $pid = pcntl_fork();
        if ($pid == 0) {
            // Child process - monitor USB
            $manager->monitorUSB(30);
        }
    }
    
    // Run application
    echo "\nApplication running...\n";
    echo "Press Ctrl+C to exit\n";
    
    while (true) {
        sleep(1);
        // Your application logic here
    }
    
} catch (Exception $e) {
    echo "ERROR: {$e->getMessage()}\n";
    exit(1);
}
```

### 6.5 Electron.js Application

```javascript
const { app, BrowserWindow, dialog } = require('electron');
const fs = require('fs');
const path = require('path');
const { LicenseClient } = require('@yourorg/licensemanager-sdk');

class USBLicenseManager {
    constructor() {
        this.licensePath = this.findLicenseUSB();
        if (!this.licensePath) {
            throw new Error('License USB drive not found!');
        }
        
        const usbRoot = path.dirname(this.licensePath);
        const publicKeyPath = path.join(usbRoot, 'public-key.pem');
        
        this.client = new LicenseClient({
            apiKey: 'not-used-offline',
            publicKey: fs.readFileSync(publicKeyPath, 'utf8')
        });
    }
    
    findLicenseUSB() {
        // Windows
        if (process.platform === 'win32') {
            for (let drive = 68; drive <= 90; drive++) { // D-Z
                const letter = String.fromCharCode(drive);
                const licensePath = `${letter}:\\license.lic`;
                if (fs.existsSync(licensePath)) {
                    return licensePath;
                }
            }
        }
        
        // Linux/Mac
        else {
            const mountPoints = ['/media', '/mnt', `/run/media/${process.env.USER}`];
            for (const mount of mountPoints) {
                if (!fs.existsSync(mount)) continue;
                
                const devices = fs.readdirSync(mount);
                for (const device of devices) {
                    const licensePath = path.join(mount, device, 'license.lic');
                    if (fs.existsSync(licensePath)) {
                        return licensePath;
                    }
                }
            }
        }
        
        return null;
    }
    
    async validate() {
        const licenseData = fs.readFileSync(this.licensePath, 'utf8');
        
        const result = await this.client.validateOfflineLicense(licenseData);
        
        if (!result.valid) {
            throw new Error(`License validation failed: ${result.errors.join(', ')}`);
        }
        
        return result;
    }
    
    startMonitoring(interval = 30000) {
        setInterval(() => {
            if (!fs.existsSync(this.licensePath)) {
                dialog.showErrorBox(
                    'License USB Removed',
                    'The license USB drive has been removed. The application will now exit.'
                );
                app.quit();
            }
        }, interval);
    }
}

// Main application
app.whenReady().then(async () => {
    try {
        // Initialize license manager
        const licenseManager = new USBLicenseManager();
        
        // Validate license
        const result = await licenseManager.validate();
        
        console.log(`✓ License valid: ${result.license.key}`);
        console.log(`✓ Expires: ${result.license.expires_at}`);
        
        // Start USB monitoring
        licenseManager.startMonitoring(30000);
        
        // Create main window
        const mainWindow = new BrowserWindow({
            width: 1200,
            height: 800,
            webPreferences: {
                nodeIntegration: true,
                contextIsolation: false
            }
        });
        
        // Pass license info to renderer
        mainWindow.webContents.once('dom-ready', () => {
            mainWindow.webContents.send('license-info', result.license);
        });
        
        mainWindow.loadFile('index.html');
        
    } catch (error) {
        dialog.showErrorBox('License Error', error.message);
        app.quit();
    }
});

app.on('window-all-closed', () => {
    if (process.platform !== 'darwin') {
        app.quit();
    }
});
```

---

## 7. Security Considerations

### 7.1 Physical Security

✅ **USB Drive Protection**
- Use branded/custom USB drives
- Optional: Hardware write-protection
- Serial number tracking
- Tamper-evident packaging

✅ **Access Control**
- Limit USB distribution
- Track USB assignments
- Audit USB usage logs

### 7.2 Cryptographic Security

✅ **Signature Verification**
- Always verify RSA signature
- Never trust unverified data
- Use RSA-4096 minimum
- Rotate keys periodically

✅ **Public Key Distribution**
- Embed in application binary
- Code sign application
- Use secure update channels

### 7.3 Anti-Tampering

✅ **Application Protection**
- Code obfuscation
- Anti-debugging measures
- Integrity checks
- Secure key storage

✅ **License File Protection**
- Read-only USB formatting
- File integrity monitoring
- Checksum verification
- Audit logging

### 7.4 Monitoring & Detection

✅ **Telemetry**
- Send validation events (when online)
- Report anomalies
- Track feature usage
- Detect suspicious patterns

✅ **Logging**
- Local validation logs
- USB insertion/removal events
- Application lifecycle events
- Error conditions

---

## 8. Troubleshooting

### 8.1 Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| USB not detected | Wrong drive letter/mount | Check OS-specific paths |
| Signature verification failed | Wrong public key or tampered file | Re-generate license file |
| License expired | Past expiration date | Generate new license |
| USB removed error | Physical disconnect | Ensure USB stays connected |
| Permission denied | File/folder permissions | Check read permissions |
| Grace period expired | Too long offline | Re-generate with new timestamp |

### 8.2 Debug Checklist

```bash
# 1. Verify USB is mounted
# Windows:
wmic logicaldisk get deviceid,volumename

# Linux:
lsblk -o NAME,LABEL,MOUNTPOINT

# 2. Check file exists
ls -la /path/to/usb/license.lic

# 3. Verify file integrity
cat /path/to/usb/license.lic | head -n 5

# 4. Check permissions
# Windows:
icacls E:\license.lic

# Linux:
ls -l /path/to/usb/license.lic

# 5. Test signature verification
openssl dgst -sha256 -verify public-key.pem \
    -signature signature.bin license-data.txt
```

### 8.3 Validation Logs

Enable detailed logging in your application:

```json
{
  "timestamp": "2024-01-20T10:30:00Z",
  "event": "license_validation",
  "result": "success",
  "license_key": "XXXXX-XXXXX-XXXXX-XXXXX",
  "usb_path": "E:\\license.lic",
  "signature_valid": true,
  "expiration_check": "pass",
  "hardware_check": "skipped",
  "features_loaded": ["module_a", "module_b"]
}
```

---

## 9. Best Practices

### 9.1 For Administrators

1. **License Generation**
   - Generate licenses with appropriate grace periods
   - Set `hardware_id` to `null` for USB licenses
   - Set `activations_limit` to `0`
   - Include all necessary features

2. **USB Preparation**
   - Use quality USB drives
   - Format as FAT32/exFAT
   - Include README with support info
   - Label physically

3. **Distribution**
   - Track USB serial numbers
   - Document customer assignments
   - Provide clear instructions
   - Include support contact info

4. **Maintenance**
   - Periodic license renewals
   - Update public keys when rotating
   - Monitor validation logs
   - Handle expired licenses proactively

### 9.2 For Developers

1. **Implementation**
   - Validate on startup
   - Implement periodic re-validation
   - Monitor USB presence
   - Handle errors gracefully

2. **User Experience**
   - Clear error messages
   - Helpful instructions
   - Grace period warnings
   - Support contact info

3. **Security**
   - Never skip signature verification
   - Protect public keys
   - Obfuscate validation code
   - Log all validation attempts

4. **Testing**
   - Test on target platforms
   - Test USB removal scenarios
   - Test grace period expiration
   - Test various error conditions

### 9.3 For End Users

1. **USB Care**
   - Keep USB connected during use
   - Store safely when not in use
   - Don't modify files
   - Back up if allowed

2. **Troubleshooting**
   - Check USB connection
   - Verify correct drive letter
   - Contact support if issues
   - Don't share USB

---

## 10. Appendix

### 10.1 Sample Deployment Package

Create a complete deployment package:

```
deployment-package/
├── application/
│   ├── YourApp.exe           # Application executable
│   └── dependencies/          # Required libraries
├── usb-setup/
│   ├── license.lic           # Generated license file
│   ├── public-key.pem        # Public key
│   ├── config.json           # Configuration
│   └── README.txt            # User instructions
├── installer/
│   ├── setup.exe             # Installation wizard
│   └── setup-guide.pdf       # Installation guide
└── documentation/
    ├── user-manual.pdf       # User manual
    ├── quick-start.pdf       # Quick start guide
    └── troubleshooting.pdf   # Troubleshooting guide
```

### 10.2 Additional Resources

- **Admin Portal Guide**: `/docs/admin-portal-user-guide.md`
- **API Developer Guide**: `/docs/api-developer-guide.md`
- **License Lifecycle**: `/docs/license-lifecycle.md`
- **Offline License Format**: `/docs/OFFLINE_LICENSE_FORMAT.md`
- **SDK Update Guide**: `/SDK_TELEMETRY_UPDATE_GUIDE.md`

### 10.3 Support

For questions or issues:
- Review documentation: `/docs/`
- Check SDK examples: `/sdks/*/examples/`
- Contact: support@getkeymanager.com

---

**Document Version:** 1.0  
**Last Updated:** 2026-01-23  
**Status:** Production Ready

---

END OF USB-BASED OFFLINE LICENSE MANAGEMENT GUIDE
