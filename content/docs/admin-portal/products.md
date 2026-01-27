---
title: Products
weight: 20
---

![Admin Portal Products Screenshot](placeholder-products-overview.png)
*Screenshot of the Products page showing the list view with search, filters, and product management actions*

---

## What Is This Page?

The **Products** page is where you define and manage all licensable products in your platform. Each product represents software, services, digital goods, or any item that requires licensing. This page serves as the foundation for your entire license management system—you must create a product here before you can generate licenses, create generators, or configure downloadables.

Think of products as the "master catalog" of everything you license. Each product has its own cryptographic keys, feature flags, branding, and configuration independent of other products in your system.

---

## When to Use This Page

You'll use the Products page when you need to:

* **Set up a new product** — The very first step before creating any licenses
* **Configure cryptography** — Generate RSA key pairs for license signing and offline validation
* **Manage product branding** — Upload logos/images that appear in portals and emails
* **Control product status** — Enable or disable licensing for specific products
* **View public keys** — Export public keys for embedding in your software
* **Rotate cryptographic keys** — Emergency key changes when keys are compromised
* **Configure product features** — Define feature flags that licenses can enable/disable
* **Set up Envato sync** — Link products to Envato marketplace items
* **Activate kill switch** — Emergency shutdown of all licenses for a product
* **Search and filter products** — Find specific products across environments
* **Delete products** — Permanently remove products and all associated data

💡 **Tip:** Always create and test products in the `development` or `staging` environment first before creating them in `production`.

---

## What You Can Do Here

### 1. View All Products

The main table displays all products in your current environment with the following information:

| Column | Description |
|--------|-------------|
| **Name** | Display name of the product (e.g., "Pro WordPress Plugin", "Enterprise SaaS") |
| **Product UUID** | Unique identifier used in APIs and URLs (with copy button) |
| **Source** | Origin of product: `manual`, `api`, `contract`, `envato`, or `import` |
| **Status** | `active` (licenses can be created) or `inactive` (paused) |
| **Require License** | Whether license verification is enforced (`Yes`) or permissive mode (`No`) |
| **Environment** | `production`, `staging`, or `development` |
| **Created** | Date when product was added to the system |
| **Actions** | Dropdown menu with Edit, View Public Key, Download Public Key, Delete |

#### Search and Filters

**Search Box** (top-left)
- Search by product name
- Search by product UUID
- Searches in real-time as you type (300ms debounce)

**Status Filter**
- All Statuses (default)
- Active only
- Inactive only

**Source Filter**
- All Sources (default)
- Manual (created via Admin UI)
- API (created via API calls)
- Contract (generated from contracts)
- Envato (synced from Envato marketplace)
- Import (bulk imported)

**Per Page Selector**
- 10 per page (default)
- 15 per page
- 25 per page
- 50 per page

**Sort Modal** (side panel)
- Click the sort icon (top-right of filters) to open
- **Sort By:** Name, Product UUID, Source, Status, Require License, Environment, Created
- **Order:** Ascending or Descending
- Changes apply immediately

💡 **Tip:** Combine filters for precise searches. For example: "Status: Active + Source: Envato + Sort by Created (Desc)" shows your newest active Envato products.

---

### 2. Create Product

Click **"Create Product"** button (top-right) to add a new product.

#### Basic Information

**Product Name** (Required)
- Human-readable name shown everywhere (Admin UI, Client Portal, emails)
- Can be changed later
- Examples: "WordPress Pro Plugin", "Cloud Suite Enterprise", "Mobile App Premium"

**Description** (Optional)
- Brief explanation of the product (multiline textarea, 4 rows)
- Shown in Client Portal and email templates
- Supports plain text only (no HTML)
- Keep it concise (1–3 sentences)

**Status** (Required, dropdown)
- **Active:** Licenses can be created and verified for this product
- **Inactive:** Product is paused—no new licenses can be created, existing licenses continue to work

**Source** (Required, dropdown)
- **Internal:** Product is managed entirely within this platform (most common)
- **Envato:** Product is synced from Envato marketplace (requires Envato Item ID)

#### Cryptographic Configuration

**Signing Algorithm** (Required, dropdown)
- **RSA-SHA256** (Recommended) — Industry standard, widely supported
- **RSA-SHA512** (More Secure) — Stronger hashing, slightly larger signatures

