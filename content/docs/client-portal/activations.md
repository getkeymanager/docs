---
title: Activations
weight: 30
---



The Activations page allows you to manage the specific devices, domains, or machines currently authenticated using your licenses. It provides self-service tools to free up license slots without needing to contact support.

---

## What Is This Page?

Every time you enter a license key into your software, it creates an "Activation" tied to that specific hardware or domain. This page lists all such active connections across your entire license library, allowing for real-time management of your installation footprint.

---

## Key Features

### 1. Device Presence Tracking
For every activation, you can monitor the following data points:
- **Identifier**: The unique Hardware ID (HWID) or Domain name associated with the installation.
- **License Context**: Which license key and product are powering the activation (masked for security).
- **Activity Status**: The "Last Seen" timestamp indicates when the device last successfully communicated with the license server.

### 2. Remote Deactivation
If you reach your license's activation limit or wish to move your software to a new machine:
- **Self-Service Clearance**: You can remotely deactivate an existing installation with the click of a button.
- **Instant Slot Recovery**: Deactivating a device immediately frees up an activation slot on your license, allowing you to register a different device.
- **Safety Prompts**: All deactivations require a confirmation to prevent accidental outages.

### 3. Visibility & Search
Manage large numbers of activations effectively with:
- **Identifier Search**: Find a specific computer or website quickly.
- **Status Filtering**: View `Active`, `Deactivated`, or `Suspended` connections.
- **Device Type Icons**: Visual indicators help distinguish between Domain-based and Hardware-based activations.

---

## How to Access

1. Log in to the **Customer Portal**.
2. Click **Activations** in the sidebar navigation.

---

## Troubleshooting

- **Deactive Button Missing**: You can only deactivate installations that are currently in an `Active` status. If an activation is already deactivated or suspended, the action will be disabled.
- **Last Seen "Never"**: This usually means the software was registered but hasn't performed a "heartbeat" check-in since the initial setup. Ensure the device has internet connectivity.
- **Cannot Re-activate**: Once you deactivate a device from this portal, you must go through the "Activate" process within the software application itself to restore access.

---

## Important Note

**You cannot create new activations from this portal.** Activations are initiated only through the software application you are using. This portal is strictly for monitoring and **removing** existing activations.

---

## Related Pages

- [Dashboard]({{< ref "/../../docs/docs/client-portal/dashboard" >}}) - View total activation counts.
- [My Licenses]({{< ref "/../../docs/docs/client-portal/licenses" >}}) - Check the activation limits for each of your products.
