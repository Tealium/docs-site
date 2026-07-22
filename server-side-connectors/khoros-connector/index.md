---
title: Khoros Connector Setup Guide
description: This article describes how to set up the Khoros connector.
url: https://docs.tealium.com/server-side-connectors/khoros-connector/
---
## Supported Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add Role to User| ✓| ✗|
|Remove Role from User| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. For more information, see  [Connector Overview](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Khoros Login Name**: (Required) The login name for the Khoros community administrator.
* **Khoros Login Password**: (Required) The password for the Khoros community administrator.
* **Khoros Community URL**: The URL for the Khoros community. For example: `community.my-community.com/`. Do not include the protocol and end with a trailing `/`.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add Role to User

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Add User to Role| Select the Khoros role to add the user to. Khoros badges must be linked to Khoros roles so AudienceStream can manage Khoros badges. When AudienceStream provisions the role, the badge will be awarded in Khoros. If the role is revoked, the badge **will not** be removed. The only way to remove a badge from a user in Khoros is to delete the badge from the system, removing it from all users.|
|User Id| The user ID to search for.|
|Username| The username to search for.|

### Action - Remove Role from User

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Remove User From Role| Select the Khoros role to remove the user from. Khoros badges must be linked to Khoros roles so AudienceStream can manage Khoros badges. When AudienceStream provisions the role, the badge will be awarded in Khoros. If the role is revoked, the badge **will not** be removed. The only way to remove a badge from a user in Khoros is to delete the badge from the system, removing it from all users.|
|User Id| The user ID to search for.|
|Username| The username to search for.|
