---
title: About user permissions
description: This article describes how user permissions work in Tealium iQ Tag Management.
url: https://docs.tealium.com/iq-tag-management/administration/user-permissions/about/
---
For server-side permissions, see [Managing Server-Side User Permissions](https://docs.tealium.com/server-side/settings/user-permissions/manage/).

## How user permissions work

There are two categories of user permissions, account-level and profile-level.  Existing users can view their permission settings and other information from [User Settings]().

### Account-level permissions

Account-level permissions pertain to the management of the account, site scans, and profiles. The following table describes the available account-level permissions:

|Permission| Description|
|---| ---|
|Manage Account|  <ul><li>Enables the user to assign account-level permissions for other users.</li></ul> |
|Manage Profiles|  <ul><li>Enables the user to create, manage, and rename profiles for this account.</li></ul> |
|Manage Site Scans|  <ul><li>Enables the user to run and delete site scans.</li><li>All users can view site scans.</li></ul> |
| Manage JavaScript Code Extensions |  <ul><li>Enables the user to edit JavaScript code extensions set up in the account.</li><li>This permission applies to the  [JavaScript Code extension](), not the [Advanced JavaScript Code extension](). </li></ul> |

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
|Manage Users|  <ul><li>Add, edit, and remove users and their permissions for this profile.</li></ul> |
|Manage Tag Templates|  <ul><li>Edit and delete all tag templates for this profile</li></ul> |
|Manage Resource Locks|  <ul><li>Apply and manage [resource locks]() for variables, tags, load rules, and extensions.</li></ul> |
|Save Existing Versions|  <ul><li>Perform a **Save** for this profile, which overwrites the existing configuration of the version with the new configurations.</li> <li>Apply [labels]() to variables, tags, load rules, and extensions.</li><li>Note: Ensure that users with this permission understand the difference between performing a Save and a Save As.</li></ul> |
|Save As New Versions|  <ul><li>Perform a **Save As** for this profile.</li></ul> |
|JavaScript Draft Promotion|  <ul><li>Promote drafts in the [Advanced JavaScript Code extension]() to be published to Dev, QA, or Prod.</li></ul> |
|Publish to Dev Environment|  <ul><li>Publish to the Dev environment and any custom environments added to this profile.</li><li>Required to publish to [custom publish environments]().</li></ul> |
|Publish to QA Environment|  <ul><li>Publish to the QA environment.</li></ul> |
|Publish to Prod Environment|  <ul><li>Publish to the Prod environment.</li></ul> |