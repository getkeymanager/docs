---
title: Abuse Case Management
weight: 186
---

![Admin Portal Abuse Case Management Screenshot](placeholder-abuse-overview.png)
*Screenshot of the Abuse Case Management page showing detected violations, investigation status, and enforcement actions*

---

## What Is This Page?

The **Abuse Case Management** page is your command center for detecting, investigating, and responding to license violations, piracy attempts, and fraudulent usage. The system automatically monitors for suspicious activity patterns and provides tools to enforce your license terms.

**Key Capabilities:**
* **Automated Detection** — Identifies unusual activation patterns, license sharing, and abuse
* **Investigation Tools** — Track violation history, analyze usage patterns, review evidence
* **Enforcement Actions** — Blacklist users, revoke licenses, block activations
* **Reporting System** — Document violations for legal or DMCA action
* **Piracy Prevention** — Protect your revenue and intellectual property

---

## When to Use This Page

* **Investigate suspicious activity** — Review flagged licenses and activation patterns
* **Respond to piracy reports** — Handle customer reports of leaked or nulled licenses
* **Enforce license terms** — Take action against violators
* **Track abuse patterns** — Identify repeat offenders or coordinated piracy
* **Generate DMCA reports** — Document violations for legal takedown requests
* **Monitor license sharing** — Detect and prevent unauthorized license distribution
* **Protect revenue** — Stop losses from fraudulent use and key sharing

---

## What You Can Do Here

### 1. View All Abuse Cases

The main dashboard displays detected abuse cases with the following information:

| Column | Description |
|--------|-------------|
| **Case #** | Unique case identifier (e.g., ABUSE-2001) |
| **Type** | Violation category (see types below) |
| **Severity** | Risk level: Low, Medium, High, Critical |
| **License Key** | Affected license(s) |
| **Customer** | Associated customer account (if known) |
| **Detection Method** | How violation was identified |
| **Status** | Investigation stage: Detected, Under Review, Confirmed, Resolved, False Positive |
| **Created** | When abuse was first detected |
| **Actions** | Investigate, enforce, or dismiss |

### 2. Abuse Case Types

The system automatically detects and categorizes violations:

| Type | Description | Auto-Detection |
|------|-------------|----------------|
| **Excessive Activations** | License activated far beyond normal limits | ✅ Yes |
| **Rapid Deactivation/Reactivation** | Pattern suggesting license sharing | ✅ Yes |
| **Geolocation Anomaly** | Simultaneous activations from distant locations | ✅ Yes |
| **Hardware ID Cycling** | Frequent hardware ID changes | ✅ Yes |
| **Nulled/Cracked Version** | Modified client detected via telemetry | ✅ Yes |
| **Leaked License** | License key found on piracy sites | Manual |
| **Fraudulent Purchase** | Chargeback or stolen payment method | Manual |
| **License Sharing** | Evidence of public key distribution | Manual |
| **Terms Violation** | Customer violated license agreement | Manual |
| **Reported Piracy** | Third-party piracy report | Manual |

### 3. Filter Abuse Cases

**Available Filters:**
* **Status** — Detected, Under Review, Confirmed, Resolved, False Positive
* **Severity** — Low, Medium, High, Critical
* **Type** — Filter by violation category
* **Date Range** — When cases were detected
* **Customer** — Show all cases for specific customer
* **Product** — Filter by affected product

**Quick Filters:**
* **Unreviewed** — Cases needing investigation
* **High Priority** — Critical and High severity cases
* **Confirmed Violations** — Cases with evidence of abuse
* **Repeat Offenders** — Customers with multiple cases

### 4. Search Cases

Search for specific cases by:
* Case number (ABUSE-2001)
* License key
* Customer name or email
* Hardware ID
* IP address

### 5. Investigate an Abuse Case

Click on any case to open the detailed investigation view:

**Case Overview:**
* Complete violation timeline
* Detection triggers and evidence
* Related licenses and activations
* Customer history and previous violations

**Evidence Panel:**
* Activation patterns (chart showing unusual spikes)
* Geolocation map (if activations from multiple countries)
* Hardware ID list (all devices used with this license)
* Telemetry data (usage patterns, modified clients)
* IP address history

