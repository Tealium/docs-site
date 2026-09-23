---
title: Developer Portal applications
description: Create and manage OAuth2 applications in the Tealium Developer Portal to authenticate API requests.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-applications/
---
An application is a set of credentials that represents a system or service making API calls. Each application has a client ID and a client secret. Your integration uses these credentials to obtain access tokens for API requests.

When you create an application, you subscribe it to one or more APIs and select the scopes (access levels) it is granted for each API. The application is then authorized to request tokens scoped to those APIs and the Tealium accounts you specify. For example, you might create one application for an analytics dashboard and a separate one for a third-party integration.

For more information, see [Scopes](https://docs.tealium.com/dev-portal-scopes/).

## Create an application

When you create an application, you configure its API subscriptions as part of the same workflow.

1. Go to **Applications** in the sidebar and click **Create Application**.
1. Enter a name and an optional description, then click **Create**.
1. Select the APIs you want to subscribe to, then click **Next: Configure Scopes**.
1. Select scopes. Expand each section to view available scopes and check each resource and action pair your application needs. Tokens include only the scopes you select. Request only what your application requires. For more information, see [Scopes](https://docs.tealium.com/dev-portal-scopes/).
1. If you are logged in as a Tealium user, click **Next: Account Profiles**. Select the Tealium accounts and profiles this subscription covers.
   
<blockquote>
External developers see **Next: Review** instead and skip the account profiles and engine steps. Access to Tealium customer resources is granted by the resource owner via [Third-party app access](https://docs.tealium.com/dev-portal-third-party-app-access/).
</blockquote>

1. Click **Next: Select Engines** or **Next: Review** depending on whether the selected APIs require engine access.
1. Select engines (if applicable). For APIs that require engine-level access, such as the Context API, a **Select Engines** step appears. Engines are grouped by account and profile. Choose specific engines, or select **All engines (current and future)** to automatically include engines added later. Disabled engines can still be selected. They show a warning chip and can be enabled later. You can skip this step and grant engine access later.
1. Click **Create Subscription**.
1. Click **View Application** to go to your new application's detail page.

For information about adding subscriptions to an existing application, editing scopes, or managing engine access, see [Subscriptions](https://docs.tealium.com/dev-portal-subscriptions/).


<blockquote>
After creation, copy your client secret from the confirmation screen. The secret is only shown once. Copy it immediately after creation or after rotating the secret. Store it in a secrets manager or environment variable. Never store a client secret in source control.
</blockquote>


## View application details

In the **Applications** screen, click an application to view its details.

* **Client ID:** Your application's public identifier, used in OAuth2 flows.
* **Client Secret:** The secret used with the client ID to authenticate. The secret is only displayed immediately after creation or after rotating the secret. If you did not save it, use **Rotate Secret** to generate a new one.
* **Account Access**: The Tealium accounts and profiles this application can access. This section is available to Tealium users only. For more information, see [Edit account access](#edit-account-access).
* **External Grants**: Tealium accounts and profiles that other users have granted to this application. This card appears only when external grants exist.
* **Engine Access**: Context API engines the application can access.
* **Subscriptions:** APIs your application is subscribed to, with their status and granted scopes.
* **API Version:** The version of each API your subscriptions target.

For a cross-application view of all account and profile associations and active scopes, go to **Tealium Accounts** in the sidebar. This section is available to Tealium users only.

## Generate a bearer token

You can generate a bearer token for testing from the application detail page. Click **Generate Token**, enter an optional scope, and copy the returned token. For full details, see [Authentication](https://docs.tealium.com/dev-portal-authentication/).

## Rotate the client secret

Rotate the client secret if it is compromised or lost.

1. Open the application detail page.
1. Click **Rotate Secret**. When prompted, confirm.
1. Copy the new secret and update all systems that use this application's credentials.

Rotating the secret immediately invalidates the old one. Existing access tokens issued with the old secret continue to work until they expire, but new token requests require the new secret.

## Delete an application

Before deleting, close all active subscriptions on the application.

To delete:

1. Open the application detail page.
1. Click **Delete** and confirm in the dialog.

Deleting an application is permanent. The application can no longer make API calls, and its credentials are invalidated.

## Edit account access

Account access controls which Tealium accounts and profiles an application's tokens can cover. Account access editing is separate from scope editing and is managed directly on the application detail page, not inside the subscription wizard.

1. Open the application detail page.
1. Click **Edit** next to the **Account Access** heading.
1. In the **Edit Account Access** dialog, add or remove accounts and profiles.
1. Save your changes.

This option is available to Tealium users only. If the application has no active subscriptions, the edit button is disabled.

## Engine access management

For engine-enforced APIs, the application detail page shows an **Engine Access** section. The section displays which engines are granted per API, grouped by account and profile.

* Engines you granted appear as editable.
* Engines granted by other users appear with a "granted by another user" chip and cannot be modified.
* An **All engines** chip indicates a wildcard grant that covers all engines in that profile.

You can edit your engine selections at any time. Changes take effect immediately. New tokens reflect the updated engine access.