This algorithm is used to:
- Sign license keys during generation
- Sign offline license files for validation
- Verify license authenticity in your software

⚠️ **Warning:** Choose carefully—changing this later requires key rotation and product updates.

#### Envato Integration (Only shown if Source = Envato)

**Envato Item ID** (Optional)
- The numeric ID from your CodeCanyon/ThemeForest product URL
- Example: `https://codecanyon.net/item/product-name/12345678` → Enter `12345678`
- Used for automatic license syncing and purchase verification
- Can be changed later

💡 **Tip:** You can find your Envato Item ID in the product URL on CodeCanyon or ThemeForest.

#### Product Options (Checkboxes)

**Require Valid License**
- ☑ Checked: License verification must pass for software to function (strict mode)
- ☐ Unchecked: Software functions even without valid license (permissive mode)
- Use unchecked for trial/demo mode or during migration periods
- Can be toggled later

**Send Email on License Issue**
- ☑ Checked: Customer receives email when a new license is created or assigned to them
- ☐ Unchecked: No automatic emails sent
- Requires Email settings to be configured in [Settings > Email]({{< ref "/../docs/docs/admin-portal/settings" >}})
- Can be toggled later

**Enable Changelog**
- ☑ Checked: Product has a public changelog page that customers can view
- ☐ Unchecked: No changelog available
- Changelog entries are managed separately (not on this page)
- Can be toggled later

#### Product Features

Define features that can be enabled/disabled for individual licenses.

**Why Use Features?**
- Create tiered licensing (Basic vs Pro vs Enterprise)
- Enable/disable specific functionality per license
- Control limits (max users, API calls, storage, etc.)
- Feature flags are embedded in licenses and offline license files

**Adding Features**
1. Click **"Add Feature"** button
2. Fill in the feature details (see fields below)
3. Click **"Add Feature"** again to add more
4. Features can be reordered or removed

**Feature Fields**

| Field | Description |
|-------|-------------|
| **Key** | Technical identifier used in code (e.g., `api_access`, `max_users`, `cloud_storage`) |
| **Label** | Human-readable name (e.g., "API Access", "Maximum Users", "Cloud Storage") |
| **Type** | Data type: `boolean` (Yes/No), `number` (integer), `string` (text) |
| **Default Value** | Value assigned to new licenses (e.g., `true`, `100`, `unlimited`) |
| **Description** | Optional explanation of what this feature does (shown in UI) |

**Example Feature Configuration**

```
Feature #1
  Key: api_access
  Label: API Access
  Type: boolean
  Default Value: true
  Description: Enables REST API access for this license

Feature #2
  Key: max_users
  Label: Maximum Users
  Type: number
  Default Value: 10
  Description: Maximum number of concurrent users

Feature #3
  Key: support_level
  Label: Support Level
  Type: string
  Default Value: standard
  Description: Support tier: basic, standard, or premium
```

💡 **Tip:** Define features **before** generating licenses. Changing features later doesn't affect existing licenses—only new ones.

---

### 3. Edit Product

Click **Edit** in the Actions menu for any product to update its details.

**Editable Fields** (Same as Create Product)
- Product Name
- Description
- Status (Active/Inactive)
- Source (Internal/Envato)
- Signing Algorithm (⚠️ requires key rotation to take effect)
- Envato Item ID (if source = Envato)
- Product Options (checkboxes)
- Product Features (add/edit/remove)

**Non-Editable Fields**
- Product UUID (immutable identifier)
- Environment (set during creation, cannot be changed)
- Created Date

⚠️ **Critical:** Changing the signing algorithm does NOT automatically rotate keys. You must explicitly click "Rotate Keys" in the Danger Zone.

---

### 4. View/Download Public Key

**View Public Key**
1. Click **Actions** → **View Public Key**
2. Modal appears showing the RSA public key in PEM format
3. Click **Copy** button to copy to clipboard
4. Click **Download** to save as `.pem` file

**Download Public Key**
1. Click **Actions** → **Download Public Key**
2. File downloads immediately as `product-{uuid}-public.pem`

**Why You Need the Public Key**
- Embed in your software to verify licenses offline
- Use in your SDK initialization
- Required for cryptographic signature verification
- Should be included in your product's source code or binary

💡 **Best Practice:** Store the public key in your product's version control system (e.g., `src/license-public-key.pem`).

---

