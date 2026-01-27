---
title: Background Jobs
weight: 150
---

The Background Jobs page provides real-time visibility into the platform's asynchronous task processing system. This is where long-running or high-volume tasks are managed to ensure optimal system performance.

---

## What Is This Page?

Background Jobs are tasks that run in the "background" to avoid slowing down the user interface. Common examples include sending emails, processing telemetry data, sync operations (like Envato), and bulk license generation. This page allows you to monitor the health of these queues and troubleshoot any issues that arise.

---

## Dashboard Overview

### 1. Job Statistics
At the top of the page, three key metrics provide a snapshot of system health:
- **Running / Queued**: The total number of tasks currently being processed or waiting to start.
- **Failed Jobs**: The number of tasks that encountered an error and could not complete.
- **Active Queues**: The number of independent processing lanes (e.g., `default`, `high`, `emails`) currently in use.

### 2. Active Jobs
A list of the **last 10 active tasks** showing:
- **Status**: Visual indicators for `Processing` (currently running) or `Queued` (waiting for an available worker).
- **Attempts**: How many times the system has tried to run the job.
- **Timing**: Relative timestamps showing when the job was created.

---

## Managing Failed Jobs

When a task fails (e.g., due to a temporary network timeout or an invalid API key), it is moved to the **Failed Jobs** section for intervention.

### Interstitial Diagnostics
- **Exception Logs**: The table displays a truncated version of the error message. Hover over the text to see the full stack trace for deep troubleshooting.
- **Connection Details**: Identifies which driver (e.g., `redis`, `database`) was used for the task.

### Recovery Actions
- **Retry Job**: Click the "Retry" button to move a failed task back into the main queue. The system will attempt to execute it again starting with 0 attempts.
- **Delete Job**: If a task is no longer relevant or the error cannot be fixed, use the "Delete" action to permanently remove it from the failure log.

---

## Common Background Tasks

| Task Category | Description |
| :--- | :--- |
| **Email Delivery** | All outbound system emails (2FA codes, license keys, alerts). |
| **Telemetry** | Processing incoming hardware fingerprints and usage data from SDKs. |
| **Webhooks** | Sending notification payloads to third-party URLs. |
| **Bulk Operations** | Generating hundreds of license keys or exporting large datasets. |
| **Sync Jobs** | Periodically pulling data from Envato or other external marketplaces. |

---

## Troubleshooting

- **Large Number of Queued Jobs**: If jobs are piling up but not processing, ensure that your **Queue Worker** (typically handled via `php artisan queue:work`) is running on the server.
- **Repeating Failures**: If a job fails immediately after a retry, check the **Exception** column for specific error details. Common causes include expired API tokens or disconnected third-party services.
- **Empty Active List**: The active list only shows pending or currently processing tasks. If your system is idle, this list will be empty—this usually indicates healthy, fast-moving queues.

---

## Related Pages

- [Logs]({{< ref "/../../docs/docs/admin-portal/logs" >}}) - Check for system-level errors associated with job failures.
- [Settings]({{< ref "/../../docs/docs/admin-portal/settings" >}}) - Configure timeout values and queue connections.
- [Email Templates]({{< ref "/../../docs/docs/admin-portal/email-templates" >}}) - Manage the content of queued email jobs.
