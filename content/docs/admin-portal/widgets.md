---
title: Dashboard Widgets
weight: 130
---



![Admin Portal Dashboard Widgets Screenshot](placeholder-widgets-dashboard-overview.png)
*Screenshot of the Dashboard Widgets management page*

---

## What Is This Page?

The **Dashboard Widgets** page allows you to customize the data visualizations displayed on your main dashboard. Create, configure, and reorder charts that monitor everything from active licenses to specific telemetry patterns.

---

## When to Use This Page

* **Personalize your view** — Choose which metrics are most important for your day-to-day work
* **Create custom analytics** — Build charts based on specific telemetry groups or flags
* **Organize the dashboard** — Drag and drop widgets to change their layout
* **Product-specific monitoring** — Create widgets that only show data for a single product
* **Team alignment** — Enable or disable global widgets for all administrators

---

## What You Can Do Here

### 1. View & Manage Widgets

The management table provides an overview of all available widget configurations:

| Column | Description |
|--------|-------------|
| **Name** | The title of the widget as seen on the dashboard |
| **Scope** | **Global** (system-wide) or **Product** (specific to one software) |
| **Chart Type** | Line, Bar, Pie, or Number |
| **Width** | How many columns the widget occupies (out of 12) |
| **Status** | **Enabled** widgets are available for display |
| **Actions** | Edit, Delete, or toggle dashboard visibility |

### 2. Create/Edit Widget

Click **"Create Widget"** or **Edit** to configure a visualization:

* **Name:** A clear title for the widget.
* **Scope:**
  * **Global:** Aggregates data across the entire environment.
  * **Product:** Filters data to a specific product.
* **Chart Type:**
  * **Number:** A single large KPI (e.g., "Total Active Licenses").
  * **Line/Bar:** Best for trends over time.
  * **Pie:** Best for comparing distributions (e.g., "Version Breakdown").
* **Width:** Choose from 3 (quarter width) to 12 (full width).
* **Telemetry Group:** (Optional) Filter by a specific SDK telemetry group.
* **X/Y Axis:** Choose which data fields to plot.

### 3. Reordering (Drag & Drop)

Use the **Grip Icon** (⋮⋮) on the left side of any row to drag widgets into your preferred order. The order saved here dictates the sequence in which widgets appear on the main dashboard.

### 4. Personal Dashboard Toggle

Click the **"Personal Pin"** icon to add or remove a specific widget from *your* personal dashboard view without affecting other administrators.

---

## Common Workflows

### Workflow 1: Creating a "Piracy Watch" Widget

**Goal:** Create a 1/2 width bar chart showing flagged telemetry for your main product.

**Steps:**
1. Click **Create Widget**.
2. Name it "Piracy Alerts - [Product Name]".
3. Set **Scope:** "Product".
4. Select your product.
5. Set **Chart Type:** "Bar".
6. Set **Width:** "6".
7. Under **Telemetry Flags**, select "Flagged".
8. **Save**.
9. Go to your [Dashboard]({{< ref "/docs/admin-portal/dashboard" >}}) to see the new chart.

### Workflow 2: Optimizing Dashboard Layout

**Goal:** Move your most important 12-column line chart to the very top.

**Steps:**
1. Go to **Dashboard Widgets**.
2. Find the widget in the table.
3. Click and hold the **Grip Icon**.
4. Drag it to the top of the list.
5. Wait for the "Order updated" notification.
6. Refresh your dashboard to see the change.

---

## Troubleshooting

**Problem:** Widget exists in management but isn't on my dashboard.

**Solution:**
1. Check the **Status** column — it must be "Enabled".
2. Check the **Personal Pin** — you may need to add it to your specific user view.
3. Ensure the **Environment** matches (e.g., Staging widgets won't show on Production dashboard).

**Problem:** Chart shows "No Data".

**Solution:**
- Verify the **Telemetry Group** name matches exactly what is sent by the SDK.
- Check if the **Filters** are too restrictive.
- Ensure [Telemetry]({{< ref "/docs/admin-portal/telemetry" >}}) is actually being received for that product.

---

## Related Pages

* [Dashboard]({{< ref "/docs/admin-portal/dashboard" >}}) — View your configured widgets in action
* [Telemetry]({{< ref "/docs/admin-portal/telemetry" >}}) — Sources for custom widget data
* [Products]({{< ref "/docs/admin-portal/products" >}}) — Map widgets to specific software assets

---

## How to Access

**Navigation:** Admin Portal → **Widgets**
**URL:** `/admin/widgets`

**Permission Required:** Admin or higher role
