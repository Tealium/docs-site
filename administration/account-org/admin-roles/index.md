---
title: Admin roles
description: This article describes admin roles in the platform permissions system.
url: https://docs.tealium.com/administration/account-org/admin-roles/
---
## How it works

An admin role defines a set of account access levels for administering client-side and server-side users, managing account-level functions, and managing the membership and structure of profiles. Account managers can use admin roles to delegate management of an account and the product features to other users.

The following admin roles are available:

* [Account admin](#account-admin)
* [User admin](#user-admin)
* [Technical admin](#technical-admin)
* [Privacy admin](#privacy-admin)
* [Profile admin](#profile-admin)
* [Standard user](#standard-user)


<blockquote>
The difference between admin roles and permission groups is that admin roles manage aspects of the account while permission groups manage aspects of profiles.
</blockquote>


### Default account admin

When account administrators turn on permissions enforcement, the system automatically assigns the account admin role to all users who previously had the manage account permission in the legacy permissions system.

This automatic permissions assignment ensures that at least one user has the account admin role when platform permissions is turned on.

## Roles

You can grant the following admin roles to users in your account:

### Account admin

The account admin role has full power and access to the account. The account admin role includes all account-level permissions and all profile-level permissions, including both client-side and server-side publishing permissions.

In addition, account admins control permissions enforcement on the account, which changes the account from legacy to platform permissions. For more information, see [Permissions Enforcement](https://docs.tealium.com/permissions-system-migration-guide-permissions-enforcement/).


<blockquote>
At least one user in your account must have the account admin role. If you are the only user with the account admin role in your account, you cannot remove this role from yourself.
</blockquote>


### User admin

The user admin role has access to the following settings:

* **Manage Permissions**: Create, edit, and delete permission groups. Also can add and remove users from permission groups, and assign profiles to permission groups.
* **Manage Users**: Add, edit, and remove users from the account.
* **Multi-Factor Authentication**: Enable and disable [multi-factor authentication](https://docs.tealium.com/multi-factor-authentication-mfa/) on the account.
* **Reset MFA for other users**: Reset multi-factor authentication tokens for other users in the account.
* **Set Password Policy**: Manage the [password policy](https://docs.tealium.com/password-policy/) for the account.
* **SSO Management**: Enable, disable, and manage [Single-Sign On (SSO)](https://docs.tealium.com/set-up-single-sign-on/).
* **Insights Management**: Manage user roles within [Tealium Insights](https://docs.tealium.com/about-data-insights/#author-and-reader-roles).

Also, the user admin role can view all profiles on the account.

### Technical admin

The technical admin role has access to the following settings:

* **First-Party Domains** - Manage [first-party domains](https://docs.tealium.com/first-party-domains/), including entering domain names and updating certificates.
* **GitHub Account** - Link the account to [a GitHub account](https://docs.tealium.com/about-linking-to-github/) for use with the Advanced JavaScript Code extension.

### Privacy admin

The privacy admin role can only be granted to users with the user admin role. The privacy admin role has access to the following settings:

* **Consent Management**: Manage [consent parameters and languages](https://docs.tealium.com/about-consent-management/), which apply to all profiles that use consent management.
* **PII View and Manage**: Manage Personally Identifiable Information (PII) user permissions and view and edit attributes with [restricted data](https://docs.tealium.com/about-restricted-data/).
* **Tag Marketplace Policy**: Enable, disable, and configure the [tag marketplace policy](https://docs.tealium.com/tag-marketplace-policy/) to control which tags are available for use on this account.

### Profile admin

The profile admin role has access to manage client-side profiles and profile settings. This role does not include profile editing or publishing permissions; those are granted through rights in a permission group, which the profile admin can set.

* **Manage Profile Libraries**: [Manage profile libraries](https://docs.tealium.com/profile-libraries/).
* **Manage Profiles**: [Create and manage profiles](https://docs.tealium.com/manage-profiles/). 
<blockquote>
Only client-side profiles can be created through the platform. To create a server-side profile, contact Tealium Support.
</blockquote>


### Standard user

The standard user role receives all of its permissions through group permissions. Users not assigned to any other admin role receive the standard user role.

## Manage a user’s admin roles

To edit a user’s admin roles:

1. In the admin menu, click **Manage Permissions**.
1. Click the **Users** tab.
1. Click the user you want to edit. The **User Details** slideout appears.
1. Click the **Account Permissions** tab and click **Edit**.
1. Add or remove the necessary admin roles for the user.
    * The interface automatically selects any additional admin roles or PII permissions that are necessary for that role.
1. When you are finished making the changes you want, click **Finish**.

The changes to the user's admin roles are effective immediately.

You can also use the checkboxes and **Bulk Actions** to assign or unassign roles to multiple users at once.