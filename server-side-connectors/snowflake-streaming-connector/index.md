---
title: Snowflake Streaming Connector Setup Guide
description: This article describes how to set up the Snowflake Streaming connector.
url: https://docs.tealium.com/server-side-connectors/snowflake-streaming-connector/
---
## API information 

This connector uses the following vendor SDK:

* Snowflake Ingest SDK Version: 4.4.2

## How it works

The Snowflake Streaming connector leverages the powerful Snowflake Snowpipe Streaming feature to enable near real-time importing of event and visitor data directly into Snowflake staging tables, enabling immediate availability for processing and analytics with data latency under 10 seconds. Send either the entire dataset or specific attributes to the staging table, ensuring customizable data integration tailored to business needs.

Using Snowpipe Streaming creates a streamlined pathway to enhance data accessibility and analytical capabilities within Snowflake while decreasing latency and costs. By removing third party integrations and using the Snowpipe Streaming serverless compute model, the Snowflake Streaming connector provides a cost effective, secure connection.

The Snowflake Streaming connector unlocks a number of use cases, including:

* Identity: Populate and activate identity graphs using cleansed, normalized, real-time identity data.
* Insights: Improve and activate differentiated intelligence with rich, high quality, integrated data.
* AI: Inform and activate AI initiatives with a real-time data layer.
* Consent: Ensure insights and activation always respect customer privacy and preferences.

### Staging tables

The staging table in Snowflake that is intended to receive data from Tealium must contain specific columns depending on the selected connector action.

When using either **Send Entire Event Data** or **Send Entire Visitor Data** actions, the staging table must have a `VARIANT` column to receive the dataset and a column to receive the timestamp. The timestamp column must support the timestamp data format that is sent.

When using either **Send Custom Event Data** or **Send Custom Visitor Data**, the staging table must have a column for each data type. Each data attribute must be assigned to a column. Ensure that each attribute is an accepted Snowflake data type and that the column is formatted properly to receive this data type. To map a timestamp, a separate timestamp column must be added.

