---
title: SCIM and identity provider configuration
description: Learn how to configure SCIM with a supported identity provider.
url: https://docs.tealium.com/administration/early-access/api/scim-api/example/
---
Use the SCIM API to automatically:

* Provision and deprovision users
    * View, create, and delete users
    * Remove users (deactivate SCIM identity)
    * Re-add users (reactivate SCIM identity)
* Update users and groups
    * Update users
    * View, create, update, and delete groups

When SCIM is enabled for Tealium, user memberships are synced between Tealium and an identity provider.

## Prerequisites

* [Account admin or user admin]() permissions.
* Long-lived bearer token. For more information on how to generate the bearer token, see [Authentication]().

## Configure an identity provider

You can configure the following identity providers:

* Microsoft Entra ID (formerly Azure Active Directory)
* Okta

These providers are fully compatible. However, other IdPs may require additional configuration or tuning. For further guidance, contact your identity provider and Tealium Support to validate compatibility.

## Configure Microsoft Entra ID

The SAML application created for [Azure Active Directory](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/view-applications-portal) during SSO setup must be configured for SCIM.

You must configure SCIM provisioning exactly as detailed in the following instructions. If misconfigured, you will encounter issues with user provisioning and sign in. If you have any trouble or questions with any step, contact Tealium support.

To configure Microsoft Entra ID for SCIM:

### Add Tealium to Microsoft Entra ID

