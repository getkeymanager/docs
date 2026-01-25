# Client / Customer Self-Service Portal User Guide  
## License Management Platform – v1.0

---

## 1. Purpose of the Client Portal

The **Client / Customer Self-Service Portal** is a secure interface designed for **end customers who own licenses**.

Its goals are to:
- Provide transparency into license ownership and usage
- Allow customers to manage their own activations
- Enable secure access to product downloads and updates
- Reduce dependency on support teams
- Maintain strict security and data isolation

The Client Portal is **not an admin interface** and does not allow system configuration.

---

## 2. Who Can Access the Client Portal

Client Portal users are:
- Customers who own one or more licenses
- Users explicitly invited or provisioned by the system (current or future)
- Authenticated via customer-specific authentication (not admin login)

Client Portal users are **completely isolated** from:
- Admin users
- Other customers
- Internal system configuration

---

## 3. Authentication & Security

### 3.1 Login Methods
- Email-based authentication
- Password or secure login link (depending on configuration)
- Session-based authentication

### 3.2 Security Characteristics
- No API key access
- No administrative permissions
- UUID-based routing only
- Strict session isolation

> Client Portal users can never authenticate as admins and cannot access admin routes.

---

## 4. Client Portal Navigation Overview

The Client Portal provides a focused and minimal navigation:

- Dashboard
- My Licenses
- Activations
- Downloads
- Changelog
- Profile & Security

All views are scoped strictly to the logged-in customer.

---

## 5. Dashboard

The Dashboard provides a **summary of license ownership**.

### Typical Dashboard Information
- Total licenses owned
- Active licenses
- Expired or suspended licenses
- Recent activation activity

The dashboard is informational only and does not allow configuration changes.

---

## 6. My Licenses

### 6.1 License List

Customers can view all licenses assigned to them.

Each license shows:
- License key (partially masked)
- Product name
- License status
- Expiry date
- Activation count
- Feature availability (if applicable)

### Supported License States (Read-Only)
- Assigned
- Active
- Suspended
- Expired
- Revoked

Customers cannot modify license state directly.

---

## 7. License Details & Explainability

Each license includes a detailed view explaining its current status.

### “Why Is My License Invalid?”

If a license is not usable, the portal explains:
- Current state
- Expiry reason
- Activation limit reached
- Hardware / domain mismatch
- Environment mismatch

This transparency reduces confusion and support requests.

---

## 8. Activations Management

Activations represent **devices, machines, or domains** where the product is installed.

### 8.1 Activation List

Customers can view:
- Activation identifier (HWID or domain)
- Activation status
- Last seen timestamp
- Product version (if available)

---

### 8.2 Deactivating an Activation

Customers may deactivate their own activations.

Rules:
- Deactivation requires confirmation
- Deactivation immediately invalidates that installation
- Deactivation does not delete the license

Typical use cases:
- Moving to a new device
- Reinstalling software
- Retiring old hardware

> Customers cannot activate new devices directly from the portal unless explicitly enabled by product rules.

---

## 9. Downloads & Updates

### 9.1 Available Downloads

Customers can access downloadable packages they are entitled to.

Access depends on:
- License validity
- License state
- Product access rules
- Time-based restrictions

### 9.2 Download Behavior

- Downloads are delivered via secure, time-limited links
- Links cannot be shared
- Files are verified server-side before access

Supported assets:
- Software packages
- Images
- Videos
- Documentation bundles

---

## 10. Changelog

The Changelog provides visibility into product updates.

### Features
- Version history
- Release dates
- Update summaries
- Detailed change descriptions

Changelog access:
- Is read-only
- May be enabled or disabled per product
- Is identical to the public changelog page (if enabled)

---

## 11. Feature Visibility & Entitlements

Some products may include **feature flags**.

Customers may:
- View which features are enabled for their license
- See limitations (e.g., seat count, usage caps)

Customers cannot modify feature flags.

---

## 12. Profile & Security

Customers can manage their own profile:

- Update name or contact information
- Change password (if applicable)
- View recent login activity

Security settings are limited to the customer’s own account.

---

## 13. Actions Customers Cannot Perform (Explicit)

For clarity, customers **cannot**:

- Create or modify products
- Generate license keys
- Modify license rules
- Change activation limits
- View telemetry of other customers
- Access logs or audit trails
- Access system settings
- Access admin dashboard

These restrictions are enforced at the service layer.

---

## 14. Data Privacy & Isolation Guarantees

The Client Portal enforces strict data isolation:

- Customers can only see data tied to their customer account
- No cross-customer access is possible
- Numeric internal IDs are never exposed
- UUIDs are used exclusively for routing

All access attempts are logged and monitored.

---

## 15. Offline & External Usage Notes

For offline or SDK-based usage:
- License validation rules are identical
- Portal visibility does not affect offline behavior
- Deactivations propagate to offline validation once connectivity resumes

---

## 16. Support & Escalation

If a customer cannot resolve an issue via the portal:
- They should contact the product vendor or administrator
- Certain actions (e.g., reassigning licenses) require admin intervention

---

## 17. Summary

The Client / Customer Self-Service Portal provides:
- Transparency into license ownership
- Control over activations
- Secure access to downloads
- Clear explanations of license status

It is intentionally **limited, secure, and customer-focused**, ensuring safety without sacrificing usability.

---

END OF CLIENT / CUSTOMER SELF-SERVICE PORTAL USER GUIDE
