---
title: Save and Publish
description: Before we finish, it is important to understand how the save and publish process works and how to navigate your version history. This section will explain the difference between Save, Save as, and Publish and how to view your version history.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/save-publish/
---
## Save

When you add, edit, or delete an element in your Customer Data Hub account you must save your changes. If you logout or close your browser without saving, your changes will be lost. Similarly, your changes will not be visible to other users in your account until you have saved them.

The **Save/Publish** button will change to green to indicate that there are unsaved changes:

![](https://docs.tealium.com/images/tutorials/getting-started-save-publish-button.png)

## Publish

Once you save your changes, you can log out or close the browser and your configuration will be preserved for you or the next user that logs into the account.

Saving ensures that you don't lose your work between working sessions, whereas publishing activates your changes. Publishing affects your connectors and actions. For example, you could set up a new connector action and save it without publishing and no actions would get triggered. But once you publish, the changes are activated and connector actions begin triggering and sending data to your vendors.

The Customer Data Hub only has one publish environment, the production one, so every publish affects your production environment. In lieu of a QA environment, you can create "test" attributes that you populate during your testing to isolate new configurations.

## Versions

To access your save and publish history, use the following methods:

* Click the profile switcher in the heading.
* Select **Server-Side Versions** in the sidebar.

Your save history is organized into versions. When you use **Save As** to save a version, you create a new version and can revert back to a previous version. When you use **Save**, you create a new revision, typically intended for minor changes, and cannot revert back to a previous revision.