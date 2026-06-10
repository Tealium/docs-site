---
title: Manage extensions
description: This article explains how to manage extensions.
url: https://docs.tealium.com/iq-tag-management/extensions/manage/
---
## Add extensions

Use the following steps to add an extension:

1. In the sidebar, navigate to **Tag Management &gt; Extensions**.
1. Click **&#43; Add Extension**.
1. Browse the extension categories using the multi-tab menu and click **&#43; Add** next to the extension you want to use.
1. Enter a **Title** to identify the extension.
1. (Optional) Click **Apply Labels** on the left to add a label to categorize the extension.
1. Under **Scope**, select a scope from the drop-down list or click **Edit Load Order**.  
Learn more about the [Load Order Manager]().
1. Click **Apply**.
1. Configure additional settings pertinent to the extension.

## Publish locations

![](/images/iq-tag-management/whiteui-tiq-extensions-publishlocations.png)

The publish location settings control which environments the extension will be published to. If you uncheck a publish location, the extension will not be published to that location. For example, if you uncheck **Prod** for an extension, and then publish to Prod, that extension will be omitted from the files in the Prod environment.

### Available publish locations

The following publish locations options are available:

* **Dev**  
The development (Dev) environment is a non-production environment intended for sandbox configuration.
* **QA**  
The Quality Assurance (QA) environment is a non-production environment intended for testing prior to releasing to production.
* **Prod**  
The Production (Prod) environment is the environment you intend to load on your live website.
* **Custom**  
(Optional) The Custom Environments selection only appears if previously configured using [Custom Environments]().

Publish locations can be used to prevent extensions that are in development from accidentally being published to Prod. For example, you may be working on a new extension and need it active for your QA environment, but do not want it to be included in any publishes to Prod. In this case, you simply uncheck the Prod publish location and the extension can remain active and not affect your Prod environment.

## Duplicate extensions

An easy way create an extension is by copying an existing one that has similar functionality.

Use the following steps to copy an extension:

1. Expand an extension.
1. In the left side panel, click **Duplicate**.  
A copy of the original extension is added to the bottom of the extension list.
1. Adjust the configuration of the new extension as needed.

## View extension change history

To view the change history of an extension:

1. In the sidebar, go to **Tag Management &gt; Extensions**.
1. Click the extension you want to review. The extension details appear.
1. Click **View Change History**.

## Edit extensions

Extensions are editable directly from the extensions view. Expand an extension and adjust the configuration. As changes are detected, the **Save/Publish** button will turn orange to indicate unsaved changes exist.

Tealium does not recommend editing the uTag Sync extension.

## Deactivate extensions

To turn off an extension and still keep it in your account for later use, use the **On/Off** switch. This is usually a better option than permanently deleting the extension because you will not lose the effort of the initial configuration.

Use the following steps to deactivate an extension:

1. Click the **On/Off** toggle next to the extension to deactivate.  
A confirmation dialog appears.
1. Click **Deactivate** to confirm your action.  

![](/images/iq-tag-management/whiteui-tiq-deactivateextension.png)

## Delete extensions

If an extension is no longer needed, it can be deleted permanently from the configuration.

Use the following steps to delete an extension:

1. Expand an extension.
1. In the left side panel click **Delete**.  
A confirmation dialog appears.
1. Click **Drop Extension** to confirm the action. 
 
![](/images/iq-tag-management/whiteui-tiq-dropextension.png)

If you accidentally delete an extension and have not saved the profile, you can reload the browser to return to the original state of your extensions.