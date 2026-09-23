---
title: Reddit Custom Audiences connector setup guide
description: This article describes how to set up the Reddit Custom Audiences connector.
url: https://docs.tealium.com/server-side-connectors/reddit-custom-audiences-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Reddit API
* API Version: v3
* API Endpoint: `https://ads-api.reddit.com/api/v3`
* Documentation: [Reddit API](https://ads-api.reddit.com/docs/v3)

## Batch limits
  
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

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

<blockquote>
When you add this connector, you are prompted to accept the vendor's data platform policy.
</blockquote>


After adding the connector, configure the following settings:

* **Account ID**  
(Required) The ID of the Reddit Ads account that the conversion event belongs to. You can find it as **Pixel ID** under **Conversion Events** in the Reddit Ads UI.


### Add User to Custom Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience | The audience to add the user to. |
| User Identifier Type | User identifiers can be one of the following types: `Email Address`, `MAID`, or `Email & MAID`. |
| User Identifier | The identifier for the user. The connector SHA-256 hashes all values before sending them. For email addresses, the connector normalizes the value before hashing by converting the full address to lowercase, removing email aliases (the `+tag` portion before `@`), and removing non-alphanumeric characters from the username portion. MAID values are hashed as provided without normalization. Normalize MAID values before mapping if required. If **User Identifier Type** is `Email & MAID`, the first value must be Email and the second value must be MAID. |
| User Identifier Already Hashed | Select the checkbox if the user identifier is already hashed. |


<blockquote>
If you do not see your newly created audience in the **Audience** drop-down list, copy the **Audience ID** (usually in the format `ca.xxxxxxxxxxx`) from the **Reddit Audience Manager** page and paste it in the **Audience** section of the connector to send data.
</blockquote>


### Remove User from Custom Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience | The audience to remove the user from. |
| User Identifier Type | User identifiers can be one of the following types: `Email Address`, `MAID`, or `Email & MAID`. |
| User Identifier | The identifier for the user. The connector SHA-256 hashes all values before sending them. For email addresses, the connector normalizes the value before hashing by converting the full address to lowercase, removing email aliases (the `+tag` portion before `@`), and removing non-alphanumeric characters from the username portion. MAID values are hashed as provided without normalization. Normalize MAID values before mapping if required. If **User Identifier Type** is `Email & MAID`, the first value must be Email and the second value must be MAID. |
| User Identifier Already Hashed | Select the checkbox if the user identifier is already hashed. |


<blockquote>
If you do not see your newly created audience in the **Audience** drop-down list, copy the **Audience ID** (usually in the format `ca.xxxxxxxxxxx`) from the **Reddit Audience Manager** page and paste it in the **Audience** section of the connector to send data.
</blockquote>
