---
title: Settings
weight: 200
---

![Admin Portal Settings Screenshot](placeholder-settings-overview.png)
*Screenshot will be added showing the settings interface with all 11 tabs*

---

## What Is This Page?

The Settings page is the **central configuration hub** for your entire License Management Platform. It contains **11 distinct tabs**, each controlling a critical aspect of system behavior, integrations, and security.

This is where you:
- Configure essential services (email, storage, integrations)
- Control security and compliance settings
- Enable or disable platform features
- Set operational parameters

**Access Level**: Super Admin and Admin roles only

---

## When to Use This Page

Use the Settings page when you need to:

✅ **Initial Setup**: Configure the platform for first use  
✅ **Integration**: Connect external services (S3, email providers, Envato)  
✅ **Troubleshooting**: Test email delivery or storage connections  
✅ **Security Hardening**: Enable abuse detection or configure logging  
✅ **Compliance**: Set data retention policies  
✅ **Optimization**: Adjust cache durations and performance settings  

---

## The 11 Settings Tabs

![Settings Navigation Tabs](placeholder-settings-tabs.png)
*Screenshot showing all 11 tabs in the settings interface*

---

# Tab 1: General Settings

Configure basic platform identity and branding.

![General Settings Tab](placeholder-settings-general.png)
*Screenshot of General Settings tab*

## Application Name

**Type:** Text input  
**Default:** "GetKeyManager"

### Description

The display name shown throughout the platform interface, including:
- Admin portal header
- Client portal branding
- Email footers
- Public changelog pages

### How to Use

1. Enter your company or product name
2. Click "Save Settings"
3. Refresh the page to see changes

### Examples

| Business Type | Suggested Name |
|---------------|----------------|
| Software Company | "Acme Software Licensing" |
| SaaS Platform | "CloudApp License Manager" |
| Marketplace Vendor | "MyProduct Licenses" |

---

## Support Email

**Type:** Email input  
**Required:** Yes

### Description

The primary contact email displayed to users for support requests. This email appears in:
- Error messages
- Email templates
- Client portal footer
- Public documentation

### Best Practices

✅ Use a monitored inbox (e.g., support@yourdomain.com)  
✅ Set up auto-responders for after-hours  
✅ Ensure email can receive attachments  
⚠️ Avoid personal email addresses  
⚠️ Don't use no-reply addresses  

---

## Support URL

**Type:** URL input  
**Required:** Yes

### Description

Link to your helpdesk, knowledge base, or support portal. Displayed alongside the support email.

### Examples

- `https://support.yourdomain.com`
- `https://help.yourproduct.com`
- `https://yourdomain.com/contact`

---

## Logo Upload

**Type:** File upload  
**Format:** PNG, JPG, GIF  
**Max Size:** 2MB  
**Recommended:** 200x200px with transparent background

### Description

Your company or product logo, stored in S3 and displayed:
- In the admin portal header
- In the client portal
- In email templates
- On public changelog pages

### How to Upload

1. Click "Choose File"
2. Select your logo image
3. Click "Save Settings"
4. Image is automatically uploaded to S3

### Tips

💡 Use PNG format for transparency  
💡 Keep file size under 500KB for fast loading  
💡 Test logo appearance in both light and dark modes  
💡 Use square dimensions for best results  

---

## Landing Page

**Type:** Toggle (Enable/Disable)  
**Default:** Disabled

### Description

When enabled, displays a public landing page at your root domain explaining what the platform is for.

**Enabled:** Root URL shows landing page  
**Disabled:** Root URL redirects to login

### When to Enable

- You want a public-facing presence
- You have multiple user types visiting the domain
- You need SEO-friendly content at the root

### When to Disable

- Platform is internal-only
- You prefer direct login access
- You have a separate marketing website

---

# Tab 2: License Settings

Control how license verification behaves across the platform.

![License Settings Tab](placeholder-settings-license.png)
*Screenshot of License Settings tab*

## Require License Verification

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Global toggle that enforces license validation for all API calls and activations.

