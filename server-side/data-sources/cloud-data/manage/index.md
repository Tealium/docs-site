---
title: Manage a cloud data source
description: This article describes how to manage a cloud data source.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/manage/
---
## Supported vendors

The configuration for cloud data sources is nearly the same for every vendor. For vendor-specific configuration details, see the following:

* [Amazon Redshift]()
* [Databricks]()
* [Google BigQuery]()
* [Snowflake]()

## Create a cloud data source

To create a cloud data source, use the following steps:

1. Go to **Connect &gt; Data Sources**.
1. Click **&#43; Add Data Source**.
1. Under **Categories**, click **Data Warehouse** and select a vendor.
1. In the **Name** field, enter a unique name for the data source related to your use case.
1. Click **Continue**.

## Establish a connection

Before you configure the data to import, you must establish a connection to your cloud data source. A connection is the reusable configuration of your vendor credentials that connects Tealium to your cloud data source.

1. On the **Connection Configuration** screen, confirm the name of the data source, then select an existing connection from the list or create a connection by clicking the **&#43;** icon. 
1. For a new connection, enter your connection information and then click **Save** to return to the **Connection Configuration** screen.
1. Click **Establish Connection**.

For more information about connecting to your vendor, see:

* [Amazon Redshift]()
* [Databricks]()
* [Google BigQuery]()
* [Snowflake]()

## Set processing

### Enable processing

Turn on **Enable Processing** to begin importing data immediately after you save and publish your changes. You can also leave this setting off while you complete the configuration and enable processing later.

### Query frequency

Set how often Tealium fetches data. Select from the following options for processing:

* Near real-time  
The process runs every 2 seconds.
* Hourly  
The process runs at the start of each hour.
* Daily  
The process runs once a day at the time you specify.
* Weekly  
The process runs once a week at the day and time you specify.

### Batch size

Select from one of the following batch options:

* **Default**: 1,000 records per batch.
* **Custom**: Create custom batches of over 1,000 records. 
* **No limit**: Create a batch with no limit to process all available data.

## Configure the query

In the **Query Configuration** screen, select from Basic or Advanced configuration mode.

* Basic mode: Your data is imported using the default schema specified in the data source configuration. You can process data from only one table or view. 
* Advanced mode: You can specify one or more tables to join using an advanced SQL editor. The tables can be from multiple schemas. 

### 1. Build query

#### Basic mode

In Basic mode, select the table and columns to include in your query. Either incrementing, timestamp, or incrementing and timestamp columns must be included in your selection.

Optionally include a SQL `WHERE` clause to import only those records that match your custom condition. The SQL `WHERE` clause does not support nested `SELECT` statements. To join multiple tables, use Advanced mode.

#### Advanced mode

In Advanced mode, use the SQL editor to enter valid, read-only SQL queries and connect with one or more tables or schemas. The SQL editor supports advanced SQL commands, such as `CAST` and `JOIN`. Either incrementing, timestamp, or incrementing and timestamp columns must be included in your selection.

#### SQL query best practices

* **Calculated fields**  
The Advanced SQL query supports calculated (derived) fields. Calculated values are re-evaluated on each batch fetch and may behave differently depending on your vendor. Using calculated fields in query mode columns (timestamp, incrementing, or timestamp and incrementing) may lead to errors in importing data (for example, skipped rows or loops in ingestion). We recommend avoiding calculated fields for query mode columns.
* **LIMIT clauses**  
Due to the streaming nature of Tealium data sources, LIMIT clauses do not reduce the total volume of data imported. To change the number of records you want to process for testing, use a WHERE clause or use End-to-End Testing. For more information, see [Test configuration]().
* **Read-only**  
Only read-only SQL queries are supported. Ensure that your queries do not modify schema or data (for example, using `DELETE`, `UPDATE`, `INSERT`, `DROP`, `ALTER`).

When you are done, click **Continue to Query Mode**.

### 2. Set query mode

The query mode determines how to select new rows, modified rows, or both for import.

* If you select **Timestamp &#43; Incrementing** (recommended) you must select two columns, a timestamp column and a strictly incrementing column. 
* If you select **Timestamp** or **Incrementing**, you must select a column to use to detect either new and modified rows or new rows only.

For more information, see .

When you are done, click **Test Query** to preview the results.

### 3. Preview test query

Use the test query preview to validate your query results.

### Source table column changes

If columns in your source table change after you configure the data source, the required action depends on the type of change:

* **Column renamed**: If a column used in the query builder is renamed in the source table, you must duplicate the data source:
  1. Select the **Duplicate** option from the data source action menu on the **Data Sources** screen. 
  1. In the duplicate data source, update the query builder to use the new column name. 
  1. Use **Set Processing Start** to configure the ingestion start point for the new data source. See [Set Processing Start]() for more information.
* **Column added**: 
  * If a new column is added to the source table and you do not need to ingest it, no action is required.
  * If the column is a timestamp or incrementing column, duplicate the data source as you would for a renamed column. 
  * For any other new column type:
    1. Toggle data source processing to **Off** and save and publish.
    1. Edit the data source to add the column in the query builder and add column mappings. 
    1. Set the processing toggle to **On**.
    1. Save and publish again.

## Map columns

Use the column mapping table to map pre-configured column labels to event attributes or manually enter the column labels for mapping. Columns not mapped to an event attribute are ignored. 

For each column label, select the corresponding event attribute from the list.  

## Map a visitor ID

To use your cloud data source with AudienceStream, map a column to a visitor ID attribute. Select a column that represents a visitor ID and map it to the corresponding visitor ID attribute.

**Visitor ID Mapping in AudienceStream** is enabled by default. Disabling visitor ID mapping may cause errors in visitor stitching. For more information, see [Visitor Identification using Tealium Data Sources]().

