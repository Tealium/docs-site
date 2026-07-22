---
title: Manage analyses
description: This article provides information on creating, printing, and publishing an analysis.
url: https://docs.tealium.com/server-side/insights/manage-analyses/
---
Users with the author role can create and save an analysis, share it with others, or publish it as a custom dashboard. 

## Create an analysis

When you create or edit an analysis, **AUTOSAVE** is on by default. If you turn it off and open the analysis again, **AUTOSAVE** is turned on again.

<blockquote>
If you turn **AUTOSAVE** off, then make changes to an analysis and publish the dashboard, the analysis changes are not saved and are not included in the published dashboard. If you turn **AUTOSAVE** off, be sure to turn it back on if you need to save your changes.
</blockquote>


Use the following steps to create an analysis:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Click **New analysis**.  
The available datasets are displayed.
1. Select a dataset, then click **USE IN ANALYSIS**.
1. To add a field to the **AutoGraph** in the sheet, click a field in the **Data** list.
1. Select a visual type under **Visual Types**.
1. To add another visual, click **+ ADD** in the **Visuals** section, add a field from the **Fields list**, and select a visual type under **Visual Types**.

## Publish an analysis

Users with the author role can publish or share an analysis. When you publish an analysis, a dashboard is created for the analysis, which can be viewed by users with the reader role.

Use the following steps to publish an analysis:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis.
1. Click **File**, then click **Publish**.

## Share an analysis

You can share an analysis Insights with other Insights authors and administrators.

Use the following steps to share an analysis:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis.
1. Click **File**, then click **Share**.
1. Enter a user name, group, or email address.
1. When you are finished adding users, groups, or email addresses, click **Share**.

## Use multiple datasets

You can add multiple datasets to an analysis to show visuals for different types of data.

Use the following steps to add a dataset to an analysis:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis.
1. Expand the Dataset drop-down list in the **Data** section, then click **Add a new dataset**, as shown in the following figure:  
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-add-dataset.png)
1. Select the dataset to add, then click **Select**.
1. Click **Close**, or click **Add a dataset** to add another dataset to the analysis.

You can now add visuals for the new dataset.

## Add a filter

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis.
1. Click the filter icon.  
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-icon-bar.png) 
1. In the **Filter** section, click **+ ADD**.
1. Select a field to filter, then click the added field to see the filter details.
1. In the filter details, select a **Filter condition** and **Enter a value**.
1. To change the visuals the filter applies to, click **Applied To** and select one of the following:  
    * **Only this visual** &ndash; The filter applies to the selected visual only.
    * **Some visuals** &ndash; The filter applies to visuals with valid column mappings.
    * **All visuals of this dataset** &ndash; The filter applies to all items based on this dataset.
    * **All applicable visuals** &ndash; The filter applies to any visuals that have valid column mappings.
1. To add the filter to the sheet and make it visible on the dashboard, click the filter menu and select **Add to sheet**.
1. To add the filter to the visual, click **APPLY**.
1. To update the published dashboard, click **PUBLISH**.

You can **Edit**, **Delete**, or **Disable** a filter from the filter menu.

## Change the title of a visual

Use the following steps to change the title of visual:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis.
1. Double-click on the title of the visual you want to change.
1. In the **Edit title** window, enter the new title in the text box, then click **Save**.
1. To update the published dashboard, click **PUBLISH**.

## Change the type of visual

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis, then select the visual to change.
1. In the **Visuals** section, under **CHANGE VISUAL TYPE**, select a new visual type.  
Hovering on a visual type displays the required fields for that visual type.
1. If needed, update the selected fields for the visual.
1. To update the title of the visual, double-click the title, then enter the new title in the **Edit title** window, then click **Save**.
1. To update the published dashboard, click **PUBLISH**.

## Add a visual to an analysis

Use the following steps to add a visual to an analysis:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis.
1. Under **Visuals**, click **Add**.
1. Add fields and a visual as described in [Create an analysis]().
1. To update the published dashboard, click **PUBLISH**.

## Change the data aggregation for a visual

Use the following steps to change the data aggregation:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis.
1. Under **Visuals**, click the menu for the field you want to change, then select a value for **Aggregate**.
1. To update the published dashboard, click **PUBLISH**.

## Print an analysis

Users with the author role can print an analysis, as follows:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis, then click **File**, and click **Print**.  

## Export an analysis

Users with the author role can export an analysis, as follows:

1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis, then click **File**, and click **Export as PDF**.  
When the PDF is ready, the following message is displayed:
![](https://docs.tealium.com/images/server-side/data-insights/data-insights-pdf-ready-msg.png) 
1. To download the exported PDF, click **DOWNLOAD**.

## Copy an analysis
1. Go to **Insights &gt; Dashboards**, and click **Analyses**.
1. Select an analysis, then click **File**, and click **Save As Analysis**. 
1. Enter name for the new copy of the analysis, then click **SAVE**.