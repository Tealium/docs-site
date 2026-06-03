---
title: Plan
description: This document describes how to plan your migration to the platform permissions system.
url: https://docs.tealium.com/administration/account-org/permissions-system-migration-guide/plan/
---
## Export Users

This feature requires Manage Account permissions on the account and Manage Users permissions on every profile. The file only contains users and legacy user permissions in profiles that the currently logged-in user has Manage Users permissions on. If permissions enforcement has been turned on, this button no longer appears.

The export users feature lets you download a comma-separated value (CSV) file with the account&#39;s users, profiles, and legacy user permissions for each profile. This makes it easy to audit your users and their permissions to build permission groups and assign admin roles in the platform permissions system.

1. In the client-side admin menu, click **Manage Users**. The table displays a list of users on the account with their general permissions.
2. Click **Export Users**.
    * Legacy permissions: In the admin menu, click **Manage Users**. When the **Manage Users** dialog appears, click **Export Users**.
    * Platform permissions: In the admin menu, click **Manage Permissions** and then click the **Users** tab. When the **Users** table appears, click **Export Users**.

The CSV file lists permission values as `TRUE` or `FALSE`.

The following screenshot demonstrates a downloaded CSV file imported into a Google Sheet, with minor formatting adjustments on row 1 and `TRUE` and `FALSE` entries changes to `Y` and `N` for readability:

![](/images/platform-permissions/permissionssystemmigrationguide-1.png)

Manage Site Scans appears in the exported data. It is a legacy function, and you do not need it for migration purposes.

In this example, **user3** appears three times in the **User** column. Unlike the other users, who have the same permission on all the profiles on the account, **user3** has different permissions on the profiles **Website A**, **Website B**, and **Website C**. Because of this, separate rows in the spreadsheet contain **user3**’s profile permissions.

## Manual inventory of client-side and server-side users and permissions

If you cannot use an automatic export or prefer to perform a manual inventory, you need to manually collect each user’s permissions on the client-side.

### Client-side

Perform the following steps to export each users’ permissions on the client-side:

1. In the client-side admin menu, click **Manage Users**. The table displays a list of users on the account with their general permissions.
1. Create a spreadsheet and label the first column **Users**.
1. In the spreadsheet, add the user list to the first column.
1. In the spreadsheet, label the second column **Profile**.
1. Click the first account.
1. Click **Edit/View User Settings**. The dialog box displays the user’s permissions on the account and on each profile (Full, Partial, or None).
1. In the spreadsheet, create three new columns with this information and note the column names to use later when you are setting up the Manage Account and Manage Users admin roles:
    * **Account**
    * **Profiles**
    * **JavaScript Code**
1. Click **Close**.
1. Click **Edit/View User Permissions**. The dialog box displays the Account, Profiles, and JavaScript permissions (You already have this information).
1. Click **Next**.
1. Select **Select from Currently Assigned Profile(s)**.
1. Select each profile from the drop-down box and click **Next**. The dialog box displays the user’s permissions on every profile.
1. If the user has the same permissions on every profile, put **All** in the **Profile** column of the spreadsheet and note the user’s permissions. If the user has different permissions on profiles, duplicate the user’s row in the spreadsheet so each line represents a different profile, enter the profile names in the **Profile** column, and note their permissions in columns titled:
    * Manage Users
    * Manage Resource Locks
    * Publish to Dev/Custom Environment
    * Publish to QA Environment
    * Publish to Prod Environment
    * Manage Tag Templates
    * Save Existing Versions
    * Save As New Versions
    * Promote to Dev/Custom Environment
    * Promote to QA Environment
    * Promote to Prod Environment
1. Click **Cancel**.
1. Repeat this process for each user.

![](/images/platform-permissions/permissionssystemmigrationguide-2.png)
You now have all the client-side user permissions.

### Server-side

Perform the following steps to export each user’s permissions on the server-side:

1. In the server-side admin menu, click **Manage Users**. If a server-side user doesn’t already exist on the spreadsheet, add it to the first column.
1. Click the user account.
1. Click **Next.** The dialog now displays the user’s permissions in every profile.
1. If the user has the same permissions on every profile, enter **All** in the **Profile** column and note the user’s permissions in the spreadsheet. If the user has different permissions on profiles, duplicate the user’s row in the spreadsheet so each line represents a different profile, enter the profile names in the **Profile** column, and note the permissions in the appropriate rows.
    * **No Access** - Cannot access profile.
    * **Reader** - Read-only access to profile.
    * **Editor** - Edit and save the profile, but cannot publish.
    * **Publisher** - Editor, plus save and publish the profile. Also has full access to every server-side product and feature.
1. Click **Close**
1. Repeat this process for each user.

Based on the previous example, the following screenshot demonstrates a spreadsheet updated with server-side users and permissions:

In this example, **user6**, **user7**, and **user8** do not have any permissions on the client-side, and they had to be added manually to the spreadsheet. Also, **user7** has different permissions on the server-side profiles **App A** and **App B**, so separate rows in the spreadsheet were created for **user7**’s profile permissions.

You now have all the user permissions for client-side and server-side profiles from the legacy permissions system.

## Audit the spreadsheet

Now that you have everyone’s permissions in a spreadsheet, check for users with too much access or not enough access to the profiles they need to perform their job. Remember that a user must be in at least one permission group to access a profile’s resources. Update the spreadsheet to reflect their actual needs.

Also, be sure to remove any users who longer work for the company or require access to the account.

## Add individual user needs to the spreadsheet

Now that you have each user&#39;s profile rights on the spreadsheet, you need add some final product and data-level needs to the spreadsheet for each user:

* The level of access to PII data the user should have.
* The products and product features each user should be able to access.
* The level of access each user should have on each product feature.

### PII data needs

PII Permissions control who can see PII data and who can edit the **Restricted Data** property that identifies PII data. Only one level of PII permissions can be assigned to a group. The three levels of PII permissions are as follows:

* **No PII** – Users can view PII attributes, but cannot see the values of these attributes. PII is obscured wherever it is shown, including Trace and Live Events.
* **View** – Users can view the values of PII attributes, data but cannot edit or manage PII data.
* **Manage &amp; View** – Users can view, edit, and manage PII data.

Note in your spreadsheet whether a user should have no access, View access, or Manage &amp; View access for PII.

 In EA and EEA, PII permissions were managed by groups. In GA, PII permissions management moved from group-based management to user-based management. PII permissions set by group in EA and EEA will automatically migrate to user-based PII permissions.

### Product and feature needs

Product access permissions specify the Tealium products and features that users can access.

Product access permissions are divided into feature permissions, and may vary depending on the product permissions assigned to the group, as shown in the following table.

Users that have **View &amp;amp; Edit** or **View, Edit &amp;amp; Delete** permission also have **Save** permission.

#### iQ Tag Management

| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------|
| JavaScript Extension|No Access, View, Edit &amp; Delete|
| Advanced JavaScript Extension - Promote to Dev|No Access, View, Edit &amp; Delete|
| Advanced JavaScript Extension - Promote to QA|No Access, View, Edit &amp; Delete|
| Advanced JavaScript Extension - Promote to Prod|No Access, View, Edit &amp; Delete|
| Publish to Dev/Custom|No Access, View, Edit &amp; Delete|
| Publish to QA|No Access, View, Edit &amp; Delete|
| Publish to Prod|No Access, View, Edit &amp; Delete|
| Save|No Access, View, Edit &amp; Delete|
| Publish Settings|No Access, View, Edit &amp; Delete|
| Code Settings|No Access, View, Edit &amp; Delete|
| Resource Lock|No Access, View, Edit &amp; Delete|
| Client-Side Versions|No Access, View, View &amp; Edit|
| Tag Templates|No Access, View, View &amp; Edit|
| Tags, Extensions, Load Rules, Data Layer|No Access, View, View &amp; Edit, View Edit &amp; Delete|
 
#### AudienceStream
 
| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------| 
| Dashboard|No Access, View|
| Discovery/Sizing|No Access, View| 
| Audiences|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Audience Connectors|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Visitor/Visit Attributes|No Access, View, View &amp; Edit, View Edit &amp; Delete|

#### EventStream

| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------|
| Data Sources|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Event Attributes|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Event Connectors|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Event Specs|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Live Events|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Omnichannel|No Access, View, View &amp; Edit, View Edit &amp; Delete|

#### DataAccess

| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------|
| Access Keys|No Access, View|
| Tealium Insights* | No Access, View|
| EventStore Legacy| No Access, View|
| AudienceDB|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| EventDB| No Access, View, View &amp; Edit, View Edit &amp; Delete|
| AudienceStore|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| EventStore|No Access, View, View &amp; Edit, View Edit &amp; Delete|

\* Tealium Insights permissions can be set by user admins through the **Insights &gt; Manage Users** page. For more information, see [About Tealium Insights]().

#### Predict

| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------|
| All features|No Access, View, View &amp; Edit, View Edit &amp; Delete|

#### Functions

| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------|
| Credentials/Authentications, Global Variables|No Access, View, View &amp; Edit, View Edit &amp; Delete|

#### Server-Side Tools

| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------|
| Manage Rules|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Visitor Delete|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Visitor Lookup|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Visitor Profile Sampler|No Access, View|

#### Server-Side (Others)

| Feature|Available Permissions|
|-----------------------------------------------|:-----------------------------------------------------------|
| Labels|No Access, View, View &amp; Edit, View Edit &amp; Delete|
| Trace|No Access, View|
| Versions|No Access, View|

