---
title: Data Retention Policies
weight: 180
---

![Admin Portal Data Retention Policies Screenshot](placeholder-retention-overview.png)
*Screenshot of the Retention Policies page with purge statistics*

---

## What Is This Page?

The **Retention Policies** page allows you to manage the automatic cleanup of operational data. Configure how long the system should keep logs, telemetry, and background job data before they are permanently deleted to optimize storage and maintain performance.

---

## When to Use This Page

* **Comply with privacy regulations** — Set data storage limits for GDPR or company policies
* **Optimize database performance** — Prevent tables from growing too large
* **Manage storage costs** — Reduce disk usage by purging old telemetry
* **Auto-cleanup** — Automate the deletion of temporary operational data
* **Environmental hygiene** — Keep development or staging environments lean

---

## What You Can Do Here

### 1. View Retention Policies

The dashboard shows an overview of all active purging rules and their current impact.

| Column | Description |
|--------|-------------|
| **Entity Type** | The type of data being managed (Logs, Telemetry, etc.) |
| **Retention Days** | How many days of data are kept before purging |
| **Cutoff Date** | The exact date before which all records will be deleted |
| **Status** | Whether the policy is active and if a purge is pending |
| **Actions** | Edit or delete the policy |

### 2. Purge Statistics

The top of the page displays summary cards for each managed entity:
* **Pending:** Number of records currently eligible for deletion.
* **Clean:** Indicates no records currently exceed the retention threshold.
* **Retention Level:** Displays the active policy duration for quick reference.

### 3. Preview Dry Run

Click **"Preview Dry Run"** to see exactly what would happen if the purge ran right now.
* Calculates records to be deleted across all policies.
* Does NOT delete any data.
* Useful for verifying impact before applying strict policies.

### 4. Create/Edit Policy

1. Click **"Create Policy"** or **Edit** on an existing one.
2. Select **Entity Type** (if creating new):
   * **System Logs** — Operational logs of admin actions and errors.
   * **Telemetry Records** — Usage data received from products.
   * **Webhook Deliveries** — History of outgoing webhook attempts.
   * **Job Execution Logs** — Records of background task results.
3. Set **Retention Days** (1 to 365 days).
4. Click **Save Policy**.

---

## Permanent Records (NEVER Purged)

To maintain platform integrity and legal compliance, the following data is **excluded** from auto-purge policies:

* **Audit Trails** — Complete, immutable history of state changes.
* **Licenses & Activations** — Core functional data required for product validation.
* **Products & Generators** — Configuration and logic definitions.
* **Customers & Contracts** — Relationships and entitlement records.

---

## Common Workflows

### Workflow 1: Implementing a 90-Day Log Policy

**Goal:** Keep system logs for exactly 3 months for security auditing, then delete to save space.

**Steps:**
1. Click **Create Policy**.
2. Select **Entity Type:** "System Logs".
3. Set **Retention Days:** "90".
4. Click **Save Policy**.
5. Click **Preview Dry Run** to see how many logs > 90 days old will be removed in the next cycle.

### Workflow 2: Aggressive Telemetry Cleanup for Staging

**Goal:** In development/staging, keep only the most recent usage data.

**Steps:**
1. Find the "Telemetry Records" policy.
2. Click **Edit**.
3. Change **Retention Days** to "7".
4. **Save**.
5. The system will now clear all telemetry older than one week on the next scheduled job.

---

## Troubleshooting

**Problem:** Can't change the Entity Type when editing.

**Solution:** For data integrity, the entity type is locked once a policy is created. To change it, **Delete** the existing policy and create a new one with the correct type.

**Problem:** Dry run shows 0 records even with old data.

**Solution:** Check the "Retention Days" value. If it is set higher than the oldest record (e.g., set to 365 but the platform has only existed for 30 days), no data will be eligible for purging.

---

## Technical Details

* **Scheduled Execution:** Purge jobs typically run once daily (usually at midnight).
* **Environment Isolation:** Policies are applied globally to the current environment only.
* **Irreversibility:** Once purged, data **cannot be recovered** unless you have an external database backup.

---

## Related Pages

* [System Logs]({{< ref "/../docs/docs/admin-portal/logs" >}}) — View the data being managed by these policies
* [Settings → Audit Trails]({{< ref "/../docs/docs/admin-portal/settings" >}}) — View the permanent history that is never purged
* [Background Jobs]({{< ref "/../docs/docs/admin-portal/background-jobs" >}}) — Monitor the status of the purge tasks

---

## How to Access

**Navigation:** Admin Portal → **Settings** → **Retention Policies**
**URL:** `/admin/retention-policies`

**Permission Required:** Super Admin role
