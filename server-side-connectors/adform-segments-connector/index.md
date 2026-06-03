---
title: Adform Segments Connector Setup Guide
description: This article describes how to set up the Adform Segments connector.
url: https://docs.tealium.com/server-side-connectors/adform-segments-connector/
---

## API Information

This connector uses the following vendor API:

* API Name: Adform API
* API Version: v1
* API Endpoint: `https://api.adform.com/v1/dmp`
* Documentation: [Adform API](https://api.adform.com/v1/help/dmp)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User to Audience Segment| ✓| ✓|
|Remove User from Audience Segment| ✓| ✓|

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Client ID**  
(Required) Provide your Client ID.
* **Client Secret**  
(Required) Provide your Client Secret.

Click **Done** when you are finished configuring the connector.

## Audience Segment

Segments can be created and deleted, and you can add users to or remove users from audience segments. AudienceStream utilizes an API endpoint to retrieve, create, and delete segments within your Tealium AudienceStream instance.

By default, the ability to dynamically create audiences is not available. To use this feature, ask your Adform administrator to make this feature available.

Only account administrators can make dynamic audience generation available or adjust the default settings for all dynamically-generated audiences. Administrators can set the price, indicate the to live (TTL) in days, and specify a data type.

To create a segment, click **Create Segment** for the following parameters:

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| Audience Name | (Required) Name of the audience to appear in Adform. |
| Adform Partner ID |  (Required) The Adform Partner ID for your account. |
| Category ID  | (Required) A category ID to which the audience should belong. |
| Owner ID |  (Required) Audience Owner ID value. |
| Price | (Required) The price to set per audience. |
| Data Type |  Set the data type according to your data sharing plans: &lt;ul&gt;&lt;li&gt;**1st Party**: Only you will be using the data. &lt;/li&gt;&lt;li&gt;**2nd Party**: You plan to share the data with your partner or partners. &lt;/li&gt;&lt;li&gt;**3rd Party**: You plan to share this data with everyone as a branded data provider. &lt;/li&gt;&lt;/ul&gt; |
| Time to Live (TTL) | (Required) The lifetime of data under an audience segment. |
| Frequency | (Required) The number of times an identifier must be qualified before the defined criteria will be added to the audience list. |

To delete a segment, click **Delete Audience** and select the audience segment to be deleted.

Additionally, the status of the segment appears in parentheses next to the audience segment name.

For example: Cart Abandoners (active)

## Action settings — parameters and options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

 The Adform Segments connector does not support sending the `UID` parameter. If the `UID` parameter is necessary. Adform suggests using [their Tealium tag](). 

### Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Add User to Audience Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience Segment (`sg`)| Select Audience Segment or type Owner ID.|
|Adform Partner ID| (Required) The Adform Partner ID of your account.|
|GAID (`gaid`)| Google Advertiser Visitor ID attribute|
|IDFA (`idfa`)| Apple Identifier for Advertisers|
|First Party Data Source| Text for the source or technology provider responsible for the included IDs. This should be a top-level domain. For example, `netid.de`|
|First Party Agent Type| An integer that identifies the type of user agent that the user identifier is from. Possible agent type values:  &lt;ul&gt;&lt;li&gt;1 - Collected from a desktop device in a browser.&lt;/li&gt;&lt;li&gt;2 - Collected from an app (in-app) on a mobile device (for example, IDFA or AAID).&lt;/li&gt;&lt;li&gt;3 - A user-based ID, which is the same across multiple devices and applications.&lt;/li&gt;&lt;li&gt;500&#43; - Vendor-specific context and ID, vendor-specific codes.&lt;/li&gt;&lt;/ul&gt; |
|First Party ID| An identifier for the first-party ID from the source provider. This might be a long string or a GUID.|

### Action — Remove User from Audience Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience Segment (`sg`)| Select Audience Segment or type Owner ID.|
|Adform Partner ID| (Required) The Adform Partner ID of your account.|
|GAID (`gaid`)| Google Advertiser Visitor ID attribute|
|IDFA (`idfa`)| Apple Identifier for Advertisers|
|First Party Data Source| Text for the source or technology provider responsible for the included IDs. This should be a top-level domain. For example, `netid.de`|
|First Party Agent Type| An integer that identifies the type of user agent that the user identifier is from. Possible agent type values:  &lt;ul&gt;&lt;li&gt;1 - Collected from a desktop device in a browser.&lt;/li&gt;&lt;li&gt;2 - Collected from an app (in-app) on a mobile device (for example, IDFA or AAID).&lt;/li&gt;&lt;li&gt;3 - A user-based ID, which is the same across multiple devices and applications.&lt;/li&gt;&lt;li&gt;500&#43; - Vendor-specific context and ID, vendor-specific codes.&lt;/li&gt;&lt;/ul&gt; |
|First Party ID| An identifier for the first-party ID from the source provider. This might be a long string or a GUID.|

## First Party ID

Adform accepts all currently available first-party ID solutions. First-party IDs are assigned to the audiences provided in the call.

The following first party IDs are supported:

|**Provider Name**| **Source Name**|
|---| ---|
|NetID| `netid.de`|
|Britepool| `britepool.com`|
|Liveramp (IdentityLink)| `liveramp.com`|
|PubCommonID| `id5-sync.com`|
|Lotame (Panorama ID)| `crwdcntrl.net`|
|Unified ID 2.0| `uidapi.com`|
|Prebid Shared ID| `sharedid.org`|
|Your Proprietary ID|  `your-top-level-domain.com` This value could potentially map the Tealium Visitor ID used for visitor stitching to send to Adform. |
