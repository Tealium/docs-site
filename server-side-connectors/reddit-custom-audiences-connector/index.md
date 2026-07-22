---
title: Reddit Custom Audiences connector setup guide
description: This article describes how to set up the Reddit Custom Audiences connector.
url: https://docs.tealium.com/server-side-connectors/reddit-custom-audiences-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Reddit API
* API Version: v3
* API Endpoint: `https://ads-api.reddit.com/api/v3`
* Documentation: [Reddit API](https://ads-api.reddit.com/docs/v3)

## Batch Limits
  
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Custom Audience | ✓ | ✗ |
| Remove User from Custom Audience | ✓ | ✗ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

<blockquote>
When you add this connector, you are prompted to accept the vendor's data platform policy.
</blockquote>


After adding the connector, configure the following settings:

* **Account ID**  
(Required) The ID of the Reddit Ad account that the conversion event belongs to. This can be found as `Pixel ID` under **Conversions Events** in the Reddit Ads UI.


### Add User to Custom Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience | The audience to which the user will be added. |
| User Identifier Type | User identifiers can be one of the following types: `Email Address`, `MAID`, or `Email & MAID`. |
| User Identifier | The identifier for the user. Normalize email addresses by trimming leading and trailing whitespace and converting all characters to lower case before hashing. All values must be SHA-256 hashed. If **User Identifier Type** is `Email & MAID`, the first value must be Email and the second value must be MAID. |
| User Identifier Already Hashed | Select the checkbox if the user identifier is already hashed. |


<blockquote>
If you do not see your newly-created audience in the **Audience** drop-down list, copy the **Audience ID** (usually in format `ca.xxxxxxxxxxx`) from the **Reddit Audience Manager** page and paste it in the **Audience** section of the connector to send data.
</blockquote>


### Remove User from Custom Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience | This is the audience from which the user will be removed. |
| User Identifier Type | User identifiers can be one of the following types: `Email Address`, `MAID`, or `Email & MAID`. |
| User Identifier | The identifier for the user. Normalize email addresses by trimming leading and trailing whitespace and converting all characters to lower case before hashing. All values must be SHA-256 hashed. If **User Identifier Type** is `Email & MAID`, the first value must be Email and the second value must be MAID. |
| User Identifier Already Hashed | Select the checkbox if the user identifier is already hashed. |


<blockquote>
If you do not see your newly-created audience in the **Audience** drop-down list, copy the **Audience ID** (usually in format `ca.xxxxxxxxxxx`) from the **Reddit Audience Manager** page and paste it in the **Audience** section of the connector to send data.
</blockquote>
