---
title: Support Tickets
weight: 70
---

![Client Portal Support Tickets Screenshot](placeholder-client-tickets.png)
*Screenshot of the Support Tickets page in the customer portal showing active tickets and the ability to create new support requests*

---

## What Is This Page?

The **Support Tickets** page is your direct communication channel with the support team. Create support requests, track their progress, and receive responses—all from within your customer portal. No need for external email or helpdesk systems.

**What You Can Do:**
* **Create support tickets** for license issues, technical problems, or general questions
* **Track ticket status** and see when your issue is being worked on
* **Reply to support team** responses directly in the portal
* **View ticket history** of all your previous support requests
* **Upload attachments** like screenshots or log files to help troubleshooting
* **Receive email notifications** when the support team responds

---

## When to Use This Page

Create a support ticket when you:

* **Cannot activate a license** — Activation errors or limit reached
* **Have license validation issues** — License not working in your application
* **Need technical help** — SDK integration, API questions, implementation support
* **Have billing questions** — Payment issues, invoices, subscription changes
* **Want to report a bug** — Found an issue with the platform or license system
* **Have a feature request** — Suggest improvements or new functionality
* **Need general assistance** — Any questions about your licenses or account

💡 **Tip:** Before creating a ticket, check the [Documentation]({{< ref "/docs" >}}) and [FAQ](#common-questions) sections—you might find an instant answer!

---

## What You Can Do Here

### 1. View Your Tickets

The main page displays all your support tickets:

| Column | What It Means |
|--------|---------------|
| **Ticket #** | Unique identifier (e.g., TICK-1001) |
| **Subject** | Brief description of your issue |
| **Status** | Current state: Open, In Progress, Waiting for You, Resolved, Closed |
| **Priority** | How urgent: Low, Normal, High, Critical |
| **Category** | Type: Technical, Billing, License, General |
| **Created** | When you submitted the ticket |
| **Last Updated** | Most recent activity (your reply or support response) |

**Status Meanings:**
* **Open** — Support team has received your ticket and will respond soon
* **In Progress** — Team member is actively working on your issue
* **Waiting for You** — Support has replied and is waiting for your response
* **Resolved** — Issue has been fixed; ticket will auto-close in 7 days if no reply
* **Closed** — Issue completed and archived

### 2. Create a New Ticket

Click the **Create Ticket** button to open the support request form:

**Required Information:**
* **Subject** — Short, clear description (e.g., "Cannot activate license XXXXX-XXXXX")
* **Category** — Choose the type of issue:
  * **Technical Support** — Activation problems, integration help, SDK questions
  * **Billing** — Payment issues, invoice requests
  * **License Issues** — Key not working, activation limits
  * **General Inquiry** — Other questions
* **Priority** — Select urgency:
  * **Low** — Non-urgent question or minor issue
  * **Normal** — Standard support request (default)
  * **High** — Major problem affecting your work
  * **Critical** — Service completely down or unable to use licenses
* **Description** — Detailed explanation of your issue

**Optional Information:**
* **License Key** — Enter the affected license (if relevant)
* **Attachments** — Upload screenshots, error logs, or configuration files (max 10 MB per file)

**Tips for Faster Resolution:**
* Be specific about the error or problem
* Include error messages exactly as they appear
* Mention what you've already tried
* Specify your environment (Windows/Mac/Linux, SDK version, etc.)
* Attach relevant screenshots or logs

**Example of a Good Ticket:**
```
Subject: Activation Error: "Limit Reached" on License XXXXX-12345

Category: Technical Support
Priority: High

Description:
I'm trying to activate my license key XXXXX-XXXXX-XXXXX-12345 
on my new computer (Windows 11), but I'm getting an error: 
"Activation limit reached (5/5)".

I previously used this license on 3 machines:
- Office desktop (still in use)
- Home laptop (still in use)  
- Old laptop (no longer using, can be deactivated)
- Two test VMs (can be deactivated)

Can you please help deactivate the test machines so I can 
activate on my new computer?

Attachment: error-screenshot.png
```

### 3. Reply to a Ticket

When the support team responds, you'll receive an email notification. To reply:

**Option 1: Reply in Portal**
1. Log into your portal
2. Click on the ticket from your tickets list
3. Read the support team's response
4. Type your reply in the message box at the bottom
5. Click **Send Reply**

**Option 2: Reply via Email**
1. Open the notification email
2. Click **Reply** in your email client
3. Type your response
4. Send the email
5. Your reply automatically appears in the ticket

**Tips for Effective Replies:**
* Answer all questions from support
* Provide requested information promptly
* Test suggested solutions and report results
* Keep replies in the same ticket thread (don't create new tickets for the same issue)

### 4. Track Ticket Progress

Monitor your ticket's journey:

**Timeline View:**
Each ticket shows a complete activity timeline:
* When you created the ticket
* When support first responded
* All back-and-forth messages
* Status changes
* Resolution and closing

**Status Updates:**
Watch the status badge to see progress:
* **Open** (Blue) → Just submitted
* **In Progress** (Yellow) → Being worked on
* **Waiting for You** (Orange) → Your turn to respond
* **Resolved** (Green) → Issue fixed
* **Closed** (Gray) → Completed

**Email Notifications:**
You'll receive emails when:
* Ticket is assigned to a support agent
* Support team replies
* Ticket status changes
* Issue is resolved
* Ticket is closed

### 5. Reopen a Closed Ticket

If the issue returns after a ticket is closed:

1. Open the closed ticket
2. Click **Reopen Ticket**
3. Explain that the issue has returned
4. Describe what happened
5. Ticket status changes back to "Open"

**Note:** You can only reopen tickets that were closed within the last 30 days.

### 6. Filter and Search Your Tickets

**Filter Options:**
* **Status** — View only Open, Resolved, or Closed tickets
* **Category** — Filter by Technical, Billing, etc.
* **Date Range** — Tickets created in a specific period

**Search:**
* Search by ticket number (TICK-1001)
* Search by subject keywords
* Search in message content

### 7. View Related License Information

When you mention a license key in your ticket, the system automatically:
* Displays license details in the sidebar
* Shows activation count and status
* Links to activation history
* Provides context to support team

This helps the support team understand your issue faster without asking for basic license information.

---

## Ticket Priority Guidelines

Choose the right priority to help support team respond appropriately:

| Priority | Use When | Typical Response Time |
|----------|----------|----------------------|
| **Critical** | Cannot validate any licenses, service completely down, business impact | 1 hour |
| **High** | Major feature broken, cannot activate licenses, blocking your work | 4 hours |
| **Normal** | Standard issues, questions, or problems with workarounds | 24 hours |
| **Low** | General questions, minor issues, feature requests | 3-5 days |

⚠️ **Important:** Choosing "Critical" for non-urgent issues may delay response to actual emergencies. Be honest about urgency.

---

## Common Questions

### How long until I get a response?

Response times depend on ticket priority:
* **Critical:** 1 hour (24/7)
* **High:** 4 hours (business hours)
* **Normal:** 24 hours
* **Low:** 3-5 days

**Business Hours:** Monday-Friday, 9 AM - 6 PM (your account timezone)

### Can I create tickets via email?

Yes! Send email to: **support@[yourdomain].com**
* Include your license key in the subject or body
* Attach any relevant screenshots or logs
* A ticket will be automatically created in the system

### How many tickets can I create?

There's no limit. Create as many tickets as you need. However, for the same issue, please reply to the existing ticket rather than creating multiple tickets.

### Can I attach files to tickets?

Yes, you can attach:
* Screenshots (PNG, JPG, GIF)
* Log files (TXT, LOG)
* Configuration files (JSON, XML, YML)
* Error reports (TXT, PDF)

**Limits:**
* Maximum 10 MB per file
* Up to 5 files per ticket
* No executable files (.exe, .dll) for security reasons

### What if I don't receive email notifications?

1. Check your spam/junk folder
2. Add support email to your contacts
3. Verify email address in [Profile Settings]({{< ref "/docs/client-portal/profile" >}})
4. Create a ticket asking to verify notification settings

### Can I call for support?

Currently, support is provided via the ticket system and email only. This allows us to:
* Track all requests and history
* Provide detailed technical responses
* Attach files and code examples
* Maintain record for future reference

For urgent issues, mark your ticket as **Critical** priority for fastest response.

### How do I escalate an urgent issue?

If your ticket is urgent:
1. Set priority to **High** or **Critical** when creating
2. Clearly explain the business impact
3. Provide detailed error information
4. If no response within target time, reply to bump priority

---

## Tips for Faster Resolution

✅ **Do:**
* Provide detailed error messages
* Include screenshots showing the problem
* Specify your environment (OS, SDK version, etc.)
* List what you've already tried
* Respond promptly to support questions
* Test suggested solutions and report results

❌ **Don't:**
* Create multiple tickets for the same issue
* Mark non-urgent tickets as Critical
* Provide vague descriptions ("it doesn't work")
* Ignore support team's questions
* Reply with just "ok" or "thanks" without testing
* Share your license keys publicly or in screenshots

---

## Self-Service Options

Before creating a ticket, try these resources:

**Documentation:**
* [License Activation Guide]({{< ref "/docs/client-portal/activations" >}})
* [Download Center]({{< ref "/docs/client-portal/downloads" >}})
* [Account Settings]({{< ref "/docs/client-portal/settings" >}})

**Common Issues:**
* **"Activation limit reached"** → [Deactivate unused installations]({{< ref "/docs/client-portal/activations#deactivate" >}})
* **"License expired"** → Check expiration date in [My Licenses]({{< ref "/docs/client-portal/licenses" >}})
* **"Invalid license key"** → Verify you copied the complete key correctly
* **"Product not found"** → Ensure you're using the correct API endpoint

---

## Ticket Management Best Practices

### For Quick Resolution:
1. **Be Specific** — "Cannot activate on Windows 11" is better than "not working"
2. **Include Context** — Environment, version, exact error message
3. **One Issue Per Ticket** — Don't combine multiple problems
4. **Respond Quickly** — Reply within 48 hours to keep ticket active
5. **Test Solutions** — Try suggestions and report results

### For Better Communication:
* Use the ticket thread for related follow-ups
* Mark resolved issues as "can be closed"
* Thank support staff for helpful responses
* Provide feedback on solutions

---

## Privacy and Security

**Your Data:**
* Ticket content is private—only you and support team can see it
* Tickets are encrypted in transit (HTTPS)
* Attachments are securely stored
* Support team follows strict confidentiality policies

**Your License Keys:**
* You can safely mention license keys in tickets
* Support team needs them to investigate issues
* Never share keys in public forums or social media

**Account Security:**
* Tickets are linked to your authenticated account
* Support may ask security questions for sensitive requests
* You can enable 2FA for additional security

---

## Technical Details

* **Ticket Numbers:** Sequential format TICK-XXXX
* **Storage:** All tickets preserved indefinitely
* **Attachments:** Stored securely, deleted if ticket deleted
* **Email Integration:** Two-way sync between portal and email
* **Notifications:** Instant via email, optional SMS (if configured)

---

## Related Pages

* [My Licenses]({{< ref "/docs/client-portal/licenses" >}}) — View and manage your licenses
* [Activations]({{< ref "/docs/client-portal/activations" >}}) — Manage license activations
* [Profile Settings]({{< ref "/docs/client-portal/profile" >}}) — Update notification preferences
* [Downloads]({{< ref "/docs/client-portal/downloads" >}}) — Access software and documentation

---

## How to Access

**Navigation:** Customer Portal → **Support** → **Tickets**
**URL:** `/customer/tickets`

**Quick Access:** Use the **Help** button in the top navigation from any page to create a ticket instantly.
