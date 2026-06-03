---
title: Manage and generate API keys
description: This article describes how to manage and generate API keys used to authenticate with the Tealium API.
url: https://docs.tealium.com/administration/security-access/api-keys/
---
## Requirements

* To generate or revoke your own API key, another user with the Manage Users legacy permission or the [user admin role]() in your primary account must authorize you.
* To authorize API keys for users on the same primary account as you:
    * You must have Manage Users legacy permissions or the [user admin role]().
    * You must be on the same primary account.
    * The user must have logged in to the platform at least once. 

## How it works

API keys authenticate with the [Tealium API](/api/) and are linked to individual user accounts.

API keys are generated as follows:

1. An administrator with the Manage Users legacy permission or the [user admin role]() authorizes an API key for one or more users.
1. The authorization action triggers an email to the affected users, which notifies them that they are authorized to generate an API key. Those users can then generate their own API key.

API keys can be authorized, revoked, and generated. The API key is displayed only once. After closing this window, it cannot be retrieved. Lost or forgotten keys must be reset or revoked by a user with the Manage Users permission.

### About the Manage Users permission

Users with the **Manage Users** permission can do the following:

* Authorize (or reset) API keys for other users within their primary account.
* Revoke API keys for other users within their primary account.

Any user who has been authorized to generate an API key can do the following:

* Generate or reset their own API key.
* Revoke their own API key.

## Managing API Keys

This section describes how to:

* Authorize a user to generate their own API key.
* Generate your own API key.
* Manage API keys (authorize, reset, or revoke) for one or more users.

### Authorize a user to generate API keys

To authorize a user to generate API keys, you must be an administrator with the Manage Users legacy permission or the [user admin role](). This step does not generate keys for a user, but authorizes them to generate their own API key.

Use the following steps to authorize a user to generate their own API keys:

1. In the admin menu, click **Manage Users**. The **User Manager** dialog is displayed.
1. Use the checkboxes to select one or more users to manage.
1. Click **Edit/View User Settings**.
1. In the left side panel, click **API Key**.
1. Click **Authorize Generation**.  
    ![](/images/iq-tag-management/whiteui-tiq-managing-and-generating-api-keys-authorize-generation.jpg)  
    A message displays that the API key authorization email was sent.
1. Click **Close** to close the window.

### Generate an API key

Users must be authorized before generating their own API key. Once authorized, they receive an email notification with instructions to generate the API key.

After the email is received, users can generate their own API key using the following steps:

1. In the admin menu, click **Edit/View User Settings**.
1. In the left side panel, click **API Key**.
1. Click **Generate Key**.  
The API key is generated and displayed in a pop-up window.  
      The API key is only shown once and cannot be viewed later. Once you close this window, the API key cannot be displayed again.
1. Copy the API key to a secure location before proceeding.
1. Click **Close** to close the window.

### Manage API keys for single users

Use the following steps to manage API keys for a single user:

1. In the admin menu, click **Manage Users** from the drop-down list.  
The **User Manager** dialog is displayed.
1. Click the checkbox next to the user for which you want to manage the API key.
1. Click **Edit/View User Settings**.  
    ![](/images/iq-tag-management/whiteui-tiq-managing-and-generating-api-keys-user-manager-editview-user-settings.jpg)
1. In the left side panel, click **API Key**.
1. Select one of the following actions:
      * **Authorize Generation**  
      Authorizes the user to generate their own key.
      * **Reset Key**  
      Resets the existing key and authorize a new key to be generated.
      * **Revoke Key**  
      Revokes the existing key.
1. Click **Close** to close the dialog.

### Manage API keys for bulk users

API keys can be authorized, reset, or revoked in bulk.

Use the following steps to manage API keys in bulk:

1. In the admin menu, click **Manage Users** from the drop-down list. The **User Manager** dialog is displayed.
1. Click the checkbox next to each user for which you want to manage the API key.
1. Click the **More** drop-down list and select **Manage API Keys**.  
    ![](/images/iq-tag-management/whiteui-tiq-managing-and-generating-api-keys-admin-select-users.jpg)  
    The selected users appear in the left panel.
1. Select one of the following actions:
    * **Authorize / Reset Keys**  
        * Authorizes new users to generate an API key and resets the API key for existing users.
        * Existing keys are immediately invalid and the user must then generate a new API key.
    * **Revoke Keys**  
        * Revokes existing API keys for selected users.
        * Revoked keys become inactive immediately for the selected users.
1. Click **Save**.  
A confirmation message is displayed and an email notification regarding the update is sent to the affected users.
1. Click **Close** to close the window to return to the previous screen.
