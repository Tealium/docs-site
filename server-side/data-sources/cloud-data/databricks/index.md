---
title: Databricks cloud data source
description: This article describes how to set up the Databricks cloud data source.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/databricks/
---
For a general overview of setting up a cloud data source, see .

## Data types

The Databricks data source supports all Databricks data types. To ensure data is imported correctly, map the Databricks data types according to the following guidelines: 

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

Tealium uses a service principal to access your Databricks compute resource. Before you proceed, you must create a service principal in Databricks and generate an OAuth secret. For more information, see [Databricks: Authorize access with a service principal using OAuth](https://docs.databricks.com/aws/en/dev-tools/auth/oauth-m2m).

 Databricks personal access tokens (PAT) are not supported. For more information, see Databricks: Authenticate with Databricks personal access token (legacy) ([AWS](https://docs.databricks.com/aws/en/dev-tools/auth/pat), [Azure](https://learn.microsoft.com/en-us/azure/databricks/dev-tools/auth/pat), [GCP](https://docs.databricks.com/gcp/en/dev-tools/auth/pat)). 
 
To configure a new connection, enter the following connection details: 

* **Hostname**: The hostname of your Databricks compute resource. Examples:
  * AWS: `MY_ACCOUNT.cloud.databricks.com`
  * Azure: `MY_ACCOUNT.azuredatabricks.net`
  * GCP: `MY_ACCOUNT.gcp.databricks.com`
* **HTTP Path**: The HTTP path to your compute resource. For example: `/sql/1.0/warehouses/3fbc78304284503a`. To find the HTTP Path, go to the **SQL Warehouses** screen in Databricks, select the warehouse where your table is located, and click **Connection details**.
* **Catalog**: The name of the catalog for this connection.
* **Schema**: The name of the schema for this connection.
* **OAuth Client ID**: The service principal&#39;s UUID or Application ID.
* **OAuth Client Secret**: The service principal&#39;s generated secret.

For more information, see Databricks: Compute settings ([AWS](https://docs.databricks.com/aws/en/integrations/jdbc/compute), [Azure](https://learn.microsoft.com/en-us/azure/databricks/integrations/jdbc/compute), [GCP](https://docs.databricks.com/gcp/en/integrations/jdbc/compute)).

After you connect to Databricks, select the data source table from the **Table Selection** list.

## Query configurations

For a general overview, see .

For Databricks, note the following requirements:

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
