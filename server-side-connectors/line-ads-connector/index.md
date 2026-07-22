---
title: LINE Ads Connector Setup Guide
description: This article describes how to set up the LINE Ads connector.
url: https://docs.tealium.com/server-side-connectors/line-ads-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: LINE Ads
* API Version: v3
* API Endpoint: `https://ads.line.me/api/v3/adaccounts`
* Documentation: [LINE API](https://ads.line.me/public-docs/v3/3.11.1/data-general-partner)

## Batch Limits
This connector uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).


After adding the connector, configure the following settings:
* **Access Key**
  * (Required) Obtain an access key from the Group settings page in the LINE Ad Manager UI.
* **Secret Key**
  * (Required) Obtain a secret key from the Group settings page in the LINE Ad Manager UI.
* **Ad Account ID**
  * (Required) Your LINE Ads account ID.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add Visitors to Custom Audience | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Add Visitors to Custom Audience


#### Parameters

| Parameter | Description |
| --- | --- |
| LINE Audience | Select the LINE audience. If the audience is not available in the drop-down, enter the Audience ID manually and set the **LINE Audience Type**. |

#### User Identifier

| **Parameter** | **Description** |
| --- | --- |
| Email Address (apply SHA256 hash) | Provide a plain text email address, or array of addresses, and the connector trims whitespace, lowercases, and hashes this value using the SHA256 hash. |
| Email Address (already SHA256 hashed) | Provide an email address, or array of addresses, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number, or array of phone numbers, and the connector trims whitespace and hashes this value using the SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number, or array of phone numbers, already whitespace trimmed and SHA256 hashed. |
| LINE Audience Type | Select the LINE audience type. Required only if you entered an Audience ID manually in the **LINE Audience** field. Possible values are `HASHED_EMAIL` and `HASHED_PHONE_NUMBER`. |
