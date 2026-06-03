---
title: Manage datasets
description: This article provides information about creating and deleting datasets and using datasets in an analysis.
url: https://docs.tealium.com/server-side/insights/manage-datasets/
---
Datasets can be created only from the predefined Redshift data source, which is automatically created after generating a dashboard based on data in DataAccess. The Redshift data source is available only for Data Access users.

## Create a new dataset

Users must have the **Author** role to create a dataset. You can only create a dataset from the predefined Redshift data source.

Use the following steps to create a new dataset:

1. Go to **Insights &amp;gt; Dashboards**, and click **Datasets**.
1. Click **New dataset**.
1. Select a data source **From Existing Data Sources**.
1. In the confirmation dialog box, click **Create dataset**.
1. In the **Choose your table** dialog, select a **Schema**.  
Select the schema with a name that ends with the name of the current profile.
1. Select a table, then click **Edit/Preview data**.  
By default, all columns of the table are displayed.
1. Edit the table as needed.  
You cannot change data in a table, add or delete records in a table, or delete columns in a table. You can make the following changes to the table:  
    * Exclude or include columns.  
You may want to exclude columns that contain PII data.
    * Rename columns.
    * Change the data type for a column.
    * Apply filters.
    * Add calculated fields.
1. Click **Save**.  
The dataset is saved immediately. Save and Publish is not required.

## Edit a dataset

Use the following steps to edit a dataset:

1. Go to **Insights &amp;gt; Dashboards**, and click **Datasets**.
1. Click on a dataset, then click **EDIT DATASET**.  
Add and remove fields as needed.
1. Click **SAVE &amp; PUBLISH**.  
To save the dataset and create a new analysis, click **PUBLISH &amp; VISUALIZE**.

## Delete a dataset

Users must have the **Author** role to delete a dataset. You can only delete datasets based on the Redshift data source.

Use the following steps to delete a dataset:

1. Go to **Insights &amp;gt; Dashboards**, and click **Datasets**.
1. Click the menu for a dataset, and select **Delete**.

## Update the dataset structure for a dashboard

When a dataset structure has been updated, the dataset will also need to be updated. A message will be displayed on the dashboard indicating that the dataset structure is obsolete and needs to be updated.

To update the dataset, use the following steps:

1. In the message, click **Update**.  
You can also go to the **Datasets** screen and click **Update**.
1. In the confirmation message, click **Submit**.  
When the dataset update is completed, a success message is displayed. 

## Refresh a dataset

When a dataset has reached its maximum capacity, a message will be displayed on the dashboard indicating that the dataset has reached its capacity limit and needs to be refreshed.

To refresh the data in a dataset, use the following steps:

1. In the message, click **Run Refresh**.  
You can also go to the **Datasets** screen and click **Run Refresh**.
1. In the confirmation message, click **Submit**.  
The dataset refresh is executed in the background. When the refresh is completed, the dataset will contain only the latest 800 million rows. 