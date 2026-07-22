---
title: Data Connect roles
description: This article provides an overview of Data Connect roles and how to set them for each Tealium profile.
url: https://docs.tealium.com/server-side/data-connect/roles/
---
Control how users access Data Connect recipes for each Tealium profile by assigning a role to that profile. Each profile can see only those recipes created in that profile. 

For more information about editing user permissions, see [About server-side permissions](https://docs.tealium.com/about-managing-server-side-user-permissions/).

## Available roles

Data Connect provides three levels of recipe permissions for Tealium profiles:

* **Recipe Creator** - Can create, edit, delete, and run Data Connect recipes.
* **Recipe Editor** - Can edit and run Data Connect recipes.
* **Data Connect User** - Can run Data connect recipes. 

All Data Connect roles can access data from Workato recipes. The default role is **Data Connect User**.

## Prerequisites
Before you can assign Data Connect roles, you need to enable personally identifiable information (PII) permissions for each Data Connect user.

1. In the admin menu, click **Manage Users**.
1. Toggle **PII Permissions Enforcement** to **ON**. 

## Set a Data Connect role

To set a Data Connect role, complete the following steps:

1. Log in to the server-side area for appropriate Tealium account and profile.
1. In the admin menu, click **Manage Users**.  
A list of all server-side users appears, including the user’s name, email address, and a timestamp for their last login.
1. Click a user to display the permission details.
1. Click **Next**.
1. In the **Account Permissions** screen, scroll to the **Data Connect Roles** section.
1. Select the permission level you want to grant to this profile.
1. Click **Save**.

