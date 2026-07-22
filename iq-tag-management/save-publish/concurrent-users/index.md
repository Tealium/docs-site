---
title: Concurrent users (iQ Tag Management)
url: https://docs.tealium.com/iq-tag-management/save-publish/concurrent-users/
---
In iQ Tag Management, concurrent user functionality offers the following features:

* **Profile Level Concurrency**  
Concurrent user tracking occurs at the Profile level. This means that concurrent users in iQ Tag Management that are editing the same profile will receive invitations to merge each other's changes, even if they are saving to different versions.
* **Continuous Merging**  
You can merge another user's in-progress profile changes multiple times before saving those changes. This lets you better collaborate over a period of time on a single profile update.
* **Overwrite Protection**  
To help prevent accidental overwrites, iQ Tag Management prevents concurrent users from saving changes within one minute of each other. If you go to the **Save/Publish** screen less than a minute after a previous save, a time appears that counts down until the next time you can safely save your own changes. The maximum time set is 60 seconds.
* **Guaranteed Latest Version**  
As part of overwrite protection, publishing changes to a profile prompts concurrent users to merge the new changes when the publish completes, not when the publish. This prevents situations in which a user may start to edit while a publish is in progress. For example, a user could be making changes to a profile version that is unknowingly outdated by only a few minutes and would lose the original user's changes when they save.
* **Lock Profile**  
You can use the **Lock Profile** setting in **General Publishing** to disable concurrent users from editing a profile.  
For more information, see: [Publish Configuration]().

The following restrictions apply to concurrent user management in iQ Tag Management:

* **Libraries Not Supported**  
You cannot merge changes to or from a profile version that is linked to a library.  
For more information, see: [Merging Versions]().
* **Resource Locks Enforced**  
You cannot merge changes that include a resource lock if that lock would prevent your user account from saving those changes.  
For more information, see: [Resource Locks]().
* **Merge Conflicts**  
When merging changes that include two different configurations of the same element, you must choose which version of that element to keep.  
For more information, see: [Merging Versions]().

## Viewing and communicating with concurrent users

When there are multiple users logged in to the same profile, the concurrent users icon appears next to the profile name in Tealium iQ for both users.

Use the following steps to view and communicate with other users:

1. Click the **Concurrent Users** icon.  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-concurrentuserstiq-collaboration-icon.png)  
    The **Concurrent Users** dialog displays a list of other users that are currently logged in and working on that profile, including each user's email address, active profile version, and status if there are pending changes.
1. To communicate with the other users and coordinate collaboration, type in the text field and click **Post**.  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-concurrent-users-tiq-post-message-to-other-users.png)
1. Click **Close** to close this window.  
You can click the collaboration icon to reopen the window at any time.

## Collaboration workflows

When another concurrent user saves changes to the profile, you are prompted to integrate those changes into your working environment. Your options are dependent on whether you have unsaved changes of your own. The following scenarios assume that before any changes are made, everyone is working on the latest published version of a profile.

### Scenario 1

* **Scenario**  
You do not have any unsaved changes when a concurrent user saves changes.
* **Result**  
Since you have no unsaved changes, you are prompted to load the new version of the profile.
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-concurrent-users-tiq-concurrent-users-save-and-publish-notification.png)
    Select **Load new version** and then click **OK**.
    When complete, the profile will reload with the newest changes.

### Scenario 2

* **Scenario**  
You have unsaved changes when a concurrent user saves changes and you choose the **Merge the new version into your current work** option.
* **Result**  
You are prompted to merge the changes into your own so that your next save includes both sets of changes.
![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-concurrent-users-tiq-merge-new-version-into-your-current-work.png)
For more information, see: [Merging Versions]().

### Scenario 3

* **Scenario**  
You have unsaved changes when a concurrent user saves changes and you choose the **Continue working and save later** option.
* **Result**  
The next time you save, you are prompted to merge the newer changes into your version or create a separate profile version.  
![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-managing-concurrent-users-tiq-merge-their-changes-with-your-changes.png)  
For more information, see: [Merging Versions]().

### Scenario 4

* **Scenario**  
With the **Lock Profile** setting enabled, you have not made changes when a concurrent user starts making changes.  
**Result**  
You will be notified that another user has begun making changes and you will be prevented from saving until the concurrent user's changes are either saved or discarded.
![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-concurrentuserstiq-concurrent-notification.png)
For more information, see: [Publish Configuration]().

### Scenario 5

* **Scenario**  
You visit the **Save/Publish** screen and find that you cannot save your changes immediately.
* **Result**  
To prevent accidental overwrites of each other's changes, iQ Tag Management prevents concurrent users from saving changes to a profile within one minute of each other. An informational message with a countdown timer indicates that another user has saved less than a minute ago. Once the save completes, other users can save changes.

## Merging Changes

If you choose to merge changes into the profile you're currently working on, you are prompted with the **Merge Changes** dialog, which shows all elements that have been added, changed, or removed, and lets you review the details of each change before choosing to accept them.
For more information, see: [Merging Versions]().
