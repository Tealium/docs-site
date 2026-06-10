---
title: Manage logs
description: This article provides information on viewing, exporting, and downloading function log files.
url: https://docs.tealium.com/server-side/functions/manage-functions/manage-function-logs/
---
Use the **Logs** tab in the functions code editor to view, export, and download logs.

## View logs

Log files contain messages from the function, as well as any errors that occurred during execution. Use the following steps to see log files for the past 24 hours.

1. Navigate to **Transform &gt; Functions**, and click a function in the list.
1. Click the **Logs** tab.

## Export logs

You can export logs for the following time frames:

* Past 1 hour
* Past 12 hours
* Past 1 day
* Past 7 days
* Past 30 days
* Custom

Use the following steps to export logs:

1. Navigate to **Transform &gt; Functions**, and click a function in the list.
1. Click **Export Logs**.
1. Select a time frame, or select **Custom** to choose the start and end date and time.
1. If you chose **Custom**, click **Select a date and time range**, and do the following:
    1. In the calendar, select a start date and adjust the default time.
    1. Select an end date and adjust the default time, then click **Apply**.

1. Click **Request Export**.

There is a short delay while the logs are processed. Exported logs are stored for seven days after the export.

When the exported logs are ready to download, a badge is displayed on the **Logs** tab to that indicates the number of log files available for download, as shown below.
![](/images/server-side/exported-logs-badge.png)
The following message is also displayed on the **Functions Overview** page:
![](/images/server-side/exported-logs-msg.png)

## View and download exported logs

Use the following steps to view the list of exported logs and download log files:

1. Navigate to **Transform &gt; Functions**, and click a function in the list.
1. Click the **Logs** tab, then click **VIew Exported Logs**.
1. Click **Download** for an exported logs file.