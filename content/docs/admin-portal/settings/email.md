---
title: Email Settings
weight: 30
---

![Email Settings Tab](placeholder-settings-email.png)
*Screenshot of Email Settings tab*

---

## Overview

Email Settings configure how your KeyManager platform **sends transactional and notification emails** to customers and administrators. Proper email configuration is critical for:

* Customer communication (license activation, expiration warnings)
* Account management (password resets, welcome emails)
* Security notifications (suspicious activity alerts)
* Administrative alerts (abuse detection, system events)
* Payment and billing confirmations
* Support ticket responses

These settings control:

1. **Email Driver** – Choose your email delivery method
2. **SMTP Configuration** – Server connection details
3. **Authentication** – Credentials and security
4. **Test Email** – Verify configuration before going live

---

## Email Driver

**Type:** Dropdown select  
**Options:** SMTP, Sendmail, Mailgun, Amazon SES  
**Default:** SMTP

![Email Driver Selection](placeholder-email-driver.png)
*Screenshot showing email driver options*

### Description

The email driver determines **how your platform sends emails**. Each driver has different configuration requirements, performance characteristics, and infrastructure needs.

### Available Drivers

#### SMTP (Simple Mail Transfer Protocol)

**Most Common Choice**

* Uses standard SMTP protocol
* Works with any email provider (Gmail, Outlook, SendGrid, etc.)
* Requires SMTP server credentials
* Suitable for all deployment sizes
* Most compatible and well-supported

**Best For:**
* ✅ General purpose email sending
* ✅ Using existing email providers (Gmail, Office 365)
* ✅ Small to medium deployments
* ✅ When you need maximum compatibility

#### Sendmail

**Server-Based Email**

* Uses local server's sendmail binary
* No external SMTP server needed
* Requires properly configured mail server on host
* Common in traditional Linux server environments
* May have deliverability challenges

**Best For:**
* ✅ Self-hosted servers with configured mail
* ✅ Internal networks with mail relays
* ✅ Legacy system compatibility

**Not Recommended For:**
* ❌ Cloud deployments (AWS, Azure, GCP)
* ❌ Docker/containerized environments
* ❌ When deliverability is critical

#### Mailgun

**Transactional Email API**

* Direct integration with Mailgun service
* API-based, not SMTP
* Excellent deliverability
* Built-in analytics and tracking
* Requires Mailgun account and API key

**Best For:**
* ✅ High-volume senders (>10,000 emails/month)
* ✅ When email analytics are important
* ✅ Applications requiring high deliverability
* ✅ SaaS products with automated emails

**Requirements:**
* Mailgun account (free tier available)
* Domain verification
* API credentials

#### Amazon SES (Simple Email Service)

**AWS-Native Email**

* Fully integrated with AWS ecosystem
* Extremely cost-effective at scale
* High deliverability with AWS reputation
* Requires AWS account and credentials
* Ideal for AWS-hosted applications

**Best For:**
* ✅ Applications hosted on AWS
* ✅ Large-scale email sending
* ✅ When cost optimization is critical
* ✅ Already using AWS services

**Requirements:**
* AWS account
* SES verified domain or email
* IAM credentials with SES permissions
* Move out of SES sandbox (for production)

### Driver Comparison

| Driver | Setup Complexity | Deliverability | Cost | Best For |
| ------ | ---------------- | -------------- | ---- | -------- |
| **SMTP** | Low | Good (depends on provider) | Varies | General purpose |
| **Sendmail** | Medium-High | Low-Medium | Free | Self-hosted servers |
| **Mailgun** | Low | Excellent | Pay-per-email | High-volume SaaS |
| **Amazon SES** | Medium | Excellent | Very low | AWS deployments |

### When to Use Each Driver

**Choose SMTP if:**
* You're using Gmail, Office 365, or other standard providers
* You want simple, universal compatibility
* You're just getting started
* You have existing SMTP credentials

