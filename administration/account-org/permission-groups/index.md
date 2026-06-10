---
title: Permission groups
description: This article describes how to manage permission groups in the platform permissions system.
url: https://docs.tealium.com/administration/account-org/permission-groups/
---
## How it works

A permission group consists of the following components:

* A list of users.
* A list of profiles and access levels on those profiles. 
* A list of product features and permissions for those product features, which includes publishing rights for client-side profiles.
* Publishing rights for server-side profiles.

Permission groups can be granted the following feature permissions:

* **No Access**: The permission group does not have access to the feature and it will not appear in their navigation.
* **View**: The permission group can view the feature and data it contains, but they cannot edit it.
* **View &amp; Edit**: The permission group can view the feature and data it contains, and they can edit the data.
* **View, Edit, &amp; Delete**: The permission group can view the feature and the data it contains, and they can edit or delete the data.

![](/images/administration/permission-groups-products-features-example.png)

Users that have **View &amp;amp; Edit** or **View, Edit &amp;amp; Delete** permission also have **Save** permission for their changes to a profile.

The interface changes based on the user&#39;s permissions:

* If a user does not have access to a product, that product does not appear in the navigation.
* If a user has access to some features, but not others, they only see the features they can access in the navigation.
* If a user does not have edit permission for a feature, the **Edit** button does not appear on pages for that feature.

A permission group can also be granted publishing rights for server-side profiles. Users in a permission group with server-side publish permissions automatically receive full access to all server-side products and features.

 Granting publish permissions to a group may result in users receiving greater permissions on products and features than you intend to give them. For example, an AudienceStream-only developer that you grant publishing rights to will receive with full permissions on a profile, which would include EventStream, DataAccess, and every other server-side product and feature.&lt;br&gt;&lt;br&gt;To avoid granting users greater permissions than necessary, we  recommend that you create a separate permission group with publishing permissions for each of your server-side profiles. 

For more information, see [About platform permissions]().

### Product features

Product access is divided into feature permissions.

For example, access to AudienceStream is divided into the following feature permissions:

* Dashboard
* Discovery/Sizing
* Audiences
* Audience Connectors
* Visitor/Visit Attributes

#### Permissions to features in multiple products

Carefully consider when you set a user to **No Access** for a feature or product. If you disable feature access for a user, that user cannot access the feature or any other features that depend on it. For example:

* If you set a user to **No Access** for AudienceStream, that user cannot select an audience to action in an AudienceStream connector.
* If you set a user to **No Access** for server-side labels, the user does not see labels on the server-side. They can still access connectors or other features with labels on them, but they cannot see or edit the labels themselves.
* AudienceStream and EventStream share several features, such as rules and labels. For example, if a user only has permissions for AudienceStream and they edit a rule in AudienceStream that is shared between AudienceStream and EventStream, the rule will change in EventStream, too.

#### Tealium Insights permissions

Insights user roles are managed through the **Analyze &gt; Insights &gt; QuickSight Users** page. However, Insights users must also be a member of a permission group with view access to the Insights feature.

For more information, see [About Tealium Insights]().

### Publishing permissions

Permission groups also manage publishing permissions on the client-side and server-side.

* On the client-side, set publishing rights with the **Publish to Dev/Custom**, **Publish to QA**, and **Publish to Prod** feature permissions.
* On the server-side, set publishing rights on the **Group Permissions** tab of the permission group.

Permission groups have publishing rights on the profiles to which you give them access.

Remember, a permission group can also be granted publishing rights for server-side profiles. Users who are members of a permission group with server-side publishing rights have full access to all server-side products and features.

&lt;!-- #### Publishing changes to features in multiple products

If you disable a product for a user, but the user has server-side publish permission and access to another product that shares features with the first product, the user can still publish changes to those shared features. For example, EventStream and AudienceStream share some features, such as rules and labels.

If a user has publish permission and only has access to EventStream, they can publish changes made to rules and labels in EventStream, and those changes also affect AudienceStream. Similarly, if a user has publish permission and only has access to AudienceStream, their published changes to rules and labels also affect EventStream. --&gt;

### Users in multiple permission groups

Access rights to profiles are cumulative. The user always receives the highest level of access granted by their permission groups, even if the permission groups have conflicting permissions.

For example, Group A has **View** permissions on a profile, while Group B has **View &amp; Edit** permissions on that profile. A user in both Group A and Group B has **View &amp; Edit** permissions on that profile.

 A user with the profile admin role has full permission on all profiles in the account.
 

## Manage permission groups

To manage permission groups, in the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears, displaying the **Groups** table.

### View a permission group

Click a permission group to display that permission group&#39;s details. Click one of the following tabs to display more details about that permission group:

* **Users**: Lists the users who are a member of the permission group.
* **Group Permissions**: Lists the group member permissions for products and features.
* **Profiles**: Lists the profiles and the group member permissions for those profiles.

### Create a permission group

To create or edit a permission group, you must have the account admin or the user admin role. To add a permission group to a profile, you must have the account admin or the profile admin role.

To create a permission group, set the access level for each product feature, and then invite users to join the account and the permission group:

1. From the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears.
1. Click **&#43; New Group**. The **New Permission Group** slideout appears.
1. In the **Name** box, enter a name for the permission group.
1. Select what the permission group initially contains:
    * **Blank Group** - Start a permission group without any existing settings.
    * **Duplicate an Existing Group** - Start a new permission group with the same permissions, profiles, and users of the permission group that you select.
1. Click **Next**. The **Set Account Permissions** slideout appears.
1. If you want to give the group permission to publish profile changes, under **Server-Side** select **Publish.** Remember that server-side publishing rights include full access to all server-side products and features.
1. Select the products you want the permission group to access.
1. Click **Next**. The **Feature Permissions** slideout appears.
1. Under **Feature Permissions**, select the access level for each product feature.
    * Some features appear in multiple products, such as access to connectors. Feature access levels apply to the feature, regardless of which product it appears in.
    * **Edit** access for a product feature includes the ability to save changes to the profile.
1. Click **Next**. The **Profiles** slideout appears.
1. Select the profiles to allow the permission group to access.
1. Click **Next**. The **Add Users** slideout appears.
1. Select up to 25 users to add to the permission group.
    * To add a user who is not already on your account, you must add the user to the account first. For more information, see [Users]().
1. Click **Add**.

The **Manage Permissions** screen appears and the new permission group appears in the list.

### Edit a permission group

To edit a permission group:

1. From the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears.
1. Click the **Permission Group** tab.
1. Click the permission group you want to edit. The permission group details appear.
1. Select the information you want to edit:
    * **Group Permissions**: Set the permission group access levels for product features.
    * **Users**: Add or remove users from the permission group. 
    * **Profiles**: Add or remove profiles from the permission group and set the permission group access levels for that profile.

### Manage user permission groups

To manage permission group membership from a user’s profile:

1. From the admin menu, click **Manage Permissions**. The **Manage Permissions** screen appears.
1. Click the **User** tab.
1. Click the user that you want to edit. The **User Details** slideout appears.
1. Click the **Group** tab, and then click **Edit**.
1. Select the permission groups you want to add the user to or remove them from.
1. Click **Finish**.