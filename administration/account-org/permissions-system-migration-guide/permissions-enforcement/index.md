---
title: Permissions Enforcement
description: This document describes how to use Permissions Enforcement in the platform permissions system.
url: https://docs.tealium.com/administration/account-org/permissions-system-migration-guide/permissions-enforcement/
---
## How it works

Permissions Enforcement disables the legacy permissions system for an account and enables platform permissions.

Permissions Enforcement was released in two phases:

* **Phase 1**: Server-side permissions and the privacy admin, technical admin, and user admin roles.
* **Phase 2**: Client-side permissions and the account admin and profile admin roles.

After you have created the necessary permission groups, assigned users and profiles to permission groups, and assigned account role permissions to users, the account admin can turn on Permissions Enforcement to enforce the permission settings for all assigned permission groups and profiles for the account.

Before turning on Permissions Enforcement, make sure that users have been added to permission groups and admin role permissions have been assigned to users that manage users, permission groups, and PII permissions. If Permissions Enforcement is turned on before users have been added to permission groups, users cannot access Tealium.

## Manage Platform Permissions

To turn on Permissions Enforcement:

1. In the admin menu, click **Manage Permissions**.
1. In the **Permissions Enforcement** section, click **Manage**.
1. Set the switches to **ON** for Phase 2 (and Phase 1) or Phase 1.
1. A success message appears, and the platform enforces permissions for the sides of the platform that you selected.

To revert the account to legacy permission settings, click the switch for that side of the platform **OFF**. You cannot revert Phase 1 permissions without also reverting Phase 2 permissions.