**Choose Sendmail if:**
* You have a properly configured mail server
* You're on a traditional Linux host
* You need no external dependencies
* Deliverability is not critical

**Choose Mailgun if:**
* You need guaranteed deliverability
* You want email analytics and tracking
* You send high volumes
* You need webhook notifications for opens/clicks

**Choose Amazon SES if:**
* Your application runs on AWS
* You need low-cost, high-volume sending
* You're already using AWS services
* You need tight AWS integration

💡 **Tip**: For production deployments, SMTP with a reputable provider (SendGrid, Mailgun, Postmark) or Amazon SES are recommended for best deliverability.

---

## SMTP Host

**Type:** Text input  
**Default:** localhost  
**Required:** When using SMTP driver

![SMTP Host Configuration](placeholder-smtp-host.png)
*Screenshot showing SMTP host field*

### Description

The SMTP host is the **server address** that will send your emails. This is provided by your email service provider.

### Common SMTP Hosts

**Gmail (Google Workspace):**
```
smtp.gmail.com
```

**Office 365 / Outlook.com:**
```
smtp.office365.com
```

**SendGrid:**
```
smtp.sendgrid.net
```

**Mailgun (SMTP mode):**
```
smtp.mailgun.org
```

**Amazon SES (SMTP mode):**
```
email-smtp.us-east-1.amazonaws.com
(Region-specific - replace us-east-1 with your region)
```

**Postmark:**
```
smtp.postmarkapp.com
```

**Sparkpost:**
```
smtp.sparkpostmail.com
```

**Custom/Self-Hosted:**
```
mail.yourdomain.com
```

### Best Practices

1. **Use provider's official SMTP hostname** – Never use IP addresses
2. **Verify hostname spelling** – Typos cause connection failures
3. **Check regional endpoints** – Some providers have region-specific hosts
4. **Use SSL/TLS-enabled hosts** – Security is mandatory
5. **Test with telnet** – Verify connectivity before configuring

### Troubleshooting

**Error: "Could not connect to SMTP host"**
* ✅ Verify hostname is correct
* ✅ Check firewall rules allow outbound SMTP
* ✅ Ensure port is correct (see SMTP Port section)
* ✅ Verify server has internet connectivity

**Error: "Connection refused"**
* ✅ Check if port is blocked by firewall
* ✅ Verify SMTP service is running
* ✅ Try telnet to test: `telnet smtp.example.com 587`

---

## SMTP Port

**Type:** Numeric input  
**Default:** 587  
**Common Values:** 25, 465, 587, 2525

![SMTP Port Configuration](placeholder-smtp-port.png)
*Screenshot showing SMTP port field*

### Description

The SMTP port determines **which network port** is used to connect to the email server. Different ports have different security and compatibility characteristics.

### Port Reference Guide

#### Port 587 (RECOMMENDED)

**STARTTLS - Submission Port**

* ✅ **Industry standard** for email submission
* ✅ Uses STARTTLS encryption
* ✅ Required by most modern providers
* ✅ Best security and compatibility
* ✅ Widely supported

**Use this port for:**
* Gmail
* Office 365
* SendGrid
* Mailgun
* Postmark
* Most professional email services

#### Port 465

**SSL/TLS - Legacy Secure**

* Implicit SSL/TLS from connection start
* Deprecated but still widely supported
* Some providers require this port
* More secure than port 25

**Use this port for:**
* Older email systems
* When provider specifically requires it
* Legacy applications

#### Port 25

**Unencrypted - Legacy**

* ⚠️ **NOT RECOMMENDED** for modern applications
* No encryption by default
* Often blocked by ISPs and cloud providers
* Vulnerable to interception
* Used for server-to-server relay

**Avoid unless:**
* Internal network only
* No sensitive data
* Required by legacy systems

#### Port 2525

**Alternative Submission Port**

* Used when port 587 is blocked
* Same security as port 587
* Offered by some providers as backup
* Common in cloud environments

**Use this port when:**
* Port 587 is blocked by firewall
* Provider offers it as alternative (e.g., SendGrid)

