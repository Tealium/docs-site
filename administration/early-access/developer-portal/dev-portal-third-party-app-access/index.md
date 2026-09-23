---
title: Developer Portal third-party app access
description: Grant and manage external application access to your Tealium accounts and profiles from the Developer Portal.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-third-party-app-access/
---Third-party app access lets you grant external applications access to your Tealium accounts and profiles. You control which accounts and profiles each application can access, and you can modify or revoke that access at any time. If you are building an application that needs access to Tealium accounts other than your own, see [For application developers](#for-application-developers).


<blockquote>
Third-party app access requires signing in with your Tealium account credentials. External developer accounts cannot grant access, because grants are made against the Tealium accounts and profiles you have permission to publish to.
</blockquote>


## About delegated authorization

Third-party access uses a delegated authorization model:

1. A developer creates an application in the Developer Portal and subscribes it to Tealium APIs with specific scopes.
1. The developer shares their application ID with you.
1. You look up the application, review its requested scopes, and grant access to specific accounts and profiles.
1. For APIs that require engine access, such as the Context API, you also select which engines the application can access.
1. The application obtains tokens scoped to the accounts and profiles you approved.



## Permission requirements

What you can grant depends on your Tealium role:

* **Account admins** can grant an application access to all profiles in an account at once.
* **Non-admins on legacy accounts** can grant access to individual profiles. You can only grant a profile if you have publish permissions for the server-side profile and for the tag management profile across all environments (dev, QA, and prod). If a profile does not appear in the grant dialog, you do not have the required permissions for it.


<blockquote>
On EEA accounts, only account admins can grant third-party app access.
</blockquote>


The portal only shows accounts and profiles you have permission to grant.

## Grant access to an application

1. Go to **Third-Party Apps** from the sidebar.
1. Enter the application ID provided by the third-party developer and click **Look Up**. The application ID is a UUID. If the input is invalid, a validation warning appears and the Look Up button stays disabled. If you enter your own application ID or one you have already granted, the Developer Portal shows that state rather than an error.
1. Click **Review Access** to examine the application's name, subscriptions, and requested scopes.
1. Check the confirmation box to acknowledge the access level being requested, then click **Continue**.
1. Select which Tealium accounts to grant access to.
1. Select which profiles within those accounts the application can access.
1. Select engines (if applicable). For APIs with engine enforcement, such as the Context API, a **Select Engines** step appears. Choose specific engines per profile, or select **All engines (current and future)**. Engine access is tracked per user. You can modify your engine grants independently of other users who have granted access to the same application. This step is optional. You can add engine access later.
1. Click **Grant Access**.

The application can only perform actions within the scopes it subscribed to, limited to the accounts and profiles you selected.

## Manage granted access

The **Third-Party Apps** page lists all applications that have access to your resources. For each application, you can:

* **View granted scopes**: Expand the application card to see which scopes, accounts, and profiles you granted.
* **View engine access**: Expand the Engine Access card for each engine-enforced API to see which engines are granted, grouped by account. Engines you granted appear as editable. Engines granted by other users appear with a "granted by another user" chip. An **All engines** chip indicates a wildcard grant for that profile. The Engine Access section is hidden when no engine selections exist.
* **Edit access**: Click the pencil icon (tooltip: "Edit access") to modify which accounts and profiles the application can access. Entries granted by other users appear locked in the edit dialog and cannot be changed by you.
* **Edit engines**: Click the pencil icon next to each API name inside the expanded card (tooltip: "Edit engine access") to modify your engine selections independently of account/profile access.
* **Revoke access**: Click the red **Revoke access** icon to remove all access immediately. The icon is disabled and shows "Granted by another user" when every grant on the application was made by someone else.

## Respond to scope drift

Scope drift occurs when an application developer changes their API subscriptions after you granted access. When the Developer Portal detects a change, a warning badge appears on the affected application card.

To respond to scope drift:

1. Click **Review Changes** on the application card.
1. Review the changes. The dialog shows added scopes (new capabilities the app is requesting) and removed scopes.
1. Click **Accept Changes** to update your scope snapshot to match the application's current subscriptions. Accepting updates the scope snapshot for your grant only. It does not re-grant accounts or profiles. To remove access instead, close the dialog and use the revoke icon on the application card.

Until you accept the changes, the application continues operating with the original scopes you approved. The portal does not grant new scopes automatically.

## Revoke access

To revoke all access from an application:

1. Go to **Third-Party Apps**.
1. Click the red revoke icon on the application card.
1. Confirm the revocation.

Revocation is immediate:

* The portal removes all access grants for your accounts and profiles from the application.
* Engine access associated with the revoked accounts and profiles is automatically removed.
* The portal attempts to revoke the application's active tokens immediately. If token revocation does not succeed, the removed scopes prevent new tokens from being issued, and any existing tokens stop working after they expire.
* The application can no longer access your resources.


<blockquote>
Revoking access is irreversible. The application owner will need to request a new grant if access is required again.
</blockquote>


### Partial revocation

You can revoke access to specific accounts or profiles without revoking everything. Only the selected account and profile entries are removed from your grant. Engine access for those accounts and profiles is also removed. The portal attempts to revoke tokens associated with the removed scopes. Remaining grants continue to work normally.

## For application developers

If you are building an application that needs access to other users' Tealium resources:

1. Create your application in the Developer Portal and subscribe to the required APIs with appropriate scopes.
1. Share your application ID with the resource owners who need to grant you access. Your application ID is visible on the application detail page.
1. Once they grant access, your application's tokens include scopes for their accounts and profiles. For engine-enforced APIs, such as the Context API, resource owners must also grant engine-level access before your application can access specific engines.

Request only the scopes your application needs. Resource owners can see exactly what your application is requesting before they grant access.
