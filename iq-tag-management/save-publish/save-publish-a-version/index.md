---
title: Save and publish a version
description: This document explains how to save and publish your settings.
url: https://docs.tealium.com/iq-tag-management/save-publish/save-publish-a-version/
---
## Save/Publish dialog

When you are ready to save and publish your settings, click **Save/Publish**.

![](/images/iq-tag-management/save-publish/client-side-publish-window.png)

### Publish Details

The **Publish Details** table displays information about your changes in this version:

* **Changes**  
This tab lists changed elements that will be saved to this version and published, including any changes as a result of updated [profile libraries](). Changes to a library do not automatically propagate to all the profiles that load it. You must re-publish each profile to include the changes to the library.
    * **Type**: The type of element (`extension`, `tag`, `event`, `load rule`, `variable` or `template`).
    * **Element Name**: The title of the element.
    * **Change**: The change performed on the element (`Added`, `Updated`, `Removed`, `Toggled On`, `Toggled Off`).
    * **Library**: The profile library this element comes from.
    * **UID**: The unique ID of the element.
* **Linked Profiles** (Profile libraries only)  
This optional tab lists profiles that are linked to this profile library. Changes to a library do not automatically propagate to all the profiles that load it. You must re-publish each profile to include the changes to the library.

### Last Published by Environment

The **Last Published Version by Environment** section of the screen lists historical details, including the environment name, version name, timestamp, the author of the change, and notes.

To compare your changes to an environment version, click **Compare** next to the version you want to compare your session’s changes to. A window is displayed that lists information about the selected environment version and compares that version to the changes you want to save and/or publish. A yellow star appears in every row that contains an unsaved change.

## Save/Publish your version

To save and publish a new version that contains your changes, perform the following steps:

1. In the **Version** field, enter the name of the new version.
    * This creates a new version, preserving a copy of the previous version. This is the default setting and the recommended save method because it provides the ability to roll back changes and retrieve previous versions.
    * This is a required field. By default, the **Version** field displays a date and timestamp.
1. (Optional) If you want to overwrite the current version, select **Overwrite current version**. This option will replace the current version, and you cannot undo your changes to it.
1. In the **Notes** field, enter notes about changes you made to the version.
The notes entered in this field are useful if you need to roll back to this version in the future. This is a required field, you cannot save the version without entering notes.
1. (Optional) Select one or more [Publish Locations]() to publish this version to a publishing environment. You can also select **Custom** to select a [custom environment]().

When you are ready to save or publish, click **Save** or **Publish**.

If you select at least one publish environment, the action button displays **Publish**. Otherwise, it displays **Save**. Click **Publish** or **Save** to begin the process of saving and/or publishing your version.

 For more information about approval workflows, see [Publish Workflow Management]() 

## Validating

When you complete a save and publish, new code is generated and the files are updated. This process can take a few minutes. The primary tool for verifying the status of the Universal tag (`utag.js`) on your site is **Web Companion**.

For more information, see [Web Companion]().

### Version number and timestamp

The version number, or timestamp of the current version, is the best way to verify that your changes are live on the site. Match the timestamp from Web Companion to the timestamp of your last publish to verify that your changes are live.

![](/images/iq-tag-management/iq-versions-timestamp.png)

Compare the timestamp to the version displayed in **Web Companion** once the version has been reloaded on the page.

![](/images/iq-tag-management/wc2.png)

The timezone reported in **Tealium iQ** is GMT, while the local timezone is reported within **Web Companion**.
