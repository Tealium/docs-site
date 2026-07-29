---
title: Salesforce Bulk cloud data source
description: This article describes how to set up the Salesforce Bulk cloud data source.
url: https://docs.tealium.com/administration/early-access/data-sources/salesforce-bulk-cloud-data-source/
---

<blockquote>
The Salesforce Bulk cloud data source is currently in Early Access and is available to select customers only. Contact Tealium Support to get started with Salesforce Bulk.
</blockquote>


For a general overview of setting up a cloud data source, see [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/).

## How it works

The Salesforce Bulk cloud data source reads data from your Salesforce org using the [Salesforce Bulk API 2.0](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/bulk_api_2_0.htm). 

Salesforce is a cloud data source that organizes data as objects and fields, rather than SQL databases. When you import data from Salesforce, Tealium processes each record from the selected object as an event.

The Salesforce Bulk data source uses a scheduled batch model:

* **Scheduled frequencies**: Supports hourly, daily, and weekly scheduling.
* **Automatic data reads**: Each scheduled run reads all new data since the previous run.

## Data types

To ensure data is imported correctly, map Salesforce field types according to the following guidelines:

| Salesforce | Tealium |
|:-----------|:--------|
| Number, Currency, Percent | Number attributes |
| Text, Email, Phone, URL, Picklist, TextArea, Time | String attributes |
| Checkbox | Boolean attributes |
| Date, Date/Time | Date attributes |
| Multi-Select Picklist | Array of strings (default), Array of numbers, Array of booleans |

For more information about Salesforce field types, see [Salesforce: Custom field types](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&type=5).

## Create a connection

To connect to Salesforce, create a reusable connection configuration. The connection configuration includes a name and authentication fields that depend on the authentication method you select.

The following OAuth 2.0 authentication methods are available. 

### Key-Pair

Use the Key-Pair method for server-to-server communication where servers exchange data without an interactive login each time. This flow uses a certificate to sign authentication requests and doesn't require a user to log in, but it does require prior approval of the connected app. Tealium generates a key pair and uses the private key to sign authentication requests. You upload the corresponding certificate to your Salesforce Connected App. The app sends the signed JWT to the Salesforce token endpoint. Salesforce validates the signature and, assuming the app has prior approval, issues an access token. For more information, see [Salesforce: OAuth 2.0 JWT bearer flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_jwt_flow.htm&type=5).

To create a connection using Key-Pair:

1. Select **Key-Pair** as the authentication method.
1. In the **Consumer Key** field, enter the consumer key of the connected app for which you registered the certificate.
1. In the **Username** field, enter your Salesforce username.
1. Click **Add Key Pair** and select **Generate key pair**. You can also reuse existing key pairs or upload a private key file.
1. Download the generated key pair certificate file.
1. Apply the downloaded certificate to the connected app.
1. Click **Done** to save the connection.

### Salesforce OAuth

Use the Salesforce OAuth method when your integration server can store secrets securely. The user approves access, and the server exchanges an authorization code for a token. For more information, see [Salesforce: OAuth 2.0 web server flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_web_server_flow.htm&type=5).

To create a connection using Salesforce OAuth:

1. Select **Salesforce OAuth** as the authentication method.
1. Select an **Account Type** to specify which Salesforce endpoint to use for the connection.
1. Click **Establish Connection**.
1. In the Salesforce login screen that opens, enter your username and password.
1. After a successful login, Salesforce redirects to an approval page. Grant access to the Tealium app.
1. Click **Done** to save the connection.

### OAuth

Use the OAuth method for server-to-server integrations where no user login is required. Tealium sends a consumer key and secret to the Salesforce OAuth token endpoint. Salesforce validates the credentials and returns an access token on behalf of an assigned integration user. Tealium uses the token to call the Salesforce API. For more information, see [Salesforce: OAuth 2.0 client credentials flow](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_oauth_client_credentials_flow.htm&type=5).

To create a connection using OAuth:

1. Select **OAuth** as the authentication method.
1. In the **Base URL** field, enter your Salesforce host URL.
1. In the **Consumer Key** field, enter the consumer key of the external client app.
1. In the **Consumer Secret** field, enter the consumer secret of the external client app.
1. Click **Done** to save the connection.

## Query configurations

For a general overview, see .

For the Salesforce Bulk data source, note the following:

* **Incrementing**, **Timestamp + Incrementing**, and **Timestamp** query modes: These query modes are not supported. Instead, specify an **Offset Column**. The offset column must be a Date or Date/Time field (for example, `CreatedDate` or `LastModifiedDate`) with monotonically increasing values. The connector uses this column to track progress and avoid duplicate reads.
* **Advanced query mode**: Write queries using [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) instead of SQL.

## IP addresses to allow

If your Salesforce org restricts API access by IP address, add the [Tealium IP addresses](https://docs.tealium.com/ip-allow-list/) to your Salesforce trusted IP ranges.
