---
title: Monetate Personalization Engine Connector Setup Guide
description: This article describes how to set up the Monetate connector.
url: https://docs.tealium.com/server-side-connectors/monetate-personalization-engine-connector/
---
## Requirements

* Monetate Account
* API Username & API Keys
* Data Schema

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **API Username**: (Required) Enter your API username, which can be found under **Settings > Sites > API Keys** of your account.
* **Private Key**: (Required) Provide your private key matching the registered public key in your account. The private key must be generated with the RSA algorithm and transformed to PEM PKCS #8 format. For more information, see: [Monetate: API Keys Overview](https://support.monetate.com/hc/en-us/articles/115001851123-API-Keys-Overview) and [Generating API Keys](#generate-api-keys).
* **Client ID**: (Required) Provide your client ID, which can be found under **Settings > API Documentation > Monetate Data API > Base URL** of your account. For example, if the URL is `https://api.monetate.net/api/data/v1/abc/production/`, then the client ID is `abc`.

Click **Test Connection** to verify API connectivity with the provided credentials.

## Generate API keys

To ensure secure communication, Monetate API uses public and private key pairs. Key pairs can be generated with a free and widely available OpenSSL command line tool.

Run the following commands:

```bash
openssl genrsa -out my_key.pem 4096
openssl pkcs8 -topk8 -inform PEM -outform PEM -in my_key.pem -out my_private_key.pem -nocrypt
openssl rsa -in my_key.pem -pubout -outform PEM -out my_public_key.pem
```

These commands generate a new key using the RSA algorithm (4096-bits key size) and then convert this key into PKCS#8 format without encrypting it. This is your private key. The final line outputs your public key in PEM format.

Once generated, open the files in a text editor and copy the keys and values accordingly. Register the public key in your Monetate account and provide the private key in the connector configuration screen.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Create or Update Data Record (Real-Time) | ✓ | ✓ |
| Create or Update Data Record (Batched) | ✓ | ✓ |

Click **Next** or go to the **Actions** tab.

This section describes how to set up parameters and options for each action.

### Update Data Record (Real-Time)

#### Parameters

| Parameter | Description |
|---| ---|
|Schema |(Required) Select the schema in which to create or update records. |
|Data Record | (Required) Map attributes to data record fields. If a record with the primary key field value already exists in the schema, the data is updated. Schemas of type `event` require an `event time` type field. If not mapped explicitly, field value will default to now. Date attributes are converted to ISO 8601 format: `YYYY-MM-DDThh:mm:ss`. |


<blockquote>
For more information, see: [Engine API: Sending Data](https://knowledge.monetate.com/hc/en-us/articles/115005090746).
</blockquote>


### Create or Update Data Record (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| Parameter | Description |
|---| ---|
|Schema |(Required) Select the schema in which to create or update records. |
|Data Record | (Required) Map attributes to data record fields. If a record with the primary key field value already exists in the schema, the data is updated. Schemas of type `event` require an `event time` type field. If not mapped explicitly, this value will default to now. Date attributes are converted to ISO 8601 format: `YYYY-MM-DDThh:mm:ss`. |

## Vendor documentation

* [Monetate: API Keys Overview](https://support.monetate.com/hc/en-us/articles/115001851123-API-Keys-Overview)
