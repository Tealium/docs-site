---
title: About platform permissions
description: This article describes the unified platform permissions system.
url: https://docs.tealium.com/administration/account-org/about-platform-permissions/
---
## How it works

Tealium provides a unified permissions system that lets you manage user access to your account and profiles through permission groups and admin roles.

A [_permission group_](https://docs.tealium.com/permission-groups/) defines a set of product access levels for the profiles in your account. Users in a group inherit those permissions for the associated profiles, which simplifies managing permissions for a large number of users and profiles.


<blockquote>
Client-side profiles are separate from server-side profiles, but a single permission group can grant access to both.
</blockquote>


An [_admin role_](https://docs.tealium.com/admin-roles/) grants access to features and settings that affect the entire account. A user with an admin role receives those permissions regardless of their permission group membership, which makes it easier for you to delegate management of your account to specific users. Users without admin roles receive only the access to the account they obtain through their membership in permission groups.

### New user activation

When you invite users to your account, they receive an email to activate their account. After a user activates their account, add them to a permission group with the appropriate profile and product feature access. You can add a user to multiple permission groups to grant the user greater access to profiles, such as publishing rights.

### Dynamic user interface

The interface changes based on the user's permissions:

* If a user does not have access to a product, that product does not appear in the navigation.
* If a user has access to some features, but not others, they see only the features they can access in the navigation.
* If a user does not have edit permission for a feature, the **Edit** button does not appear on pages for that feature.

## Setup plan

The method you use to set up your account, users, and permissions structure differs depending on your organization's size and complexity.

The following steps describe one possible strategy to organize the initial access to your account:

1. Determine the users and teams that need access to your Tealium account.
1. Organize the users into groups based on their job responsibilities and the access they need for your account's profiles and Tealium features.
1. Create [permission groups](https://docs.tealium.com/permission-groups/) with the necessary access to profiles and features based on the groups you came up with in Step 2.
1. Add [users](https://docs.tealium.com/users/) to your account.
1. Assign those users to the permission groups you created in Step 3.
1. Assign user permissions and [admin roles](https://docs.tealium.com/admin-roles/) to users in your account to delegate management of users, features, products, and Personally Identifiable Information (PII).

As you progress through your plan, you may identify the need for more profiles and permission groups to access those profiles.

For help with migrating your existing settings to the platform permissions system, see [Permissions System Migration Guide](https://docs.tealium.com/permissions-system-migration-guide/).

### Publish permissions

Users in a permission group with server-side publish permissions automatically receive full access to all server-side products and features.

For example, if User X is a member of Permission Group Y and Permission Group Y has server-side publishing access, User X has full access on every server-side product and feature.

## Access the Manage Permissions screen


<blockquote>
Only users with the account admin or user admin roles can access this screen. For more information, see [Admin roles](https://docs.tealium.com/admin-roles/).
</blockquote>


In the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears, and it displays the following tabs:

* [**Permission Groups**](https://docs.tealium.com/permission-groups/) - Create and manage permission groups.
* [**Users**](https://docs.tealium.com/users/) - Invite new users and manage existing users in the account.

### Permissions Enforcement

On EEA accounts, the **Manage Permissions** screen also displays the Permissions Enforcement status on the account. Permissions Enforcement disables the legacy permissions system for an account and enables platform permissions. This setting is available for only EEA accounts as part of their migration plan; it is not available for GA accounts.

For more information, see [Permissions Enforcement](https://docs.tealium.com/permissions-system-migration-guide-permissions-enforcement/).