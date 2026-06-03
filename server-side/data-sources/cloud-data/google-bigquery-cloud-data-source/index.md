---
title: Google BigQuery cloud data source
description: This article describes how to set up the Google BigQuery cloud data source.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/google-bigquery-cloud-data-source/
---For a general overview of setting up a cloud data source, see .

## Data types

The Google BigQuery data source supports all Google BigQuery data types. To ensure data is imported correctly, map the Google BigQuery data types according to the following guidelines: 

| Google BigQuery | Tealium |
|:----------------|:--------|
| Numeric data types  | Number attributes |
| String and binary data types | String attributes |
| Logical data types | Boolean attributes|
| Date and time data types| Date attributes |
| Arrays | Array of strings, array of numbers, or array of booleans|
| JSON | String attributes |
| STRUCT | See [Importing STRUCT columns](#importing-struct-columns).

For more information, see [Google BigQuery: Data types](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types).

## Create a connection

Tealium uses the OAuth 2.0 flow to authenticate with Google. This process requires a service account and a private key file.

The service account must have the following BigQuery IAM roles:

* [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer)
* [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser)

To generate a public/private key pair:

1. Go to **Google Cloud &gt; Service Accounts** and select a project or create one.
1. Select your service account or create one, then go to the **Keys** tab and choose **Add key &gt; Create new key**.
1. Select the **JSON** option and click **Create**.  
Your private key is generated and downloaded to your machine.

To configure a new connection, enter the following connection details: 

* **Dataset**: The name of the dataset within the specified project. Do not include the project name.
* **Project ID**: The project ID of your Google Cloud project.
* **Service Account Email Address**: The generated email address for the service account.
* **Key File**: Upload the generated private key file for the service account or select a previously uploaded key file.

After you connect to Google BigQuery, select a table or view from the **Data Selection** list.

For more information, see [Google for Developers: Using OAuth 2.0 for Server to Server Applications](https://developers.google.com/identity/protocols/oauth2/service-account#creatinganaccount).

## Query batch size

The default query batch size is 1,000 records per batch. Changing the query batch size from the default may require additional permissions. To grant permissions to change the query size limit, go to **Google Cloud console &gt; IAM menu &gt; Select the appropriate service account &gt; Grant Access &gt; Add BigQuery Read Session User Role**. For example, enter `BigQuery Read Session User (roles/bigquery.readSessionUser)`. For more information, see [Google: BigQuery IAM roles and permissions](https://docs.cloud.google.com/bigquery/docs/access-control) and .

## Query configurations

For a general overview, see .

For query modes that use **Timestamp**, the selected timestamp column must be the type `TIMESTAMP`.

For more information, see [Google BigQuery: TIMESTAMP](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#timestamp_type).

For query modes that use **Incrementing**, the selected numeric column must increment in value for every row added. Use whole number types, such as `INT64` instead of `FLOAT` or `DECIMAL`.

For more information, see [Google BigQuery: Numeric types](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_types).

### Importing STRUCT columns

BigQuery `STRUCT` columns cannot be imported directly into Tealium. To import data from a `STRUCT` column, create a view with the `STRUCT` fields flattened into separate columns.

For example, you might have addresses defined as a `STRUCT`:

```sql
shipping_address STRUCT&lt;
  street STRING,
  city STRING,
  state STRING,
  postal_code STRING,
  country STRING
&gt;
```

To create a view with these address fields flattened into separate columns, use a SQL statement like this:

```sql
CREATE OR REPLACE VIEW ecommerce.order_shipping_view AS
SELECT
  order_id,
  customer_id,
  shipping_address.country AS country,
  shipping_address.postal_code AS postal_code
FROM
  ecommerce.orders;  
```

The flattened `STRUCT` columns can be imported and mapped like the other supported data types.