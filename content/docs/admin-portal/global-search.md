---
title: Global Search
weight: 220
---

Global Search is a powerful tool designed to help administrators navigate the platform efficiently by providing instant access to critical data from anywhere in the Admin Portal.

---

## What Is This Page?

Global Search is accessible via the search bar in the top header or through the global keyboard shortcut. It performs a real-time, environment-aware search across multiple core entities, including Customers, Licenses, and Products.

---

## Key Features

### 1. Unified Search Interface
Instead of navigating to individual departments, you can search for:
- **Customers**: Search by Name or Email address.
- **Licenses**: Search by License Key (supports partial matches).
- **Products**: Search by Product Name or Description.

### 2. Efficiency Tools
- **Keyboard Shortcut**: Press `⌘K` (Mac) or `Ctrl+K` (Windows/Linux) to immediately focus the search bar from any page.
- **Debounced Results**: Results filter as you type (after a 300ms pause) to ensure a smooth, lag-free experience.
- **Instant Preview**: View the most relevant records in a categorized dropdown without leaving your current page.

---

## How to Use Global Search

1. **Activate**: Click the search input in the header or use the `⌘K` / `Ctrl+K` shortcut.
2. **Type**: Enter at least **2 characters** to begin seeing results.
3. **Navigate**: 
    - Use the **Up/Down** arrow keys to highlight a result (or your mouse).
    - Press **Enter** to navigate directly to the selected record.
    - Press **ESC** to clear search results and close the dropdown.
4. **Environment Scoping**: Results are automatically filtered based on your current active environment (e.g., you will only see "Production" licenses while in the Production dashboard).

---

## Troubleshooting

- **No Results Found**: 
    - Ensure you have typed at least 2 characters.
    - Check if the record exists in the **current environment**. A customer created in "Development" will not appear in "Production" searches.
    - Verify your search spelling; searches are based on "contains" logic (e.g., searching "test" will find "test-user@example.com").
- **Search Bar Not Opening**: Ensure no other application or browser extension is overriding the `⌘K` / `Ctrl+K` shortcut. You can always click the search bar manually.

---

## Related Pages

- [Dashboard]({{< ref "/docs/admin-portal/dashboard" >}}) - System status summary.
- [Licenses]({{< ref "/docs/admin-portal/licenses" >}}) - Manage full license lifecycle.
- [Customers]({{< ref "/docs/admin-portal/customers" >}}) - View detailed customer history.