### Port Recommendations by Provider

| Provider | Primary Port | Alternative Port | Encryption |
| -------- | ------------ | ---------------- | ---------- |
| **Gmail** | 587 | 465 | TLS/SSL |
| **Office 365** | 587 | - | TLS |
| **SendGrid** | 587 | 2525, 25 | TLS |
| **Mailgun** | 587 | 465, 2525 | TLS/SSL |
| **Amazon SES** | 587 | 465, 25 | TLS/SSL |
| **Postmark** | 587 | 2525, 25 | TLS |

### Security Considerations

**Port Security Ranking:**
1. **Port 587 (TLS)** – Most secure and recommended
2. **Port 465 (SSL)** – Secure, legacy support
3. **Port 2525 (TLS)** – Secure, firewall-friendly
4. **Port 25** – Insecure, avoid if possible

⚠️ **Warning**: Never use port 25 for sending customer emails. Many cloud providers block it to prevent spam.

### Best Practices

1. **Always use 587 unless provider specifies otherwise**
2. **Enable encryption** (TLS/SSL) regardless of port
3. **Test port connectivity** before deployment
4. **Document your configuration** for team reference
5. **Use fallback port** if primary is blocked

### Testing Port Connectivity

**Linux/Mac:**
```bash
telnet smtp.gmail.com 587
# Should connect successfully
```

**Windows PowerShell:**
```powershell
Test-NetConnection -ComputerName smtp.gmail.com -Port 587
# Should show TcpTestSucceeded: True
```

---

## SMTP Username

**Type:** Text input  
**Default:** Empty  
**Required:** When SMTP authentication is required (most providers)

![SMTP Username Field](placeholder-smtp-username.png)
*Screenshot showing SMTP username configuration*

### Description

The SMTP username is your **authentication credential** for the email server. This proves you have permission to send emails through the provider.

### Username Format by Provider

**Gmail:**
```
your-email@gmail.com
(Full email address)
```

**Google Workspace:**
```
your-email@yourdomain.com
(Full email address)
```

**Office 365:**
```
your-email@yourdomain.com
(Full email address)
```

**SendGrid:**
```
apikey
(Literally the word "apikey" - not your actual key)
```

**Mailgun:**
```
postmaster@your-domain.com
(Provided by Mailgun in your domain settings)
```

**Amazon SES:**
```
AKIAIOSFODNN7EXAMPLE
(IAM SMTP credentials, NOT your AWS access key)
```

**Postmark:**
```
Your-Server-Token
(Found in your Postmark server settings)
```

### Provider-Specific Notes

#### Gmail / Google Workspace

**Important:**
* Use full email address as username
* **Must enable "Less Secure Apps"** OR use App Password
* **Recommended:** Create App-Specific Password for better security
* 2FA users MUST use App Password

**Creating Gmail App Password:**
1. Go to Google Account settings
2. Security → 2-Step Verification
3. App Passwords
4. Generate password for "Mail"
5. Use generated password (not your account password)

#### Office 365

* Use full email address
* Modern authentication supported
* May require app-specific password for 2FA accounts
* Legacy authentication being phased out

#### SendGrid

