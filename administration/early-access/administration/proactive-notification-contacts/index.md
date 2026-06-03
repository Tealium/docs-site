---
title: Proactive notification contacts
description: This article explains proactive notification contacts and how to specify them for time-sensitive service communications.
url: https://docs.tealium.com/administration/early-access/administration/proactive-notification-contacts/
---
Proactive notification contacts is currently in Early Access and is available to select customers only. Contact your Tealium Support representative to get started.

## How it works

Proactive notification contacts specify who Tealium should contact about incidents, security issues, urgent migrations, or other time-sensitive service communications.

These contacts are used only for service and operational communications initiated by Tealium (for example, proactive incident notices or required action emails).

Tealium may use proactive notification contacts for the following scenarios:

* When Tealium identifies an issue that may impact your implementation and action or awareness is required.
* When Tealium must contact you about an issue with potential regulatory or compliance impact.
* When deprecations, migrations, or configuration changes require you to update your settings within a defined timeframe.

Tealium uses the email address and its associated roles for proactive notifications. Emergency phone numbers are managed separately and are used only when a phone call is required for high-priority situations.

## Requirements

* Account admin role. Other users in your account cannot see or change these settings.
* A validated email address for each contact.
* A direct phone number (recommended) for urgent or out-of-hours communication. Include the country code with each phone number.

We recommend at least two proactive notification contacts for each account (for example, a primary technical owner and a backup contact).

Account admins are responsible for ensuring the following:
*  Admins have all authorizations required to disclose contact information to Tealium for the notification purposes.
* Admins must ensure proactive notification contact information remains accurate and up to date.

## Access proactive notification contacts

To access proactive notification contacts, you must be an account admin.

You can access contact information from either Tealium iQ Tag Management or from Server-side profiles.

**Tealium iQ Tag Management**

1. Click your user initial in the upper-right corner.
1. Under **Manage Platform**, click **Contact Information**.

**Server-side**

1. Click your user initial in the upper-right corner.
1. Click **Server-Side Settings**.
1. Click **Contact Information**.

If you do not see this section, verify that your user account has the account admin role or contact Tealium Support.

## Add a proactive notification contact

To add a proactive notification contact:

1. In **Contact Details (Account-wide)**, click **Add contact**.
1. **Edit Contact**  
    *  **Email Address**: Enter the email address you want Tealium to use for proactive notifications. 
    * **Role**: Select one or more roles that describe why this address should be contacted (for example, Finance or Technical). 
    * **Alias/Distribution List**: Indicate whether the email address is an alias or distribution group.
1. **Emergency Phone (Optional)**  
Enter one or more comma-separated phone numbers including the country code (for example, &#43;`1 415 555 0100, &#43;44 20 7946 0958`). We recommend including an emergency phone number for urgent or out-of-hours communication. Roles are not available for emergency phone numbers.
1. Review the contact information for accuracy, then click **Save Changes**. Your changes are effective immediately. You do not need to save the profile.

## Edit or remove a contact

To update an existing contact:

1. Open **Contact Details (Account-wide)**.
1. Find the relevant email address, then click **Edit** under **Actions**.
1. Edit the email address, role, and alias or distribution group settings and click **Update Contact**.
1. Edit the **Emergency Phone** field as needed.
1. Click **Save Changes**.

To remove a contact who should no longer receive proactive notifications:

1. Open **Contact Details (Account-wide)**.
1. Find the relevant email address, then click **Delete** under **Actions**.
1. Edit the **Emergency Phone** field as needed, removing any phone numbers that are no longer relevant.
1. Click **Save Changes**.

We recommend that you update a contact when someone&#39;s role changes and remove a contact when they leave your organization.

## Best practices

To keep your proactive notification contacts effective:

* Review your list of contacts at least once per quarter, or whenever key staff or responsibilities change.
* Add a direct phone number so Tealium can reach someone quickly for high-priority incidents or regulatory-driven communications.
* Where your organization supports it, consider using role-based addresses (for example, `tealium-operations@example.com`) in addition to individual contacts.
* Where possible, choose contacts who are familiar with your Tealium implementation and who can coordinate internally when action is required (for example, publishing a profile or updating a configuration).

## Contact roles

When you add proactive notification contacts, include people from the following areas so the right teams are notified for each type of issue:

* **Finance:** Billing and contract-related questions that may arise from incident credits, service-level discussions, or commercial changes tied to operational issues.
* **Business:** Business or marketing stakeholders who are familiar with downstream impact from situations or who make decisions about prioritizing migration work.
* **Developer:** Implementation changes in your sites or apps, such as updating tags, data layer, or SDK integrations in response to a required fix or migration.
* **Technical:** Day-to-day technical ownership of your Tealium implementation, including profile publishes, configuration changes, and coordination with internal operations teams.
* **Security:** Security-sensitive situations, including vulnerabilities, credentials, or behaviors that may require immediate investigation or containment by your security team. Note that any security contact information provided does not supersede contact details in your contract with Tealium.

Proactive notification contacts are used for service communications about your Tealium account. These contacts are not used for marketing emails.

## Troubleshooting

### The proactive notification contacts section is missing

* Verify that you are signed in with an account admin user.
* If you still do not see the section, contact your internal Tealium administrator or open a ticket with Tealium Support.

### A contact left the company but still receives emails

* Remove the user from **Proactive notification contacts**.
* Update your internal systems so that any shared or forwarding mailboxes are redirected as required.
* If you continue to see issues, contact Tealium Support with the affected email address.
