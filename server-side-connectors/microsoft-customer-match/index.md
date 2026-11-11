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

Until these terms are accepted, the API may reject audience creation or membership update requests unless the **Accept Customer Match Terms** checkbox is enabled in the action configuration.

## API information

This connector uses the following vendor API:

* API Name: Campaign Management API
* API Version: v13
* API Endpoint: `https://campaign.api.bingads.microsoft.com/CampaignManagement/v13/`
* Documentation: [Microsoft: Campaign Management API](https://learn.microsoft.com/en-us/advertising/campaign-management-service/campaign-management-service-reference?view=bingads-13)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 60 minutes
* Max size of requests: 5 MB

Microsoft's Campaign Management REST API accepts up to 1,000 `CustomerListItems` per request, which determines these batch thresholds.

## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Account ID**: (Required) The identifier of the ad account that owns or is associated with the entities in the request. It can be found in the URL (for example, `AID=`) when the advertiser logs into Microsoft Ads UI.
* **Customer ID**: (Required) The identifier of the manager account (customer) the user is accessing or operating from. It can be found in the URL (for example, `CID=`) when the advertiser logs into Microsoft Ads UI.

After you configure the connector, click **Done**.

After setting **Account ID** and **Customer ID**, click **Establish Connection** to connect to Microsoft's servers.

### Create customer match list

Use this option to create customer match lists to add subscribers to target with advertising. The task calls the Campaign Management REST `Audiences` endpoint and returns the new list's **Audience ID** synchronously.

After you click **Create**, wait for the confirmation message. If the customer list is successfully created, the interface displays the **Audience ID**. Copy the **Audience ID** and paste it into the **Customer Match List ID** field in the action configuration.

| Field | Description |
| --- | --- |
| Name | (Required) The name of the customer list. This field can contain a maximum of 128 characters. |
| Description | (Optional) The description of the customer list. Use a description to help you remember what audience you are targeting with this customer list. This field can contain a maximum of 1,024 characters. |
| Scope | (Optional) The level at which the customer list is created.<ul><li>**Account**: The list is created under the Account ID from the connector configuration and can only be associated with ad groups within this account.</li><li>**Customer**: The list is created under the Customer ID from the connector configuration and can be associated with ad groups across all of the customer's accounts.</li><li>If no scope is selected, **Customer** is used.</li></ul> |
| Membership Duration | (Optional) When you create a customer list, you can specify how far back in time Microsoft Advertising should look for actions that match your customer list definition to add people to your list.<ul><li>The minimum duration is `1` day and the maximum duration allowed is `390` days.</li><li>If membership duration is `-1`, there is no expiration.</li><li>If membership duration is null, the default duration (30 days) is used.</li></ul> |

### Check customer match list

Use this option to look up a customer match list and view its metadata. The task calls the Campaign Management REST `Audiences/QueryByIds` endpoint and displays the list name, ID, scope, and size.


<blockquote>
The size value may show as "still building" for up to 48 hours after a list is created or after audience members are added.
</blockquote>


| Field | Description |
| --- | --- |
| Customer Match List ID | (Required) The identifier of the customer match list to check. |

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

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
| Add User to Audience | ✓ | ✗ |
| Remove User from Audience | ✓ | ✗ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Add User to Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Match List ID | Enter the customer match list ID.<br>To find your customer match list ID: log into [Microsoft Advertising UI](https://ui.ads.microsoft.com/) and select **Tools**, then click the **Audiences** tab.<br>Note: Before you can upload customer list data, you must first accept the terms and conditions in the Microsoft Advertising UI, or by selecting the **Accept Customer Match Terms** checkbox below. |
| Email Address (already SHA256 hashed) | Provide an email address which has been already SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address, and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Accept Customer Match Terms | (Optional) Select this checkbox to programmatically accept the [Microsoft Customer Match Terms](https://go.microsoft.com/fwlink/?linkid=2106709) on behalf of the advertiser with this request. If this checkbox is cleared, you must accept the terms manually in the Microsoft Ads UI before uploading customer list data. For more information, see [Accept Microsoft Terms of Service](#accept-microsoft-terms-of-service). |

### Remove User from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Match List ID | Enter the customer match list ID.<br>To find your customer match list ID: log into [Microsoft Advertising UI](https://ui.ads.microsoft.com/) and select **Tools**, then click the **Audiences** tab.<br>Note: Before you can upload customer list data, you must first accept the terms and conditions in the Microsoft Advertising UI, or by selecting the **Accept Customer Match Terms** checkbox below. |
| Email Address (already SHA256 hashed) | Provide an email address which has been already SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address, and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Accept Customer Match Terms | (Optional) Select this checkbox to programmatically accept the [Microsoft Customer Match Terms](https://go.microsoft.com/fwlink/?linkid=2106709) on behalf of the advertiser with this request. If this checkbox is cleared, you must accept the terms manually in the Microsoft Ads UI before uploading customer list data. For more information, see [Accept Microsoft Terms of Service](#accept-microsoft-terms-of-service). |