---
title: Microsoft Bing Ads Offline Conversions Connector Setup Guide
description: This article describes how to set up the Microsoft Bing Ads Offline Conversions connector.
url: https://docs.tealium.com/server-side-connectors/microsoft-bing-ads-offline-conversions-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Microsoft API
* API Version: v13
* API Endpoint: `https://campaign.api.bingads.microsoft.com/Api/Advertiser/CampaignManagement/v13/CampaignManagementService.svc`
* Documentation: [Campaign Management API](https://learn.microsoft.com/en-us/advertising/campaign-management-service/campaign-management-service-reference?view=bingads-13)

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion Event | ✗ | ✓ |

## Configure settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Customer ID**  
(Required) You can find the customer ID in the URL after `CID=` when logged into the Microsoft Ads UI.
* **Account ID**  
(Required) You can find the account ID in the URL after `AID=` when logged into the Microsoft Ads UI.

Click **Establish Connection** to connect to Microsoft. Follow the on-screen directions to complete the connection process.

### Create offline conversion goal

Click **Create Offline Conversion Goal** to set a goal for conversions. Enter the following information:

1. Enter a unique **Name** for the conversion goal. The maximum length of the name is 100 characters.
1. Select a **Goal Category** to segment the conversion goal.
1. Select a **Scope** to determine if the goal applies to all accounts of just the specified account. After you set the scope, you can only change the scope by creating a new conversion goal and pausing the old one.
1. Under **ID**, enter the Microsoft Advertising identifier for the conversion goal.
1. Under **Conversion Window in Minutes**, enter the length of time in minutes after a click that you want to track conversions. The default value is `43200`. The minimum value supported is `1` minute. The maximum value supported is `129600` minutes (90 days). Shorter conversion windows reduce the number of conversions your account records.
1. Select a **Count Type** to determine how your conversions are recorded within the conversion window. The default is `All`:
    * **All**: All conversions with different offline conversion times that happen after an ad click are counted. This is a common choice for sales.
    * **Unique**: Only the first conversion that happens after an ad click is counted. This is a common choice for leads.
1.  Under **Exclude from Bidding**, select whether to include or exclude this goal from bidding. This determines whether data related to this conversion goal appears in a subset of performance report columns.
1. Under **Revenue Value**, enter a value to determine how much each conversion is worth to your business.
1. Under **Revenue Code**, enter the currency type that you use in reports.
1. (Optional) Under **Status**, select `Active`, `Paused`, or `Deleted` to define the possible user-determined status values of a conversion goal.
1. Click **Create &amp; Close**.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Conversion Name | (Required) The conversion goal name. This name must match an existing conversion goal name, otherwise the offline conversion goal data is not applied.|
| Microsoft Click ID | (Required) The unique ID for the landing page URL set by Microsoft Advertising.  |
| External Attribution Model |  Specifies the attribution model name. This field can be set only for conversions actions that use external attribution. |
| External Attribution Credit | Represents the fraction of the conversion that is attributed to each click. The value must be greater than 0 and less than or equal to 1. This field can only be set for conversions actions which use external attribution. |
| Conversion Value | The offline conversion value. |
| Conversion Time | (Required) The period of time after the user completed the action that Bing Ads uses to record conversion data. |
| Currency Code | The currency code for the offline conversion. If you do not specify an offline conversion currency code, then the Currency Code element of the goal&#39;s &lt;a href=&#34;https://learn.microsoft.com/en-us/advertising/campaign-management-service/conversiongoalrevenue?view=bingads-13&#34; target=&#34;_blank&#34;&gt;Conversion Goal Revenue&lt;/a&gt; is used. |
| Email Address (already SHA256 hashed) | Provide an email address which has been already whitespace trimmed, lowercased and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector trims whitespace, lowercases, and hashes this value using SHA256. |
| Phone Number (already SHA256 hashed) | Provide a phone number according to the E.164 standard which has already been trimmed of whitespace, lowercased, and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector removes all non-digit symbols, prefixes the number with a plus sign (`&#43;`), trims whitespace, lowercases, and hash this value using SHA256. |