---
title: Save and publish
description: This section explains the save and publish process and how to navigate your version history.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/save-publish/
---
## Save

When you add, edit, or delete an element in your account, you must save your changes to preserve that work. If you log out or close your browser without saving, your changes are discarded. Similarly, your changes are not available to other users of your account until you save them.

The **Save/Publish** button turns orange to indicate that there are unsaved changes:

![](https://docs.tealium.com/images/server-side/getting-started-save-publish-button.png)

In the **Save** dialog box you have the option to **Save As**, in which you must set a descriptive title for the new version.

![](https://docs.tealium.com/images/server-side/getting-started-eventstream-save-publish.png)

Use this option to re-publish (rollback) to a previous version. If you only save your changes, you cannot revert to the state that existed prior to your changes.

## Publish

After you save your changes, you can log out or close the browser. Your configuration is preserved for you or the next user that logs into the account. However, until you publish, your configuration won't be active.

Publishing affects your connectors and actions. For example, you could set up a new connector action and save it without publishing, and the action would not get triggered. But after you publish, the changes are activated, and connector actions begin triggering and sending data to your vendors.

EventStream only has one publish environment, so every publish affects your production environment. To mimic a QA environment, create test attributes to set during your testing, and then use them to test new event feeds, enrichments, and connectors.

## Versions

To access your save and publish history, use the following methods:

* Click the profile switcher in the heading.
* Select **Server-Side Versions** in the sidebar.

Your save history is organized into versions. When you use **Save As** to save a version, you create a new version and can revert back to a previous version. When you use **Save**, you create a new revision, typically intended for minor changes, and cannot revert back to a previous revision.


<blockquote>
Write descriptive notes when you save. It's a great habit to form that your co-workers will appreciate. Plus, it will remind you of what you did. You'd be surprised how easily you can forget your own work!
</blockquote>


Well, that about wraps it up. The final page in the tutorial lists additional resources.