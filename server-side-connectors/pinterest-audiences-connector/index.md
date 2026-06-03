---
title: Pinterest Audiences Connector Setup Guide
description: This article describes how to set up the Pinterest Audiences connector.
url: https://docs.tealium.com/server-side-connectors/pinterest-audiences-connector/
---
This article provides information about using the latest version of the Pinterest Audiences connector. The previous version of the Pinterest Audiences connector is still available, but eventually will be deprecated.&lt;br&gt;To update your Pinterest Audiences connector, authenticate it, and add mappings again.

## API Information

This connector uses the following vendor API:

* API Name: Pinterest REST API
* API Version: v5
* API Endpoint: `https://api.pinterest.com/v5/`
* Documentation: [Pinterest Audiences](https://developers.pinterest.com/docs/ads/targeting/#Audiences)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().
When you add this connector you are prompted to accept the vendor&#39;s data platform policy.

After adding the connector, configure the following settings:

* **Ad Account ID**  
 (Required) Unique identifier of an ad account. You can find this identifier with the following methods:
    * Log in to the Pinterest account that owns your advertiser account and then navigate to [https://ads.pinterest.com/](https://ads.pinterest.com). In the top navigation section, click **Viewing**. The ad account ID will be the number underneath the ad account name in the drop-down list.
    * Navigate to **Ads &gt; Overview** and locate the ad account ID in the URL path. The URL uses the following format: `ads.pinterest.com/advertiser/{ad_account_id}/?...`.

Click **Establish Connection** to connect to Pinterest.

 Authorization tokens expire after 60 days. To prevent audience sync interruptions, log in to Tealium and click **Establish Connection** at least once every 60 days. 

### Create a Customer List

To create a customer list on Pinterest:

1. Click **Create Customer List**.
1. Enter the customer list name.
1. Enter an audience name. A Pinterest audience with type `CUSTOMER_LIST` will be created automatically after successful customer list creation.
1. Select the type of customer list:
    * **Email**: An email address as identifier.
    * **Apple Identifier for Advertisers (IDFA)**: A random device identifier assigned by Apple to a user&#39;s device. The IDFA can also identify when users interact with a mobile advertising campaign. This is possible if the channel offers IDFA tracking and the advertiser tracks users who interact with ads successfully.
    * **Mobile Ad ID (MAID)**: Hexadecimal digit strings that Android or Apple assigns to a mobile device.
## Action Settings - Parameters and Options
1. Enter a list of emails, MAIDs, or IDFAs in any combination with one record per line.
    * Emails must be lowercase and can be plain text or hashed using SHA1, SHA256, or MD5.
    * MAIDs and IDFAs must be hashed with SHA1, SHA256, or MD5.
1. Enter a description of the audience.
1. Click **Done**.

Enter a name for the action and select the action type from the drop-down list.

The following section describes how to set up parameters and options for each action.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Audience | ✓ | ✗ |
| Remove User from Audience | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Add User to Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer List | Select the list to add records to.&lt;br&gt;Customer lists are a type of audience. For more information, see [Audience targeting](https://help.pinterest.com/en/business/article/audience-targeting) or the [Audiences](https://developers.pinterest.com/docs/ads/targeting/#Audiences) section of the ads management guide. |
| Email Address (plain text) | Provide a plain text email address (must include an `@`). |
| Email Address (already hashed) | Provide an email address which has been already whitespace trimmed, lowercased, and MD5, SHA1 or SHA256 hashed. |
| Email Address (apply MD5 hash) | Provide a plain text email address (must include an `@`) and the connector whitespace trims, lowercases, and hashes this value using MD5 hash. |
| Email Address (apply SHA1 hash) | Provide a plain text email address (must include an `@`) and the connector whitespace trims, lowercases, and hashes this value using SHA1 hash. |
| Email Address (apply SHA256 hash) | Provide a plain text email address (must include an `@`) and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Apple IDFA (already hashed) | Provide an Identifier for Advertisers which has been already whitespace trimmed, and MD5, SHA1 or SHA256 hashed. |
| Apple IDFA (apply MD5 hash) | Provide an Identifier for Advertisers and the connector whitespace trims and hashes this value using MD5 hash. |
| Apple IDFA (apply SHA1 hash) | Provide an Identifier for Advertisers and the connector whitespace trims and hashes this value using SHA1 hash. |
| Apple IDFA (apply SHA256 hash) | Provide an Identifier for Advertisers and the connector whitespace trims and hashes this value using SHA256 hash. |
| Mobile Ad ID (already hashed) | Provide a Mobile Ad ID which has been already whitespace trimmed and MD5, SHA1 or SHA256 hashed. |
| Mobile Ad ID (apply MD5 hash) | Provide a Mobile Ad ID and the connector whitespace trims and hashes this value using MD5 hash. |
| Mobile Ad ID (apply SHA1 hash) | Provide a Mobile Ad ID and the connector whitespace trims and hashes this value using SHA1 hash. |
| Mobile Ad ID (apply SHA256 hash) | Provide a Mobile Ad ID and the connector whitespace trims and hashes this value using SHA256 hash. |

### Remove User from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer List | Select the list to remove records from.&lt;br&gt;Customer lists are a type of audience. For more information, see [Audience targeting](https://help.pinterest.com/en/business/article/audience-targeting) or the [Audiences](https://developers.pinterest.com/docs/ads/targeting/#Audiences) section of the ads management guide. |
| Email Address (plain text) | Provide a plain text email address (must include an `@`). |
| Email Address (already hashed) | Provide an email address which has been already whitespace trimmed, lowercased, and MD5, SHA1 or SHA256 hashed. |
| Email Address (apply MD5 hash) | Provide a plain text email address (must include an `@`) and the connector whitespace trims, lowercases, and hashes this value using MD5 hash. |
| Email Address (apply SHA1 hash) | Provide a plain text email address (must include an `@`) and the connector whitespace trims, lowercases, and hashes this value using SHA1 hash. |
| Email Address (apply SHA256 hash) | Provide a plain text email address (must include an `@`) and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Apple IDFA (already hashed) | Provide an Identifier for Advertisers which has been already whitespace trimmed and MD5, SHA1 or SHA256 hashed. |
| Apple IDFA (apply MD5 hash) | Provide an Identifier for Advertisers and the connector whitespace trims and hashes this value using MD5 hash. |
| Apple IDFA (apply SHA1 hash) | Provide an Identifier for Advertisers and the connector whitespace trims and hashes this value using SHA1 hash. |
| Apple IDFA (apply SHA256 hash) | Provide an Identifier for Advertisers and the connector whitespace trims and hashes this value using SHA256 hash. |
| Mobile Ad ID (already hashed) | Provide a Mobile Ad ID which has been already whitespace trimmed and MD5, SHA1 or SHA256 hashed. |
| Mobile Ad ID (apply MD5 hash) | Provide a Mobile Ad ID and the connector whitespace trims and hashes this value using MD5 hash. |
| Mobile Ad ID (apply SHA1 hash) | Provide a Mobile Ad ID and the connector whitespace trims and hashes this value using SHA1 hash. |
| Mobile Ad ID (apply SHA256 hash) | Provide a Mobile Ad ID and the connector whitespace trims and hashes this value using SHA256 hash. |