For more information, see [Snowflake: Supported Java data types](https://docs.snowflake.com/en/user-guide/data-load-snowpipe-streaming-overview#supported-java-data-types).

### Data types

The following table summarizes the data types supported by the Snowflake Streaming connector:

| **Snowflake Data Type** | **Supported** |
| --- | --- |
| Numeric data types | ✓ |
| String and binary data types | ✓ |
| Logical data types |✓ |
|Date and time data types | ✓ |
| Arrays | ✓ |
| Object | ✓ |
| Variant |✓|
| Vector | ✗|
| Geography | ✗|
| Geometry | ✗ |

### Table and column configurations

The connector does not support the following table or column configurations:

* Columns with collations
* `TRANSIENT` or `TEMPORARY` tables
* Tables with `AUTOINCREMENT` or `IDENTITY` column settings
* A default column value that is not `NULL`

### IP addresses to allow

Snowflake has strict rules about which systems it accepts requests from. Add the [Tealium IP addresses]() to your Snowflake allow list.


<blockquote>
You must add the `us-west-1` and the server-side profile region addresses to your allowlist. If you do not add these addresses to your allowlist, you will see errors when you try to fetch data. Tealium uses the `us-west-1` IP addresses during connector configuration.
</blockquote>


## Best practices

We recommend the following Snowflake table configurations for the Snowflake Streaming connector:

* 1 event feed per table
* 1 audience per table


<blockquote>
Concurrent writing of tables by more than one feed or audience may result in performance errors.
</blockquote>


## Snowflake native app

Tealium provides a free native app in the Snowflake marketplace: [Tealium Snowflake Connector](https://app.snowflake.com/marketplace/listing/GZSOZ70FXN/tealium-tealium-snowflake-connector).

The app includes helper utilities for setting up and managing streamed data from Tealium in Snowflake. It automates initial landing table setup tasks, including creating schemas, tables, and views.

The native app is optional and does not replace the configuration steps in this guide. To perform the setup manually, follow the instructions below.


<blockquote>
The Tealium Snowflake App currently transforms visitor payload data only. Event payload data is not supported.
</blockquote>


## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Authentication Type**: Select the authentication type for the connection. Possible values are: `Private key` or `Public key`.
* **User Name**:  The Snowflake account username. Must either have `OWNERSHIP` or `INSERT` rights to the Snowflake table that is receiving the data.
* **Role**: (Optional) Specify an account role if your user needs to switch roles after connecting. Leave blank if using the Tealium Snowflake Connector native app and the application role has been granted directly to your user.
* **Account identifier**: Account identifier is used to construct your account URL in the following format: `ACCOUNT_IDENTIFIER.snowflakecomputing.com.` If your account identifier contains underscores, use the dashed format instead:
    * URL with underscores: `https://acme-marketing_test_account.snowflakecomputing.com`
    * URL with dashes: `https://acme-marketing-test-account.snowflakecomputing.com`
* For private key authentication:
    * **Private Key**: The customer-generated private key. Supports both encrypted and unencrypted private keys. For instructions on generating the Snowflake private key, see [Snowflake: Key-pair authentication and key-pair rotation](https://docs.snowflake.com/en/user-guide/key-pair-auth#generate-the-private-key). 
<blockquote>
If the private key is encrypted, you must provide the Private Key Passphrase.
</blockquote>

    * **Private Key Passphrase**: The encrypted private key passphrase for use with an encrypted private key. Do not assign a value if the private key is unencrypted.
    * To use the private key:
        1. Generate a public key in Snowflake. For more information, see [Generate a Public Key](https://docs.snowflake.com/en/user-guide/key-pair-auth#generate-a-public-key).
        1. Assign the public key to the above user by using an `ALTER USER` command in Snowflake. Only owners of users or users with SECURITYADMIN roles or higher can alter a user. For more information, see [Assign the public key to a Snowflake user](https://docs.snowflake.com/en/user-guide/key-pair-auth#assign-the-public-key-to-a-snowflake-user).  
        To successfully assign the public key to the user, ensure the following:
            * Enter the Snowflake username in double quotes (`"`). For example, `"SNOWFLAKE.USER"`.
            * Copy and paste the public key without line breaks.
        1. Run the query to update the user with the new public key.
* For public key authentication:
    * **Key Algorithm**: Select an algorithm to generate the key pair, then click **Generate**. A key fingerprint appears below. Click **Regenerate** to generate a new key. `RSA-2048`, `RSA-3072`, or `RSA-4096` are supported.
    * To use the public key:
        1. Click **Download Public Key** to download your public key below.
        1. Copy the key from the file.
        1. Execute the following query on your Snowflake instance:   
        ```ALTER USER [your username] SET RSA_PUBLIC_KEY = [your public key from the file].```
        1. Click **Done** to create the new connection.
* **Enable Snowpipe Streaming for Iceberg Tables**: Enable this option if your target table in Snowflake is a managed Iceberg table.


<blockquote>
Snowflake supports public and private key rotations. For more information, see [Configuring key-pair rotation](https://docs.snowflake.com/en/user-guide/key-pair-auth#configuring-key-pair-rotation).
</blockquote>


## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Entire Log Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |

The following section lists the supported parameters for each action.

### Send Custom Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Database Name | The Snowflake database that contains the required table. |
| Schema Name | The name of the schema used in the table. |
| Table Name | The name of the table you want to insert data into.|
|Event Parameters | Map the event parameters to the columns in the Snowflake table.|

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Database Name | The Snowflake database that contains the required table.  |
| Schema Name | The name of the schema used in the table. |
| Table Name | The name of the table you want to insert data into.|
| Column to record the payload | Choose the **VARIANT** column to record the event data.|
| Timestamp | Select the column to send the timestamp variable to.|
| Timestamp Attribute | (Optional) By default, the connector sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send a different format. For more information, see [Snowflake: Supported Java data types](https://docs.snowflake.com/en/user-guide/data-load-snowpipe-streaming-overview#supported-java-data-types). If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Additional Event Data | The following parameters are only available when using Tealium iQ and EventStream.<ul><li>**First-party Cookies** - Include first-party cookie information captured with the event.</li><li>**DOM** - Include DOM data captured with the event.</li><li>**Meta** - Include Meta data captured with the event.</li></ul> |

### Send Custom Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Database Name | The Snowflake database that contains the required table. |
| Schema Name | The name of the schema used in the table. |
| Table Name |The name of the table you want to insert data into. |
|Visitor Parameters | Map the visitor parameters to the columns in the Snowflake table.|

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Database Name | The Snowflake database that contains the required table. |
| Schema Name | The name of the schema used in the table. |
| Table Name | The name of the table you want to insert data into. |
| Column to record the visitor data | Choose the **VARIANT** column to record the visitor data. |
| Include Current Visit Data | Selecting this option includes both visitor data and current visit data in the data sent to Snowflake. |
| Timestamp | Select the column to send the timestamp variable to.|
| Timestamp Attribute | (Optional) By default, the connector sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send a different format. For more information, see [Snowflake: Supported Java data types](https://docs.snowflake.com/en/user-guide/data-load-snowpipe-streaming-overview#supported-java-data-types). If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Include Current Visit Data with Visitor Data | Select to include the current visit data with visitor data. |

### Send Entire Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Database Name | The Snowflake database that contains the required table. |
| Schema Name | The name of the schema used in the table. |
| Table Name | The name of the Snowflake table that the data will be inserted into. |
| Column to record the payload | Choose the column to record the payload. |
| Column to record the Timestamp | Choose the column to record the Timestamp. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Database Name | The Snowflake database that contains the required table. |
| Schema Name | The name of the schema used in the table. |
| Table Name | The name of the Snowflake table that the data will be inserted into. |
| Log event resource attributes | These fields capture information about the entity for which telemetry is recorded. |
| Log event HTTP attributes | These fields log the HTTP requests and responses within the logging system. To map the entire `http` array to a single column, map the `http` attribute. If the target column is of type **VARIANT**, the raw array is sent; otherwise, it is converted to a string. |
| Log event result attributes | These fields log the outcome of the operation, detailing whether it was successful or if it encountered errors. |
| Log event other attributes | These fields provide additional metadata about the logged events. |

## Drop channels

To drop channels that Tealium has created, provide a list of channels in CSV format. You can retrieve the list of channels by running **SHOW CHANNELS** in your Snowflake instance. To drop all channels created by Tealium, leave the list blank.

To configure channels to drop, use the following steps:

1. Go to **Connect > Event Connectors** or to **Connect > Audience Connectors**.
1. Select a Snowflake connector.
1. Under **Remote Configuration**, click **Drop Channel**.
1. Enter the following information:  
    * **Database Name**  
        (Required) The Snowflake database name for the table.
    * **Schema Name**  
        (Required) The name of the schema used in the table.
    * **Table Name**  
        (Required) The name of the Snowflake table.
    * **Channel Name**  
        The names of the Snowflake channels to drop, in CSV format. If no channel name is provided, all channels are dropped.
1. Click **Drop**.

If your list of tables is large and the deletion takes longer than 30 seconds, a false error stating that channels were not deleted may occur. We recommend that you validate that channels were successfully deleted by running **SHOW CHANNELS** in your Snowflake instance.