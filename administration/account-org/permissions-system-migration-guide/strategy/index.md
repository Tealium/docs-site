---
title: General Strategy
description: This document describes a general strategy to follow when building a migration plan for the permissions system.
url: https://docs.tealium.com/administration/account-org/permissions-system-migration-guide/strategy/
---
## General migration strategy

Use the following steps to help you build your migration strategy:

1. Make an inventory of your users’ current access levels and permissions.
1. Audit those permissions to ensure they’re accurate for the users’ needs.
1. Analyze the results of your audit to determine logical functional groups.
1. Add permission groups to match those bundles of access rights to profiles and product features.
1. Add users to those permission groups.
1. Assign admin roles to users in your account to delegate management of users, features, and profiles.
1. Set PII permissions for each user.
1. Test the permissions with your users.
1. Test saving and publishing rights with your users.
1. Adjust the permission groups and admin roles as needed.

If you need assistance with this process, please contact Tealium Support.

## Migration suggestions

Some important things to consider as you plan your migration:

* **Non-disruptive migration** - Building your permissions groups and admin roles under the platform permissions system will not disrupt your current permissions and access. Your account continues to use the legacy permissions until you enable Permissions Enforcement to use the platform permissions system. If you have any major problems with the platform permissions system, you can switch back to the legacy system to make any necessary changes.
* **Permission groups are cumulative** - You can create a permission group with view rights on one profile, create another permission group with editor rights on other profile, and then add a user to both. The user inherits permissions from both groups, and if the permissions overlap, the user inherits the greater permissions for a resource.