**ON**: All license operations require valid, active licenses  
**OFF**: Permissive mode – licenses can be bypassed (development only)

### When to Enable

✅ Production environments  
✅ Live customer deployments  
✅ Marketplace integrations  
✅ Security-critical applications  

### When to Disable

🔧 Development and testing  
🔧 Internal QA environments  
🔧 Debugging license issues  

> ⚠️ **Warning**: Never disable in production. This bypasses all license security.

---

## Verification Cache Duration

**Type:** Numeric input (seconds)  
**Default:** 3600 (1 hour)  
**Range:** 60 - 86400 seconds

### Description

How long license validation responses are cached before re-checking with the server.

**Lower values**: More accurate, more API calls  
**Higher values**: Better performance, less real-time

### How It Works

1. Client validates license with server
2. Response is cached locally for X seconds
3. During cache period, offline validation is used
4. After expiry, server is checked again

### Recommended Values

| Use Case | Duration | Reasoning |
|----------|----------|-----------|
| SaaS APIs | 300s (5 min) | Frequent checks for real-time control |
| Desktop Software | 3600s (1 hour) | Balance of accuracy and performance |
| Offline Tools | 86400s (24 hours) | Minimize server dependency |
| Development | 60s (1 min) | Quick feedback during testing |

### Tips

💡 Consider your internet connectivity requirements  
💡 Shorter duration = more server load  
💡 Balance security needs with user experience  

---

## Enable Auto License Renewal

**Type:** Toggle (On/Off)  
**Default:** Off

### Description

Automatically extends license expiration dates based on configured rules (e.g., subscription renewal detection).

**ON**: Licenses are auto-renewed when conditions are met  
**OFF**: Manual renewal required

### Prerequisites

- Integrated payment system or subscription service
- Renewal webhooks configured
- Contract terms allow automatic renewal

### When to Enable

✅ Subscription-based products  
✅ Integrated with payment processor  
✅ Automated billing system  

### When to Disable

❌ One-time purchases  
❌ Manual license management  
❌ Complex renewal approval workflows  

---

# Tab 3: Email Settings

Configure SMTP and email delivery for automated communications.

![Email Settings Tab](placeholder-settings-email.png)
*Screenshot of Email Settings tab*

## Overview

Email settings control how the platform sends:
- License assignment notifications
- Expiry warnings
- Password reset emails
- Admin alerts
- Custom email templates

---

## Email Driver

**Type:** Dropdown selection

### Available Options

| Driver | Description | Best For |
|--------|-------------|----------|
| **SMTP** | Standard email protocol | Most providers, full control |
| **Sendmail** | Unix sendmail command | Server-based, simple setup |
| **Mailgun** | Mailgun API integration | High volume, tracking |
| **SES** | Amazon SES integration | AWS users, scalability |

### Choosing a Driver

**Use SMTP if:**
- You have an existing email account (Gmail, Outlook, custom)
- You need maximum compatibility
- You want detailed control

**Use Mailgun/SES if:**
- You send high email volumes (>1000/day)
- You need delivery analytics
- You want webhook notifications

---

## SMTP Configuration

### Host

**Type:** Text input  
**Example:** `smtp.gmail.com`, `smtp.office365.com`

The SMTP server address provided by your email service.

**Common SMTP Hosts:**

| Provider | SMTP Host |
|----------|-----------|
| Gmail | smtp.gmail.com |
| Office 365 | smtp.office365.com |
| SendGrid | smtp.sendgrid.net |
| Custom | mail.yourdomain.com |

---

### Port

**Type:** Numeric input

**Standard Ports:**

| Port | Encryption | Use Case |
|------|------------|----------|
| **587** | TLS (STARTTLS) | **Recommended** - Modern standard |
| **465** | SSL/TLS | Older standard, still widely supported |
| 25 | None | Unencrypted (not recommended) |

> 💡 **Tip**: Port 587 with TLS is the most compatible option

---

### Username

**Type:** Text input

