# Admin Portal User Guide

![Admin Portal Placeholder Image](PLACEHOLDER_FOR_IMAGE)

---

## Purpose
The **Admin Portal** is the control plane of the License Management Platform. It is used to:
- Configure products and licensing rules
- Govern license creation and lifecycle
- Manage enterprise contracts and resellers
- Monitor activations, telemetry, logs, and audits
- Control security, storage, and system-wide settings

> The Admin Portal is not accessible to customers and must never be confused with the Client Self-Service Portal.

---

## Admin Roles & Access Control

### Admin User Types
- **Super Admin**: Full system access, security, keys, disaster recovery
- **Admin**: Full product & license management
- **Operator**: Day-to-day operations, limited destructive actions
- **Viewer**: Read-only access

All admin actions are audited.

---

### Authentication & Security
- Email + password login
- Optional Magic Link
- Two-Factor Authentication (TOTP)
- Session-based authentication
- Automatic session expiry

> Admins are never authenticated via API keys.
