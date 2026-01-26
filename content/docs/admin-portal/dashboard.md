---
title: Dashboard
weight: 10
---

# Dashboard

![Admin Portal Dashboard Screenshot](placeholder-dashboard-overview.png)
*Screenshot will be added showing the main interface*

---

## What Is This Page?

The Dashboard is your command center for the entire license management platform. It provides a comprehensive, real-time operational overview with KPIs, activity feeds, and customizable widgets.

---

## When to Use This Page

Use the dashboard as your starting point each day to quickly assess system health, monitor key metrics, identify issues, and get an at-a-glance view of platform performance. It's perfect for morning reviews, quick status checks, or monitoring during critical periods.

---

## Key Features

- Real-time KPI cards showing critical metrics
- Activity feed with recent system events
- Customizable telemetry widgets
- Quick action buttons for common tasks
- Environment-aware data display

---

## Detailed Guide

### KPI Cards

Display critical metrics that update in real-time. These cards give you immediate insight into platform health.

![KPI Cards Screenshot](placeholder-dashboard-kpi-cards.png)
*Screenshot will be added*

#### What This Shows

- **Total Products**: Number of products configured in the system
- **Active Licenses**: Licenses currently in active state (excludes expired, suspended, revoked)
- **Total Activations**: All device/domain activations across all licenses
- **Activations Today**: New activations created today
- **Failed Verifications**: License verification failures (potential piracy indicator)
- **Revenue Metrics**: Optional financial data if configured

#### 💡 Tips & Tricks

- Watch for sudden spikes in failed verifications - may indicate piracy attempts
- Compare activations today vs. yesterday to spot trends
- Use KPIs to quickly identify if immediate action is needed
- Click any KPI card to drill down into detailed data

---

### Activity Feed

Real-time stream of important events happening across the platform.

![Activity Feed Screenshot](placeholder-dashboard-activity-feed.png)
*Screenshot will be added*

#### What This Shows

- Recent license activations with product and customer info
- License assignments to customers
- Product updates and configuration changes
- Contract activity and quota usage
- System alerts and warnings

#### 💡 Tips & Tricks

- Use the activity feed to spot unusual patterns or suspicious behavior
- Filter by product or customer to focus on specific areas
- Click any activity item to view full details
- Activity feed shows last 50 events by default

---

### Telemetry Widgets

Customizable data visualizations that you can configure, reorder, and personalize for your workflow.

![Telemetry Widgets Screenshot](placeholder-dashboard-telemetry-widgets.png)
*Screenshot will be added*

#### What This Shows

- Product usage trends over time
- Activation patterns by geography
- License expiration timelines
- Custom metrics you configure
- Environment-specific data

#### 💡 Tips & Tricks

- Drag and drop widgets to reorder based on priority
- Create separate widgets for different products
- Use filters to focus on specific time ranges
- Widgets auto-refresh - set refresh intervals in widget settings
- Export widget data for external analysis

---

## Common Tasks

Here are the most frequent operations you'll perform on this page:

1. Check morning metrics to assess overnight activity
2. Monitor failed verifications for potential issues
3. Review recent activations for unusual patterns
4. Quick access to frequently used admin functions
5. Spot trends in product usage and adoption

---

## ✅ Best Practices

- Start each day by reviewing the dashboard
- Set up widgets that matter most to your role
- Configure alerts for critical metrics
- Use the dashboard on a second monitor for continuous monitoring
- Customize KPI thresholds based on your business needs

---

## ❗ Troubleshooting

### KPI cards not updating

**Solution**: Check your internet connection. Refresh the page (F5). Clear browser cache if issue persists.

### Widgets showing no data

**Solution**: Verify you have telemetry enabled in Settings. Check that products are sending telemetry data. Confirm date range filter is appropriate.

### Activity feed is empty

**Solution**: If system is new, this is normal. If established system, check that logging is enabled in Settings > Logging.

---

## How to Access

1. Log in to the Admin Portal with your admin credentials
2. Click **Dashboard** in the main navigation menu
3. The page will load showing the main interface

**Keyboard Shortcut**: Press `Ctrl+K` (Windows) or `Cmd+K` (Mac) to open Global Search, then type the page name.

---

## Related Pages

- [Dashboard](../dashboard) - Main overview and KPIs
- [Settings](../settings) - System configuration
- [Profile](../profile) - Your admin profile and security