Your email account username, typically your full email address.

**Examples:**
- `notifications@yourdomain.com`
- `noreply@yourcompany.com`
- `your.email@gmail.com`

---

### Password

**Type:** Password input (encrypted at rest)

Your email account password or app-specific password.

### Security Notes

🔒 Password is encrypted before storage  
🔒 Never displayed after initial entry  
🔒 Use app-specific passwords when possible (Gmail, Outlook)  

### App-Specific Passwords

For Gmail and similar providers:
1. Enable 2FA on your account
2. Generate an app-specific password
3. Use that password here instead of your main password

---

### Encryption

**Type:** Dropdown  
**Options:** TLS, SSL

**TLS (Transport Layer Security):**
- Modern standard
- Used with port 587
- **Recommended**

**SSL (Secure Sockets Layer):**
- Older standard
- Used with port 465
- Still widely supported

---

## From Address

**Type:** Email input  
**Required:** Yes

The email address that appears in the "From" field of all outgoing emails.

### Best Practices

✅ Use no-reply@ or notifications@ addresses  
✅ Match your domain for better deliverability  
✅ Avoid generic addresses like info@ or admin@  

**Examples:**
- `noreply@yourdomain.com`
- `licenses@yourproduct.com`
- `system@yourcompany.com`

---

## From Name

**Type:** Text input  
**Required:** Yes

The friendly name shown alongside the from address.

### Examples

| Business | From Name |
|----------|-----------|
| Software Company | "Acme Software Licensing" |
| SaaS | "CloudApp Notifications" |
| Product | "MyProduct License System" |

---

## Test Email Functionality

### Description

Send a test email to verify your SMTP configuration is working correctly.

### How to Use

1. Configure all SMTP settings above
2. Enter a test recipient email address
3. Click "Send Test Email"
4. Check the recipient inbox (and spam folder)

### Troubleshooting

| Issue | Solution |
|-------|----------|
| Connection timeout | Check host and port are correct |
| Authentication failed | Verify username and password |
| Email not received | Check spam folder, verify from address |
| SSL/TLS errors | Try different encryption settings |

💡 **Tip**: Always test emails before going live!

---

# Tab 4: S3/Storage Settings

Configure cloud storage for product images, downloadable files, and backups.

![S3 Storage Settings Tab](placeholder-settings-s3.png)
*Screenshot of S3/Storage Settings tab*

## Overview

S3 (or S3-compatible) storage is **required** for:
- Product logos and images
- Downloadable software versions
- License file exports
- Backup files
- Generated reports

**No files are stored on local disk** - all persistent storage uses S3.

---

## Storage Driver

**Type:** Dropdown  
**Options:** S3, S3-compatible

**Amazon S3**: Native AWS S3 integration  
**S3-Compatible**: Works with DigitalOcean Spaces, Wasabi, MinIO, Backblaze B2, etc.

---

## Access Key

**Type:** Text input  
**Required:** Yes

Your AWS Access Key ID or equivalent from your storage provider.

**Format:** `AKIAIOSFODNN7EXAMPLE`

### Where to Find

**AWS S3:**
1. Go to IAM Console
2. Create/select a user
3. Security Credentials tab
4. Create Access Key

**Other Providers:**
- Check your provider's API settings or credentials page

---

## Secret Key

**Type:** Password input (encrypted at rest)  
**Required:** Yes

Your AWS Secret Access Key or equivalent.

**Format:** `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`

### Security

🔒 Encrypted before storage  
🔒 Never logged or displayed  
🔒 Restricted to required S3 operations only  

---

## Region

**Type:** Text input  
**Required:** Yes

The AWS region or storage region where your bucket is located.

### AWS Regions

| Region Code | Location |
|-------------|----------|
| `us-east-1` | N. Virginia |
| `us-west-2` | Oregon |
| `eu-west-1` | Ireland |
| `ap-southeast-1` | Singapore |

### S3-Compatible Providers

**DigitalOcean Spaces:**
- `nyc3`, `sfo3`, `sgp1`, etc.

