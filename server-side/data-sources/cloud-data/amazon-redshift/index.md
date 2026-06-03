---
title: Amazon Redshift cloud data source
description: This article describes how to set up the Amazon Redshift cloud data source.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/amazon-redshift/
---
For a general overview of setting up a cloud data source, see .

## Data types

The Amazon Redshift data source supports all Amazon Redshift data types. To ensure data is imported correctly, map the Amazon Redshift data types according to the following guidelines: 

| Amazon Redshift | Tealium |
|:----------|:--------|
| Numeric types  | Number attributes |
| Strings, multibyte characters, SUPER, and VARBYTE types| String attributes |
| Boolean type | Boolean attributes|
| Datetime types | Date attributes |

For more information, see [Amazon Redshift: Data types](https://docs.aws.amazon.com/redshift/latest/dg/c_Supported_data_types.html).

## Create a connection

Tealium uses JDBC to connect to Amazon Redshift. This process requires the full JDBC URL, username, and password of your cluster.

The JDBC URL uses the following format:  
`jdbc:redshift://hostname:port/database`

To configure a new connection, enter the following connection details: 

* **Hostname**: The hostname of the Amazon Redshift cluster. For example, `examplecluster.abc123xyz789.us-west-2.redshift.amazonaws.com`
* **Port**: The port number that you specified when you launched the cluster.
* **Database**: The database to connect to.
* **Schema**: The schema to connect to.

After you connect to Amazon Redshift, select a table or view from the **Data Selection** list.

For more information, see [Amazon Redshift: Getting the JDBC URL](https://docs.aws.amazon.com/redshift/latest/mgmt/jdbc20-obtain-url.html).

## Query configurations

For a general overview, see .

For query modes that use **Timestamp**, the selected timestamp column must be the type `TIMESTAMP` or `TIMESTAMPTZ`.

For more information, see [Amazon Redshift: TIMESTAMP](https://docs.aws.amazon.com/redshift/latest/dg/r_Datetime_types.html).

For query modes that use **Incrementing**, the selected numeric column must be one of the integer types and increment in value for every row added.

For more information, see [Amazon Redshift: Integer types](https://docs.aws.amazon.com/redshift/latest/dg/r_Numeric_types201.html#r_Numeric_types201-integer-types).

