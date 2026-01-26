---
title: Email Templates
weight: 120
---

The Email Templates page allows you to manage and customize the automated communications sent by the platform to both customers and administrators.

---

## What Is This Page?

Email Templates serve as the blueprints for situational messages triggered by system events, such as license issuance, credential resets, or security alerts. You can control the branding, content, and dynamic data displayed in every email sent from the platform.

---

## Key Features

### 1. Template Management
The main dashboard provides a high-level view of all configured templates:
- **Usage Statistics**: Track how many times a template has been sent (`Sent Count`).
- **Last Sent**: Monitor the last time a specific template was active.
- **Categorization**: Group templates by function (e.g., "Licenses", "Identity", "Admin") for easier management.

### 2. Customization & Logic
Templates support sophisticated formatting and dynamic content:
- **Dynamic Variables**: Use placeholders like `{{customer_name}}`, `{{license_key}}`, or `{{expiry_date}}` to personalize messages.
- **Markdown/HTML Support**: Design rich emails that match your brand's aesthetic.
- **Subject Line Customization**: Define unique subjects for every template to ensure high open rates.

### 3. Testing & Verification
Before going live with a new template, you can:
- **Seed Defaults**: Quickly populate your database with professionally written default templates for common scenarios.
- **Test Delivery**: Send a live test email to any address, including mock data for dynamic variables, to verify layout and rendering across different email clients.

---

## Managing Templates

### Creating or Editing
1. Click **Create Template** or select **Edit** from the actions menu of an existing template.
2. Define the **Slug**: This is the unique identifier used by the system to trigger this specific email (e.g., `license-issued`).
3. Set the **Category**: Help organize your inbox by grouping similar alerts.
4. Define **Variables**: Explicitly list the dynamic placeholders this template expects to receive.

### Seeding Default Templates
If you are setting up a new environment, click the **Seed Defaults** button in the header. This will automatically generate standard templates for:
- License Issuance
- Activation Confirmations
- 2FA Setup & Security Alerts
- Password Reset Requests

---

## Troubleshooting

- **Variables Not Replacing**: Ensure your variable names in the content match exactly with the variables defined in the "Variables" section of the form (case-sensitive). Use double curly braces `{{variable_name}}`.
- **Emails Not Sending**:
    - Verify that the template is **Enabled**.
    - Check the system's SMTP or Mail Driver configuration in the global [Settings](../settings).
    - Review the [Background Jobs](../background-jobs) queue to ensure email delivery tasks are completing successfully.
- **Styling Issues**: Different email clients (Gmail, Outlook) render HTML differently. Always use the **Test Email** feature to verify styling before enabling a template for Production.

---

## Related Pages

- [Settings](../settings) - Configure global mail drivers.
- [Logs](../logs) - Check for email delivery errors.
- [Background Jobs](../background-jobs) - Monitor the mail delivery queue.
