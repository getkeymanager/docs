---
title: Ticket Management
weight: 185
---

![Admin Portal Ticket Management Screenshot](placeholder-tickets-overview.png)
*Screenshot of the Ticket Management page showing the support ticket list with status, priority, and assignment filters*

---

## What Is This Page?

The **Ticket Management** page provides a complete support ticketing system built directly into the platform. Customers can create support tickets from their portal, and your team can manage, respond to, and resolve them—all without external helpdesk software.

**Key Benefits:**
* **Unified Platform** — No need for Zendesk, Freshdesk, or other external tools
* **License Context** — Tickets automatically include customer and license information
* **Team Collaboration** — Assign tickets to team members and track resolution status
* **Priority Management** — Categorize and prioritize support requests
* **Customer Portal Integration** — Customers create tickets directly from their dashboard

---

## When to Use This Page

* **Provide customer support** — Handle license issues, activation problems, and general inquiries
* **Track support requests** — Monitor open tickets and response times
* **Assign to team members** — Distribute support workload across your team
* **Manage priorities** — Escalate critical issues and organize by urgency
* **View ticket history** — Track all customer interactions in one place
* **Generate support reports** — Analyze ticket volume and resolution times

---

## What You Can Do Here

### 1. View All Tickets

The main table displays all support tickets with the following information:

| Column | Description |
|--------|-------------|
| **Ticket #** | Unique ticket identifier (e.g., TICK-1001) |
| **Subject** | Brief description of the issue |
| **Customer** | Customer name and email who created the ticket |
| **Status** | Current state: Open, In Progress, Waiting, Resolved, Closed |
| **Priority** | Urgency level: Low, Normal, High, Critical |
| **Assigned To** | Team member responsible for the ticket (or "Unassigned") |
| **Category** | Ticket type: Technical, Billing, License, General |
| **Created** | When the ticket was submitted |
| **Last Updated** | Most recent activity timestamp |
| **Actions** | View details, reply, or change status |

### 2. Filter Tickets

Use the filter bar to quickly find specific tickets:

**Available Filters:**
* **Status** — Open, In Progress, Waiting for Customer, Resolved, Closed
* **Priority** — Low, Normal, High, Critical
* **Assigned To** — Filter by team member or show unassigned tickets
* **Category** — Technical, Billing, License Issues, Feature Request, General
* **Date Range** — Created/updated within specific timeframe
* **Customer** — Show all tickets from a specific customer

**Quick Filters:**
* **My Tickets** — Show only tickets assigned to you
* **Unassigned** — Tickets waiting for assignment
* **Urgent** — High and Critical priority tickets
* **Needs Response** — Tickets awaiting team reply

### 3. Search Tickets

Use the search bar to find tickets by:
* Ticket number (TICK-1001)
* Subject keywords
* Customer name or email
* Response content

### 4. View Ticket Details

Click on any ticket to open the detail view showing:

**Ticket Information:**
* Full subject and description
* Customer details and contact information
* Related license keys (if mentioned)
* Attachments (screenshots, log files)
* Complete conversation thread
* Ticket timeline and status history

**Customer Context:**
* Customer's licenses and activation status
* Recent telemetry and usage data
* Purchase history and account status
* Previous tickets from this customer

### 5. Respond to Tickets

**Replying to a Customer:**
1. Open the ticket detail view
2. Scroll to the reply section
3. Type your response in the message editor
4. Optionally change ticket status (e.g., Open → In Progress)
5. Optionally change priority
6. Click **Send Reply**

**Reply Options:**
* **Send and Keep Open** — Reply but leave ticket in current status
* **Send and Mark Waiting** — Reply and mark as "Waiting for Customer"
* **Send and Resolve** — Reply and mark ticket as resolved
* **Internal Note** — Add a note visible only to team members

**Email Notifications:**
* Customers automatically receive email when you reply
* Email includes full response and link to view in their portal
* Customer can reply via email or through the portal

### 6. Assign Tickets

**Manual Assignment:**
1. Open the ticket
2. Click **Assign** dropdown
3. Select a team member
4. Team member receives notification

**Auto-Assignment (if enabled in Settings):**
* Round-robin distribution
* Based on team member availability
* By category or expertise
* Load balancing across team

### 7. Change Ticket Status

**Status Workflow:**
```
Open → In Progress → Waiting for Customer → Resolved → Closed
```

**Status Definitions:**
* **Open** — New ticket, not yet worked on
* **In Progress** — Team member actively working on the issue
* **Waiting for Customer** — Awaiting customer response or action
* **Resolved** — Issue fixed, awaiting customer confirmation
* **Closed** — Ticket completed and archived

