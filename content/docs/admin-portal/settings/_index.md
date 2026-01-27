---
title: Settings
weight: 200
---

# Settings

![Admin Portal Settings Overview](placeholder-settings-overview.png)
*Screenshot showing the settings interface with all 11 tabs*

---

## What Are Settings?

The Settings area is the **central configuration hub** for your entire License Management Platform. It's organized into **11 distinct tabs**, each controlling a critical aspect of system behavior, integrations, and security.

**Access Level**: Super Admin and Admin roles only

---

## Settings Tabs

The settings are organized into 11 categories. Click any tab below to view detailed documentation:

### [1. General Settings](settings/general)

Configure basic platform identity, branding, and display settings.

**Key Settings:** Application name, support email/URL, logo upload, landing page

---

### [2. License Settings](settings/license)

Control how license verification behaves across the platform.

**Key Settings:** Require license verification, verification cache duration, auto-renewal

---

### [3. Email Settings](settings/email)

Configure SMTP and email delivery for automated communications.

**Key Settings:** Email driver, SMTP configuration, from address, test email

---

### [4. S3/Storage Settings](settings/storage)

Configure cloud storage for product images, downloadable files, and backups.

**Key Settings:** S3 credentials, bucket configuration, test connection

---

### [5. Changelog Settings](settings/changelog)

Control the public-facing product changelog feature.

**Key Settings:** Enable changelog, public access, items per page, slug

---

### [6. Telemetry Settings](settings/telemetry)

Configure usage data collection from products in the field.

**Key Settings:** Enable telemetry, storage duration

---

### [7. Webhook Settings](settings/webhooks)

Configure webhook delivery log retention.

**Key Settings:** Retention days for webhook delivery logs

---

### [8. Logging Settings](settings/logging)

Control what system activities are logged.

**Key Settings:** Log dashboard activities, API calls, failed calls, blocklisted calls

---

### [9. KeyManager License](settings/keymanager-license)

Configure the platform's own license key (if using commercial version).

**Key Settings:** Platform license key

---

### [10. Envato Integration](settings/envato)

Connect to Envato Marketplace for automatic license synchronization.

**Key Settings:** Envato personal token, auto-create products

---

### [11. Abuse Detection](settings/abuse-detection)

Protect licenses from misuse with intelligent monitoring and automatic enforcement.

**Key Settings:** Enable abuse detection, abuse threshold, auto-suspend

---

## How to Access

1. Log in to the Admin Portal with your admin credentials
2. Click **Settings** in the main navigation menu
3. Select the specific tab you want to configure

**Keyboard Shortcut**: Press `Ctrl+K` (Windows) or `Cmd+K` (Mac) to open Global Search, then type "settings".

---

## Common Tasks

1. **Initial Setup**: Configure General, Email, and Storage settings first
2. **Email Configuration**: Set up SMTP in Email Settings and test
3. **Storage Setup**: Configure S3 credentials and test connection
4. **Security Hardening**: Enable Abuse Detection and configure thresholds
5. **Integration**: Set up Envato or other third-party integrations

---

## Best Practices

✅ Complete all required settings during initial setup  
✅ Test email and storage configurations before going live  
✅ Review security settings (logging, abuse detection) regularly  
✅ Document your configuration choices for your team  
✅ Use environment-specific settings for staging vs production  

---

## Related Pages

- [Dashboard]({{< ref "/docs/docs/content/docs/admin-portal/dashboard" >}}) - Main overview
- [Profile]({{< ref "/docs/docs/content/docs/admin-portal/profile" >}}) - Your admin profile
- [Logs]({{< ref "/docs/docs/content/docs/admin-portal/logs" >}}) - View system logs