#### Cross-feature permission issues

Carefully consider when you disable access to a feature or product. If you disable access to a feature for a user, that user cannot access the feature in any other features that depend on it. For example:

* If you disable access to AudienceStream audiences for a user, that user cannot select an audience to action in an AudienceStream connector.
* If you disable access to server-side labels for a user, the user cannot see labels on the server-side. They can access connectors or other features with labels on them, but they cannot see or edit the labels themselves.
* EventStream and AudienceStream share some features, such as rules and labels. If a user only has access to EventStream but edits rules shared between EventStream and AudienceStream, the rules will still change in AudienceStream.

### Update the spreadsheet

Create columns in the spreadsheet for each product and feature, and mark the level of access that the user should have on each.

![](/images/platform-permissions/permissionssystemmigrationguide-3.png)

Congratulations. You now have all your users&#39; individual needs in the spreadsheet.

The next step is to organize the users into groups.

## Add organizational information

Every organization has a unique structure, needs, and workflow. Setting permissions to match your organization&#39;s workflow can ensure that each person has access appropriate for their job role, and does not have access to data due to privacy regulations. So, you need to ask some questions about your users and organization to help sort them into groups.

Here are some suggestions:

* Do you want separate permission groups for your client-side and server-side profiles because different parts of your organization manage these products?
* Do you want to create permission groups based on job responsibilities (Developer, QA, Data Manager, Engineer, Compliance, et cetera) so that when you add, move, or remove users, you can quickly assign permissions based on their job title?
* Do you want to break down permission groups by region because your profiles and users are organized by geographic campaigns and sites, and different data storage and data privacy laws apply to them?
* Do you want to break down permission groups by product (AudienceStream, EventStream, Customer Data Hub, et cetera)?

For each Yes answer, add another column to the spreadsheet, and add notes in that column about how that question impacts that user&#39;s relationship to the organization and workflow.

![](/images/platform-permissions/permissionssystemmigrationguide-4.png)

### Profile audit

If you have only one main client-side profile and one main server-side profile, but your brand and organization is split among multiple regions and responsibility structures, this data can be useful as part of a future project to configure regional profiles on your account. However, we recommend that you set up and test permissions on the platform permissions system first.

## Sort the users into groups

Now that you have all the users’ needs and relationships to the organization documented in your spreadsheet, sort the users by each of the columns.

You can now organize those users into groups based on their common needs and access rights:

* The profiles users in the group needs to access.
* The level of access group members need on each profile.
* Whether group members should have publishing rights for client-side and server-side profiles. Because users with server-side publishing rights also have full access to all server-side products and features, you should be careful which groups are granted those rights. We recommend that you create a dedicated group called **Server-side Publishing** for server-side publishers.
* The products and product features each group should be able to access.
* The level of access each group should have on each product feature.
* Whether users should have access to PII data.
* Whether users should be able to save and/or publish profiles on the client-side, server-side, or both.
    * **Edit** access on a product or feature also grants **Save** permission for a user&#39;s changes to a profile.
    * Server-side publishing access includes full access to server-side products and features.

You can break the users into smaller groups based on your organization’s other needs, such as managing users by department or job function, grouping them by geography, and so on.

These final groups of users are the permission groups you need to create.

## Add admin roles

Now that you have the groups planned out, it&#39;s time to plan out the admin roles.

Looking at your spreadsheet, ask yourself some questions about the account itself:

* Who needs full access to the account?
* Who manages users and user membership in the account’s groups?
* Who manages the technical configuration of the account?
* Who manages the Personally Identifiable Information (PII) data rights on the account?
* Who manages the account’s profiles?

The Admin and Profiles settings from the client-side inventory of user permissions can help you determine who should get admin roles for the account in the platform permission system:

* **Account Admin** -This role has full access to the account (Includes the permissions of other roles).
* **User Admin** - This role manages permission groups and user permissions. Anyone responsible for adding users, editing users, and assigning users to permission groups should have this role.
* **Technical Admin** - This role manages account configuration features, such as first-party domains.
* **Privacy Admin** - This role manages the PII permission level in groups (Requires the User Admin role). Anyone responsible for data privacy and compliance should be a candidate for this role.
* **Profile Admin** - This role manages access to profiles and libraries. Anyone who builds and organizes profiles on your account should have this role. This role does not include profile editing or publishing permissions; those are granted through rights in a permission group.
* **Standard User** - This role receives all of its permissions through group permissions.

For more information about admin roles, see [Admin Roles]().

The **User Admin** admin role is especially useful for the migration process because these people can help you refine the permission groups as your users test the platform permission system.

Congratulations. You now know the permission groups you need to create and the admin roles you need to assign.