**Status Actions:**
* Open → In Progress (when you start working)
* In Progress → Waiting (when you need customer info)
* Waiting → In Progress (when customer responds)
* In Progress → Resolved (when issue is fixed)
* Resolved → Closed (automatically after 7 days, or manually)
* Any status → Open (if issue reopens)

### 8. Set Priority Levels

**Priority Guidelines:**

| Priority | Use When | Response Time |
|----------|----------|---------------|
| **Critical** | Service completely down, cannot validate licenses, security breach | 1 hour |
| **High** | Major feature broken, multiple users affected, revenue impact | 4 hours |
| **Normal** | Standard issues, single user affected, workaround available | 24 hours |
| **Low** | Feature requests, minor bugs, documentation questions | 3-5 days |

**Changing Priority:**
1. Open the ticket
2. Click current priority badge
3. Select new priority level
4. Priority change is logged in ticket history

### 9. Add Internal Notes

Team members can add internal notes that customers cannot see:

1. Open ticket detail view
2. Click **Add Internal Note**
3. Type your note (troubleshooting steps, investigation findings, etc.)
4. Click **Save Note**

**Use Cases for Internal Notes:**
* Document troubleshooting steps
* Share context with other team members
* Record technical details or workarounds
* Track investigation progress
* Note customer communication preferences

### 10. Merge Duplicate Tickets

If a customer submits multiple tickets for the same issue:

1. Open one of the duplicate tickets
2. Click **Merge Tickets**
3. Select the ticket(s) to merge
4. Choose which ticket to keep as primary
5. Confirm merge

All responses and history are combined into the primary ticket.

---

## Ticket Categories

Configure ticket categories in **Settings → Ticket Management**:

**Default Categories:**
* **Technical Support** — Activation issues, integration help, SDK questions
* **Billing** — Payment problems, invoice requests, subscription changes
* **License Issues** — Key not working, activation limit reached, expiry questions
* **Feature Request** — Product enhancement suggestions
* **General Inquiry** — Questions about products, documentation, or platform

**Custom Categories:**
You can create custom categories specific to your products (e.g., "WordPress Plugin", "Mobile SDK", "Enterprise Contracts").

---

## Team Collaboration Features

### Ticket Assignment Rules

Configure in **Settings → Ticket Management → Assignment Rules**:

* **Auto-assign by category** — Route technical tickets to developers
* **Round-robin** — Distribute evenly across available team members
* **Skill-based routing** — Assign based on expertise tags
* **Load balancing** — Consider current ticket count per member

### Team Member Permissions

Control who can access tickets:

| Role | Permissions |
|------|-------------|
| **Super Admin** | Full access to all tickets, can delete tickets |
| **Admin** | Can view and respond to all tickets, cannot delete |
| **Support Agent** | Can view assigned tickets and unassigned tickets |
| **Developer** | Can view technical category tickets only |

Configure roles in **Settings → Admin Users**.

### Notification Settings

Control email notifications per team member:

* **New Ticket Created** — Alert all available agents
* **Ticket Assigned to Me** — Personal assignment notification
* **Customer Replied** — Notify assigned agent
* **Priority Changed** — Alert if ticket escalated
* **Ticket Mention** — Notify when @mentioned in responses

---

## Customer Self-Service Options

Reduce ticket volume by enabling self-service features:

**Knowledge Base Integration:**
* Link to documentation articles
* Show relevant help docs when customer creates ticket
* Suggest solutions before ticket submission

**FAQ System:**
* Create category-specific FAQs
* Display on ticket creation page
* Update based on common support requests

**Canned Responses:**
* Pre-written responses for common issues
* Insert with keyboard shortcuts
* Customizable per category

Configure in **Settings → Ticket Management → Self-Service**.

---

## Common Workflows

### Workflow 1: Handling a New License Activation Issue

**Scenario:** Customer reports they cannot activate their license key.

**Steps:**
1. Open the ticket from "Unassigned" queue
2. Review ticket details and click on mentioned license key
3. System opens license detail in split view
4. Check activation count (e.g., 5/5 used)
5. Add internal note: "Activation limit reached"
6. Assign ticket to yourself
7. Change status to "In Progress"
8. Reply: "I can see your activation limit is reached. I've increased it to 10. Please try again."
9. Update license activation limit in split view
10. Change ticket status to "Resolved"

**Result:** Issue resolved without leaving the ticket interface, all context preserved.

### Workflow 2: Escalating a Critical Issue

**Scenario:** Multiple customers report validation API is down.

**Steps:**
1. Filter tickets by **Status: Open** and **Priority: Critical**
2. Notice 5 similar tickets in past 10 minutes
3. Click first ticket, change priority to **Critical**
4. Assign to team lead or DevOps
5. Add internal note with error pattern
6. Merge duplicate tickets into primary ticket
7. Reply to all: "We're investigating validation API issues. Will update within 30 minutes."
8. Change status to "In Progress"
9. Monitor system logs and health check (linked in ticket context)
10. Once resolved, update all tickets with solution

