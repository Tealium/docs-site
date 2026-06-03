---
title: Users
description: This article describes how to manage users on your account in the platform permissions system.
url: https://docs.tealium.com/administration/account-org/users/
---
## How it works

Each person who requires access to your Tealium account needs an email username and password to log in. Before they can log in, you need to invite the users to the account, and they will receive an email to activate their account.

Users receive permissions on the account through permission groups, admin roles, and user-level permissions.

* [Permission groups]() grant access to profiles, product features, and publishing rights. Add a user to multiple permission groups to provide access to multiple profiles and permission levels to those profiles.
* [Admin roles]() delegate specialized or highly sensitive responsibilities to trusted members of your team, such as user or permission groups management.
* User-level permissions set [Multi-factor Authentication (MFA)]() tokens, [API Keys](), and Personally Identifiable Information (PII) access levels.

### Dynamic user interface

In the unified platform permissions system, the platform&#39;s interface changes based on the user&#39;s permissions:

* If a user does not have access to a product, that product does not appear in the navigation.
* If a user has access to some features, but not others, they only see the features they can access in the navigation.
* If a user does not have edit permission for a feature, the **Edit** button does not appear on pages for that feature.

For more information, see [About platform permissions]().

## Manage users

To access user management in the Tealium platform, click **Manage Permissions** in the admin menu, then click the **Users** tab.

The **User Manager** dialog appears, displaying a table that lists all of the users in the account.

### Export users

The export users function downloads a comma-separated value (CSV) file with the account&#39;s users, profiles, and legacy user permissions for each profile. Use this feature to audit your users and their permissions for the purpose of creating permission groups and assigning admin roles in the new platform permissions system.

There are two ways to download this file:

* In the admin menu, click **Manage Users**. When the **Manage Users** dialog appears, click **Export Users**.
* In the admin menu, click **Manage Permissions** and then click the **Users** tab. When the **Users** table appears, click **Export Users**.

The CSV file lists permission values as `TRUE` or `FALSE`.

So that a complete list of permissions appears in the file, this feature requires legacy Manage Account permissions on the account and Manage Users permissions on every profile. If [Permissions Enforcement]() is active, this button no longer appears.

### Add new users

To add new users:

1. In the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears.
1. Click the **Users** tab.
1. In the **User Manager** screen, click **&#43; New User**. The **Add New Users** slideout appears.
1. In the **New User Emails** box, enter up to 25 email addresses. You can separate them with commas, tabs, semicolons, or paste the contents of a Comma Separated Values (CSV) file.
1. Click **Send Invitations**. The **Manage Permissions** screen appears, and the new user email addresses appears in the table with a **Pending Registration** note.

Tealium sends out email invitations to users who do not already have access to the Tealium platform. Those new users need to accept the invitation and set a password.

 When you add and invite a user, the user will not automatically receive access to any profiles on the account. You must [edit that user](#edit-a-user) to add them to permission groups to access profiles, grant them admin roles if they need to manage aspects of the account, and set their user-level permissions for MFA, API Key, and PII access. Otherwise, when they accept the invite and try to log in, they will see an error. 

To revoke an invitation to a user:

1. In the **Users** tab, select the more actions button for the user.
1. Click **Revoke Invitation**.
1. Click **Revoke** to confirm.

### View user details

To view a user&#39;s details, click that user. A slideout appears with the following three tabs:

* **Overview**: The user&#39;s name, email address, primary account, and the permissions for platform features. This tab contains functions to reset the user&#39;s Multi-Factor Authentication (MFA) tokens and manage API key authorization permissions.
* **Account Permissions**: The user&#39;s admin roles, Data Connect permissions, and Personally Identifiable Information (PII) access level on profiles they can access.
* **Groups**: The user&#39;s permission groups.

### PII access levels

A user can be set to one of the following PII access levels:

* **No PII**: Users can manage and view PII-restricted data throughout the interface.
* **View**: Users can view PII-restricted data throughout the interface.
* **Manage &amp; View**: Users can view, edit, and manage all PII data fields throughout the account.

### Profile permissions

Permissions are cumulative between the user&#39;s permission groups and admin roles. For example, if a user is in one permission group with view access, another permission group with view and edit access, and has the profile admin role, the table displays a checkmark in the **View, Edit &amp; Delete** column.

To check a user&#39;s access to a profile, select that profile from the **Profile** drop-down menu in the **Overview** tab. The user&#39;s permissions for that profile will appear. This information can help you diagnose any access issues your users have with profiles or ensure that users have access to only the features they require.

## Edit a user

To edit a user:

1. In the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears.
1. Click the **Users** tab.
1. Click the user you want to edit. The **User Details** slideout appears, open to the **Overview** tab.
    * Manage the user&#39;s Single Sign-on (SSO) settings, [MFA tokens](), and [API key]() authorization permissions.
    * If [Federation ID]() is enabled on your account, the **Federation ID** field will appear. Unless the ID is different from the user&#39;s email address, leave the **Federation ID** field blank.
1. To make changes to the user&#39;s admin roles and PII access level, click **Account Permissions**.
    * Select the admin roles that you want to grant to the user.
    * Select the user&#39;s PII access level.
    * Select the user&#39;s Data Connect access level.
    * The interface automatically selects any additional admin roles or PII permissions that are necessary for that role.
    * For more information, see [Admin Roles]().
1.  To make changes to the user&#39;s permission groups, click **Groups**.
    * Select the groups to add or remove the user from.
    * To add a new permission group, click **&#43; Permission Group**.
    * For more information, see [Permission Groups]().
1. Click **Save**. The **Manage Permissions** screen appears.

 Users without an admin role and who are not in any permission groups cannot access any profile. 

## Bulk action user management

You can use the checkboxes in the Users table and **Bulk Actions** to perform changes to multiple users at once.

To edit multiple users&#39; admin roles at the same time:

1. In the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears.
1. Click the **Users** tab.
1. Select the checkboxes for the users in the **Users** table.
1. Click **Bulk Actions**.
    * To edit multiple user&#39;s admin roles, click **Assign Admin Roles** and select the roles you want to assign to the users.
    * To edit multiple users&#39; permission groups, click **Add to Groups**, select the groups to add the users to, and click **Save**.
    * To edit multiple users&#39; PII access, click **PII Permissions** and Select the PII permissions you want to assign to the users.

## Remove a user

If a user no longer requires access to the account, you can remove that user from the account. However, this action does not remove the user from any other Tealium accounts they have access to.

This action cannot be undone.

To remove a user from your account:

1. In the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears.
1. Click the **Users** tab.
1. Select the appropriate checkboxes for the user or users you want to remove.
1. Click **Bulk Actions**, and then click **Remove Access**.
1. A confirmation message appears. Click **Remove Access** to continue.