**Wasabi:**
- `us-east-1`, `us-west-1`, `eu-central-1`

💡 **Tip**: Use a region close to your primary users for better performance

---

## Bucket Name

**Type:** Text input  
**Required:** Yes

The name of your S3 bucket or storage container.

### Requirements

- Globally unique (for AWS S3)
- Lowercase letters, numbers, hyphens only
- 3-63 characters
- No underscores, spaces, or special characters

**Examples:**
- `my-license-platform-files`
- `acme-software-downloads`
- `product-assets-2024`

---

## Public URL (Optional)

**Type:** URL input

If you're using a CDN or custom domain for your S3 files, enter it here.

**Examples:**
- `https://cdn.yourdomain.com`
- `https://files.yourproduct.com`
- `https://d111111abcdef8.cloudfront.net`

### When to Use

✅ You have CloudFront or CDN in front of S3  
✅ You want custom branded URLs  
✅ You need HTTPS for non-AWS S3  

---

## Custom Endpoint (S3-Compatible Only)

**Type:** URL input

For non-AWS S3-compatible services, enter the endpoint URL.

### Examples

**DigitalOcean Spaces:**
```
https://nyc3.digitaloceanspaces.com
```

**Wasabi:**
```
https://s3.us-east-1.wasabisys.com
```

**MinIO (Self-Hosted):**
```
https://minio.yourdomain.com
```

---

## Test Connection

### Description

Upload a test image to verify your S3 configuration is working.

### How to Use

1. Configure all S3 settings above
2. Click "Choose File" and select a test image
3. Click "Test S3 Connection"
4. System attempts to upload the file
5. Success message shows the uploaded file URL

### Troubleshooting

| Issue | Solution |
|-------|----------|
| Access Denied | Check IAM permissions include s3:PutObject |
| Bucket Not Found | Verify bucket name and region are correct |
| Connection Timeout | Check endpoint URL and firewall rules |
| Invalid Credentials | Verify access key and secret key |

