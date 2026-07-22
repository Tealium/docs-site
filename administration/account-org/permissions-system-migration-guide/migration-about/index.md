---
title: Permissions system migration guide
description: This document explains Tealium's migration plan for platform permissions and the benefits of migration.
url: https://docs.tealium.com/administration/account-org/permissions-system-migration-guide/migration-about/
---
## How it works

Previously, account administrators had to manage client-side users, server-side users, and administration rights separately. Separately administering accounts required a lot of time and effort to audit each user’s viewing and editing rights as well as manage their access to profiles.

Tealium now provides a unified permissions system that lets you manage user access to your account and profiles through permission groups and admin roles. Permission groups can manage user access to both client-side and server-side profiles, simplifying the process of assigning and managing permissions.

For more about the new permissions management system, see [Platform Permissions System](https://docs.tealium.com/about-platform-permissions/).

## Terminology

Before you plan out your migration strategy, review the following basic concepts:

* **Product**: A grouping of features licensed at the account level (for example, AudienceStream CDP, EventStream API Hub, iQ Tag Management, etc.)
* **Feature**: A subsection of a product that allows management and access to data and configurations.
* **Account**: Contains configuration and access that spans multiple profiles.
* **Profile**: A configuration set for either server-side or client-side products and features.
* **User**: An individual login to an account, defined by the user’s email address.

The platform permissions system introduces the following two new concepts:

* [**Permission group**](https://docs.tealium.com/permission-groups/): (usually referred to as **group**) defines a set of access levels to product features in specific profiles. They also determine access to publishing. Users in a group receive permissions for the associated profiles, making it easier for you to manage permissions for a large number of users.
* [**Admin role**](https://docs.tealium.com/admin-roles/): grants access to specific account-level features. Use admin roles to delegate specialized or highly sensitive responsibilities to trusted members of your team. Users without admin roles receive a basic user role.


<blockquote>
To access Tealium, users must be assigned to one or more permission groups that provide the necessary product and feature permissions.
</blockquote>


## Tealium's project rollout plan

We plan to roll out platform permissions in the following steps:

1. All new customers after December 18, 2023 use platform permissions to manage their Tealium account.
1. Existing customers are migrated to EEA platform permissions without Permissions Enforcement enabled, so they can continue to use legacy permissions until they are ready to migrate.
1. Tealium assists existing customers with setting up platform permissions for their accounts.
1. Customers enable Permissions Enforcement to change from legacy to platform permissions.
    * If your users encounter problems, disable [Permissions Enforcement](https://docs.tealium.com/permissions-system-migration-guide-permissions-enforcement/) to roll back to legacy permissions while you diagnose and fix the problems.
1. When all customers are on platform permissions, platform permissions EEA becomes platform permissions GA.

## Benefits of migration

Migrating from the old permissions system to the new one gives you an opportunity to audit the permissions, security, and structure of your account:

* Remove users who no longer use the platform or work for your organization.
* Use admin roles to delegate account management responsibility to others.
* Remove unnecessary levels of access on the platform.
* Organize access to profiles for easier management.
* Give permission groups descriptive names for easier security auditing and management.
* Gather data for any future plans to break up profiles into multiple regional profiles to better handle regional brands, offices, management structures, and data privacy compliance regulations.
* It is easier for Tealium Support to assist you with access issues on the platform permissions system than with the legacy system.