---
title: Connectors dashboard
description: This article provides information about the connectors dashboard and the visuals it displays.
url: https://docs.tealium.com/server-side/connectors/connectors-dashboard/
---
The connectors dashboard displays the following tabs that contain visualizations of information about connectors and actions:

* **1. Connector and Action Activity**
* **2. Connector and Action Errors**
* **3. Connector and Action Data Volume**
* **4. Connector and Action Retries**

Unless otherwise specified, the time frame for the dashboard data begins on the date the dashboard was enabled. It can take up to 48 hours for new data to appear in the Connectors Dashboard visuals. 

Total actions sent may be lower than the total events/visitors sent because batch enabled connectors send multiple requests in a single action.

For more information about connectors, see [About connectors]().

## Visuals on connectors dashboard tabs

* **1. Connector and Action Activity** tab 
    * **Most frequently triggered connectors** &amp;ndash; Shows the number of times the connector was triggered, connector name, source type, and connector ID.
    * **Most frequently triggered actions** &amp;ndash; Shows the number of times the action was triggered, action name, connector name, source type, and action ID.
    * **Connectors and their actions** &amp;ndash; Shows connector names, source type, and connector ID, and its associated actions.
    * **Total connectors triggered over time** &amp;ndash; Shows the total number of connectors triggered over time. For example, connectors triggered per week.
    * **Total actions triggered over time** &amp;ndash; Shows the total number of actions triggered over time. For example, actions triggered per week.
* **2. Connector and Action Errors** tab
    * **Most frequent connector failures** &amp;ndash; Shows the connectors with the most frequent errors.
    * **Most frequent action failures** &amp;ndash; Shows the actions with the most frequent errors.
    * **Failed connector counts over time** &amp;ndash; Shows the total number of connector failures over time. For example, the number of connector failures per week.
    * **Failed action counts over time** &amp;ndash; Shows the total number of action failures over time. For example, the number of action failures per week.
    * **Most frequent errors** &amp;ndash; Shows error names and number of occurrences of each.
    * **Action error counts by error type over time** &amp;ndash; Shows the number of errors over time. Hover over a numbered block to see the error name, time period, and number of errors. 
* **3. Connector and Action Data Volume** tab
    * **Actions success rate** &amp;ndash; Shows the number of action successes and the number of action failures.
    * **Successful vs Failed events/visitors counts over time** &amp;ndash; Shows the number of action successes and the number of action failures over time. For example, errors and successes per week.
    * **Total successful processed events/visitors (bar) and successful actions count (line) over time** &amp;ndash; A bar graph that shows the number of processed events/visitors for each time period and a line graph that shows the number of actions per time period.
    * **Failed events/visitors counts (bar) over time vs Failed actions counts (line) over time** &amp;ndash; A bar graph that shows the number of failed events/visitors for each time period and a line graph that shows the number of failed actions per time period.
    * **Successful vs Failed events/visitors counts per action** &amp;ndash; Shows the number of successfully processed events/visitors and the number of failed events/visitors.
* **4. Connector and Action Retries** tab
    * **Total retries count** &amp;ndash; Shows the total number of retries and the number of retries per retry type.
    * **Connectors with retries** &amp;ndash; Shows the number of retries per connector.
    * **Actions with retries** &amp;ndash; Shows the number of retries per connector action.
    * **Retries count by retry type over time** &amp;ndash; Shows the number of retries by retry type for each time period. For example, retries per retry type by week.
    * **Retries count by connector over time** &amp;ndash; Shows the number of retries per connector for each time period.
    * **Retry error codes** &amp;ndash; Shows the number of retries for each error code.
    * **Retries response status** &amp;ndash; Shows the number of successful and failed responses.
    * **Retry response failed vs success over time** &amp;ndash; Shows the number of successful and failed responses per time period.

## View the connectors dashboard

1. Go to **Analyze &gt; Insights &gt; Dashboards**.
1. Click **Connectors Dashboard**.

## Export a PDF

Use the following steps to generate and download a PDF file:

1. Go to **Analyze &gt; Insights &gt; Dashboards**.
1. Click **Connectors Dashboard**, then select the visual to export.
1. Click the **Export** icon, as shown below, then select **Generate PDF**.
![](/images/server-side/connectors-dashboard-export-icon.png)  
The following message is displayed when your PDF is ready to download:
![](/images/server-side/connectors-dashboard-pdf-ready.png)
1. In the message, click **Download**.  

To download the PDF later, use the following steps:

1. Click the **Export** icon, then select **View exports**.
2. For the PDF file you want to download, click **Click to download**.

## Export to CSV file

Use the following steps to export visual data to a CSV file:

1. Go to **Analyze &gt; Insights &gt; Dashboards**.
1. Click **Connectors Dashboard**.
1. Select a visual, then click the visual menu and select **Export to CSV**.
![](/images/server-side/connectors-dashboard-export-csv.png)
The following message is displayed:  
![](/images/server-side/connectors-dashboard-working-on-csv.png)
When the CSV file is ready, the following message is displayed:
![](/images/server-side/connectors-dashboard-csv-ready.png)
The CSV file is automatically downloaded to your default downloads folder.

To download the CSV file later, use the following steps:

1. Click the **Export** icon, then select **View exports**.
2. For the CSV file you want to download, click **Click to download**.

## Add a filter

Visual data can be filtered based on the value of the attributes used in the visual. For example, you can add a filter on the time attribute to change the time frame of a visual.

To add a filter to a visual, use the following steps:

1. Go to **Analyze &gt; Insights &gt; Dashboards**.
1. Click **Connectors Dashboard**.
1. Select a visual and click **Applied filters**.  
![](/images/server-side/connectors-dashboard-applied-filters.png)
1. Click **View dashboard filters**.
1. In the **Filters** section, click **ADD FILTER**.  
For information about configuring filters, see [Using filters on dashboard data](https://docs.aws.amazon.com/quicksight/latest/user/filtering-dashboard-data.html).