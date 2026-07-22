---
title: About server-side permissions
description: This article describes how to manage server-side users and permission roles for the Tealium Customer Data Hub.
url: https://docs.tealium.com/server-side/settings/user-permissions/about/
---
## How it works

Server-side user permissions provide control over the degree of access users have for each profile by creating a separation of access between the Tealium client-side interface and the server-side interface. From the server-side **Manage Users** screen, you can do the following:

* **Grant Access to New Users**  
New users are added to accounts in Tealium iQ Tag Management. After new users are added, the new users appear in the server-side user permissions list where server-side access can be granted, by profile. To add new users to an account, you must have the **Manage Users** permission. To assign roles on the server-side, you you must have the **Manage Account** permission.
* **Specify Access**  
Account administrators can grant access to users only for the areas that they intend to work on. They can also grant Save and Publish permissions for client-side products for a profile that do not carry over to server-side products for that profile.
* **Set Permissions for Future Profiles**  
For active profiles, you can set the permissions for future profiles, which allows user admins to define a profile-level permission role for users of new profiles created for an account.
* **Add and Edit Bulk Users**  
You can add and edit users in bulk (up to 25 users at a time) and search user profiles and filter users by permission type.

## Admin users

Admins of the server-side interface are the only users that have the ability to change the permissions of server-side users. None of the server-side permission roles grant this ability.


<blockquote>
To be an admin on the server-side, you must have the **Manage Account** permission in the client-side interface.
</blockquote>


Only the **Manage Users** permission on the client-side grants the ability to add users to the account. To learn more about managing user permission in Tealium iQ Tag Management, see [Managing User Permissions in iQ Tag Management](https://docs.tealium.com/about-user-permissions/).

## Server-side permission roles

Server-side access is controlled using predefined permission roles. For each profile in the account, users are assigned a permission role to determine their access level.

The following table describes the four available server-side permission roles:

| PERMISSION ROLE                   | DESCRIPTION                                                                                                                                                                                                                                                                                                            |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **No Access (default)**           | <ul><li>This is the default role for all users other than account administrators.</li><li>The **No Access** permission role does not grant any access to the server-side profile.</li><li>If the user attempts to access the server-side, their profile is blocked and an **Access Denied** message appears.</li></ul> |
| **Reader**                        | <ul><li>The **Reader** permission grants read-only access to the server-side profile.</li><li>A user in this role can browse the profile configuration, but **Save/Publish** is disabled. Users with this role cannot save any changes.</li></ul>                                                                      |
| **Editor**                        | <ul><li>The **Editor** permission grants edit and save access to the server-side profile.</li><li>With this role, you can save but not publish.</li><li>Users with this role can also access and edit settings from the **Profile Admin > Settings** menu.</li></ul>                                                   |
| **Publisher<br> (Admin default)** | <ul><li>This is the default role for account administrators.</li><li>The **Publisher** permission grants the same access as the **Editor** role, with the addition of the ability to save and publish the profile.</li></ul>                                                                                           |

Profile access between the server-side and client-side product is mutually exclusive. For example, you can grant Save and Publish permissions for client-side products without impacting server-side product permissions for a given profile. In addition, if you remove or change user access to a profile on the client-side, it is not removed or changed on the server-side.