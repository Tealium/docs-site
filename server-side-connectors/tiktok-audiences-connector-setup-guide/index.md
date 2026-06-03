---
title: TikTok Audiences Connector Setup Guide
description: This article describes how to set up the TikTok Audiences connector.
url: https://docs.tealium.com/server-side-connectors/tiktok-audiences-connector-setup-guide/
---
 This connector has been deprecated. We recommend that you use the [TikTok Audiences (Tealium-Provided Credentials) Connector]() instead. 

## API information

This connector uses the following vendor API:

* API Name: TikTok HTTP API
* API Version: v1.3
* API Endpoint: `https://business-api.tiktok.com/open_api/v1.3`
* Documentation: [TikTok Audience segment](https://ads.tiktok.com/marketing_api/docs?id=1736874036878337)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 30 minutes
* Max size of requests: 1 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Advertiser ID**: (Required) The ad account ID from your TikTok Ads Manager. For more information, see [TikTok: How to find your ad account ID](https://ads.tiktok.com/help/article/find-your-ad-account-id?lang=en). Click **Establish Connection** to test the connection to TikTok.

To create an audience for this connector, follow these steps:

1. Click **Create Audience**.
1. Under **Custom Audience Name**, enter the audience name for this connector to use.
1. From the **Encryption Type** drop-down list, select the encryption type to use when populating the audience.
1. Click **Create**, then click **Done**.

To remove an audience, follow these steps:

1. Click **Remove Audience**.
1. From the **Audience ID** drop-down list, select the audience to remove.
1. Click **Remove**, then click **Done**.

When you are finished configuring the connector, click **Done**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add Visitor to Audience| ✓| ✗|
| Remove Visitor from Audience | ✓ | ✗ |

Click **Continue** to configure the connector actions. Enter a name for the action and then select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Add Visitor to Audience

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience ID| Select audience or enter audience ID.|
|IDFA (apply MD5 hash)| Provide a plain text iOS IDFA. The connector whitespace trims, lowercases, and hashes this value using MD5 hash.|
|IDFA (already MD5 hashed)| Provide an iOS IDFA that has already been MD5 hashed.|
|AAID (apply MD5 hash)| Provide a plain text Ad identifier for Android devices. The connector whitespace trims, lowercases, and hashes this value using MD5 hash.|
|AAID (already MD5 hashed)| Provide an Ad identifier for Android devices that has already been MD5 hashed.|
|IDFA (apply SHA256 hash)| Provide a plain text iOS IDFA. The connector whitespace trims, lowercases, and hashes this value using SHA256 hash.|
|IDFA (already SHA256 hashed)| Provide an iOS IDFA that has already been SHA256 hashed.|
|AAID (apply SHA256 hash)| Provide a plain text Ad identifier for Android devices. The connector whitespace trims, lowercases, and hashes this value using SHA256 hash.|
|AAID (already SHA256 hashed)| Provide an Ad identifier for Android devices which has already been SHA256 hashed.|
|Email Address (apply SHA256 hash)| Provide a plain text email address (must include an `@`). The connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
|Email Address (already SHA256 hashed)| Provide an email address that has already been SHA256 hashed. |
|Phone Number (apply SHA256 hash)| Provide a plain text phone number. The connector whitespace trims and hashes this value using SHA256 hash.|
|Phone Number (already SHA256 hashed)| Provide a phone number that has already been SHA256 hashed.|

### Remove Visitor from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience ID | Select audience or enter audience ID. |
| IDFA (apply MD5 hash) | Provide a plain text iOS IDFA. The connector whitespace trims, lowercases, and hashes this value using MD5 hash. |
| IDFA (already MD5 hashed) | Provide an iOS IDFA which has already been MD5 hashed. |
| AAID (apply MD5 hash) | Provide a plain text Ad identifier for Android devices. The connector whitespace trims, lowercases, and hashes this value using MD5 hash. |
| AAID (already MD5 hashed) | Provide an Ad identifier for Android devices which has already been MD5 hashed. |
| IDFA (apply SHA256 hash) | Provide a plain text iOS IDFA. The connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| IDFA (already SHA256 hashed) | Provide an iOS IDFA which has already been SHA256 hashed. |
| AAID (apply SHA256 hash) | Provide a plain text Ad identifier for Android devices. The connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| AAID (already SHA256 hashed) | Provide an Ad identifier for Android devices which has already been SHA256 hashed. |
|Email Address (apply SHA256 hash)| Provide a plain text email address (must include an `@`). The connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
|Email Address (already SHA256 hashed)| Provide an email address that has already been SHA256 hashed. |
|Phone Number (apply SHA256 hash)| Provide a plain text phone number. The connector whitespace trims and hashes this value using SHA256 hash.|
|Phone Number (already SHA256 hashed)| Provide a phone number that has already been SHA256 hashed.|