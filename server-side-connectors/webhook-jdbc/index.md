---
title: Webhook JDBC Connector Setup Guide
description: Connect this webhook connector to a JDBC-compatible database to write event or visitor data directly into your tables, either by storing the full JSON payload or mapping individual attributes to specific columns.
url: https://docs.tealium.com/server-side-connectors/webhook-jdbc/
---
To use a webhook to send data to an HTTP API endpoint, see [About webhook connectors]().

This connector is compatible with the following databases:

* Amazon Redshift
* MariaDB
* MySQL
* PostgreSQL
* SQL Server

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following three thresholds is met:

* Max number of requests: 1,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

## Configuration

Go to the connector marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Username**: The username to log into your database from Tealium. For security reasons, allow this user to connect only from these [IP addresses]().
* **Password**: The password for the username provided.
* **JDBC URL**: The fully qualified JDBC URL to establish the connection (for example, `jdbc:postgresql://host:5432/dbname?p1=a&amp;p2=b`).
* **Additional properties**: A set of comma-separated pairs to pass as properties when establishing the connection. For example, `prop1=a,prop2=b` results in the following adjustment to the connection:

    ```java
    props.setProperty(&#34;prop1&#34;, &#34;a&#34;);
    props.setProperty(&#34;prop2&#34;, &#34;b&#34;);
    Connection conn = DriverManager.getConnection(url, props);
    ```

### Column data types

To make it easier to map attributes to table columns, the columns appear with their data type appended to the name. For example, if you have a column named `customer_id` of type `VARCHAR`, it appears in the mapping list as `customer_id//VARCHAR`.

### Batch configuration

All actions that support batch processing support the following parameters:

| **Parameter** | **Description** |
| --- | --- |
| Batch time to live | Set the time to live (`TTL`) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |
| Max query size | Set the maximum size of the query in megabytes. The default value is `1`. The maximum value is `100`. |

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Execute Custom Query | ✓ | ✓ |

### Send Entire Event Data

Use this action to send the entire event JSON object to a single table column.

For more information, see .

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Schema | The schema name you want to connect to. |
| Table | The table name you want to connect to. |
| Payload | Choose the column to store the JSON data object. |
| Timestamp | Choose the column to record the timestamp. |
| Timestamp Attribute | Select an attribute to assign as the timestamp to send the timestamp in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Print Attribute Names | If attribute names get updated, the names in the payload reflect the update. |

### Send Custom Event Data

Use this action to send specific event attributes to specific table columns.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Schema | The schema name to connect to. |
| Table | The table name to connect to. |
| Upsert | Select to update the data if a record with the same key already exists. To perform an update operation in the database, you must map an attribute to a primary key column.|

### Send Entire Log Event

For more information, see .

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Schema | The schema name to connect to. |
| Table | The table name to connect to. |
| Payload | Choose the column to store the JSON data object. |
| Timestamp | Choose the column to record the timestamp. |
| Timestamp Attribute | An attribute to assign as the timestamp to send the timestamp in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |

### Send Log Event

For more information, see .

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Schema | The schema name to connect to. |
| Table | The table name to connect to. |

#### Log event resource attributes

These fields capture information about the entity for which telemetry is recorded.

#### Log event HTTP attributes

These fields log the HTTP requests and responses within the logging system.

If you want to map the entire HTTP array to a single column, map the `http` attribute. If the target column is of type `VARIANT`, the raw array is sent; otherwise, it is converted to a string.

#### Log event result attributes

These fields log the outcome of the operation, detailing whether it was successful or if it encountered errors.

#### Log event other attributes

These fields provide additional metadata about the logged events.

### Send Entire Visitor Data

Use this action to send the entire visitor JSON object to a single table column.

For more information, see .

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Schema | The schema name to connect to. |
| Table | The table name to connect to. |
| Payload | Choose the column to store the JSON data object. |
| Timestamp | Choose the column to record the timestamp. |
| Timestamp Attribute | Select an attribute to assign as the timestamp to send the timestamp in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Include Current Visit Data With Visitor Data | Select to include the current visit data with visitor data. This includes event visit data, unless **Exclude Current Visit Data** is selected. |
| Exclude Current Visit Event Data | Select to exclude event data from the current visit data. |
| Print Attribute Names | If attribute names get updated, the names in the payload reflect the update. |

### Send Custom Visitor Data

Use this action to send specific visitor attributes to specific table columns.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Schema | The schema name to connect to. |
| Table | The table name to connect to. |
| Upsert | Select to update the data if a record with the same key already exists. To perform an update operation in the database, you must map an attribute to a primary key column.|

### Execute Custom Query

Use this action to run custom SQL statements.

Only `INSERT`, `UPDATE` or `MERGE` statements are allowed, but they can include `SELECT` sub-queries. Including multiple `INSERT`, `UPDATE` or `MERGE` statements within the same query causes an error.

To use this feature, map your attributes to named placeholders, that you reference in your SQL using the `:MY_PLACEHOLDER` format. For example, if you map a boolean attribute to a placeholder named `:my_bool_param`, then reference `:my_bool_param` in the query where you want that value to be replaced by the mapped attribute&#39;s value.

Examples:

```sql
-- Example
INSERT INTO redshift_table
(col1, col2) VALUES (:col1Value, :col2Value)

-- Example
UPDATE redshift_table
SET col1 = :col1Value, col2 = :col2Value
WHERE col3 = :col3Value

-- Example
UPDATE redshift_table
SET col2 = (
  SELECT new_col2 FROM source_table WHERE source_table.col1 = redshift_table.col1
)
WHERE EXISTS (
  SELECT 1 FROM source_table WHERE source_table.col1 LIKE :col1Value
);
```

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Schema | The schema name to connect to. |
| Query Parameters | Map the parameters to the placeholder to replace in the query. Parameters must use the format: `:ParameterName`. You must map at least one parameter. |
| Query | The raw statement to pass into the `SQL` attribute. |