---
title: Moments API Insights
description: This article provides information about the data and visualizations displayed in the Moments API Insights tab.
url: https://docs.tealium.com/server-side/moments-api/insights/
---
## How it works

The Moments API **Insights** tab displays visualizations and data about Moments API engine writes and engine reads. An engine write occurs when visitor data used in an engine is updated. An engine read occurs when a `GET` request is made to the endpoint. 

The Moments API **Insights** tab displays the following visualizations and data:

* Engine reads
* Engine writes
* Engine reads and writes 
* Engine write requests that exceeded the data limit and were not written
* Average size of engine writes that exceeded the data limit
* Total reads over time
* Total writes over time
* Total reads by engine
* Total writes by engine
* Total data in bytes not written over time (due to write requests that exceeded the data limit)

The following figure shows an example of the visualizations and data shown in the **Moments API Insights** tab:
![](/images/server-side/moments-api-insights-tab-example.png)

### Write requests that exceed the data limit

If a large number of audiences, badges, and attributes are specified for an engine, the size of an engine write can exceed the maximum amount of data that can be stored per visitor per engine. Using names for audiences, badges, and attributes can also increase the write size. For more information, see [Limits]().

If engine writes are exceeding the maximum amount of data per visitor per engine, you can reduce the write size in one of the following ways:

* Use attribute IDs instead of names for audiences, badges, and attributes.
* Divide the data between two or more engines.

## Select a date range

The default **Date Range** for the data and visualizations is **Last 30 days**. To select a new **Date Range**, use the following steps:

1. Click the **Controls** bar.  
![](/images/server-side/moments-api-insights-tab-control-bar.png)
1. Click the current **Date range**.
1. Do one of the following:  
    * To display data by weeks, months, quarters, or years, click **Relative by** and select an option.  
    * To display data for an absolute date range, click **Absolute date range**, then select the beginning and ending dates.    
    The display is refreshed with the new data.
1. To close the list, click the **Controls** bar.

## Select an engine

The default **Engine** for the data and visualizations is **All**. To select a specific engine, use the following steps:

1. Click the **Controls** bar.  
![](/images/server-side/moments-api-insights-tab-control-bar.png)
1. Click the current **Engine** and select a new engine.  
The display is refreshed with the new data.
1. To close the list, click the **Controls** bar.

## Updates to the Moments API Insights tab

The visuals shown in the Moments API **Insights** tab are also available in Tealium Insights as the Moments API Dashboard. Tealium Insights dashboards and the Moments API **Insights** tab display messages when the insights template or data needs to be updated. The following sections describe how to update the template or the dataset when these messages are displayed on the Moments API **Insights** tab.

### Update the Moments API Insights template

The following message is displayed when the Moments API Insights template needs to be updated:
![](/images/server-side/data-insights/datainsights-updates-available-message.png)

To update the template, use the following steps:

1. Click **View Updates** in the message.
1. Click **View Details** for the Moments API Insights template.
1. Click **Update Dashboard**.
1. In the **Confirm Update** dialog, click **Update**.  
Save and publish is not required after updating a template.

### Update the Moments API Insights dataset

When the dataset structure for Moments API Insights has been updated, a message is displayed on the Moments API Insights tab indicating that the dataset structure is obsolete and needs to be updated.

To update the dataset, use the following steps:

1. In the message, click **Update**.
1. In the confirmation message, click **Submit**.  
When the dataset update is completed, a success message is displayed.

### Refresh the Moments API Insights dataset

When the data set for the Moments API **Insights** tab has reached its maximum capacity, a message is displayed indicating that the dataset has reached its capacity limit and needs to be refreshed.

To refresh the data in the dataset, use the following steps:

1. In the message, click **Run Refresh**.
1. In the confirmation message, click **Submit**.  
The dataset refresh is executed in the background. When the refresh is completed, the dataset will contain only the latest 800 million rows.