**Customer Context:**
* All licenses owned by this customer
* Purchase history and payment methods
* Previous abuse cases (if any)
* Customer account status
* Communication history

**Automated Risk Score:**
The system calculates a risk score (0-100) based on:
* Number of violations
* Severity of violations
* Customer history
* Activation patterns
* Telemetry signals

### 6. Detection Rules and Triggers

Configure automated detection in **Settings → Abuse Detection**:

**Activation Pattern Rules:**
* **Activation Spike** — X activations within Y minutes (default: 10 in 1 hour)
* **Geographic Spread** — Activations from Y+ countries within X hours (default: 3 countries in 24 hours)
* **Rapid Cycling** — Deactivate + reactivate pattern (default: 5+ cycles in 1 day)
* **Hardware ID Churn** — X+ different hardware IDs per license (default: 20+)

**Telemetry-Based Detection:**
* **Modified Client Signature** — Checksum mismatch in telemetry
* **Unusual Usage Patterns** — Activity outside normal hours or volumes
* **API Abuse** — Excessive validation requests from single key
* **Offline Validation Anomaly** — Same offline license file on multiple machines

**External Signals:**
* **Blacklist Check** — Email/IP matches known piracy database
* **Payment Fraud** — Chargeback or declined transaction
* **Known Pirate Domains** — License used from flagged hostnames

### 7. Take Enforcement Actions

When abuse is confirmed, you can take immediate action:

#### Action 1: Revoke License
* Immediately disable the license
* Block all future activations
* Deactivate all existing installations
* Customer loses access instantly

**Steps:**
1. Open abuse case
2. Click **Enforce** → **Revoke License**
3. Select revocation reason
4. Optionally notify customer via email
5. Confirm action

#### Action 2: Blacklist Customer
* Block customer email and payment methods
* Prevent future purchases
* Revoke all customer's licenses
* Add to global blacklist

**Use When:**
* Repeat offender
* Fraudulent purchases
* Deliberate piracy distribution

**Steps:**
1. Open abuse case
2. Click **Enforce** → **Blacklist Customer**
3. Select scope: Email only, Payment method, or Both
4. Add reason for record
5. Confirm blacklist

#### Action 3: Suspend License
* Temporarily disable license
* Can be unsuspended later
* Less severe than revocation
* Useful for investigation period

**Use When:**
* Investigating suspicious activity
* Awaiting customer response
* First-time violation with explanation

#### Action 4: Increase Activation Limit
* Allow more activations if false positive
* Common for development teams
* Adjust limits to legitimate use case

#### Action 5: Add Notes / Warning
* Document violation without action
* Issue warning to customer
* Track for future reference
* No immediate enforcement

### 8. Customer Communication

**Automated Violation Emails:**
When abuse detected, system can auto-send:
* **Warning Email** — First violation notice
* **Suspension Notice** — License temporarily disabled
* **Revocation Notice** — License permanently disabled
* **Appeal Instructions** — How customer can respond

**Manual Communication:**
* Send custom message from case detail
* Attach evidence (screenshots, logs)
* Request explanation from customer
* Offer resolution path (e.g., purchase additional licenses)

### 9. False Positive Handling

If investigation shows legitimate use:

1. Open the abuse case
2. Click **Mark as False Positive**
3. Document the reason (e.g., "Customer runs development cluster")
4. Optionally whitelist customer/license from similar detections
5. Case status → "False Positive" (archived)

**Common False Positives:**
* Development teams with multiple test machines
* CI/CD pipelines activating licenses
* Legitimate resellers distributing licenses
* Customers in regulated environments (VPNs, proxies)

**Prevention:**
* Create whitelist for known good actors
* Adjust detection thresholds
* Add customer notes to skip certain rules

### 10. Generate DMCA / Legal Reports

For takedown requests or legal action:

1. Select confirmed abuse cases
2. Click **Generate Report**
3. Choose report type:
   * **DMCA Takedown Notice** — For hosting providers
   * **Piracy Evidence Report** — For legal team
   * **Violation Summary** — For customer disputes
