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
* Documentation: [Adform: DMP API reference](https://api.adform.com/v1/help/dmp)

## Configuration

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Client ID**: (Required) Provide your Client ID.
* **Client Secret**: (Required) Provide your Client Secret.
* **Authentication Type**: Select the authentication mode for your Adform account:
  * **Partner Level** (default): uses your Adform Partner ID. Select this for legacy Adform DMP accounts.
  * **Advertiser Level**: uses the Adform Audience Manager with an Adform Advertiser ID.
* **Adform Partner ID**: (Required for Partner Level) Enter your Adform Partner ID.
* **Adform Advertiser ID**: (Required for Advertiser Level) Select your Adform Advertiser ID from the list or enter it manually. The list shows only active advertisers.

## Manage audience segments

Create and delete segments, and add or remove users from audience segments. The connector uses an API endpoint to retrieve, create, and delete segments in your customer data platform.

The admin tasks available depend on the **Authentication Type** you selected during configuration:

| Authentication Type | Available tasks |
|---|---|
| Partner Level | New Audience Segment, Delete Audience Segment |
| Advertiser Level | New Audience (Audience Manager) |

Only account administrators can enable dynamic audience generation and adjust its default settings. Administrators can set the price, indicate the time to live (TTL) in days, and specify a data type.

To delete a segment, click **Delete Audience Segment** and select the audience segment to be deleted. This task is only available for Partner Level.


<blockquote>
By default, the ability to dynamically create audiences is not available. To use this feature, ask your Adform administrator to make this feature available.
</blockquote>


### Partner Level

To create a partner-level segment, click **New Audience Segment** and configure the following settings:

|**Setting**| **Description**|
|---| ---|
| Name | (Required) Name of the audience to appear in Adform. |
| Adform Partner ID |  (Required) The Adform Partner ID for your account. |
| Category ID  | (Required) A category ID for the audience. |
| Owner ID |  (Required) Audience Owner ID value. |
| Price | (Required) The price to set per audience. |
| Data Type |  Set the data type according to your data sharing plans: <ul><li>**1st Party**: Only you use the data. </li><li>**2nd Party**: You share the data with your partner or partners. </li><li>**3rd Party**: You share this data with everyone as a branded data provider. </li></ul> |
| Time to Live (TTL) | (Required) The lifetime of data under an audience segment. |
| Frequency | (Required) The number of times a user must fall into a category to be assigned to an audience. |

The status of the segment appears in parentheses next to the audience segment name. For example: `Cart Abandoners (active)`

### Advertiser Level

To create an advertiser-level audience for Audience Manager global accounts, click **New Audience (Audience Manager)** and configure the following settings:

|**Setting**| **Description**|
|---| ---|
| Name | (Required) Name of the audience to appear in Adform. |
| Third Party Audience ID |  (Required) A unique external identifier for this audience. Used as the segment ID in add/remove user calls. |
| Category ID  | (Required) A category ID for the audience. |
| Time to Live (TTL) | (Required) The lifetime of data under an audience segment. |
| Frequency | (Required) The number of times a user must fall into a category to be assigned to an audience. |
| ID Fusion | Enable ID Fusion for cross-device identity resolution. Default: `Yes`. |
| Lookalike | Enable lookalike audience modeling. Default: `No`. |

## Actions

| Action Name | AudienceStream | EventStream | Authentication Type |
| --- | :---: | :---: | --- |
|Add User to Audience Segment| ✓| ✓| Partner Level |
|Remove User from Audience Segment| ✓| ✓| Partner Level |
|Add User to Audience Segment (Audience Manager)| ✓| ✓| Advertiser Level |
|Remove User from Audience Segment (Audience Manager)| ✓| ✓| Advertiser Level |


<blockquote>
The Adform Segments connector does not support sending the `UID` parameter. If the `UID` parameter is required, Adform suggests using the [Adform tag](https://docs.tealium.com/adform-tag/).
</blockquote>


### Add user to audience segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience Segment (`sg`)| The audience segment to update. Select from the list or enter the Owner ID directly.|
|Adform Partner ID| (Required) The Adform Partner ID of your account.|
|GAID (`gaid`)| The Google Advertiser Visitor ID attribute.|
|IDFA (`idfa`)| The Apple Identifier for Advertisers.|
|First Party Data Source| Text for the source or technology provider responsible for the included IDs. Use a top-level domain, for example, `netid.de`.|
|First Party Agent Type| An integer that identifies the type of user agent that the user identifier is from. Possible agent type values:  <ul><li>1 - Collected from a desktop device in a browser.</li><li>2 - Collected from an app (in-app) on a mobile device (for example, IDFA or AAID).</li><li>3 - A user-based ID, which is the same across multiple devices and applications.</li><li>500+ - Vendor-specific context and ID, vendor-specific codes.</li></ul> |
|First Party ID| An identifier for the first-party ID from the source provider. This might be a long string or a GUID.|

### Remove user from audience segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience Segment (`sg`)| The audience segment to update. Select from the list or enter the Owner ID directly.|
|Adform Partner ID| (Required) The Adform Partner ID of your account.|
|GAID (`gaid`)| The Google Advertiser Visitor ID attribute.|
|IDFA (`idfa`)| The Apple Identifier for Advertisers.|
|First Party Data Source| Text for the source or technology provider responsible for the included IDs. Use a top-level domain, for example, `netid.de`.|
|First Party Agent Type| An integer that identifies the type of user agent that the user identifier is from. Possible agent type values:  <ul><li>1 - Collected from a desktop device in a browser.</li><li>2 - Collected from an app (in-app) on a mobile device (for example, IDFA or AAID).</li><li>3 - A user-based ID, which is the same across multiple devices and applications.</li><li>500+ - Vendor-specific context and ID, vendor-specific codes.</li></ul> |
|First Party ID| An identifier for the first-party ID from the source provider. This might be a long string or a GUID.|

### Add user to audience segment (Audience Manager)

Uses the same parameters as [Add user to audience segment](#add-user-to-audience-segment). For the `sg` parameter, use the **Third Party Audience ID** of the Audience Manager segment.

### Remove user from audience segment (Audience Manager)

Uses the same parameters as [Remove user from audience segment](#remove-user-from-audience-segment). For the `sg` parameter, use the **Third Party Audience ID** of the Audience Manager segment.

## First Party ID

Adform accepts all currently available first-party ID solutions. The connector assigns first-party IDs to the audiences in the call.

The connector supports the following first-party IDs:

|**Provider Name**| **Source Name**|
|---| ---|
|NetID| `netid.de`|
|Britepool| `britepool.com`|
|Liveramp (IdentityLink)| `liveramp.com`|
|PubCommonID| `id5-sync.com`|
|Lotame (Panorama ID)| `crwdcntrl.net`|
|Unified ID 2.0| `uidapi.com`|
|Prebid Shared ID| `sharedid.org`|
|Your Proprietary ID|  `your-top-level-domain.com` This value can map the Tealium visitor ID to Adform for visitor stitching. |
