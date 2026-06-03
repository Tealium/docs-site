---
title: AudienceStream Dashboard
description: This article explains the features of the AudienceStream Dashboard.
url: https://docs.tealium.com/server-side/audiences/audiencestream-dashboard/
---
## Trend Graphs

The **Trend Graphs** section shows data across a time range. You can view trends for the following objects:

* Audiences
* Connector actions
* Badges attributes
* Number attributes
* Boolean attributes

View trends for one or more values in the same graph. Viewing two values in a graph allows to you compare these values and look for correlations. You can view the same value across different time ranges, or compare the trends of two different values.

 To set up a trend graph, use the following steps:

1. In the sidebar, go to **AudienceStream &gt; Dashboard.**
1. Click the gear icon on the lower-right corner of any displayed graph.
  ![](/images/server-side/audiencestream-dashboard-click-gear-to-flip.png)  
The graph &#34;flips&#34; over to display values and ranges.
  ![](/images/server-side/audiencestream-dashboard-graph-flipped.png)
Two drop-down lists appear.
1. Use the drop-down list to select the value to view.
1. Use the drop-down list to select the **Current** or **Previous** time range.
1. Use the drop-down list to select one of the following:
    * Calendar Day
    * Calendar Week
    * Calendar Month
    * Rolling Day
    * Rolling Week
    * Rolling Month
1. Click **Finish**. The graph will flip back to trend lines.
  ![](/images/server-side/whiteui-audiencestream-select-values-and-finish.png)

## Time range

When you view a value in a trend graph, you must choose a time range. The range is the time range for which you want to view data and is calculated in relation to today. There are two main parameters to select: Current and Previous.

### Current

This value refers to the time range that today is contained within.

* **Day**: The current day.
* **Week**: This time range begins from the most recent Sunday and ends on the current day.
* **Month**: This time range begins on the first day of this month and ends on the current day.
* **Rolling Day**
* **Rolling Week**
* **Rolling Month**

This value is the time range before the time range that today is contained within.

* **Day**: The time range for the previous day. For example, if today is Wednesday, then this date range covers 12:00 AM through 11:59 PM of Tuesday.
* **Week**: This time range for the previous week. Weeks begin on Sunday and end on Saturday.
* **Month**: The time range for the previous month. For example, if today is June 14, then this date range covers May 1-31.
* **Rolling Day**
* **Rolling Week**
* **Rolling Month**

### Badge activity

The **Badge activity** window appears on the right side of the screen and lists the number of times for a given time range badges were assigned to and removed from your visitors.

![](/images/server-side/whiteui-audiencestream-badgeactivity.png)

Click a badge to view the details of how and when it was assigned or removed from a visitor.

![](/images/server-side/whiteui-audiencestream-badge-activity-details.png)

### Dashboard sheets

Dashboard sheets are a customized view of trend graphs. The default sheet is named **Main** and cannot be renamed or deleted. Dashboard sheets are numbered and are available through the dashboard side bar seen here:

![](/images/server-side/whiteui-audiencestream-dashboard-dashboardsheetscollapsed.png)

Click the arrow at the top of the side bar to see the names of the sheets and to edit sheets. The following actions are available using the dashboard side bar:

![](/images/server-side/whiteui-audiencestream-dashboard-dashboard-sheets-expanded.png)

* **Add a Sheet**: Click **&#43; Add Dashboard Sheet** at the bottom of the side bar to add a sheet and then click the edit icon to name the sheet. Click **Save** to save the sheet with the new name.
* **Rename a Sheet**: Click the edit icon to change the name of a sheet and then click **Save**.
* **Delete a Sheet**: Click the &#34;**X**&#34; icon to to the right of the name to delete a sheet and then click **Yes** to confirm.