4. Report includes:
   * License keys involved
   * Evidence (screenshots, logs, telemetry)
   * Violation timeline
   * Customer information
   * Recommended actions
5. Export as PDF or send directly to legal team

---

## Abuse Detection Settings

Configure detection rules in **Settings → Abuse Detection**:

### General Settings
* **Enable Abuse Detection** — Turn on/off automated monitoring
* **Auto-Create Cases** — Automatically create cases when violations detected
* **Detection Sensitivity** — Low, Normal, High (affects trigger thresholds)
* **Notification Recipients** — Email alerts when new cases detected

### Activation Pattern Rules

| Rule | Default Threshold | Severity | Configurable |
|------|-------------------|----------|--------------|
| **Activation Spike** | 10 in 1 hour | High | ✅ Yes |
| **Geographic Anomaly** | 3 countries in 24h | Medium | ✅ Yes |
| **Rapid Cycling** | 5 cycles in 1 day | Medium | ✅ Yes |
| **Hardware ID Churn** | 20+ unique IDs | High | ✅ Yes |
| **Simultaneous Activation** | 5+ at same time | Critical | ✅ Yes |

### Telemetry-Based Detection

* **Enable Telemetry Analysis** — Monitor usage patterns
* **Client Signature Verification** — Detect modified/cracked versions
* **Anomaly Detection AI** — Machine learning-based pattern detection (requires data)

### IP and Geolocation

* **Enable IP Tracking** — Log activation IP addresses
* **GeoIP Database** — Use MaxMind or similar for location detection
* **VPN/Proxy Detection** — Flag activations from known VPN providers
* **Country Blacklist** — Auto-flag activations from specific countries

### Customer Blacklist

* **Blacklisted Emails** — Prevent purchases from these addresses
* **Blacklisted Domains** — Block entire domains (e.g., disposable emails)
* **Blacklisted Payment Methods** — Block specific cards/PayPal accounts
* **Blacklist Import** — Upload CSV of known pirates/fraudsters

### Automatic Enforcement

Configure automated responses to violations:

| Violation Type | Auto-Action | Configurable |
|----------------|-------------|--------------|
| **Critical Severity** | Auto-suspend license | ✅ Yes |
| **Repeat Offender (3+)** | Auto-blacklist customer | ✅ Yes |
| **Nulled Client Detected** | Auto-revoke + report | ✅ Yes |
| **Fraudulent Purchase** | Auto-blacklist payment | ✅ Yes |

⚠️ **Use with caution:** Automatic enforcement may impact legitimate users. Start with manual review.

---

## Common Workflows

### Workflow 1: Investigating Activation Spike

**Scenario:** System detects 15 activations in 30 minutes for a single license.

**Steps:**
1. Review case ABUSE-2001 in "Detected" queue
2. View activation timeline chart (shows 15 activations at 2:00 AM)
3. Check hardware IDs: All different, all newly created
4. Check IP addresses: All from same data center IP block
5. Review telemetry: All installations reporting same application signature
6. **Conclusion:** Bot attack or license sharing via automation
7. **Action:** Revoke license immediately
8. **Follow-up:** Notify customer, offer legitimate multi-seat license

### Workflow 2: Handling Leaked License on Piracy Forum

**Scenario:** Customer reports their license key posted on forum.

**Steps:**
1. Create manual abuse case: **Type: Leaked License**
2. Add forum URL and screenshots as evidence
3. Check license activations: 50+ activations from different countries
4. **Action 1:** Revoke license immediately
5. **Action 2:** Generate new license for legitimate customer
6. **Action 3:** Generate DMCA takedown report
7. Submit DMCA to forum host
8. Monitor for reposting (set alert on license key)

### Workflow 3: Resolving False Positive for Development Team

**Scenario:** Development agency flagged for 20 activations (CI/CD pipeline).

**Steps:**
1. Review case ABUSE-2005
2. Customer replies explaining CI/CD usage
3. Verify activations all from company's IP range
4. **Action:** Mark as "False Positive"
5. **Whitelist:** Add customer to automation whitelist
6. **Document:** Add note to customer account: "Uses CI/CD, expect high activation count"
7. **Adjust:** Increase activation limit to 100 for this license
8. Case status → "False Positive" (archived)