* Username is always `apikey`
* Password is your actual API key
* API key format: `SG.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

#### Amazon SES

* **CRITICAL**: Use SMTP credentials, not IAM access keys
* Generate SMTP credentials in SES console
* Format: `AKIAIOSFODNN7EXAMPLE`
* Region-specific credentials

#### Mailgun

* Username format: `postmaster@mg.yourdomain.com`
* Found in Mailgun dashboard under domain settings
* Not the same as your Mailgun account email

### Security Best Practices

1. **Never hardcode credentials** in source code
2. **Use environment variables** for configuration
3. **Rotate credentials** periodically (every 90 days)
4. **Use app-specific passwords** when available
5. **Limit permissions** to send-only (no read access)
6. **Monitor usage** for unauthorized activity

💡 **Tip**: Create a dedicated email account for application sending rather than using personal credentials

---

## SMTP Password

**Type:** Password input (hidden)  
**Default:** Empty  
**Required:** When SMTP authentication is required  
**Security:** Encrypted at rest

![SMTP Password Field](placeholder-smtp-password.png)
*Screenshot showing SMTP password configuration*

### Description

The SMTP password authenticates your connection to the email server. This is **highly sensitive** and must be protected.

### Password Types by Provider

**Gmail:**
* Use App-Specific Password (recommended)
* Or account password if 2FA disabled (not recommended)

**Office 365:**
* Use account password
* Or app-specific password for 2FA

**SendGrid:**
* API Key (starts with `SG.`)
* Generate in SendGrid dashboard

**Mailgun:**
* API Key or SMTP password
* Found in Mailgun domain settings

**Amazon SES:**
* SMTP password (generated with SMTP credentials)
* Different from AWS Secret Access Key

**Postmark:**
* Server API Token
* Found in Postmark server settings

### Security Considerations

⚠️ **CRITICAL SECURITY WARNINGS:**

1. **Never share SMTP passwords** via email or chat
2. **Never commit passwords** to version control (Git)
3. **Use environment variables** for deployment
4. **Rotate credentials** if compromised
5. **Limit password scope** to sending only
6. **Monitor for unauthorized use** via provider dashboards

### Password Storage

**Development:**
```bash
# .env file (never commit!)
SMTP_PASSWORD=your-secret-password
```

**Production:**
* Use environment variables
* Use secrets management (AWS Secrets Manager, HashiCorp Vault)
* Use platform-specific secret stores (Heroku Config Vars, etc.)

### What to Do If Password is Compromised

1. **Immediately rotate credentials** in provider dashboard
2. **Update password** in KeyManager settings
3. **Review sent emails** for unauthorized activity
4. **Check provider logs** for suspicious access
5. **Enable 2FA** if not already active
6. **Notify team** of security incident

### Testing Password

After entering password, use the **Test Email** feature to verify:
* Password is correct
* Authentication succeeds
* Email sends successfully

---

## Email Encryption

**Type:** Dropdown select  
**Options:** None, TLS, SSL  
**Default:** TLS  
**Recommended:** TLS

![Email Encryption Setting](placeholder-email-encryption.png)
*Screenshot showing encryption options*

### Description

Email encryption determines **how data is secured** during transmission to the SMTP server.

### Encryption Options

#### TLS (Transport Layer Security)

**RECOMMENDED - Modern Standard**

* ✅ Industry standard for email security
* ✅ Encrypts connection after initial handshake (STARTTLS)
* ✅ Compatible with port 587
* ✅ Required by most modern providers
* ✅ Better performance than SSL

**How it works:**
1. Connect to server unencrypted
2. Send STARTTLS command
3. Upgrade connection to encrypted
4. Authenticate and send email

**Use with:**
* Port 587 (most common)
* Port 2525 (alternative)

#### SSL (Secure Sockets Layer)

**Legacy Secure Option**

* Implicit encryption from connection start
* Used with port 465
* Older protocol (technically TLS 1.0)
* Still widely supported
* Less flexible than TLS

**Use when:**
* Provider requires port 465
* Legacy system compatibility
* TLS connection fails

#### None

**NO ENCRYPTION - NOT RECOMMENDED**

* ⚠️ Credentials sent in plain text
* ⚠️ Email content visible to eavesdroppers
* ⚠️ Vulnerable to man-in-the-middle attacks
* ⚠️ Violates security best practices

**Only use for:**
* Internal networks (behind firewall)
* Testing environments
* When explicitly required by provider

### Encryption Recommendations

| Scenario | Recommended Encryption | Port |
| -------- | --------------------- | ---- |
| **Production (All)** | TLS | 587 |
| **Gmail** | TLS | 587 |
| **Office 365** | TLS | 587 |
| **SendGrid** | TLS | 587 |
| **Mailgun** | TLS | 587 |
| **Legacy Systems** | SSL | 465 |
| **Internal Only** | TLS | 587 |

⚠️ **Never use "None" in production** – Customer data and credentials will be exposed

---

## Sender Name (From Name)

**Type:** Text input  
**Default:** Application Name  
**Maximum Length:** 64 characters

![Sender Name Configuration](placeholder-sender-name.png)
*Screenshot showing sender name field*

### Description

The sender name appears as the **"From" name** in recipient email clients. This is the friendly name customers see, separate from the email address.

**Example:**
```
From: Acme License Portal <noreply@acme.com>
       ^^^^^^^^^^^^^^^^^^^^
       Sender Name
