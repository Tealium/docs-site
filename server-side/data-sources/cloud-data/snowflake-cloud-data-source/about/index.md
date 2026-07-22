---
title: Snowflake cloud data source
description: This article provides specific details about setting up the Snowflake cloud data source.
url: https://docs.tealium.com/server-side/data-sources/cloud-data/snowflake-cloud-data-source/about/
---
For a general overview of setting up a cloud data source, see [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/).

## User role

To allow Tealium to poll data from only the selected Snowflake tables or views, create a custom user role with `USAGE` privileges for the database, schema, warehouse, and table or view you want to connect to.

For more information, see [Snowflake: Custom roles](https://docs.snowflake.com/en/user-guide/security-access-control-overview#custom-roles) and [Snowflake: Access control privileges](https://docs.snowflake.com/en/user-guide/security-access-control-privileges).

## Data types

The Snowflake data source supports all Snowflake data types. To ensure data is imported correctly, map the Snowflake data types according to the following guidelines:

| Snowflake | Tealium |
|:----------|:--------|
| Numeric data types  | Number attributes |
| String and binary data types | String attributes |
| Logical data types | Boolean attributes|
| Date and time data types| Date attributes |
| Arrays | Array of strings, array of numbers, or array of booleans|
| Object, variant, geography, geometry, and vector data types| String attributes |

For more information about Snowflake data types, see [Snowflake: Summary of Data Types](https://docs.snowflake.com/en/sql-reference/intro-summary-data-types).

## Create a connection

You must have the following account information to create a connection to Snowflake:

* Hostname
* Connection warehouse
* Database name
* Database schema
* Connection role
* Snowflake username


<blockquote>
It's important to note that your connection information might be case sensitive depending on your Snowflake data account settings.
</blockquote>


To configure a new connection, enter the following connection details. 

* **Snowflake Connection Configuration Name**: Provide a name for the reusable connection configuration.
* **Account Identifier**: The Snowflake account identifier without the `http://` prefix in the following format:
    * Using a Snowflake account name: `ACCOUNT_NAME.snowflakecomputing.com`.
    * Using a Snowflake account locator in region: `ACCOUNT_LOCATOR.CLOUD_REGION_ID.CLOUD.snowflakecomputing.com`.
* **Connection Warehouse**: The name of the Snowflake warehouse to use for this connection.
* **Database Name**: The name of the Snowflake database to connect to.
* **Database Schema**: The name of the Snowflake database schema to connect to.
* **Connection Role**: The role assigned to the user in Snowflake. This role must have `USAGE` privileges.

For more information, see [Snowflake: Custom roles](https://docs.snowflake.com/en/user-guide/security-access-control-overview#custom-roles) and [Snowflake: Access control privileges](https://docs.snowflake.com/en/user-guide/security-access-control-privileges).

### Authentication

You can authorize a Snowflake connection with an RSA key pair in three ways:

* **Generate a new key pair** in Tealium.
* **Upload a private key file** that you generated outside of Tealium.
* **Reuse an existing key pair** that you previously generated or uploaded in Tealium.

In all cases, you must assign the corresponding public key to the Snowflake user account that requires access to the specified tables or views.

Select from the following key algorithms based on your security requirements: **RSA-2048**, **RSA-3072**, or **RSA-4096**.

#### Steps to configure authentication

1. **Username**: Enter the username of the Snowflake user with access to the required database, schema, warehouse, and table or view.
1. **Authentication**: Choose one of the following credential options:
   * **Generate new key pair**: Select an RSA algorithm. Tealium displays the private key (once only) and the public key. Download the keys and store them securely.
   * **Upload private key file**: Upload an existing private key file. If the file is encrypted, enter the passphrase to unlock it.
   * **Reuse existing key**: Select a key from the existing generated and uploaded keys. Confirm that the associated public key is already assigned to the correct Snowflake user.
1. **Download**: Download the public key file. The key is only the text between the lines `-----BEGIN PUBLIC KEY-----` and `-----END PUBLIC KEY-----`.
1. **Assign**: Assign the public key to the Snowflake user with the following SQL command:

   ```sql
   ALTER USER your_username
   SET RSA_PUBLIC_KEY='your_public_key';
   ```

   For more information, see [Snowflake: Assign a public key to a Snowflake user](https://docs.snowflake.com/en/user-guide/key-pair-auth#assign-the-public-key-to-a-snowflake-user).
1. (Optional) Copy the key fingerprint to verify that the key was assigned correctly. See [Snowflake: Verify the user’s public key fingerprint](https://docs.snowflake.com/en/user-guide/key-pair-auth#verify-the-user-s-public-key-fingerprint).

After you connect to Snowflake, select the data source table from the **Table Selection** list.

## Query configurations

For a general overview, see .

For the **Timestamp + Incrementing** and **Timestamp** query modes, the selected timestamp column must be one of the following Snowflake data types: `TIMESTAMP_LTZ`, `TIMESTAMP_TZ`, or `TIMESTAMP_NTZ`.

For more information, see the [Snowflake: Date & time data types](https://docs.snowflake.com/en/sql-reference/data-types-datetime#timestamp-ltz-timestamp-ntz-timestamp-tz).

For the **Incrementing** query mode, the selected numeric column must increment in value for every row added. A recommended definition for an auto-increment column is:

```sql
COL1 NUMBER AUTOINCREMENT START 1 INCREMENT 1
```