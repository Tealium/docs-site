---
title: Google BigQuery Connector Setup Guide
description: This article describes how to set up the Google BigQuery connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/google-bigquery-connector/
---
This article describes how to set up the Google BigQuery connector.

## API Information

This connector uses the following vendor API:

* API Name: Google API
* API Version: v2
* API Endpoint: `https://bigquery.googleapis.com/bigquery/v2`
* Documentation: [Google API](https://cloud.google.com/bigquery/docs/loading-data)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100,000
* Maximum time since oldest request: 60 minutes
* Maximum size of requests: 90 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, use the following steps to authenticate to Google:

1. Select the **Authentication type**:
    * **Sign in with Google**
        1. Select your Google account and allow Tealium to access your Google Account.
        1. Click **Reload** below the **Project ID** field.
    * **Private key JSON file**: (This option is not available in the legacy connectors interface.)
        1. Navigate to **IAM & Admin > Service Accounts > Create Service Account (optional)**.
        1. Click the action menu (three dots) on the service account **Manage Keys > Add Key > Create New Key > JSON > Create**.
        1. Paste the content of the JSON key generated for your Service Account. For more information, see [Google: Using OAuth 2.0 for Server to Server Applications](https://developers.google.com/identity/protocols/oauth2/service-account#creatinganaccount). 
1. Select the **Project ID** to connect to.
1. Click **Done**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Append record | ✓ | ✓ |
| Append record batch | ✓ | ✓ |
| Execute Custom Statement | ✓ | ✓ |
| Send Entire Event Data batch | ✗ | ✓ |
| Send Entire Visitor Data batch | ✓ | ✗ |
| Send Entire Log Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Append record

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the ID of the collection of tables to connect to. |
| Table | Provide the table name to connect to. |

#### Event Parameters

Map the parameters to the columns of the table. You must map at least one parameter.

The parameters available for mapping are dependent on the dataset and table selected when the connector is configured.

### Append record batch

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100,000
* Maximum time since oldest request: 60 minutes
* Maximum size of requests: 90 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the ID of the collection of tables that you want to connect to. |
| Table | Provide the table name you want to connect to. |

#### Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between 5 and 60 minutes. The default value is 60 minutes. |

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 500
* Maximum time since oldest request: 10 minutes
* Maximum size of requests: 1 MB

### Execute custom statement

Use this action to run custom SQL statements against your BigQuery tables. 

To use this feature, map your attributes to named placeholders, which you will reference in your SQL using the `@MY_PLACEHOLDER` format. Then map data types for each mapped placeholder. For example, if you mapped an integer attribute to a placeholder named `MY_NUM_PARAM`, then map `INT64` → `MY_NUM_PARAM`.

Finally, write your SQL statement using the placeholders to dynamically substitute your mapped values at runtime.

Here's an example that shows how to execute an `INSERT` statement to add a row with a string value and a boolean value.

First, map attributes to placeholders:

![](https://docs.tealium.com/images/server-side-connectors/bigquery-custom-sql-map-values.png)

Next, map data types to the placeholders:

![](https://docs.tealium.com/images/server-side-connectors/bigquery-custom-sql-map-types.png)

Then write a SQL statement that references those placeholders:

```none
INSERT INTO bigquery_table (my_string_col, my_bool_col)
VALUES ('@MY_STRING_PARAM', @MY_BOOLEAN_PARAM);
```

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | (Required) Select the ID of the collection of tables that you want to connect to. |
| Query parameters | (Required) Map attributes to placeholder names used in the SQL query. You must map at least one parameter. |
| Query parameter type | (Required) Specify the type for each mapped parameter. Valid values are: `STRING`, `INT64`, `FLOAT64`, `BOOL`, `TIMESTAMP`, `DATE`, `TIME`, `DATETIME`, `ARRAY`, `STRUCT`. For example, if you mapped a an integer attribute to a placeholder named `MY_PARAM`, then map `INT64` to `MY_PARAM`. |
| Query | (Required) Enter the SQL statement to execute. Only a single `INSERT`, `UPDATE` or `MERGE` statement is allowed. Reference mapped parameters with the `@` symbol. For example, if you mapped a boolean attribute to `MY_BOOLEAN_PARAM`, then use `@MY_BOOLEAN_PARAM` in the SQL where that value should appear. |
| Batch Time To Live | Set the time to live (TTL) with a value between 1 and 60 minutes. The default value is 10 minutes. |

### Send Entire Event Data batch

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100,000
* Maximum time since oldest request: 60 minutes
* Maximum size of requests: 90 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the ID of the collection of tables that you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Timestamp | Choose the column to record the timestamp. |
| Column to record the Payload | Choose the column to record the payload. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send it in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) with a value between 5 and 60 minutes. The default value is 60 minutes. |

### Send Entire Visitor Data batch

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100,000
* Maximum time since oldest request: 60 minutes
* Maximum size of requests: 90 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the ID of the collection of tables that you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Timestamp | Choose the column to record the timestamp. |
| Column to record the Payload | Choose the column to record the payload. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send it in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Include Current Visit Data with Visitor Data | Include the current visit data with the visitor data. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between 5 and 60 minutes. The default value is 60 minutes. |

### Send Entire Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the ID of the collection of tables that you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Timestamp | Choose the column to record the timestamp. |
| Column to record the Payload | Choose the JSON column to record the payload. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send it in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Dataset | Select the ID of the collection of tables that you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Log event resource attributes | These fields capture information about the entity for which telemetry is recorded. |
| Log event HTTP attributes | These fields log HTTP requests and responses in the logging system. To map the entire HTTP array to a single column, map the `http` attribute. If the target column type is JSON, the raw array is sent. Otherwise, the array is converted to a string. |
| Log event result attributes | These fields log the outcome of the operation, detailing whether it was successful or if it encountered errors. |
| Log event other attributes | These fields provide additional metadata about the logged events. |
