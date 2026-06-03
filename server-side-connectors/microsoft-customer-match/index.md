---
title: Microsoft Customer Match Setup Guide
description: This article describes how to set up the Microsoft Customer Match connector.
url: https://docs.tealium.com/server-side-connectors/microsoft-customer-match/
---
## Requirements

* Microsoft Ads account
* Microsoft user with super admin or write access within the Microsoft Ads tenant.
    * The authenticating user must be a Personal Microsoft account (MSA).
    * You may use your work email address, but it must be registered as a personal account rather than accessed through SSO. If your organization uses SSO or MFA for Microsoft login, you may still use your work email by registering it as a personal account. During registration, choose **Use a personal account**.
* Customer match is enabled and approved for your account region. For more information, see [Microsoft: Customer match - Use your own data to find customers](https://help.ads.microsoft.com/#apex/ads/en/56921/1).

### Accept Microsoft Terms of Service

If the Microsoft user you use to authenticate to Tealium is new to the business account, you must first:

1. Sign in to Microsoft Ads with that user.
1. Create an audience manually once to trigger acceptance of the Microsoft Customer Match Terms and Conditions.

Until these terms are accepted, the API rejects audience creation requests originating from Tealium.

## API information

This connector uses the following vendor API:

* API Name: Bulk API
* API Version: v13
* API Endpoint: `https://bulk.api.bingads.microsoft.com/Api/Advertiser/CampaignManagement/V13/BulkService.svc`
* Documentation: [Microsoft: Bulk API](https://learn.microsoft.com/en-us/advertising/bulk-service/bulk-service-reference?view=bingads-13)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Account ID**: (Required) The identifier of the ad account that owns or is associated with the entities in the request. It can be found in the URL (for example, `AID=`) when the advertiser logs into Microsoft Ads UI.
* **Customer ID**: (Required) The identifier of the manager account (customer) the user is accessing or operating from. It can be found in the URL (for example, `CID=`) when the advertiser logs into Microsoft Ads UI.

After setting **Account ID** and **Customer ID**, click **Establish Connection** to connect to Microsoft&#39;s servers.

### Create customer match list

Use this option to create customer match lists to add subscribers to target with advertising. The resulting **Request ID** value can be used to determine if the list creation process has completed. 

After you click the **Create** button, wait until you receive a confirmation message. If the customer list has successfully uploaded, the interface will display the upload&#39;s **Request ID**. You can copy the **Request ID** and use it to check the upload status.

| Field |  Description |
| --- |--- |
| Name |(Required) The name of the customer list. This field can contain a maximum of 128 characters. |
| Description | (Optional) The description of the customer list. Use a description to help you remember what audience you are targeting with this customer list. This field can contain a maximum of 1,024 characters. |
| Parent ID | (Optional) The Microsoft Advertising identifier of the customer that contains the customer list. |
| Client ID | (Optional) Used to associate records in the bulk upload file with records in the results file. This field can be any valid string with a maximum of 100 characters. |
| Membership Duration | (Optional) When you create a customer list, you can specify how far back in time Microsoft Advertising should look for actions that match your customer list definition to add people to your list.&lt;ul&gt;&lt;li&gt;The minimum duration is `1` day and the maximum duration allowed is `180` days.&lt;/li&gt;&lt;li&gt;If membership duration is `-1`, there is no expiration.&lt;/li&gt;&lt;li&gt;If membership duration is null, the default duration (30 days) is used.&lt;/li&gt;&lt;/ul&gt; |

### Check upload status

Use this option to check the status of your list creation and upload status. This lets you confirm that customers are being subscribed to the proper lists. 

If the upload status is `Completed` or `CompletedWithErrors`, the URL of the results file will appear. Use this URL to download the results file. The URL expires five minutes after the Check the Status operation displays the upload status. If you do not start the download within this period of time, you will need to check the status again to get a new URL.

| Field | Description |
| --- |--- |
| Request ID | The identifier of the upload request. | 

## Use cases

#### High value remarketing across Microsoft properties

Activate high-value user segments across Bing, MSN, Outlook, and Edge with improved accuracy by syncing real-time audience lists from Tealium. Behavioral remarketing powered by first-party identifiers improves match rates, reduces dependency on browser-based tracking, and increases ROAS.

Examples:

* Re-engage cart abandoners who viewed products but didn’t convert.
* Reinforce promotions for users who previously interacted with your brand.
* Extend the reach of CRM audiences into Microsoft’s native ad environment.

#### Suppression lists for budget efficiency

Remove converted users from prospecting and broad-match campaigns. Advertisers reduce wasted budget and direct spend toward incremental users more likely to convert sharpening bidding efficiency.

Examples:

* Exclude recent purchasers from acquisition campaigns.
* Suppress customer service or refund requesters.
* Remove churned or unsubscribed users.

#### Lifecycle and CRM-to-Ad activation

Sync loyalty tiers, subscription statuses, and customer lifecycle stages directly from your CDP into Microsoft Ads. This unlocks a powerful bid strategy: target users differently based on lifetime value and customer stage.

Examples:

* Loyalty tiers for VIP-only upsell campaigns.
* Subscription renewal reminders.
* Push known in-store customers into digital remarketing campaigns.

#### Omnichannel personalization

Bridge offline and online interactions by syncing hashed first-party identifiers.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Audience | ✓ | ✗ |
| Remove User from Audience | ✓ | ✗ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Add User to Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Match List ID | Enter the customer match list ID.&lt;br&gt;To find your customer match list ID: log into [Microsoft Advertising UI](https://ui.ads.microsoft.com/) and select **Tools**, then click the **Audiences** tab.&lt;br&gt;Note: Before you can upload customer list data, you must first accept the terms and conditions in the Microsoft Advertising UI.&lt;br&gt; |
| Email Address (already SHA256 hashed) | Provide an email address which has been already SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address, and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |

### Remove User from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Match List ID | Enter the customer match list ID.&lt;br&gt;To find your customer match list ID: log into [Microsoft Advertising UI](https://ui.ads.microsoft.com/) and select **Tools**, then click the **Audiences** tab.&lt;br&gt;Note: Before you can upload customer list data, you must first accept the terms and conditions in the Microsoft Advertising UI.&lt;br&gt; |
| Email Address (already SHA256 hashed) | Provide an email address which has been already SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address, and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |