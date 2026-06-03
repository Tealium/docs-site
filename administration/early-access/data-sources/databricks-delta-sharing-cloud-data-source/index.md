---
title: Databricks Delta Sharing cloud data source
description: This article describes how to set up the Databricks Delta Sharing cloud data source.
url: https://docs.tealium.com/administration/early-access/data-sources/databricks-delta-sharing-cloud-data-source/
---
 The Databricks Delta Sharing cloud data source is currently in Early Access and is available to select customers only. Contact Tealium Support to get started with Databricks Delta Sharing. 

For a general overview of setting up a cloud data source, see .

## How it works

The Databricks Delta Sharing cloud data source uses the Databricks-to-Databricks sharing protocol. This protocol securely shares data assets between Databricks and Tealium.

In this protocol, you are the provider and Tealium is the recipient. You create shares in Databricks and grant Tealium access to those shares. Shares are collections of read-only tables and assets.

You configure the secure connection to Tealium in Databricks using the Tealium sharing identifier (metastore ID). No database usernames, passwords, or access tokens leave Databricks.

When used with [CloudStream](), the data pipeline is zero-copy. Data remains in your Databricks environment and is accessed on demand for activation.

## Data types

The Databricks Delta Sharing data source supports all Databricks data types. To ensure data is imported correctly, map the Databricks data types according to the following guidelines:

| Databricks | Tealium |
|:----------|:--------|
| Numeric data types  | Number attributes |
| String and binary data types | String attributes |
| Logical data types | Boolean attributes|
| Date and time data types| Date attributes |
| Arrays | Array of strings, array of numbers, or array of booleans|
| Map, struct, object, variant | String attributes |

For more information, see Databricks: Data Types ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-datatypes), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-datatypes), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-datatypes)).

## Create a connection

 Users must have the following Databricks Unity Catalog permissions to configure Delta Sharing: `CREATE RECIPIENT`, `CREATE SHARE`, `USE CATALOG`, `USE SCHEMA`, and `SELECT`. A metastore admin already has these permissions. 

To create a connection with Databricks Delta Sharing, complete the following steps in Databricks:

1. Enable Delta Sharing in the Databricks Unity Catalog metastore that contains the data you want to share.  
For more information, see Databricks: Enable Delta Sharing on a metastore ([AWS](https://docs.databricks.com/aws/en/delta-sharing/set-up#enable), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/set-up#enable), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/set-up#enable)). 
1. Create a share with the tables, views, or catalogs that you plan to share with Tealium.  
For more information, see Databricks: Create and manage shares for Delta Sharing ([AWS](https://docs.databricks.com/aws/en/delta-sharing/create-share), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/create-share), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/create-share)).
1. Create a recipient. Contact Tealium Support for the `metastore_id` that you need to create the Tealium recipient.  
For more information, see Databricks: Create and manage data recipients for Delta Sharing (Databricks-to-Databricks sharing) ([AWS](https://docs.databricks.com/aws/en/delta-sharing/create-recipient), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/create-recipient), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/create-recipient)).
1. Grant Tealium access to one or more shares.  
For more information, see Databricks: Manage access to Delta Sharing data shares (for providers) ([AWS](https://docs.databricks.com/aws/en/delta-sharing/grant-access), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/grant-access), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/grant-access)).
1. Contact Tealium Support to create the connection for you. Tealium Support will need your Databricks Workspace name to create the connection.

Complete the following steps in Tealium to create a Databricks Delta Sharing cloud data source: 

1. After Tealium Support creates the connection for you, create a Databricks Delta Sharing cloud data source in Tealium. For more information, see .
1. Click **Establish Connection**. Establishing the Delta Sharing connection to Databricks may take up to 2-3 minutes.

## Query configurations

For a general overview, see .

For Databricks Delta Sharing, note the following requirements:

* **Timestamp &#43; Incrementing** and **Timestamp** query modes: The selected timestamp column must be the type `TIMESTAMP`.  
For more information, see Databricks: TIMESTAMP type ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/data-types/timestamp-type), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/data-types/timestamp-type), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/data-types/timestamp-type)).
* **Incrementing** query mode: The selected numeric column must increment in value for every row added. A recommended definition for an auto-increment column is:

```sql
COL1 BIGINT GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1)
```

For more information, see Databricks `CREATE TABLE` ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-ddl-create-table-using), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using)).

## IP access list

If your Databricks workspace is restricted by IP addresses, add the [Tealium IP addresses]() to your Databricks IP access list.

For more information, see Databricks: Manage IP access list ([AWS](https://docs.databricks.com/aws/en/security/network/front-end/ip-access-list), [Azure](https://learn.microsoft.com/en-us/azure/databricks/security/network/front-end/ip-access-list), [GCP](https://docs.databricks.com/gcp/en/security/network/front-end/ip-access-list)).