### Workflow 3: Proactive Customer Outreach

**Scenario:** License expiring soon, reach out before customer creates ticket.

**Steps:**
1. Navigate to **Licenses** page
2. Filter: **Expires in 7 days**
3. Select customer licenses
4. Click **Create Support Ticket** (bulk action)
5. Subject: "License Renewal Reminder"
6. Category: "Billing"
7. Priority: "Normal"
8. Message: Pre-filled renewal instructions
9. Status: "Waiting for Customer"
10. Assign to billing team

**Result:** Proactive support, reduce reactive ticket volume.

---

## Reporting and Analytics

Access ticket analytics in **Reports → Support Tickets**:

**Available Metrics:**
* **Ticket Volume** — Total tickets by period (daily, weekly, monthly)
* **Resolution Time** — Average time to close tickets by category/priority
* **First Response Time** — How quickly team responds to new tickets
* **Customer Satisfaction** — Based on customer ratings (if enabled)
* **Team Performance** — Tickets resolved per agent, response times
* **Category Distribution** — Which categories have most tickets
* **Trending Issues** — Patterns in ticket subjects and descriptions

**Export Options:**
* CSV export of filtered ticket lists
* Detailed reports with response threads
* Team performance summaries
* Monthly ticket summaries for stakeholders

---

## Settings Configuration

### Ticket Management Settings

Navigate to **Settings → Ticket Management** to configure:

**General Settings:**
* **Enable Ticket System** — Turn on/off the entire feature
* **Auto-Close Resolved Tickets** — Automatically close tickets after X days in "Resolved"
* **Customer Can Reopen** — Allow customers to reopen closed tickets
* **Require Category Selection** — Make category mandatory when creating tickets
* **Allow Customer Attachments** — Let customers upload files
* **Max Attachment Size** — File upload limit (default: 10 MB)

**Email Settings:**
* **Ticket Creation Email** — Send confirmation to customer
* **Team Notification Email** — Alert team of new tickets
* **Customer Reply Email** — Notify assigned agent
* **Resolution Email** — Confirm ticket closure to customer
* **Email Template Customization** — Modify notification templates

**Auto-Assignment:**
* **Enable Auto-Assignment** — Automatically assign new tickets
* **Assignment Method** — Round-robin, skill-based, or load-balanced
* **Business Hours** — Only auto-assign during specific hours
* **Category Rules** — Route by ticket category

**Priority SLA:**
* **Critical Response Time** — Target: 1 hour
* **High Response Time** — Target: 4 hours
* **Normal Response Time** — Target: 24 hours
* **Overdue Notifications** — Alert supervisors if SLA breached

**Canned Responses:**
* Create reusable response templates
* Assign keyboard shortcuts (e.g., `/activation-help`)
* Organize by category
* Include variables (customer name, license key)

---

## Troubleshooting

**Problem:** Customers not receiving ticket emails

**Solution:**
1. Check **Settings → Email Configuration**
2. Verify SMTP settings are correct
3. Check spam folder
4. Test email delivery with **Send Test Email**
5. Check **Logs** for email delivery errors

---

**Problem:** Ticket auto-assignment not working

**Solution:**
1. Verify **Settings → Ticket Management → Auto-Assignment** is enabled
2. Check that team members have "Available" status
3. Ensure category assignment rules are configured
4. Review **Background Jobs** for assignment job errors

---

**Problem:** Cannot see tickets created by customers

**Solution:**
1. Check admin user role and permissions
2. Verify you have access to "Support Agent" or higher role
3. Clear ticket filters (might be filtering out new tickets)
4. Check environment selector (tickets are environment-specific)

---

## Technical Details

* **Ticket Numbers:** Auto-generated with prefix `TICK-` + sequential number
* **Storage:** All tickets and responses stored in database
* **Attachments:** Stored in S3 or configured storage backend
* **Search:** Full-text search on subject, description, and responses
* **Performance:** Indexed by status, assigned_to, and created_at
* **Retention:** Tickets are never auto-purged (unlike logs/telemetry)

---

## Related Pages

* [Customers]({{< ref "/docs/admin-portal/customers" >}}) — View customer account details and license history
* [Licenses]({{< ref "/docs/admin-portal/licenses" >}}) — Quickly access license information from tickets
* [Settings]({{< ref "/docs/admin-portal/settings" >}}) — Configure ticket management settings
* [Notifications]({{< ref "/docs/admin-portal/notifications" >}}) — Manage team notification preferences

---

## How to Access

**Navigation:** Admin Portal → **Support** → **Tickets**
**URL:** `/admin/tickets`

**Permission Required:** Support Agent role or higher
