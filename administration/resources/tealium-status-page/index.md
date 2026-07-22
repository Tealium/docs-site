---
title: Tealium status page
description: This document explains the status page and how to subscribe to announcements.
url: https://docs.tealium.com/administration/resources/tealium-status-page/
---
## How it works

The status page at <https://status.tealium.com/> lists status updates for all Tealium services and features. Click a service or feature to expand it and list all of its sub-services.

## Statuses

A service can be in one of the following states:

* **Operational**: All systems and error rates are at acceptable operating levels.
* **Maintenance**: This notification announces a planned maintenance window and it follows the maintenance through to completion. For more information, see [Planned maintenance](#planned-maintenance).
* **Degraded Performance**: Response times are slow and error rates are higher, but the system is fully operational.
* **Partial Service Disruption**: A portion of the service or feature is unavailable or error rates are higher and errors are unrecoverable.
* **Service Disruption**: Services or features are fully unavailable or error rates are completely unrecoverable.
* **Security Event**: There is a security compromise that requires immediate notification.

If a service or feature is not operational, click **History** to see the full details of the issue.

## Status history

Click **History** to go to the **Status history** page. The **Status history** page lists all recent issues in reverse chronological order.

All issues and their updates include timestamps in [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time).

### Incident states

Service disruptions list the components affected by the issue and the following status updates:

* **Investigating**: We are aware of the issue and are investigating.
* **Identified**: We have identified the issue and next course of action, and we are working toward a resolution.
* **Monitoring**: We have resolved the issue so there is no further impact. We are monitoring the system to confirm that the issue has been resolved, and we are repairing anything was was impacted by the issue.
* **Resolved**: We have resolved the issue. There will be no short-term recurrence of the issue. If repairs are necessary, they are ongoing.

The announcement contains any actions you need to perform during the disruption or afterwards.

Click an announcement title to expand or collapse the announcement. You can also click **Expand All Notices** or **Collapse All Notices** to toggle the expand state of every announcement.

Click **Back to current status** to return to the status page.

## Planned maintenance

Tealium announces maintenance windows ten days in advance. Maintenance window announcements contain the following information:

* **Description**: A description of the planned maintenance, how it will affect you, and what actions you may need to perform during the maintenance window.
* **Components**: The components we are working on during the maintenance window.
* **Schedule**: The planned start and ending time of the maintenance window. The maintenance may end sooner that planned or it may take longer than planned.

Maintenance can be in one of the following states:

* **Scheduled**: Maintenance is planned. Times and details have been communicated.
* **Active**: Maintenance has begun and is ongoing.
* **Completed**: Maintenance is complete, as successful or rescheduled if necessary.

If any issues occur during the maintenance window, such as the engineers needing more time to perform the maintenance, they will appear as **Updates**.

# Subscribe

Click **Subscribe** to receive notices of announcements through your preferred method or methods:

* **Email**: Enter your email address and click **Subscribe** to receive announcements through email.
* **Webhook**: Enter the webhook URL to send announcements in JSON format through a POST method.
* **RSS Feed**: Click RSS feed to open a browser tab that contains the RSS feed of announcements. Add the feed's URL to your preferred RSS feed reader.
* **Slack**: Click **Add to Slack** to open a Status.io permission request page. Log in to your preferred Slack workspace, select the channel for Status.io to post as an app, and click **Allow**. Your workspace administrators will need to approve Status.io access to the workspace.

Click **Manage Existing Subscription** to request a link through email to a page where you can manage your subscription. You will need to enter your email address, webhook URL, or Slack channel ID to identify the method you are using to receive updates.

On the **Manage Subscription** page, you can perform the following actions:
  * Select the checkboxes for each sub-service you want to receive announcements for and then click **Save Subscription**.
  * Click **Select All** and **Deselect All** to change all checkboxes at once.
  * Click **Unsubscribe** to stop receiving announcements.