## Summary

In this final step, view the summary, make any needed corrections, and then save and publish your profile. To edit your configuration, click **Previous** to return to the step where you want to make changes.

1. View the event attribute and visitor ID mappings.  
1. Click **Finish** to create the data source and exit the configuration screen. The new data source is listed in the **Data Sources** dashboard.
1. Click **Save/Publish** to save and publish your changes.

## Processed rows and errors

To see import activity, navigate to **Data Sources** and expand the data source.

![](/images/server-side/data-sources/cloud-data-source-status-line.png)

## Statuses

After configuring a cloud data source, it may display one of the following statuses:

| **Status**       | **Description** |
|------------------|-----------------|
| **Failed**       | A connection error has occurred, such as an authentication failure, and imports are halted until the error is resolved. Row-level errors during an import do not trigger this status and are logged while the data source remains in **Running**. |
| **Inactive**     | The data source was created but was never turned on or transitioned to any other status. |
| **Initializing** | The connector is starting for the first time or resuming from a **Stopped** state. This is a temporary state before transitioning to **Running** or **Scheduled**. |
| **Running**      | The connector is actively querying and importing data. |
| **Scheduled**    | The next import is scheduled to run. This state can follow **Initializing** or **Running**. |
| **Stopped**      | The data source was previously enabled but is now turned off. No data imports occur until it is enabled. |
| **Unassigned**     | The task is awaiting allocation to a cloud worker. |

## Test configuration

We recommend that you test the data source and query before enabling data sources, segments, or activations. However, running a test may activate segments, trigger enabled actions, or affect downstream systems. To prevent unintended results, disable connectors and functions, limit test records, and coordinate with recipients.

To test your data source configuration, use the following steps:

![](/images/early-access/cloudstream/cloudstream_test_configuration.png)

1. Locate your data source in the Data Sources screen and click the edit icon.
1. Click the action button in the upper-right corner of a data source window, and then click **End-to-End Testing**.
1. Select how you want to receive the output:
    * **New Trace Session**: The output is displayed in a new trace session with up to 10 records. This option is best for confirming end-to-end verification and log details.
    * **Existing Trace Session**: The output is displayed in a trace session you have already started. Enter the **Trace ID** and click **Join Trace**.
    * **Direct Output**: The raw results from the output is displayed on the screen. No trace ID will be added to the data records and trace will not be available. This option is best for quickly confirming the query and attribute mapping.
1. Select the number of rows to process for the test. The maximum number of rows is 10.
1. Under **Test Query**, select the columns from the table to include in the test. Click the **X** in a column to remove it from the list. You must select at least one column.
1. Under **From Table**, select the table you want to query. The **Select Columns** box will update with the table’s columns.
1. Under **Where**, enter the SQL query to perform on the table.
1. Click **Check Query** to validate the SQL and verify that required fields are set.
1. The results will appear in a table under the **Query Result Preview** tab: ![](/images/early-access/cloudstream/cloudstream_test_check_query.png)
1. Click **Start Test** to start the configuration test.

The right sidebar will display a progress bar that estimates the amount of time to finish the test and status messages to let you know if the test has encountered any errors. 

![](/images/early-access/cloudstream/cloudstream_test_output.png)

When the test is complete, the results are displayed.

![](/images/early-access/cloudstream/cloudstream_test_results.png)

* If you want to watch the test run in a trace, click **Join Trace**.
* If the test fails, you can do the following:
     * Click **Edit Test Configuration** to change the configuration settings.
     * Click **Retry Test** to run the current configuration again.

## Set processing start

Data sources track the date or incrementing value position where querying begins in your cloud data view or table. You can reset or manually set that position to control where in the view or table to start querying.

For example, suppose a recent mailing list activation contained an error and processed 100 records, and now the current incrementing position is 342. To reprocess those records after correcting the email activation, set the start point to 242. When you restart the data source, it queries records starting from that position and sends the corrected email.

You can only manage the start point if the following conditions are true:

* The current profile is published.
* The query mode is **Timestamp &#43; Incrementing (Recommended)**, **Timestamp**, or **Incrementing**. You cannot manage the start point for **Full Resync** query mode.
* The data source is stopped.
    * If the data source status is running, scheduled, or failed, you cannot edit the start point. Only information about the current start point is available.
    * If the status is initializing, inactive, or there is a connection error, the start point is not available.

To manage the start point for the data source, use the following steps:

![](/images/early-access/cloudstream/manage_offset.png)

1. Locate your data source in the **Data Sources** screen and click the edit icon.
1. Click the action button in the upper-right corner of the data source details window and then click **Set Processing Start**.
1. The start point methods available are **Processing Start Timestamp** and **Incrementing Start Point**. Your query mode determines which start points are available.
1. Under **Timestamp Column**, select the column in the table that represents the timestamp.
1. Under **New Timestamp**, select a date and time to use as a starting position when importing the data.
    * The new timestamp must be a past time and date. It cannot be a future date and time.
    * The current timestamp field displays the currently used starting position.
1. Under **Incrementing column**, select the column that represents the incrementing value for each row added to the table.
1. Under **New Increment**, enter a number to use to set the start point when importing the data.
    * The new start point must be a positive integer.
    * The current start point field displays the currently used starting position to use as a start point.

Click **Validate Processing Start Changes** to preview the data that will be imported from the new start point. The table shows sample rows. It also provides an estimate of how many rows will be processed after you adjust the start point.

![](/images/early-access/cloudstream/validate_offset.png)

Click **Done** to confirm the new start point settings. Click **Cancel** to discard your changes.
Restart the data source after changing the start point.