---
title: Merging changes between concurrent users
description: This article describes how to bring in changes from concurrent users of the same profile version.
url: https://docs.tealium.com/iq-tag-management/save-publish/merging-changes-between-concurrent-users/
---
In a **locked** profile, only one user is allowed to modify a version at any given time. But in the case of an **unlocked** profile, several users are able to make changes in the same version at the same time. In the event that one of them saves or publishes their version first, the remaining concurrent users are alerted to the new change.

In this event, the remaining users have the opportunity to salvage any changes they made in that version before it was overwritten. This is made possible by **Merge Changes**, a feature built into Tealium iQ for resolving concurrent user situations. This feature is automatically invoked the instant it detects a combination of saved and unsaved changes inside the same version. It then allows concurrent users to merge their unsaved changes with the saved changes to keep from losing their efforts.

### How Merge Changes works

In this scenario, User A is editing a certain Version X and overwrites it with **Save/Publish** just when User B is also editing it. Version X now has an update, along with unsaved changes. What can User B do to salvage their changes? There are two options to saving changes:

* **Merge the new version into your current work**: Keeps B&#39;s and A&#39;s changes together in a new version.
* **Continue working and save later**: User B continues to work and can save as a new version later.

![](/images/iq-tag-management/save-publish/concurrent-user-profile-has-been-saved.png)

The **Concurrent Notification** alert message is a cue for you to take action. 

### Merge your changes with another user&#39;s saved changes

To bring concurrent changes into your version:

1. Select the **Merge the new version into your current work** option and then click **OK**
1. In the next window, you are presented a list of the other user&#39;s changes that were saved ahead. Check the items you want to merge into your version. Unchecked items are NOT merged.
    ![](/images/iq-tag-management/their-changes.png)
1. Review the changes in the confirmation window and click **Merge** to complete.
    ![](/images/iq-tag-management/confirm-their-changes.png)  
1. **Save/Publish** to place all the changes into a new version. For more information, see [Save and Publish a Version]().
    ![](/images/iq-tag-management/save-publish/save-publish-merge.png)

Concurrent users will see an alert that announces your new version. If they want to view your new version, they should save their work in progress first.

#### Save your changes without merge

If you decide to keep only your changes and discard the other user&#39;s changes, perform a **Save As** without merging:

1. Select the **Continue working and save later** option and click **OK**.
1. Click **Save/Publish** to save your changes into a new version.

    ![](/images/iq-tag-management/save-publish/save-publish-merge.png)

1. Save your changes as a new version. For more information, see [Save and Publish a Version]().

### Resolve conflicts before merge

Conflicts arise when you to attempt to merge the saved and unsaved instances of the same Tealium iQ element. This is typically the case when the element is modified by several users at the same time. For example, a certain load rule condition with a date range will conflict and collide with same load rule condition without a date range. Merging the two load rules is not possible unless you accept one instance and discard the other.

To resolve a conflict from the **Merge Changes** window:

1. Click the **eye icon** to reveal the conflicting changes.
    ![](/images/iq-tag-management/conflict-their-and-yours.png)  

1. Read the configurations and determine which instance you want to keep.
1. Click the **Use this** bar to move the change you want into the **Accepted Changes** column. Unaccepted changes will be discarded before merging.
    ![](/images/iq-tag-management/accepted-column.png)  

1. Proceed to merge then **Save/Publish** your version.

### Troubleshoot merge issues

The merging operation may fail if you lack required permissions in the account, or when different versions of linked libraries are present in the version. More details are available in the [troubleshooting guide](https://support.tealiumiq.com/en/support/solutions/articles/36000363479-troubleshooting-tips-to-resolve-merging-issues-in-tiq).
