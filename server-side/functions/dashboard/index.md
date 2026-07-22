---
title: Functions dashboard
description: This article provides information about the functions dashboard.
url: https://docs.tealium.com/server-side/functions/dashboard/
---
The **Functions Overview** screen has two tabs, **Overview** and **Insights**. The **Insights** tab displays visualizations and data about functions on three tabs, as follows: 

* **Overview** tab
    * Total invocations
    * Total unique functions invoked
    * Functions enabled vs created
    * Success rate
    * Total invocations over time
    * Invocations by type
    * Most invoked functions
    * Most popular runtime versions
* **Executions** tab
    * Minimum execution time (ms)
    * Maximum execution time (ms)
    * Average execution time (ms)
    * Total execution time (ms)
    * Total execution time over time (ms)
    * Longest-running functions (ms)
    * Average execution time over time (ms)
    * Average execution time (ms)
* **Errors** tab
    * Functions with errors
    * Errors by function type
    * Function with most errors
    * Errors over time
    * Dropped functions due to limits
    * Dropped function logs due to limits
    * Most dropped functions
    * Dropped functions over time

The following figure shows an example of the functions insights visuals.
![](https://docs.tealium.com/images/server-side/functions-insights-tab.png)

## Turn on functions insights

Functions insights is off by default and can be turned on at any time. Use the following steps to turn on functions insights:

1. On the **Server-Side** User Menu, select **Server-Side Settings**, then click **Insights**.
1. Under **Feature Insights**, click the **Functions Dashboard** toggle to turn it on.
1. Save and publish your changes.

After you turn on functions insights dashboards, it may take up to 2 hours for data to appear in the reports. If you turn off functions insights later on, the dashboard and its data is deleted 30 days after the change is published.

## View functions insights

1. Go to **Transform > Functions**.
1. Click the **Insights** tab.
You may need to scroll down to see all the graphs.

For more information about dashboards and templates, see [About Tealium Insights]() and [About templates]().