### Required IAM Permissions

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "s3:PutObject",
      "s3:GetObject",
      "s3:DeleteObject",
      "s3:ListBucket"
    ],
    "Resource": [
      "arn:aws:s3:::your-bucket-name/*",
      "arn:aws:s3:::your-bucket-name"
    ]
  }]
}
```

---

# Tab 5: Changelog Settings

Control the public-facing product changelog feature.

![Changelog Settings Tab](placeholder-settings-changelog.png)
*Screenshot of Changelog Settings tab*

## Enable Changelog

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Master switch for the changelog feature across the entire platform.

**ON**: Changelog functionality is available  
**OFF**: Changelog is completely disabled

### What It Controls

When enabled:
- Admin can create changelog entries
- Changelog pages are accessible
- API endpoints return changelog data

When disabled:
- Changelog menu items are hidden
- Public pages return 404
- API endpoints return disabled status

---

## Public Access

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Controls whether the changelog is visible to non-authenticated users.

**ON**: Anyone can view the changelog (no login required)  
**OFF**: Only authenticated users can access the changelog

### Use Cases

| Setting | Best For |
|---------|----------|
| **Public ON** | Public software, SaaS products, transparency |
| **Public OFF** | Enterprise tools, internal software, sensitive releases |

---

## Items Per Page

**Type:** Numeric input  
**Default:** 20  
**Range:** 5-100

### Description

Number of changelog entries displayed per page before pagination.

### Recommendations

| Product Type | Suggested Value |
|--------------|-----------------|
| Frequent Updates | 10-15 (easier to scan) |
| Quarterly Releases | 20-30 (show more history) |
| Annual Updates | 50+ (rarely paginate) |

---

## Show Drafts

**Type:** Toggle (On/Off)  
**Default:** Off

### Description

**Admin-only setting.** Controls whether draft (unpublished) changelog entries are visible in the admin interface.

**ON**: Admins see draft entries marked with a badge  
**OFF**: Only published entries are shown

> 📝 **Note**: This setting never affects public views - drafts are never public

---

## Changelog Slug

**Type:** Text input  
**Default:** `changelog`  
**Pattern:** Lowercase letters, numbers, hyphens only

### Description

The URL path used to access the public changelog.

**Example:** If slug is `changelog`, the URL is:
```
https://yourdomain.com/changelog
```

### Custom Examples

| Slug | URL |
|------|-----|
| `changelog` | `/changelog` (default) |
| `updates` | `/updates` |
| `release-notes` | `/release-notes` |
| `whats-new` | `/whats-new` |

### Tips

💡 Keep it short and memorable  
💡 Use SEO-friendly terms  
💡 Avoid changing after public release  

---

# Tab 6: Telemetry Settings

Configure usage data collection from products in the field.

![Telemetry Settings Tab](placeholder-settings-telemetry.png)
*Screenshot of Telemetry Settings tab*

## Enable Telemetry

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Controls whether the platform accepts and stores telemetry data from products.

**ON**: Telemetry endpoints accept data  
**OFF**: All telemetry is rejected

### What is Telemetry?

Telemetry is usage data sent from your products, including:
- Product version information
- Feature usage statistics
- Error reports
- Performance metrics
- Custom analytics

### When to Enable

✅ You want usage insights  
✅ You need piracy detection  
✅ You want to track feature adoption  
✅ You need to identify issues in the field  

### When to Disable

❌ Privacy-sensitive applications  
❌ Completely offline products  
❌ During testing phases  

---

## Storage Duration

**Type:** Dropdown  
**Options:** 1, 3, 6, 9, 12 months

### Description

How long telemetry data is retained before automatic purging.

| Duration | Best For |
|----------|----------|
| 1 month | Limited storage, recent data only |
| 3 months | Typical SaaS, quarterly analysis |
| 6 months | Standard recommendation |
| 12 months | Annual comparisons, trends |

### Data Retention Notes

- Telemetry is purged automatically
- No way to recover purged data
- Purging happens nightly
- Export data before purge if needed

💡 **Tip**: Balance storage costs with analytical needs

---

# Tab 7: Webhook Settings

Configure webhook delivery log retention.

![Webhook Settings Tab](placeholder-settings-webhook.png)
*Screenshot of Webhook Settings tab*

## Webhook Retention Days

**Type:** Dropdown  
**Options:** 7, 15, 30 days  
**Default:** 30 days

### Description

How long webhook delivery logs are stored before automatic deletion.

### What Are Webhook Logs?

For each webhook delivery attempt, the system logs:
- Request timestamp
- Target URL
- HTTP status code
- Request body
- Response body
- Retry attempts
- Error messages

### Choosing Retention

| Days | Best For |
|------|----------|
| **7** | Low traffic, storage-constrained |
| **15** | Moderate traffic, adequate for debugging |
| **30** | High traffic, compliance requirements |

### When Logs Are Useful

- Debugging integration issues
- Verifying webhook delivery
- Troubleshooting partner systems
- Compliance auditing

💡 **Tip**: Longer retention helps with historical troubleshooting but uses more storage

---

# Tab 8: Logging Settings

Control what system activities are logged.

![Logging Settings Tab](placeholder-settings-logging.png)
*Screenshot of Logging Settings tab*

## Log Dashboard Activities

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Records all actions performed by admins in the dashboard.

**Logged Events:**
- User logins/logouts
- Record creation, updates, deletions
- Settings changes
- Report generation
- Export operations

### When to Enable

✅ Compliance requirements  
✅ Security auditing  
✅ User accountability  
✅ Troubleshooting admin actions  

### When to Disable

❌ Privacy concerns  
❌ Development environments  
❌ Storage constraints  

---

## Log API Calls

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Records all API requests, including successful operations.

**Logged Data:**
- API endpoint called
- Request parameters
- Response status
- API key used
- Timestamp
- IP address

### Storage Impact

⚠️ High-traffic systems generate large log volumes

**Estimated Log Size:**

| API Calls/Day | Log Size/Month |
|---------------|----------------|
| 1,000 | ~30 MB |
| 10,000 | ~300 MB |
| 100,000 | ~3 GB |
| 1,000,000 | ~30 GB |

---

## Log Failed API Calls

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Records API requests that result in errors (4xx, 5xx responses).

### Why Log Failures?

- Identify integration problems
- Detect authentication issues
- Monitor abuse attempts
- Debug customer problems

💡 **Tip**: Always keep this ON - failures indicate problems

---

## Log Blocklisted API Calls

**Type:** Toggle (On/Off)  
**Default:** On

### Description

Records API requests from blocklisted IP addresses or API keys.

### Use Cases

- Monitor potential attackers
- Track repeat offenders
- Evidence for abuse reports
- Security incident investigation

---

# Tab 9: KeyManager License Settings

Configure the platform's own license key (if using commercial version).

![KeyManager License Settings Tab](placeholder-settings-keymanager.png)
*Screenshot of KeyManager License Settings tab*

## Platform License Key

**Type:** Text input (license key format)

### Description

If you're using the **commercial version** of GetKeyManager, enter your platform license key here.

### Open Source vs Commercial

| Version | Requires License | Features |
|---------|------------------|----------|
| **Open Source** | No | Core functionality |
| **Commercial** | Yes | Premium features, support, updates |

### Where to Get Your License

1. Purchase from getKeyManager.com
2. Receive license key via email
3. Enter it here
4. Platform validates and unlocks features

### Troubleshooting

| Issue | Solution |
|-------|----------|
| Invalid key | Check for typos, copy-paste carefully |
| Expired key | Renew subscription |
| Wrong edition | Verify key matches your edition |

---

# Tab 10: Envato Integration Settings

Connect to Envato Marketplace for automatic license synchronization.

![Envato Integration Settings Tab](placeholder-settings-envato.png)
*Screenshot of Envato Integration Settings tab*

## Envato Personal Token

**Type:** Text input (API token)

### Description

API token from Envato that allows the platform to verify purchase codes and sync license data.

### How to Get Your Token

1. Log in to Envato Market
2. Go to Settings > API Keys
3. Create a new Personal Token
4. Grant "View sales and earnings" permission
5. Copy token and paste here

### What It Enables

✅ Automatic purchase code verification  
✅ License auto-creation from Envato sales  
✅ Product synchronization  
✅ Customer data import  

---

## Auto-Create Products from Envato Purchases

**Type:** Toggle (On/Off)  
**Default:** Off

### Description

Automatically creates product records when Envato purchase codes are verified.

**ON**: New products are created automatically  
**OFF**: Products must be created manually first

### When to Enable

✅ You sell exclusively on Envato  
✅ You want minimal manual work  
✅ Your products match 1:1 with Envato items  

### When to Disable

❌ You have complex product structures  
❌ You need manual product configuration  
❌ You sell on multiple platforms  

---

# Tab 11: Abuse Detection & Auto-Suspension

Protect licenses from misuse with intelligent monitoring and automatic enforcement.

![Abuse Detection Settings Tab](placeholder-settings-abuse.png)
*Screenshot of Abuse Detection Settings tab*

## Overview

Abuse detection monitors license activations and flags **suspicious activation patterns** (for example, excessive activations across devices or locations in a short time). When configured correctly, it helps you:

* Prevent license sharing and key leakage
* Automatically respond to abnormal usage
* Reduce manual monitoring and support overhead

These controls work together:

1. **Enable Abuse Detection** – Turns monitoring on or off
2. **Abuse Threshold** – Defines when usage becomes suspicious
3. **Auto-Suspend on Abuse** – Enforces automatic action

---

## Enable Abuse Detection

**Type:** Toggle (On / Off)  
**Default:** On

### Description

Enables or disables abuse monitoring for licenses.

* **ON**: The system actively evaluates activation behavior against defined rules
* **OFF**: No abuse evaluation is performed. All activations are allowed unless blocked by other limits

### When to Enable

Enable this option if:

✅ Your product is distributed publicly or via marketplaces  
✅ License keys can be reused or copied  
✅ You want early detection of misuse  
✅ You operate at scale and need automation  

### When to Disable

You may temporarily disable abuse detection:

🔧 During internal testing or QA  
🔧 For trusted enterprise customers  
🔧 While troubleshooting false positives  

> ⚠️ **Warning**: Disabling abuse detection also disables threshold evaluation and auto-suspension.

---

## Abuse Threshold (Number of Suspicious Activations)

**Type:** Numeric input  
**Default:** 5  
**Range:** 1-100

### Description

Defines the **maximum number of suspicious activations** allowed before a license is considered abusive.

A *suspicious activation* may include patterns such as:

* Rapid activations within a short time window (e.g., 10 devices in 1 hour)
* Activations from multiple IPs, regions, or countries
* Repeated re-activations beyond normal usage
* Activations from known VPN or proxy servers
* Unusual device fingerprint patterns

### How It Works

1. Each suspicious activation increments an internal counter
2. When the counter **reaches or exceeds** the abuse threshold:
   * The license is marked as *abused*
   * Enforcement actions may occur (depending on Auto-Suspend setting)
   * Event is logged for review

### Example Scenarios

| Threshold | Behavior | Use Case |
| --------- | -------- | -------- |
| **1** | Very strict; first suspicious activity triggers | High-security APIs, enterprise software |
| **3** | Moderately strict; 2-3 violations before action | SaaS products, cloud services |
| **5** | Balanced; suitable for most desktop software | **Recommended default** |
| **10** | Lenient; tolerates some legitimate edge cases | Consumer software, trial licenses |

### Real-World Example

**Scenario**: Desktop software with threshold = 3

1. User activates on work PC (activation 1) ✅
2. User activates on laptop (activation 2) ✅
3. User travels and activates on hotel Wi-Fi (activation 3, different IP) ⚠️ Suspicious +1
4. User's friend tries to activate with same key (activation 4, different device) ⚠️ Suspicious +2
5. Another friend activates (activation 5) ⚠️ Suspicious +3 → **Threshold reached!**

### Best Practices

**Starting Out:**
1. Start with a **moderate value (3–5)**
2. Monitor abuse logs for 30 days
3. Adjust based on false positive rate
4. Tighten for high-piracy products
5. Relax for legitimate multi-device use cases

**Monitoring:**
- Review flagged licenses weekly
- Check if suspended licenses are legitimate users
- Adjust threshold if seeing too many false positives

💡 **Tip**: It's better to start lenient and tighten than to frustrate legitimate customers

---

## Auto-Suspend on Abuse

**Type:** Toggle (On / Off)  
**Default:** Off

### Description

Automatically suspends a license when the abuse threshold is reached.

* **ON**: The license is immediately suspended
* **OFF**: The license is only flagged; no automatic action is taken

### What Happens on Auto-Suspension

When enabled and abuse is detected:

1. ⛔ License status changes to **Suspended**
2. 🚫 All further activations and validations fail
3. 📱 SDKs and APIs return a suspension response
4. 📧 Optional notification email to admin (if configured)
5. 📝 Event is logged for audit and review
6. 🔔 Alert appears in admin dashboard

### When to Enable

Enable auto-suspension if:

✅ You want zero-tolerance enforcement  
✅ Your product is frequently pirated  
✅ You operate at scale and need automation  
✅ You have a clear abuse policy communicated to users  
✅ You can quickly respond to support requests about suspensions  

### When to Keep Disabled

Keep disabled if:

❌ You prefer manual review before action  
❌ You sell to enterprise or offline environments  
❌ You want to notify customers before enforcement  
❌ Your support team needs to investigate first  
❌ You have low abuse rates  

### Manual vs Automatic Enforcement

| Approach | Pros | Cons |
|----------|------|------|
| **Manual (Auto-Suspend OFF)** | Flexible, fewer false positives, better customer experience | Requires monitoring, delayed response, manual work |
| **Automatic (Auto-Suspend ON)** | Immediate protection, scales well, zero admin effort | May frustrate legitimate users, requires good thresholds |

### Recovery Process

If a legitimate user is auto-suspended:

1. User contacts support
2. Admin reviews abuse log
3. Admin determines it was false positive
4. Admin unsuspends license manually
5. Admin may adjust abuse threshold
6. User can activate again

💡 **Tip**: Have a clear support process for handling suspension appeals

---

## Recommended Configurations

### SaaS / API Products

**High-value targets for abuse**

* **Enable Abuse Detection:** ON
* **Abuse Threshold:** 1–2
* **Auto-Suspend on Abuse:** ON

**Reasoning:** API keys are easily shared. Immediate suspension prevents ongoing abuse.

---

### Desktop / On-Premises Software

**Moderate abuse risk, legitimate multi-device use**

* **Enable Abuse Detection:** ON
* **Abuse Threshold:** 3–5
* **Auto-Suspend on Abuse:** OFF or ON (with review process)

**Reasoning:** Users may legitimately use multiple devices. Manual review prevents false positives.

---

### Internal / Trial Licenses

**Low abuse risk, testing environment**

* **Enable Abuse Detection:** OFF or ON with high threshold
* **Abuse Threshold:** 10+
* **Auto-Suspend on Abuse:** OFF

**Reasoning:** Internal teams need flexibility. Trials should be lenient to encourage evaluation.

---

### Enterprise / B2B Software

**Trusted customers, contracted usage**

* **Enable Abuse Detection:** ON (for monitoring)
* **Abuse Threshold:** High (10-20)
* **Auto-Suspend on Abuse:** OFF

**Reasoning:** Enterprise customers have contracts. Use abuse detection for insights, not enforcement.

---

## Important Notes

⚠️ **Abuse detection does not replace activation limits** – they complement each other

🔄 **Suspension can usually be reversed** by an admin

📊 **Always review abuse logs** before permanently revoking a license

🤝 **Communicate your policy** to customers clearly

📧 **Set up notifications** so admins know when abuse is detected

---

## Summary Table

| Setting | Purpose | Typical Value |
| ---------------------- | ----------------------------- | ------------- |
| Enable Abuse Detection | Turns monitoring on/off | ON |
| Abuse Threshold | Defines tolerance level | 3-5 |
| Auto-Suspend on Abuse | Enforces automatic protection | OFF (manual review) or ON (zero-tolerance) |

---

## Testing Your Configuration

### Step 1: Set Threshold to 2 (for testing)

Temporarily lower the threshold so you can trigger abuse with fewer activations.

### Step 2: Create a Test License

Generate a test license key for experimentation.

### Step 3: Activate Multiple Times

Activate from different devices, IPs, or using different identifiers in rapid succession.

### Step 4: Monitor the Logs

Watch the abuse detection logs to see when suspicions are flagged.

### Step 5: Verify Suspension (if Auto-Suspend ON)

Confirm the license is suspended after threshold is reached.

### Step 6: Reset and Adjust

Unsuspend the test license, adjust thresholds based on findings, and set production values.

---

## Frequently Asked Questions

**Q: What if a legitimate user triggers abuse detection?**  
A: They should contact support. An admin can review the case, unsuspend the license, and adjust settings if needed.

**Q: Can I whitelist specific customers from abuse detection?**  
A: Not currently, but you can set a very high threshold for specific products used by trusted customers.

**Q: How long does the abuse counter persist?**  
A: The counter resets after a configurable time period (typically 24-72 hours of normal behavior).

**Q: What data is used to detect suspicious activations?**  
A: Device fingerprints, IP addresses, geographic locations, activation frequency, and activation patterns.

**Q: Can users see they've been flagged for abuse?**  
A: If auto-suspended, they'll receive an error message. Otherwise, flagging is admin-only visibility.

---

**Proper configuration ensures strong protection without disrupting legitimate users.**