### 5. Delete Product

Click **Actions** → **Delete** to permanently remove a product.

**Confirmation Required**
- Displays modal: "Are you sure you want to delete this product? This action cannot be undone."
- Must click **Delete** again to confirm

**What Gets Deleted**
- The product record itself
- ALL licenses for this product (in all states)
- ALL activations for this product
- ALL generators for this product
- ALL downloadables for this product
- Product images (from S3)
- All associated audit trails remain (immutable)

⚠️ **Warning:** Deletion is permanent and irreversible. Consider setting status to `inactive` instead to preserve data.

---

### 6. Validate Public Key (Top-right button)

Click **"Validate Public Key"** to verify cryptographic key integrity.

**What This Does**
- Tests that public/private key pairs are valid
- Verifies keys can sign and verify data correctly
- Checks for corrupted or mismatched keys
- Validates algorithm consistency

**Use This When**
- After rotating keys
- After importing products
- If license verification fails unexpectedly
- During troubleshooting

💡 **Tip:** Run this validation immediately after key rotation to catch issues early.

---

## Danger Zone (Edit Mode Only)

When editing an existing product, a **Danger Zone** section appears at the bottom of the form.

⚠️ **Warning:** These actions are irreversible and can have serious consequences for your customers.

### Rotate Cryptographic Keys

**What This Does**
- Generates a brand new RSA key pair (public + private)
- Old keys are archived (not deleted)
- Old public key remains embedded in existing product versions
- New public key must be embedded in future product versions

**When to Use This**
- Private key is compromised or leaked
- Suspected unauthorized license generation
- Regulatory compliance requirements
- Security audit recommendations

