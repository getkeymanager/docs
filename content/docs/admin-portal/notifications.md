---
title: Notifications
weight: 190
---

The Notifications page provides a centralized hub for managing system alerts, activity updates, and administrative tasks. It ensures that system administrators are promptly informed about critical events and routine operations within the platform.

---

## What Is This Page?

The Notifications page displays a chronological list of events relevant to the logged-in administrator. These notifications can range from system alerts (like background job failures) to administrative actions (like license assignments or activations) and automated reminders.

---

## Key Features

### 1. Unified Inbox
View all system notifications in a single, paginated list. Each notification includes:
- **Status Indicator**: Unread notifications are highlighted with a distinct background and a status dot.
- **Title & Description**: Clear, concise information about the event.
- **Actionable Links**: Many notifications include a direct link to the relevant record (e.g., clicking a "License Activated" notification takes you directly to that license).
- **Time Offsets**: Timestamps are displayed in relative format (e.g., "5 minutes ago") for immediate context.

### 2. Filtering & Organization
Quickly find specific types of alerts using the built-in filters:
- **All**: View your entire notification history.
- **Unread**: Focus on new alerts that require attention.
- **Read**: Reference past notifications that have already been acknowledged.

### 3. Bulk Actions
Manage your inbox efficiency with bulk operations:
- **Mark All as Read**: Instantly clear your unread count once you've reviewed your latest alerts.
- **Individual Read Status**: Toggle the read status for specific items to keep your workspace organized.

---

## Common Notification Types

| Type | Description |
| :--- | :--- |
| **System Alerts** | Critical failures in background jobs or infrastructure issues. |
| **License Activity** | Notifications for new assignments, activations, or revocations. |
| **Security Alerts** | Login attempts from new locations or 2FA changes. |
| **Telemetry Events** | Alerts triggered by forensic flags or suspicious hardware fingerprints. |
| **Integrations** | Webhook delivery failures or API key usage milestones. |

---

## How to Access

1. Log in to the **Admin Portal**.
2. Click the **Notification Bell** icon in the top navigation bar to view a quick summary.
3. Click **"View All Notifications"** at the bottom of the dropdown, or select **Notifications** from the sidebar menu to access the full page.

---

## Troubleshooting

- **Missing Notifications**: Notifications are scoped per admin. You will only see alerts relevant to your role or specific assignments.
- **Email Delivery**: If you are not receiving email mirrors for notifications, verify your email address in the [Profile]({{< ref "/../docs/docs/admin-portal/profile" >}}) page and check your system's SMTP configuration.
- **Real-time Updates**: The notification counter in the header updates automatically via WebSockets/Livewire events. If it seems stuck, a page refresh will sync the state.

---

## Related Pages

- [Dashboard]({{< ref "/../docs/docs/admin-portal/dashboard" >}}) - Summary of system health.
- [Profile]({{< ref "/../docs/docs/admin-portal/profile" >}}) - Manage your personal notification preferences.
- [Logs]({{< ref "/../docs/docs/admin-portal/logs" >}}) - Deep dive into system-level events and errors.
