---
title: Yahoo DataX Connector Setup Guide
description: This article describes how to set up the Yahoo DataX connector.
url: https://docs.tealium.com/server-side-connectors/yahoo-datax-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Yahoo API
* API Version: v1
* API Endpoint: `https://datax.yahooapis.com`
* Documentation: [Yahoo API](https://help.yahooinc.com/datax/docs/yahoo-ad-tech-datax-api-specifications)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

When you add this connector you are prompted to accept the vendor&#39;s data platform policy.

After adding the connector, configure the following settings:

* **GDPR Mode** (Required) GDPR Mode. Supported values:
    * **oath_is_controller**: Yahoo acts as a data controller. Each identified data subject has given explicit consent for Yahoo to process their data for specified purposes, following the IAB-EU Transparency and Consent standard.
    * **oath_is_processor**: Yahoo acts as a data processor under the General Data Protection Regulation (GDPR), based on a contract with a third-party data controller.

If you are implementing this connector for the first time, perform the following steps:

1. Click **New Taxonomy Segments**.
1. On the **Create New Taxonomy Segments** screen, enter your Yahoo MDM Number to add it to the taxonomy branch.
    * If multiple users are being added, separate those entries with a comma.
1. Enter a **Name** for the segment your audience data is being sent to. We recommend that this segment name match the Tealium audience name.
1. (Optional) Enter a **Description**.
1. Click **Create Account (Profile) Segment**.

This adds three nodes to the taxonomy file: your Tealium account name, Tealium profile name, and the audience segment that receives the data.

If you have already created an account and profile segment for the taxonomy file (by setting up a different YahooX connector on your Tealium profile), perform the following steps:

1. Click **Add Audience to Taxonomy**.
1. Enter the audience **Name**.
1. (Optional) Enter a **Description**.
1. Click **Add Audience**.  Yahoo’s process for setting up taxonomy segments can take up to 45 minutes. If you begin sending data during this window, it is not accepted and gives an error because the segments do not yet exist in Yahoo. 

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Segment | ✓ | ✗ |
| Opt Out | ✓ | ✗ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Add User to Segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| URN Type | (Required) The user identifier (URN) type.&lt;ul&gt;&lt;li&gt;DXID&lt;/li&gt;&lt;li&gt;ZIP4&lt;/li&gt;&lt;li&gt;IXID&lt;/li&gt;&lt;li&gt;IDFA (iOS ID for Advertisers)&lt;/li&gt;&lt;li&gt;GPADVID (Google Play Advertising ID)&lt;/li&gt;&lt;li&gt;Email (apply SHA256 hash)&lt;/li&gt;&lt;li&gt;Email (already SHA256 hashed)&lt;/li&gt;&lt;/ul&gt; To create new taxonomy segments, click **Create New Taxonomy Segment** and follow the on-screen instructions. |
| URN Value | (Required) The user identifier (URN) value. |
| Taxonomy ID | (Required) The ID of a taxonomy. |

#### Segment

| **Parameter** | **Description** |
| --- | --- |
| Timestamp | Timestamp associated with this qualification in UNIX epoch time, measured in seconds. For example: `1376244670`. This value must represent a time in the past. |
| Expiration Timestamp | Timestamp when the qualification expires in UNIX epoch time, measured in seconds. For example: `1379234569`. |
| GDPR | Supported values: &lt;ul&gt;&lt;li&gt;**true**: European audience data. The data provider indicates that the data is subject to GDPR regulations.&lt;/li&gt;&lt;li&gt;**false**: The rest of the world. The data provider indicates that the data is not subject to GDPR regulations.&lt;/li&gt;&lt;/ul&gt; |

### Opt Out

This action uses the same parameters and mapping options as the **Add User to Segment** action. For more information, see [Add User to Segment](#add-user-to-segment).