**Impact**
- ALL existing offline licenses become invalid (they were signed with old key)
- Online licenses continue to work (server validates with either key during grace period)
- Customers using offline validation must update to new product version
- Activations are not affected (they don't rely on signatures)

**Process**
1. Click **"Rotate Keys"** button
2. Confirmation modal appears
3. System generates new RSA-4096 key pair
4. Old keys are archived with timestamp
5. New public key is immediately available for download
6. **YOU MUST:** Update your product's source code with the new public key and release an update

⚠️ **Critical:** Do NOT rotate keys unless absolutely necessary. This is an emergency measure.

---

### Product Kill Switch

**What This Does**
- Immediately sets product status to `inactive`
- Marks all licenses for this product as `revoked`
- Stops all license verifications from succeeding
- Activations are immediately disabled

**When to Use This**
- Critical security vulnerability discovered in your product
- DMCA takedown or legal requirement
- Unauthorized distribution detected
- Emergency shutdown required

**Impact**
- ALL customers lose access immediately (within minutes as verifications fail)
- All licenses show as `revoked` in system
- No new licenses can be created
- Customer support will receive complaints/tickets
- Cannot be undone easily (requires manual license restoration)

**Process**
1. Click **"Activate Kill Switch"** button
2. Confirmation modal appears with strong warning
3. System immediately revokes all licenses
4. Email notifications sent (if configured)
5. Event logged in audit trail

⚠️ **Critical:** Use this only in extreme emergencies. This will immediately break your product for all customers.

---

### Delete Product

Same as the Delete action in the main list, but available directly in the edit form.

⚠️ **Warning:** This is at the bottom of the Danger Zone because it's the most destructive action.

---

## Use Cases & Workflows

### Workflow 1: Setting Up Your First Product

**Scenario:** You're launching a new WordPress plugin and need to set up licensing.

**Steps:**
1. Go to Admin Portal → **Products**
2. Click **Create Product**
3. Fill in:
   - Name: "WP SEO Master Pro"
   - Description: "Advanced SEO toolkit for WordPress"
   - Status: Active
   - Source: Internal
   - Signing Algorithm: RSA-SHA256
   - ☑ Require Valid License
   - ☑ Send Email on License Issue
   - ☑ Enable Changelog
4. Add features:
   - Feature 1: `seo_analysis` → "SEO Analysis Tools" → boolean → true
   - Feature 2: `max_sites` → "Maximum Sites" → number → 1
   - Feature 3: `support_level` → "Support Level" → string → "standard"
5. Click **Create Product**
6. Click **Actions** → **Download Public Key**
7. Add the public key file to your WordPress plugin at `includes/license-key.pem`
8. Next: Create a [Generator]({{< ref "/../docs/docs/admin-portal/generators" >}}) for this product
9. Next: Create [Licenses]({{< ref "/../docs/docs/admin-portal/licenses" >}}) for testing

---

### Workflow 2: Migrating Envato Marketplace Product

**Scenario:** You have an existing CodeCanyon plugin and want to migrate to this licensing system.

**Steps:**
1. Go to Admin Portal → **Products**
2. Click **Create Product**
3. Fill in:
   - Name: "Ultimate Form Builder"
   - Description: "Drag-and-drop form builder for WordPress"
   - Status: Active
   - Source: **Envato** (triggers Envato Item ID field)
   - Envato Item ID: `12345678` (from your CodeCanyon URL)
   - Signing Algorithm: RSA-SHA256
   - ☑ Require Valid License
   - ☑ Send Email on License Issue
   - ☐ Enable Changelog (using Envato's changelog)
4. Add features if needed (or keep empty to start)
5. Click **Create Product**
6. Go to [Settings > Envato]({{< ref "/../docs/docs/admin-portal/settings" >}}) to configure API credentials
7. System will automatically sync purchases and generate licenses

---

### Workflow 3: Creating Product Tiers (Basic, Pro, Enterprise)

**Scenario:** You want to sell 3 different license tiers with different capabilities.

**Option A: Single Product with Feature Flags** (Recommended)

1. Create **one product** named "Cloud Storage App"
2. Add features:
   - `tier` → "License Tier" → string → "basic"
   - `storage_gb` → "Storage (GB)" → number → 10
   - `api_access` → "API Access" → boolean → false
   - `priority_support` → "Priority Support" → boolean → false
   - `max_users` → "Maximum Users" → number → 1
3. Create **three generators** for the same product:
   - Basic Generator: `tier=basic, storage_gb=10, api_access=false, max_users=1`
   - Pro Generator: `tier=pro, storage_gb=100, api_access=true, max_users=5`
   - Enterprise Generator: `tier=enterprise, storage_gb=1000, api_access=true, priority_support=true, max_users=unlimited`
4. Generate licenses from the appropriate generator based on purchase tier

**Option B: Separate Products** (Simpler, but less flexible)

1. Create 3 products:
   - "Cloud Storage App - Basic"
   - "Cloud Storage App - Pro"
   - "Cloud Storage App - Enterprise"
2. Each product has different default features
3. Use different public keys (customers cannot "upgrade" their license by changing files)

💡 **Recommendation:** Option A is better for most use cases because it allows easier upgrades/downgrades and simpler product management.

---

### Workflow 4: Emergency Key Rotation (Compromised Private Key)

**Scenario:** You suspect your private key has been leaked or stolen.

**Steps:**
1. Go to Admin Portal → **Products**
2. Click **Actions** → **Edit** for the affected product
3. Scroll to **Danger Zone**
4. Click **"Rotate Keys"** button
5. Read the confirmation message carefully
6. Click **Confirm**
7. System generates new key pair
8. Immediately click **Actions** → **Download Public Key**
9. **Critical:** Update your product's source code with the new public key
10. Release an emergency update to all customers
11. Notify customers that offline licenses must be regenerated
12. Monitor [Telemetry]({{< ref "/../docs/docs/admin-portal/telemetry" >}}) and [Logs]({{< ref "/../docs/docs/admin-portal/logs" >}}) for verification failures

**Communication Template (Email to Customers)**

```
Subject: Important Security Update Required

Dear Customer,

We've detected a potential security issue and have taken immediate action
to protect your license. Please update to version X.X.X immediately, which
includes updated security certificates.

Your license key remains valid, but offline validation requires the update.
Online verification continues to work without any action needed.

If you have any questions, please contact support.

Best regards,
Your Team
```

---

### Workflow 5: Activating Kill Switch (Emergency Shutdown)

**Scenario:** Critical security vulnerability discovered that must be patched before customers can use your product.

**Steps:**
1. Go to Admin Portal → **Products**
2. Click **Actions** → **Edit** for the affected product
3. Scroll to **Danger Zone**
4. Click **"Activate Kill Switch"** button
5. Read the confirmation message **very carefully**
6. Type confirmation text (if required)
7. Click **Confirm**
8. System immediately:
   - Sets product status to `inactive`
   - Revokes all licenses
   - Sends notifications (if configured)
9. Prepare and release fixed version of your product
10. Go to [Licenses]({{< ref "/../docs/docs/admin-portal/licenses" >}}) page
11. Bulk select all affected licenses
12. Click **"Restore"** to reactivate them
13. OR: Create new licenses for affected customers

⚠️ **Warning:** Only use kill switch in true emergencies. Customer trust is hard to rebuild.

---

## Security Considerations

### Private Key Security

**How Private Keys Are Stored**
- Encrypted at rest in database
- Never transmitted over network (except during generation)
- Never shown in Admin UI (only public keys are visible)
- Only accessible by system during license signing
- Backed up with application database (encrypted)

**Best Practices**
- Use strong database encryption keys (see Settings > Security)
- Restrict database access to trusted administrators only
- Enable 2FA for all admin accounts
- Audit logs track all key rotation events
- Never store private keys in source control
- Never share private keys with anyone (including customers)

---

### Public Key Distribution

**How to Embed Public Keys in Your Product**

**Option 1: Hardcode in Source** (Most Secure)
```php
// PHP Example
const LICENSE_PUBLIC_KEY = "-----BEGIN PUBLIC KEY-----
MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEA...
-----END PUBLIC KEY-----";
```

**Option 2: Include as File** (Easier to Update)
```php
// PHP Example
$publicKey = file_get_contents(__DIR__ . '/license-key.pem');
```

**Option 3: Download on First Run** (Least Secure, but most flexible)
```php
// Fetch from your server
$publicKey = file_get_contents('https://yoursite.com/api/product/public-key');
```

💡 **Recommendation:** Use Option 1 or 2 for maximum security. Option 3 can be bypassed by blocking network access.

---

### Environment Isolation

Products are **strictly isolated by environment**:
- `production` products are completely separate from `staging` and `development`
- Cross-environment access is forbidden by the system
- Licenses from one environment cannot be used in another
- Public keys are environment-specific

**Why This Matters**
- Test licensing changes safely in staging without affecting production customers
- Debug issues in development without exposing production data
- Simulate production scenarios without risk

**Best Practice Workflow**
1. Create product in `development` first
2. Test thoroughly with test licenses and SDK integration
3. Once validated, create identical product in `staging`
4. Test again with staging licenses
5. Finally, create in `production` when confident
6. Keep all three in sync as you make changes

---

## Common Pitfalls & Solutions

### Pitfall 1: Forgetting to Download Public Key

**Problem:** Created product but didn't download public key before integrating SDK.

**Solution:**
1. Go to Products page
2. Find your product
3. Click **Actions** → **Download Public Key**
4. Add to your product's source code
5. Public key never changes unless you rotate keys

---

### Pitfall 2: Using Wrong Environment

**Problem:** Created product in `development` but trying to verify licenses in `production`.

**Solution:**
- Environment is set during product creation and cannot be changed
- Delete the incorrectly-created product
- Recreate in correct environment
- Update your SDK configuration to point to correct environment

---

### Pitfall 3: Changing Signing Algorithm Without Key Rotation

**Problem:** Changed signing algorithm in form but licenses still use old algorithm.

**Solution:**
- Changing algorithm in dropdown does NOT rotate keys
- You must explicitly click **"Rotate Keys"** in Danger Zone
- Existing licenses continue using old algorithm
- New licenses will use new algorithm after rotation

---

### Pitfall 4: Deleting Product Instead of Setting Inactive

**Problem:** Deleted product to "pause" it temporarily, but lost all licenses and data.

**Solution:**
- **NEVER** delete products unless you want permanent data loss
- Use **Status: Inactive** instead to pause a product
- Inactive products prevent new licenses but preserve all data
- Can be reactivated at any time

---

### Pitfall 5: Not Testing in Staging First

**Problem:** Created product directly in production, discovered issues later.

**Solution:**
- **Always** create products in `staging` or `development` first
- Test end-to-end: create product → generate licenses → SDK integration → verification
- Only move to `production` after thorough testing
- Keep test products around for ongoing development

---

## FAQs

### Can I change a product's environment after creation?

**No.** Environment is set during creation and is immutable. If you need to move a product to a different environment, you must:
1. Create a new product in the target environment (use same name and settings)
2. Export licenses from old product (if needed)
3. Import or recreate licenses in new product
4. Update your software to use new product UUID and public key

This is intentional to enforce strict environment isolation.

---

### What happens to licenses when I set a product to "Inactive"?

**Existing licenses continue to work normally.** Setting a product to inactive:
- ☑ Prevents new licenses from being created
- ☑ Prevents new activations (if configured)
- ☐ Does NOT revoke existing licenses
- ☐ Does NOT disable existing activations
- ☐ Does NOT affect license verification

Use the Kill Switch if you need to immediately disable all licenses.

---

### Can I have multiple products with the same name?

**Yes, but not recommended.** Product names are not unique identifiers—Product UUIDs are. However, having multiple products with identical names causes confusion in:
- Admin UI (hard to distinguish)
- Client Portal (customers see duplicate names)
- Reports and analytics
- Support tickets

**Best Practice:** Use suffixes like "Product Name (Staging)" or "Product Name v2" to differentiate.

---

### How do I "upgrade" a customer from Basic to Pro tier?

This depends on your product architecture:

**If using single product with feature flags:**
1. Go to [Licenses]({{< ref "/../docs/docs/admin-portal/licenses" >}}) page
2. Find the customer's license
3. Click **Edit**
4. Update feature flags (e.g., change `tier` from "basic" to "pro")
5. Save changes
6. Customer's next verification will reflect new features

**If using separate products per tier:**
1. Create a new license from the "Pro" product
2. Assign it to the customer
3. Revoke or expire the old "Basic" license
4. Customer must update their license key in your software

**Recommendation:** Single product with feature flags makes upgrades/downgrades much easier.

---

### Can I restore a deleted product?

**No.** Product deletion is permanent and irreversible. All associated data (licenses, activations, generators, downloadables) is deleted immediately.

**Audit trails are preserved** for compliance, but the functional data cannot be restored.

**Prevention:** Always use Status: Inactive instead of deletion unless you're absolutely certain.

---

### What's the difference between "Source" and "Environment"?

**Source** = Where the product came from
- `manual`: Created via Admin UI
- `api`: Created via API call
- `contract`: Auto-generated from a contract
- `envato`: Synced from Envato marketplace
- `import`: Imported from external system

**Environment** = Deployment stage for isolation
- `production`: Live customer licenses
- `staging`: Pre-production testing
- `development`: Local/dev testing

Source is informational; Environment affects system behavior (strict isolation, API endpoints, etc.).

---

### Why can't I see private keys in the UI?

**Security by design.** Private keys:
- Are stored encrypted in the database
- Are never displayed in any UI
- Are only decrypted temporarily during license signing operations
- Cannot be exported or downloaded (only public keys can)

If you lose access to your database, you lose the private keys. There is no recovery mechanism (by design).

**Disaster Recovery:** Back up your database regularly. The private keys are in the `products` table (encrypted).

---

### How do I test license verification before going live?

1. Create a product in `development` environment
2. Download the public key
3. Create a [Generator]({{< ref "/../docs/docs/admin-portal/generators" >}}) for the product
4. Generate a few test licenses
5. Integrate your SDK with the `development` public key
6. In your code, point SDK to `https://yourdomain.com/api/v1` and use `environment: development`
7. Test verification with valid licenses, expired licenses, revoked licenses
8. Once confident, repeat process in `production`

**Pro Tip:** Keep development product around permanently for ongoing testing.

---

## ✅ Best Practices Summary

1. **Always test in non-production environments first** before creating products in production
2. **Download and backup public keys immediately** after product creation
3. **Use descriptive product names** that clearly identify the product
4. **Define product features upfront** to avoid confusion later
5. **Use RSA-SHA256 signing algorithm** unless you have specific need for SHA-512
6. **Set status to Inactive** instead of deleting products to preserve data
7. **Document your products** in internal wiki/docs (especially cryptographic details)
8. **Rotate keys only when absolutely necessary** (major security risk)
9. **Use Kill Switch only in true emergencies** (breaks all customer access immediately)
10. **Keep product images consistent** in size and style across all products

---

## ❗ Troubleshooting

### Problem: Cannot create product - "Environment required"

**Solution:**
- Environment selector is missing or has validation error
- Refresh the page and try again
- Check that your admin account has permission to create products
- Verify database migration is complete (environment column exists)

---

### Problem: "Source filter shows no products"

**Solution:**
- You may have no products with that specific source in the current environment
- Try "All Sources" filter
- Verify you're in the correct environment (check environment filter if available)
- Check if products exist at all using "All Statuses" + "All Sources"

---

### Problem: Public key modal is blank/empty

**Solution:**
- Product may not have cryptographic keys generated yet
- This can happen if product creation was interrupted
- Edit the product and click **"Rotate Keys"** to generate new keys
- If problem persists, check [Logs]({{< ref "/../docs/docs/admin-portal/logs" >}}) for errors

---

### Problem: Product features not showing in generated licenses

**Solution:**
- Features defined on product are templates/defaults only
- They must be configured in the [Generator]({{< ref "/../docs/docs/admin-portal/generators" >}}) for the product
- Edit the generator and set feature values there
- Already-generated licenses won't be affected (features are copied at creation time)

---

### Problem: "Envato Item ID" field not appearing

**Solution:**
- Field only appears when **Source = Envato**
- Change Source dropdown to "Envato" and field will appear
- Save product before entering Envato Item ID

---

### Problem: Image upload succeeds but image doesn't appear

**Solution:**
- Check [Settings > S3]({{< ref "/../docs/docs/admin-portal/settings" >}}) configuration is correct
- Verify S3 bucket has public read permissions (or signed URLs are enabled)
- Clear browser cache (Ctrl+F5 / Cmd+Shift+R)
- Check browser console for CDN/CORS errors
- Verify image URL is accessible directly in new browser tab

---

### Problem: Can't delete product - "Product has associated licenses"

**Solution:**
- System prevents accidental deletion of products with licenses
- You must first delete or revoke all licenses for the product
- Go to [Licenses]({{< ref "/../docs/docs/admin-portal/licenses" >}}) page
- Filter by product
- Bulk delete or revoke licenses
- Then try deleting product again
- **Alternative:** Set product to Inactive instead of deleting

---

### Problem: License verification fails after changing signing algorithm

**Solution:**
- Changing algorithm in dropdown does NOT rotate keys
- Click **"Rotate Keys"** in Danger Zone to generate new keys with new algorithm
- Download new public key
- Update your product's source code with new public key
- Release update to customers

---

### Problem: Kill Switch didn't revoke all licenses

**Solution:**
- Kill Switch is processed by background job (may take 30-60 seconds)
- Check [Background Jobs]({{< ref "/../docs/docs/admin-portal/background-jobs" >}}) page for job status
- Refresh license list after 1-2 minutes
- If still not working, check [Logs]({{< ref "/../docs/docs/admin-portal/logs" >}}) for errors
- Manual workaround: Bulk select licenses and click "Revoke" directly

---

## Related Documentation

- **[License Generators]({{< ref "/../docs/docs/admin-portal/generators" >}})** — Configure how licenses are created for this product
- **[License Keys]({{< ref "/../docs/docs/admin-portal/licenses" >}})** — View and manage licenses generated for this product
- **[Downloadables]({{< ref "/../docs/docs/admin-portal/downloadables" >}})** — Add product files/updates that customers can download
- **[Settings > S3]({{< ref "/../docs/docs/admin-portal/settings" >}})** — Configure image storage for product logos
- **[Settings > Envato]({{< ref "/../docs/docs/admin-portal/settings" >}})** — Set up Envato marketplace integration
- **[Telemetry]({{< ref "/../docs/docs/admin-portal/telemetry" >}})** — Monitor product usage and license verification patterns

---

## How to Access

1. Log in to the Admin Portal with your admin credentials
2. Click **Products** in the main navigation menu (usually second item after Dashboard)
3. The page will load showing all products in your current environment

**Direct URL:** `/admin/products`

**Keyboard Shortcut:** Press `Ctrl+K` (Windows) or `Cmd+K` (Mac) to open Global Search, then type "products" and press Enter.

---

## Related Pages

- [Dashboard]({{< ref "/../docs/docs/admin-portal/dashboard" >}}) - Main overview and KPIs
- [License Generators]({{< ref "/../docs/docs/admin-portal/generators" >}}) - Configure license creation rules
- [License Keys]({{< ref "/../docs/docs/admin-portal/licenses" >}}) - View and manage all licenses
- [Settings]({{< ref "/../docs/docs/admin-portal/settings" >}}) - System-wide configuration
- [Profile]({{< ref "/../docs/docs/admin-portal/profile" >}}) - Your admin profile and security settings
