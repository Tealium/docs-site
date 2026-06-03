---
title: Trino cloud data source
description: This article describes how to set up the Trino cloud data source.
url: https://docs.tealium.com/administration/early-access/data-sources/trino-cloud-data-source/
---
 The Trino cloud data source is currently in Early Access and is available to select customers only. Contact Tealium Support to get started with Trino. 

For a general overview of setting up a cloud data source, see .

## Data types

The Trino data source supports all Trino data types. To ensure data is imported correctly, map the Trino data types according to the following guidelines: 

| Trino | Tealium |
|:----------|:--------|
| Integer types (SMALLINT, INTEGER, BIGINT), decimal, and floating-point types (REAL, DOUBLE) | Number attributes |
| Character types (CHAR, VARCHAR), binary types (VARBINARY), UUID, IPADDRESS, and JSON | String attributes |
| Boolean type | Boolean attributes|
| Date and time types (DATE, TIME, TIMESTAMP) | Date attributes |
| Arrays | Array of strings, array of numbers, or array of booleans|
| Map, Row, and other complex types | String attributes |

For more information about Trino data types, see [Trino: Data types](https://trino.io/docs/current/language/types.html).

## Create a connection

The Tealium Trino cloud data source supports username and password authentication. To configure a new connection, enter the following connection details:

* **Trino Connection Configuration Name**: Provide a name for the reusable connection configuration.
* **Hostname**: The hostname of your Trino server. Do not include the `http://` or `https://` prefix.
* **Port**: (Optional) The port number for your Trino server. If not specified, the default port 8080 is used.
* **Catalog**: The name of the catalog to connect to.
* **Schema**: (Optional) The name of the schema to connect to within the catalog.

### Authentication

To authorize a Trino connection, enter the following credentials:

* **Username**: The username for authentication to the Trino server.
* **Password**: The password associated with the username.

After you connect to Trino, select the data source table from the **Table Selection** list.

## Query configurations

For a general overview, see .

For Trino, note the following requirements:

* **Timestamp &#43; Incrementing** and **Timestamp** query modes: The selected timestamp column must be the type `TIMESTAMP` or `TIMESTAMP WITH TIME ZONE`.  
For more information, see [Trino: Date and time types](https://trino.io/docs/current/language/types.html#date-and-time).
* **Incrementing** query mode: The selected numeric column must increment in value for every row added and must be one of the integer types (SMALLINT, INTEGER, or BIGINT).

For more information about Trino data types, see [Trino: Data types](https://trino.io/docs/current/language/types.html).