1. Go to the [Azure Portal](https://portal.azure.com/).
1. Go to **Microsoft Entra ID &gt; Enterprise applications**.
1. Click **&#43; New application** and then click **Create your own application**.
1. Enter a **Name** (for example, Tealium), and choose **Integrate any other application you don’t find in the gallery**.
1. Click **Create**.

### Configure SCIM provisioning

1. In your app, click the **Provisioning** tab and click **Connect your application**.
1. Under **Admin Credentials**, enter the following values:
   * In the **Tenant URL** field, enter the SCIM API endpoint URL from Tealium: `https://developer.tealiumapis.com/scim/v2?aadOptscim062020`. The `aadOptscim062020` flag enables group management specifically for Microsoft Entra ID.
   * In the **Secret Token** field, enter your SCIM bearer token from Tealium.
1. Click **Test Connection**. A success message appears.
1. Click **Create**.
1. Click **Get Started** and then click **Start provisioning**.

### Configure user assignments

SCIM group provisioning is not currently supported in Early Access.

1. Click **Provisioning**.
1. Set **Provisioning Status** to `ON`.
1. Expand the **Mappings** section.
1. Click each mapping and ensure that all **Target Object Actions** are enabled.
1. Click **Attribute mapping** and configure the attribute mapping between Microsoft Entra ID and Tealium. For more information, see [Microsoft: Customize user provisioning attribute-mappings for SaaS applications in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/app-provisioning/customize-application-attributes).

The following table lists the attribute mappings that you need to set for Tealium to authenticate to Microsoft Entra ID through SCIM. Delete all other mappings so only the following mappings remain:

| Microsoft Entra ID source attribute | `customappsso` target attribute | Matching precedence |
|-------------------------------------------------------------------|-------------------|-----|
| `userPrincipalName`                                               | `userName`        |  1  | 
| `Switch([IsSoftDeleted], , &#34;False&#34;, &#34;True&#34;, &#34;True&#34;, &#34;False&#34;)` \*  | `active`          |     |
| `displayName`                                                     | `displayName`     |     |
| `givenName`                                                       | `name.GivenName`  |     |
| `surname`                                                         | `name.familyName` |     |
| `mailNickname`                                                    | `externalId`      |     |

\* This is an expression type, not a direct mapping. Select **Expression** from the **Mapping type** list.

While Microsoft transitions from Azure Active Directory to Entra ID naming schemes, you might notice inconsistencies in your user interface. If you’re having trouble, contact Tealium Support.

Each attribute mapping contains the following:

* A `customappsso` attribute, which corresponds to a target attribute.
* A Microsoft Entra ID attribute, which corresponds to a source attribute.

For each attribute, use the following steps:

1. Edit the existing attribute or add a new attribute.
1. Select the required source and target attribute mappings from the lists.
1. Click **Ok**.
1. Click **Save**.

If your SAML configuration differs from the recommended SAML settings, select the mapping attributes and modify them accordingly. The source attribute that you map to the `externalId` target attribute must match the attribute used for the SAML `mailNickname`.

If a mapping is not listed in the table, use the Microsoft Entra ID defaults. For a list of required attributes, see [Microsoft: Develop and plan provisioning for a SCIM endpoint in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/app-provisioning/use-scim-to-provision-users-and-groups).

### Assign groups

1. Select **Provision Microsoft Entra ID Groups**.
1. On the **Attribute Mapping** page, set the **Provisioning Status** toggle to `ON`.
1. Click **Save**. 

### Assign users

1. Go to **Users and groups**.
1. Click **&#43; Add user/group**.
1. Select the users or groups you want to sync.
1. Click **Assign**.

### Configure final settings and start provisioning

Configure the following settings:

1. (Optional) Select the **Send an email notification when a failure occurs** checkbox.
1. (Optional) Select the **Prevent accidental deletion** checkbox.
1. Click **Save** to ensure all changes are saved.
1. Go to **Provisioning** and click **Start provisioning**.

Provisioning usually starts within a few minutes, but may take up to 40 minutes for the first sync.

## Configure Okta

To configure Okta for SCIM:

1. Log in to Okta.
1. Go to  **Applications &gt; Applications**.
1. Click **Browse App Catalog**.
1. Select **SCIM 2.0 Test App (OAuth Bearer Token)** and click **Add Integration**.
1. Click **Next** and **Done** to skip the **General Settings** and **Sign-On Options** pages.

### Connect to Tealium SCIM API

1. On the **SCIM Application** screen, click the **Provisioning** tab. 
1. Click **Configure API integration**.
1. Enable the **Enable API integration** checkbox.
1. Enter the following information:
    * Under **Base URL**, paste the URL you copied from **SCIM API endpoint URL** on the Tealium SCIM configuration page: `https://developer.tealiumapis.com/scim/v2/`
    * Under **OAuth Bearer Token**, paste the SCIM bearer token you copied from **Your SCIM token** on the Tealium SCIM configuration page.
    * To verify the configuration, click **Test API Credentials**.
1. Click **Save**.

### Configure provisioning settings

1. Under the **Provisioning** tab, scroll down to **Settings** and click **To App**.
1. Under the **Provisioning to App** section, click **Edit**.
1. Enable the **Enable** checkbox for **Create Users**, **Update User Attributes**, and **Deactivate Users**.
1. Click **Save**.

## User access

During the synchronization process, all new users receive Tealium accounts and are welcomed to their identity provider groups with an invitation email. You can bypass email confirmation with a verified domain.

During provisioning, both primary and secondary emails are considered when checking whether a Tealium user account exists. Duplicate usernames are handled by adding suffix `1` when creating the user. For example, if `test_user` already exists, `test_user1` is used. If `test_user1` already exists, Tealium increments the suffix to find an unused username. If no unused username is found after 4 tries, a random string is attached to the username.

On subsequent visits, new and existing users can access identity provider groups either through the identity provider’s dashboard or by visiting links directly. 

## Remove access

Remove or deactivate a user on the identity provider to remove their access.

After the identity provider performs a sync based on its configured schedule, the identity provider revokes the user&#39;s membership and they lose access. 

Removing or deactivating a user on the identity provider does not delete the Tealium user account. The Tealium user account is deactivated, and it can be reactivated by re-adding the user to the identity provider.

## Reactivate access

After a user is removed or deactivated through SCIM, reactivate that user by adding them to the SCIM identity provider. 

After the identity provider performs a sync based on its configured schedule, the identity provider reactivates the user&#39;s SCIM identity and restores their group memberships.