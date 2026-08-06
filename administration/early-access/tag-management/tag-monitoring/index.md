---
title: Tag monitoring
description: Monitor tag execution health and identify errors across your profile.
url: https://docs.tealium.com/administration/early-access/tag-management/tag-monitoring/
--- 

<blockquote>
Tag monitoring is in Early Access and is only available to select customers. If you are interested in trying this feature, [contact support](https://docs.tealium.com/support/).
</blockquote>


Tag monitoring collects Tealium tag execution data and displays it in the **Tags** list view and the **Insights** tab of each tag detail view. This data helps you identify client-side tag health issues faster than waiting for downstream analytics reports or external alerts. Tag monitoring sends data in a dedicated stream, separate from your business event data.


<blockquote>
Tag monitoring telemetry does not count against your event volume. It uses a dedicated collection endpoint separate from your business events.
</blockquote>


## Requirements

This feature requires the following:

* `utag.js` version 4.55 or later. To check and update your templates, use the [Template Status Checker](https://docs.tealium.com/template-status-checker/).
* Tealium Tag Monitoring tag

## What tag monitoring collects

Tag monitoring collects the following data for each tag execution in your profile:

* Tag UID and vendor name/ID
* Account and profile name
* Profile version
* Page URL with query string stripped (domain and path only)
* Event name (`tealium_event`)
* Timestamp (UTC)
* Template execution successes and failures

## Set up tag monitoring

To set up tag monitoring, complete the following steps:

1. Update `utag.js` to version 4.55 or later using the [Template Status Checker](https://docs.tealium.com/template-status-checker/).
1. Go to **Tag Management > Tags**.
1. Click **+ New Tag**.
1. Search for **Tag Monitoring**, select it, and click **Continue**.
1. Review the tag settings and click **Save**.
1. Click **Save/Publish** to publish the profile.

After publishing, you can see tag data in the **Insights** tab in each tag detail view.

## View tag monitoring metrics

### Tags list view

The tags list view displays a **Summary** section above the tags table with two metric cards:

* **Tag Template Executions**: The total number of tag template executions for the selected time period, with a sparkline trend (a small inline chart).
* **Execution Errors**: The total number of execution errors for the selected time period, with a sparkline trend. A high error count relative to total executions may indicate a tag configuration or site issue.

Use the date range selector to filter summary metrics by **24 hours**, **7 days**, **30 days**, or a custom range.

### Insights tab

Click any tag in the **Tags** list to open its detail view, then click **Insights**. The Insights tab contains two sub-tabs: **Execution** and **Events**.

#### Execution

The **Execution** tab shows execution health for the selected tag:

* **Tag Template Executions**: Total executions in the selected time period.
* **Errors**: Total errors in the selected time period.
* **Success Rate**: Percentage of executions that completed without errors.

The **Execution Overview** chart plots executions and errors as separate lines over time. Hover over any point to see the counts for that date.

#### Events

The **Events** tab breaks down execution data by event name:

* **Total Events**: The total number of event firings recorded.
* **Unique Events**: The number of distinct event names recorded.

The **All Events** table lists each event name with the following columns:

* **Executions**: Execution count with a sparkline trend.
* **Errors**: Error count and its percentage of total executions.
* **Success Rate**: Percentage of executions that completed without errors.

Columns are sortable and the table supports pagination.

## Limitations

* Metrics in the UI may lag behind actual activity.
* Tag Monitoring does not monitor vendor JavaScript, outbound vendor network requests, extension failures, or `utag.sync.js` failures.
* Tag Monitoring does not capture the outbound data payload sent to the vendor. It reflects only what was present in the data layer at the time of tag execution.
