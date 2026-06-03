---
title: About user permissions
description: This article describes how user permissions work in Tealium iQ Tag Management.
url: https://docs.tealium.com/iq-tag-management/administration/user-permissions/about/
---
For server-side permissions, see [Managing Server-Side User Permissions](/server-side/administration/user-permissions/manage/).

## How user permissions work

There are two categories of user permissions, account-level and profile-level.  Existing users can view their permission settings and other information from [User Settings]().

### Account-level permissions

Account-level permissions pertain to the management of the account, site scans, and profiles. The following table describes the available account-level permissions:

|Permission| Description|
|---| ---|
|Manage Account|  &lt;ul&gt;&lt;li&gt;Enables the user to assign account-level permissions for other users.&lt;/li&gt;&lt;/ul&gt; |
|Manage Profiles|  &lt;ul&gt;&lt;li&gt;Enables the user to create, manage, and rename profiles for this account.&lt;/li&gt;&lt;/ul&gt; |
|Manage Site Scans|  &lt;ul&gt;&lt;li&gt;Enables the user to run and delete site scans.&lt;/li&gt;&lt;li&gt;All users can view site scans.&lt;/li&gt;&lt;/ul&gt; |
| Manage JavaScript Code Extensions |  &lt;ul&gt;&lt;li&gt;Enables the user to edit JavaScript code extensions set up in the account.&lt;/li&gt;&lt;li&gt;This permission applies to the  [JavaScript Code extension](), not the [Advanced JavaScript Code extension](). &lt;/li&gt;&lt;/ul&gt; |

### Profile-level permissions

Profile-level permissions are assigned using one of the following three methods:

* **All Current and Future Profiles**  
Use this option for Admin users or any user that requires access to all profiles for the account, including those that will be created in the future.
* **Select from Currently Assigned Profile(s)**  
Use this option to filter the available profiles to only those that the user is currently assigned. Select the profiles assigned from the **Profile List**.
* **Select Profile(s)**  
Use this option to edit permissions for the selected profiles in the **Profile List**.

The following table describes the available profile-level permissions:

|Permission| Description|
|---| ---|
|Manage Users|  &lt;ul&gt;&lt;li&gt;Add, edit, and remove users and their permissions for this profile.&lt;/li&gt;&lt;/ul&gt; |
|Manage Tag Templates|  &lt;ul&gt;&lt;li&gt;Edit and delete all tag templates for this profile&lt;/li&gt;&lt;/ul&gt; |
|Manage Resource Locks|  &lt;ul&gt;&lt;li&gt;Apply and manage [resource locks]() for variables, tags, load rules, and extensions.&lt;/li&gt;&lt;/ul&gt; |
|Save Existing Versions|  &lt;ul&gt;&lt;li&gt;Perform a **Save** for this profile, which overwrites the existing configuration of the version with the new configurations.&lt;/li&gt; &lt;li&gt;Apply [labels]() to variables, tags, load rules, and extensions.&lt;/li&gt;&lt;li&gt;Note: Ensure that users with this permission understand the difference between performing a Save and a Save As.&lt;/li&gt;&lt;/ul&gt; |
|Save As New Versions|  &lt;ul&gt;&lt;li&gt;Perform a **Save As** for this profile.&lt;/li&gt;&lt;/ul&gt; |
|JavaScript Draft Promotion|  &lt;ul&gt;&lt;li&gt;Promote drafts in the [Advanced JavaScript Code extension]() to be published to Dev, QA, or Prod.&lt;/li&gt;&lt;/ul&gt; |
|Publish to Dev Environment|  &lt;ul&gt;&lt;li&gt;Publish to the Dev environment and any custom environments added to this profile.&lt;/li&gt;&lt;li&gt;Required to publish to [custom publish environments]().&lt;/li&gt;&lt;/ul&gt; |
|Publish to QA Environment|  &lt;ul&gt;&lt;li&gt;Publish to the QA environment.&lt;/li&gt;&lt;/ul&gt; |
|Publish to Prod Environment|  &lt;ul&gt;&lt;li&gt;Publish to the Prod environment.&lt;/li&gt;&lt;/ul&gt; |