```

### Best Practices

**Professional Naming:**
* Use your company or product name
* Be consistent across all emails
* Avoid generic names like "Noreply" or "System"
* Match your brand voice

**Examples:**

| Business Type | Sender Name | Reasoning |
| ------------- | ----------- | --------- |
| SaaS Company | "CloudSync Pro Support" | Clear, professional |
| Enterprise | "Acme License Team" | Human-friendly |
| Marketplace | "MarketName Licensing" | Brand recognition |
| Agency | "Agency Name - Client Portal" | Clear ownership |

### Impact on Email Delivery

**Good Sender Names:**
* ✅ Professional and recognizable
* ✅ Match email domain
* ✅ Build trust and engagement

**Bad Sender Names:**
* ❌ All caps: "URGENT NOTIFICATION"
* ❌ Generic: "noreply"
* ❌ Spammy: "Click Here!"
* ❌ Misleading: "Your Friend"

### Regional Considerations

**Localization:**
* For international audiences, consider localized sender names
* Use language-appropriate characters
* Test display in various email clients

💡 **Tip**: Match your sender name to your application name for consistency

---

## Sender Email (From Address)

**Type:** Email input  
**Default:** noreply@yourdomain.com  
**Validation:** Must be valid email format

![Sender Email Configuration](placeholder-sender-email.png)
*Screenshot showing sender email field*

### Description

The sender email is the **"From" email address** that appears in sent emails. This must be an address you control and have permission to send from.

### Best Practices

**Address Selection:**

**Recommended Formats:**
* `noreply@yourdomain.com` – Automated emails
* `support@yourdomain.com` – Customer can reply
* `licensing@yourdomain.com` – Specific purpose
* `notifications@yourdomain.com` – System alerts

**Avoid:**
* ❌ Personal addresses (@gmail.com, @yahoo.com)
* ❌ Addresses you don't control
* ❌ Generic providers (looks unprofessional)
* ❌ Addresses without SPF/DKIM records

### Domain Authentication

**Critical for Deliverability:**

**SPF (Sender Policy Framework):**
* DNS record authorizing servers to send on your behalf
* Required by most email providers
* Prevents spoofing

**DKIM (DomainKeys Identified Mail):**
* Cryptographic signature proving email authenticity
* Increases trust and deliverability
* Set up in your email provider dashboard

**DMARC (Domain-based Message Authentication):**
* Policy for handling failed authentication
* Builds on SPF and DKIM
* Essential for enterprise senders

### Provider-Specific Requirements

**Gmail/Google Workspace:**
* Must use @gmail.com or verified domain
* Must match SMTP username

**Amazon SES:**
* Must verify email or domain in SES console
* Requires clicking verification link
* Different process for production access

**SendGrid:**
* Domain verification required
* Single sender verification for testing
* Full domain authentication for production

**Mailgun:**
* Domain must be verified and DNS configured
* SPF and DKIM records required
* Takes 24-48 hours to fully propagate

### Noreply vs Reply-Enabled

| Approach | Pros | Cons |
| -------- | ---- | ---- |
| **noreply@** | Prevents inbox overload, clear expectations | Impersonal, blocks legitimate replies |
| **support@** | Allows customer replies, better engagement | Requires monitoring, more work |

**Recommendation:** Use reply-enabled address (support@) for better customer experience

---

## Test Email Functionality

**Type:** Button action with email input  
**Purpose:** Validate configuration before production use

![Test Email Interface](placeholder-test-email.png)
*Screenshot showing test email functionality*

### Description

The test email feature sends a **sample email** to verify your SMTP configuration is working correctly before going live.

### How to Use

1. Configure all SMTP settings (host, port, username, password, encryption)
2. Enter a recipient email address
3. Click **Send Test Email**
4. Check recipient inbox (and spam folder)
5. Verify email arrived successfully

### What the Test Email Contains

**Subject:** `Test Email from [Application Name]`

**Body:**
```
This is a test email from your KeyManager platform.

