# Admin Portal User Guide  
## License Management Platform – v1.0

---

## 1. Purpose of the Admin Portal

The **Admin Portal** is the **control plane** of the License Management Platform.

It is used to:
- Configure products and licensing rules
- Govern license creation and lifecycle
- Manage enterprise contracts and resellers
- Monitor activations, telemetry, logs, and audits
- Control security, storage, and system-wide settings

The Admin Portal is **not** accessible to customers and must never be confused with the Client Self-Service Portal.

---

## 2. Admin Roles & Access Control

### 2.1 Admin User Types

Admin users belong to one or more roles:

- **Super Admin**
  - Full system access
  - Security, keys, disaster recovery
- **Admin**
  - Full product & license management
- **Operator**
  - Day-to-day operations
  - Limited destructive actions
- **Viewer**
  - Read-only access

> All admin actions are audited.

---

### 2.2 Authentication & Security

- Email + password login
- Optional Magic Link
- Two-Factor Authentication (TOTP)
- Session-based authentication
- Automatic session expiry

Admins are **never authenticated via API keys**.

---

## 3. Admin Portal Navigation Overview

### Primary Sections

- Dashboard
- Products
- Generators
- License Keys
- Contracts
- Activations
- Downloadables
- API Keys
- Telemetry
- Logs
- Audit Trails
- Email Templates
- Dashboard Widgets
- Settings
- Profile & Security

All routes use **UUIDs**, never numeric IDs.

---

## 4. Dashboard

The Dashboard provides a **high-level operational overview**.

### Key Components
- KPI cards:
  - Total products
  - Active licenses
  - Activations today
  - Failed verifications
- Recent activity log
- Telemetry widgets (configurable & reorderable)

Widgets reflect **real-time telemetry data** and respect environment isolation.

---

## 5. Products Management

### 5.1 Product List

Each product represents a licensable software or service.

Columns include:
- Name
- Source (Internal / Envato)
- Status
- Require valid license
- Environment
- Created date

Supports:
- Search
- Filters
- Pagination
- Bulk actions

---

### 5.2 Add / Edit Product

Products are created and edited on **dedicated pages**.

Fields include:
- Name
- Description
- Source
- Status
- Require license toggle
- Product image upload (stored in S3)
- Cryptographic configuration:
  - Private key
  - Passphrase
  - Algorithm

> Product keys can be rotated for disaster recovery.

---

### 5.3 Product Image

- Upload image via file picker
- Stored in S3 under product UUID
- Used in:
  - Admin UI
  - Public changelog page
  - Client portal (future)

---

## 6. Generators

Generators define **how license keys are created**.

### Supported Generator Types
- UUID-based
- Chunk-based
- Custom function

Each generator is:
- Product-scoped
- Environment-scoped
- Fully configurable

Activation limits and validity are enforced at runtime.

---

## 7. License Keys

### 7.1 License List

Displays all licenses with:
- Product
- Customer (if assigned)
- Status
- Expiry
- Activation count

Supports:
- Advanced filtering
- Bulk actions
- Search by partial key

---

### 7.2 License Lifecycle Awareness

Admins always see the current **license state**:
- available
- assigned
- active
- suspended
- expired
- revoked

State transitions:
- Are validated
- Are audited
- Cannot be skipped

---

### 7.3 License Explainability

Admins can view:
> “Why is this license invalid?”

Includes:
- Failed rule
- State
- Expiry reason
- HWID mismatch
- Activation limit details

This reduces support time and ambiguity.

---

## 8. Contracts (Enterprise / Resellers)

Contracts allow controlled license generation by third parties.

### Contract Features
- Product binding
- Generator enforcement
- License quota
- Expiry
- Scoped permissions

Admins can:
- Create / edit / delete contracts
- Monitor usage
- Revoke contract access

All contract actions are audited.

---

## 9. Activations

Activations represent **real installations**.

Admins can:
- View activations per license
- See identifier (HWID / domain)
- See last seen timestamp
- Deactivate activations

Deactivation:
- Requires confirmation
- Is audited
- Invalidates offline licenses

---

## 10. Downloadables & Updates

### 10.1 Downloadable Packages

Admins manage:
- Versions
- Numeric versions
- Changelog entries
- File uploads

Uploads support:
- Drag & drop
- ZIP files
- Images
- Videos

All files are stored in **S3 under product UUID folders**.

---

### 10.2 Access Rules

Admins define rules such as:
- License assigned after/before date
- License expiry constraints
- Access window

Access is enforced both online and offline.

---

## 11. Changelog Management

Each product can expose a **public changelog page**.

Admins can:
- Enable per product
- Enable globally via settings
- Control visibility

Changelog is also accessible via API (read-only).

---

## 12. API Keys

Admins manage API keys for automation.

API key features:
- Environment-scoped
- IP allowlisting
- Endpoint-level permissions
- Rate limits

API keys are never shown again after creation.

---

## 13. Telemetry

Telemetry shows how products are used in the field.

Admins can:
- View raw telemetry data
- Filter by product, version, license
- Inspect JSON payloads

Malformed telemetry is stored and flagged, not discarded.

---

## 14. Logs vs Audit Trails

### Logs
- Operational
- API calls
- Failures
- Jobs
- Auto-purged based on retention settings

### Audit Trails
- Immutable
- Append-only
- Cannot be deleted
- Track:
  - Before & after values
  - Actor
  - Request ID

Admins can **view**, not modify, audit trails.

---

## 15. Email Templates

Admins can manage email templates used for:
- License issuance
- Assignment notifications

Features:
- HTML & text versions
- Variable placeholders
- Preview support

---

## 16. Dashboard Widgets

Widgets visualize telemetry data.

Admins can:
- Create widgets
- Choose chart types
- Configure axes & filters
- Reorder widgets via drag & drop

Widgets are environment-aware.

---

## 17. Settings

### 17.1 UI Settings
- Brand name
- Date & time formats
- Pagination defaults

### 17.2 API Settings
- Response signing method
- Cryptographic algorithms
- Accepted user agents

### 17.3 Storage (S3)
- Bucket configuration
- Credentials
- Test connection

### 17.4 Data Retention
- Auto-purge intervals:
  - 1, 3, 6, 9, 12 months
- Applies only to logs & telemetry

Audit trails are never purged.

---

## 18. Background Jobs Visibility

Admins can monitor:
- Queued jobs
- Processing jobs
- Failed jobs

Jobs include:
- Bulk generation
- Emails
- Telemetry processing
- Webhooks

---

## 19. Profile & Security

Admins can:
- Update profile details
- Change password
- Enable/disable 2FA
- View recent login activity

---

## 20. Safety & UX Rules

- All deletes require confirmation
- Create/Edit always on separate pages
- UUID-based routing everywhere
- Pagination on all tables
- Bulk actions guarded by confirmation
- Clear “Danger Zone” sections

---

## 21. Summary

The Admin Portal provides:
- Full governance
- Security controls
- Compliance visibility
- Operational insight

It is intentionally powerful, explicit, and auditable.

---

END OF ADMIN PORTAL USER GUIDE
