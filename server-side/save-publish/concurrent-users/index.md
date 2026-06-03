---
title: Concurrent users
description: This article explains how the platform manages changes from concurrent users.
url: https://docs.tealium.com/server-side/save-publish/concurrent-users/
---
## Requirements

* [Platform permissions]() enabled on the account.

## Overview

The server-side platform offers support for managing changes from concurrent users who are logged into the server-side platform at the same time.

The following functionality is supported:

* Users see active collaborators displayed in the UI.
* Logged-in users receive in-app notifications about save and publish actions from other users.
* Saved changes from other users are made available to integrate into your unsaved changes.

To understand the possible concurrency scenarios, the following terms are helpful:

* **Currently published version**: The configuration set that is currently in production.
* **Current version**: The configuration set that you are working on.
* **Your changes**: The unsaved changes you have made to the current version.

## Enable concurrency

To enable concurrency on a profile, use the following steps:

1. In the admin menu, click **Manage Concurrency**. The **Manage Concurrency for this Profile** screen appears.
1. Toggle **Enable Concurrency** to **On**.

## How it works

When you are logged in and anticipate changes from concurrent users, it&#39;s important to know which version you are working in. The current version is displayed in the heading, below the account and profile:

![](/images/server-side/save-publish/server-side-concurrency-heading.png)

When you want to start a new long-term project, load the currently published version using the profile switcher and perform a **Save As** to create a new version for your planned changes. Make all configuration changes to the new version. When the changes are completed and tested, publish the new version to production.

When you make changes to a version, logged-in users who have that version loaded are notified, even if you haven’t saved or published the changes. After you save the changes, those other users are notified that they can integrate those changes into their versions to ensure they have the latest updates. If you do not immediately update your version to include those changes, you can include the changes the next time you save or publish.

## Viewing other active users

When you log in, the product area that you are working in is highlighted in blue in the left navigation bar. If another user is also logged in and active on your version, that user&#39;s initials appear as a circle with a unique background color at the top of the screen. The same unique color is used to highlight which area of the product the other user is currently working in, as shown in the following example:

![](/images/server-side/whiteui-udh-concurrent-user-management-udh-3-users-logged-in.png)

## Another user starts a change

If another user starts making changes to the version you are using, a message notifies you of unsaved changes in progress:

![](/images/server-side/save-publish/another-user-is-making-changes.png)

Click **Got it** to acknowledge the message.

## Another user saves their changes

When another user saves changes to a version you are working on, you will receive a notification message. The notification message depends on whether you have made changes to the version.

### You have not made changes

If you have not made any changes, the following notification appears:

![](/images/server-side/save-publish/concurrency-notification-nochangesmade.png)

Click **Update** to refresh the screen and load the other user&#39;s saved changes.

### You have made changes

If you have made changes, the following notification appears:

![](/images/server-side/save-publish/concurrency-notification-changesmade.png)

Click **Save** to integrate the other user’s changes into your work. A new dialog opens that contains information about the save:

![](/images/server-side/save-publish/review-changes.png)

The **Changes to be saved** or **Changes to be published** table contains the following information:

* The type of change.
* The name of the item that changed.
* The action on that object (Updated, Created, or Deleted).
* The user who made the change.

If both your changes and those in the latest published version have altered the same item and the system cannot reconcile the changes, an **Overwrite** badge will appear next to it.

![](/images/server-side/save-publish/concurrent-user-publish-conflict.png)

Publishing your version replaces the existing items in the published version with yours.

## Another user publishes

When another user publishes a version, regardless of the version you are on, a message appears to inform you of that publish:

![](/images/server-side/save-publish/another-user-published.png)

We recommend that you save and include those changes to keep your version up to date. For more information, see [Save and Publish]().