If you received this email, your email configuration is working correctly.

Configuration Details:
- SMTP Host: smtp.example.com
- Port: 587
- Encryption: TLS
- Sent at: 2024-01-15 14:30:00 UTC

Do not reply to this email.
```

### Interpreting Test Results

**✅ Success Indicators:**
* Email appears in inbox within 1-2 minutes
* Sender name displays correctly
* From address is correct
* No warnings or spam flags

**❌ Failure Indicators:**
* Email does not arrive
* Email goes to spam
* Sender appears as "via smtp.example.com"
* Authentication warnings displayed

### Common Test Failures and Solutions

#### "Connection Refused"

**Possible Causes:**
* Incorrect SMTP host
* Wrong port number
* Firewall blocking outbound SMTP

**Solutions:**
* ✅ Verify hostname spelling
* ✅ Try port 587 (TLS) or 465 (SSL)
* ✅ Check firewall rules
* ✅ Test connectivity: `telnet smtp.host.com 587`

#### "Authentication Failed"

**Possible Causes:**
* Incorrect username or password
* Account requires app-specific password
* 2FA enabled without app password

**Solutions:**
* ✅ Double-check credentials
* ✅ Generate app-specific password
* ✅ Verify account is active

#### "Email Goes to Spam"

**Possible Causes:**
* Missing SPF/DKIM records
* Unverified domain
* Poor sender reputation

**Solutions:**
* ✅ Set up SPF and DKIM
* ✅ Verify domain with provider
* ✅ Warm up sender reputation gradually
* ✅ Use reputable email provider

#### "Email Not Delivered"

**Possible Causes:**
* Recipient address invalid
* Aggressive spam filters
* Sender domain blocklisted

**Solutions:**
* ✅ Check recipient email is valid
* ✅ Try different recipient (Gmail, Outlook)
* ✅ Check sender reputation
* ✅ Review provider logs

### Best Practices for Testing

1. **Test before production deployment**
2. **Test to multiple providers** (Gmail, Outlook, Yahoo)
3. **Check spam folders** in addition to inbox
4. **Review email headers** for authentication results
5. **Test after any configuration change**
6. **Document successful configuration** for reference

💡 **Tip**: Send test emails to yourself and a colleague to verify from multiple perspectives

---

## Recommended Configurations

### Gmail (Google Workspace)

**Popular choice for small businesses**

* **Driver:** SMTP
* **Host:** smtp.gmail.com
* **Port:** 587
* **Encryption:** TLS
* **Username:** your-email@gmail.com
* **Password:** App-Specific Password
* **Sender Email:** Same as username

**Setup Steps:**
1. Enable 2FA in Google Account
2. Generate App Password
3. Use app password in SMTP Password field

---

### Office 365

**Enterprise email solution**

* **Driver:** SMTP
* **Host:** smtp.office365.com
* **Port:** 587
* **Encryption:** TLS
* **Username:** your-email@yourdomain.com
* **Password:** Account password or app password
* **Sender Email:** Same as username

---

### SendGrid

**High-volume transactional email**

* **Driver:** SMTP or Mailgun (API)
* **Host:** smtp.sendgrid.net
* **Port:** 587
* **Encryption:** TLS
* **Username:** apikey (literally)
* **Password:** Your SendGrid API key
* **Sender Email:** verified@yourdomain.com

**Setup Steps:**
1. Create SendGrid account
2. Verify domain or single sender
3. Generate API key
4. Use "apikey" as username

---

### Amazon SES

**Cost-effective AWS solution**

* **Driver:** Amazon SES or SMTP
* **Host:** email-smtp.us-east-1.amazonaws.com
* **Port:** 587
* **Encryption:** TLS
* **Username:** SMTP username (from SES)
* **Password:** SMTP password (from SES)
* **Sender Email:** verified@yourdomain.com

**Setup Steps:**
1. Verify domain in SES console
2. Generate SMTP credentials (not IAM)
3. Request production access (exit sandbox)
4. Configure SPF and DKIM

---

### Mailgun

**Developer-friendly email API**

* **Driver:** Mailgun (preferred) or SMTP
* **Host:** smtp.mailgun.org
* **Port:** 587
* **Encryption:** TLS
* **Username:** postmaster@mg.yourdomain.com
* **Password:** Your Mailgun password
* **Sender Email:** verified@yourdomain.com

---

## Important Notes

⚠️ **Always use encryption (TLS/SSL)** – Never send credentials unencrypted

🔒 **Rotate passwords every 90 days** – Security best practice

📧 **Verify domain for better deliverability** – SPF and DKIM are essential

✉️ **Test thoroughly before production** – Avoid surprises with customer emails

🚫 **Never use personal email accounts** – Use dedicated service accounts

---

## Summary Table

| Setting | Purpose | Typical Value |
| ------- | ------- | ------------- |
| Email Driver | Delivery method | SMTP |
| SMTP Host | Mail server address | smtp.provider.com |
| SMTP Port | Connection port | 587 (TLS) |
| SMTP Username | Authentication user | your-email@domain.com |
| SMTP Password | Authentication password | (API key or app password) |
| Encryption | Security protocol | TLS |
| Sender Name | From name | Your Company Name |
| Sender Email | From address | noreply@yourdomain.com |

---

## Frequently Asked Questions

**Q: Which email provider is best for KeyManager?**  
A: For most users, SendGrid or Amazon SES offer the best balance of reliability, deliverability, and cost. Gmail works well for low-volume senders.

**Q: Can I use a free Gmail account?**  
A: Yes for testing, but not recommended for production. Gmail has sending limits (500/day) and may flag automated emails as spam.

**Q: What's the difference between TLS and SSL?**  
A: TLS is the modern, more secure version. Both encrypt email, but TLS is preferred. Use TLS with port 587.

**Q: Why do my emails go to spam?**  
A: Most often due to missing SPF/DKIM records. Verify your domain with your email provider and set up proper DNS records.

**Q: How do I know if my configuration is correct?**  
A: Use the Test Email feature. If the email arrives in your inbox with correct sender info, configuration is valid.

**Q: Can I change email settings without affecting sent emails?**  
A: Yes, settings only apply to future emails. Already-sent emails are not affected.

**Q: Should I use noreply@ or support@ as sender?**  
A: Use support@ or a monitored address for better customer experience. Noreply addresses frustrate users who want to respond.

---

## How to Access

1. Log in to the Admin Portal
2. Navigate to **Settings** in the main menu
3. Click the **Email Settings** tab
4. Configure SMTP settings
5. Send test email to verify
6. Click **Save Settings** at the bottom
7. Monitor email delivery in production

---

## Related Settings

- [Settings Overview]({{< ref "/content/docs/admin-portal/settings/_index" >}}) - All settings tabs
- [General Settings]({{< ref "/content/docs/admin-portal/general" >}}) - Configure support email
- [Webhook Settings]({{< ref "/content/docs/admin-portal/webhooks" >}}) - Email event notifications
- [Logging Settings]({{< ref "/content/docs/admin-portal/logging" >}}) - Track email sending events

---

**Proper email configuration ensures reliable communication with customers and administrators.**
