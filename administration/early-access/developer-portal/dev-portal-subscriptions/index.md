---
title: Developer Portal subscriptions
description: Manage API subscriptions for your applications in the Tealium Developer Portal.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-subscriptions/
---
A subscription connects an application to a Tealium API. When you subscribe, you select scopes that determine which resources and actions the application's access tokens cover. You must create at least one application before you can subscribe to APIs. For more information, see [Applications](https://docs.tealium.com/dev-portal-applications/) and [Scopes](https://docs.tealium.com/dev-portal-scopes/).


<blockquote>
We recommend subscribing to APIs through the application process. For more information, see [Applications](https://docs.tealium.com/dev-portal-applications/).
</blockquote>


## Subscribe to an API from the API Catalog

If you already have an application configured, you can subscribe to an API directly from the API catalog:

1. Go to **API Catalog** and select an API.
1. Click **Subscribe**.
1. Select a plan and click **Next: Select Scopes**. Plans determine the security mechanism (for example, OAuth2 or JWT) and may have different rate limits.
1. Select scopes and click **Next: Select Application**. Check the resource and action pairs your application needs. Tokens include only the scopes you select.
1. Select the application for this subscription and click **Next: Review**.
1. If you are logged in as a Tealium user and the API requires account-scoped access, an **Account Profiles** step appears. Select the Tealium accounts and profiles this subscription should have access to, then click **Next: Select Engines** or **Next: Review**.
   
<blockquote>
External developers skip this step. Access to Tealium customer resources is granted by the resource owner via [Third-party app access](https://docs.tealium.com/dev-portal-third-party-app-access/).
</blockquote>

1. If any selected API is in preview, a warning appears on the review screen. Check the box to confirm that your organization has a signed early access agreement with Tealium and that you have reviewed which account profiles you are granting access to. The **Create Subscription** button stays disabled until you check the box.
1. Review and click **Confirm Subscription**.

## Subscribe an existing application to additional APIs

1. Go to **Applications** and select an application.
1. Click **Subscribe to APIs**.
1. Select the APIs you want to subscribe to and click **Next: Configure Scopes**.
1. Select scopes. Check each resource and action pair your application needs. Tokens include only the scopes you select. Request only what your application requires.
1. If you are logged in as a Tealium user, click **Next: Account Profiles**. Select the Tealium accounts and profiles this subscription covers, then click **Next: Select Engines** or **Next: Review**.
   
<blockquote>
External developers see **Next: Review (N apps selected)** instead and skip the account profiles and engine steps.
</blockquote>

1. Select engines (if applicable). For APIs that require engine-level access, such as the Context API, a **Select Engines** step appears. Engines are grouped by account and profile. Choose specific engines, or select **All engines (current and future)** to include engines added later. Disabled engines can still be selected for future use. You can skip this step and grant engine access later.
1. If any selected API is in preview, a warning appears on the review screen. Check the box to confirm that your organization has a signed early access agreement with Tealium and that you have reviewed which account profiles you are granting access to. The **Create Subscription** button stays disabled until you check the box.
1. Review your configuration and confirm.

## Engine selection

The engine selection step appears when one or more APIs in the subscription require engine-level authorization. Engines are grouped by account and profile.

* Select individual engines by name or ID.
* Select **All engines (current and future)** to grant a wildcard that automatically includes engines created after the subscription.
* Disabled engines can still be selected. They appear with a disabled badge.
* Engine selection is optional. You can add or change engine access after the subscription is created.

After the subscription is created, you can update engine access from the **Engine Access** section on the application detail page. For more information, see [Engine access management](https://docs.tealium.com/dev-portal-applications/#engine-access-management).

If you are an external developer, Tealium users who grant your application access also complete a **Select Engines** step in the grant flow. For more information, see [Third-party app access](https://docs.tealium.com/dev-portal-third-party-app-access/).

## Subscription status

After you subscribe to an API, the subscription enters one of the following states:

| Status | Meaning |
|---|---|
| Accepted | Active and ready to use. Your application can request tokens with the subscribed scopes. |
| Pending | Awaiting processing. Subscriptions are approved automatically and this state typically resolves immediately. |
| Closed | The subscription has been terminated. You cannot make further API calls. To regain access, create a new subscription. |

## Manage subscriptions

Go to **Subscriptions** in the sidebar to view all subscriptions across your applications. You can filter the list by application or by API using the dropdowns at the top of the page. Hover over a scopes chip to see the specific permissions assigned to that subscription.

To edit or close a subscription, go to the application details page and open the **Subscriptions** section.

## Edit a subscription

You can update the scopes on an active subscription at any time.

1. Go to the application details page.
1. Open the **Subscriptions** section.
1. Click the edit icon next to the subscription.
1. Add or remove scopes as needed.
1. Click **Save**.


<blockquote>
Existing access tokens continue to work with their original scopes until they expire. Tokens expire after 2 hours. New token requests use the updated scope set. If any resource owners have granted your application access to their accounts, changing scopes may trigger a scope drift notification for them to review the changes.
</blockquote>


To edit which Tealium accounts and profiles an application can access, use the **Account Access** section on the application detail page. For more information, see [Edit account access](https://docs.tealium.com/dev-portal-applications/#edit-account-access).
