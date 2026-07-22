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

## Configuration

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Client ID**: (Required) Provide your Client ID.
* **Client Secret**: (Required) Provide your Client Secret.
* **Account Scope Type**: Select the account mode for your Adform account:
  * **Partner Level** (default): uses your Adform Partner ID. Select this for legacy Adform DMP accounts.
  * **Advertiser Level**: uses the Adform Audience Manager with an Adform Advertiser ID.
* **Adform Partner ID**: (Required with Partner Level) Enter your Adform Partner ID.
* **Adform Advertiser ID**: (Required with Advertiser Level) Select your Adform Advertiser ID from the list or enter it manually. Only active advertisers are shown.

## Manage Audience Segments

Create and delete segments, and add or remove users from audience segments. The connector uses an API endpoint to retrieve, create, and delete segments in your Tealium AudienceStream instance.

Only account administrators can make dynamic audience generation available or adjust the default settings for all dynamically-generated audiences. Administrators can set the price, indicate the time to live (TTL) in days, and specify a data type.

To delete a segment, click **Delete Audience Segment** and select the audience segment to be deleted.


<blockquote>
By default, the ability to dynamically create audiences is not available. To use this feature, ask your Adform administrator to make this feature available.
</blockquote>


### Partner Level

To create a partner-level segment, click **New Audience Segment** and configure the following settings:

|**Setting**| **Description**|
|---| ---|
| Name | (Required) Name of the audience to appear in Adform. |
| Adform Partner ID |  (Required) The Adform Partner ID for your account. |
| Category ID  | (Required) A category ID to which the audience should belong. |
| Owner ID |  (Required) Audience Owner ID value. |
| Price | (Required) The price to set per audience. |
| Data Type |  Set the data type according to your data sharing plans: <ul><li>**1st Party**: Only you use the data. </li><li>**2nd Party**: You share the data with your partner or partners. </li><li>**3rd Party**: You share this data with everyone as a branded data provider. </li></ul> |
| Time to Live (TTL) | (Required) The lifetime of data under an audience segment. |
| Frequency | (Required) The number of times a user must fall into a category to be assigned to an audience. |

The status of the segment appears in parentheses next to the audience segment name. For example: `Cart Abandoners (active)`

### Audience Manager

To create an advertiser-level audience for Audience Manager global accounts, click **New Audience Segment (Audience Manager)** and configure the following settings:

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

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User to Audience Segment| ✓| ✓|
|Remove User from Audience Segment| ✓| ✓|
|Add User to Audience Segment (Audience Manager)| ✓| ✓|
|Remove User from Audience Segment (Audience Manager)| ✓| ✓|


<blockquote>
The Adform Segments connector does not support sending the `UID` parameter. If the `UID` parameter is required, Adform suggests using the [Adform tag](https://docs.tealium.com/adform-tag/).
</blockquote>


### Add User to Audience Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience Segment (`sg`)| Select Audience Segment or type Owner ID.|
|Adform Partner ID| (Required) The Adform Partner ID of your account.|
|GAID (`gaid`)| Google Advertiser Visitor ID attribute|
|IDFA (`idfa`)| Apple Identifier for Advertisers|
|First Party Data Source| Text for the source or technology provider responsible for the included IDs. This should be a top-level domain. For example, `netid.de`|
|First Party Agent Type| An integer that identifies the type of user agent that the user identifier is from. Possible agent type values:  <ul><li>1 - Collected from a desktop device in a browser.</li><li>2 - Collected from an app (in-app) on a mobile device (for example, IDFA or AAID).</li><li>3 - A user-based ID, which is the same across multiple devices and applications.</li><li>500+ - Vendor-specific context and ID, vendor-specific codes.</li></ul> |
|First Party ID| An identifier for the first-party ID from the source provider. This might be a long string or a GUID.|

### Remove User from Audience Segment

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Audience Segment (`sg`)| Select Audience Segment or type Owner ID.|
|Adform Partner ID| (Required) The Adform Partner ID of your account.|
|GAID (`gaid`)| Google Advertiser Visitor ID attribute|
|IDFA (`idfa`)| Apple Identifier for Advertisers|
|First Party Data Source| Text for the source or technology provider responsible for the included IDs. This should be a top-level domain. For example, `netid.de`|
|First Party Agent Type| An integer that identifies the type of user agent that the user identifier is from. Possible agent type values:  <ul><li>1 - Collected from a desktop device in a browser.</li><li>2 - Collected from an app (in-app) on a mobile device (for example, IDFA or AAID).</li><li>3 - A user-based ID, which is the same across multiple devices and applications.</li><li>500+ - Vendor-specific context and ID, vendor-specific codes.</li></ul> |
|First Party ID| An identifier for the first-party ID from the source provider. This might be a long string or a GUID.|

### Add User to Audience Segment (Audience Manager)

Uses the same parameters as [Add User to Audience Segment](#add-user-to-audience-segment). For the `sg` parameter, use the **Third Party Audience ID** of the Audience Manager segment.

### Remove User from Audience Segment (Audience Manager)

Uses the same parameters as [Remove User from Audience Segment](#remove-user-from-audience-segment). For the `sg` parameter, use the **Third Party Audience ID** of the Audience Manager segment.

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
|Your Proprietary ID|  `your-top-level-domain.com` This value could potentially map the Tealium Visitor ID used for visitor stitching to send to Adform. |
