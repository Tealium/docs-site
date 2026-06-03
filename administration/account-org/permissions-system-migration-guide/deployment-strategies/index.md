---
title: Deployment Strategies
description: This document describes example deployment strategies for migrating to the platform permissions system.
url: https://docs.tealium.com/administration/account-org/permissions-system-migration-guide/deployment-strategies/
---
## Deployment strategies

Now that you have your planned list of users, permission groups, and admin roles, you’re ready to deploy your permissions structure.

* For instructions on how to create a permission group, see [Permission Groups]().
* For instructions on how to assign an admin role to a user, see [Admin Roles]().
* For instructions on how to invite and manage users, see [Users]().

The following examples describe strategies for deploying the platform permissions system:

### Deployment Strategy 1 - Build job functions and roles, then add people

This strategy uses small groups of users with identical needs and roles that you generated after the final audit of your inventory. Users with similar or identical responsibilities can be bundled and added to groups with the correct permissions and access.

The advantage of this method is that you are organizing users into groups based on similar job responsibilities and roles in your organization, so group membership parallels your organization chart and workgroups.

The disadvantage is that users who perform multiple or overlapping roles or require special access may need some extra planning and adjustment.

To manage permissions through role-based permission groups for your account:

1. Assign admin roles to the users that will help you with migration and testing.
1. Create permission groups for groups of users with identical needs and roles.
1. Add users to the appropriate permission groups.
1. Warn your users that you will be testing the platform permissions system and ask for feedback.
1. Set the [Permissions Enforcement]() switches to **ON**.
1. Gather feedback from your users, and implement any changes in permissions that are necessary.
1. If there are too many permission and access issues to deal with quickly, set the **Permissions Enforcement** switch to **OFF** so you can revise your plans, permission groups, and admin roles before running another test.

For more information about Permissions Enforcement, see [Permissions Enforcement]().

### Deployment Strategy 2 - Stacked granular permission groups

Another possible strategy for creating permission groups uses stacking of multiple permission groups to build access for each user. This strategy uses the additive property of permission groups, where a user who is a member of multiple groups inherits the greatest access of those permission groups. This strategy lets you manage your users through multiple layers of resource access permission groups instead of job role or workgroup-based permission groups.

The advantage of this method is that you are organizing permission groups by a resource’s permission levels, and you can add or remove users from permission groups as their needs change.

The disadvantage of this method is that you need to manage many more permission groups when a new user joins your organization or when a user changes job responsibilities or leaves. There are also a large number of permission groups to build and set permissions for, which takes a lot of time to configure and test.

For example, if you create permission groups to manage publishing for three client-side profiles, you need to create nine permission groups:

* Profile 1, Publish to Dev
* Profile 1, Publish to QA
* Profile 1, Publish to Prod
* Profile 2, Publish to Dev
* Profile 2, Publish to QA
* Profile 2, Publish to Prod
* Profile 3, Publish to Dev
* Profile 3, Publish to QA
* Profile 3, Publish to Prod

 This method becomes even more complex if the account uses custom publishing environments
 

To manage permissions through stackable permission groups for your account:

1. Assign admin roles to the users that will help you with the migration and testing process.
1. Create 4 permission groups: **Publish to Dev/Custom**, **Publish to QA**, **Publish to Prod**, and **Publish Server-Side**.
    * Assign users to these permission groups as necessary based on their rights to publish.
1. Create permission groups that bundle access to product features as needed for various roles in your organization (Development, QA, Data Manager, Account Manager, etc.)
    * Add users to the appropriate permissions groups.
    * Set **View**, **Edit**, and **Delete** rights on each feature as necessary.
    * Set server-side publishing rights as necessary. Remember that server-side publishing rights include full access to all server-side products and features.
1. Add users to the appropriate permission groups.
1. Set PII permissions for each of your users.
1. Warn your users that you will be testing the platform permissions system and ask for feedback.
1. Set the **Permissions Enforcement** switches to **ON**.
1. Gather feedback from your users, and implement any changes in permissions that are necessary.
1. If there are too many issues to deal with quickly, set the Permissions Enforcement switches to **OFF** so you can revise your plans, permission groups, and admin roles before running another test.

For more information about Permissions Enforcement, see [Permissions Enforcement]().