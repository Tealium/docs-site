---
title: About cloud data sources
description: This article describes how to import data from a cloud datawarehouse or database.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/about/
---
## Requirements

This feature requires the following:

* Tealium EventStream, Tealium AudienceStream, or Tealium CloudStream

## Supported vendors

The configuration for cloud data sources is nearly the same for every vendor. For an overview, see [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/).

For vendor-specific configuration details, see the following:

* [Amazon Redshift](https://docs.tealium.com/amazon-redshift-cloud-data-source/)
* [Databricks](https://docs.tealium.com/databricks-cloud-data-source/)
* [Google BigQuery](https://docs.tealium.com/google-bigquery-cloud-data-source/)
* [Snowflake](https://docs.tealium.com/about-snowflake-cloud-data-source/)

## How it works

A cloud data source connects your cloud data warehouse or database to Tealium, so you can import data as events for processing. The process involves several key components:

* **Connection**:  
  Set up a secure reusable connection to your cloud data source by providing the necessary credentials and authentication details.
* **Processing**:  
  Configure the data processing frequency and batch size. 
* **Query configuration**: 
  Select from a Basic or Advanced query configuration. Basic lets you select the columns to import from your default schema and refine that data using a SQL `WHERE` clause. Advanced lets you join multiple tables and use advanced SQL commands to have full control over your data processing. In either configuration, use the query modes to control how new or updated rows are detected—using a timestamp column, an incrementing column, or both.
* **Column mapping**:  
  Map the columns from your cloud database to Tealium event attributes. This ensures that data from your source is correctly assigned to the appropriate attributes in Tealium.
* **Visitor ID mapping**:  
  To unify data across sources, map a column from your data source to a visitor ID attribute in AudienceStream. This enables accurate visitor stitching and profile enrichment.

Each imported row is processed as an event in Tealium, which lets you bring in bulk data from your cloud systems and use it alongside other event data for real-time processing, segmentation, and activation.


<blockquote>
A maximum of 10 cloud data warehouse data sources per profile can be enabled at a time.
</blockquote>


## Event processing

Each imported row is processed as an event with columns mapped to event attributes. Columns not mapped to an event attribute are ignored. 

In the default Tealium [data collection order of operations](https://docs.tealium.com/server-side-order-of-operations/), events from a cloud data source are processed before the **Event received** step and do not change the order of operations.

Cloud data source rows are processed in EventStream and AudienceStream in the same way as events from other data sources, but with the following important exceptions:

* **Browser-specific attributes**: Browser-specific attributes, such as `User agent`, are not set.
* **Enrichments**: AudienceStream enriches only the `First visit` preloaded attribute. All other enrichments for preloaded attributes are skipped.
* **Single-page visits**: Incoming events are exempt from the single-page visit  criteria. Single-page visits and visitors from other data sources are not persisted in AudienceStream. For more information, see [How are single-page visits processed in AudienceStream?](https://docs.tealium.com/single-event-visitor/)
* **Visit length**: A visit started by a cloud data source event lasts for 60 seconds.
* **Visitor ID mapping**: If you map an AudienceStream visitor ID attribute in your cloud data source configuration, the visitor ID is set directly to the value of the column you choose without the need for an enrichment.

### Scheduling

The **Processing Settings** section controls how and when your cloud data source imports new data. You can enable or disable processing and configure the frequency at which data is imported. Each import processes data in batches of 1,000 rows.

### Frequency

Select how often to import data:

| **Option**         | **Description**                                                |
| ------------------ | -------------------------------------------------------------- |
| **Near Real-Time** | Fetches data every 2 seconds. Ideal for low-latency use cases. |
| **Hourly**         | Runs at the beginning of every hour.                           |
| **Daily**          | Runs once per day at the hour of the day you set (UTC).                |
| **Weekly**         | Runs once per week at the day and hour you set (UTC).          |


<blockquote>
Fetching data with high frequency (near real-time or hourly) may lead to increased costs and system strain in your data warehouse.
</blockquote>


### Batch size

The cloud data sources import data in batches, with a default of 1,000 rows per batch. This limit applies to the size of each batch, not the total number of rows processed in an import. Each scheduled import continues processing until all available rows are ingested, regardless of how many batches are required.

Select from one of the following batch options:

* **Default**: 1,000 records per batch.
* **Custom**: Create custom batches of over 1,000 records. 
* **No limit**: Create a batch with no limit to process all available data.

Optimizing the query batch size for your use case can have the following benefits:

* **Reduced compute costs**: Lowers computational expenses within your external data warehouses and databases.
* **Improved data integrity**: Prevents the system from retrieving repeated records that can result from repeated timestamps.

Your cloud provider may calculate billing based on the number of queries or the size of queries.

This behavior is important to consider when selecting a [query mode](#query-mode-batch-processing-behavior).

### Rate limits

Imports from cloud data sources are typically limited to 200 events per second per account, but may vary. Standard attribute size limits still apply. For more information, see [About attributes > Size limits](https://docs.tealium.com/about-attributes/#size-limits).

## Query configurations

Tealium data sources support two configurations to process data: basic and advanced. 

* Basic mode: Your data is imported using the default schema you specify in the data source configuration. You can process data from only one table or view. Optionally include a SQL `WHERE` clause to import only those records that match your custom condition. 
* Advanced mode: You can select one or more tables to join using an advanced SQL editor. The tables can be from multiple schemas. The SQL editor supports advanced SQL commands, such as `CAST` and `JOIN`.

### Data types

The cloud data source supports all data types. In general, use the following data type mappings to ensure data is imported correctly: 

| Cloud data    | Tealium |
|:--------------|:--------|
| Numeric       | Number attributes |
| String        | String attributes |
| Logical       | Boolean attributes|
| Date and time | Date attributes |
| Arrays        | Array of strings, array of numbers, or array of booleans|
| Other         | String attributes |

For more vendor-specific data types, see:

* [Amazon Redshift](https://docs.tealium.com/amazon-redshift-cloud-data-source/#data-types)
* [Databricks](https://docs.tealium.com/databricks-cloud-data-source/#data-types)
* [Google BigQuery](https://docs.tealium.com/google-bigquery-cloud-data-source/#data-types)
* [Snowflake](https://docs.tealium.com/snowflake-cloud-data-source/#data-types)

### Query modes

The cloud data source supports the following three query modes to control how data is imported from your table or view:

* Timestamp + Incrementing
* Timestamp
* Incrementing

Each mode uses a timestamp column, an increment column, or both to determine which rows to import.

#### Requirements for columns

To ensure a query mode works effectively, you must have one or both of the following:

* **Timestamp column**  
A timestamp column set to the current time when a row is added or modified. If the timestamp column is not properly set, rows may never be read or may be read more than once.
* **Increment column**  
A numeric column that increments in value for every row added. A recommended definition for an auto-increment column is:
  ```sql
  COL1 NUMBER AUTOINCREMENT START 1 INCREMENT 1
  ```
  This definition results in an always ascending unique key as new rows are added. If there is not an always ascending unique key, rows may never be read or may be read more than once.

For vendor-specific requirements, see:

* [Amazon Redshift](https://docs.tealium.com/amazon-redshift-cloud-data-source/#query-configurations)
* [Databricks](https://docs.tealium.com/databricks-cloud-data-source/#query-configurations)
* [Google BigQuery](https://docs.tealium.com/google-bigquery-cloud-data-source/#query-configurations)
* [Snowflake](https://docs.tealium.com/snowflake-cloud-data-source/#query-configurations)

Select a mode that aligns with the requirements of your use case. For an example of how these modes work, see [Query mode batch processing behavior](#query-mode-batch-processing-behavior).

#### Timestamp + Incrementing (Recommended)

This mode uses both a timestamp column and an incrementing column to import new or modified rows.

Rows are imported if they have a newer timestamp than the previous import, or the same timestamp with a higher increment value.

This mode provides the highest reliability for ensuring that all rows are imported as intended.

#### Timestamp

This mode uses a timestamp column to import new or updated rows.

Rows are imported only if they have a newer timestamp than the previous import. If you attempt to import rows with the same timestamp, rows with duplicate timestamps may not be imported.

Use this mode if your table has a timestamp column set on every insert or update operation.

#### Incrementing

This mode uses an incrementing column to import rows.

Rows are imported if they have a larger increment value than the last imported row. Rows with an increment value less than or equal to the maximum value from the previous import are skipped. This mode does not detect modifications to existing rows.

Use this mode if your table does not have a timestamp column.

If you maintain your own increment column, as opposed to using an auto-increment column, ensure that the values always increase. 

#### Query mode batch processing behavior

Each query mode determines what boundary values the system records at the end of a batch. The next batch uses these recorded values to determine which rows to fetch.

| Query mode | Values recorded at batch boundary |
|---|---|
| Timestamp + Incrementing | Last timestamp value and last increment value |
| Timestamp | Last timestamp value only |
| Incrementing | Last increment value only |

The following example shows how these batch boundaries affect which rows are imported in the next batch.

In this example, a cloud data source fetches data in serial batches of 1,000 rows per scheduled run and continues until no records are returned. Depending on which query mode you use, row 1001 may or may not be imported.

In the following table, `modification_time` is the timestamp column, `customer_id` is the incrementing column, and Batch indicates the batch that the rows are processed in.

| `customer_id` | `modification_time` | `customer_segment` | Batch |
|---------------|---------------------|--------------------|-------|
| `1`           | `01Apr 13:00`       | `A`                | A     |
| `2`           | `01Apr 13:00`       | `B`                | A |
| ...           | ...                 | ...                | A |
| `1000`        | `01Apr 13:00`       | `D`                | A |
| `1001`        | `01Apr 13:00`       | `E`                | ? |
| `1002`        | `02Apr 14:00`       | `A`                | B |

After processing Batch A (rows 1-1000), the system records the maximum values found depending on the selected query mode. The next batch uses these values to determine which rows to fetch.

#### Timestamp + Incrementing

Using the Timestamp + Incrementing mode successfully processes all rows with the following SQL queries:

**Batch A** query:

```sql
SELECT * FROM customers
WHERE modification_time < NOW()
ORDER BY modification_time, customer_id ASC
LIMIT 1000
```

After Batch A finishes processing, the system records:

* Final batch timestamp: `01Apr 13:00`
* Final batch ID: `1000`

**Batch B** query:

```sql
SELECT * FROM customers
WHERE modification_time < NOW()
AND ((modification_time = '01Apr 13:00' AND customer_id > 1000)
OR modification_time > '01Apr 13:00')
ORDER BY modification_time, customer_id ASC
LIMIT 1000
```

Row 1001 is successfully imported because it has the same timestamp with a higher ID value. Row 1002 is imported because it has a newer timestamp.

#### Incrementing

Using the Incrementing mode, rows added after each batch are processed, but modifications to existing rows may not be detected.

**Batch A** query:

```sql
SELECT * FROM customers
ORDER BY customer_id ASC
LIMIT 1000
```

After Batch A finishes processing, the system records:

* Final batch ID: `1000`

**Batch B** query:

```sql
SELECT * FROM customers
WHERE customer_id > 1000
ORDER BY customer_id ASC
LIMIT 1000
```

Rows 1001 and 1002 are imported because they have higher ID values. However, if any rows from 1-1000 were modified after Batch A, those updates are not detected.

#### Timestamp (`modification_time` in the example)

Using the Timestamp mode results in missing rows.

**Batch A** query:

```sql
SELECT * FROM customers
WHERE modification_time < NOW()
ORDER BY modification_time ASC
LIMIT 1000
```

After Batch A finishes processing, the system records:

* Final batch timestamp: `01Apr 13:00`

**Batch B** query:

```sql
SELECT * FROM customers
WHERE modification_time > '01Apr 13:00'
ORDER BY modification_time ASC
LIMIT 1000
```

The system skips row 1001 because it has the same timestamp value as the previous batch boundary. Only row 1002 is imported.


<blockquote>
When thousands of records share the same timestamp at a batch boundary, entire batches can be skipped. Records sharing the same timestamp is a common problem for bulk imports into the source data warehouse where many records are inserted or updated simultaneously.
</blockquote>


## Column mapping

The column mapping configuration determines the event attributes that correspond to each column in the cloud database table. 

Column names are often different from the attribute names in your Tealium account, so this mapping ensures that the data is imported properly. For example, if your table uses the column name `postalCode` but the event attribute in Tealium is `customer_zip`, create a mapping to associate these fields.

For information about mapping cloud data types to Tealium data types, see the [Data Types](#data-types) section.

For vendor-specific data types, see the following:
* [Amazon Redshift](https://docs.tealium.com/amazon-redshift-cloud-data-source/#data-types)
* [Databricks](https://docs.tealium.com/databricks-cloud-data-source/#data-types)
* [Google BigQuery](https://docs.tealium.com/google-bigquery-cloud-data-source/#data-types)
* [Snowflake](https://docs.tealium.com/snowflake-cloud-data-source/#data-types)

## Visitor ID mapping

To ensure your imported data is stitched with other sources, such as web, mobile, or HTTP API, ensure that every row in the table has a column with a unique visitor ID.

Map the visitor ID column and corresponding event attribute to a visitor ID attribute (a unique attribute type for visitor identification in AudienceStream). The value in the mapped event attribute is assigned to the `tealium_visitor_id` attribute and matched directly to any existing visitor profiles.

For more information about Visitor ID Mapping in AudienceStream, see [Visitor Identification using Tealium Data Sources](https://docs.tealium.com/visitor-identification-data-sources/).

## IP addresses to allow

If your cloud data account has strict rules about which systems it accepts requests from, add the [Tealium IP addresses]() to your cloud database allowlist.

