---
title: Yahoo DataX (Deprecated) Connector Setup Guide
description: This article describes how to set up the Yahoo DataX connector.
url: https://docs.tealium.com/server-side-connectors/yahoo-datax-connector-deprecated/
---

<blockquote>
This connector is now deprecated and no longer available in the connector marketplace. For the current connector, see [Yahoo DataX connector](https://docs.tealium.com/yahoo-datax-connector/).
</blockquote>


## API Information

This connector uses the following vendor API:

* API Name: Yahoo API
* API Version: v1
* API Endpoint: `https://datax.yahooapis.com`
* Documentation: [Yahoo API](https://developer.yahooinc.com/datax/guide)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: `10000`
* Max time since oldest request: `60 minutes`
* Max size of requests: `100 MB`

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User to Segment| ✓| ✗|
|Opt Out| ✓| ✗|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/server-side/connectors/manage/) article.

When configuring the Yahoo DataX connector, you will be prompted with an End User Licensing Agreement (EULA) that must be accepted before continuing with the configuration. At the bottom of the window, you can download the agreement for legal review. Redlines are not accepted on the EULA.

In the **Connector Configuration** section, perform the following steps:

1. Enter a name for this connector configuration and any optional notes for the connector.
2. Under the **Authentication** section, set **Environment** to **Production**.

    
<blockquote>
This value must always be set to **Production**, unless a Yahoo or Tealium representative instructs you to change it.
</blockquote>


3. Select the GDPR mode that will be assigned to the segments.

The data that is sent to Yahoo must have the appropriate segment created within a Yahoo-hosted taxonomy file.

If you are implementing this connector for the first time, perform the following steps:

1. Click **New Taxonomy Segments**.
1. On the **Create New Taxonomy Segments** screen, enter your Yahoo MDM Number to add it to the taxonomy branch.
    * If multiple users are being added, separate those entries with a comma.
1. Enter a name for the segment your audience data is being sent to. We recommend that this segment name match the Tealium audience name.
1. (Optional) Enter a **Description**.
1. Click **Create Account (Profile) Segment**.
    * This adds three nodes to the taxonomy file: your Tealium account name, Tealium profile name, and the audience segment that receives the data.

If you have already created an account and profile segment for the taxonomy file (by setting up a different YahooX connector on your Tealium profile), perform the following steps:

1. Click **Add Audience to Taxonomy**.
1. Enter an audience name.
1. (Optional) Enter a **Description**.
1. Click **Add Audience**.

    
<blockquote>
Yahoo’s process for setting up taxonomy segments can take up to 45 minutes. If you begin sending data during this window, it will not be accepted and will give an error because the segments do not yet exist in Yahoo.
</blockquote>


1. Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down list.

The following section describes how to set up parameters and options for each action.


<blockquote>
Yahoo keeps the user data in their segment for only 30 days, at which point users need to be re-sent through the DataX connector. We recommend performing [Audience Sizing](https://docs.tealium.com/about-audience-sizing/) to capture the active visitors for the audience and then creating a job for the audience to send that data to Yahoo so Yahoo maintains the data in their segment.
</blockquote>


### Action — Add User to Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|URN Type| (Required) The user identifier (URN) type.|
|URN Value| (Required) The user identifier (URN) value.|
|Taxonomy ID| (Required) The ID of the taxonomy.|
|Timestamp| Represents when the qualification occurs. A UNIX epoch time in seconds.|
|Expiration Timestamp| Represents when the qualification expires. A UNIX epoch time in seconds, up to 90 days in the future.|
|GDPR| (Required) Whether the data is subject to GDPR regulations. |

### Action — Opt Out

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|URN Type| (Required) The user identifier (URN) type.|
|URN Value| (Required) The user identifier (URN) value.|
|Taxonomy ID| (Required) The ID of the taxonomy.|
|Timestamp| Represents when the qualification occurs. A UNIX epoch time in seconds.|
|Expiration Timestamp| Represents when the qualification expires. A UNIX epoch time in seconds, up to 90 days in the future.|
|GDPR| (Required) Whether the data is subject to GDPR regulations. |