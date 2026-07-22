---
title: Yahoo! JAPAN Ads API Connector Setup Guide
description: This article describes how to set up the Yahoo! JAPAN Ads API connector.
url: https://docs.tealium.com/server-side-connectors/yahoo-japan-ads-api-connector-setup-guide/
---
## API Information

This connector uses the following vendor API:

* API Name: Yahoo! JAPAN API
* API Version: v18
* API Endpoint: `https://ads-display.yahooapis.jp`
* Documentation: [Yahoo! JAPAN API](https://ads-developers.yahoo.co.jp/developercenter/en/)

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/server-side/connectors/manage/) article.

After adding the connector, configure the following settings:

* **Client ID**: (Required) Your application client ID.
* **Client Secret**: (Required) Your application client secret.

Click **Done** when you are finished configuring the connector.

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 200
* Max time since oldest request: 360 minutes
* Max size of requests: 10 MB

## Actions

|Action Name| AudienceStream| EventStream|
|---| ---| ---|
| Add User List | ✓ | ✗ |

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type.

The following section describes how to set up parameters and options for each action.

### Add User List

#### Standard Parameters

|**Parameter**| **Description**|
|---| ---|
|Account ID| (Required) The account ID.|
|Audience List ID| (Required) The audience list ID.|
|Base Account ID | (Required) The base account ID if the account ID is an MCC account. |

#### User ID

|**Parameter**| **Description**|
|---| ---|
|Email (already SHA256 hashed)| Provide an email address that has already been whitespace trimmed, lowercase, and SHA256 hashed.|
|Email (apply SHA256 hash)| Provide a plain text email address and the connector whitespace trims, lowercase, and hashes this value using the SHA256 hash.|
|IDFA| Ad identifier for iOS devices.|
|AAID| Ad identifier for Android devices.|
|Unknown| Unknown value.|