---

## Reporting and Analytics

### Abuse Dashboard

View abuse metrics in **Reports → Abuse Cases**:

* **Total Cases** — By status, type, and severity
* **Detection Rate** — How many violations detected per month
* **False Positive Rate** — Percentage of cases dismissed
* **Top Violation Types** — Which abuse patterns are most common
* **Repeat Offenders** — Customers with multiple cases
* **Revenue Protection** — Estimated losses prevented by enforcement
* **Geographic Distribution** — Map of where violations occur

### Export Options

* **Case List Export** — CSV of all cases with filters
* **Evidence Bundle** — ZIP file with all evidence for legal team
* **Monthly Summary** — Executive report for stakeholders

---

## Integration with Other Features

### Automatic License Revocation
When case is confirmed, revoke action triggers:
* License state → "Revoked"
* All activations deactivated
* Customer notification sent
* Audit trail created

### Customer Portal Impact
Customers with abuse cases:
* See violation notice in their dashboard
* Cannot create new activations (if suspended/revoked)
* Can submit appeal via ticket system
* Licenses show "Suspended" or "Revoked" status

### Webhook Notifications
Fire webhooks when:
* New abuse case detected
* Case status changed
* License revoked due to abuse
* Customer blacklisted

Configure in **Webhooks** settings.

---

## Legal and Compliance Considerations

### DMCA Compliance
* Document evidence thoroughly
* Include timestamps and technical details
* Generate proper DMCA notices
* Track takedown responses

### Privacy Regulations
* **GDPR:** Abuse data is processed for legitimate interest (contract enforcement)
* **Data Retention:** Cases retained for legal purposes (not subject to auto-purge)
* **Customer Rights:** Allow appeals and provide explanation of enforcement

### Terms of Service
Ensure your license agreement includes:
* Prohibition on sharing/distribution
* Monitoring and enforcement clauses
* Consequence of violations
* Appeal process

---

## Troubleshooting

**Problem:** Too many false positives

**Solution:**
1. Review detection thresholds in Settings
2. Increase activation spike threshold (e.g., 10 → 20 activations)
3. Increase timeframe (e.g., 1 hour → 4 hours)
4. Whitelist known good actors
5. Enable manual review for Medium severity

---

**Problem:** Abuse cases not being created

**Solution:**
1. Verify **Settings → Abuse Detection → Enable Abuse Detection** is ON
2. Check detection rules are configured
3. Ensure telemetry is being received
4. Review logs for detection job errors
5. Check **Background Jobs** for processing status

---

**Problem:** Customer disputes revocation

**Solution:**
1. Review case evidence
2. Check for false positive indicators
3. If legitimate: Mark false positive, restore license
4. If abuse confirmed: Provide evidence, explain policy
5. Offer resolution (purchase additional licenses if sharing)
6. Document all communication in case notes

---

## Technical Details

* **Detection Engine:** Runs every 15 minutes via background job
* **Storage:** Cases and evidence stored permanently (not purged)
* **Performance:** Indexed by license_key, customer_id, created_at
* **Machine Learning:** Optional AI-based anomaly detection (requires training data)
* **API Access:** Full API for integrating external fraud detection tools

---

## Related Pages

* [Licenses]({{< ref "/docs/admin-portal/licenses" >}}) — View and manage affected licenses
* [Customers]({{< ref "/docs/admin-portal/customers" >}}) — Customer history and blacklist status
* [Settings]({{< ref "/docs/admin-portal/settings" >}}) — Configure detection rules and thresholds
* [Webhooks]({{< ref "/docs/admin-portal/webhooks" >}}) — Automate enforcement actions
* [Audit Logs]({{< ref "/docs/admin-portal/settings#audit-trails" >}}) — Complete record of all enforcement actions

---

## How to Access

**Navigation:** Admin Portal → **Security** → **Abuse Cases**
**URL:** `/admin/abuse-cases`

**Permission Required:** Admin role or higher
